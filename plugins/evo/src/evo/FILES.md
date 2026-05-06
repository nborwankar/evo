# plugins/evo/src/evo/

The Python package implementing the `evo` CLI and dashboard.

| File | Purpose |
|------|---------|
| `__init__.py` | Package init. Defines `__version__` and `DISTRIBUTION_NAME = "evo-hq-cli"` (used by skill checks to distinguish from the unrelated `evo` SLAM tool on PyPI). |
| `cli.py` | argparse entrypoint. Defines every subcommand as `cmd_<name>` (init, host, dispatch, new, run, done, discard, prune, gc, reset, status, tree, frontier, scratchpad, get, path, diff, traces, annotate, annotations, log, set, infra, gate, dashboard). Wired to the `evo` console script in `pyproject.toml`. |
| `core.py` | Workspace primitives. Owns `.evo/` layout (graph.json, config.json, meta.json, run_NNNN/, worktrees/), atomic JSON writes, git operations, host registry (`SUPPORTED_HOSTS`, `DISPATCH_HOSTS`), node/experiment helpers. Every other module imports from here. |
| `locking.py` | `advisory_lock()` context manager built on `portalocker` (cross-platform: fcntl on POSIX, LockFileEx on Windows). All workspace state writes go through this. |
| `frontier_strategies.py` | Frontier picker registry. Single `FRONTIER_STRATEGIES` dict drives the CLI validator, dashboard picker, and `evo frontier` subcommand. Strategies: `argmax`, `top_k`, `epsilon_greedy`, `softmax`, `pareto_per_task`. |
| `dispatch.py` | Explorer-cache infrastructure for `evo dispatch`. Owns the on-disk schema for cached explorer sessions, predicates that decide when a cached explorer can be reused, the EXPLORE-phase prompt template. Subprocess spawning lives in `hosts/`. |
| `dashboard.py` | Flask app for the local dashboard. Serves `static/`, exposes config + graph endpoints, persists chosen port to `.evo/dashboard.port`. Wired to the `evo-dashboard` console script. |
| `scratchpad.py` | Helpers for assembling the scratchpad view (best score, ascii tree, etc.) consumed by `evo scratchpad`. |

| Subdir | Purpose |
|--------|---------|
| `hosts/` | Per-host spawn handlers used by `evo dispatch`. |
| `static/` | Dashboard front-end assets (HTML/JS/CSS), bundled into the wheel. |
