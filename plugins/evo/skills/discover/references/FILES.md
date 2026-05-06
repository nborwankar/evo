# plugins/evo/skills/discover/references/

Long-form material the discover SKILL.md links into. Kept out of the main
prompt to stay under the SKILL.md line-count cap.

| File | Purpose |
|------|---------|
| `proposing-dimensions.md` | Guidance for proposing unexplored optimization dimensions when the right benchmark isn't obvious. Where to look, what counts as "already measured". |
| `constructing-benchmark.md` | How to build a benchmark from scratch when no existing eval covers the chosen dimension. Designing the scoring function, assembling test cases. All work happens in the baseline worktree, not main. |
| `inline_instrumentation.py` | Drop-in Python instrumentation snippet for benchmarks that don't want the SDK. Reads `EVO_TRACES_DIR` / `EVO_EXPERIMENT_ID` / `EVO_RESULT_PATH` from env, exposes `log_task()` + `write_result()`. |
| `inline_instrumentation.js` | Node equivalent of the Python helper above. Same env contract. |
| `sdk_python.py` | Reference usage example for the `evo-hq-agent` Python SDK (`Run`, `Gate`). |
| `sdk_node.js` | Reference usage example for the `@evo-hq/evo-agent` Node SDK. |
