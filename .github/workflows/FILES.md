# .github/workflows/

GitHub Actions workflow definitions.

| File | Purpose |
|------|---------|
| `ci.yml` | CI on every push/PR. Five jobs: `version-consistency` (runs `scripts/check_versions.py`), `cli-wheel-assets` (builds the plugin wheel on Linux+Windows × Py 3.10–3.14, asserts dashboard `static/` files are inside the wheel, smoke-tests the installed CLI), `sdk-python` (build + run `sdk/python/test/test_run.py` on Py 3.10–3.14), `sdk-node` (`npm test` on Node 18/20/22/24), `unit-tests` (runs `tests/unit/test_core.py` + `test_locking.py` as scripts on Linux+Windows × Py 3.10–3.14). |
| `publish.yml` | Release workflow. Publishes the plugin and SDKs when a release is cut. |
