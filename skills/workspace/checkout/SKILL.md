---
name: checkout
disable-model-invocation: true
description: >
  End of day. Resolves every unfinished item into done, superseded, dropped, or carried —
  persisting the carries so they survive tomorrow's overwrite — sweeps context files for rot,
  and proposes rule changes for your agent instruction file.
---

# Checkout

`/checkin` decides what the day is for. `/checkout` makes sure the day survives it.

The load-bearing part is Step 1b: `today-tasks.md` is overwritten at the next check-in, so an
unfinished item that lives only there is **gone**. Persisting it is what makes the loop work.

**Invoke:** `/checkout`

## The session boundary

> **This is a read, log, and reconcile session. Nothing else.**
>
> No drafting, no building, no *offering* to. A task that surfaces needing work becomes a line
> in a project file and stops there. If you catch yourself about to say "want me to draft
> that?" — stop and re-read this.

## Triage discipline — one thing at a time

Propose exactly one next action per turn, concrete: the sub-steps and the output, never the
project name alone.

## Step 1 — Log every project touched today

**Before anything else.** Write the session's progress and history into the project files —
`context.md` and `log.md` for each project this session touched. Skip it and tomorrow's
check-in reports stale tasks as live work.

Checkout used to delegate this to a separate `/sync` command. It no longer exists: completion
is one command (`/done`), and checkout logs what `/done` did not.

## Step 1a — Run the scans

Steps 1b, 3 and 4 are read-only sweeps. Dispatch them as concurrent subagents if you can, then
do the judgment yourself. If you cannot, run them inline.

> **Checkout is a write skill; its subagents are not.** No agent writes `context.md`, `log.md`,
> or `today-tasks.md`. Every write happens in the main session, after approval. Say so
> explicitly in each brief. And require verbatim lines with paths and line numbers — a
> summarised line loses the figure or the name that made it actionable.

**Scan 1 — reconcile evidence.** Read `today-tasks.md` and extract every unchecked `[ ]` item
verbatim. For each, open the owning project's `context.md` and report what the file already
settles: marked done there, superseded by a later ruling, date moved, blocker cleared, or
nothing found. Return the evidence line, not a verdict. Flag every place `today-tasks.md` and a
`context.md` **contradict** each other, quoting both.
**Also search by entity, not by wording:** for each unchecked item, pull out its person,
client, document, deliverable, project, date, and amount, and grep the owning `context.md` and
`log.md` for each. Return any line mentioning the same entity even when it shares no words with
the task. That is how a later step in the same chain gets found.

**Scan 2 — hygiene.** Report every `context.md` over ~80 lines, with its line count, and which
blocks inside it are completed tasks or old dated entries. Note which projects have no
`log.md`. **Move nothing.**

**Scan 3 — dated-line age.** Scan active projects' `context.md` for dated lines older than 14
days against today, which the brief must state explicitly. Return each verbatim with
`path:line`. Separate genuine rot from dates that are historical by design — a log pointer, a
"delivered 19 Aug", a closed ruling — but when unsure, return it and say so.

## Step 1b — Reconcile today-tasks.md (carry-forward is the default)

**Files before the user.** Read the owning `context.md` for every project carrying an unchecked
item **before** asking anything. Resolve everything the files settle: items already marked done
there, figures since recorded, dates that moved, blockers since cleared. Then present only the
residue:

1. Items **no file can settle** — was it done offline? should it be dropped?
2. Any place `today-tasks.md` **contradicts** a `context.md` — state which is right and why.

**A scheduled event that has passed is a question, not a status.** Ask two things: did it
happen, and what was ruled. A file's silence is not "it didn't happen", and a participant's
position is not the outcome.

**Never hand over the full unchecked list.** The residue is the entire point of this step.

> **The residue list is uncapped** — an explicit exception to the cap-at-three rule on surfaced
> batches. Present all of it in one pass.

**First, drain "Ruled dead — write owed".** If `today-tasks.md` carries that section, each
entry is a ruling already made with no write behind it. Close each — strikethrough, named
cause, date, in the owning `context.md` — and clear the section. **Never re-ask for these rulings.**

Then resolve **every** remaining unchecked item into one of four outcomes. None may be left
sitting only in `today-tasks.md`:

- **Done** (confirmed by the user) → `[x]` in `today-tasks.md`, updated in the owning
  `context.md` and `log.md`.
- **Superseded** (settled by the evidence, not the user) →
  **read [supersession-sweep.md](../done/supersession-sweep.md).** Scan 1 returns supersession
  evidence; this outcome is where it lands, and without it that evidence silently defaults to
  carry. Test against the four shapes. An **entailed** item closes in this pass and is reported
  for reversal; a merely **likely** one joins the residue list. Close as strikethrough, named
  cause, date, in both files. Never delete.
- **Dropped** (explicitly cancelled) → remove it, and note the drop in the owning `context.md`
  if it was tracked there.
- **Otherwise → carry forward.** Ensure the item exists as an open `- [ ]` line in its project's
  `## Next actions`. Add it if missing. **This is what makes it survive.**

**Silence means carry.** An unfinished item carries unless it is explicitly marked done or
dropped, or the evidence supersedes it. Do not ask for each carry to be re-confirmed; surface
the list once so the exceptions can be flagged.

This catches work done in other tools, in other sessions, or offline — not just what happened
in this conversation.

## Step 1c — Split every carry: task or decision?

Before writing the carry lines, put **every** carried item through this test:

> **Could an hour of uninterrupted time just *do* it?**
>
> - **Yes → a task.** It goes into the project's `## Next actions` as `- [ ]`, tagged with its
>   carry count: `- [ ] Draft the pricing note (carried 2x since 26 Aug)`.
> - **No — somebody first has to decide what it should be, or choose between options →
>   a decision.** It goes into the project's `## Open questions`, **stated with its options**,
>   and the task line carries as usual.

A task carried because the day ran out is a task. **A task carried for the fourth consecutive
day is almost never a task** — repeat carries are the strongest available signal that something
underneath is unruled and nobody has noticed. **Three or more carries triggers the split
question automatically.**

Writing a decision properly is most of the value: *"the client project has a pending decision"*
is a failure. *"Is the coaching channel email-only from now on, or does the next live session
get a committed date?"* is the step working. If the answer to "what does this block?" is
"nothing", it is not a decision — it is a task.

**Report the counts, including the zeroes.** "0 decisions opened, 7 tasks carried, 1 closed as
superseded." Silence is how this step goes unperformed: it starts as one advisory sentence and
nothing ever checks that it fired.

## Step 2 — Propose rule changes

Read your agent instruction file — `CLAUDE.md`, `AGENTS.md`, whatever your tool loads on every
session.

> **This step is the only channel for changing it.** The agent never self-writes always-loaded
> behavioural memory and never auto-graduates a rule into it. It suggests here; you approve;
> Step 3 applies. Other learning types route elsewhere and must not come here: project-scoped
> learnings go to that project's `## Learnings` via `/done`.

Re-read the session for corrections and rejections. For each one that is a **reusable rule**
rather than a one-off fix, propose a specific edit:

```
**File:** CLAUDE.md
**Section:** [section]
**Change:** Add / Update / Remove
**Supersedes:** [the existing rule, quoted, with its section — or `nothing`]
**Content:**
[exact text]
```

**The `Supersedes` line is required, not optional.** Suggestions here are additive by nature,
which is how an always-loaded instruction file ends up with two rules pointing in opposite
directions — and unlike a stale task, a contradictory rule misfires on *every* future session.
Before proposing, search the file for the rule the new one narrows, replaces, or contradicts.
Name it, quote it, and propose the edit **to it** rather than a second rule beside it.

## Step 3 — Approve, then apply

Ask which suggestions to apply. Apply only what was approved. Confirm.

## Step 4 — Context hygiene

For each `context.md` touched this session:

- Over ~80 lines → move completed tasks and old dated entries into `log.md` in the same folder.
  This is a **relocation of text that already exists**, not new logging.
- Keep only live state in `context.md`: current status, next actions, open risks, open questions.
- Add the pointer if it is missing: `> Full history → log.md`

## Step 5 — The dated-line age sweep

Live-state files must not carry a fact that quietly rotted by the calendar. This sweep is keyed
to the date — not to memory, and not to any incoming write.

The supersession sweep runs at *write* time and catches every line a new fact contradicts. What
it cannot catch is the line **no new fact ever arrived about** — the request that simply
fizzled. That residue is what this is for, which is why neither replaces the other.

1. Take Scan 3's output: every dated line in an active project older than 14 days.
2. Surface them as **one list**, and ask per line: **still true / update / drop?**

> **This sweep is uncapped** too. Every flagged line appears in the single list; none are held
> back for a later turn.

Resolutions land in `context.md` the normal way. Do not nag item by item beyond this one pass.

## Step 6 — Report and stop

Name every file written and what changed in each. State the Step 1c counts. State the
supersession result even when it is "nothing". Then stop — no next task proposed.
