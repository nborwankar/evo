# tests/skills/

Skill-regression test design + (future) implementation. The actual harness
isn't fully wired up yet — see `README.md` for the four-level strategy and
current status.

| File | Purpose |
|------|---------|
| `README.md` | Design doc for skill regression testing. Covers Level 0 static checks (free, every push), Level 1 smoke tests (~$1-2 per skill, PR-only), Level 2 behavioral checks, Level 3 LLM-judge rubrics. As of writing only Level 0 is implemented. |

| Subdir | Purpose |
|--------|---------|
| `fixtures/` | Frozen pristine repos used as inputs for skill smoke tests. |
