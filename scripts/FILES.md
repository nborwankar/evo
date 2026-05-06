# scripts/

Repo-level maintenance scripts and dev shims. Distinct from
`plugins/evo/bin/` — those wrappers ship with the plugin; these are for
people working on evo itself.

| File | Purpose |
|------|---------|
| `check_versions.py` | Asserts the version string matches across all 7 sources (plugin pyproject + `__init__.py`, both plugin manifests, both SDK pyproject + `__init__.py`, Node `package.json`). CI-gated; run locally before bumping. |
| `evo` | One-line shim that calls `evo.cli.main()`. For dev use when running directly from a checkout without going through the plugin's `bin/` wrapper. |
| `dashboard.py` | One-line shim that calls `evo.dashboard.main()`. |
| `graph.py` | One-line shim that runs `evo.cli.main(["tree"])` — i.e. quick `evo tree` invocation. |
| `scratchpad.py` | One-line shim that runs `evo.cli.main(["scratchpad"])`. |

| Subdir | Purpose |
|--------|---------|
| `rlm_eval/` | Evaluation harness that measures whether the optimize skill actually helps an orchestrator find cross-cutting failure patterns. Has its own README. |
