# P1 — Framing the Intent & Inception Inputs

> **Module:** P1 · **Track:** Product Manager add-on · **Time:** ~75 min · **Format:** 📖 Read + 🧪 Hands-on
> **Prerequisites:** Shared Core [C1–C6](../shared-core/C1-why-aidlc.md)

## Learning objectives

By the end of this lesson you can:

- Frame an **Intent** that gives the AI enough to route and plan without over-specifying.
- Supply the inputs Inception needs: problem, users, success metrics, MVP IN/OUT, risks/open questions.
- Work with the **`aidlc-product-agent`** through Requirements Analysis (stage 2.3) to a solid `requirements.md`.
- Recognize the product-lead reviewer's bar: completeness, business alignment, testability.

## Why this matters

As a PM, you are the human counterpart to the agent that's most active in early AI-DLC — the product agent. Everything downstream (units, bolts, code, tests) inherits the clarity or the ambiguity of what you put in at Inception. A tight intent and crisp requirements are the highest-leverage contribution any single person makes to a run.

## Read

### Meet your counterpart: the product agent

AI-DLC ships an **`aidlc-product-agent`** that plays *product manager / business analyst*. It leads intent capture, scope definition, **Requirements Analysis (2.3)**, and **User Stories (2.4)** — the most active agent across Ideation and Inception. Your job isn't to do its work; it's to **steer and validate** it. Think of P1–P3 as learning to be the sharpest possible human in the room while that agent drafts.

### A good Intent: destination, not directions

Recall the Google Maps framing from C1 — you set the destination, the AI proposes the route. A strong intent names the **outcome** and the **boundaries**, and leaves the "how" to the workflow.

- 🚫 *"Build a rewards system."* — no user, no outcome, no boundary.
- ✅ *"Let signed-in customers earn and redeem points at checkout, starting with earn-only; redemption is a later phase."* — clear user, outcome, and an explicit scope line.

The single most valuable thing you can add is **what's out of scope** and **what must not change** — these prevent the AI from quietly expanding the work.

### The inputs Inception wants

Whether you provide these up front or answer them at gates, Inception is built to elicit the following. Bring them and you cut the back-and-forth dramatically:

| Input | What to say | Why the AI needs it |
| --- | --- | --- |
| **Problem** | The specific business problem, in 1–2 lines | Anchors every requirement to a reason |
| **Target users** | Who uses it, what each type needs | Drives personas and user stories (2.4) |
| **Success metrics** | Measurable targets | Lets requirements trace to business intent |
| **MVP — IN** | Features included now | Defines the Units to build |
| **MVP — OUT** | Deliberately excluded (and why) | Prevents scope creep; the AI honors it |
| **Risks & open questions** | Known unknowns | Pre-declared ambiguities the AI resolves early, not mid-build |

> **Tip:** pre-declaring open questions is a gift to yourself. They feed straight into Requirements Analysis as things to resolve *early*, instead of surfacing as surprises three stages later.

### Requirements Analysis (stage 2.3)

This stage **always runs**. The product agent produces `requirements.md` from your intent plus its clarifying questions (asked through the interaction modes you learned in C5 — Guide Me / Edit File / Chat). Your work here:

- **Answer with intent, not just letters.** "B — earn points on paid orders only, not refunds" beats "B." The rationale carries forward.
- **Resolve, don't defer.** If you have a doc that answers a question, tell the agent to read it and answer itself; only escalate what's genuinely unclear.
- **Read `requirements.md` before approving.** This is the contract everything downstream builds on — the C5 rule (never vibe code) matters most right here.

### The reviewer's bar

A quality-gate reviewer (**`aidlc-product-lead-agent`**) checks requirements/stories/mockups for **completeness, business alignment, and testability**, appending a READY / NOT-READY verdict before your human gate. It never blocks — *you* decide — but treat its findings as a free senior-PM review. If it flags a requirement as untestable, that's usually a real gap.

## 🎧 See it (6 min)

*Screencast placeholder — [P1: From one-line intent to requirements.md, 6 min].* A PM frames an intent with an explicit OUT list, runs Requirements Analysis in Guide Me mode, answers with rationale, reads the draft, requests one change for testability, then approves.

## 🧪 Try it (25 min)

On the workshop repo, using a product idea you know well:

1. **Write the intent** in two sentences — outcome + one explicit "out of scope" line.
2. **Fill the six inputs** from the table above in a scratch doc (problem, users, metrics, IN, OUT, risks).
3. **Run Requirements Analysis** (`/aidlc --scope mvp <your intent>`, advance to stage 2.3). Choose an interaction mode and answer with rationale.
4. **Read `requirements.md`** in the intent's record dir. Find one requirement that isn't clearly **testable** and request a change to fix it.
5. **Check the reviewer verdict** (READY/NOT-READY) and note whether it caught the same gap you did.

✅ **Done when:** you have a `requirements.md` you'd stake the build on, and you fixed at least one testability gap before approving.

## Terminology

<details>
<summary><b>Show traditional-term mapping</b></summary>

| AI-DLC term | ≈ Traditional analogue |
| --- | --- |
| Intent | Epic / product brief / initiative |
| `aidlc-product-agent` | Your AI product analyst |
| Requirements Analysis (2.3) | Requirements gathering / elaboration |
| `requirements.md` | The requirements doc / PRD-lite |
| Product-lead reviewer | Senior PM peer review / sign-off |
| MVP IN / OUT | Scope in / scope out |

</details>

## ✅ Checkpoint

<details>
<summary>1. What are the two most valuable things to add to an intent, and why?</summary>

What's out of scope and what must not change — they stop the AI from silently expanding the work and give the gates something concrete to check.
</details>

<details>
<summary>2. Why pre-declare open questions?</summary>

They feed Requirements Analysis as pre-declared ambiguities the AI resolves early, rather than surfacing them as surprises mid-design.
</details>

<details>
<summary>3. Which stage produces requirements.md, and who leads it?</summary>

Requirements Analysis (2.3), led by the aidlc-product-agent. It always runs.
</details>

<details>
<summary>4. What does the aidlc-product-lead reviewer check, and can it block you?</summary>

Completeness, business alignment, and testability, with a READY/NOT-READY verdict. It never blocks — the human always decides — but its findings are a free senior review.
</details>

## Key takeaways

- You're the human counterpart to the **product agent** — steer and validate, don't do its typing.
- A strong **intent** = outcome + boundaries; the highest-value additions are **OUT** and **must-not-change**.
- Bring the **six Inception inputs**; **pre-declare open questions**.
- **Read `requirements.md` before approving** — it's the contract; use the reviewer verdict as a free check.

**Next:** [P2 — Facilitating workshop-mode Inception](P2-facilitating-inception.md) — running Inception for a group, the practices affirmation, and driving Intent → Units.
