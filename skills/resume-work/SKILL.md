---
name: resume-work
description: Reorient at the start of a session. Use when the user says "resume",
  "where were we", "pick up where we left off", or after a PC restart. Reads the
  handoff note and recent git history, then proposes the next step.
---

# Resume work

1. Read `HANDOFF.md` at repo root if it exists; summarize it in 3-4 lines.
2. Surface rule changes: report the "standing rules / skills updated"
   section from HANDOFF.md, one line each (skip silently if the section
   does not exist). Cross-check for changes made outside a session:
   run `git log --oneline --since="<date from HANDOFF.md>" -- CLAUDE.md
   .claude/` for repo-tracked instruction files, and check whether any
   file under ~/.claude/ (CLAUDE.md, skills/) was modified after the
   handoff date. If something changed that HANDOFF.md does not mention,
   flag it explicitly. Confirm the surfaced rules are in effect for this
   session before proposing next steps.
3. Run `git log --oneline -10` and `git status` to confirm the repo matches the note.
4. If they disagree, trust the repo and say exactly what differs.
5. State the next 1-3 steps from the handoff and start the first one if it is
   unambiguous; otherwise ask which to start.
