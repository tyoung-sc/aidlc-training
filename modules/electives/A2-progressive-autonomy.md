---
title: "A2 — Progressive Autonomy"
parent: Electives
nav_order: 2
---

# A2 — Rules, Sensors & Progressive Autonomy

> **Module:** A2 · **Track:** Elective (self-paced) · **Time:** ~45 min · **Format:** 📖 Read
> **Prerequisites:** [A1 — Inside v2](A1-inside-v2.md) (and, for developers, [D4](../developer/D4-build-test-control-loop.md))

## Learning objectives

By the end of this lesson you can:

- Explain **progressive autonomy** — hydrating verification in *safe increments*.
- Describe the **control loop** (Rules + Sensors) and the **Learning Loop** as its growth engine.
- Name the three **extensibility** modes (additive, replacement, composability).
- Decide what to encode next to reduce your team's manual gate load.

## Why this matters

Teams don't get to autonomous delivery in one leap — and shouldn't try. The interesting question isn't "can the AI run unattended?" but "how do we *safely widen* what it can run unattended, one verified check at a time?" This lesson is the strategy behind the mechanics you've been using.

## Read

### The core idea: distill judgment into checks

AI-DLC's founding bet is that much of the human effort spent validating AI can be **distilled into machine-executable constructs**. Every stage is framed in three compartments: **what** it produces (inputs/outputs), **how we know it's right** (post-conditions), and **what it learned** (runtime observations). A stage can self-correct only when its post-conditions are checkable by a program it can't edit. Where they are, it converges autonomously; where verification is a judgment call, a human stays in the loop — for now.

### Two kinds of verification (recap, then the strategy)

From D4: **inferential** checks are LLM-judged quality heuristics (can't self-halt alone — a human validates); **computational** checks are deterministic executables (linters, type-checks, "no unauth endpoint"). The strategy follows directly:

> **The proportion of stages that can run without human gating grows exactly as fast as you convert judgment into deterministic checks.**

You don't flip a switch to "autonomous." You *earn* it, one Sensor at a time.

### Safe increments, not big-bang

Real organizations carry guardrails, compliance rules, and no-go-zones encoded in documents, checklists, and tribal knowledge. Translating all of that into enforceable post-conditions is a large undertaking no one finishes at once. AI-DLC treats that as the *expected adoption path*:

1. **Start with what you have** — encode the checks you already know (coding standards, naming, basic security). The AI runs autonomously within those and escalates for everything else.
2. **Hydrate incrementally** — each guardrail you distill into a Sensor widens what the AI can self-verify, shrinking human intervention there.
3. **Expand the increment** — as the check library matures, larger spans of work run autonomously.

The ladder prompt (D3) is the day-to-day face of this: your walking skeleton + current checks decide how much you trust the rest.

### The Learning Loop is the growth engine

Manually authoring every check would be slow. The **Learning Loop** hydrates from *practice*: the agent keeps a `memory.md` diary during a stage; at the gate you confirm which observations to keep; each becomes a **Rule** (promotable org→team→project) or scaffolds a **Sensor**. So the corrections you make during real work *are* the roadmap for automation — a repeated correction is a signal to encode a check. Practice becomes policy.

### Extensibility: three ways to make it yours

Because no vendor can anticipate your org, AI-DLC is extensible with the same constructs it ships:

- **Additive** — layer your own Rules/post-conditions on top of the baseline.
- **Replacement** — override a specific baseline rule where your requirements diverge, taking ownership of that piece.
- **Composability** — author entirely new stages (same three-compartment shape) that the orchestrator stitches into the workflow.

In practice that means: add team Knowledge and Rules (D2/U2), scaffold Sensors from the Learning Loop, define a custom **scope** via `compose` (C4), or — advanced — add an agent or stage. All of it is configuration, not forking the engine.

### What to encode next (a heuristic)

Pick your next check by leverage: *frequency × determinism × risk.* A correction you make **often**, that is **deterministically checkable**, on something **risky**, is the best Sensor to write next. Rare, subjective, low-risk things stay human. Over a few projects, this quietly moves your team up the autonomy ladder without ever gambling on an unverified leap.

## Terminology

<details>
<summary><b>Show traditional-term mapping</b></summary>

| AI-DLC term | ≈ Traditional analogue |
| --- | --- |
| Progressive autonomy | Incrementally trusting automation |
| Post-condition | Definition-of-done check |
| Hydration | Building up your rule/check library |
| Additive / replacement / composability | Extend / override / add-new |
| Learning Loop | Retro that writes standards automatically |

</details>

## ✅ Checkpoint

<details>
<summary>1. What determines how much of the workflow can run without human gates?</summary>

How much of your verification is computational (deterministic) rather than inferential (judgment). Converting judgment into deterministic checks widens safe autonomy.
</details>

<details>
<summary>2. Why is autonomy adopted in safe increments rather than big-bang?</summary>

Org guardrails/compliance/tribal knowledge can't all be distilled into enforceable post-conditions at once. You start with what you can encode, hydrate incrementally, and expand the increment as the check library matures.
</details>

<details>
<summary>3. How does the Learning Loop accelerate this?</summary>

It turns real corrections into Rules/Sensors at the gate, so practice hydrates your verification library instead of relying only on manual authoring.
</details>

<details>
<summary>4. Name the three extensibility modes.</summary>

Additive (layer on), replacement (override a baseline rule), composability (author new stages the orchestrator stitches in).
</details>

<details>
<summary>5. What's a good heuristic for the next check to encode?</summary>

Frequency × determinism × risk — encode the correction you make often, that's deterministically checkable, on something risky.
</details>

## Key takeaways

- **Progressive autonomy** = converting judgment into deterministic checks, one at a time.
- The **control loop** (Rules + Sensors) plus the **Learning Loop** grow that check library from real practice.
- Extend via **additive / replacement / composability** — all configuration, no engine fork.
- Encode next by **frequency × determinism × risk**; leave rare/subjective/low-risk to humans.

**You've completed the electives — and the full bootcamp.** Back to the [program plan](../../aidlc-bootcamp-plan.md) or the [module index](../README.md).
