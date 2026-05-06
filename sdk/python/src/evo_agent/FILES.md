# sdk/python/src/evo_agent/

The `evo_agent` package. Public surface: `Run`, `Gate`, `Backend`,
`LocalBackend`. Internal modules use a leading underscore.

| File | Purpose |
|------|---------|
| `__init__.py` | Re-exports the public API and pins `__version__`. |
| `_run.py` | `Run` — benchmark reporting context. Wraps a benchmark call so per-task traces flush on each `report()` (lets the dashboard stream progress live) and the final result is written atomically to `EVO_RESULT_PATH`. |
| `_gate.py` | `Gate` — safety-check reporting context. Mirrors `Run` for gate scripts; surfaces pass/fail to evo's gate machinery. |
| `_backend.py` | `Backend` protocol + `LocalBackend` file-based implementation. Where traces and results actually get written. `default_backend()` resolves env vars and returns a configured instance. |
