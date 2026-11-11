# Cross-AI QA prompt

Paste this into a **different** model than the one that produced the output, in a **fresh**
conversation.

```xml
<task>
Verify the AI-generated output below against the source material and
requirements, using the layered check in <instructions>: trace every
countable to the source, check each required element exists, then read
for logic breaks. Check facts, not taste. Catch the errors the human
should not waste time finding.
</task>

<source>
[PASTE: the original brief, spec, context file, or requirements]
</source>

<output_to_check>
[PASTE: the AI-generated output to verify]
</output_to_check>

<instructions>
Run 3 layers of verification. Do NOT skip any layer.

LAYER 1 -- COUNTABLE
Extract every number, date, name, quantity, and unit from the output.
Cross-check each against the source. Flag any mismatch, inconsistency,
or item that cannot be verified from the source.

LAYER 2 -- BINARY
Check that every required element exists: sections, salutation, sign-off,
referenced attachments, formatting rules, mandated terminology.
Flag anything missing or incorrectly applied.

LAYER 3 -- LOGIC
Read the output from start to end. Flag:
- Logical jumps (conclusion without supporting argument)
- Internal contradictions
- Redundancies (the same point made twice)
- Cause-effect breaks (stated outcome does not follow from stated action)
- Claims that go beyond what the source supports

LAYER 4 -- JUDGMENT (do NOT answer these)
List 2-3 decisions in the output that depend on priorities, context, or
judgment not present in the source. Frame each as a question for the
human: "Is this what you intended?"

Output format: a structured table per layer.
For each flag: quote the specific text, cite the source contradiction,
and mark status with the emoji alone, no word: 🟢 = matches source ·
🔴 = mismatch, contradiction, or missing element · 🟡 = unverified,
interpretation, or a judgment call for the human.

End with a summary count per layer.
</instructions>

<rules>
- A wrong "pass" is worse than a false flag. When in doubt, flag.
- Do NOT resolve ambiguity. Surface it.
- Do NOT make Layer 4 decisions. Identify them and stop.
- No confidence scores. No hedging. Flag or pass.
- No preamble. No "Great output!" Start with Layer 1.
</rules>
```
