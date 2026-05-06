# sdk/node/test/

Node SDK tests using Node's built-in `node:test` runner. Run from
`sdk/node/` with `npm test`.

| File | Purpose |
|------|---------|
| `run.test.js` | Tests for `Run` and `Gate`. Each case allocates a temp dir, exercises the SDK, and asserts the on-disk artefacts match expectations. Mirrors `sdk/python/test/test_run.py` for parity. |
