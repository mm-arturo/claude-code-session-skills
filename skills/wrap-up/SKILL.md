---
name: wrap-up
description: Prepare the current session for a PC restart or shell close. Use when
  the user says "prepare for restart", "wrap up", "save session", "closing the
  shell", or similar. Commits and pushes work, writes a handoff note, confirms resume.
---

# Session wrap-up

Run these steps in order and report each briefly.

1. Inspect: `git status` and `git diff --stat`. List important untracked files.
2. Guard secrets: never stage `.env`, keys, wallets, or gitignored files. If a
   secret is tracked, STOP and warn instead of committing.
3. Persist lessons: review this session for durable knowledge a future
   session would otherwise re-learn. Candidates:
   - corrections the user made to my behavior or output
   - environment quirks discovered the hard way (commands, flags, paths,
     versions, workarounds)
   - wrong assumptions I had to abandon mid-session
   - workflow or performance optimizations that verifiably worked
   Route each item to the right permanent home:
   - project-specific -> project CLAUDE.md (or .claude/rules/), so it
     ships with the repo
   - applies across all projects -> ~/.claude/CLAUDE.md
   - improves an existing skill's procedure -> edit that SKILL.md directly
   - a genuinely new repeatable workflow -> propose a new skill, but ask
     before creating it
   Quality bar - persist only what is (a) verified this session,
   (b) non-obvious, (c) likely to recur. Write each as one short
   imperative rule, not a story. Check for duplicates first; prefer
   rewriting an existing line over appending a near-duplicate. If nothing
   meets the bar, say so and skip.
   Finish by listing exactly what was written to which file, so the user
   can veto before commit.
4. Commit: stage meaningful changes with a descriptive message summarizing this
   session. Prefix `wip:` if work is unfinished. If tests are fast, run them and
   note the result.
5. Push the current branch (`git push -u origin <branch>` if no upstream).
6. Create or update `HANDOFF.md` at repo root with today's date:
   - completed this session
   - in progress, and exactly where it stopped (file/function)
   - next 1-3 concrete steps
   - known issues / failing tests / open questions
   - commands to resume (venv activation, env vars, services)
   - standing rules / skills updated this session: one line per change with
     the file and the rule (copied from the persist-lessons step; write
     "none" if nothing was persisted)
7. Confirm: print commit hash + branch, and remind that `claude --continue`
   resumes this session after restart.
