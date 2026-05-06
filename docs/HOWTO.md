# HOWTO

Common commands for working in this repo. All Python work goes through `uv`
(no `pip install` step needed). Always run the CLI via the project root so
the plugin's pinned deps resolve.

## CLI

```bash
uv run --project plugins/evo evo --version       # → evo-hq-cli 0.3.3
uv run --project plugins/evo evo --help

# Start the dashboard (auto-increments port if 8080 busy)
uv run --project plugins/evo evo dashboard --port 8080
```

## Tests

```bash
# Plugin unit tests (these are scripts, not pytest discovery)
python tests/unit/test_core.py
python tests/unit/test_locking.py

# Plugin's internal pytest suite
cd plugins/evo && uv run --with pytest pytest tests/
cd plugins/evo && uv run --with pytest pytest tests/test_dispatch.py::test_specific_case  # single test

# SDKs
cd sdk/python && uv run --with pytest pytest test/
cd sdk/node   && npm test
```

CI runs the unit tests on Python 3.10–3.14 and Node 18/20/22/24. There is no
lint step.

## Release / version checks

```bash
# Asserts versions match across all 7 sources (see ARCHITECTURE.md)
python3 scripts/check_versions.py

# Build wheels — mirrors what CI does
cd plugins/evo && python -m build
cd sdk/python  && python -m build
```
