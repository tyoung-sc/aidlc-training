---
title: "Capstone — Workshop Run"
nav_order: 7
---

# X1 — Capstone: A Real Workshop-Mode Run

> **Module:** X1 · **Track:** Capstone (all roles, mixed teams) · **Time:** ~2.5 h · **Format:** 🧪 Hands-on (assessed)
> **Prerequisites:** Shared Core [C1–C6](../shared-core/C1-why-aidlc.md) + your role add-on ([PM](../pm/P1-framing-the-intent.md) · [UX](../ux/U1-stories-as-contracts.md) · [Developer](../developer/D1-setup-claude-code-gitlab.md))

## What the capstone is

A mixed-role "mob" takes **one Intent** from inputs through Inception gates and into **parallel Construction Bolts** on a shared remote — greenfield or brownfield — using the built-in **`workshop` scope**. It's the whole method, end to end, exactly as a real team would run it. Everyone practices their role *and* sees how the roles interlock.

## Learning objectives

By the end you can:

- Run AI-DLC end to end as a team: Inception → Bolt plan → parallel Construction → Build & Test.
- Play your role at each gate and hand off cleanly to the next.
- Read and decide at gates under mild time pressure without vibe-coding.
- Reflect on what you'd encode as Knowledge/Rules to make the next run better.

## Setup (facilitator, ~15 min before)

1. Prepare a shared remote from a **greenfield** or **brownfield** seed repo (pick one per team).
2. `AWS_AIDLC_DEFAULT_SCOPE=workshop` in `.claude/settings.json` so every clone starts in workshop scope.
3. Confirm `/aidlc --doctor` is green on the shared repo; push it.
4. Pre-decide the project and write a one- or two-sentence **Intent** (this is a workshop — participants build it, they don't choose it).

## The run (≈2 h)

### Phase A — Inception, together (~45 min) · led by the PM/facilitator

1. `/aidlc --scope workshop` — confirm state shows `Scope: workshop` (Ideation is skipped).
2. **Practices Discovery (2.2)** — affirm way-of-working *as a group*: base branch, walking-skeleton stance, testing posture. (This governs everyone's Construction — see [P2](../pm/P2-facilitating-inception.md).)
3. **Requirements (2.3)** — PM drives; UX contributes user needs; read `requirements.md` before approving ([P1](../pm/P1-framing-the-intent.md)).
4. **User Stories (2.4)** — the mob; UX ensures stories are testable contracts with accessibility criteria ([U1](../ux/U1-stories-as-contracts.md)).
5. **Refined Mockups (2.5)** *(if UI)* — UX reviews against encoded standards ([U2](../ux/U2-design-in-the-workflow.md)).
6. **Units (2.7) + Delivery Planning (2.8)** — review `unit-of-work.md`, the DAG, and `bolt-plan.md` together; agree who claims what ([P3](../pm/P3-scope-and-bolt-plan.md)). Push approved Inception to the remote.

### Phase B — Construction, in parallel (~60 min) · developers claim; all review

7. **Walking skeleton first.** One developer runs Bolt 1 (stages 3.1–3.5) with the group watching; the whole team reviews the skeleton gate — it sets the shape for everyone ([D3](../developer/D3-construction-bolts.md)).
8. **Ladder choice.** The group decides `autonomous` or `gated` for the remaining Bolts, and says why.
9. **Claim & build.** Developers `git fetch --all`, branch `bolt-<name>` off the affirmed base, `git push` to claim (first push wins), and run their Bolt locally. UX/PM review design and requirement fidelity at gates.
10. **Push back** approved Bolts to the remote.

### Phase C — Integrate & verify (~20 min)

11. **Build & Test (3.6)** runs once across all Bolts; read the quality report together ([D4](../developer/D4-build-test-control-loop.md)).
12. **CI (3.7)** *(if in scope)* — review the emitted pipeline config.
13. Reach **Verification Gate 3**. Note what shipped and what's logged as residual.

## Assessment rubric

Score each 0–2 (0 missing · 1 partial · 2 solid). **Pass = 12/16 and no zeros on the ⚠️ items.**

| # | Criterion | Evidence |
| --- | --- | --- |
| 1 | **Intent & inputs** clear and bounded (OUT list, must-not-change) | `requirements.md` |
| 2 | **Practices affirmed as a group** at 2.2 | space memory `## Way of Working` |
| 3 | **Stories are testable contracts** with accessibility | `stories.md` / `personas.md` |
| 4 ⚠️ | **Read before approving** at every gate (no vibe-coding) | revision feedback quality |
| 5 | **Units well-sized**; Bolt plan sequences risk early | `bolt-plan.md`, DAG |
| 6 ⚠️ | **Walking skeleton** retires real integration risk | Bolt 1 artifacts |
| 7 | **Deliberate ladder choice** justified for this project | state + rationale |
| 8 | **Clean Bolt claiming** via git; Build & Test read critically | branches + quality report |

## Debrief (~15 min)

As a group, answer:

- Where did a gate catch something a rubber-stamp would have missed?
- What one thing would you encode as **Knowledge** or a **Rule/Sensor** to make the next run smoother? (Tie it to the Learning Loop.)
- Greenfield vs. brownfield: what differed in practice from what you expected in [C6](../shared-core/C6-greenfield-vs-brownfield.md)?
- What surprised you about your *own* role — and about another role's?

## Terminology

<details>
<summary><b>Show traditional-term mapping</b></summary>

| AI-DLC term | ≈ Traditional analogue |
| --- | --- |
| Workshop-mode run | A facilitated team build sprint |
| Mob | Whole-team working session |
| Bolt claiming | Assigning a work slice |
| Walking skeleton | Tracer bullet / thin MVP |
| Verification Gate 3 | End-of-construction sign-off |

</details>

## Key takeaways

- You've run **the whole method as a team** — Inception to verified build — on the workshop scope.
- The roles **interlock**: PM frames, UX contracts the experience, developers build, everyone gates.
- The habit that carried the whole run was **read-before-approve**.
- The Learning Loop turns this run's corrections into next run's standards.

**You've completed the bootcamp core.** Go deeper with the electives: [A1 — Inside v2](../electives/A1-inside-v2.md) · [A2 — Rules, Sensors & progressive autonomy](../electives/A2-progressive-autonomy.md).
