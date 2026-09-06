---
name: checkin
disable-model-invocation: true
description: >
  Daily planning. Scans every project's context.md for open work and deadlines, recovers
  everything unfinished from yesterday, asks what is already in the calendar, and proposes a
  time-blocked day. Writes nothing until the plan is approved.
---

# Check-in

The first conversation of the day. It produces one artifact: `today-tasks.md`, approved before
it is written.

**Invoke:** `/checkin`

Reads: every `projects/*/context.md`, the existing `today-tasks.md`, `PROFILE.md`.
Writes: `today-tasks.md` only, and only after approval. **Never** `context.md`, never `log.md`.

## The session boundary

> **This is a read, plan, and confirm session. Nothing else.**
>
> No emails drafted, no decks built, no posts written — and no *offering* to. If a task
> surfaces that needs drafting, it becomes a line in `today-tasks.md` and stops there. The
> work happens in a fresh conversation, never inside the check-in.
>
> If you catch yourself about to say "want me to draft that?" — stop and re-read this. A
> surfaced need is a task entry, not a deliverable.

The reason is not tidiness. A check-in that turns into two hours of drafting never produces
the plan, and the day gets shaped by whichever item happened to come up first.

## Triage discipline — one thing at a time

When the user is clearing a list — short messages, sequential "what's next", one-word
confirmations — propose **exactly one** next action per turn. Do not queue a second ask in the
same message; that forces them to reject the second offer in order to focus on the first.

The one proposal must be **concrete**: the specific sub-steps and the output, not the project
name. *"Client prep"* is not a proposal. *"Confirm the topic with the organiser and propose two
prep slots"* is.

## Step 0 — Run the scans

Steps 0a to 0c are read-only sweeps over many files. If your agent supports subagents, dispatch
them **in one message** so they run concurrently, then do the judgment yourself on what comes
back. If it does not, run them inline — never skip a step because a subagent failed. Say it
failed, then do it directly.

**The scans are delegated; the triage is not.** Agents return evidence. Picking the focus
projects, ranking the deadlines, and building the schedule stay with the main agent. Never ask
a subagent to propose the plan.

**Verbatim, or it is useless.** End every subagent brief with: *"Return the matching lines
verbatim — full text, with file path and line number. Do not summarise, shorten, re-word or
de-duplicate."* A summarised line loses the exact figure and the near-identical name, and the
check-in degrades without anyone noticing.

### 0a — Every project's state

Read every `projects/*/context.md`. Return, per project: the name, the status line, and every
open `- [ ]` item verbatim. Flag any project whose `context.md` was last touched more than 14
days ago.

**Absence from a tracker is not evidence of absence.** When a client or workstream has no row
in the file, that is an **untracked-item risk**, not "nothing is owed". Say *"this isn't tracked
— verify at the source."* Never reason "no row, so no deliverable."

### 0b — Dated lines

Grep every `context.md` for dates inside the next seven days, and for **past** dates whose
`- [ ]` is still open.

An overdue item keeps reporting for a fortnight, deliberately: an alarm that fires on the due
date and vanishes the day after goes silent exactly when the work is actually owed. **Treat
overdue as hot.**

For every hard deadline found:

1. Compute the remaining working days, using the working-week definition in `PROFILE.md`.
2. **Two days or fewer left → that project must appear in today's plan with concrete
   sub-steps**, not a single "check status" line. It cannot be triaged out of the focus set.
3. Surface it in a **Deadline Watch** callout above the schedule.
4. **Then put it in the schedule table too** — see the visibility rule below. The callout alone
   does not count.

A multi-day rolling block ("Days 4-6: pick a form and draft") is actionable **today** if today
falls inside or immediately before the window. Decompose it into today's specific sub-step
rather than reading it as "in progress, skip".

### 0c — Yesterday's unfinished work

Two sources, merged and de-duplicated by task rather than by wording:

1. **`projects/*/context.md`** — the open `- [ ]` items from 0a. This is the durable carry
   medium, the one `/checkout` writes to.
2. **The existing `today-tasks.md`** — read it *before* it is archived in Step 3, and extract
   every unchecked `[ ]` item. This is the safety net for a day when `/checkout` was skipped.

**When they disagree:** an item in `today-tasks.md` but not in `context.md` still carries — and
gets flagged, because it means the last checkout failed to persist it, or its project was
archived out from under it. Say which.

**Carry by default. Silence means carry.** An item drops off only when the user explicitly
drops or defers it. Present carried items in a **Carried over** group at the top of the
proposal, so each one can be vetoed individually.

**Carried items are never silently triaged out** the way fresh backlog can be. If a carried
item belongs to a non-focus project, list it anyway — one line is fine.

**Count the carries.** Anything carried three days or more gets surfaced with its count
attached. "Carried four days" is information, and it is the signal that something underneath is
unruled and belongs in the project's Open questions rather than its task list. Never present a
five-day carry as if it were fresh.

## Step 0d — Supersession check, before anything is carried

**Read [supersession-sweep.md](../done/supersession-sweep.md) first — it is binding.**

Step 0c carries by default and treats silence as carry. That is right for items nobody has news
about, and wrong for items the scans just proved dead. Carrying a dead item puts it in the day
plan as live work, and it stays alive until someone reconciles it by hand.

The scans have just returned every project line and every dated line **in one place**. This is
the only step in the day with that whole view, so it is the only step that can catch a carry
killed by evidence in a *different* project's file.

For every item about to be carried, pull its entities — person, client, document, deliverable,
project, date, amount — and check them against everything the scans returned. Test each hit
against the four shapes: entailment, replacement, reversal, duplicate.

**Check-in cannot write `context.md` and closes nothing here.** What it does instead:

- **Entailed dead** — the carried item cannot still be open, given what another line proves. Do
  not schedule it as live work. It goes into the **"Ruled dead — write owed"** section of
  `today-tasks.md` at Step 3, with the killing line quoted and its `path:line`. `/done` or
  `/checkout` does the actual write.
- **Likely dead** — ask, in one line, inside the plan proposal. **If it is ruled dead during
  the check-in, it joins the same section.** A ruling heard here is never left in chat.
- Everything else carries as normal.

If nothing is superseded, say "nothing superseded" in the proposal.

> **The section is a file write, not a spoken group.** A kill that exists only in the
> conversation is worse than no kill: the item stays `- [ ]` in its `context.md`, and tomorrow's
> check-in re-carries it as live work having never heard the ruling. Saying it in the proposal
> is not the deliverable. The section in `today-tasks.md` is.

## Step 1 — Ask about the day

**The agent cannot see a calendar.** Ask outright — not "anything the file can't see" — for
start and end times: meetings and calls, appointments and errands, travel, deadlines due today,
and any personal commitment that constrains time or energy. Best estimates are fine.

**A scheduled event that has passed is a question, not a status.** For any meeting the calendar
carried today or yesterday, ask **two** things: did it happen, and what was ruled. A file's
silence is not "it didn't happen". And a participant's *position* — what they want — is not the
*outcome*. Positions are inputs. Outcomes come from the user.

## Step 2 — Propose the plan

Place the fixed and calendar items first, then build around them. Take working hours, fixed
daily blocks, and any day-of-week rules from `PROFILE.md` — never invent them. Pick three to
five projects to focus on, prioritised by deadline, then by what is blocking something else,
then by quick wins.

### The schedule table is the answer to "what's on today?"

Everything live gets a row. This rule exists because of a specific failure: a deadline expiring
that same day was written up correctly in the Deadline Watch callout *and* in the notes section
— and left out of the schedule table. The day was asked about five times and it was never once
mentioned. The write-ups were not the failure. The missing row was.

**A reader — the agent included — answers "what's on today?" off the schedule table**, because
it is the only ordered, complete view of the day. Anything not in it is invisible, however well
documented elsewhere.

So every hot or overdue item, and every deadline expiring today, gets a row. No exceptions,
including the ones with no work in them:

- **Work today** → a normal timed row.
- **Live but untimed** — a watch, a reply window, something that could land any time → an
  **`ALL DAY (ambient)`** row, placed first.
- **Deliberately no action today** → still a row: **`⛔ NO ACTION`**, saying in the block cell
  why not, and when it does fire. A decision not to work on something today is a scheduling
  decision about today, and it belongs where the day is described.

**Notes and conflicts is commentary, not the schedule.** If you find yourself writing "no block
today, deliberately" in the notes, that item needs a `⛔ NO ACTION` row.

### Specificity

Every block carries concrete sub-steps and a clear definition of done.

| Bad | Why | Good |
|---|---|---|
| "Work on the programme" | No concrete action | "Send one follow-up on capstone facilitator coverage and the contract ETA" |
| "Prepare for the meeting" | No definition of done | "Review the Week 1 draft; produce a final edit list with timing per section" |

### Example

```
## Proposed plan — <date>

### Deadline Watch
- Compliance training closes TODAY — 0 days left.

### Schedule
| Start-End | Block | Definition of done |
|---:|---|---|
| **ALL DAY (ambient)** | Compliance training — watch for "already completed" replies | Each reply recorded before the count |
| 08:00-10:30 | Programme: Week 4 email draft + publisher review | Email drafted, ready for review |
| 10:30-12:00 | Client meeting prep | Talking points drafted |
| 14:00-16:00 | Workshop deck | Share-ready by Wednesday 09:00 |
| **⛔ NO ACTION** | Invoice — it is the vendor's move, no dated trigger | Nothing owed today; re-check next check-in |

### Carried over
- [ ] ... (carried 4 days — worth ruling rather than re-carrying?)

### Ruled dead — write owed
- ... or "nothing superseded"

### Notes / conflicts
- ...
```

Order the day with quick mechanical work early — logging, formatting, short replies — and
reasoning-heavy work after.

## Step 3 — Approve, then write

Present the plan. Ask: *"Does this look right? Anything to add, remove, or reprioritise?"*

**Nothing is written until it is approved.**

Then:

1. **Archive the outgoing file first.** *Move* the existing `today-tasks.md` to
   `archive/today-tasks/YYYY-MM-DD-today-tasks.md`, where the date is the one written **inside
   that file** — the day it covered, not today. Check-ins get skipped; do not assume it was
   yesterday. Move it, never delete it. If that filename exists, suffix `-2`, `-3`, and say so.
   If there is no existing file, say so in one line and continue.
2. **Write the new `today-tasks.md`.**

> **The "Ruled dead — write owed" section is mandatory** whenever Step 0d found something, or
> something was ruled dead during this session. Each entry carries the item text, the killing
> line quoted, its `path:line`, and the date. Omit the section only when both are empty. Until
> `/done` or `/checkout` drains it, this is the *only* durable record of that ruling.
