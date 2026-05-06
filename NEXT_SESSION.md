# NEXT_SESSION

Handoff for the next Claude Code session on this evo fork.

---

## Where we are (as of 2026-05-05)

**Repo:** `~/Projects/dirs/github/evo` — local fork of `evo-hq/evo`, branch
`main` clean and tracking `origin/main`. Last upstream merge:
`e2dc7c4 Merge pull request #33 from evo-hq/v0.3.3` (release 0.3.3).

**State of this fork:**
- No code changes from upstream.
- Fork-local documentation scaffold added this session: `CLAUDE.md`,
  `docs/{ARCHITECTURE,HOWTO,SKILL_HOWTO}.md`, plus 38 per-directory
  `FILES.md` index files. All committed.

**Auto-memory:** `evo fork purpose` → checkout exists for integration with
`n2` and `n2-research`.

## What to do next (open question for you)

The fork has documentation but no integration code yet. Concrete next steps
depend on what you actually want from evo in the n2 / n2-research context.
A few plausible starting points — pick one or define your own:

1. **Survey the consumers.** Before touching evo, look at how `n2` and
   `n2-research` would invoke an iterative-experiment loop. Run
   `aishell pfind n2` / `aishell pfind n2-research` to confirm paths, then
   read their CLAUDE.md / README / current entry points to identify what
   "an experiment" means in each context (a model checkpoint? a scoring
   script? a config sweep?). Outcome: a one-page "integration target"
   note in `docs/`.

2. **Run discover end-to-end on a toy n2 problem.** Pick a small slice of
   `n2` that has a measurable score, install the plugin against this fork
   (`/plugin marketplace add evo-hq/evo` if not already, or use the local
   `.claude-plugin/marketplace.json`), invoke `/evo:discover`, see what
   evo proposes. Outcome: a sense of what evo's current heuristics make of
   an n2 codebase, captured in a session note.

3. **Identify upstream divergence points.** If integration will require
   evo changes (new frontier strategy? n2-specific gate type? config-sweep
   support?), enumerate them as proposed-divergence notes in `docs/` so
   you can decide later which become upstream PRs and which stay fork-local.

## Quick commands

```bash
cd ~/Projects/dirs/github/evo

# Verify the CLI works in this checkout
uv run --project plugins/evo evo --version       # → evo-hq-cli 0.3.3

# Run unit tests
python tests/unit/test_core.py
python tests/unit/test_locking.py

# Plugin pytest suite
cd plugins/evo && uv run --with pytest pytest tests/

# Find sibling repos
aishell pfind n2
aishell pfind n2-research
```

See `docs/HOWTO.md` for the full command reference.

## Resume command

> "Resume evo fork — read NEXT_SESSION.md and DONE.md for context, then
> let's pick one of the three next-step options or define a new one."

## Open questions

- Which n2 / n2-research surface is the first integration target?
- Will integration changes go upstream, or stay fork-local?
- Is `/portfolio-refresh` still part of your weekly workflow? (Skipped this
  session — last snapshot is from 2026-03-26.)
