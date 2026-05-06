# plugins/evo/skills/optimize/

The `optimize` skill — runs the round-by-round optimization loop.

| File | Purpose |
|------|---------|
| `SKILL.md` | The optimize prompt. Per round: read state → fan out RLM-style scan sub-agents → write per-subagent briefs → spawn N subagents in parallel (claude-code via `evo dispatch`, others via host's parallel-Task tool) → collect results → prune + pick frontier → repeat until `stall` rounds without improvement. |
