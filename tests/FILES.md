# tests/

Repo-level tests. Distinct from `plugins/evo/tests/` (the plugin's internal
suite) — these live here so they can exercise cross-cutting behaviour and
hold shared fixtures.

| File | Purpose |
|------|---------|
| `e2e.py` | End-to-end harness that drives `uv run --project plugins/evo evo ...` against a freshly-initialised git repo in tmpdir. Helper functions: `run`, `evo`, `write`, `init_repo`. Used as a building block for ad-hoc end-to-end checks. |

| Subdir | Purpose |
|--------|---------|
| `unit/` | Unit tests for `evo.core` and `evo.locking`. CI runs them as scripts (`python tests/unit/test_*.py`). |
| `skills/` | Design + (future) implementation of skill-regression tests. See `tests/skills/README.md`. |
| `fixtures/` | Demo benchmark fixtures (`auto_harness_demo`, `tau3_demo`) used by manual dev runs. |
