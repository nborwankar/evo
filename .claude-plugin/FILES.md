# .claude-plugin/ (repo root)

Top-level Claude Code marketplace manifest. **Distinct from**
`plugins/evo/.claude-plugin/` — that one is the *plugin*'s manifest; this one
is the *marketplace*'s manifest.

| File | Purpose |
|------|---------|
| `marketplace.json` | Declares the marketplace name (`evo-hq-evo`) and lists the plugin source path (`./plugins/evo`). Resolved when a user runs `/plugin marketplace add evo-hq/evo` in Claude Code. |
