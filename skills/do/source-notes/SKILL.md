---
name: source-notes
disable-model-invocation: true
description: >
  Turn a URL, file, pasted text, or video into a three-layer note — what you can use from it,
  a full structured extraction, and a Cornell-style recall sheet — saved to your library and
  pushed to today's tasks. Use when you intend to act on the source, not just know about it.
---

# Source Notes

Most note-taking on a source produces a summary you never open again. This produces three
things at once, because they answer three different questions:

| Layer | Answers |
|---|---|
| **Learn / Adapt** | What can I actually use from this, and where? |
| **Structured Notes** | What did it say, in full, so I never re-read the original? |
| **Cornell Notes** | Do I understand it well enough to explain it? |

All three are mandatory. The first is the reason to run this instead of `/tldr`.

**Invoke:** `/source-notes <URL, file path, or pasted text>`

## Accepted sources

| Source | How to get the content |
|---|---|
| YouTube URL | Pull the transcript with `yt-dlp` (below). Never write the note from a title, description, or chapter list. |
| Article / blog URL | Fetch the page, extract the main content. If the fetch returns a summary or a paywall stub, say so and ask for a paste. Do not write from partial content. |
| PDF, markdown, text file | Read it directly. |
| Pasted text | Use as-is. Ask where it came from — a note without a source is not a note. |

### Getting a YouTube transcript

```bash
UA="Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0 Safari/537.36"

# 1. What caption tracks exist, and are any human-made?
yt-dlp --no-update --user-agent "$UA" --js-runtimes node --list-subs "<URL>"

# 2. Pull them — a fixed language list, never a wildcard
yt-dlp --no-update --user-agent "$UA" --js-runtimes node --skip-download   --write-subs --write-auto-subs --sub-langs "en,en-orig,en-US,en-GB"   --sub-format vtt -o "src.%(ext)s" "<URL>"
```

Auto-caption VTT is a rolling window — every line repeats the tail of the one before it.
**De-dupe before reading** (strip `<...>` tags, drop timing and header lines, skip any line
already contained in the previous one), or the transcript triples in length and the notes
inherit the repetition.

**When extraction fails, work this order — and do not start at the network.**

| # | Cause | Signature | Fix |
|---|---|---|---|
| 1 | No browser User-Agent | `Video unavailable`, or a "restricted — check with your network administrator" message | Pass `--user-agent` as above |
| 2 | No JavaScript runtime | `No supported JavaScript runtime could be found`, then `Video unavailable` | `--js-runtimes node` (or deno / bun, whichever is installed) |
| 3 | Wildcard in `--sub-langs` | The run writes no file on a video that clearly has captions | Use a fixed list — see below |
| 4 | Caption listing throttled | Zero tracks on every client, or `HTTP Error 429`, while the video's metadata still lists caption tracks | Wait. A different route (e.g. the `youtube-transcript-api` Python package) may still work. Do not retry in a loop — retries *cause* this |
| 5 | Genuinely no captions | The YouTube page's own **Show transcript** panel is empty too | Ask for a transcript |

Causes 1 and 2 both look exactly like a network or policy block from the outside. A network
diagnosis sends the user off to chase their router for nothing, so **never offer one until
1–3 are ruled out.** This order exists because exactly that misdiagnosis once cost an hour:
the evidence was a test that changed the User-Agent and the network route in one step and then
credited the route.

**Never pass a wildcard to `--sub-langs`.** `"en.*"` looks like a safe widening, but yt-dlp
reads it as a regex — on a video whose base track is not English it matches the whole
auto-*translated* set ("English from Chinese", "English from Portuguese", hundreds of rows).
The run writes nothing, looks like a caption failure, and the request volume is what trips the
throttle in row 4.

**Prefer the human-made track; treat auto-caption quotes as approximate.** A manual track can
hide under a randomised language code (`en-` plus a string of characters) that no fixed list
matches — `--list-subs` shows it, and it is worth the extra call when all you hold is the
auto track. Auto captions have no speaker labels and no sentence casing, and they garble proper
nouns and set phrases. If the note is built on auto captions, or the transcript has no speaker
labels on a multi-speaker source, **say so in the note and mark every quotation as
approximate.** On a source whose value *is* its wording, that is a reason to go and get the
manual track.

If nothing works: stop and ask for the transcript. Do not proceed on metadata.

**Never report "this video has no captions" as a fact — the tools cannot establish it.** A tool
returning nothing means only that *it* got nothing, and the two causes take opposite responses:
a genuinely caption-less video needs a transcript from the user, while a broken or throttled
fetch needs fixing and costs them nothing. Report the failure, name which tools failed and how,
and say the cause is undetermined. **Never upgrade "we got nothing" to "there is nothing."**

This is worth the paragraph because it was learned expensively: three extractors all reported
failure on a video that had a full auto-caption track the whole time. One was aborting on format
selection before it ever wrote the subtitle file, and an hour of retries then got caption
*listing* throttled to zero rows on every client — which looks identical to genuine absence.
Rapid repeated retries are what cause the throttle. Diagnose, do not hammer.

## Pre-flight — has this been done already?

Search your notes folder before extracting: the video ID, the URL's domain and path, or a
distinctive phrase from the text. On a match, **stop** and say: *"Already processed:
`<file>`. Open it, or append new notes?"* Do not create a second file.

## The file

Save to `library/source-notes/YYYY-MM-DD_<slug>.md` — slug lowercase, hyphenated, max five
words from the title. If the filename exists, suffix `_v2`. **Never overwrite.**

### Section 1 — Learn / Adapt

The section that decides whether the source changes anything. Read
[capture-doctrine.md](./capture-doctrine.md) before writing it — it defines the three buckets,
the gate each must clear, and where the failures go. It is binding.

```markdown
## Learn / Adapt

### Steal to Teach / Share
### Steal to Adapt
### Steal to Write
```

Every candidate lands in **exactly one** bucket, or drops to Inventory. Omit a bucket heading
with no survivors — never write "none".

**Zero steals is a legitimate outcome.** Write the note with a full Inventory, push nothing,
report *"0 steals, N inventoried."* If three consecutive sources yield zero, say so out loud.
That is a signal about what you are choosing to read, not about the notes.

Filter through the roles in `PROFILE.md`, not through generic interestingness. And **no
manufactured angle**: if the source is not about the thing you are currently preoccupied
with, it is not about it. A passing mention is not a theme.

### Section 2 — Structured Notes

The bar: a reader who sees only these notes can reconstruct the argument, cite its numbers,
explain its frameworks to someone else, and name the tools it named.

```markdown
## Structured Notes

**Source:** [title + author/channel + date + URL]
**Published:** YYYY-MM-DD (or `unknown` — never guess, never ask)
**Length:** [X min / X pages / X words]
**One-line thesis:** [the core argument, one sentence]

### 0. Inventory
[The full enumeration plus every gate failure. On a roundup: every item, numbered, one tight
line each — what it is and the catch. On an argument source: the candidates that failed the
gate. A preserved list, not a pitch. Nothing here gets pushed anywhere.]

### I. [Theme]

**[Concept]** — [2-3 sentences: what it is, how it works, why it matters]
- [supporting detail, example, or data point]
- [the comparison, if one was drawn — both sides, with the specific disparity]
```

Extraction rules:

1. **Every proper noun.** Tools, frameworks, people, companies, products. Named means captured.
2. **Every number.** Metrics, percentages, costs, timescales, headcounts.
3. **Every comparison.** X vs Y, before/after, old way vs new way — both sides, with the gap.
4. **Mechanistic depth.** Not "they use AI for customer research" but "an agent scans 90 days
   of call recordings, CRM notes, surveys and support tickets, then synthesises themes with
   links back to the source artifacts — eight days of research in eight minutes."
5. **Tactical rationale.** When a decision is explained, capture the *why*. "They plan three
   months out because three months now equals three years previously" beats "quarterly planning."
6. **Speaker attribution.** Multiple speakers — record who said what for the key claims.

### Section 3 — Cornell Notes

```markdown
## Cornell Notes

| Cue / Question | Notes |
|---|---|
| [question testing a key concept] | [concise answer from the source] |

### Summary (5-7 sentences)
[A narrative, not a topic list — the argument, its evidence, its conclusion, as you would
brief someone in 60 seconds.]
```

12-20 cue questions. Questions test **understanding, not recall**: *"What is X?"* is weak,
*"Why does X lead to Y instead of Z?"* is strong. Mix definitional, causal, procedural,
comparative, and evaluative.

## Final step — push the steals to today-tasks.md

Mandatory unless zero survived. Append a dated block at the end of `today-tasks.md`; never
merge into an existing one, so each source stays attributable.

```markdown
## Steals to review (from [Author] — "[Short title]" [source date])

Source: library/source-notes/YYYY-MM-DD_<slug>.md

**Teach / Share**
1. **[headline]** `[Free]` or `[Paid $20]` — [what someone can now do, and where you would use it].

**Adapt**
1. **[headline]** — [current way, better way, switch cost].

**Write**
1. **[headline]** — [the argument or story, and the piece it belongs in].
```

**Cap three per bucket.** The remainder stays in the note — nothing is lost, because
Inventory holds it. Omit an empty sub-block rather than writing "none". Never push Inventory.

## Downstream

`/adopt-or-drop` walks these notes later and stamps a `REVIEW STATUS` banner under the H1
once a verdict is given. **Do not add that banner here** — a fresh note is unreviewed by
definition. Leave the H1 clean so the banner has somewhere to go.

## Constraints

- **No shallow summaries.** A concept mentioned is a concept explained.
- **No missing names, no missing numbers.**
- Rough length: Structured Notes 1,500-3,000 words by source density; Cornell 500-800;
  Learn/Adapt 300-500.
- **Never infer a video's content from its metadata.** No transcript means stop and ask.
- Print the saved path in chat. Do not dump the note body — the file is where it gets read.
