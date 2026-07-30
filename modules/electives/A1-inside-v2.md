# A1 — Inside v2: Engine, Conductor & Agents

> **Module:** A1 · **Track:** Elective (self-paced) · **Time:** ~45 min · **Format:** 📖 Read + 🎧 Watch
> **Prerequisites:** Shared Core [C1–C6](../shared-core/C1-why-aidlc.md)

## Learning objectives

By the end of this lesson you can:

- Explain the **engine ↔ conductor** split and why routing is deterministic.
- Name the four **execution topologies** (inline / subagent / pipeline / mob) and an example of each.
- Describe the **14-agent** roster and "small mob, broad agents."
- Explain the **three planes** and why a mid-run learning applies on the *next* run.

## Why this matters

You can use AI-DLC well knowing only the workflow. But understanding the machinery explains *why* it behaves as it does — why routing is reproducible, why some stages feel collaborative and others autonomous, and why a correction you make now shows up next time, not this instant. That mental model makes you better at customizing it (A2).

## Read

### Engine and conductor

AI-DLC runs a simple loop with a deliberate division of labor:

- The **engine** (`aidlc-orchestrate.ts`) is **deterministic**. It owns *routing*: which stage is next, which scope, when to stop, gate status. It has exactly three verbs — `next`, `report`, `park` — and emits a typed **directive** ("run this stage," "ask this," "you're done").
- The **conductor** (the `/aidlc` session, `SKILL.md`) carries out each directive — running the stage, asking you questions, dispatching a swarm — then reports the outcome and asks the engine for the next move.

The split matters: routing is deterministic (so runs are reproducible and recover cleanly after a restart), while execution quality lives with the conductor and agents. The engine decides *what*; the conductor owns *how well*.

### Four execution topologies

Most stages run **inline** — the conductor adopts the stage's lead agent as a persona and works with you directly, supporting real-time questions and approval. Some stages instead **dispatch** collaborators. There are four modes, and the shipped split is **28 inline / 2 subagent / 1 pipeline / 1 mob**:

| Topology | Shape | Shipped example |
| --- | --- | --- |
| **inline** | Conductor adopts the persona in-conversation | most stages |
| **subagent** | Hub-and-spoke: lead + independent contributors | Practices Discovery (2.2), Code Generation (3.5) |
| **pipeline** | Chain: links advance artifacts in sequence | Reverse Engineering (2.1) |
| **mob** | Mesh: collaborators write in parallel, lead integrates | User Stories (2.4) |

On every topology **the conductor performs every delegation** — agents never invoke each other. That "no hidden delegation" rule keeps the run auditable.

### Small mob, broad agents

Rather than dozens of narrow specialists (which recreates waterfall handoffs), AI-DLC ships **14 personas**: 11 broadly capable domain experts, 2 reviewers, and a composer. Each expert spans multiple stages and carries context forward, so there are fewer handoffs and fewer information-loss points. You've already met your role's counterpart — product, design, developer — plus the architect (the broadest, ~9 stages), delivery, AWS-platform, devsecops, compliance, quality, pipeline-deploy, and operations agents. Support agents (e.g. devsecops, compliance) participate *within* stages led by others rather than existing as separate lead roles.

### The three planes

Borrowing from networking, the framework separates three concerns:

- **Control plane** — the *schema* of what should run: stage definitions, Rules, Sensors. Compiled **once** at workflow start (allowed to be slow and clever).
- **Data plane** — the *actual runs*: stage executions, agent invocations, the files in the intent record. Fast, repeated, reads pre-resolved answers.
- **Management plane** — *observe and configure*: `/aidlc --doctor`, the audit log, `CLAUDE.md`. Human-cadence.

This is why a learning captured mid-workflow waits for the **next** compile: answers are computed at "topology-change time" (workflow start), not "packet time" (every stage). The payoff is reproducible runs and clean recovery.

## 🎧 See it (6 min)

*Screencast placeholder — [A1: The engine/conductor loop in one run, 6 min].* Trace a single stage: engine emits `run-stage` → conductor executes inline → reports → engine routes to the next, pausing to show a subagent dispatch and the audit rows.

## Terminology

<details>
<summary><b>Show traditional-term mapping</b></summary>

| AI-DLC term | ≈ Traditional analogue |
| --- | --- |
| Engine | Deterministic workflow router/orchestrator |
| Conductor | The session that runs the plan |
| Inline / subagent / pipeline / mob | Execution/collaboration patterns |
| Control/data/management plane | Config vs. runtime vs. ops surfaces |
| Composer | Adaptive planner that tailors the workflow |

</details>

## ✅ Checkpoint

<details>
<summary>1. What does the engine own vs. the conductor?</summary>

The engine deterministically owns routing (next stage, scope, stop, gate status) via next/report/park; the conductor executes each directive and owns execution quality.
</details>

<details>
<summary>2. Name the four execution topologies and one example each.</summary>

Inline (most stages), subagent/hub-and-spoke (Practices Discovery 2.2, Code Generation 3.5), pipeline (Reverse Engineering 2.1), mob (User Stories 2.4).
</details>

<details>
<summary>3. Why "small mob, broad agents"?</summary>

Broad agents span multiple stages and carry context, cutting handoffs and information loss versus many narrow specialists (which recreates waterfall).
</details>

<details>
<summary>4. Why does a mid-run learning apply only next run?</summary>

Rules/sensors compile into the control-plane graph once at workflow start; the data plane reads pre-resolved answers, so a new learning takes effect at the next compile.
</details>

## Key takeaways

- **Engine (deterministic routing) + conductor (execution)** = reproducible runs, clean recovery.
- Four topologies — **inline / subagent / pipeline / mob**; the conductor always delegates, agents never self-invoke.
- **14 broad agents** minimize handoffs.
- **Three planes** explain why learnings land on the next compile.

**Next:** [A2 — Rules, Sensors & Progressive Autonomy](A2-progressive-autonomy.md) — how to extend and safely automate more of the workflow over time.
