---
title: "U1 — Stories as Contracts"
parent: UX Designer
nav_order: 1
---

# U1 — Stories, Personas & Acceptance Criteria as Contracts

> **Module:** U1 · **Track:** UX Designer add-on · **Time:** ~60 min · **Format:** 📖 Read + 🧪 Hands-on
> **Prerequisites:** Shared Core [C1–C6](../shared-core/C1-why-aidlc.md)

## Learning objectives

By the end of this lesson you can:

- Explain how **User Stories (stage 2.4)** runs as a **mob** and where you fit in it.
- Write **user stories and acceptance criteria** the AI can build against — as contracts, not wishes.
- Shape **personas** that make downstream design and generation user-centered.
- Read `stories.md` / `personas.md` critically before the gate.

## Why this matters

In AI-DLC, a user story isn't a sticky note — it's a **contract** the AI uses to generate code and tests. Vague stories produce plausible-but-wrong software; precise acceptance criteria produce software that does what users actually need. As the UX voice, you keep the human at the center of artifacts the machine will treat literally.

## Read

### Your counterpart: the design agent

AI-DLC ships an **`aidlc-design-agent`** playing *UX/UI designer* — wireframes, interaction design, and **accessibility** are its domain. It **leads** the mockup stages and **supports** User Stories (2.4) and Application Design (2.6). So in story-writing you're partnering with both the product agent (who leads 2.4) and the design agent (who contributes the UX lens). Your role: make sure stories and personas reflect real user needs and are precise enough to build against.

### User Stories (2.4) is a mob

Stage 2.4 runs as a **mob**: the product agent leads and the design, developer, and quality agents each contribute in parallel via contribution files, which the lead integrates into `stories.md` and `personas.md`. Sometimes the mob surfaces a judgment call mid-stage — that's your cue to weigh in on the UX trade-off. The stage is **conditional** (it runs for user-facing features), and it's where your design perspective enters the record formally.

### Stories that work as contracts

A buildable story names **who**, **what**, and **why**, and pairs with **acceptance criteria** that are concrete enough to test.

- ⚠️ *"As a user, I want a nice dashboard."* — untestable; "nice" builds nothing.
- ✅ *"As a returning customer, I want to see my last five orders on the account home so I can reorder quickly."*
  - **AC:** Shows exactly the 5 most recent orders, newest first.
  - **AC:** Each row shows date, total, and a **Reorder** action.
  - **AC:** Empty state for customers with no orders.
  - **AC:** Meets WCAG AA contrast; keyboard-navigable.

Notice the acceptance criteria pin down **counts, states, and accessibility** — the details the AI would otherwise guess. Recall from C1: you set the destination precisely; you don't hand-draw the route.

### Personas that steer generation

`personas.md` isn't decoration — it gives every downstream stage a concrete user to design and build for. Strong personas capture **goals, context, constraints, and accessibility needs** (device, assistive tech, literacy, environment). A persona that says "uses a screen reader on a slow connection" changes what "done" means for a story — and the AI will honor it if you write it down.

### Read before the gate

`stories.md` and `personas.md` pass a product-lead review (completeness, business alignment, **testability**) before your human gate. Apply the C5 rule hard here: **read before approving.** For each story ask —

- Could a developer *and a test* be written from this without asking you a question?
- Do the acceptance criteria cover empty/error/edge states, not just the happy path?
- Is accessibility explicit, or silently assumed?

## 🎧 See it (5 min)

*Screencast placeholder — [U1: Turning a fuzzy request into a buildable story, 5 min].* The User Stories mob drafts a story; the UX voice adds an empty-state and an accessibility acceptance criterion, sharpens a persona, then reviews `stories.md` before approving.

## 🧪 Try it (25 min)

On the workshop repo, for a user-facing feature:

1. **Draft one story** in who/what/why form with **4+ acceptance criteria** — include at least one **state** (empty/error) and one **accessibility** criterion.
2. **Run User Stories (2.4)** and contribute your story/AC into the mob. Watch how the lead integrates it.
3. **Sharpen a persona** — add a concrete accessibility or context constraint and note how it changes a story's "done."
4. **Review `stories.md`** — find one story a test *couldn't* be written from and fix it before approving.

✅ **Done when:** every story you own could yield both code and a test with no follow-up questions.

## Terminology

<details>
<summary><b>Show traditional-term mapping</b></summary>

| AI-DLC term | ≈ Traditional analogue |
| --- | --- |
| `aidlc-design-agent` | Your AI UX/UI designer |
| User Stories (2.4) | Story-writing workshop |
| Mob (stage mode) | Collaborative session where everyone contributes |
| Acceptance criteria | Definition of done for a story |
| `personas.md` | User personas / proto-personas |
| `stories.md` | Product backlog (as contracts) |

</details>

## ✅ Checkpoint

<details>
<summary>1. Why is a user story a "contract" in AI-DLC?</summary>

The AI uses stories and acceptance criteria literally to generate code and tests, so precision determines what gets built. Vague stories produce plausible-but-wrong software.
</details>

<details>
<summary>2. How does User Stories (2.4) run, and what's your role?</summary>

As a mob — the product agent leads while design, developer, and quality contribute in parallel. As the UX voice you contribute the user lens and weigh in on judgment calls the mob surfaces.
</details>

<details>
<summary>3. What should strong acceptance criteria pin down beyond the happy path?</summary>

Counts, states (empty/error/edge), and accessibility — the specifics the AI would otherwise guess.
</details>

<details>
<summary>4. Why do personas matter to generation, not just design?</summary>

They give downstream stages a concrete user with goals/constraints/accessibility needs, which the AI honors when defining "done."
</details>

## Key takeaways

- Stories and acceptance criteria are **contracts the AI builds from** — write them testable.
- User Stories (2.4) is a **mob**; you bring the user lens and settle UX judgment calls.
- **Personas** with real constraints (esp. accessibility) steer generation.
- **Read `stories.md` before approving** — could a test be written from every story?

**Next:** [U2 — Bringing design into the workflow](U2-design-in-the-workflow.md) — mockups, and encoding your design system + accessibility standards so generated UI aligns.
