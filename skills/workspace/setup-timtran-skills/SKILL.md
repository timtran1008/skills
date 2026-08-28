---
name: setup-timtran-skills
disable-model-invocation: true
description: "Run once per workspace. Creates the substrate the Plan-Do-Judge skills read from: PROFILE.md, PRINCIPLES.md, a projects folder, today-tasks.md, and a library index."
---

# Setup

Run this once, in the folder where you keep your work. It creates the small amount of
structure the other skills assume — nothing more.

**This does not impose a filing system.** It does not require PARA, or Zettelkasten, or any
other method. It adds a handful of files alongside whatever you already have. If you already
keep projects in folders, the projects step just adds two files to each one.

## Step 0 — Ask before creating anything

Show the user what will be created, where, and let them adjust:

```
I'll create, in <cwd>:

  PROFILE.md              — you fill this in; skills read it to calibrate
  PRINCIPLES.md           — operating rules the skills assume
  today-tasks.md          — one file, today only
  projects/               — one folder per active piece of work
  library/INDEX.md        — index of notes and sources you capture

Nothing existing is touched. Proceed, or tell me what to change?
```

If any of these already exist, say so and **skip that item**. Never overwrite.

## Step 1 — PROFILE.md

Copy `PROFILE.template.md` from this repo into the workspace as `PROFILE.md`, with the
placeholders intact.

Then offer, and only if the user says yes: interview them through it, one section at a time,
and fill it in. Do not invent answers. A blank section is fine; a fabricated taste rule is
not — the agent will follow it for months.

Say plainly: **the good-enough-bar table is the highest-value part.** If they fill in nothing
else, fill in that.

## Step 2 — PRINCIPLES.md

Copy `PRINCIPLES.md` from this repo into the workspace, unmodified.

Tell the user they should read it and delete anything they disagree with. A principle they
don't believe in is worse than no principle, because the agent will enforce it anyway.

## Step 3 — projects/

Create `projects/`. For each active piece of work, a folder containing exactly two files:

**`context.md` — live state. What is true right now.**

```markdown
# <Project name>

**Status:** <active / blocked / dormant> · <one line on why>

## What this is
<2-4 sentences. Written for someone with zero context — including you in six weeks.>

## Key facts
| | |
|---|---|
| Owner / client | |
| Deadline | |
| Where the work lives | |

## Decisions made
- <dated, one line each, with the reason>

## Next actions
- [ ] <specific enough to start without thinking>

## Open questions
- <the things not yet decided, and who decides them>
```

**`log.md` — history. What happened, newest at top.**

```markdown
# <Project name> — Log

## YYYY-MM-DD — <what happened>
- <what was done, decided, sent, or learned>
```

**Why two files and not one.** `context.md` is read every time work resumes; it must stay
short and current, which means old entries get overwritten. `log.md` is append-only and read
almost never — but when a decision needs defending six months later, it is the only record
that exists. Merging them produces a file too long to read at resume time and too lossy to
audit. This split is the load-bearing part of the whole setup.

Ask which projects to create. Do not guess from folder names.

## Step 4 — today-tasks.md

One file at the root. Today only. It gets rewritten daily, not appended to.

```markdown
# Today — <date>

## Doing today
- [ ]

## Ruled dead — write owed
<Things decided to be dead in conversation but not yet written into their project file.
Drain this at the end of the day. See PRINCIPLES.md §8.>
```

## Step 5 — library/INDEX.md

Only if the user captures notes from books, talks, papers, or articles. If they don't, skip
it and say so.

```markdown
# Library Index

| Date | Source | Type | Note file | Reviewed? |
|---|---|---|---|---|
```

The `Reviewed?` column is what `adopt-or-drop` reads.

## Step 6 — Report and stop

List what was created and what was skipped. Then:

> "Setup done. Next: fill in the good-enough-bar table in `PROFILE.md` — it's the part that
> changes the most about how the other skills behave."

Do not proceed to run any other skill. Hard brake (PRINCIPLES.md §7).
