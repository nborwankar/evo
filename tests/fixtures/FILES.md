# tests/fixtures/

Demo benchmark fixtures used for manual dev runs and exploratory testing.
Each is a self-contained mini-project with an `agent/`, a `benchmark.py`,
a `gate.py`, and its own README.

| Subdir | Purpose |
|--------|---------|
| `auto_harness_demo/` | Minimal demo benchmark exercising the auto-harness path (no SDK required — uses inline instrumentation). Contains `agent/`, `benchmark.py`, `gate.py`, `README.md`. |
| `tau3_demo/` | Larger demo benchmark with a `config.json`, used for end-to-end exercises that need a richer configuration surface. Contains `agent/`, `benchmark.py`, `gate.py`, `config.json`, `README.md`. |
