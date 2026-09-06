---
name: handoff
disable-model-invocation: true
description: >
  Compact this conversation into one handoff document so a fresh agent — in a new session, or
  a different tool entirely — can pick the work up. Writes the briefing and nothing else: no
  project files touched, nothing marked done.
---

# Handoff

Long sessions rot. The context fills with dead ends and stale file dumps, the agent gets
slower and more forgetful, and you cannot paste a transcript into a new chat. `/handoff` is
the clean save point: it keeps what the next agent needs, throws away the noise, and lets the
work continue somewhere fresh instead of dying when this session ends.

It is a **document writer, not a state keeper.** It deliberately updates no tracking files.

| Skill | Does |
|---|---|
| `/handoff` | Writes the baton. Touches no source files. |
| `/done` | Persists this session's progress to the project files. **Run this first** if state isn't saved. |

**Invoke:** `/handoff <what the next session is for>`

## Step 0 — Trigger guard

Run only when `/handoff` was actually typed. "Let's hand this off", "pass it to a fresh
Claude", "give this to Codex" are conversation, not an invocation.

- `/handoff <purpose>` → the argument **is** the Mission. Proceed.
- `/handoff` bare → ask **exactly one** question: *"What's the next session for?"* Then
  proceed. Never infer the Mission silently. A handoff with no target is just a transcript dump.

## Step 1 — Write the document

Save to `projects/<project>/handoff-YYYY-MM-DD-<topic>.md`, in the folder of the project the
session's work belongs to. If it belongs to no project, the workspace root. `<topic>` is a
short kebab-case slug from the Mission.

```markdown
# <Topic> — Handoff (YYYY-MM-DD)

**Expires:** YYYY-MM-DD (the day after this doc's date). After that this is residue — bin it;
the durable state lives in `context.md` / `log.md`.

One sentence: pick up here in a fresh session. <Why this work started, if not obvious.>

## Mission
What the NEXT session is for. One or two lines. This is the lens — everything below serves it.

## State now
Where things actually stand, and the why behind the current shape. Decisions already made and
accepted. Only what bears on the Mission.

## Resume here
The single exact next action. Concrete enough to start on without re-deriving the context. If
there is an ordered next-few, number them — but lead with the very next move.

## References
Paths and URLs only — do NOT copy the content.
- projects/<name>/context.md — live state
- projects/<name>/log.md — history
- <plans, drafts, tickets, commits, prior handoffs> by relative path or URL

## Gotchas
The landmines the next agent will otherwise hit blind. Fragile steps, naming traps,
"do NOT do X". Omit the section only if there genuinely are none.

## Suggested skills (optional)
Slash commands that would accelerate the work, if the receiving agent has them. Framed as
optional — the document must work fully for a receiver with no skills at all.
```

### Rules while writing every section

1. **Reference, don't duplicate.** Anything already in `context.md`, `log.md`, a plan, or an
   artifact gets linked by path — never re-pasted. The document is a map to the work, not a
   copy of it. Stale copies are the trap.
2. **Self-contained for any tool.** Assume the receiver may be a different model in a
   different product with no access to your skills or your conventions. It must stand alone.
   Skill references live only in the optional block at the end.
3. **Redact secrets.** Strip API keys, tokens, passwords, and personal data before writing.
   Never carry a credential into the document.
4. **Plain relative paths**, no backticks and no absolute paths, so they stay clickable.
5. **Judgment over completeness.** Capture what the next agent needs to continue, not
   everything that happened. Cut the noise — that is the entire point of the skill.

## Step 1b — Lifecycle: the doc expires the next day

**A handoff expires daily.** It is a baton, not a document — written for one next session, and
dead once the day it was written for has passed. Anything worth keeping beyond that belongs in
`context.md` and `log.md`, which is `/done`'s job, not this file's.

Every handoff carries the `**Expires:**` line under the title, dated the day after it was
written. One exception: a handoff still named as a `**Source:**` by a live derived artifact
stays until that artifact is finished.

⚠️ **This skill writes nothing but the one doc.** It does not retire its own past output — it
cannot delete and must not move files. Expired handoffs are collected by whatever cleanup pass
you run, which surfaces them for a ruling.

**The expiry line is what makes that ruling mechanical instead of a judgment call.** Before it
existed, fifteen handoffs across six projects had piled up over three months with no retirement
rule, because the generator defined none. A file with no stated lifespan is a file nobody can
throw away.

## Step 2 — Report and stop

Print the path and a two or three line summary of what was captured. **Do not preview the
full draft in chat** — it goes in the file precisely so it does not go in a context window.

Then stop. Nothing marked done, no tracking file updated, no next task proposed. If session
state clearly is not persisted yet, one line — *"State not saved — run `/done` before you
close this session?"* — but do not act on it.

```
✓ Wrote projects/acme-rollout/handoff-2026-06-04-day3-prep.md
Captured: current state, resume at the Day 3 outline, 2 gotchas, refs to context.md + log.md.
State not saved this session — run /done before closing?
```
