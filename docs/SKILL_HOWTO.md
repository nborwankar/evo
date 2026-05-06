# SKILL_HOWTO

Notes on the `discover`, `optimize`, `subagent` SKILL.md prompts under
`plugins/evo/skills/`.

## Hosts and skill prompts

Skills target the generic Agent Skills spec but sometimes need host-specific
behavior. The pattern in every SKILL.md is to phrase steps generically and let
each host map them to its own primitive (e.g. "spawn N subagents in parallel"
→ Claude Code `Agent` with `run_in_background`, Codex `spawn_agent`, etc.).

Host-specific carveouts (notably `evo dispatch`) are documented inline in the
optimize skill and gated by `DISPATCH_HOSTS` in
`plugins/evo/src/evo/core.py`. `claude-code` is the only host in that set
today; every other host falls back to its native parallel-task primitive for
spawning optimization subagents.

## Editing SKILL.md files

The design doc at `tests/skills/README.md` describes a 4-level regression
strategy:

- **Level 0** — static checks (frontmatter parse, line-count cap, reference
  paths exist, no bare `python` / `pytest` / `npm` / `cargo` in command
  examples). Free, deterministic.
- **Level 1** — smoke test (`claude -p` end-to-end against pristine fixtures).
- **Level 2** — behavioral checks (parse stream-json, assert tool-call
  patterns).
- **Level 3** — rubric evaluator (second Claude as judge).

Today only Level 0 is wired up. Levels 1-3 are designed but not implemented.
When editing a skill, run the static checks; for anything riskier, plan to do
a manual dry-run on a fixture under `tests/skills/fixtures/` before merging.

## Substitution gotcha

Claude Code skill substitutions (`${CLAUDE_SKILL_DIR}`, `${CLAUDE_SESSION_ID}`,
`$ARGUMENTS`) are rendered **only when the skill is invoked via slash command
or the Skill tool**, not when raw SKILL.md text is fed to `claude -p` as a
prompt. Test harnesses that read SKILL.md and pass the text to `-p` mode must
pre-substitute or assert on behavior that doesn't depend on substitutions.
