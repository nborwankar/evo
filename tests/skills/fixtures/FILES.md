# tests/skills/fixtures/

Frozen pristine fixtures used by skill smoke tests. Each fixture is a tiny
repo with no existing benchmark — it forces the discover skill down the
"construct from scratch" path.

| Subdir | Purpose |
|--------|---------|
| `pristine_python/` | Minimal Python project: an `agent/solve.py`, a `data/problems.jsonl`, a `tests/` directory, and a README. No `.evo/` — fresh slate for `discover` to instrument. |
