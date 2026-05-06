# plugins/evo/

The plugin package. Houses the `evo-hq-cli` Python source, the `discover` /
`optimize` / `subagent` skill prompts, host marketplace manifests, and the
plugin-internal pytest suite.

| File | Purpose |
|------|---------|
| `pyproject.toml` | Python build config for the `evo-hq-cli` package. Pins `flask`, `portalocker`, `pyyaml`. Declares the `evo` and `evo-dashboard` console scripts. |
| `README.md` | Plugin-internal README (currently a stub; user-facing docs live in the repo-root `README.md`). |
| `LICENSE`, `NOTICE` | Apache 2.0 license + NOTICE, duplicated here so wheels ship with their own license metadata. |
| `uv.lock` | `uv`-managed lockfile for the plugin's Python deps. Regenerated with `uv lock`. |

| Subdir | Purpose |
|--------|---------|
| `bin/` | Bash wrappers (`evo`, `evo-version-check`) added to the host's PATH. |
| `src/evo/` | Python package implementing the CLI. |
| `skills/` | `SKILL.md` prompts for `discover`, `optimize`, `subagent`. |
| `tests/` | Plugin-internal pytest suite. |
| `.claude-plugin/` | Claude Code plugin manifest. |
| `.codex-plugin/` | Codex plugin manifest. |
