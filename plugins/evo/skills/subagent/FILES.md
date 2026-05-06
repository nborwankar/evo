# plugins/evo/skills/subagent/

The `subagent` skill — protocol every optimize subagent reads when it starts
work on its brief.

| File | Purpose |
|------|---------|
| `SKILL.md` | The subagent prompt. Tells the spawned agent how to read its brief + pointer traces, form a concrete edit, run the benchmark, call `evo done` / `evo discard`, and (if budget remains) iterate within its branch. |
