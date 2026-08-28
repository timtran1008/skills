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
- **[setup](./skills/workspace/setup-timtran-skills/SKILL.md)** — run once. Creates the
  substrate the other skills read from.

### Coming
`plan/` and `do/` are next: `grill-me`, `reverse-plan`, `structure-first`, `scaffold`,
`source-notes`, `handoff`. Work in progress lives in [`skills/in-progress/`](./skills/in-progress/).

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
