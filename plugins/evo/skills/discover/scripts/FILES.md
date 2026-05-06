# plugins/evo/skills/discover/scripts/

Helpers the agent runs from inside a benchmark worktree during discover.

| File | Purpose |
|------|---------|
| `validate_result.py` | Asserts that a benchmark result file exists, is non-empty, and is a JSON object with a numeric `score` field. Exit 0 = valid; exit 1 with stderr diagnostic = invalid. The agent runs this after producing a baseline result to catch instrumentation mistakes early. |
