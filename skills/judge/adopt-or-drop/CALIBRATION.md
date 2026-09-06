# adopt-or-drop — calibration record

Provenance for the rules in `SKILL.md`. The rules themselves live there and bind every run;
this file holds the cases that produced them, so `SKILL.md` stays legible.

Read this only when a rule's *intent* is unclear, or before changing one — the case usually
explains why the obvious-looking edit is wrong.

---

## Role-anchoring, and why the default is wrong

Most people wear several hats: a job, a side practice, a subject they teach, something they
write, a family. The failure mode this rule exists to kill is forcing every idea into whichever
lens is currently loudest — usually the one with the most active project behind it.

A parenting idea serves the parent. A meeting-habit idea serves the office worker. A
training-design idea serves the teacher. One idea may legitimately serve exactly one role. Do
not manufacture a second angle to make it look more valuable.

---

## No manufactured AI angle on non-AI sources

**Case:** a philosophy talk — not an AI source — came back with two of its five ideas bent into
an AI-hallucination and AI-delegation lens. Both were rejected outright.

**Rule derived:** if a source's core subject is not AI, frame each idea in the role it genuinely
serves, however tempting the analogy. A passing mention of AI inside a philosophy or business
talk does not make it an AI source.

---

## Plain-English use cases

Two changes landed together.

**The formula was retired.** *"As a [role], with this idea, X → Y"* turned out to be unhelpful
scaffolding. Name the role inside a normal sentence instead.

**The bar is comprehension speed.** If the line has to be re-read to be understood, it is too
abstract — rewrite it plainer. Write like a person talking, not like a framework.

- Bad (abstract): "A capability/job/catch card inventory before recommending any tool."
- Good (plain): "When you show managers a bunch of AI tools, don't just hand them a list. For
  each one write a line — what it does, when to use it, what can go wrong — so they learn to
  pick the right one themselves."

Concrete beats clever.

---

## The three-bucket rebuild — the case behind the whole gate

**The complaint:** "I reject almost every recommendation — none of it has any relevance to my
current work and life."

**The evidence sweep (~50 files):** 64% of reviewed files tossed overall, 80% in the
tools-and-articles pool. Four batches were rejected **wholesale** — 18, 15, 14 and 10 items,
every one a tool roundup in full-enumeration mode. Six verdicts recorded **no reason at all**.
Where reasons existed they clustered on two words: *too technical* and *boring*. Across the
~20 files that were kept, the conversion was one tool built, three published pieces (all from a
single run), and nothing else. What survived was human material. What died was infrastructure.

**Diagnosis — the earlier fix overcorrected, twice.**

1. *"Every idea needs a use case"* fixed legibility and did nothing for substance. A weak idea
   could survive by having a plausible use case **manufactured** for it. The rule became a
   formatting hoop that laundered filler.
2. *"Never narrow a roundup"* was right about preservation and wrong about presentation. The
   ask was that the full list be **preserved**; the rule pitched the full list back **as
   candidates**.

Neither was a template problem, so no template edit could have fixed either. What was missing
was a kill test, and a definition of relevance the agent could actually check.

**What replaced them:**

- **Three buckets, and exactly one per item.** Fits none = cut to Inventory. That is the kill
  test. The Write bucket exists because the two AI-shaped definitions yield nothing from the
  human sources that have the highest keep rate.
- **Hard live-state binding.** Read the project list and the current task file before writing
  any recommendation. A dormant or archived project fails automatically. This is the change
  that attacks the miss rate directly.
- **No hardcoded project names in skill text.** One skill was still naming a project six weeks
  after it had been killed — doctrine teaching irrelevance by example.
- **Inventory absorbs everything else** — the full roundup enumeration and every gate failure.
  Nothing is lost; nothing is pitched.
- **Confidence flags retired as a category.** "Deploy as-is vs needs experimentation" is a
  confidence note, not a bucket, and it was where weak items went to survive instead of being
  cut.
- **Caps at three per bucket.** The 18-item push is precisely the batch that got rejected
  without a reason.

**Open tension, flagged rather than resolved.** A strategy or positioning document is *not* the
relevance test. In the case above, the kept ideas skewed heavily toward a book the strategy
document explicitly excluded — so a gate reading that document would have cut the exact items
its owner kept. **The gate reads the live project list and the current tasks, never the profile.**

---

## Under-extraction, re-pointed at Inventory

The original rule said a four-hour source yielding five ideas is an extraction failure, not a
thin source. Under a three-bucket gate that flag would fire on every well-run source, because a
strict gate routinely yields two or three survivors, or zero, from a long one.

**Re-pointed, not retired.** The flag now measures **Inventory depth**, not survivor count. A
long source with a thin Inventory is genuinely under-mined. A long source with a rich Inventory
and two survivors was mined properly and the rest didn't clear the gate — that is the system
working, and flagging it would punish the fix.

The original complaint — *"almost four hours and that's all?"* — is preserved exactly. It was
about extraction volume, and extraction volume now lives in Inventory.

---

## A reason is required on every verdict

Six verdicts in the pool read "no reason given." Diagnosing why the pipeline was failing
therefore cost a full evidence sweep across fifty files, reconstructing intent from the two
reasons that happened to be recorded.

One phrase per verdict is the price of never doing that again. Ask once if none is volunteered.
**Never invent one** — an agent-supplied reason poisons the next calibration worse than a blank
does, because a blank is at least visibly missing.

---

## Backlog reachability

Review-status banners start on the day you adopt them. Everything written before that is
unstamped, so a default recent-window scan cannot see it — those files are structurally
invisible, not reviewed.

They stay reachable only through an explicit wider window. Do not quietly pretend the backlog
does not exist; if a wider window is asked for, honour it.
