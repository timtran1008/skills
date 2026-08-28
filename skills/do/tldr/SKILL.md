---
name: tldr
disable-model-invocation: true
description: >
  Notes only. Distils a URL, file, pasted text, or video into bulleted notes grouped by the
  argument the source is making — no recommendations, no action items, no follow-up. Use when
  you want to know what a source said. Use /source-notes when you want to use it.
---

# TLDR

One layer: what the source itself argues, in the source's own terms.

**Invoke:** `/tldr <URL, file path, or pasted text>`

`/tldr` distils a source so you can read, cite, or reference it. It does **not** mine the
source for things you should adopt. For that — Learn/Adapt, the three idea buckets, recall
questions, a push to today's tasks — run `/source-notes` instead.

**This is the whole rule.** No `Learn / Adapt` section. No recommendations. Nothing about
what you should do with the source. If the extraction is good, the source speaks for itself.
Do not smuggle advice in as an aside, a framing, or a "note the relevance to..." line.

**A bullet is not a recommendation.** Every bullet is a claim, principle, or prescription
**the source makes**, in the source's own terms. Never ranked by usefulness to you, never
connected to your projects. The test: if a line cannot be traced back to a specific moment in
the source, it does not go in the file. Never write "worth applying to", never write "you
should".

## Accepted sources

| Source | How to get the content |
|---|---|
| YouTube URL | `yt-dlp` transcript — see below. Never write from title, description, or chapters. |
| Article / blog URL | Fetch and extract the main content. Partial or paywalled means stop and ask for a paste. |
| PDF, markdown, text file | Read it directly. |
| Pasted text | Use as-is. |

### Diagnose a YouTube failure before declaring it

"No transcript" is two different failures with different fixes.

```bash
yt-dlp --no-update --extractor-args "youtube:player_client=ios,tv,mweb" --list-subs "<URL>"
```

- **Caption tracks are listed but the fetch failed** → an access or IP problem. Pull the
  track directly.
- **`has no automatic captions` / `has no subtitles`** → the uploader disabled captions on
  that upload. No amount of retrying that video ID will work. Try a mirror.

**The mirror route.** Lectures, talks and interviews from big channels are widely
re-uploaded, and mirrors usually have auto-captions on even when the official upload does not.

```bash
yt-dlp --no-update --skip-download --flat-playlist \
  --print "%(id)s | %(title)s | %(channel)s | %(duration_string)s" \
  "ytsearch12:<exact video title>"
```

Pick a candidate whose **duration is within a couple of minutes of the original** — that is
what distinguishes a full mirror from a clip. Check its captions, then pull them:

```bash
yt-dlp --no-update --skip-download --write-auto-subs --sub-langs "en,en-orig" \
  --sub-format vtt -o "src.%(ext)s" "https://youtu.be/<MIRROR_ID>"
```

Auto-caption VTT is a rolling window — every line repeats the tail of the one before it.
**De-dupe before reading**: strip `<...>` inline tags, drop cue-timing and header lines, and
skip any line already contained in the previous one. Skip this and the transcript triples in
length and the notes inherit the repetition.

**Provenance is mandatory when the notes come from a mirror.** Name the mirror ID, its
duration, and any timestamp offset in the header block. A future reader must be able to tell
that the timestamps do not match the URL on the `Source:` line.

**Never use a clip, a re-cut, or a highlights version.** If only clips have captions, that is
a failed extraction — stop and ask.

## Pre-flight — is notes-only the right call?

Gauge the source first. **If it is long or flagship — over ~90 minutes, over ~15 pages, or a
marquee thinker — stop and confirm:**

> "This is a [X]-hour source. `/tldr` gives notes only — nothing extracted that you could
> use. On something this dense that leaves the applicable material unmined. Run
> `/source-notes` for the full extraction, or `/tldr` anyway?"

`/tldr` deliberately captures nothing applicable. That is correct for a source you want to
know about and wrong for one you want to use, and on a flagship source the difference is
expensive — it forces a re-mine later.

**Ask once, and only once.** If the next message pushes on something else — fixing the
extraction, supplying a transcript, "try again" — that is the user proceeding with `/tldr`,
not an unanswered question. Do not re-raise it after the transcript lands.

## Pre-flight — duplicate check

Search the notes folder for the video ID, the URL's domain and path, or a distinctive phrase.
On a match, **stop**: *"Already processed: `<file>`. Open it, append, or upgrade with
`/source-notes`?"*

## The file

Save to `library/source-notes/YYYY-MM-DD_<slug>_tldr.md`. The `_tldr` suffix distinguishes it
in a folder listing. If the filename exists, suffix `_v2` — **never overwrite**.

```markdown
# [Source title]

> **REVIEW STATUS (YYYY-MM-DD): N/A — notes only, nothing captured to act on.**

**Source:** [title + author/channel + date + URL]
**Length:** [X min / X pages / X words]
**One-line thesis:** [the core argument, one sentence]
**Transcript provenance:** [only if the transcript did not come from the URL above — mirror
ID, its duration, the timestamp offset]

## [Argument section — names the move the source is making, never a timestamp]

- **[Bolded claim.]** [The claim, its mechanism, and the specifics that carry it.]

**Named but lesson-free:** [sponsor reads, plugs, housekeeping — one line, only if present]
**Caption caveats:** [garbled names, unrecoverable words — one line, only if present]
```

**Group by argument, not by transcript position.** Sections are named for the move the source
is making — "Why bonding is the default", "The data he leans on", "Practice two: become a
social scientist". If a source returns to a topic three times, those points merge into one
section. Within a section, run roughly in the order the source made them. Audience Q&A gets
its own section at the end.

**Lead each bullet with its point in bold**, so the file is skimmable at the bold layer alone
and readable in full at the second.

The goal: **the argument, reconstructed — not the transcript, compressed.**

## Extraction rules

1. **Distil, don't transcribe.** The failure this format exists to prevent is a
   sentence-by-sentence rewrite. If a bullet exists only because the speaker said a sentence
   there, cut it. Two sentences making one claim are one bullet.
2. **But don't strip it to the skeleton either.** A file of load-bearing claims alone is too
   thin — it throws away exactly what made the source worth watching.
3. **The test for keeping a detail: is it surprising, quantified, named, or memorable?** If
   yes it earns **its own bullet**, not a parenthetical inside another one. An illustration
   that merely restates a claim already made gets cut.
4. **Mechanistic depth.** A bullet states the claim *and* how it works. Not "he says to
   practise deliberately" but "ten minutes a day on the sub-skill you are worst at, scaling
   five minutes a week, with a coach naming one correction per session."
5. **Every number** the source quantifies — effect sizes, timescales, counts, prices — sits
   inside the bullet that carries it.
6. **Named studies, books, and citations keep their names**, inline, where the source gave them.
7. **Speaker attribution.** A host's contribution is captured as the host's.
8. **Report, don't advise.** Where the source contradicts itself, hedges, or a guest pushes
   back, capture that as its own bullet — because it happened in the source, not as your
   critique.
9. **Flag garbled specifics.** Auto-captions mangle names and figures. Mark uncertain ones
   unverified inline rather than guessing silently; put unrecoverable words in the caveats
   line, and say so there when you reconstruct a mangled name.
10. **Flag a title/content mismatch.** If the title misrepresents what the source covers, one
    line under the header block.

**Length** is set by how much distinct substance there is. Rough calibration: a 45-50 minute
talk lands around 60-90 bullets; a 90 minute interview around 70-100. Both directions are
errors — 20 bullets for a dense hour is too thin, one bullet per transcript sentence is too
long.

**A source carrying several separable arguments legitimately runs over.** A lecture can hold
four distinct arguments where an interview holds one, and compressing it to the interview
budget throws away whole arguments rather than repetition. Run the merge pass first — collapse
every pair where the second bullet only restates the first — and if it still sits above the
guide, ship it and say why. **Never cut a specific, a number, or a named study to hit a
bullet count.**

## After saving

Print the saved path. **Do not dump the bullets in chat** — the file is where they get read.
One line on calibration (bullet count, what was merged or cut) is enough.

## Constraints

- **No shallow bullets.** A bullet states the claim *and* its mechanism. "Aim matters" is not
  a bullet; "aim installs a perceptual filter that admits only facilitators and obstacles and
  hides everything else" is.
- **No prose blocks.** A paragraph in the body is a format error, not a style choice.
- **No numbered lists.** Numbering invites transcript-order dumping; the sections carry the
  structure instead.
- **No buried specifics.** A striking detail parked inside another bullet is a miss.
- **No recommendations.** See the rule at the top — this skill reports, it does not advise.
- **Never infer a video's content from its metadata.** No transcript means stop and ask.
