# plugins/evo/skills/

The natural-language skill prompts the orchestrator agent reads. One subdir
per skill.

| Subdir | Purpose |
|--------|---------|
| `discover/` | Initial setup: explore the repo, propose what to optimize, build the benchmark, run the baseline. |
| `optimize/` | The optimization loop — orchestrator + parallel subagents, runs until interrupted or stalled. |
| `subagent/` | Brief-execution protocol every optimize subagent reads when it starts. |

When editing any `SKILL.md`, see `docs/SKILL_HOWTO.md` for host conventions
and the static-check rules CI enforces.
