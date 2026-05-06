# plugins/evo/skills/discover/

The `discover` skill — runs once per repo to set evo up and produce a baseline.

| File | Purpose |
|------|---------|
| `SKILL.md` | The discover prompt. Frontmatter declares `name: discover`. Body walks the agent through: version check → ask user for context → propose dimensions → build benchmark in baseline worktree → run baseline → commit. |

| Subdir | Purpose |
|--------|---------|
| `references/` | Long-form material the SKILL.md links into instead of embedding (keeps the SKILL body small). |
| `scripts/` | Helper scripts the agent runs from inside a benchmark worktree (e.g. result validation). |
