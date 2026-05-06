# Architecture

(Repo layout overview lives in `CLAUDE.md`.)

This document zooms in progressively: a one-paragraph summary, then the
plugin's shape, then the loop, then the state model, then the components.
Stop reading at the altitude that answers your question.

---

## 10,000 ft — what evo does

You point evo at a codebase. It figures out what to measure, runs a baseline,
then loops: try something, score it, keep it if it improved, throw it away if
not. Repeat until it stops finding wins.

---

## 5,000 ft — the plugin shape

evo is **not** a standalone tool. It's a plugin for AI coding agents (Claude
Code, Codex, OpenClaw, Hermes). It rides on the agent's ability to read code,
edit files, and spawn subagents. Two artefacts ship together:

1. **CLI** (`evo-hq-cli`) — owns state: the experiment tree, git worktrees,
   the dashboard. The agent shells out to it.
2. **Skills** (`discover`, `optimize`, `subagent`) — natural-language SKILL.md
   prompts the agent reads to choreograph the loop.

The agent does the thinking. The CLI does the bookkeeping. Neither calls into
the other's domain.

```
┌──────────────────────────────────────────────────────────────────┐
│  Orchestrator agent  (running inside Claude Code / Codex / ...)  │
│  Reads SKILL.md ─►  shells out to `evo` CLI  ─►  spawns subagents │
└────────────────────┬─────────────────────────────┬───────────────┘
                     │ reads/writes               │ each subagent runs in
                     ▼                            ▼ its own git worktree
              ┌─────────────┐              ┌──────────────────┐
              │  .evo/      │              │ worktrees/exp_* │
              │  graph.json │              │   <experiment>   │
              │  config     │              └────────┬─────────┘
              │  scratchpad │                       │ commits/discards
              │  run_NNNN/  │◄──────────────────────┘
              └─────────────┘
                     ▲
                     │ HTTP polls
              ┌──────┴──────┐
              │  Dashboard  │  Flask app, served from src/evo/static/
              │  :8080      │  (assets must ship in the wheel — CI checks)
              └─────────────┘
```

---

## 1,000 ft — the loop

Two phases:

**Discover** — agent explores the repo, decides what's worth optimizing,
builds an evaluation, runs a baseline. One-shot.

**Optimize** — repeats until it stalls:

```
Each round:
  1. Read state + traces
  2. Fan out RLM-inspired scan sub-agents to find cross-cutting failure patterns
  3. Write one structured brief per subagent
       (objective + parent + boundaries + pointer traces)
  4. Spawn N subagents in parallel, each on its own branch
       claude-code → `evo dispatch run --background` (fork-cache)
       other hosts → host's parallel-Task primitive
     Each subagent has a `budget` (max iterations on its branch).
  5. Each subagent: read brief, edit target, run benchmark, evo done/discard,
     iterate if budget remains.
  6. Collect results, prune dead branches, pick frontier for next round.
  7. Stop after `stall` consecutive rounds with no improvement.
```

This is **tree search**, not a single hill climb — multiple branches stay
live, scored, and prunable. Subagents commit through `evo done <id> --score N`
(passes gate → committed) or `evo discard <id>` (fails → worktree torn down).
Main branch never receives commits during optimize.

---

## 500 ft — state model

All workspace state lives under `.evo/`:

- `graph.json` — experiment tree (nodes = experiments, edges = parent links)
- `config.json` — host, frontier strategy, run config
- `meta.json` — active run, next run id, host signature
- `annotations.json`, `infra_log.json`, `notes.md`, `scratchpad.md`
- `run_NNNN/` — per-round artifacts (per-experiment logs, traces, outcomes)
- `worktrees/exp_*` — git worktrees, one per live experiment

Subagents work in worktrees so `main` is never touched during optimize. A
successful experiment commits to *its* branch and stays in the tree as a
possible parent for future branches. The dashboard is a Flask app that polls
`.evo/` over HTTP.

Concurrent subagents writing the graph is real, so **all state writes go
through `core.atomic_write_json` + `locking.advisory_lock`** (portalocker,
cross-platform). Bypass that and you'll race-clobber the tree.

---

## Ground level — components

### CLI surface

`plugins/evo/src/evo/cli.py` defines all subcommands as `cmd_<name>`:

```
init  host  dispatch  new  run  done  discard  prune  gc  reset
status  tree  frontier  scratchpad  get  path  diff  traces
annotate  annotations  log  set  infra  gate  dashboard
```

Two are notable:

- `evo dispatch` — explorer-cache spawn for parallel subagents. **Only
  supported on `claude-code` host** (KV-cache prefix reuse via fork). On every
  other host it exits 2; the optimize skill falls back to the host's native
  parallel-Task tool. See `dispatch.py` and `hosts/claude_fork.py`.
- `evo frontier` — returns ranked frontier nodes per the active strategy
  (`argmax`, `top_k`, `epsilon_greedy`, `softmax`, `pareto_per_task`).
  Strategies live in `frontier_strategies.py` with a single
  `FRONTIER_STRATEGIES` registry — adding a strategy means one registry entry
  + one picker function.

### Versioning

The version string lives in **7 places**, all asserted equal by
`scripts/check_versions.py` (CI-gated):

```
plugins/evo/pyproject.toml                    [project] version
plugins/evo/src/evo/__init__.py               __version__
plugins/evo/.claude-plugin/plugin.json        version
plugins/evo/.codex-plugin/plugin.json         version
sdk/python/pyproject.toml                     [project] version
sdk/python/src/evo_agent/__init__.py          __version__
sdk/node/package.json                         version
```

Why all of them: hosts refetch the **plugin manifest** on version bump but do
**not** reinstall the CLI on PATH. Drift = silent skill breakage. The
`evo-version-check` shim in `bin/` is the runtime guard the skills run before
doing anything else.
