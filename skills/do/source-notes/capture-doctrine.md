# Capture doctrine

Binding on `/source-notes` and `/ai-lib`. `/adopt-or-drop` consumes what it produces.

Read this before writing any `Learn / Adapt` block. It defines the three buckets, the gate
each must clear, where the failures go, and what reaches `today-tasks.md`.

---

## 0 — Why it works this way

The obvious rule — *every idea you keep must name a use for it* — fixes legibility and
nothing else. It gives weak ideas a survival route: manufacture a plausible use case and the
item ships. Combined with "never narrow a roundup", it produces 15-item blocks that get
rejected wholesale, usually with no reason recorded, which teaches you nothing.

So the use-case rule is demoted. It is a **writing standard** applied to items that have
already passed a gate — not the admission test. The gate is the admission test.

## 1 — Bind to live state first, every run

An idea that cannot point at something live in your actual work is not relevant to it, and
by your own definition is not worth keeping.

Read these two before writing anything:

| File | What it answers |
|---|---|
| `projects/` — each `context.md` status line | What exists, its real name, and whether it is active, blocked, or dormant |
| `today-tasks.md` | What is live this week |

Then, only for the one project a given idea claims, that project's Next actions.

**Never hardcode project names into a skill.** Any fixed list rots — a skill can end up
naming a project that was killed months earlier, which is the skill actively teaching
irrelevance. The folder is the only list that stays true. An idea naming a **dormant or
archived** project fails automatically to Inventory.

## 1b — Strip to the core workflow, then gate

**Gate the idea, not the vendor.** Before routing a candidate that arrives packaged in the
source's own tool, product, repo, or paid tier, strip it to its core workflow:

> **trigger → input → transform → output → where it lands**

Then ask whether that workflow can be rebuilt with general-purpose assistants — **Claude,
ChatGPT, or Gemini** — instead of the vendor's tool:

| Bucket | Rebuild on |
|---|---|
| **Adapt** (you are the user) | Whatever you already pay for among those three, including any agent or file setup you run them in. |
| **Teach / Share** (the audience is the user) | **Free or ~$20/month tiers** of the same three, tagged `[Free]` / `[Paid $20]` (Teach gate 3). Anything that only works through your own agent setup does not count for them. |

- **The bar is a two-hour build, not "replicable."** With enough AI help nearly anything can
  be rebuilt, so replicability alone admits everything. The test: *can you get the rebuilt
  workflow working on your tools in about two hours of your own time* — one sitting, no new
  subscription, no waiting on anyone else.
- **Passes** → route the *rebuilt* version through the bucket gate. Name the tool, the steps,
  and the estimate ("~1.5h: one Claude project, three reference files, one saved prompt"). The
  estimate doubles as Adapt gate 3's switch cost.
- **Fails** (over two hours, or needs the vendor's proprietary data, integration, or model) →
  Inventory, with the blocker named in one line ("~1 day: needs a mail-to-spreadsheet
  pipeline"; "needs the vendor's CRM connector").
- **For Teach,** the two hours is your prep time. The audience's side still has to clear gate
  3: free or $20 tier (tagged), no command line, doable in the room.
- **Do not test the rebuild live.** Judge from the shape of the workflow; mark the idea
  `[untested]` when the rebuild is plausible but unproven.

Why: without this step, a good idea shown inside a CLI tool or a paid demo dies at the Teach
gate or at the no-fabrication rule — even when the same result is one prompt away in a tool
you already have.

## 2 — The three buckets

Every candidate lands in **exactly one**. Dual-listing is how padding sneaks back in. An
item that fits none is **cut to Inventory** — that is the kill test.

### Steal to Teach / Share
> Something people can now do that they could not one or two months ago.

You are the deliverer; the audience is a room or a feed.

**Gate — all four:**
1. **Recency.** Source published within ~60 days, and the capability is what the source is
   *about*. `Published: unknown` is allowed — run the other three.
2. **Novel to your audience** — not already in `library/INDEX.md`. Not "new to the world",
   which is unverifiable and not the question. The question is *not yet taught by you*.
3. **A non-technical person can do it with tools they already have** — no command line, no
   API key, no repo, no self-hosting — **and can reach it on a free or ~$20/month tier.**
   **This gate does the heaviest lifting.** It is the one that kills the
   interesting-to-you-only material.

   Ask the price half concretely: *can someone do this today on a free account, or on a
   ~$20/month plan* (ChatGPT Plus, Claude Pro, Google AI Pro)? Many people now pay for one
   subscription at that price, so the gate says which is needed rather than excluding it:
   - **Free** → passes, tagged `[Free]`.
   - **~$20/month only** → passes, tagged `[Paid $20]`. Name the plan.
   - **Above $20** (ChatGPT Pro, Claude Max, Gemini Ultra, any $100+ tier) → fails. Record it
     in Inventory with the tier named. Do not bend it into a "preview" of what they might buy.

   Every Teach idea carries exactly one tag, in the note and in the today-tasks push. When
   both work, tag `[Free]` and say in one clause what the $20 plan adds.

   This half exists because a whole source died on it: a ten-use-case head-to-head comparison
   cleared recency, novelty and landing, and was tossed outright because it compared *paid*
   versions to an audience that is overwhelmingly on free accounts. Browser use and voice-thread
   orchestration are both real capabilities and both sit behind a subscription. **The strongest
   item in a source can be the reason the whole source fails this gate.**

   **But run §1b first.** If the *core workflow* behind a pricier demo runs on a free or $20
   tier of Claude, ChatGPT, or Gemini, the cheapest rebuild is what gets gated, tagged, and
   taught. Only the demo as shown fails.
4. **It lands somewhere real** — a session actually in the calendar, or a channel you
   actually publish to.

Audience is the generic person in that room, sanity-checked against one real session. Do
**not** pin an idea to a specific audience too early — that is what produces the forced
angle, where a philosophy talk gets bent into a productivity pitch.

**A known gap, stated rather than papered over:** no file records what you actually said in a
room. "Already covered in that workshop" cannot be checked automatically. Say so when it matters.

### Steal to Adapt
> You already do X a particular way; here is a better way. Want to try it?

You are the user; nobody else sees it.

**Gate — all three:**
1. **Names the specific documented current way** — a step in a written SOP, or a named
   `SKILL.md`. **No named current way means it is not an Adapt idea.** "More efficient"
   without a written comparison is an assertion, not a comparison.
   **Widened by §1b:** a capability you do not have yet also qualifies if the rebuilt
   workflow runs on your tools **and** binds to a named recurring task or live project where
   it would land. Gate 2 then reads "what that task costs today without it." No named landing
   spot means Inventory, same as before.
2. **Says what is actually worse about the current way** — the step that costs time, breaks,
   or gets redone.
3. **States the switch cost** — what you have to change, build, or learn.

### Steal to Write
> Human material: an argument, a story, a line.

This bucket exists because the highest-keep-rate sources are usually not about your subject
at all, and yield nothing under buckets shaped around it.

**Gate — both:**
1. Binds to a live section of something you are actually writing, or an existing idea slot in it.
2. It is an argument, story, or line — **not a concept**.

## 3 — Every surviving idea still needs a concrete use

Applied *after* the gate. An abstract idea reads as homework; one you can picture reads as
an opportunity. Do the imagining now, while the source is in front of you.

- **Weak:** "Steal the constitution pattern for the writing skill."
- **Strong:** "Steal the constitution pattern: write the twelve style rules down once as
  things a script can check, then `/fact-check` runs them on every draft — so you stop
  re-reading each post hunting for the same five violations."

Name the real project or artifact, not a vague area of life. Show what changes on a Tuesday.
Never invent a project or a workflow to make an idea land. If you cannot construct a real
use, it failed the gate — back to Inventory.

## 4 — Inventory: where the non-survivors go

**Every candidate that fails its gate goes to Inventory. Nothing is lost, and nothing is
pitched as a recommendation.**

Inventory also absorbs the **full roundup enumeration**. Preserving the whole list of a
13-tool roundup is right; pitching all thirteen as things to adopt is not. The source
already did the reviewing. The list ships — in Inventory, numbered, one tight line per item:
what it is, and the catch.

| Skill | Where Inventory lives |
|---|---|
| `/ai-lib` | Its own `## Inventory` section, between the body and `## Learn / Adapt` |
| `/source-notes` | A subsection inside `## Structured Notes` |

## 5 — Zero is a legitimate outcome

Under this gate a 15-tool roundup can yield **nothing**. That is the gate working.

Write the note with a full Inventory, push nothing, and report *"0 steals, N inventoried."*
**If three sources in a row yield zero, say so explicitly.** That is a signal about the
source diet, not about the notes — and it is the kind of drift that otherwise takes a
deliberate audit to notice.

## 6 — The push to today-tasks.md

Only gate-survivors push. **Cap three per bucket** — the remainder stays in the note, and
Inventory means nothing is lost by the cap. Append at the end of the file; never merge into
an existing block, so each source stays attributable.

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

Omit an empty sub-block rather than writing "none". Never push Inventory.

## 7 — Standing quality rules

- **No fabrication.** Every idea traces to specific lines in the source. Your extrapolation
  is not the source's idea — cut it. **The idea must trace; the rebuild need not:** a §1b
  rebuild onto your own tools is allowed when the core workflow is cited from the source and
  the idea names the exact tool and steps. Inventing a workflow the source never showed is
  still fabrication.
- **Blank beats wrong.** One strong idea beats one strong plus three filler.
- **Highest-leverage first** within each bucket — what could ship this week, not what is
  most abstract.
- **Strip the flattery.** No "interesting", no "thought-provoking", no "may be worth
  considering", no generic "of course it is not a silver bullet".
