# U2 — Bringing Design into the Workflow

> **Module:** U2 · **Track:** UX Designer add-on · **Time:** ~75 min · **Format:** 🎧 Watch + 🧪 Hands-on
> **Prerequisites:** [U1 — Stories as contracts](U1-stories-as-contracts.md)

## Learning objectives

By the end of this lesson you can:

- Locate where design work happens — **Rough Mockups (1.6)** and **Refined Mockups (2.5)** — and which runs in workshop mode.
- Encode your **design system and accessibility standards** as **team Knowledge** so the AI follows them.
- Add design **Rules** that apply across stages.
- Explain why design post-conditions stay human-validated (for now).

## Why this matters

Left unguided, the AI invents its own UI conventions every run. The leverage move for a UX designer is to make your design system and accessibility standards *part of the AI's context*, so generated mockups and code start aligned instead of needing rework. This is the difference between fighting the AI on every screen and having it default to your patterns.

## Read

### Where design happens

Two stages are led by the design agent:

| Stage | Phase | Produces | Runs when |
| --- | --- | --- | --- |
| **1.6 Rough Mockups** | Ideation | Wireframes, user flows, concept deck | UI projects — **but Ideation is skipped by the `workshop` scope** |
| **2.5 Refined Mockups** | Inception | Hi-fi mockups, interaction spec | UI projects |

Two practical notes. First, in **workshop mode** (our labs and capstone) Ideation is skipped, so you'll typically engage at **Refined Mockups (2.5)** and in the User Stories mob (2.4) — plan your contribution there. Second, the design agent has **WebSearch** for design research, so it can pull in references when you ask.

### Make your standards part of the AI's brain: team Knowledge

AI-DLC loads a **two-tier knowledge** stack into each agent. Tier 1 is methodology knowledge that ships with the framework. **Tier 2 is *your team's* knowledge**, which you manage — and this is your lever:

```
aidlc/knowledge/
├── aidlc-shared/            # standards every agent should see
└── aidlc-design-agent/      # design-specific standards, loaded when the design agent runs
```

Drop your design-system tokens, component inventory, spacing/typography rules, content guidelines, and **accessibility standards** (e.g., "WCAG 2.2 AA minimum; all interactive elements keyboard-operable") into `aidlc/knowledge/aidlc-design-agent/`. From then on, the design agent loads them at stage start and designs *from* them. Team-wide constraints go in `aidlc/knowledge/aidlc-shared/` so every agent — including the developer agent generating UI code — sees them.

> This is the same "hydration" idea from the spec's Generate-Verify-Learn model: the more of your standards you encode, the less the AI guesses and the less you correct.

### Rules for design behavior

Beyond reference knowledge, you can author **Rules** — persistent behavioral constraints resolved through an org → team → project → phase → stage chain (they live in the active space's `memory/`). A design Rule might mandate "never introduce a new color outside the token palette" or "every form field has an associated label." Rules are the *feedforward* half of the control loop; a Sensor can pair with one for a deterministic check (e.g., a linter that flags non-token colors). You'll see corrections become Rules in U3 via the Learning Loop.

### Why design still needs your eyes

The spec is candid: some post-conditions are **deterministically checkable** (does every input have a label?) and some are **judgment calls** (does this flow feel trustworthy?). Design and mockups sit heavily in the judgment bucket, so those stages **retain human validation** — the AI won't self-approve them. That's not a limitation to route around; it's exactly where your expertise is the point. Over time, as you encode more standards, more of the checkable part gets automated and you focus on the genuinely human judgment.

## 🎧 See it (8 min)

*Screencast placeholder — [U2: Teaching the AI your design system, 8 min].* A designer adds design-system tokens and a WCAG AA rule to `aidlc/knowledge/aidlc-design-agent/`, re-runs Refined Mockups (2.5), and shows the generated mockups now defaulting to the team's components and contrast.

## 🧪 Try it (25 min)

On the workshop repo:

1. **Encode standards** — create `aidlc/knowledge/aidlc-design-agent/design-standards.md` with three real constraints from your design system + one accessibility bar (e.g., WCAG 2.2 AA).
2. **Author one Rule** — write a design behavioral rule (e.g., "colors must come from the token palette") into the active space's `memory/` project layer.
3. **Run Refined Mockups (2.5)** — advance a UI feature to 2.5 and see whether the output reflects your standards.
4. **Compare** — note one thing the AI got right *because* you encoded it, and one thing that still needs your human judgment.

✅ **Done when:** the design agent visibly designs from your standards, and you can name what still needs a human.

## Terminology

<details>
<summary><b>Show traditional-term mapping</b></summary>

| AI-DLC term | ≈ Traditional analogue |
| --- | --- |
| Team Knowledge (Tier 2) | Your design system / brand guidelines the AI reads |
| Rough Mockups (1.6) | Wireframes / low-fi concepts |
| Refined Mockups (2.5) | Hi-fi comps / interaction spec |
| Rule | A design guardrail / lint rule for behavior |
| Sensor | Automated check (e.g., contrast/label linter) |
| Post-condition | Definition-of-done check for a stage |

</details>

## ✅ Checkpoint

<details>
<summary>1. In workshop mode, which design stage will you usually engage at, and why?</summary>

Refined Mockups (2.5), because workshop scope skips Ideation (so Rough Mockups 1.6 doesn't run). You also contribute to the User Stories mob (2.4).
</details>

<details>
<summary>2. Where do you put design-system and accessibility standards so the design agent uses them?</summary>

In Tier 2 team knowledge — `aidlc/knowledge/aidlc-design-agent/` (design-specific) or `aidlc/knowledge/aidlc-shared/` (team-wide). The agent loads them at stage start.
</details>

<details>
<summary>3. What's the difference between team Knowledge and a Rule?</summary>

Knowledge is reference material agents read; a Rule is a persistent behavioral constraint resolved through the org→team→project→phase→stage chain, and can pair with a Sensor for a deterministic check.
</details>

<details>
<summary>4. Why do mockup/design stages retain human validation?</summary>

Much of design quality is a judgment call, not a deterministic pass/fail, so those stages don't self-approve — human validation stays until standards are encoded as checkable post-conditions.
</details>

## Key takeaways

- Design lives in **Rough (1.6)** and **Refined (2.5)** mockups; in workshop mode you engage at **2.5** (+ the 2.4 mob).
- Encode your **design system + accessibility** as **Tier 2 team Knowledge** so the AI designs from them.
- Add **Rules** (optionally with Sensors) for behavioral guardrails.
- Design stays **human-validated** — that's where your expertise is the point.

**Next:** [U3 — Reviewing generated UI at the gates](U3-reviewing-ui-at-gates.md) — critiquing AI output against your standards and feeding corrections into the Learning Loop.
