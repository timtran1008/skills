---
name: log-it
disable-model-invocation: true
description: >
  The full-record completion tier. Writes a completed piece of work into all three trackers —
  log.md, context.md, today-tasks.md — and files any sent artifact. Use for deliverables that
  deserve a permanent history entry.
---

# Log it

`/done` marks things done. This also writes them into history, which is what you will actually
need in six months when a decision has to be defended.

**Invoke:** `/log-it`

## The rule that gets broken

> **All three files are updated on every invocation. No exceptions.**
>
> The known failure mode is updating `log.md` and `context.md` and quietly skipping
> `today-tasks.md`. Before reporting, **enumerate all three files by name** and confirm each
> was touched. If `today-tasks.md` has no matching task, say so out loud — never skip it
> silently.

Run this **after** completion is confirmed. If nobody has said "sent", "done", or the
equivalent, this skill does not run.

## Step 0 — Identify what happened

State it back before writing anything:

1. **What was completed** — an email sent, a file delivered, a decision made, a task finished.
2. **Which project** it belongs to.
3. **The evidence** — the user's own words, or something confirmed in the conversation.

Anything ambiguous, ask. Do not guess.

## Step 1 — log.md

**Duplicate check first.** Read today's date heading if it exists and scan the bullets. If one
carries the same key phrase — recipient plus action, or filename plus action — stop and ask:
*"This looks already logged today: '<existing bullet>'. Log again?"* Wait.

Append under today's date heading, creating it at the top of the file (below the header, above
all earlier dates) if it does not exist:

```markdown
## YYYY-MM-DD

- **{What happened}.** {Recipients, decisions, paths, outcomes, numbers.} → `{filename}`
```

- One bullet per discrete event or decision.
- Include recipient names for anything sent, paths for anything created or moved, and the
  numbers behind any decision.
- Keep it factual. No commentary, no interpretation.
- **If follow-up work emerged, it goes in `context.md` too** (Step 2). A pending item logged
  only here is invisible to the next check-in.

## Step 2 — context.md

The live state. The next check-in reads this file, not the log.

**2a — Mark the completed task.** Already `[x]`? Skip it and note "already marked, no change"
in the confirmation. Otherwise:

```
- [x] {original task text} — {outcome} {date}
```

**2b — Update the status line** if the completion moved the project's phase.

**2c — Add what the work created.** New tasks as `- [ ]`; new waiting-on entries with the date
and the person.

**2d — Resolve waiting-on items** the completion answers:
`- ~~**Name:** original item~~ — RESOLVED {date}`

**2e — The supersession sweep. Mandatory, never skipped.**

**Read [supersession-sweep.md](../sync/supersession-sweep.md) first — it is binding.**

2a through 2d handle the item that was named. This step handles the ones that were not: what
does this completion make untrue elsewhere in the file?

Pull the entities out of what was just logged — person, client, document, deliverable, date,
amount — and search `context.md` and `today-tasks.md` for each. Test every hit against the
four shapes: **entailment, replacement, reversal, duplicate**.

- **ENTAILED** — the logged fact is *impossible* unless the older item happened. Close it in
  this pass and report it. Never applies to a draft the agent produced.
- **LIKELY** — present it numbered and wait for a ruling.
- Close as strikethrough, named cause, date. Never delete. The supersession goes into `log.md`
  as a **new dated bullet**, never as an edit to a past entry.

## Step 3 — today-tasks.md

Find the matching task. Already `[x]`? Note it and move on. Otherwise mark it
`- [x] {task} — {outcome}`.

**If no matching task exists** — which happens whenever something unplanned gets finished —
say so explicitly (*"No matching task in today-tasks.md. Adding as completed."*) and add it
under the right project heading as `- [x] {description} — {outcome} (unplanned)`.

**Never skip this file just because there is no matching line.**

## Step 4 — File the artifact

If the work involved something sent — an email draft, a proposal, a deck — and the file is
still sitting in the project's working folder, move it to that project's `archive/`. If no
artifact was involved, skip and say so.

## Step 5 — Confirm

```
Logged:
- log.md        — {what was logged}
- context.md    — {tasks marked, items added, status updated}
- today-tasks.md — {which tasks marked done}
- archive       — {file moved, or "n/a"}
- superseded    — {each item closed, with what superseded it — "reverse if wrong";
                   or "nothing superseded"}
```

**Any file not updated gets its reason stated.** Never omit one silently.

## Guardrails

- **Preparation is not completion.** Drafting an email is not sending it. Do not mark `[x]`
  without confirmation that the thing actually happened.
- **No fabrication.** Log only what was reported or confirmed. Unsure whether it landed? Ask.
- **Closing is half the write.** New information that leaves a contradicting old line open is
  an incomplete log. Step 2e is not optional, and it reports even when it finds nothing.
- **Pending items belong in `context.md`.** Anything still outstanding that a log entry
  mentions must also exist as a `- [ ]` line.
