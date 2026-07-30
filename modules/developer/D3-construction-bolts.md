---
title: "D3 — Construction Bolts"
parent: Developer
nav_order: 3
---

# D3 — Construction Bolts, Stage by Stage

> **Module:** D3 · **Track:** Developer add-on · **Time:** ~75 min · **Format:** 🧪 Hands-on
> **Prerequisites:** [D2 — Knowledge & Rules](D2-knowledge-and-rules.md)

## Learning objectives

By the end of this lesson you can:

- Walk a Unit through the per-Bolt stages **3.1–3.5** and name what each produces.
- Explain the **walking skeleton** and answer the **ladder prompt** deliberately.
- Claim a Bolt in workshop mode by pushing a `bolt-<name>` branch.
- Validate designs, ADRs, and generated code at each Bolt gate.

## Why this matters

Construction is where your review discipline meets real code. The Bolt shape exists to keep slices reviewable — miss the point of a stage and you either rubber-stamp designs you didn't read or drown in a giant code drop. This lesson makes each stage's purpose concrete so your gate reviews are sharp.

## Read

### The Bolt: stages 3.1–3.5

A **Bolt** is one pass through the per-Unit Construction stages for a Unit (or a small dependency-linked group). Each stage is conditional by the execution plan, except Code Generation which always runs:

| Stage | Produces | What you check at the gate |
| --- | --- | --- |
| **3.1 Functional Design** | `business-logic-model.md`, `business-rules.md` | Does the logic match the requirement? Edge cases captured? |
| **3.2 NFR Requirements** | Security, performance, reliability NFRs | Are the right non-functionals named for this Unit? |
| **3.3 NFR Design** | NFR design specs | Do the chosen patterns actually satisfy those NFRs? |
| **3.4 Infrastructure Design** | Infra specs, IaC designs | Right services, least privilege, cost sane? |
| **3.5 Code Generation** | Application code + docs | Follows your Knowledge/Rules? Tests meaningful? |

Design stages (3.1–3.4) are led by the architect / AWS-platform agents with security and quality support; **Code Generation (3.5)** is led by the developer agent and dispatches as a focused subagent. Your job across all of them: **read the artifact, then decide** (C5).

### The walking skeleton comes first

Construction begins by reading `bolt-plan.md` and the dependency DAG, then executing **Bolt 1 — the walking skeleton**: the thinnest end-to-end slice that proves the architecture across every integration point. It's **always gated and interactive** — no autonomy yet — so you confirm the shape before anything else is built. Treat this gate as the most important one in the whole run: everything after inherits the skeleton's decisions.

### The ladder prompt: your autonomy choice

Immediately after you approve the walking skeleton, the **ladder prompt fires exactly once**:

```
Continue autonomously, or gate every Bolt?
```

- **`autonomous`** — remaining Bolts run without per-Bolt gates. Fast, but you're trusting the skeleton + your Rules/Sensors to hold. Good when Units are similar and well-covered by Sensors.
- **`gated`** — every Bolt stops for approval. Slower, safer; right for high-risk work or when Units differ a lot.

Your answer is recorded in state and governs all remaining Bolts. Choose for *this* project, not by habit. (Stages **3.6 Build & Test** and **3.7 CI** run once at the end regardless — that's D4.)

### Claiming a Bolt in workshop mode

In a workshop, after Inception is shared, Bolts become claimable. The claim is **plain git**:

```bash
git fetch --all                       # always, right before claiming — stale refs hide claims
git switch -c bolt-<name> <base>      # base = your affirmed way-of-working branch (D1/D2)
git push -u origin bolt-<name>        # FIRST PUSH WINS — the remote branch namespace is the registry
```

A non-fast-forward rejection means someone claimed it first — pick another Bolt. Then run that Bolt's Construction stages locally in your worktree, and push back when the gate approves. There's no special "claim" command — the shared remote *is* the registry, and `git push` is the atomic claim.

> 📌 **Platform note:** identical on GitLab — only the review artifact name changes (PR ↔ MR). See the mapping in [D1](D1-setup-claude-code-gitlab.md).

## 🧪 Try it (30 min)

On the workshop repo, from an approved `bolt-plan.md`:

1. **Claim** — `git fetch --all`, branch `bolt-<name>` off the affirmed base, and push to claim. Confirm it's yours on the remote.
2. **Walking skeleton** — if yours is Bolt 1, run stages 3.1→3.5, reading each artifact at its gate. Note where `business-rules.md` lands.
3. **Ladder** — at the ladder prompt, choose `autonomous` or `gated` and write one sentence justifying it for this work.
4. **Code review** — at 3.5, verify the generated code follows the example pattern and Rules you set in D2. Request changes if not.
5. **Push back** — once the Bolt's gate approves, push your branch.

✅ **Done when:** you've claimed a Bolt, taken it through 3.1–3.5 reading each gate, and made a reasoned ladder choice.

## Terminology

<details>
<summary><b>Show traditional-term mapping</b></summary>

| AI-DLC term | ≈ Traditional analogue |
| --- | --- |
| Bolt | One slice's worth of build (hours/days) |
| Functional Design (3.1) | Domain/business-logic design |
| NFR Requirements/Design (3.2/3.3) | Non-functional requirements + architecture |
| Infrastructure Design (3.4) | Infra / IaC design |
| Code Generation (3.5) | Implementation |
| Walking skeleton | Tracer bullet / thin end-to-end MVP |
| Ladder prompt | "How much do we review?" decision |

</details>

## ✅ Checkpoint

<details>
<summary>1. What are the per-Bolt stages 3.1–3.5, and which always runs?</summary>

Functional Design, NFR Requirements, NFR Design, Infrastructure Design, Code Generation. Code Generation (3.5) always runs; the design stages are conditional by the execution plan.
</details>

<details>
<summary>2. Why is the walking-skeleton gate the most important one?</summary>

It's always gated, proves the architecture end-to-end, and every subsequent Bolt inherits its decisions; its approval triggers the ladder prompt.
</details>

<details>
<summary>3. What does the ladder prompt decide, and how often does it fire?</summary>

Whether remaining Bolts run autonomously or gated. It fires exactly once, right after the walking skeleton, and is recorded in state.
</details>

<details>
<summary>4. How do you claim a Bolt, and what does a push rejection mean?</summary>

`git fetch --all`, branch `bolt-<name>` off the affirmed base, and `git push` — first push wins. A non-fast-forward rejection means it's already claimed; pick another.
</details>

## Key takeaways

- A **Bolt** runs **3.1–3.5**; read each design/code artifact before its gate.
- The **walking skeleton** is first, always gated, and sets the shape — treat it as the key gate.
- The **ladder prompt** (once) sets autonomous vs gated for the rest — choose for the project.
- **Claiming is plain git**: fetch, branch off the affirmed base, push — first push wins.

**Next:** [D4 — Build, Test & the control loop](D4-build-test-control-loop.md) — the once-at-end Build & Test and CI stages, Rules + Sensors, and knowing when to halt or escalate.
