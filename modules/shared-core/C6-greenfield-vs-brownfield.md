# C6 — Greenfield vs. Brownfield: Choosing Your Path

> **Module:** C6 · **Track:** Shared Core (all roles) · **Time:** ~30 min · **Format:** 📖 Read
> **Prerequisites:** [C5 — Interaction discipline](C5-interaction-discipline.md)

## Learning objectives

By the end of this lesson you can:

- Explain how AI-DLC decides a project is **greenfield** or **brownfield**.
- Describe what **Reverse Engineering** (stage 2.1) does and when it runs.
- State what changes — and what stays the same — between the two paths.
- Pick the **lab track** you'll follow for the rest of the bootcamp.

## Why this matters

Almost no real team only builds new apps. Most AI-DLC work is *changing something that already exists*, where the risk isn't writing code — it's breaking what's already there. AI-DLC handles both, and the good news is that the *skills* you've learned (scopes, gates, never vibe code) are identical. Only one stage and one mindset differ. This lesson makes that difference explicit so you choose the right track and know what "safe change" looks like.

## Read

### How AI-DLC knows which you're in

You don't set a flag. During Initialization, **Workspace Detection** (stage 0.2) runs a deterministic scan: it walks one level into the project plus known source directories (`src/`, `app/`, `lib/`, `pages/`, `components/`, `tests/`), and if nothing fires at the top it descends into container folders (like `backend/`). It classifies **greenfield vs. brownfield** from source files, framework configs, and package manifests. An empty repo is greenfield; a repo with real code is brownfield — even if the code lives in an oddly named subfolder.

### The one stage that's different: Reverse Engineering (2.1)

Brownfield adds exactly one notable stage up front. **Reverse Engineering** runs *only* for existing codebases and executes as a two-link **pipeline**: the `aidlc-developer-agent` scans the code, then the `aidlc-architect-agent` synthesizes and writes the artifacts — about **9 reverse-engineering artifacts** capturing what each part of the system is and how it fits together. Those land in the intent's **`codekb/`** (code-knowledge) store, giving every downstream stage an accurate, concise picture of the existing system instead of the AI guessing.

Greenfield simply skips 2.1 — there's nothing to reverse-engineer.

```
  GREENFIELD                         BROWNFIELD
  ──────────                         ──────────
  0 Initialization (detects "new")   0 Initialization (detects "existing")
  2.2 Practices Discovery            2.1 Reverse Engineering  ◀── extra: scan → synthesize
  2.3 Requirements                   2.2 Practices Discovery
  2.4 User Stories …                 2.3 Requirements
  2.7 Units → 2.8 Delivery Plan      2.4 User Stories …
  3.x Construction Bolts             2.7 Units → 2.8 Delivery Plan
  (same from here on)                3.x Construction Bolts
```

### What stays the same (almost everything)

From Requirements Analysis onward, the two paths converge: the same Inception stages, the same Units-of-work decomposition, the same Construction Bolts, the same gates, the same "never vibe code." Everything you practiced in C1–C5 applies unchanged. Brownfield just starts from a *map of what exists*.

### The brownfield mindset: "what must not change"

The one habit brownfield adds is protecting the existing system. When you frame a brownfield intent, state the boundaries explicitly:

- **What must not change** — public APIs, data schemas, contracts other systems depend on.
- **What you're deliberately touching** — the surface area of this change.
- **Known constraints** — existing patterns to follow, tech you can't introduce.

These aren't bureaucracy; they steer routing and give the gates something concrete to check the AI's proposals against. Reverse Engineering gives the AI the *map*; your constraints tell it where the *guardrails* are.

### Which scope, roughly

Scope still does the heavy lifting (C4). Common pairings:

| Situation | Typical scope |
| --- | --- |
| New product from scratch | `mvp` or `feature` |
| New feature in an existing app | `feature` |
| Fixing a defect in existing code | `bugfix` |
| Restructuring without behavior change | `refactor` |
| Security/CVE work | `security-patch` |

Greenfield leans on `mvp`/`feature`; brownfield spans `feature`/`bugfix`/`refactor`/`security-patch`. Either way, read the confirmation line before you consent.

## 🧪 Try it (5 min)

1. Classify three recent pieces of work from your team as greenfield or brownfield.
2. For the brownfield ones, write the single most important **"must not change"** for each.
3. Decide which **lab track** you'll take for the rest of the bootcamp — greenfield (new-app seeded repo) or brownfield (existing-app seeded repo). Pick the one closest to your real day-to-day.

## Terminology

<details>
<summary><b>Show traditional-term mapping</b></summary>

| AI-DLC term | ≈ Traditional analogue |
| --- | --- |
| Greenfield | New build / from-scratch project |
| Brownfield | Existing system / legacy change / enhancement |
| Reverse Engineering (2.1) | Codebase discovery / system archaeology / onboarding analysis |
| Workspace Detection (0.2) | Project type sniffing |
| `codekb/` | Living architecture map / code knowledge base |

</details>

## ✅ Checkpoint

<details>
<summary>1. How does AI-DLC decide greenfield vs. brownfield?</summary>

Workspace Detection (stage 0.2) deterministically scans the project and known source dirs for source files, framework configs, and package manifests. Real code → brownfield; empty → greenfield. No manual flag.
</details>

<details>
<summary>2. What does Reverse Engineering do, and when does it run?</summary>

Only for brownfield. A two-link pipeline (developer scan → architect synthesis) produces ~9 artifacts describing the existing system, stored in the intent's codekb/ so downstream stages have an accurate map.
</details>

<details>
<summary>3. Once past Reverse Engineering, how different are the two paths?</summary>

Nearly identical — Requirements, Units, Construction Bolts, gates, and discipline are all the same. Brownfield just starts from a map of what exists.
</details>

<details>
<summary>4. What's the key extra input a brownfield intent should carry?</summary>

"What must not change" — the APIs, schemas, and contracts the new work must not break — plus the change surface and known constraints.
</details>

## Key takeaways

- Greenfield vs. brownfield is **auto-detected** at Initialization; you don't set a flag.
- Brownfield adds **one stage** — Reverse Engineering (2.1) — which maps the existing system into `codekb/`.
- From Requirements onward the paths **converge**; all your C1–C5 skills transfer.
- The brownfield mindset is **"what must not change"** — state your guardrails.

**You've finished the Shared Core.** Next, branch into your role add-on:
[Product Manager](../pm/P1-framing-the-intent.md) · [UX Designer](../ux/U1-stories-as-contracts.md) · [Developer](../developer/D1-setup-claude-code-gitlab.md) *(role modules to be authored)* — then regroup for the [Capstone](../capstone/X1-workshop-run.md).
