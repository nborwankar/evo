# tests/unit/

Unit tests run by CI as plain scripts (no pytest discovery). The `if
__name__ == "__main__"` blocks invoke the cases.

| File | Purpose |
|------|---------|
| `test_core.py` | Unit tests for `evo.core` — workspace init, graph load/save, atomic-write helpers, host registry. |
| `test_locking.py` | Unit tests for `evo.locking.advisory_lock` — exclusive acquisition, timeout behaviour, cross-platform via portalocker. |
