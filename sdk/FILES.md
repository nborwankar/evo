# sdk/

Reporting SDKs for benchmarks that want to talk to evo. Both are
zero-dependency packages that auto-read `EVO_TRACES_DIR`,
`EVO_EXPERIMENT_ID`, and `EVO_RESULT_PATH` from the environment.

| Subdir | Purpose |
|--------|---------|
| `python/` | `evo-hq-agent` — Python 3.10+ SDK. Imports as `evo_agent`. Exposes `Run`, `Gate`, `LocalBackend`. |
| `node/` | `@evo-hq/evo-agent` — Node 18+ SDK. Same surface in JS. |

Both are versioned in lockstep with the plugin — see
`docs/ARCHITECTURE.md` § Versioning.
