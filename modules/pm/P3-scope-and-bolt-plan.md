# P3 — Scope Judgment & the Bolt Plan

> **Module:** P3 · **Track:** Product Manager add-on · **Time:** ~45 min · **Format:** 📖 Read + ✅ Quiz
> **Prerequisites:** [P2 — Facilitating Inception](P2-facilitating-inception.md)

## Learning objectives

By the end of this lesson you can:

- Judge whether the AI's **Units of work** are well-sized and independently buildable.
- Read the **dependency DAG** and the **Bolt plan** and spot sequencing problems.
- Explain **parallel batches** and how the walking skeleton anchors the plan.
- Push back on scope creep at the right gate.

## Why this matters

The decomposition into Units and Bolts is where "what we're building" becomes "how the work flows." Get the sizing right and Construction hums — reviewable slices, parallelizable work, an early confidence checkpoint. Get it wrong and you either drown in ceremony or land 15,000 lines of code in one unreviewable gate. As PM you're the person best placed to judge whether the slices match business reality.

## Read

### Units Generation (2.7): the decomposition

**Units Generation** always runs. The architect agent (with delivery support) decomposes your requirements/stories into **Units of work** and produces three artifacts worth reading carefully:

- **`unit-of-work.md`** — the Units themselves.
- **`unit-of-work-dependency.md`** — a **dependency DAG** (directed acyclic graph) showing which Units depend on which.
- **`unit-of-work-story-map.md`** — which user stories map to which Unit.

A good Unit is **cohesive** (one clear responsibility) and **loosely coupled** (buildable and, ideally, deployable on its own). Your validation questions:

- Could one person build this Unit end-to-end without constantly reaching into another?
- Does each Unit deliver something a user or the business can recognize?
- Are the dependencies real, or did the AI over-couple things that could be independent?

If a Unit is a grab-bag, ask to split it. If two Units are joined at the hip, ask whether they're really one.

### Delivery Planning (2.8): the Bolt plan

**Delivery Planning** turns Units into a **`bolt-plan.md`** (plus team allocation, sequencing rationale, and an external-dependency map). Recall from C2/C5: a **Bolt** is one Construction pass (stages 3.1–3.5) over a Unit or a small group of dependency-linked Units. The Bolt plan is the sequence and grouping of that work.

Read `risk-and-sequencing-rationale.md` alongside it — it tells you *why* the AI ordered things this way. Check that:

- The **walking skeleton** (first Bolt) is genuinely the thinnest end-to-end slice that touches the most integration points — not just the easiest Unit.
- High-risk or foundational Units come **early**, where a wrong assumption is cheap to fix.
- External dependencies (a third-party API, another team) are surfaced, not buried.

### Parallel batches

Bolts whose dependencies are satisfied and that don't depend on each other form a **parallel batch** — they can run concurrently, with a single gate at the end of the batch. This is the engine of workshop-mode throughput: after the walking skeleton, independent Bolts get claimed by different participants at once. When you review the plan, look for parallelism the DAG makes possible — and for false serialization (Bolts queued behind each other that don't actually depend on one another).

### The walking skeleton anchors everything

The first Bolt can't be flipped or skipped — it's the architecture's proof of life and the moment the **ladder prompt** sets autonomy for the rest. So the single most important sequencing judgment you make is *what goes in the walking skeleton*. Aim for the slice that retires the most integration risk: touch the database, an API boundary, and the UI (or equivalent) in the thinnest possible path.

### Saying no at the gate

Scope creep in AI-DLC usually shows up as Units quietly growing or new ones appearing. Your tools:

- At the Units or Delivery gate, **request changes** to cut or defer a Unit — point back to your MVP **OUT** list from P1.
- Use **"what must not change"** as a veto on Units that would touch protected surfaces.
- Remember the Units gate is an Ideation/Inception gate, so you can also **add a skipped stage** if the plan reveals you need one.

The gate is where product judgment earns its keep — the AI optimizes for a complete plan; you optimize for the *right* plan.

## 🧪 Try it (10 min)

Using the `bolt-plan.md` and Unit artifacts from your P2 run:

1. **Grade the Units.** Pick one and argue whether it's cohesive and independently buildable. Would you split or merge anything?
2. **Read the DAG.** Identify one pair of Bolts that could run as a **parallel batch**.
3. **Interrogate the skeleton.** Does the first Bolt retire the most integration risk? If not, propose a better one.
4. **Find the creep.** Spot one Unit or story that drifts beyond your P1 MVP-IN list and draft the "request changes" note to cut/defer it.

## Terminology

<details>
<summary><b>Show traditional-term mapping</b></summary>

| AI-DLC term | ≈ Traditional analogue |
| --- | --- |
| Unit of work | Buildable feature slice / component |
| Dependency DAG | Dependency graph / sequencing diagram |
| Bolt | Sprint's worth of one slice (hours/days) |
| Parallel batch | Concurrent workstreams |
| Walking skeleton | Thin end-to-end MVP / tracer bullet |
| `bolt-plan.md` | Iteration / release plan |

</details>

## ✅ Checkpoint

<details>
<summary>1. What makes a good Unit of work?</summary>

Cohesive (one clear responsibility) and loosely coupled (buildable, ideally deployable, on its own), delivering something recognizable to a user or the business.
</details>

<details>
<summary>2. What three artifacts does Units Generation produce, and which shows dependencies?</summary>

unit-of-work.md, unit-of-work-dependency.md (the dependency DAG), and unit-of-work-story-map.md. The dependency file shows the DAG.
</details>

<details>
<summary>3. What is a parallel batch and why does it matter in workshop mode?</summary>

A group of Bolts with satisfied, non-mutual dependencies that run concurrently under one end-of-batch gate. It's what lets multiple participants claim and build Bolts simultaneously.
</details>

<details>
<summary>4. Why is choosing the walking skeleton your most important sequencing call?</summary>

It can't be skipped/flipped, it proves the architecture, and its approval triggers the ladder prompt that sets autonomy for all remaining Bolts. It should retire the most integration risk.
</details>

<details>
<summary>5. How do you push back on scope creep?</summary>

Request changes at the Units/Delivery gate to cut or defer a Unit, citing your MVP OUT list and "what must not change"; add a skipped stage if needed.
</details>

## Key takeaways

- Validate that **Units are cohesive and independently buildable**; split grab-bags, merge Siamese twins.
- Read the **DAG** and **`bolt-plan.md`** together; check sequencing puts risk early and exposes parallelism.
- The **walking skeleton** is your highest-leverage sequencing choice — maximize integration-risk retired.
- The gate is where you **say no** — defend the MVP boundary you set in P1.

**PM track complete.** Regroup for the [Capstone](../capstone/X1-workshop-run.md) *(to be authored)*, or explore another role: [UX](../ux/U1-stories-as-contracts.md) · [Developer](../developer/D1-setup-claude-code-gitlab.md).
