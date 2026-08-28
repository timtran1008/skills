---
name: honest-extraction
description: >
  Evidence-first extraction, synthesis, and scoring from provided source material. Use when
  extracting facts, reviewing documents, summarising transcripts, analysing meeting notes,
  scoring against a rubric, or producing structured output where guessing is expensive.
  Every claim is marked explicit, inferred, missing, or conflicted.
---

# Honest Extraction

For extraction where a wrong answer costs more than a blank one.

The default behaviour of a language model reading a source is to produce a complete-looking
answer. Fields get filled. Gaps get smoothed. The output looks the same whether the source
said it or the model assumed it — and that is the whole problem. This skill makes the
difference visible on every line.

## Workflow

1. Restate the extraction target and the allowed sources.
2. Default to **source-bounded** work. Do not use outside knowledge unless explicitly allowed.
3. Assign every field a status: `explicit`, `inferred`, `missing`, or `conflicted`.
4. Require short, auditable evidence for every non-trivial claim.
5. Keep extracted facts separate from interpretation and recommendations.
6. If the source is ambiguous or self-contradictory, surface that — never resolve it silently.

## Core rules

- **A wrong answer is worse than a blank answer.**
- Do not guess when evidence is missing, weak, or conflicting.
- No confidence scores. Status labels and evidence instead.
- Evidence means quotes, snippets, timestamps, page numbers, speaker turns, or section
  references — whatever the source format offers.
- Mark interpretations as interpretations. Never present one as an extracted fact.

## Output schema

| Field | Meaning |
|---|---|
| `field` | The item being extracted, judged, or summarised |
| `value` | The answer, or blank if unsupported |
| `status` | `explicit` / `inferred` / `missing` / `conflicted` |
| `reason` | One sentence: why it is inferred, missing, or conflicted |
| `evidence` | The quote, page, timestamp, or section supporting the value |

- `explicit` — directly supported by the source
- `inferred` — derived from context, not directly stated
- `missing` — not supported by the source
- `conflicted` — the source contains incompatible signals

Save as `{source-filename}-extraction.md` next to the source.

## Reusable prompt

Use or adapt when precision matters:

```xml
<role>
You are performing a high-accuracy extraction and analysis task.
</role>

<rules>
Core rule:
A wrong answer is worse than a blank answer. If the evidence is missing,
ambiguous, or conflicting, do not guess.

Behaviour rules:
1. Use only the provided source material unless I explicitly allow outside knowledge.
2. If a value is not explicitly supported, mark it `missing` or `inferred` rather
   than inventing it.
3. If two parts of the source conflict, mark the field `conflicted`.
4. Keep reasoning short and auditable. Do not hide uncertainty.
5. Confidence scores are not allowed. Use evidence and status labels instead.
</rules>

<output>
For every item, include: field, value, status, reason, evidence.

Status rules:
- explicit:   directly supported by the source
- inferred:   derived from source context, not directly stated
- missing:    the source does not provide enough information
- conflicted: the source provides incompatible signals

Requirements:
- Return a structured table or JSON array.
- Do not omit uncertain items. Include them with the correct status.
- If you infer anything, say exactly what was inferred from what evidence.
- If the task asks for recommendations, separate them from extracted facts.
</output>

<guardrails>
Prefer silence over guessing. A claim you cannot back with evidence is not a value -
it is inferred, missing, or conflicted.
</guardrails>
```

## Variants

**Meeting notes.** Fields: `action_item`, `owner`, `due_date`, `blocker`.
Rule: if an owner or date was not explicitly assigned, leave it blank and mark `missing`.
**Never infer ownership from who spoke most.**

**Interview or coaching transcript.** Fields: `observed_evidence`, `interpretation`,
`gap`, `recommended_action`.
Rule: keep what the person actually did or said separate from what you concluded about it.
Interpretation is not observation.

**Contract or document review.** Fields: `clause_name`, `extracted_term`, `risk_flag`.
Rule: if two clauses disagree, mark `conflicted` and cite both locations.

**Scoring against a rubric.** Add `criterion`, `score`, `anchor`.
Rule: a score with no anchor quote is `inferred`, whatever the number looks like.

## When the ask is analysis, not extraction

Still preserve the three-way separation:

- facts grounded in the source
- interpretations derived from the source
- recommendations layered on top

If a narrative is wanted, produce the structured extraction first, or keep the narrative
explicitly anchored to the schema.
