# scripts/rlm_eval/

Evaluation harness that measures whether evo's `optimize` skill actually
helps an orchestrator find cross-cutting patterns in an experiment tree.
Named after the Recursive Language Model paper (arXiv:2512.24601) that
seeded the design. See `README.md` for the full design.

Pairs trials of two skill versions: **V** (vanilla baseline) vs **R**
(current). Each trial runs `claude -p` against a synthetic `.evo/` tree
with six planted patterns and is scored both strictly and by an LLM judge.

| File | Purpose |
|------|---------|
| `README.md` | Full design + workflow doc. Read this first. |
| `rlm_eval.py` | The CLI: subcommands `check`, `setup`, `trial`, `matrix`, `score`, `clean`. Cross-platform (sandbox is weaker on Windows). |
| `generate_fixture.py` | Builds the synthetic `.evo/` tree. One batched LLM call per case produces N narrative objects; procedural assembly turns them into outcome.json + 20 task traces per experiment. |
| `score.py` | Strict scorer. Credits a reported pattern only if its keywords overlap a planted signature **and** Jaccard(reported_ids, planted_ids) ≥ 0.6. |
| `score_llm.py` | LLM judge that rates each reported pattern with a 0/1/2 rubric and records `planted_recall` per planted pattern (A/B/C/D/E/S). Catches legitimate analytical observations the strict scorer would mark as hallucinations. |
| `baseline_SKILL.md` | Frozen pre-RLM SKILL.md used as the V-arm baseline. Do not edit; replace only when intentionally re-baselining. |
