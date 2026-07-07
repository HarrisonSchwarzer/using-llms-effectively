---
name: load-repo
description: Load this repo's core context by reading README.md, SPEC.md, and any local notes in .local/. Use at the start of a session or after /clear to get oriented before working on the deck.
---

Read the following at the repo root to load the project context:

1. `README.md` — project overview, how the deck is built and published
2. `SPEC.md` — the spec for the deck's content and structure
3. `.local/` — untracked local notes for local work (start with `.local/notes.md`, then any other files in the folder)

Read them in full. If `SPEC.md` does not exist yet, say so rather than erroring, and continue with what README.md provides. If `.local/` is missing or empty, skip it without comment.

The `.local/` folder is gitignored on purpose: treat its contents as personal working notes — follow the preferences recorded there, and never commit them or copy their contents into tracked files.

After reading, give the user a two-sentence summary of the project state so they can confirm you're oriented, then wait for their task.
