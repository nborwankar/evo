# DONE

Session-by-session log of completed work on this evo fork.

---

## 2026-05-05 — Fork-local documentation scaffold

First substantive session on the local fork of `evo-hq/evo`. No code changes;
all work was documentation infrastructure to make future Claude Code sessions
productive on this checkout.

### Accomplished

- **Auto-memory** — Saved the project memory `evo fork purpose` so future
  sessions know this checkout is a fork intended for integration with `n2`
  and `n2-research` (sibling repos under `~/Projects/dirs/github/`).
- **`CLAUDE.md`** — Created the project guidance file at the repo root.
  Iterated through several restructurings based on user feedback:
  1. Started with everything inline (architecture, commands, skill notes).
  2. Extracted into `docs/ARCHITECTURE.md`, `docs/HOWTO.md`,
     `docs/SKILL_HOWTO.md` so the always-loaded `CLAUDE.md` stays lean.
  3. Pulled the repo-layout tree back into `CLAUDE.md` (it's an overview, not
     architecture).
  4. Restructured `ARCHITECTURE.md` top-down (10kft → 5kft → 1kft → 500ft →
     ground) so readers can stop at the altitude that answers their question.
  5. Moved the three docs from repo root into `docs/` per the global
     "root = state files only" convention.
- **`FILES.md` per directory** — Wrote 38 `FILES.md` index files, one per
  directory in the tree (skipping `docs/`, `.git/`, and the demo-fixture
  sub-trees `auto_harness_demo/` / `tau3_demo/`). Each is a small markdown
  table listing files/subdirs in that directory with one-line purposes,
  capturing *why* not just *what* where it matters (e.g. why versions live
  in 7 places, why `bin/evo` delegates through `uv`, why `claude_fork.py`
  only exists for one host).
- **`CLAUDE.md` index** — Added a final pointer flagging the
  `<dir>/FILES.md` convention so future sessions know to look for the local
  index before diving into an unfamiliar directory.

### Decisions

- **Naming: `FILES.md`, not `README.md`.** Several directories already have
  user-facing `README.md` files (`plugins/evo/`, `sdk/python/`, `sdk/node/`,
  `tests/skills/`, `scripts/rlm_eval/`); `FILES.md` is purely a navigation
  index and avoids the clash.
- **Documentation in fork, not upstream.** The `CLAUDE.md` / `docs/*` /
  `FILES.md` files are fork-local. Not intended for upstream PR — they
  encode user-specific conventions and the n2/n2-research integration
  framing.

### Housekeeping

- No stale docs to archive (fresh fork; no prior `older_docs/` needed).

### Skipped

- **Portfolio refresh** — latest snapshot in
  `~/Projects/dirs/metaproject/status/` is from 2026-03-26 (~5 weeks old).
  The daily-refresh workflow appears to have drifted, so I did not invoke
  `/portfolio-refresh` autonomously. Run it explicitly when you want it.
