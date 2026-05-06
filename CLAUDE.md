# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Local context

This checkout is a fork of `evo-hq/evo` kept locally for integration with `n2`
and `n2-research` (sibling repos under `~/Projects/dirs/github/`). Treat those
two as the primary downstream consumers when making design choices; verify
their paths with `aishell pfind n2` / `aishell pfind n2-research` before
referencing them.

## Repo layout

```
evo/
├── plugins/evo/         # The plugin: CLI source + skill prompts + manifests
│   ├── src/evo/         #   Python package `evo` — the `evo-hq-cli` binary
│   ├── skills/          #   discover/, optimize/, subagent/ SKILL.md files
│   ├── bin/             #   `evo` and `evo-version-check` shell wrappers
│   ├── .claude-plugin/  #   plugin.json (Claude Code marketplace manifest)
│   ├── .codex-plugin/   #   plugin.json (Codex marketplace manifest)
│   └── tests/           #   Plugin-internal pytest suite
├── sdk/python/          # `evo-hq-agent` — zero-dep reporting SDK
├── sdk/node/            # `@evo-hq/evo-agent` — zero-dep reporting SDK
├── scripts/             # Maintenance helpers (check_versions, dashboard, rlm_eval)
└── tests/
    ├── unit/            # test_core.py, test_locking.py — run as scripts
    ├── skills/          # Design doc + fixtures for skill regression (mostly TODO)
    ├── fixtures/        # auto_harness_demo, tau3_demo
    └── e2e.py           # End-to-end harness driving `uv run evo ...`
```

## Where to look

Load these on demand, not by default — keep CLAUDE.md lean:

- **`docs/ARCHITECTURE.md`** — top-down: 10kft summary → plugin shape → loop
  → state model → component-level detail (CLI surface, frontier strategies,
  versioning). Read when making design decisions or touching the experiment
  graph, CLI subcommands, frontier strategies, or release plumbing.
- **`docs/HOWTO.md`** — common dev commands: running the CLI, tests
  (incl. single-test invocation), SDK tests, build, version-consistency check.
  Read when you need to run something.
- **`docs/SKILL_HOWTO.md`** — host conventions, the 4-level skill regression
  design, the `${CLAUDE_SKILL_DIR}` substitution gotcha. Read when editing
  anything under `plugins/evo/skills/`.
- **`README.md`** — user-facing install + usage for the plugin itself.
- **`<dir>/FILES.md`** — every directory (except `docs/` and demo-fixture
  sub-trees) carries a `FILES.md` listing each file/subdir in that directory
  with a one-line purpose. Read the relevant one before exploring or editing
  inside an unfamiliar directory.
