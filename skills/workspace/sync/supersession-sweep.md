# The supersession sweep

Binding on `/sync`, `/log-it`, `/done`, and the reconcile step of `/checkout`.

**Adding new information is only half the write. The other half is closing what that
information just killed.** A tracker that only ever grows is a tracker you have to reconcile
by hand later — which is the entire cost this doctrine exists to remove.

---

## 0 — The failure it was written for

A session captured a signed contract arriving from a client. It was appended correctly. But
the task *"forward the dossier for signature"* sat open in the same file, because nothing in
the skill told the agent to ask what the new fact implied about the lines already there.

The contract cannot arrive unless the dossier was sent. The evidence to close the old task
was in the same paragraph that opened the new one, and it went unused for weeks.

The failure is structural, not a slip. Every step in a tracking skill is phrased additively —
*append the entry, add the new items, mark the tasks named in this session*. None of them
looks backward from the new fact to the old line.

## 1 — The trigger

Runs **once per project touched**, after new information has been identified and **before**
any write is committed. Not optional, not conditional on something looking suspicious.

Every new item — a task, a status line, a date, a waiting-on entry, a log bullet — gets one
question asked of it:

> **What in this file can no longer be true, now that this is true?**

## 2 — Search by entity, not by wording

The superseded line almost never shares wording with the new one. *"Forward the dossier for
signature"* and *"contract received"* have no words in common. Matching text finds nothing.

So pull the **entities** out of the new information — person, client, document, deliverable,
project, amount, date — and search the project's `context.md` and `today-tasks.md` for each
one. Every hit is a candidate, whatever it says.

## 3 — The four shapes

Check each candidate against these. They cover every case seen so far.

1. **Entailment.** The new fact is a *later step in the same chain*, so the earlier step must
   have happened. Contract received ⇒ it was sent. Feedback received ⇒ the draft went out.
   Meeting held ⇒ the invite landed. **The most-missed shape, because nobody says the earlier
   step out loud.**
2. **Replacement.** A date, number, name, owner, or venue changed. The old value is still
   quoted elsewhere in the file — often inside a line about something else entirely.
3. **Reversal.** A decision voids a task, a gate, or a deadline. Chase what was back-planned
   from it: killing a gate invalidates every date derived from it.
4. **Duplicate.** The same work is now tracked under new wording. Two live lines for one job.
   The older one gets closed against the newer, never left to age.

## 4 — Two tiers, two behaviours

**ENTAILED — close it, report it.** The new fact is *impossible* unless the old item
happened. Not "probable", not "strongly suggests" — impossible. Close it in the same write
and list it in the confirmation so it can be reversed in one word.

This is a deliberate, narrow carve-out to *preparation is not completion*. It does **not**
license inferring completion from a draft the agent produced, from a plan, or from an
intention. If the chain has a plausible gap — someone else could have sent it, it could have
arrived another way — it is not entailed. Downgrade it.

**LIKELY — present, wait.** Everything else: contradicts-but-doesn't-entail,
probably-stale, looks-replaced. Numbered in the confirm table, pre-marked with the flip the
agent would make. The user rules by number. Never flip one unasked.

Uncertain which tier? It is LIKELY. The tie always breaks toward asking.

## 5 — How to write a close

**Never delete. Never silently flip.** Strike it, name the cause, date it.

```
- [x] ~~Forward the signed dossier~~ — CLOSED (entailed by contract received) 27 Aug
- ~~**Client:** countersigned contract~~ — RESOLVED 27 Aug
- Kickoff ~~5 Sep~~ → **12 Sep** — superseded 27 Aug (client reschedule)
```

- Name **what** superseded it. `SUPERSEDED` with no referent is the same dead end the open
  line was.
- Date every close.
- `log.md` is append-only — never edit a past entry there. Log the supersession as a new
  dated bullet naming the entry it corrects.
- If the close orphans a date something else was back-planned from, mark that date
  **unsound** in its own file in the same pass. Do not invent a replacement.

## 6 — Report it, always

The sweep gets its own line in the skill's confirmation, **even when it found nothing**:

```
Superseded:
- [x] Forward the dossier — CLOSED (entailed by contract received) 27 Aug   ← reverse if wrong
Nothing else superseded.
```

"Nothing else superseded" is a real result and has to be stated. Silence reads as *the sweep
was skipped* — and once that has happened, it is the assumption anyone will make.
