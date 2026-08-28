# Triage what comes back

Read this before acting on a single returned finding.

## Do not accept-all

**An AI reviewer's false-positive rate runs roughly 3× a human's. What comes back is a
*candidate list*, not a task list.** Accept-all is the second way this gate fails. (The first
is the round-two fold that the Reviewer Contract exists to prevent.)

Sort every finding into exactly one of four:

1. **Real, and yours to fix** → fix it, note the location.
2. **Real, but a design boundary** → it belongs in a Limitations section, not in a rewrite.
   Record it as a deliberate limitation rather than silently absorbing the criticism.
3. **Norm-based and ungrounded** → the reviewer asserts "the field expects X." **Down-rate to
   Minor unless the norm is grounded in a checkable source for *this* field** — a regulation,
   a named reporting guideline, an instruction from someone with authority over the work, a
   cited precedent. Canonical example: a reviewer demanding open-data artifacts from a
   collaboration that legitimately keeps its data internal — correct against a generic
   standard, wrong as a severity judgment for that context. A generic international standard
   is not automatically the norm for your field or market.
4. **Not yours to resolve alone** → tag it `[ESCALATE]` and route it to whoever actually
   decides.

## Decompose bundled complaints

Feedback arrives bundled: "the method section is weak." Before acting, split it into atomic
sub-claims and record who raised each one.

- Silence from a reviewer is **not** agreement and **not** opposition. Record it as
  `not-mentioned`.
- The denominator is the whole group, not the people who spoke. Two of five agreeing is
  *corroborated*, not unanimous.
- A genuine split requires an explicit *conflicting* position, not one person's silence. A
  real split gets escalated, not settled by picking the louder voice.

## Why each contract block exists

So a future session doesn't strip them as clutter.

| Piece | The failure it prevents |
|---|---|
| Rebuttal ladder | Reviewer folds under pushback; the weakness reaches the person who mattered |
| No consecutive concessions | One legitimate concession opens a cascade |
| Anti-anchoring (Step 0b) | Reviewer verifies a prior verdict instead of examining the draft |
| Typed evidence anchors | "The methodology has problems" — unactionable, and often unfounded |
| Coverage receipt | Both failure directions: manufactured findings to fill a quota, and lazy "looks fine" |
| Field-norm grounding | Over-correcting toward standards nobody in your actual field applies |
| Sub-claim decomposition | Over-revising in response to one vague complaint; reading a quiet room as endorsement |
