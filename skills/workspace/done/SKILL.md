---
name: done
disable-model-invocation: true
description: >
  Mark something finished: write it to context.md, log.md and today-tasks.md, capture any
  project learning, and sweep for what the completion just made untrue. The only completion
  command.
---

# Done

The single completion command. There is no tier to choose.

Earlier versions of this repo split completion three ways — a light `/done`, a `/log-it` that
also wrote history, and a `/sync` that captured learnings. That was a mistake in practice:
picking a tier is a decision you have to make *before* you know whether the session produced
anything worth keeping, and the cheap option always won. Learnings went unrecorded because the
skill that captured them was the one nobody chose. The tiers are gone; this skill absorbed all
three.

**Writes:** the touched project's `context.md` and `log.md`, `today-tasks.md`, and your
voice/taste log if you keep one. Moves a sent email draft into the project's `archive/`.
**Never writes:** your instruction files, skills, or any consolidated doctrine file. Never
deletes.

**Invoke:** `/done` (infer the completion from the conversation) or `/done <thing>`.

## Step 0 — Trigger guard

Run only when `/done` was actually typed. "Mark it done", "update the file", "ok that's
finished" are direct inline edits, not this skill. Handle those inline.

## Step 1 — Write the completion

**Typing `/done` is the explicit completion confirmation** — it satisfies *preparation is not
completion* for the named items and no others. Scope still applies: a drafted-but-unsent email
is logged as *drafted*, not *sent*. Never upgrade the verb, and never infer completion from a
draft the agent produced. If you genuinely cannot tell what was finished, ask **one** question.

1. **`context.md`** — mark `- [x] {task} — {outcome} {date}`. Update the status line if the
   phase moved. Add any follow-up that emerged as a new `- [ ]`; a pending item that lives only
   in `log.md` is invisible to the next check-in. Strike through any waiting-on this resolves,
   with a named cause and date.
2. **`log.md`** — append under today's date heading (create it at the top; create the file with
   the header `# [ID] — [Name] – Log & Reference` if missing):
   `- **{what happened}.** {recipients, amounts, decisions, file paths, outcomes}. -> \`{file}\``
   One bullet per discrete event. Check today's heading first and do not double-log.
3. **`today-tasks.md`** — mark the matching item `[x]`. If there is no matching item, say
   **"No matching task — adding as completed"** and add it. Never skip this file silently; that
   is the recurring failure.
4. **Email** — if a draft was actually sent, move it to the project's `archive/`.

## Step 2 — Sweep what this makes untrue

**Read [supersession-sweep.md](./supersession-sweep.md) first — it is binding.**

**Files before the user.** Read the owning `context.md` and resolve everything the file can
answer — items already marked done there, dates that moved, blockers since cleared. Ask only
about the residue. Never hand over a raw list of open items to sort.

**Absence from a tracker is not evidence of absence.** If a workstream or a client has no row
in the file, that is an *untracked-item risk*, not "nothing is owed". Say "this isn't tracked —
verify at the source." Never reason "no row, so no deliverable."

Pull the entities out of what was just completed — person, client, document, deliverable,
project code, date, amount — and search the project's `context.md` and `today-tasks.md` for
each. Keep the read boundary tight: one project, no grep-chaining across everything. Within it,
list **every** item matching these categories, not a selection:

- Open `[ ]` tasks the conversation shows are actually done or superseded.
- Waiting-on items the conversation shows are resolved.
- Dated lines more than two weeks old still quoted as live state.
- Items that now contradict something updated this session.
- **Items superseded by what was just completed** — test every hit against the four shapes:
  entailment, replacement, reversal, duplicate. **Entailment is the one that hides**: the
  completion is a later step in a chain, so an earlier step must already have happened even
  though nobody said so.

| # | File | Item | Why stale / what superseded it | Flip to |
|---|---|---|---|---|

Present the table, numbered, and **wait**. Nothing gets flipped unasked.

**One exception: entailed rows.** Where the completion is *impossible* unless the older item
happened, close it in this pass without asking and report it in Step 4 for reversal. Narrow
carve-out. Never applies to a draft the agent produced, and any plausible gap in the chain
downgrades it to a normal row.

Closes are strikethrough plus a named cause and date. Never delete. If nothing is stale and
nothing is superseded, **say both words explicitly** in one line. Silence reads as a skipped
sweep.

## Step 3 — Learnings

If the session produced something that should change how future work on **this project** is
done — a stakeholder preference, an audience behaviour, a revealed constraint, a process
adjustment — append to `## Learnings` in its `context.md`: `- [YYYY-MM-DD] {one-liner}`. Append
only. Corrections to how the *agent* behaves in general do not go here; those belong in your
instruction file, via `/checkout`.

If the session produced writing in your voice that you then edited, append the draft→final
delta to your taste log with a `**Rule:**` line. **A rule is admissible only if two readers
would agree whether a piece followed it.** Adjectives — "warmer", "tighter", "more direct" —
fail that test; write those as `**Rule:** UNPROMOTED` and leave the evidence intact. Never
invent a behaviour to make an adjective pass.

**Then sweep the backlog, every run.** Read the touched project's `log.md` for blocks stamped
`PENDING` — each one is a draft→final delta that was observed and written down but never
transferred. Move it into the taste log under the same rules as above, then restamp the source
line in `log.md`: strike through the `PENDING` marker with the transfer date, never delete it.

This sweep exists because the write-it-down step and the transfer step were owned by different
skills, and the transfer never fired. Deltas sat pending for six weeks with no owner. A capture
step with no sweep behind it is a queue, not a system.

## Step 4 — Confirm

```
- context.md      — {tasks marked, items added, status}
- log.md          — {what was logged}
- today-tasks.md  — {marked, or "no match — added"}
- archive         — {file moved, or n/a}
- superseded      — {each close, "reverse if wrong"; or "nothing superseded, nothing stale"}
```

State every file by name. If one was not touched, say why.

**Never write a file with a whole-file truncating call.** Read → modify → write, with the
encoding stated explicitly.
