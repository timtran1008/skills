---
name: fact-check
description: >
  Post-generation QA for AI output. Runs countable, binary, and logical-consistency checks
  against source material or stated requirements, and identifies where human judgment is
  needed without answering it. Use when asked to QA a deliverable, verify output, or check
  something against a source.
---

# Fact-Check — three-layer QA

Catch the errors a human should not have to waste attention finding. The highest-value case
is checking a *different* model's output.

**The agent checks layers 1-3. The human checks layer 4.**

## Sibling skill

| | `honest-extraction` | `fact-check` |
|---|---|---|
| **Purpose** | Extract facts FROM a source | Verify output AGAINST a source |
| **Direction** | source → structured data | output + source → pass/flag report |
| **Labels** | explicit / inferred / missing / conflicted | pass / flag / missing / conflict |
| **When** | Before the work — understand the inputs | After the work — verify the outputs |

"What does this source say?" → `honest-extraction`.
"Does this output match what it should say?" → here.

## The layers

| Layer | What | Method | Speed |
|---|---|---|---|
| 1 — Countable | Numbers, dates, names, quantities, totals, units | Exact match against source or stated requirement | Seconds |
| 2 — Binary | Required sections present? Salutation correct? Format followed? Attachments referenced? | Exists or doesn't | ~1 minute |
| 3 — Logic | Flow holds? No contradictions? No redundancy? Cause precedes effect? | Sequential read + cross-reference | ~5 minutes |
| 4 — Judgment | Priorities, trade-offs, "it depends" | **Identified, never answered** | — |

## Workflow

1. **Identify the source of truth.** The brief, spec, requirement, or context file. If none
   is provided, ask. If none exists, state that the check is requirement-bounded only, and
   proceed with what's available.
2. **Layer 1.** Extract every number, date, name, quantity, and unit from the output.
   Cross-check each against the source. Flag mismatches and anything unverifiable.
3. **Layer 2.** Check every required element — sections, salutation, sign-off, references,
   attachments, formatting rules, mandated terminology. Flag what's missing or misapplied.
4. **Layer 3.** Read top to bottom. Flag logical jumps (A to C with no B), internal
   contradictions, redundancies, cause-effect breaks, and claims that go beyond what the
   source supports.
5. **Surface layer 4.** List the 2-3 decisions in the output that depend on context or
   priorities not present in the source. **Do not answer them.** Frame each as: "Is this what
   you intended?"
6. **Output the report.**

## Core rules

- **A wrong "pass" is worse than a false flag.** When in doubt, flag.
- Do not resolve ambiguity silently. Surface it.
- Do not decide layer 4. Identify where it lives, then stop.
- **Fixes come after the report, never inside it.** Deliver the report first. Propose fixes
  only if asked.
- Use direct quotes, line numbers, or section references as evidence.
- No confidence scores. Status labels only: `pass`, `flag`, `missing`, `conflict`.

## Output

```markdown
# Fact-Check Report

**Source:** [what it was checked against]
**Output:** [what was checked]
**Checked by:** [model + date]

## Layer 1 — Countable
| Item | Output value | Source value | Status | Note |
|---|---|---|---|---|

## Layer 2 — Binary
| Required element | Present? | Status | Note |
|---|---|---|---|

## Layer 3 — Logic
| Location | Issue type | Description | Status |
|---|---|---|---|

## Layer 4 — Judgment (for the human)
| Decision point | Why this needs you |
|---|---|

## Summary
- Layer 1: X/Y passed
- Layer 2: X/Y present
- Layer 3: X flags
- Layer 4: X items for review
```

Save as `{source-filename}-factcheck.md` next to the file checked.

## Variants

**Email.** L1: recipient name, dates, amounts, reference numbers. L2: salutation, sign-off,
CC list, attachment mentioned, register matches. L3: the ask-to-action flow, no contradictory
commitments.

**Report or deck.** L1: data points, chart labels, page numbers, citations. L2: required
sections per template, branding, disclaimer. L3: executive summary matches the body,
recommendations follow from the analysis.

**Training or session design.** L1: session durations sum correctly, dates match the calendar,
headcount. L2: objectives stated, assessment method defined, materials listed. L3: day-to-day
progression holds, no topic repeated, difficulty actually ramps.

**Contract or policy.** L1: dates, amounts, notice periods, defined terms used consistently.
L2: required clauses present. L3: no clause contradicts another; defined terms defined before
first use.

## The two-agent workflow

The highest-value use of this skill:

| Step | Who | Role |
|---|---|---|
| 1. Do the work | Model A | Drafts from brief + context |
| 2. Fact-check | **Model B** | Runs this skill against source + output |
| 3. Review | You | Reads layer 4 flags only. Approves or rejects. |

**Why a different model?** Same reason you don't proofread your own essay — same weights,
same biases, same blind spots. And the checker must work from a **fresh context**, not the
conversation that produced the output: a same-session self-check re-runs work the model
already did and inherits the error that caused the problem.

Ready-to-paste prompt for the checker: [`cross-ai-qa-prompt.md`](./cross-ai-qa-prompt.md).
