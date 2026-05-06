# plugins/evo/bin/

Shell wrappers placed on the host's PATH when the plugin is enabled.

| File | Purpose |
|------|---------|
| `evo` | Bash wrapper that delegates to `uv run --project <plugin-root> evo "$@"`. Ensures the CLI resolves against the plugin's pinned deps regardless of which project the user is currently in. Errors out with install instructions if `uv` isn't on PATH. |
| `evo-version-check` | Bash wrapper that asserts the installed `evo-hq-cli` version matches the plugin manifest version. Skills run this as their first step (exit 0 OK, 1 mismatch with diagnostic, 2 environment error). Prevents silent skill breakage when the host refetches a new plugin manifest but the user hasn't reinstalled the CLI. |
