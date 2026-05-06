# plugins/evo/src/evo/hosts/

Per-host spawn handlers used by `evo dispatch`. Only hosts with a usable
fork primitive get a handler; everything else falls back to the host's
native parallel-Task tool (handled inside the optimize SKILL.md, not here).

| File | Purpose |
|------|---------|
| `__init__.py` | Module header + `HOST_HANDLERS` registry (`{"claude-code": claude_fork}`). Documents the two-function contract every handler must satisfy: `spawn_explorer(...)` and `spawn_child(...)`. |
| `claude_fork.py` | Claude Code handler. Owns the actual subprocess invocations for `claude -p --resume <SID> --fork-session`, which gets ~99% prefix cache reuse on long forked transcripts. Cache validation, record schema, and prompt rendering live in `evo.dispatch`; this module only does the spawning. |
