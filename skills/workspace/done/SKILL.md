---
name: done
disable-model-invocation: true
description: >
  The lightest completion tier. Marks what was just finished done in context.md and
  today-tasks.md, and sweeps for what that completion made untrue elsewhere. No history
  entry — use /log-it for that, or /sync when the session produced lessons.
---

# Done

Three completion tiers exist. Pick the lightest that fits:

| Skill | Does | Use when |
|---|---|---|
| **`/done`** | Marks done, sweeps for stale. No history. | Routine. Most completions. |
| `/log-it` | The same, plus a permanent `log.md` entry. | A real deliverable worth a record. |
| `/sync` | A reflective pass — learnings plus a full reconcile. | The session produced lessons. |

`/done` deliberately skips `log.md`. That is the trade for being fast. If a completion is
worth remembering in six months, it deserves `/log-it` instead.

**Invoke:** `/done` (infer the completion from the conversation) or `/done <thing>`.

## Step 0 — Trigger guard

Run only when `/done` was actually typed. "Mark it done", "update the file", "ok that's
finished" are direct inline edits, not this skill. Handle those inline.

## Step 1 — Identify the completion

Name exactly what is being marked done. **Typing `/done` is the explicit completion
confirmation** — it satisfies *preparation is not completion* for these items and no others.

- **Scope still applies.** A drafted-but-unsent email is *drafted*, not *sent*. Mark what
  actually happened; do not upgrade the verb.
- If you genuinely cannot tell what was completed, ask **one** question. Do not guess.
- Locate the matching `[ ]` lines in the project's `context.md` and in `today-tasks.md`.

## Step 2 — The sweep

**Read [supersession-sweep.md](../sync/supersession-sweep.md) first — it is binding.**

**Files before the user.** Read the owning `context.md` and resolve everything the file can
answer — items already marked done there, dates that moved, blockers since cleared. Ask only
about the residue. Never hand over a raw list of open items to sort.

**Absence from a tracker is not evidence of absence.** If a workstream or a client has no row
in the file, that is an *untracked-item risk*, not "nothing is owed". Say "this isn't tracked
— verify at the source." Never reason "no row, so no deliverable."

Keep the read boundary tight — the one owning file, no grep-chaining across everything — but
within it, list **every** item matching these five categories, not a selection:

- Open `[ ]` tasks the conversation shows are actually done or superseded.
- Waiting-on items the conversation shows are resolved.
- Dated lines more than two weeks old still quoted as live state.
- Items that now contradict something updated this session.
- **Items superseded by what was just completed.** Pull the entities out of the Step 1
  completion — person, client, document, deliverable, date, amount — search the file for each,
  and test every hit against the four shapes: entailment, replacement, reversal, duplicate.
  **Entailment is the one that hides**: the completion is a later step in a chain, so an
  earlier step must already have happened even though nobody said so.

| # | File | Item | Why stale / what superseded it | Flip to |
|---|---|---|---|---|

Present the table, numbered, and **wait**. Nothing gets flipped unasked.

**One exception: entailed rows.** Where the completion is *impossible* unless the older item
happened, close it in this pass without asking and report it in Step 4 for reversal. Narrow
carve-out. Never applies to a draft the agent produced, and any plausible gap in the chain
downgrades it to a normal row.

If nothing is stale and nothing is superseded, **say both words explicitly** in one line.
Silence reads as a skipped sweep.

## Step 3 — Write

The Step 1 items need no further confirmation — the `/done` was it. Step 2 items do.

1. Mark confirmed items `[x]` in `context.md` and `today-tasks.md`.
2. Strikethrough and tag any resolved waiting-on items that were approved.
3. Update status fields only where the completion makes the old value wrong.

**Do not** write `log.md`, and do not capture learnings. If the session clearly produced a
lesson worth keeping, end with a one-line nudge — *"Worth a `/sync` for that lesson?"* — and
do not act on it.

## Step 4 — Confirm

One tight summary: what was marked done, what stale or superseded items were flipped (or
"none"), which files changed. List entailed auto-closes separately, tagged **"reverse if
wrong"**. No ceremony.
