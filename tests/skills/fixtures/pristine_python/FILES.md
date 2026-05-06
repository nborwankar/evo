# tests/skills/fixtures/pristine_python/

Frozen pristine Python repo used as a fixture for skill smoke tests. Has no
existing benchmark, so it forces the discover skill down the
"construct-from-scratch" path.

Treat the contents as opaque test data — they were captured from a real
dry-run of `feat/discover-rewrite` and represent a realistic small project
the agent might be asked to instrument.

| Entry | Purpose |
|-------|---------|
| `README.md` | Project description as the agent will see it. |
| `agent/` | Tiny agent under test (`solve.py`). |
| `data/` | Problem set the agent is scored on (`problems.jsonl`). |
| `tests/` | The project's own tests (`test_solve.py`). |
