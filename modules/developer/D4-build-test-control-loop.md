# D4 — Build, Test & the Control Loop

> **Module:** D4 · **Track:** Developer add-on · **Time:** ~60 min · **Format:** 📖 Read + 🧪 Hands-on + ✅ Graded
> **Prerequisites:** [D3 — Construction Bolts](D3-construction-bolts.md)

## Learning objectives

By the end of this lesson you can:

- Explain **Build & Test (3.6)** and **CI Pipeline (3.7)** — the once-at-end stages.
- Distinguish **inferential** (LLM) from **computational** (executable) verification and where each belongs.
- Wire a **Sensor** to back a Rule and read its advisory results.
- Recognize the **self-correcting loop** and when the engine **halts and escalates**.

## Why this matters

This is where quality gets verified rather than asserted. Understanding which checks the AI can trust to a program versus which need your judgment is what lets you safely turn up autonomy. Get this right and you know exactly how much to review — and why.

## Read

### The once-at-end stages

After every Bolt is built, two stages run a single time across the whole workflow:

- **3.6 Build and Test** (led by the quality agent, with devsecops support) — builds all Units and runs the test suite at your chosen **test strategy** level, producing test results and a quality report. This is where cross-Unit integration actually gets exercised.
- **3.7 CI Pipeline** (pipeline-deploy agent, conditional) — emits CI configuration and quality gates.

Running Build & Test once at the end (rather than per Bolt) is deliberate: it keeps per-Bolt reviews small while still verifying the whole system together before Verification Gate 3.

> 📌 **Platform note:** the CI config target differs by host — a workflow under `.github/workflows/` on GitHub, `.gitlab-ci.yml` on GitLab. The stage's job (define build/test/quality gates) is the same. See [D1](D1-setup-claude-code-gitlab.md).

### Two kinds of verification

The spec draws a sharp line, and it's the key idea in this lesson:

- **Inferential verification (LLM instructions)** — for post-conditions that are *not* a binary pass/fail. Most code-review heuristics ("is this readable / idiomatic / well-factored?") are judgment calls the AI can assess with nuance but not prove. A stage whose checks are *only* LLM-judged **does not self-halt** — it still presents to you for validation, because a model grading its own output can satisfy the letter of a check without its intent.
- **Computational verification (executables)** — for post-conditions that must be enforced **deterministically**, zero tolerance for ambiguity: "no endpoint exposed without auth," "no code path deletes a prod stack," type-checks, linters. These belong in a **Sensor** or tool, not an LLM's opinion.

The practical upshot: **the more of your checks you make computational, the more the workflow can safely self-verify** — and the less you have to review by hand. That's the path to higher autonomy from D3's ladder.

### Sensors: deterministic checks in practice

A **Sensor** is a deterministic check that fires on writes to a stage's outputs and records an advisory `SENSOR_*` result (it never blocks your workflow). A stage declares which Sensors fire. So a Rule like "all colors from tokens" or "handlers validate input" graduates into a Sensor (a linter/static check) that flags violations automatically. Rules are *feedforward* (steer before), Sensors are *feedback* (verify after) — together they're the **control loop**.

### The self-correcting loop, and halting

Within a stage, the AI can run a **self-correcting loop**: generate → check against post-conditions → fix → repeat. But it never loops forever. Every loop has a **halting condition** — a max iteration count or token budget. If the AI can't converge within those bounds, it doesn't spin; it **escalates to you** for guidance. That's the safety net that makes autonomy practical: the AI works independently inside well-defined boundaries and pulls in a human exactly when it's stuck or when a check is a genuine judgment call.

So when a stage escalates mid-loop, that's the system working as designed — it's telling you "this needs human judgment," which is precisely where your value is.

### Reading the outputs

At the Build & Test gate, read the **quality report** and test results the same way you read any artifact (C5): confirm failures were understood and fixes were real, not papered over. If a Sensor flagged something advisory, decide whether it's a must-fix. Then approve, request changes, or — after repeated cycles — accept-as-is with the residual logged.

## 🧪 Try it — graded (25 min)

Finish a small workshop build through 3.6:

1. **Wire a Sensor** — take one Rule from D2 and describe (or scaffold) the deterministic Sensor that would enforce it; note where results are recorded.
2. **Classify checks** — list three quality checks for your feature and label each **inferential** or **computational**. Justify one that surprised you.
3. **Run Build & Test (3.6)** — read the quality report. Find one test result you'd dig into and say why.
4. **Force/observe an escalation** — identify a point where the AI escalated (or would) and explain what human judgment it needed.
5. **Decide the gate** — approve, request changes, or accept-as-is with a logged residual — and justify it.

✅ **Graded pass = you:** correctly classified inferential vs computational checks, read the quality report critically, and justified your gate decision.

## Terminology

<details>
<summary><b>Show traditional-term mapping</b></summary>

| AI-DLC term | ≈ Traditional analogue |
| --- | --- |
| Build and Test (3.6) | Integration build + test run |
| CI Pipeline (3.7) | CI config (GitHub Actions / GitLab CI) |
| Inferential verification | Human-judgment code review |
| Computational verification | Automated gate (lint/type/policy) |
| Sensor | CI check that records a result |
| Self-correcting loop | Generate-fix-retry with a budget |
| Halting condition | Retry/timeout limit before escalation |

</details>

## ✅ Checkpoint

<details>
<summary>1. When do Build & Test (3.6) and CI (3.7) run?</summary>

Once each, at the end of Construction across all Bolts (not per Bolt), before Verification Gate 3. CI is conditional on scope.
</details>

<details>
<summary>2. What's the difference between inferential and computational verification?</summary>

Inferential = LLM-judged, non-binary quality heuristics (needs human validation; can't self-halt alone). Computational = deterministic executable checks (linters, type-checks, "no unauth endpoint"). Zero-tolerance checks should be computational.
</details>

<details>
<summary>3. Why does making more checks computational enable more autonomy?</summary>

Deterministic checks let a stage self-verify and self-halt without human validation, so more can run autonomously and you review less.
</details>

<details>
<summary>4. What happens when the self-correcting loop can't converge?</summary>

It hits its halting condition (max iterations / token budget) and escalates to a human rather than looping forever.
</details>

<details>
<summary>5. Rules vs. Sensors in the control loop?</summary>

Rules are feedforward (steer before work); Sensors are feedback (deterministic checks after). A hand-checked Rule is a candidate to back with a Sensor.
</details>

## Key takeaways

- **Build & Test (3.6)** and **CI (3.7)** run **once at the end** — full-system verification with small per-Bolt reviews.
- Split checks into **inferential** (your judgment) vs **computational** (Sensors/tools); push zero-tolerance checks to computational.
- **Sensors** back Rules deterministically; together they're the **control loop**.
- The **self-correcting loop halts and escalates** — escalation is the system asking for your judgment, by design.

**Developer track complete.** Regroup for the [Capstone](../capstone/X1-workshop-run.md) *(to be authored)*, or go deeper with the electives: [A1 — Inside v2](../electives/A1-inside-v2.md) · [A2 — Rules, Sensors & progressive autonomy](../electives/A2-progressive-autonomy.md).
