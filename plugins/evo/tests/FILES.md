# plugins/evo/tests/

Plugin-internal pytest suite. Run from `plugins/evo/`:

```
uv run --with pytest pytest tests/
```

| File | Purpose |
|------|---------|
| `test_dashboard_frontier_strategy.py` | End-to-end test of the dashboard → config → picker chain. POSTs a strategy change to the dashboard API, asserts it persists to `config.json`, asserts the next `evo frontier` call reads the new strategy. Needs Flask. |
| `test_dispatch.py` | Tier-1 tests for `evo.dispatch`: pure logic + orchestration error paths. No mocks — workspaces are real (`git init` in tmpdir + `evo.init_workspace`); subprocesses for the pid-liveness state machine are real `python -c "..."` processes. Live-claude tests are gated separately by `EVO_LIVE_TEST_CLAUDE=1`. |
| `test_frontier_strategies.py` | Unit tests for each strategy's picker function and the `FRONTIER_STRATEGIES` registry validation. |
| `test_inline_instrumentation.py` | Tests the `inline_instrumentation.py` reference helper. Each case runs a small driver script in a subprocess (the helper has module-global state, so it can't be re-imported cleanly in-process). |
| `test_load_result.py` | Unit tests for `evo.core.load_result` and `parse_score` — the entry points that turn a benchmark result file into a numeric score. |
