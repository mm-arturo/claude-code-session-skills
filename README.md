# claude-code-session-skills

Two [Claude Code](https://claude.com/claude-code) skills that are really two halves of one thing:
**context does not survive a restart, so write it down before it dies.**

A skill is a folder with a `SKILL.md` in it. Claude reads the front matter, decides when the
skill applies, and follows the procedure inside. No plugin, no build step, no dependencies.

| Skill | What it does |
|---|---|
| [**wrap-up**](skills/wrap-up) | Close a session cleanly: commit, push, persist what you learned into the right permanent file, write a `HANDOFF.md`. |
| [**resume-work**](skills/resume-work) | Open a session cleanly: read the handoff, cross-check it against git, surface rule changes, start the next step. |

## Install

Copy the folders into your skills directory.

**All projects** — `~/.claude/skills/` (Windows: `C:\Users\<you>\.claude\skills\`):

```bash
git clone https://github.com/mm-arturo/claude-code-session-skills.git
cp -r claude-code-session-skills/skills/* ~/.claude/skills/
```

```powershell
git clone https://github.com/mm-arturo/claude-code-session-skills.git
Copy-Item -Recurse claude-code-session-skills\skills\* "$env:USERPROFILE\.claude\skills\"
```

**One project only** — put them in `<repo>/.claude/skills/` instead, and they ship with the repo
for everyone on the team.

Restart Claude Code, then check with `/skills`. Invoke one by name (`/wrap-up`, `/resume-work`)
or just describe what you want — the `description` in the front matter is what Claude matches
against, which is why each one is written as a list of the phrases people actually type.

## How the pair works

At the end of a session `wrap-up` does not only commit. It asks what this session taught you
that a future session would otherwise re-learn the hard way — a flag that does not work on
Windows, an assumption you had to abandon, a workaround that cost an hour — and routes each item
to a permanent home. The skill that runs that work comes first, then a rule skill, memory or the
handoff; the always-loaded `CLAUDE.md` files come last and get only one short line that points
to the full lesson. Every character in them is paid for in every session.

It also keeps those files from growing back. It corrects stale lines instead of adding new ones,
measures each always-loaded file before and after, and moves stories and dates out to the skill
that owns them. It never deletes knowledge to save space, and a one-line rule leaves `CLAUDE.md`
only with your yes. It lists what it wrote, moved or retired, with the sizes, so you can veto
before it commits.

At the start of the next session `resume-work` reads `HANDOFF.md`, then checks it against
`git log` and `git status` — and **trusts the repo when they disagree**, saying exactly what
differs. It also surfaces rule changes made outside the last session, so you find out that a
standing instruction moved before you act on the old one.

Run them for a couple of weeks and the handoff note stops being a chore and starts being the
thing you read first.

## Writing your own

Two things matter more than the rest.

**The description is the trigger.** Claude never reads the body until the description matches, so
write it as the phrases a user actually types — "prepare for restart", "where were we" — not as
an abstract summary of the skill's purpose.

**Write procedure, not prose.** Numbered steps, exact commands, and the failure mode after each
one. The most valuable lines in a skill are the traps: knowledge somebody paid for once, written
down so nobody pays again.

## See also

[**claude-code-ollama-qwen-setup**](https://github.com/mm-arturo/claude-code-ollama-qwen-setup) —
install Ollama and Qwen3.8-27B from zero, sized to the VRAM you actually have.

## License

MIT — see [LICENSE](LICENSE). Take them, change them, ship them.
