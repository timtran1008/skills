# Plan · Do · Judge

An operating system for office work, as a set of agent skills.

Most AI advice for office workers is a prompt pack. This is not that. These are **skills** —
procedures an agent runs the same way every time, so the quality of your output stops
depending on how well you happened to phrase the request that day.

They come out of years of running an L&D function and a training practice through an
agent. Every skill here was extracted from one I use on real work, then stripped
of everything specific to me.

> **Credit where it's due.** The shape of this repo — small composable skills, one `SKILL.md`
> each, user-invoked vs model-invoked — is taken from
> **[mattpocock/skills](https://github.com/mattpocock/skills)**. Matt's repo is for engineers;
> this one is for everyone else in the building. Two of the skills here (`grill-me`,
> `handoff`) started as forks of his and grew into something different. Two more that I use
> daily are still essentially his — **install `teach` and `wait-what` from
> [his repo](https://github.com/mattpocock/skills)**, not from mine.

## The spine

Every skill belongs to one of three moves:

| | | |
|---|---|---|
| **Plan** | Decide what to do, before doing it | Interrogate the request, find the unknowns, shape the argument, break the work down |
| **Do** | Produce the thing | Draft, extract, capture, hand off |
| **Judge** | Find out whether it's any good | Red-team it, check it, decide what to keep |

Plus **workspace** — the small amount of structure the loop runs on.

Most people's AI use is all *Do*. That's why the output is fast and mediocre. The leverage is
in Plan and Judge.

## What's here

### Plan
- **[tna](./skills/plan/tna/SKILL.md)** — training needs analysis with a gatekeeper on the
  front. Diagnoses whether the request is actually a skill gap before any design starts,
  because most training requests are not.

### Do
- **[source-notes](./skills/do/source-notes/SKILL.md)** — three-layer notes on any source:
  what you can use from it, a full extraction, and a recall sheet. For sources you intend to
  act on.
- **[tldr](./skills/do/tldr/SKILL.md)** — the same extraction with the advice removed. Notes
  only, grouped by the argument the source is making, never by transcript order.
- **[ai-lib](./skills/do/ai-lib/SKILL.md)** — save a reference to your library in one command:
  a distilled card, an index row, and whatever came out of it worth acting on.
- **[handoff](./skills/do/handoff/SKILL.md)** — compact a dying session into one briefing a
  fresh agent can start from, in any tool.
- **[pmlt](./skills/do/pmlt/SKILL.md)** — design a training session on the Convince ·
  Introduce · Practise · Commit arc, calibrated to the room and red-teamed as a participant.
- **[traps](./skills/do/traps/SKILL.md)** — a five-beat micro-loop for teaching one technique
  as a story: the trap, why it felt right, what it cost, the fix, the fix applied.

### Judge
- **[for-review](./skills/judge/for-review/SKILL.md)** — package a finished deliverable so a
  *different* AI can red-team it cold, with a reviewer contract that stops it folding the
  moment you push back.
- **[fact-check](./skills/judge/fact-check/SKILL.md)** — post-generation QA in three layers:
  countable, binary, logical. Identifies where human judgment is needed and stops there.
- **[honest-extraction](./skills/judge/honest-extraction/SKILL.md)** — extraction where
  guessing is expensive. Every claim marked `explicit` / `inferred` / `missing` / `conflicted`.
- **[adopt-or-drop](./skills/judge/adopt-or-drop/SKILL.md)** — weekly review of the ideas
  you've been saving. One verdict each, a reason required, stamped so it never resurfaces.

### Workspace

The daily loop. `checkin` opens the day, `checkout` closes it, and `done` handles everything
you finish in between.

- **[setup](./skills/workspace/setup-timtran-skills/SKILL.md)** — run once. Creates the
  substrate the other skills read from.
- **[checkin](./skills/workspace/checkin/SKILL.md)** — scans every project, recovers what
  yesterday left unfinished, and proposes a time-blocked day. Writes nothing unapproved.
- **[checkout](./skills/workspace/checkout/SKILL.md)** — resolves every unfinished item into
  done, superseded, dropped, or carried, and *persists the carries* so tomorrow still has them.
- **[done](./skills/workspace/done/SKILL.md)** — the only completion command. Writes all three
  trackers plus the history entry, captures the session's learnings, and sweeps for what the
  completion just made untrue.

This used to be three skills — a light `done`, a `log-it` that also wrote history, and a `sync`
that captured learnings. Picking a tier meant deciding, before you knew whether the session had
produced anything worth keeping, how much of it to keep. The cheap option always won and the
learnings went unrecorded. One command, no choice.

The piece worth stealing even if you use none of the rest is the
**[supersession sweep](./skills/workspace/done/supersession-sweep.md)**: adding new information
is only half the write, and the other half — closing what that information just killed — is the
half every tracking system skips.

### Coming
`plan/` fills out next: `grill-me`, `reverse-plan`, `structure-first`, `scaffold`. Work in
progress lives in [`skills/in-progress/`](./skills/in-progress/).

## Install

**Claude.ai** — Settings → Capabilities → Skills → upload the folder for the skill you want.
Each skill directory is self-contained.

**Claude Code** — clone this repo and point a plugin marketplace at it, or copy individual
skill folders into `.claude/skills/`.

Then run `/setup-timtran-skills` once, in whatever folder you keep your work in.

## The two files that matter most

Read these before any individual skill:

- **[PRINCIPLES.md](./PRINCIPLES.md)** — the operating rules underneath everything: decision
  tiers, why preparation is never completion, the no-fabrication rule, verify-don't-guess.
  These are role-independent. They're also the part that took longest to learn.
- **[PROFILE.template.md](./PROFILE.template.md)** — you fill this in. Your role, your taste,
  your good-enough bar per task type. Skills read it. Without it they're generic; with it
  they're yours.

## Adapt these

Fork them. Rewrite them. A skill that doesn't match how you actually work is worse than no
skill, because you'll follow it anyway. Everything here is MIT — see [LICENSE](./LICENSE).

---

Built by [Tim Tran](https://www.linkedin.com/in/timqtran) — L&D manager and corporate
trainer. I write about this at *Tim on A.I.*
