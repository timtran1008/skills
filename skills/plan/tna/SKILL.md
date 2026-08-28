---
name: tna
disable-model-invocation: true
description: >
  Training needs analysis with a gatekeeper on the front. Diagnoses whether the request is
  actually a skill gap before any design happens, then builds the rubric, tests the requester's
  assumptions, and produces learning outcomes and a validation survey.
---

# Training Needs Analysis

Most training requests arrive already solved: *"they need a workshop on communication."* The
request names the intervention, not the problem. This skill refuses to design until it knows
which problem it is looking at — because training is the wrong fix for most of them.

**Invoke:** `/tna <the request as it arrived>`

## The gatekeeper — skill gap or something else?

**Before any analysis, diagnose the cause.** Three questions, in order:

1. **"If their life depended on it, could they do it correctly?"**
   - Yes → **not a skill gap.** Training will not help.
   - No → possible skill gap. Continue.
2. **"Have they done it correctly before?"**
   - Yes → they have the skill and are not using it. Not a training problem.
   - No → skill gap confirmed. Proceed.
3. **"What happens when they don't do it correctly?"**
   - Nothing → a motivation or environment problem.
   - A real consequence exists and the behaviour continues anyway → dig further; something is
     rewarding the wrong behaviour.

```
              Request for training
                       │
    "Could they do it if their life depended on it?"
                       │
              ┌────────┴────────┐
             YES                NO
              │                  │
       NOT A SKILL GAP   "Have they done it correctly before?"
              │                  │
              │           ┌──────┴──────┐
              │          YES            NO
              │           │              │
              │     MOTIVATION      SKILL GAP
              │           │              │
              ▼           ▼              ▼
        Feedback     Remove barriers   Proceed
        Incentives   Clarify expectations  with TNA
        Remove obstacles  Consequences
```

### The refusal

When training is not the answer, say so:

> "From what you've described this looks like a **[motivation / environment]** problem rather
> than a skill gap, and training won't move it. What would: **[the specific alternative — a
> feedback conversation, a process change, removing the obstacle]**.
>
> Happy to help you think that through instead. Or if you think there *is* a skill gap I'm
> missing, tell me what specifically they cannot do."

**Proceed only when a skill gap is confirmed, or the requester explicitly overrides.** Record
the override — it belongs in the post-mortem when the training does not fix the problem.

---

## The analysis

Pause after each step and wait for confirmation. Do not run ahead.

### Step 1 — Define the skill

*"What specific skill are we focused on?"* Push until it is observable. "Communication" is not
a skill. "Giving corrective feedback to a direct report" is. "Handling an angry customer on the
phone" is.

### Step 2 — Gather the context

| Input | Format |
|---|---|
| Industry | Short answer |
| Job role | Multiple choice, options drawn from the context |
| Experience | `<1 year` / `1-3` / `3-5` / `5+` |

### Step 3 — Build the five-level rubric

Steps are **observable criteria** — what a person does. Levels are **behaviour examples** — how
well they do it.

| Step | 1 (Novice) | 2 | 3 (Competent) | 4 | 5 (Expert) |
|---|---|---|---|---|---|
| [observable action] | [behaviour] | [behaviour] | [behaviour] | [behaviour] | [behaviour] |

- Every step measurable and observable.
- Clear progression between levels — not the same sentence with "better" added.
- Concrete behaviours, never vague descriptors.
- **Level 3 is the minimum acceptable standard.** Level 5 is aspirational but real.

### Step 4 — Locate the gap

For each step, ask for the **current** level and the **target** level. Only steps with a gap
need learning outcomes. This is usually where a five-day programme becomes a two-hour session.

### Step 5 — Test the assumptions

The requester's diagnosis is a hypothesis. Surface it:

> "Do you think your learners **[the belief]**, or could it be that **[the blind spot]**?"

- *"...know what good feedback looks like, or could it be that they have never once seen it
  modelled?"*
- *"...are resisting the new process, or could it be that nobody explained why it changed?"*

Ask for honest answers. One of these usually changes the design.

### Step 6 — Write the learning outcomes

For each gap step:

| Step | Current | Target | Outcome |
|---|---|---|---|
| [step] | L2 | L4 | "By the end, learners will be able to **[verb] + [observable action] + [condition]**" |

Verbs by level: *remember* — list, recall, identify · *understand* — explain, summarise,
interpret · *apply* — demonstrate, use, implement · *analyse* — compare, differentiate,
examine · *evaluate* — assess, critique, justify · *create* — design, construct, develop.

### Step 7 — The validation survey

Ten multiple-choice questions plus two short-answer, completable in under ten minutes. It
should validate the assumed gaps, surface barriers nobody named, and gauge readiness.

Include a covering description:

> "We're designing training on **[skill]** and want to make sure it's relevant to what you
> actually deal with. This takes ten minutes, and your answers shape the content."

---

## The five-minute version

When the requester will not sit through the full analysis, offer this instead of skipping it:

1. What specific behaviour do you want changed? (one sentence)
2. What happens now, and what should happen instead?
3. Have they been trained on this before?
4. What does it cost the business if it doesn't change?
5. Who are the learners — role, level, group size?

Enough to design a focused session without full rubric development. Say plainly what it
trades away.

## Boundaries

- **Never skip the gatekeeper.** It is the entire value of the skill.
- Never design training for a motivation problem.
- Never proceed to the next step without confirmation.
- **Stop at the analysis.** Do not suggest content or a delivery plan — that is `/pmlt`.
- Never assume the requester diagnosed it correctly, and be willing to push back respectfully
  when training is not the answer.
