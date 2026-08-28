---
name: sync
description: >
  Persist a session's progress to the project files: enumerate every open item, reconcile it
  against what the conversation actually established, close what the new facts killed, and
  write the session's history. Run before a long session ends or its context is lost.
---

# Sync

A conversation is not a record. Everything decided, sent, learned, or reversed in this
session exists only in a context window until this skill writes it down.

**Invoke:** `/sync`

Writes to: each touched project's `context.md` and `log.md`, and `today-tasks.md`.
Never writes: your agent instruction file, content files, anything it did not read first.

## Step 1 — Capture project learnings

Re-read the conversation for insights that should change how future work on **this project**
is done. Scoped to the project, not to the agent's global behaviour.

**Counts:** a stakeholder preference discovered ("the CEO wants the summary on page 1"), an
audience behaviour observed ("this group disengages after slide 15"), a process adjustment
("send the agenda 48 hours ahead, not 24"), a constraint revealed ("approval needs two
sign-offs"), something that worked or failed unexpectedly, or anything the user prefixed with
"note for next time".

**Does not count:** corrections to how the agent behaves in general, personal preferences, or
a one-off fact with no future implication.

Present candidates and let the user confirm, edit, or cut:

| # | Project | Learning | Source |
|---|---|---|---|

Then append confirmed ones to `## Learnings` in that project's `context.md`, as
`- [YYYY-MM-DD] <one line>`. **Append only** — never edit or remove an existing learning.

## Step 2 — Enumerate and reconcile

For each project discussed, **read `context.md` and enumerate every open item.** Enumerate,
do not scan.

### 2a-pre — Drain "Ruled dead, write owed"

Read `today-tasks.md`. If it carries a **"Ruled dead — write owed"** section, every entry is a
ruling already made that has no `context.md` write behind it. Close each one now — strikethrough,
named cause, date, in the owning file — then clear the section.

These are **not** re-openable questions. Do not ask for a re-ruling; report what was closed. If
an entry's file or line cannot be found, say so and leave the entry in place rather than
dropping it.

### 2a — Open task audit

**Files before the user.** The files answer first. Resolve everything `context.md` can settle
before asking anything, and put the answer in the Evidence column. The user is asked only about
what the evidence genuinely cannot settle. **Never hand over a raw list of open items to sort.**

| # | Task | Disposition | Evidence |
|---|---|---|---|

- **DONE** — explicitly confirmed, in the user's own words. Cite it. **Never infer completion
  from a draft the agent produced.**
- **OPEN** — no evidence of completion. Say so.
- **NEW INFO** — partial progress or a status change. Describe it.
- **ORPHAN** — a task, usually one "carried from <date>", whose referent nobody can identify
  after checking `context.md`. **If neither party knows what it is, kill it** — struck, dated,
  `KILLED (orphan)`. Unidentifiable tasks must not auto-carry forever.

*Preparation is not completion.* Drafting an email is not sending it. Building a folder is not
sharing it. Present the table and **wait**.

### 2b — Waiting-on audit

Same table for every "waiting on" item: RESOLVED / STILL WAITING / UPDATED, with evidence. If
the conversation produced an email that attached the awaited deliverable, that item is
RESOLVED. Present and wait.

### 2b2 — Supersession sweep (mandatory, runs even when 2a and 2b found nothing)

**Read [supersession-sweep.md](./supersession-sweep.md) before this step — it is binding.**

2a and 2b ask *did the items in the file change?* This step asks the reverse: *given what this
session established, what in the file can no longer be true?* Both directions are required,
and the second is the one that gets skipped.

For every new fact — **including facts that opened no task and closed nothing by name** — pull
out its entities and search `context.md` and `today-tasks.md` for each. Test every hit against
the four shapes: entailment, replacement, reversal, duplicate.

| # | File | Item | Superseded by | Shape | Flip to |
|---|---|---|---|---|---|

**ENTAILED** rows close in this pass and are reported for reversal. **LIKELY** rows wait for a
ruling by number. Write closes as strikethrough, named cause, date — never delete. If nothing
is superseded, **say so in one line**; silence reads as a skipped sweep.

### 2c — Write the updates

After both tables are confirmed:

1. Mark confirmed items `[x]` in `context.md`.
2. Strikethrough resolved waiting-on items and tag the outcome.
3. **Log every completion to `log.md`.** A task marked `[x]` with no log entry is silent data
   loss.
4. Add items that emerged during the conversation — **especially follow-ups. These go into
   `context.md` as `- [ ]`, not just into a log bullet.**
5. Update statuses, dates, and phases the completions made wrong.
6. Write the 2b2 closes.

### 2d — Write the session log entry (fires even when nothing was completed)

Step 2c logs **completions**. This step logs **what happened.** They are not the same event,
and keying history to ticked checkboxes is how history gets lost: a document signed, a session
delivered, a decision reversed, an escalation — none of them ticks a box, so none of them was
ever written down.

**Every project touched gets a dated `log.md` entry, whether or not any task changed state.**
An unchanged task list is not evidence that nothing happened.

```markdown
## YYYY-MM-DD

- **[What happened]** — [the substance: decided, sent, delivered, received, learned, or
  reversed. Name the people, amounts, dates, and paths.]
```

What must be logged, none of which is a completion:

- **Decisions and reversals** — with the reasoning, and what the decision replaced. A killed
  gate goes here along with the dates it orphaned.
- **Real-world events** — a session delivered, a meeting held, a document signed, a payment
  received, someone leaving a role.
- **Sends and receipts** — what went to whom, on what channel, what came back. An unsent draft
  is logged as unsent.
- **State that moved without a task moving** — a date confirmed, a blocker cleared, a number
  corrected.
- **What was ruled out** — options rejected, and why. Future sessions re-litigate anything
  that was not written down.

Skip only when a project was mentioned in passing and genuinely nothing changed. When unsure,
write it: an over-logged project costs a line, an under-logged one costs the history.

**Never fabricate.** Log only what the conversation actually establishes. If something was
reported without confirmation that it landed, log it in exactly those terms — *"reported as
sent; not independently confirmed."* A definition of done is a spec, not a status.

**`log.md` is append-only here.** Never edit or delete an existing entry. If a past entry turns
out to be wrong, append a correction with today's date saying what it supersedes.

### 2e — Close what was ruled

Any question this session answered gets its answer written into the owning `context.md` — in
`## Decisions made` with the date, and struck out of `## Open questions`. A ruling that stays
in the chat is not a ruling.

**Trace the kill.** If a ruling voids a date something else was back-planned from, mark those
dates **unsound** in their own files in the same pass. Never silently keep an orphaned
deadline; never invent a replacement. The check runs both ways — before marking a date
unsound, verify it was actually derived from the thing that just died.

If the session ended with a *new* question unruled, add it to `## Open questions` **stated
with its options**, not as a note that a question exists.

A one-word "yes" or "next" does not close anything on its own. Restate the ruling in full and
confirm before writing it.

## Step 3 — Reconcile today-tasks.md

Read it, mark `[x]` what Step 2a confirmed, add what emerged during the conversation, write it
back.

## Step 4 — Report

Name every file written and what changed in each, including the supersession line — *"nothing
else superseded"* is a result and must be stated. Then stop.
