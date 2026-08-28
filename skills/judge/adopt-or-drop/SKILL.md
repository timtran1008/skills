---
name: adopt-or-drop
disable-model-invocation: true
description: >
  Weekly review of the ideas you saved from books, talks, articles, and courses. Walks each
  unreviewed note one at a time for a keep / already-used / drop verdict, routes what you keep,
  requires a reason on every verdict, and stamps the note so it never resurfaces.
---

# Adopt or Drop

You capture more than you convert. Notes pile up with a "worth trying" list at the bottom that
nobody ever returns to, and every week the backlog gets heavier and less inviting. Reading it
again isn't the answer — **deciding** is.

This skill turns the backlog into decisions you make once. Each note gets a verdict, gets
stamped, and disappears from every future review.

**Invoke:** `/adopt-or-drop` (default window: the last 7 days) or
`/adopt-or-drop since YYYY-MM-DD`.

## Step 1 — Find the unreviewed notes

1. **Run `date` first.** Never assume today.
2. Search your note locations — `library/` and anywhere else the user keeps captured notes.
   Find candidates by file modification time **or** by a date in the filename. Both cases
   happen: a note written late but dated earlier, and a note dated late but edited earlier.
3. **Exclude any file that already contains a `REVIEW STATUS` banner.** Those are decided.
   Never resurface them — this is the entire point of the skill.
4. Exclude index files.
5. If nothing unreviewed remains, say so and stop. **Do not invent sources.**
6. Report the count and where they came from before starting.

Notes older than the stamping habit are invisible to the default window and reachable only
with an explicit `since` date. Never imply the backlog doesn't exist — honour a wider window
when asked.

## Step 2 — Under-mining check

Before reviewing, compare each note's source length against how much was actually captured.

- **A long or flagship source with a thin note** — a three-hour talk yielding two lines, a
  300-page book yielding a paragraph → flag it *before* reviewing:
  > "⚠ `[file]` is a [X]-hour source with only [N] captured items — likely under-mined.
  > Re-read before reviewing, or review as-is?"
- **A richly captured note with few keepers** — do **not** flag. The source was mined properly
  and the ideas didn't clear the bar. That is the system working, not laziness.

Give the user the choice before they pass verdict. A verdict on a badly-mined note is a
verdict on your note-taking, not on the source.

## Step 3 — Check what already happened

For each note, quickly check whether its ideas already got used — in something published,
built, or taught. If so, pre-label it **ALREADY USED** rather than re-pitching material that's
already been consumed.

## Step 4 — Review ONE at a time

Interactive. Concise, numbered, no hedging.

For each note, one compact block, **in this order**:

1. **Title and file.**
2. **A summary FIRST** — 2-4 plain sentences: what the source actually is and its core
   argument. The user almost certainly has no memory of it. **Never open with a list of ideas
   they can't place.** This is mandatory.
3. **The ideas, grouped by bucket**, numbered continuously across buckets so "keep 4" is
   unambiguous. Skip any empty bucket.

   | Bucket | Means |
   |---|---|
   | **Teach / Share** | Material for a session, a talk, a post, a conversation |
   | **Adapt** | Changes how you actually work — a process, a tool, a checklist |
   | **Write** | Belongs in something longer you're writing |

   For each idea, two parts:
   - **Name it** — one short bold phrase.
   - **A plain-English use case.** Explain it the way you'd explain it to a smart beginner.
     Simple words, short sentences, concrete. Say what they would actually *do* with it and
     why that helps. No jargon, no template. **If they'd have to re-read the line to get it,
     it's too abstract — rewrite it plainer.** Comprehension speed is the bar.
4. **Any caveat** in one line, also in plain English.
5. End with: **"Your call?"**

Then **stop and wait**. Do not present the next note until they answer. One question at a
time — never batch.

### Anchor each idea to a role, and don't default to one

Read the user's roles from `PROFILE.md`. Frame each idea in whichever role it genuinely
serves — one idea usually serves exactly one. The failure mode is running everything through
whichever role is most top-of-mind, which makes every source sound like it's about the same
thing.

**No manufactured angle.** If the source isn't about X, don't frame it as being about X just
because X is what the user is currently interested in. A passing mention is not a theme.

### Verdicts

| They say | Meaning | Action |
|---|---|---|
| `drop` / `kill` / `overused` | Rejected | Stamp **DROPPED — <reason>** |
| `keep [n]` | Worth converting | **Route by the bucket the idea is already in** — don't re-derive it. Teach/Share → the ideas file or session material. Adapt → the owning project's Next Actions. Write → the relevant piece's notes. Stamp accordingly. |
| `used` / `already did that` | Already converted | Stamp **ALREADY USED → <where>** |
| `park` | No keepers, but worth holding the quotes | Stamp **PARKED — <reason>** |
| `next` | Skip without deciding | Move on, **no stamp** — it stays in the queue |

**A reason is required on every verdict.** If they drop or park without one, ask once, in one
line: *"Reason? (one phrase)"* — then stamp it.

Accept anything concrete: "too technical", "boring", "already covered", "wrong audience",
"not now". **Do not accept a reason you invented.** If they decline to give one, stamp
**DROPPED — no reason given** and say that this is exactly the case the rule exists to
prevent: a backlog of unexplained rejections tells you nothing about what to stop reading.

**Verdicts belong to the user.** Never auto-decide. Present, wait, stamp.

## Step 5 — Stamp

On any verdict except `next`, prepend directly under the file's H1:

```markdown
> **REVIEW STATUS (YYYY-MM-DD): <VERDICT> — <one-line reason or pointer>. Do not resurface.**
```

Record the bucket a kept idea came from, so routing stays auditable:
`KEPT → <project> Next Actions (Adapt)`, `KEPT (post) (Teach)`.

Rules:
- **Prepend only.** Never edit or delete the captured ideas themselves — the banner records
  the decision *above* the intact note.
- Use the real date from Step 1's `date` call.
- Never overwrite an existing banner. If one exists, Step 1 failed.

## Step 6 — Close with the ledger

After the last note, a compact numbered ledger:

- **Already used:** [note → where]
- **Kept:** [ideas, and where each was routed]
- **Dropped:** [note + reason — every line carries one]
- **Parked:** [note + reason]

Then **one line on the drop pattern** — the most common reason this run, verbatim:
*"3 of 5 dropped as 'too technical'."*

That is a signal about what you're choosing to read, not about the notes. **Surface it. Do
not act on it.** One run is not a pattern; four runs saying the same thing is.

## Constraints

- Never claim a conversion that didn't happen. Only stamp ALREADY USED if you actually found
  the thing.
- Never mark the review "done" beyond what was genuinely stamped.
- Banners prepend; bodies stay untouched.
