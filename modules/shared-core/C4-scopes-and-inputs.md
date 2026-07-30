# C4 — Scopes, Depth & Inputs That Work

> **Module:** C4 · **Track:** Shared Core (all roles) · **Time:** ~75 min · **Format:** 📖 Read + 🧪 Hands-on
> **Prerequisites:** [C3 — Setup & first `/aidlc`](C3-setup.md)

## Learning objectives

By the end of this lesson you can:

- Pick an appropriate **scope** for a task and read the confirmation line before consenting.
- Choose a **depth** (and know it's overridable at any gate).
- Write an **intent** specific enough for the engine to route well.
- Explain **auto-detect vs. explicit scope vs. compose**, and how greenfield/brownfield is inferred.

## Why this matters

Scope is the single most consequential choice in a run: `poc` executes 8 stages with 5 gates; `feature` executes all 32 with 29 gates. Pick too heavy and the team drowns in ceremony; too light and you skip the design a risky change needed. Learning to match scope and depth to the task — and to write an intent the engine can read — is most of what "using AI-DLC well" means day to day.

## Read

### Three dials: scope, depth, test strategy

- **Scope** = *which stages run.* One of 9 presets (or a composed one).
- **Depth** = *how much detail* each stage produces (Minimal / Standard / Comprehensive).
- **Test strategy** = *how many tests* get generated (Minimal / Standard / Comprehensive).

A scope sets sensible defaults for the other two; you can override either at any gate.

### The 9 scopes at a glance

| Scope | Stages | Depth | Use when |
| --- | --- | --- | --- |
| `enterprise` | 32/32 | Comprehensive | Regulated feature, full audit trail |
| `feature` | 32/32 | Standard | **Default** for a new feature of any size |
| `mvp` | 22/32 | Standard | Greenfield MVP; skips late Operation stages |
| `poc` | 8/32 | Minimal | Prove feasibility fast |
| `bugfix` | 7/32 | Minimal | Fix a specific bug |
| `refactor` | 8/32 | Minimal | Restructure code without changing behavior |
| `infra` | 13/32 | Standard | Infrastructure / deployment change |
| `security-patch` | 10/32 | Minimal | CVE / vulnerability response |
| `workshop` | 25/32 | Standard (**Minimal** tests) | **Our lab scope** — pre-decided project, mob run, skips Ideation |

The order-of-magnitude spread is the point: choose the lightest scope that still produces every artifact your outcome depends on.

### Writing an intent that works

Your intent is the input the engine routes on. A good one names the **outcome** and enough **specificity** to disambiguate — without pre-writing the design.

- 🚫 *"Improve the app"* — no outcome, no scope signal.
- ⚠️ *"Add search"* — routable but vague; expect many clarifying questions.
- ✅ *"Build a REST endpoint that lets signed-in users search their own orders by date range, in-memory for now"* — clear outcome, boundary, and a stated simplification.

You don't write the plan; you write the *destination* clearly (recall the Google Maps analogy from C1). Constraints and "what must not change" are especially valuable — they steer routing and later gates.

### Three ways a scope gets chosen

**1. Auto-detect from keywords.** Just describe the work; the engine matches keywords to a scope:

| Keywords | Scope |
| --- | --- |
| fix, bug, broken | `bugfix` |
| refactor, clean up, simplify | `refactor` |
| infrastructure, deploy, infra | `infra` |
| security, CVE, vulnerability, patch | `security-patch` |
| proof of concept, prototype, poc, spike | `poc` |
| mvp, minimum viable | `mvp` |
| workshop, lab, training | `workshop` |
| everything else | `feature` |

After a clear match you get a **confirmation line** that names the exact ceremony — *"a 'bugfix' workflow … 7 of 32 stages, 4 approval gates, 1 stage repeats per unit of work. Confirm, name a different scope, or say 'compose'."* **Read it before you confirm** — that's you consenting to the ceremony.

**2. Explicit scope.** Name it yourself when you already know:

```
/aidlc bugfix Fix the login timeout issue
/aidlc --scope workshop
```

**3. Compose (the adaptive composer).** When no stock scope fits — rich prose, a keyword buried in a long description (the *disambiguation rule*: keyword + more than ~5 words of description defers to compose) — `/aidlc` offers to **compose** a tailored plan. The composer scores five entropy signals (intent ambiguity, codebase uncertainty, verification entropy, risk, unresolved assumptions) and proposes the *minimum viable* EXECUTE/SKIP grid, with a reason for every stage, at a gate you approve, edit, or reject. Nothing is written until you approve.

### Depth: right-sizing the detail

| Depth | You get | Use for |
| --- | --- | --- |
| **Minimal** | 1–2 page artifacts, key decisions only | quick fixes, PoCs |
| **Standard** | Complete artifacts, concise rationale | most features and MVPs |
| **Comprehensive** | Exhaustive detail, compliance cross-refs | regulated / enterprise |

Override anytime: the `--depth` flag (`/aidlc --scope bugfix --depth standard`), at scope confirmation, or as feedback at any approval gate.

### Greenfield vs. brownfield — mostly automatic

You don't set a "brownfield" flag. Initialization detects whether the workspace already has code, and scope/compose decide whether **Reverse Engineering** (stage 2.1) runs to model the existing system before changes. Greenfield work skips it. So the same intent behaves differently in an empty repo vs. an existing codebase — which is exactly why the two tracks in this bootcamp practice the *same* skills against different seeded repos.

## 🎧 See it (6 min)

*Screencast placeholder — [C4: One intent, three scopes, 6 min].* Run the same intent three ways — auto-detected, explicitly as `poc`, and via `compose` — pausing on each confirmation line to compare stage/gate counts, then override depth at a gate.

## 🧪 Try it (25 min)

Reusing the intent you sketched in C1–C2, on the workshop repo from C3:

1. **Predict.** Before running, write down which scope you *expect* and why.
2. **Auto-detect.** Run `/aidlc <your intent>` (no scope flag). Read the confirmation line — does the matched scope and gate count match your prediction? **Don't confirm past the first gate.**
3. **Compare.** Start again naming a lighter scope explicitly (e.g. `/aidlc poc <intent>`). Note how the stage/gate count drops.
4. **Depth.** On one of them, override with `--depth minimal` (or ask for a different depth at the confirmation line). Notice the artifact-detail promise change.
5. **Reflect.** Which scope + depth would you actually choose for this work, and what constraint in your intent most influenced the routing?

✅ **Done when:** you can state your chosen scope + depth and justify it from the confirmation line's numbers.

## Terminology

<details>
<summary><b>Show traditional-term mapping</b></summary>

| AI-DLC term | ≈ Traditional analogue |
| --- | --- |
| Scope | Workflow preset / project template / "which ceremony" |
| Depth | Level of documentation detail |
| Test strategy | Test coverage ambition |
| Intent | Epic / feature request / ticket title+summary |
| Compose | Tailoring the process to the task (a bespoke plan) |
| Reverse Engineering (2.1) | Codebase discovery / onboarding analysis |

</details>

## ✅ Checkpoint

<details>
<summary>1. What's the difference between scope, depth, and test strategy?</summary>

Scope = which stages run; depth = how much detail each stage produces; test strategy = how many tests are generated. Scope sets defaults for the other two.
</details>

<details>
<summary>2. You type an intent with no scope flag. How is a scope chosen, and what must you do before it runs?</summary>

The engine auto-detects a scope from keywords and shows a confirmation line naming the exact stage/gate counts. Read it and confirm (or name a different scope / say "compose") before the workflow starts.
</details>

<details>
<summary>3. When does the composer get involved instead of a stock scope?</summary>

When no stock scope clearly fits — rich prose with no keyword hit, or a keyword buried in a longer description (keyword + >~5 words). It proposes a minimum-viable custom grid at a gate you approve.
</details>

<details>
<summary>4. How do you get a more detailed artifact out of one stage without changing scope?</summary>

Override depth — via the `--depth` flag, at scope confirmation, or as feedback at that stage's approval gate.
</details>

<details>
<summary>5. How does AI-DLC know a task is brownfield?</summary>

Initialization detects existing code in the workspace; scope/compose then decide whether Reverse Engineering (2.1) runs. You don't set a flag.
</details>

## Key takeaways

- **Scope** is the highest-leverage choice — pick the lightest one that still yields every needed artifact; the **confirmation line** tells you the exact ceremony.
- **Depth** and **test strategy** are separate dials, overridable at any gate.
- A good **intent** names the outcome + key constraints, not the plan.
- **Compose** exists for when no preset fits; **greenfield/brownfield** routing is inferred, not flagged.

**Next:** [C5 — Interaction discipline](C5-interaction-discipline.md) *(to be authored)* — working the gates, the interaction modes, the walking skeleton + ladder prompt, and the cardinal rule: never vibe code.
