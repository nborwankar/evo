# sdk/node/src/

Source for the Node SDK. Public surface mirrors the Python SDK: `Run`,
`Gate`, `LocalBackend`, `defaultBackend`.

| File | Purpose |
|------|---------|
| `index.js` | Re-exports the public API. |
| `run.js` | `Run` — benchmark reporting context. Per-task `report()` flushes traces; final result written to `EVO_RESULT_PATH`. |
| `gate.js` | `Gate` — safety-check reporting context. Mirrors `Run` for gate scripts (`gate.check(id, {score})`). |
| `backend.js` | `LocalBackend` — file-based backend (uses `node:fs` atomic-write pattern: write to tempfile, `renameSync`). `defaultBackend()` resolves env vars and returns a configured instance. |
