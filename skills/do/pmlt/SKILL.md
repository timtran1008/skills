---
name: pmlt
disable-model-invocation: true
description: >
  Design a training session on the PMLT arc — Convince, Introduce, Practise, Commit — with an
  audience-calibration step in front of it and a participant red-team behind it. For corporate
  sessions where people arrive with a working method they are not looking to replace.
---

# PMLT — session design

Four steps, in this order, every time:

| | Vietnamese | English | Does |
|---|---|---|---|
| **P** | Phục | Convince | Surface dissatisfaction with the current way |
| **M** | Mới | Introduce | Present the new method, and the resistance to it |
| **L** | Làm | Practise | Apply it in something close to their real work |
| **T** | Theo | Commit | Bridge to a behaviour that survives Monday |

Most corporate training runs M and L only. That is why it feels like being handed a solution to
a problem you did not have, and why nothing changes the following week.

**Invoke:** `/pmlt <topic>`

---

## Step 0 — Đọc: read the room

**Before designing anything.** Two dimensions decide how the whole session is calibrated:

**Awareness of the problem.** High → Phục can be light; they already feel it. Low → Phục has to
work, and it has to find a gap they have not noticed themselves.

**Identity investment.** Low → challenge the current approach directly. High → frame the gap as
**incomplete, not wrong**. Honour what works before showing what is missing. Skip this and you
lose the room in the first ten minutes and never get it back.

Ask, and confirm the assessment before proceeding:

- Who is the audience — role, level, industry?
- Do they already feel a problem?
- Is their current approach tied to their identity or their success?
- What kind of gap will land — failure, missed opportunity, wasted effort, relationship cost?
- How much time is there?
- What technique is being taught, **and how many?** (One → PMLT alone. Two or more → nest
  `/traps`, see below.)
- What language is it delivered in?

## Step 1 — Phục: convince

**Goal:** dissatisfaction with the status quo, and openness to something else.

- Open on a problem they commonly experience with the topic.
- *"What's the usual way people handle this?"* → *"And what does that usually produce?"*
- *"Why did that approach become so common?"* — **validate the logic before questioning it.**
- Show how the current thinking produces the current result.

**Delivery:** curiosity, not judgment. The old way made sense in its context; say so and mean
it. If they do not feel the gap, do not force it. For a low-awareness, high-investment room,
reach for data, industry examples, or hidden-cost framing — never anything that implies they
have been failing.

## Step 2 — Mới: introduce

**Goal:** the new method, clearly, alongside the resistance it will meet.

- Start with the new *thought*, not the new *technique*. Invite a different way of seeing it.
- Then the technique, action, or framework.
- Then the result it can produce.
- **Anticipate resistance out loud**, address the common objections, and ask *"what else comes
  to mind?"*

**Delivery:** present it as an option, not a correction. Acknowledge the real constraints — no
time, no authority, an unsupportive manager — honestly rather than wishing them away. Name the
practical details: when, where, how long it takes. **If they have little authority, give them
options that need none.**

## Step 3 — Làm: practise

**Goal:** try it somewhere safe, with feedback.

- A realistic scenario, close to their actual work.
- Individual preparation time **before** group practice.
- Observe, then analyse together.
- Handle the messy reality: what if the other person doesn't respond the way the script assumes?
- One **pro tip** — the nuance that lifts a competent attempt into a good one.
- Summarise.

**Delivery:** frame practice as experimentation, not assessment. Written prep before spoken
practice lowers the cost of participating. Deliver the pro tip as an enhancement, never as a
reveal that their answer was wrong.

## Step 4 — Theo: commit

**Goal:** cross the gap between the room and the job.

- One small, specific challenge for the coming week.
- **Low risk** — something they can do without asking permission.
- An artifact in a format that fits their actual life. Something on their phone, not a card
  they will lose by Thursday.
- Tie it to a trigger: *"next time X happens, do Y."*
- Optional peer accountability — message a partner once it is done.

**Delivery:** be honest that not everyone will follow through, and that this is partly outside
your control. The job is to make following through as easy as it can be.

---

## Pairing with TRAPS

PMLT is the **macro arc** for the session. When a session teaches **two or more techniques**
under Mới and Làm, wrap each one in a [TRAPS](../traps/SKILL.md) micro-loop so each gets its
own story shape.

- **Session-level Phục** opens with the umbrella problem. **Technique-level Trap + Rationale +
  Aftermath** surfaces the local gap for each one. Do not run a full Phục per technique.
- Patch is Mới at technique level; Solution is Làm at technique level.
- **One persona across every loop** — same name, same role, same situation, different traps.
- **Session-level Theo comes after the final Solution**, never once per technique.
- **Single-technique session → PMLT alone.** TRAPS adds overhead and no new shape.

## Workflow

1. Ask the Step 0 questions. All of them.
2. Confirm the Đọc assessment before designing.
3. Build the session. Learner-facing material — artifacts, spoken lines, example phrases — in
   the delivery language; facilitator guidance and design rationale in your working language.
4. **Offer the red team:** *"Want me to red-team this as a participant before we build slides?"*
5. If yes, run it (below).
6. Offer the revision.
7. Only then move to slides — see [deck-design.md](./deck-design.md).

## The red team

Adopt the mindset of the actual audience, not a generic sceptic:

- What would make them resist this session?
- What feels unrealistic about the scenarios or the advice?
- What constraint makes follow-through unlikely?
- **What are they thinking and not saying?**

Then summarise: the core vulnerability at each of the four steps, whether Đọc calibrated Phục
correctly, and the adjustments you would make.

## Boundaries

- One Phục does not fit all audiences. **Never skip Step 0.**
- Design for real constraints, not ideal conditions.
- Do not claim the framework solves everything — some learners will not engage and some managers
  will not reinforce.
- **Always offer the red team** before slides.
