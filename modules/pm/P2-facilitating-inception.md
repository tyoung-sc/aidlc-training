# P2 — Facilitating Workshop-Mode Inception

> **Module:** P2 · **Track:** Product Manager add-on · **Time:** ~60 min · **Format:** 🎧 Watch + 🧪 Hands-on
> **Prerequisites:** [P1 — Framing the Intent](P1-framing-the-intent.md)

## Learning objectives

By the end of this lesson you can:

- Run **Inception solo** on a shared remote so a whole group starts from the same approved artifacts.
- Facilitate the **Practices Discovery (2.2)** affirmation with the group, and explain why it's load-bearing.
- Drive Inception through to a reviewed **`bolt-plan.md`** the group can claim from.
- Explain the facilitator's handoff to participants.

## Why this matters

In a workshop — and in this bootcamp's capstone — one person runs Inception for everyone. If that Inception is sloppy or the practices aren't affirmed as a group, every participant inherits the mess on their own machine. The PM is the natural facilitator: Inception is your home turf. This lesson is how you set a group up to succeed.

## Read

### The shape of a facilitated run

Workshop mode has three parties: the **facilitator** (you) runs Inception solo on the shared remote; **participants** each clone that remote and claim a Construction Bolt to run locally; the **group** reviews gates together. Inception is **serial, at the facilitator's keyboard**; parallelism kicks in only in Construction. So your goal in Inception is a clean, approved set of artifacts everyone can build from.

Start it by naming the scope on a fresh workspace:

```
/aidlc --scope workshop
```

That births the first intent and stamps `Scope: workshop` (and `Default Test Strategy: Minimal`) into state. Workshop scope **skips Ideation entirely** (1.1–1.7) — the project is pre-decided, so there's nothing to ideate — and runs 25 of 32 stages, keeping every gate (the point is to *teach* the method, not skip ceremony).

> **Set it once for everyone:** put `AWS_AIDLC_DEFAULT_SCOPE=workshop` in `.claude/settings.json` so every participant who runs `/aidlc` in a clone gets workshop routing without remembering the flag.

### Inception, stage by stage (2.1–2.8)

You'll drive these in order, hitting each gate:

| Stage | What you produce | Your facilitation focus |
| --- | --- | --- |
| 2.1 Reverse Engineering *(brownfield only)* | ~9 artifacts mapping the existing system | Confirm the map matches reality |
| **2.2 Practices Discovery** | `team-practices.md`, `discovered-rules.md` | **Run the affirmation with the group** (see below) |
| 2.3 Requirements Analysis | `requirements.md` | Apply everything from P1 |
| 2.4 User Stories *(mob)* | `stories.md`, `personas.md` | Review stories as contracts |
| 2.6 Application Design | design artifacts, ADRs | Sanity-check the shape (lean on architects) |
| 2.7 Units Generation | `unit-of-work.md`, dependency DAG, story map | The decomposition participants will claim |
| 2.8 Delivery Planning | **`bolt-plan.md`**, team allocation, sequencing rationale | **Review with the group before Construction** |

### Stage 2.2 is load-bearing — do it with the group

**Practices Discovery** is where the team affirms its **way of working**: branching strategy, walking-skeleton stance, testing posture, deployment cadence. Construction reads those affirmations on *every per-Bolt decision* on *every participant's machine* — including the git base branch each participant branches from. Run this gate **with the group, not solo**. Affirmed practices get promoted into the active space's memory (`team.md` / `project.md`), becoming the single source of truth everyone pulls. Rush it and participants will make inconsistent choices later.

### End Inception on a reviewed Bolt plan

When **Delivery Planning (2.8)** emits **`bolt-plan.md`**, review it **with the group before proceeding to Construction** — the Bolt list is literally what participants will claim, so they need to see and agree on it. Then push the approved Inception artifacts to the shared remote. From here, participants pull and claim (that's P3 and the Developer track's D3).

### The handoff

Your Inception output — approved requirements, stories, units, and the Bolt plan, plus affirmed practices in space memory — is the contract the whole group builds against. A good facilitator makes that handoff explicit: "Here's the Bolt plan; here's our affirmed way of working; claim a Bolt by pushing its branch."

## 🎧 See it (8 min)

*Screencast placeholder — [P2: Facilitating Inception for a mob, 8 min].* A facilitator runs `--scope workshop`, drives 2.2 as a group affirmation (branching + testing posture), moves through requirements and units, reviews `bolt-plan.md` with the room, and pushes to the shared remote.

## 🧪 Try it (25 min)

Pair up if you can (one facilitator, one+ participants); solo is fine too.

1. **Start workshop mode** — `/aidlc --scope workshop` on the shared repo. Confirm state shows `Scope: workshop`.
2. **Run Practices Discovery (2.2)** — at its gate, *decide as a group*: trunk-based or gitflow? walking-skeleton first? test posture? Affirm and note where it lands in space memory.
3. **Advance to Units (2.7)** — read `unit-of-work.md` and the dependency DAG. Are the Units independently buildable?
4. **Reach Delivery Planning (2.8)** — read `bolt-plan.md`. Confirm each Bolt is something a single person could claim and run.
5. **Handoff** — write the one-line instruction you'd give participants to claim their first Bolt.

✅ **Done when:** you have an approved `bolt-plan.md` and an affirmed way-of-working the group agreed to.

## Terminology

<details>
<summary><b>Show traditional-term mapping</b></summary>

| AI-DLC term | ≈ Traditional analogue |
| --- | --- |
| Practices Discovery (2.2) | Team working-agreements / definition-of-done workshop |
| Way of working | Team norms / branching + testing conventions |
| Units Generation (2.7) | Breaking the epic into buildable slices |
| `bolt-plan.md` | Sprint/iteration plan |
| Delivery Planning (2.8) | Release/sequencing plan |
| Shared remote | The team's origin repo |

</details>

## ✅ Checkpoint

<details>
<summary>1. Why does workshop scope skip Ideation?</summary>

The project is pre-decided by the facilitator, so there's nothing to ideate. It runs 25/32 stages and keeps every gate to teach the method.
</details>

<details>
<summary>2. Why must Practices Discovery (2.2) be run with the group?</summary>

Its affirmations (branching, testing posture, walking-skeleton stance, base branch) govern per-Bolt decisions on every participant's machine. If it's rushed or done solo, participants make inconsistent choices in Construction.
</details>

<details>
<summary>3. What is bolt-plan.md and why review it with the group?</summary>

The output of Delivery Planning (2.8) — the list of Bolts participants will claim. They need to see and agree on it before Construction opens.
</details>

<details>
<summary>4. In workshop mode, which phase is serial and which is parallel?</summary>

Inception is serial at the facilitator's keyboard; Construction is parallel — participants claim and run Bolts on their own clones.
</details>

## Key takeaways

- The facilitator runs **Inception solo** on a shared remote; participants build in **parallel** afterward.
- `--scope workshop` **skips Ideation**, keeps every gate, defaults to Minimal tests.
- **Practices Discovery (2.2) is a group affirmation** — it sets the way of working everyone inherits.
- End Inception on a **group-reviewed `bolt-plan.md`**, then push and hand off.

**Next:** [P3 — Scope judgment & the Bolt plan](P3-scope-and-bolt-plan.md) — sizing Units, sequencing Bolts, and validating the AI's decomposition.
