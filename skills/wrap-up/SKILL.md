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
   Route each item to the FIRST home in this list that fits. The
   always-loaded files come last on purpose: every character in them is
   paid for in every session, and long files are followed less well.
   a. The skill that runs that work (a deploy, a release, a site, an API,
      a pipeline step): edit that SKILL.md. This is the default.
   b. A rule skill (for example `~/.claude/skills/rules-<topic>/SKILL.md`,
      or a project rule skill) when the lesson is a trap of a tool or a
      platform that can bite in more than one workflow. Give it a
      description that names the moments it must be loaded.
   c. Memory (`~/.claude/projects/<project>/memory/`) for the user's
      preferences and rulings, facts about accounts and services, and the
      state of work in flight. One topic per file; update the existing
      file before creating a new one.
   d. HANDOFF.md for anything that is only true today (what is running,
      what waits, this session's ids).
   e. A genuinely new repeatable workflow -> propose a new skill, and ask
      before creating it.
   f. An always-loaded file (`~/.claude/CLAUDE.md`, the project CLAUDE.md
      or AGENTS.md) ONLY when the item passes one of two tests: it is a
      hard safety line, or most sessions in that scope would hit it with
      no earlier moment to load a skill. Then it is written twice: the
      full lesson (case, date, evidence) in its home from a-c, and ONE
      imperative line of at most 200 characters in the always-loaded
      file, ending with the name of that home.
   Quality bar - persist only what is (a) verified this session,
   (b) non-obvious, (c) likely to recur. Check for a duplicate first: grep
   the skills, memory and the CLAUDE.md files for its key words, and
   rewrite the existing line instead of adding a second one. A date, an
   incident story, a file count or an id never goes into an always-loaded
   file: it goes in the home from a-c. If nothing meets the bar, say so
   and skip.
   Retire - nothing is deleted, it is moved. For every always-loaded line
   this session proved stale (a status such as "queued" or "pending", a
   default that changed, a script or account fact that is no longer true):
   correct the line, and move the old text to the history part of its
   skill or memory file.
   Memory - for each memory file this session touched or finished: bring
   its `description` up to date, and keep its MEMORY.md line a hook of at
   most 150 characters with no status, ids or dates of state (Claude Code
   loads only the first 200 lines or 25 KB of MEMORY.md). Propose a
   finished file for archive only when every lesson in it is named as
   living in a skill, a CLAUDE.md or another memory; list such proposals
   for the user and never archive unasked.
   Measure - after writing, count the characters of `~/.claude/CLAUDE.md`,
   the project CLAUDE.md or AGENTS.md, and MEMORY.md (for example
   `(Get-Content -Raw -Encoding UTF8 <file>).Length` or `wc -m <file>`).
   Set a target per file and treat it as a target, not a ceiling: about
   20,000 for the global file and 25,000 for a project file is a
   reasonable start. A file that ends the session larger than it started
   needs a reason in the report. A file over its target has its incident
   detail (stories, dates, evidence) moved to its home from a-c without
   asking, keeping each one-line rule in place. Moving or removing a
   one-line rule, a user ruling or a safety line out of an always-loaded
   file needs the user's yes: list such proposals in the report. Never
   delete knowledge to save space; move it, and confirm the moved text is
   in its new home word for word. Do not wait for Claude Code's startup
   warning about instruction-file size.
   Finish by listing what was written, moved or retired, file by file,
   with the before and after character counts of the always-loaded files.
4. Write `HANDOFF.md` at repo root: today's entry goes at the TOP, and the
   file keeps only the three newest entries. Move older entries,
   unchanged, to `docs/handoffs/HANDOFF-<yyyy-mm>.md` (or `handoffs/` when
   the repo has no `docs/`). Today's entry:
   - completed this session
   - in progress, and exactly where it stopped (file/function)
   - next 1-3 concrete steps
   - known issues / failing tests / open questions
   - commands to resume (venv activation, env vars, services)
   - standing rules / skills updated this session: one line per change
     with the file and the rule (from step 3; write "none" if nothing was
     persisted), and the character counts from the Measure step
5. Commit: stage meaningful changes with a descriptive message summarizing
   this session. Prefix `wip:` if work is unfinished. Commit moves of rules
   between instruction files as their own commit, so one revert undoes
   them. If tests are fast, run them and note the result.
6. Push the current branch (`git push -u origin <branch>` if no upstream).
7. Confirm: print commit hash + branch, and remind that `claude --continue`
   resumes this session after restart.
