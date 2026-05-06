# sdk/python/

The `evo-hq-agent` Python SDK. Zero dependencies, Python 3.10+.

| File | Purpose |
|------|---------|
| `pyproject.toml` | Build config for the `evo-hq-agent` package. Version must match the CLI. |
| `README.md` | User-facing SDK docs (install + usage). |
| `LICENSE` | Apache 2.0 license — duplicated so the wheel ships with its own. |

| Subdir | Purpose |
|--------|---------|
| `src/evo_agent/` | Source: `_run.py`, `_gate.py`, `_backend.py`, public exports in `__init__.py`. |
| `test/` | Test suite — runnable as `python3 sdk/python/test/test_run.py`. |
