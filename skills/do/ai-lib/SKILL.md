---
name: ai-lib
disable-model-invocation: true
description: >
  Save an article, video, or reference to your library with minimal friction — a distilled
  card, an index row, and whatever came out of it that is worth acting on. Built for reading
  mode: fast, comprehensive enough that you never re-open the original.
---

# Library — save an entry

You are reading, not working. This should cost you one command and one confirmation.

What it produces: one entry file in `library/<folder>/`, one row in `library/INDEX.md`, and —
if anything survived the gate — a block appended to `today-tasks.md`.

**Invoke:** `/ai-lib <URL, or pasted text, or a URL plus your own commentary>`

## Step 1 — Identify the source

| Input | Action |
|---|---|
| Article URL | Fetch it. Extract title, author, publication, full content. |
| YouTube URL | Pull the full transcript with `yt-dlp` — never metadata only. |
| Pasted text | Use as-is, then **ask where it came from** before writing anything. |
| URL plus commentary | Fetch, and keep the commentary — it belongs in the body or in an idea, not in a section of its own. |
| "Save what we discussed about X" | Distil the thread, then ask for the original source. |

**Capture the publish date.** Byline, upload date, PDF date — it feeds the recency gate. If
it is genuinely not stated, write `**Published:** unknown` and run the other gate criteria.
Never guess a date and never ask for one.

**Source attribution is mandatory.** Author, publication, URL, clickable. No source, no entry.

**If the fetch returns partial content**, try once more with an explicit "return the complete
text, every paragraph" instruction. Still partial means paywalled: say so and ask for a
paste. **Do not write an entry from partial content.** If the fetch fails outright, say so
and ask. Do not fill the gap from memory.

## Step 2 — Capture the whole thing

**Do not summarise, do not truncate, do not skip sections.** The entry should be
comprehensive enough that the original is never needed again.

- **Core argument** — one to three sentences at the top.
- **Every key concept, framework, data point, and named entity**, under clear headers.
- **All specific numbers, quotes, and evidence** — this is why the entry exists.
- **Inventory** — the full enumeration plus every candidate that failed the gate.
- **Learn / Adapt** — see Step 5.

A very long source gets more headers, not less content. If a quick summary card is wanted
instead, the user will say so.

## Step 3 — Classify

One subfolder. If it spans two, pick the primary. If it fits none, say so and propose a name
— never create a folder unasked.

| Folder | Signal |
|---|---|
| `skills/` | skill design, agent architecture, orchestration, tool use |
| `prompting/` | prompt and context engineering, system prompts, specs |
| `strategy/` | org adoption, ROI, change management, enterprise deployment |
| `tools/` | named products, launches, updates |
| `cases/` | a company plus what they actually did |
| `coaching/` | teaching it, workshop design, diagnostics, adoption frameworks |

Then 3-6 lowercase hyphenated tags. Tags differentiate entries *within* a folder.

## Step 4 — Duplicate check

Read `library/INDEX.md`. Look for the same URL, the same author on the same topic, or a very
similar title.

**On a match: skip. Do not write, do not ask.** Name the existing entry, list in two to four
bullets what the new source carries that it does not — so a merge is possible later — and
stop. Nothing is written to the entry file, the index, or today's tasks.

- An article and its video twin are duplicates: same framework, same evidence.
- A prompt kit already distilled into an entry is a duplicate, even handed over raw.
- Override only on an explicit "update it" or "save it anyway".

## Step 5 — Write the entry

Filename `YYYY-MM-DD-short-slug.md`, two to four words, lowercase, hyphenated.

```markdown
# [Title]

**Source:** [author / publication — URL]
**Published:** YYYY-MM-DD (or `unknown`)
**Saved:** YYYY-MM-DD
**Tags:** [comma-separated]

---

[The distilled body — core argument first, then every concept, framework, number and quote
under clear headers.]

## Inventory

[The full enumeration plus every gate failure. On a roundup: all items, numbered, one tight
line each — what it is and the catch. A preserved list, not a pitch.]

## Learn / Adapt

### Steal to Teach / Share
### Steal to Adapt
### Steal to Write
```

**The gates are binding** and live in
[capture-doctrine.md](../source-notes/capture-doctrine.md) — read it before writing this
section. The short version:

| Bucket | Passes only if |
|---|---|
| **Teach / Share** | Published within ~60 days · not already in `INDEX.md` · a non-technical person could do it with tools they already have · it lands in a real session or channel |
| **Adapt** | It names the specific documented current way (an SOP step, a named `SKILL.md`) · says what is worse about it · states the switch cost |
| **Write** | It binds to a live section of something being written · it is an argument, story, or line, not a concept |

Anything failing its gate goes to Inventory. Exactly one bucket per item — dual-listing is
how padding returns. Omit an empty bucket heading; never write "none". Highest-leverage
first. The procedure for generating and filtering candidates, with worked passes and fails,
is in [learn-adapt-guide.md](./learn-adapt-guide.md).

**Zero is a legitimate outcome.** Write the Inventory, push nothing, report *"0 steals, N
inventoried."* Three consecutive zero-yield sources — say so; that is about the reading, not
the notes.

**Pure reference** — a spec, a changelog, API docs with no argument to adapt — gets
`N/A — reference material` under Learn / Adapt and no subsections. The Inventory is still
written. Only skip for a true reference. **Never write filler. Blank beats wrong.**

## Step 6 — Update the index

Append one row to `library/INDEX.md`:

```
| YYYY-MM-DD | [Author — Title (brief distinguishing detail)] | [folder] | [tags] | [folder/filename.md](folder/filename.md) | |
```

Keep the title cell scannable; include the author name for searchability. Leave the
`Reviewed?` column empty — `/adopt-or-drop` fills it.

## Step 6b — Push what survived

Append a dated block at the end of `today-tasks.md`. Never merge into an existing block —
one per invocation, so sources stay attributable.

```markdown
## Steals to review (from [Author] — "[Short title]" [source date])

Source: library/<folder>/<filename>.md

**Teach / Share**
1. **[headline]** — [what someone can now do, and where you would use it].

**Adapt**
1. **[headline]** — [current way, better way, switch cost].

**Write**
1. **[headline]** — [the argument or story, and the piece it belongs in].
```

Cap three per bucket. Never push Inventory. Skip this step entirely on a reference entry or a
zero-yield source, and say *"0 steals, N inventoried — nothing added to today-tasks."*

## Step 7 — Hard brake

Report: file saved (path), folder and tags, index row added. Then ask:

> "Entry saved. Ready for review?"

Do not propose the next task. Do not mark anything done. The user is reading, not working.

## Edge cases

- **Several URLs at once** — one entry each, **capped at five per invocation**. Save the
  first five, list the rest, ask before continuing. One combined hard brake.
- **"Save this" with no source** — ask where it is from before writing anything.
- **Content outside the library's subject** — say so and suggest a better home rather than
  bending the taxonomy.
