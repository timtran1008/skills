---
name: for-review
disable-model-invocation: true
description: "Package a finished deliverable plus its full context into one self-contained file, so a different AI can red-team it cold."
---

# For Review — cross-AI red-team package

Package the current session's deliverable into a single markdown file that another model —
one that has never seen this conversation — can consume and attack.

**Why a different model, and a fresh context.** A model that just produced the draft
re-runs the reasoning it already did, and inherits the blind spots that produced the flaw.
Self-review is proofreading your own essay. This is the single highest-leverage habit in
the repo and it costs one copy-paste.

The output file has three sections: **Context Brief**, **The Deliverable**, **The Ask**.

## Step 0 — Identify the deliverable

State back to the user:
1. What is the final product? (file path, or content produced in conversation)
2. What project or piece of work does it belong to?

If ambiguous — several outputs in one session, or no clear final product — ask. Do not guess.

## Step 0b — Anti-anchoring: what must NOT go in

**Send the draft and the brief. Send nothing else.**

Never include:

- **Your own review, critique, or self-assessment of the draft.**
- **The user's own suspicion of where the weakness is** ("I think section 3 is thin"). If they
  volunteer one while you're building the package, keep it out of the file and tell them you did.
- **The rubric or evaluation criteria** — when the reviewer is being asked to *find problems*
  rather than *score against a known standard*. If the ask genuinely is "score this against
  the rubric," the rubric goes in and this doesn't apply.

**Why:** a reviewer handed a prior verdict anchors to it and verifies the prior instead of
examining the draft. One-line change, almost everyone gets it wrong, free to fix.

**Related and worth knowing separately:** do not draft in the same session where the rubric
was pasted. A model that has seen the rubric while generating orients toward its surface
features. Draft in one session, evaluate in a fresh one. Separate invocations, not just
separate instructions.

## Step 1 — Section 1: Context Brief

Reconstruct from the conversation:

- **Original request** — in the user's own words; quote where it matters
- **Why it matters** — audience, stakes, the "so what"
- **Constraints** — what must or must not be included
- **Key decisions** — major choices and why, including rejected alternatives
- **Revisions** — what changed, was cut, or was reworked, and why
- **Honest uncertainty** — what you are *not* confident about, flagged explicitly

Rules:
- Write for a reader with **zero** prior context.
- Be specific: names, dates, numbers, paths. Not vague summaries.
- Separate **facts** (what the user said) from **your interpretations**.
- Where context is thin, say so: "Context is thin here — you may want to ask about X."

## Step 2 — Section 2: The Deliverable

- If it's a file: read it, embed it verbatim.
- If it was produced in conversation: copy the final version exactly.
- **Do not edit, improve, polish, or summarise.** Verbatim only.
- Wrap it in a clear delimiter so the reviewer knows where it starts and ends.

## Step 3 — Section 3: The Ask

### Required — the Reviewer Contract goes FIRST

The known failure of this gate is **round two**: the user explains why the reviewer is wrong,
the reviewer says "you're right, good point," and the real weakness survives all the way to
the person who mattered. The cause is that a model's training rewards conversational harmony,
so persistence gets read as evidence. This contract is the fix. Paste it verbatim.

```
REVIEWER CONTRACT — read before reviewing.

1. REBUTTAL SCORING. When I push back on a finding, score my rebuttal 1-5 and let the
   score decide your action. Do not let my tone decide it.
     5 = new evidence or logic that directly dismantles the finding  -> WITHDRAW it
     4 = substantially weakens it, minor gaps remain                 -> DOWNGRADE severity
     3 = partially addresses it, the core survives                   -> HOLD, name what is unaddressed
     2 = tangential, answers a related but different point           -> RESTATE, name the deflection
     1 = assertion without evidence, or repetition                   -> STRENGTHEN with a new angle
   Log every one: [REBUTTAL: finding #X | score Y/5 | action | one-line reason]

2. NO CONSECUTIVE CONCESSIONS. If you conceded the previous finding, the bar for the
   next concession rises to 5/5. A 4/5 rebuttal after a concession is a HOLD.

3. PRESSURE IS NOT EVIDENCE. Me pushing back three times with the same argument does
   not raise its score. Do not soften language, add caveats, or apologise to restore
   agreement. Restate the finding once and stop.

4. CONCESSION-RATE SELF-AUDIT. If you have withdrawn or downgraded more than half of
   your findings, say so explicitly: "I have conceded most of my findings - either the
   draft genuinely improved, or I am accommodating. Verify this yourself."

5. REGISTER INDEPENDENCE. A polite finding is not thereby a minor one, and an
   aggressive one is not thereby major. Severity is decision impact only.

6. SYMMETRIC BURDEN. "This section is fine" carries the same evidence burden as "this
   section is broken." Do not wave sections through for free.
```

### Required — the Finding Contract, immediately after

```
FINDING FORMAT. Every weakness you report carries exactly three things.

(1) SEVERITY, by decision impact alone:
    CRITICAL - this defect alone, uncorrected, invalidates a core claim
    MAJOR    - materially weakens confidence in a core claim; needs substantial rework;
               the core survives
    MINOR    - quality or clarity improves if fixed; core claims unaffected
    Rules: assign each finding the band its own impact justifies - never inherit a band
    from the cluster it sits in. If a defect needs sibling findings to reach
    rejection-level impact, it is not CRITICAL alone. There is no expected number of
    findings in any band.

(2) EVIDENCE ANCHOR, typed, one per finding:
    text:     p.12 "verbatim quote, 25 words max"
    table:    Table 3 - a percentage reported with no denominator
    figure:   Figure 2 - axis unlabelled
    absence:  Method - expected a sampling statement; checked section 3, 4, appendix
    A CRITICAL or MAJOR claim you cannot anchor is not yet a finding. Either do the check
    that produces the anchor, or move it to "Questions for the author."
    An "absence" anchor must name where you looked, or it is not checkable.

(3) CONFIDENCE 1-5, with a competence basis:
    "4 - core expertise: survey methodology"   "2 - adjacent field: applying general standards"

COVERAGE RECEIPT. If your strengths list or your weaknesses list is empty, you must say
what you examined and why nothing was found:
    | Dimension examined | What you checked | Basis for "nothing found" |
An empty list with no receipt is not a valid review.
```

### Then the red-team prompt

```
## Your Task

You are reviewing this as an independent red-team reviewer. The author produced the
deliverable above with an AI collaborator. Your job is to challenge it.

**Do this:**
- Challenge the logic, structure, and completeness
- Find blind spots, weak arguments, and missing perspectives
- Flag anything that contradicts the stated context or misfits the audience
- Check internal consistency - does the product match what was asked for?
- Be direct and specific - name the problem, explain why it matters, suggest a fix
- If something is genuinely strong, say so in one line and move on

**Do NOT do this:**
- Don't say "this is great but..." - lead with the issue
- Don't repeat the context back - go straight to findings
- Don't hedge - if it's wrong, say it's wrong

**Output format:**
1. Critical issues (must change before this ships)
2. Weak spots (would improve it, not blockers)
3. Missing (perspectives, data, or arguments not considered)
4. Verdict (one sentence: ready, almost ready, or needs rework?)
```

### Required — 6-10 specific things to red-team

Generic prompts produce generic findings. Naming the load-bearing weaknesses upfront is what
turns platitudes into usable critique. Always append:

```
**Specific things to red-team hard (not exhaustive - find your own too):**

- [load-bearing assumption #1, named explicitly]
- [a specific number / threshold / target - is it defensible, or is "why X, not Y?" fatal]
- [a specific framework or model applied - does it fit, or has it been force-fitted]
- [the audience or stakeholder assumption - does it map to reality]
- [a measurement or validation claim - does the instrument measure what it claims]
- [a cross-reference or dependency - does this work standalone or break]
- [anything flagged as uncertain in Section 1 - is it visible in the deliverable itself,
   or only in the brief]
- [anything in the deliverable that contradicts the stated context or constraint]
```

**How to find the right 6-10:**

| In the deliverable | Ask |
|---|---|
| A number, threshold, or target | Is this defensible if challenged? |
| A named framework or model | Operationalised for *this* audience, or used as a slogan? |
| A time estimate or scope | Realistic, or wishful? |
| A measurement plan | Does the instrument measure what it claims? |
| An audience or role definition | Does this map to reality on the ground? |
| A cross-reference or handoff | Does the deliverable work if the reader has only this document? |
| Anything you flagged as uncertain | Is the uncertainty visible in the deliverable, or hidden in the brief? |

## Step 4 — Assemble and save

```markdown
# For Review: {topic}

**Date:** {YYYY-MM-DD}
**Project:** {name}
**Reviewer:** {which model this is going to}

---
## 1. Context Brief
---
## 2. The Deliverable
---
## 3. Your Task
```

Save as `for-review-{topic}-{YYYY-MM-DD}.md` next to the deliverable. Topic is 2-4 lowercase
hyphenated words. **Never overwrite** — append `-v2`, `-v3` if the name exists.

## Step 5 — Hard brake

Show the file. Ask: **"Review package ready. Want to check it before sending?"**
Mark nothing done. Propose no next step.

## Step 6 — When the review comes back

**Do not accept-all.** See [`triage-returned-findings.md`](./triage-returned-findings.md) —
read it before acting on a single finding.

## Edge cases

| Scenario | Action |
|---|---|
| No clear final product | Ask. Do not guess. |
| Multiple deliverables | Ask which. Run once per deliverable. |
| Product is a file | Read it, embed verbatim, include the path in the brief. |
| Thin conversation context | Reconstruct what exists, flag the gaps explicitly for the reviewer. |
| "Skip the context" | Still include 2-3 lines. The reviewer needs something. |
