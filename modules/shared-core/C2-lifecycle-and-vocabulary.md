---
title: "C2 — Lifecycle & Vocabulary"
parent: Shared Core
nav_order: 2
---

# C2 — The Lifecycle & the Vocabulary Bridge

> **Module:** C2 · **Track:** Shared Core (all roles) · **Time:** ~45 min · **Format:** 📖 Read + ✅ Quiz
> **Prerequisites:** [C1 — Why AI-DLC](C1-why-aidlc.md)

## Learning objectives

By the end of this lesson you can:

- Name the **5 phases** of AI-DLC and what each is for.
- Explain how a workflow is driven (engine vs. conductor) and what an **approval gate** is.
- Read the core vocabulary the tool prints — **Intent, Unit, Bolt, Scope, Space, Agent** — and map each to a traditional analogue.
- Explain "small mob, broad agents" and how **scope** and **depth** shape a run.

## Why this matters

The moment you run `/aidlc`, the screen fills with words like *Intent*, *stage 2.4*, *Bolt*, *scope: mvp*. If those are unfamiliar you'll hesitate at exactly the points where you're supposed to be deciding. This lesson makes the vocabulary and the shape of a run second nature, so your attention goes to judgment, not jargon.

## Read

### One command, a driven loop

You start everything with a single command:

```
/aidlc Build a REST API for inventory management
```

Under the hood a deterministic **engine** decides what happens next (which stage, which scope, when to stop) and a **conductor** — the `/aidlc` session itself — carries it out and then asks the engine for the next move. You don't memorize a pipeline; you respond at the gates. `bun` is the only prerequisite, and in this bootcamp you'll run it on the **Claude Code** harness.

### The 5 phases (and 32 stages)

A workflow moves through five phases in order. Each phase holds several numbered stages (e.g. `2.4`), and each stage has defined inputs/outputs, a lead **agent**, and — for most — an **approval gate** where you review before moving on. Between phases, an automated **verification gate** checks traceability so nothing downstream builds on a broken link.

```
  0 INITIALIZATION   (0.1–0.3)  auto, no gates — is born in <1s
        │
  1 IDEATION         (1.1–1.7)  shape the idea (skipped by some scopes)
        │  ▼ verification gate
  2 INCEPTION        (2.1–2.8)  requirements, user stories, units of work
        │  ▼ verification gate
  3 CONSTRUCTION     (3.1–3.7)  design → code → build & test → CI, in Bolts
        │  ▼ verification gate
  4 OPERATION        (4.1–4.7)  deploy, observe, maintain
        └───────── feedback loop back to Ideation
```

- **Initialization** runs automatically in under a second — it "births" the intent and sets up state. No gate.
- **Inception** is where requirements, user stories, and the decomposition into **Units of work** happen — the heart of planning.
- **Construction** turns Units into working, tested code, executed in **Bolts** (more below).
- **Operation** covers deployment and running the system.

### Small mob, broad agents

Rather than dozens of narrow specialists (which recreates waterfall handoffs), AI-DLC uses **14 personas**: 11 broadly capable domain experts — architect, developer, product manager, and so on — plus 2 reviewers and a composer. Each agent spans multiple stages and carries context forward, mirroring how a tight 3–5 person mob covers a whole feature. When a stage runs, the conductor adopts that stage's lead agent's perspective and works with you directly.

### Scope and depth: the two dials

You rarely run all 32 stages. A **scope** selects which stages execute and their default **depth**:

- **Scope** — one of 9 named presets (`enterprise`, `feature`, `mvp`, `poc`, `bugfix`, `refactor`, `infra`, `security-patch`, `workshop`), or auto-detected from your request. A `bugfix` skips most of Inception; `enterprise` runs the works; **`workshop`** is the one we use for training labs.
- **Depth** — Minimal, Standard, or Comprehensive — how much detail each stage produces. You can override it at any gate.

Greenfield vs. brownfield mostly comes down to scope plus whether **Reverse Engineering** (stage 2.1) runs to model an existing codebase first.

### Bolts, the walking skeleton, and the autonomy ladder

Construction executes in **Bolts** — a Bolt is one pass through the core Construction stages (3.1–3.5) for a Unit or a small group of Units. The **first** Bolt is the **walking skeleton**: the thinnest end-to-end slice that touches every integration point, always gated so you can confirm the overall shape. Right after you approve it, a **ladder prompt** asks whether the remaining Bolts should run **autonomously** or stay **gated**. That single choice is how you dial in how much you review — and it's the practical face of "progressive autonomy."

### The vocabulary bridge

Here's the cheat-sheet. AI-DLC term first (because the tool prints it), traditional analogue alongside.

| AI-DLC term | ≈ Traditional analogue | One-line definition |
| --- | --- | --- |
| **Intent** | Epic / initiative | High-level statement of what to build; the root of a tracked record. |
| **Unit (of work)** | Sub-domain / component slice | Independently implementable piece; decomposed at stage 2.7. |
| **Bolt** | Sprint (hours/days) | One Construction pass over a Unit; first Bolt = walking skeleton. |
| **Phase / Stage** | SDLC phase / step | 5 phases, 32 numbered stages. |
| **Scope** | Workflow preset | Chooses which stages run + default depth. |
| **Space** | Team workspace | Holds a team's memory, knowledge, and intent records. |
| **Agent (persona)** | Specialist role | One of 14 personas the conductor activates. |
| **Approval gate** | Review / sign-off | Where you approve, request changes, or accept-as-is. |
| **Walking skeleton** | Thin end-to-end MVP slice | The first, always-gated Bolt. |
| **Autonomy mode** | How much you review | `autonomous` vs `gated`, set at the ladder prompt. |

## 🎧 See it (6 min)

*Screencast placeholder — [C2: Anatomy of a `/aidlc` run, 6 min].* Watch a single intent move from Initialization through an Inception gate into the first Construction Bolt, pausing to point out the scope banner, a stage number, an agent persona, and the ladder prompt.

## 🧪 Try it (5 min)

Still no install needed. Using the intent you wrote in C1:

1. Which **scope** would you pick — `poc`, `mvp`, `feature`, or `enterprise` — and why?
2. Sketch two or three **Units of work** you'd expect the AI to decompose it into.
3. Which Unit would make the best **walking skeleton** (thinnest slice touching the most integration points)?

Keep this — you'll reuse it when you run the real thing in C3–C5.

## Terminology

<details>
<summary><b>Show traditional-term mapping</b></summary>

Use the vocabulary-bridge table above as your toggle reference. Rule of thumb: if a teammate says "epic," they mean **Intent**; "sprint" ≈ **Bolt**; "which template are we running?" ≈ **scope**. The tool never says "epic" or "sprint" — so learn to hear both.

</details>

## ✅ Checkpoint

<details>
<summary>1. List the 5 phases in order.</summary>

Initialization → Ideation → Inception → Construction → Operation.
</details>

<details>
<summary>2. What's the difference between the engine and the conductor?</summary>

The engine deterministically decides what happens next (routing, scope, stop conditions); the conductor (the `/aidlc` session) carries out each move and reports back, owning execution quality.
</details>

<details>
<summary>3. What is a Bolt, and what's special about the first one?</summary>

A Bolt is one Construction pass (stages 3.1–3.5) over a Unit or small group. The first Bolt is the walking skeleton — the thinnest end-to-end slice, always gated — after which the ladder prompt sets autonomy mode.
</details>

<details>
<summary>4. What do "scope" and "depth" control, and which scope do we use for labs?</summary>

Scope selects which stages run (and default depth); depth controls how much detail each stage produces. Labs use the `workshop` scope.
</details>

<details>
<summary>5. A teammate says "I've decomposed the epic into three stories for this sprint." Translate to AI-DLC terms.</summary>

"I've decomposed the **Intent** into three **user stories** for this **Bolt**." (Units of work sit between Intent and Bolt; user stories keep their name.)
</details>

## Key takeaways

- One command (`/aidlc`), a driven loop: **engine decides, conductor executes, you approve.**
- **5 phases / 32 stages**, with gates between phases and at most stages.
- **Scope** and **depth** shape every run; **`workshop`** is our lab scope.
- Construction runs in **Bolts**; the **walking skeleton** + **ladder prompt** set how much you review.
- Learn the vocabulary bridge cold — the tool speaks AI-DLC, your teammates may speak Agile.

**Next:** [C3 — Setup & your first `/aidlc`](C3-setup.md) *(to be authored)* — install `bun` + Claude Code, run `--doctor`, and launch a tiny workflow end to end.
