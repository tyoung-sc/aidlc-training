# U3 — Reviewing Generated UI at the Gates

> **Module:** U3 · **Track:** UX Designer add-on · **Time:** ~45 min · **Format:** 🧪 Hands-on + ✅ Graded
> **Prerequisites:** [U2 — Design in the workflow](U2-design-in-the-workflow.md)

## Learning objectives

By the end of this lesson you can:

- Critique generated mockups/UI against your design system and accessibility standards at a gate.
- Give **specific, actionable** revision feedback the design agent can act on.
- Turn a repeated correction into a durable **Rule/Sensor** via the **Learning Loop**.
- Decide when to approve, request changes, or accept-as-is on a design artifact.

## Why this matters

The gate is where your judgment actually lands. Approving a mockup that violates your standards ships that violation into the code the developer agent generates from it. But the deeper payoff is compounding: every correction you make can become a Rule the AI follows *next time*, so your review work makes future runs better instead of repeating itself.

## Read

### Reviewing a design artifact at the gate

When Refined Mockups (2.5) — or any UI-bearing stage — reaches its approval gate, you're the reviewer. Recall the gate options from C5: **Approve**, **Request Changes**, and (after enough revision cycles) **Accept-as-is**. Before touching them, open the artifact and run it against a checklist:

- **Design system** — components, tokens, spacing, typography from your standards? Any invented patterns?
- **Accessibility** — contrast (AA/AAA as you set), keyboard operability, labels, focus order, alt text, target sizes.
- **States** — empty, loading, error, and edge states present, not just the happy path?
- **Content** — labels/microcopy match your voice and are unambiguous?
- **Interaction spec** — behaviors defined enough that a developer (and the developer agent) won't guess?

### Feedback the agent can act on

Vague feedback wastes a revision cycle. Compare:

- 🚫 *"Make it more on-brand."*
- ✅ *"Replace the custom green (#2ea44f) with `color.primary` from our tokens; increase body text to 16px for AA contrast; add an empty state for zero results using the standard EmptyState component."*

Specific, testable feedback is the design equivalent of a good acceptance criterion — it tells the agent exactly what "fixed" means.

### Turn corrections into durable Rules: the Learning Loop

Here's the compounding part. While a stage runs, the orchestrator records observations in a `memory.md` diary. **At the approval gate, it surfaces those observations and asks which to keep.** Each confirmed learning is written as a **practice** into the active space's project memory (with one-click promotion to team memory), or it **scaffolds a new Sensor**. So when you correct the same thing twice — "colors must come from tokens" — you can promote it to a Rule the design agent honors on every future run, or a Sensor that deterministically flags non-token colors. Your review stops being repetitive and starts hydrating the system (exactly the Generate-Verify-**Learn** idea from the spec).

Practically: when the gate asks what to keep, say yes to the corrections you'd otherwise have to repeat.

### Approve, request changes, or accept-as-is?

- **Request changes** when a standard is violated and it's fixable — the normal path; be specific.
- **Approve** only after re-reading the revised artifact against your checklist.
- **Accept-as-is** (available after repeated revisions) when remaining issues are minor and logged — don't let a design stage trap the workshop, but record the debt.

Remember the human-turn safeguard from C5: your approval requires a real action, and it should follow a real read. Never vibe-approve a screen.

## 🧪 Try it — graded (25 min)

Continue a UI feature on the workshop repo to a Refined Mockups (2.5) gate.

1. **Checklist review.** Run the generated mockup against the five checklist areas above; write down every deviation.
2. **Specific feedback.** Use **Request Changes** with at least three concrete, testable fixes (name tokens/components/criteria).
3. **Re-review.** Confirm the revision fixed exactly what you asked — not more, not less.
4. **Promote a learning.** At the gate, confirm one correction into a **Rule** (or Sensor) via the Learning Loop, and note where it landed in space memory.
5. **Decide.** Approve deliberately, or justify an accept-as-is with the residual issue logged.

✅ **Graded pass = you:** reviewed against the checklist, gave specific fixes, and promoted at least one correction into a durable Rule/Sensor.

## Terminology

<details>
<summary><b>Show traditional-term mapping</b></summary>

| AI-DLC term | ≈ Traditional analogue |
| --- | --- |
| Learning Loop | Design-review feedback that becomes a standard |
| Practice / Rule | Design guideline the AI now follows |
| Sensor | Automated check (contrast/token/label linter) |
| `memory.md` | The stage's running notes/observations |
| Accept-as-is | Approve with logged design debt |

</details>

## ✅ Checkpoint

<details>
<summary>1. What should you do before touching the gate buttons on a mockup?</summary>

Open the artifact and review it against your checklist — design system, accessibility, states, content, interaction spec.
</details>

<details>
<summary>2. What makes design feedback actionable?</summary>

Specificity — name the exact token/component/criterion and what "fixed" means, like a good acceptance criterion. Not "make it on-brand."
</details>

<details>
<summary>3. How does a one-off correction become a durable standard?</summary>

The Learning Loop surfaces stage observations at the gate; you confirm which to keep, and each becomes a practice/Rule in project memory (promotable to team) or scaffolds a Sensor.
</details>

<details>
<summary>4. When is accept-as-is appropriate for a design artifact?</summary>

After repeated revisions, when remaining issues are minor and logged — so a design stage can't stall the workshop, while the debt is recorded.
</details>

## Key takeaways

- The gate is where your judgment lands — **review against a checklist before approving.**
- Give **specific, testable** revision feedback, not vibes.
- Use the **Learning Loop** to promote repeated corrections into **Rules/Sensors** — your review compounds.
- Never **vibe-approve** a screen; approval follows a real read.

**UX track complete.** Regroup for the [Capstone](../capstone/X1-workshop-run.md) *(to be authored)*, or explore another role: [PM](../pm/P1-framing-the-intent.md) · [Developer](../developer/D1-setup-claude-code-gitlab.md).
