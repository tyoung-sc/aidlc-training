---
title: Program Plan
nav_order: 2
---

# AI-DLC Adoption Bootcamp — Program Plan & Curriculum Outline

**Version:** Draft 0.2 · **Owner:** Trevor Young · **Date:** 2026-07-27
**Status:** For review — this is the starting plan, not the finished courseware.
**Grounded against:** the installed **v2 source** in this repo (`docs/guide/`, `docs/reference/`, `glossary.md`, `workshop-mode.md`) — a later, more elaborate build than the AWS 2.0 spec PDF. Where they differ, the installed docs win.

---

## 1. Purpose & Framing

This document is the **project plan and curriculum outline** for a role-inclusive bootcamp that gets a product development team productive on the **AWS AI-DLC (AI-Driven Development Life Cycle) v2** process. It is deliberately a *plan*, not the content itself — it defines what to build, for whom, in what formats, how to publish it, and how learners will interact with it.

### What AI-DLC v2 actually is (the installed build)

AI-DLC is a methodology that structures AI-assisted software development into repeatable, traceable phases, implemented from one harness-neutral core and invoked with a single command. The essentials a team must internalize:

- **A single command.** You run `/aidlc <what you want>` (`$aidlc` on the Codex harness). A deterministic **engine** decides the next move; a **conductor** (the `/aidlc` session) carries it out, then loops. `bun` is the only runtime prerequisite.
- **Five phases, 32 stages.** Initialization (0) → Ideation (1) → Inception (2) → Construction (3) → Operation (4). Each stage has defined inputs/outputs, a lead agent, and an approval gate. *(This is the biggest change from the 2.0 spec PDF, which described only three phases.)*
- **Scopes decide what runs.** One of **9 scopes** (enterprise, feature, mvp, poc, bugfix, refactor, infra, security-patch, **workshop**) — or auto-detected from your request — selects which stages execute and at what **depth** (Minimal / Standard / Comprehensive). Greenfield vs. brownfield is largely a matter of scope + whether Reverse Engineering (2.1) runs.
- **"Small mob, broad agents."** 14 personas (11 broad domain experts — architect, developer, product manager, etc. — plus 2 reviewers and a composer) each span multiple stages, carrying context to eliminate handoffs.
- **Human control at gates.** After each stage you review and Approve / Request changes (or, after 3 revisions, accept as-is). Construction runs in **Bolts**; the first is a **walking skeleton**, after which a **ladder prompt** lets you choose autonomous or gated for the rest.
- **It learns.** **Rules** (feedforward standards) + **Sensors** (deterministic checks) form a control loop, and a **Learning Loop** promotes your in-stage corrections into durable practices — the concrete realization of the spec's Generate-Verify-Learn / three-compartment model.

> **Design principle for the whole bootcamp:** teach the *habits and judgment*, not just the button-presses. AI-DLC's value comes from disciplined human review at gates, good inputs, scope/depth choices, and clean context management — all transferable across roles.

### Assumptions baked into this plan

| Area | Assumption |
| --- | --- |
| Core AI model | **Claude** (via Claude Code) |
| Prerequisite / invocation | **`bun`** installed; workflows run via **`/aidlc`** |
| Primary harness | **Claude Code** — terminal and its **VS Code** integration (best-supported harness) |
| Other IDEs | **Cursor is not an official v2 harness.** Devs who prefer it use Claude Code alongside it; a custom Cursor harness is an *advanced, optional* path (see risks) |
| Source control | **GitHub** (repos, PRs, CI, Pages, wiki) — also the backbone of workshop-mode's shared-remote claiming |
| Learners | Developers, Product Managers, UX Designers — plus "ambidextrous" people who want it all |
| Training environment | The built-in **`workshop` scope** + a shared GitHub repo (a safe, provider-neutral lab that ships with v2 — no bespoke simulator needed) |
| Two scenarios | **Greenfield** (new app) and **Brownfield** (existing app; Reverse Engineering runs) — taught as parallel tracks |
| Time budget | **~5 days at half-days**, or **~2.5 dedicated days** (a weekend), per individual |

---

## 2. Vocabulary Bridge (teach this on Day 1 to everyone)

AI-DLC renames some familiar concepts to signal a faster tempo — but **the tool prints these terms on screen, in the state file, and in the audit log**, so learners must recognize them at the keyboard. Approach agreed for the courseware: **lead with the AI-DLC term, pair it with a traditional analogue on first use, and give rendered lessons a toggle/tooltip** (a "Show traditional terms" switch) plus this dual-column cheat-sheet. Note that v2 already dropped the most arbitrary v1 flavor terms (the old "Mob Elaboration/Construction" rituals and "Deployment Unit" are gone).

| AI-DLC term | ≈ Traditional analogue | Definition |
| --- | --- | --- |
| **Intent** | Epic / initiative / feature request | High-level statement of what to build; tracked as a row in the space registry; the root of an intent record. |
| **Unit (of work)** | Sub-domain / component slice | An independently implementable piece, decomposed at stage 2.7; bundled into Bolts. |
| **Bolt** | Sprint (but hours/days) | One Construction pass (stages 3.1–3.5) over a Unit or small dependency-linked group. First Bolt = walking skeleton. |
| **Phase / Stage** | SDLC phase / step | 5 phases, 32 numbered stages (e.g. 2.4, 3.5). |
| **Scope** | Workflow preset / project template | One of 9 (enterprise…workshop) choosing which stages run and at what depth. |
| **Space** | Team workspace / project area | Per-team workspace holding memory, knowledge, and intent records. |
| **Agent (persona)** | Specialist role | One of 14 personas the conductor activates for a stage/review. |
| **Approval gate** | Review / sign-off | Checkpoint after each stage: approve, request changes, or accept-as-is. |
| **Walking skeleton** | Thin end-to-end MVP slice | The first, always-gated Bolt that exercises every integration point. |
| **Autonomy mode** | How much you review | `autonomous` vs `gated`, chosen at the ladder prompt after the walking skeleton. |
| **User story** | User story (unchanged) | Kept as-is; the shipped "mob" stage (2.4) generates them collaboratively. |
| **Rules / Sensors** | Standards + automated checks | Feedforward behavioural rules paired with deterministic verification. |
| **Learning Loop** | Retrospective (automated) | Promotes your in-stage corrections into durable practices/sensors. |

Three ideas that reframe how everyone works:

- **Reverse the conversation direction.** The AI *initiates and directs* — it decomposes intent, proposes options, and asks clarifying questions. Humans are **approvers**: validate, select, decide at gates. (Analogy: Google Maps — you set the destination, it proposes the route, you steer.)
- **Human oversight is a "loss function."** Gates exist to catch and prune errors early, before they snowball. Approving without reading defeats the method.
- **v2 is Generate → Verify → Learn.** Rules + Sensors + the Learning Loop let stages self-check and improve, moving toward safe, *incremental* autonomy — useful context even for non-engineers.

---

## 3. Learning Outcomes by Role

Everyone shares a common foundation; each role then goes deeper where they add the most value. Outcomes are written so an "ambidextrous" learner can pursue all of them.

**Shared core (all roles) — by the end, a learner can:**
- Explain the 5-phase / 32-stage lifecycle and why AI-DLC "reimagines rather than retrofits."
- Use the vocabulary bridge fluently (Intent, Unit, Bolt, Phase/Stage, Scope, Space, Agent, gate).
- Install `bun` + the Claude Code harness, run `/aidlc --doctor`, and launch a first workflow.
- Pick a **scope** and **depth** appropriate to the task; recognize greenfield vs. brownfield routing.
- Work the interaction modes (Guide Me / Edit File / Chat) and **read before approving** at gates.
- Manage context across sessions/compaction and **never vibe code**.

**Product Manager — additionally can:**
- Author a strong **Intent** and the Inception inputs (problem, users, success metrics, MVP IN/OUT, risks/open questions).
- Facilitate a **workshop-mode** Inception and drive Intent → Units decomposition (stage 2.7) with the team.
- Own requirements, user-story review, and measurement criteria that trace to business intent.
- Judge scope: what belongs in a Unit/Bolt, what's out, when to split.

**UX Designer — additionally can:**
- Contribute user stories, personas, and acceptance criteria that act as contracts for the AI.
- Bring UX/mockup decisions into Inception and gate-review generated UI against design-system + accessibility standards.
- Encode design standards as **team Knowledge / Rules** so generated UI aligns (feeding the Learning Loop).

**Developer — additionally can:**
- Complete setup on **Claude Code** (terminal + VS Code integration) with GitHub; understand the other shipped harnesses exist.
- Author **team Knowledge and Rules** (languages, frameworks, allow/deny lists, security, testing) so generation follows house style.
- Drive per-Unit **Construction Bolts** (stages 3.1–3.5) through Build & Test (3.6) and CI (3.7); handle the walking skeleton + ladder prompt.
- Validate designs, ADRs, and generated tests; use Sensors/Rules; know when to halt/escalate.
- Run **workshop-mode** claiming: `git push` a `bolt-<name>` branch to the shared remote to claim a Bolt; keep intent records versioned.

---

## 4. Program Architecture

A **strong shared core** (~55% of time) every role takes together, plus **thin role add-ons** (~30%), plus a **shared capstone** (~15%). Greenfield and brownfield run as **parallel scenario tracks** through the hands-on portions. The whole hands-on spine uses the built-in **`workshop` scope** against a shared GitHub repo.

```
                        ┌───────────────────────────────────────────┐
                        │              SHARED CORE (all roles)        │
                        │  C1 Why AI-DLC → C2 Lifecycle & Vocab       │
                        │  C3 Setup & first /aidlc → C4 Scopes/Inputs │
                        │  C5 Interaction discipline (gates/context)  │
                        └───────────────┬─────────────┬──────────────┘
                                        │             │
                    ┌───────────────────┘             └───────────────────┐
              GREENFIELD track                                     BROWNFIELD track
        (new app: Intent → Units)                     (Reverse Engineering 2.1 → change safely)
                    │                                                     │
        ┌───────────┴───────────┐                             ┌───────────┴───────────┐
        │  ROLE ADD-ONS         │                             │  ROLE ADD-ONS         │
        │  PM · UX · Developer  │                             │  PM · UX · Developer  │
        └───────────┬───────────┘                             └───────────┬───────────┘
                    └─────────────────────┬───────────────────────────────┘
                                          │
                                ┌─────────┴─────────┐
                                │  CAPSTONE (workshop scope)  │
                                │  Facilitator Inception →    │
                                │  parallel Construction Bolts│
                                └─────────────────────────────┘
```

**Modality mix** (AI-DLC is best learned by *doing* — the docs ship a dedicated workshop mode for exactly this):
- ~35% **reading** (blog/article-format lessons, guides, cheat-sheets)
- ~20% **watch/listen** (short videos, a podcast-style episode, recorded runs)
- ~45% **hands-on** (`/aidlc` labs on the workshop scope, gate practice, a graded capstone)

---

## 5. Curriculum Outline (modules)

Format legend: 📖 read · 🎧 watch/listen · 🧪 hands-on lab · ✅ checkpoint/quiz. Durations are learner-time.

### Shared Core (all roles) — ~5.5 h

| # | Module | Format | Time | Key content |
| --- | --- | --- | --- | --- |
| C1 | **Why AI-DLC: reimagine, don't retrofit** | 📖 + 🎧 | 45 m | AI-assisted vs AI-driven; reverse the conversation; velocity/quality/DX; Google Maps analogy. |
| C2 | **The lifecycle & the vocabulary bridge** | 📖 + ✅ | 45 m | 5 phases / 32 stages; personas; Intent/Unit/Bolt/Scope/Space; AWS-term-primary + traditional toggle. Quiz. |
| C3 | **Setup & your first `/aidlc`** | 🧪 | 60 m | Install `bun` + Claude Code harness; `/aidlc --doctor`; run a tiny workflow end-to-end. (Note: Cursor not an official harness.) |
| C4 | **Scopes, depth & inputs that work** | 📖 + 🧪 | 75 m | Choosing scope + depth; what makes a good Intent; Initialization/Ideation/Inception inputs; kick off Inception on the sandbox repo. |
| C5 | **Interaction discipline** | 📖 + 🧪 + ✅ | 75 m | Guide Me / Edit File / Chat modes; approval gates; walking skeleton + ladder prompt; context/compaction; **never vibe code**. Graded lab: review-and-decide at a gate. |
| C6 | **Greenfield vs. brownfield** | 📖 | 30 m | When Reverse Engineering (2.1) runs; "what must not change"; how scope changes the stage set. Learner picks a track. |

### Role Add-on — Product Manager — ~3.0 h

| # | Module | Format | Time | Key content |
| --- | --- | --- | --- | --- |
| P1 | **Framing the Intent & Inception inputs** | 📖 + 🧪 | 75 m | Problem/users/success metrics; MVP IN/OUT; risks & open questions; lab: draft an Intent + run Requirements. |
| P2 | **Facilitating workshop-mode Inception** | 🎧 + 🧪 | 60 m | Running Inception solo/with the group; stage 2.2 practices affirmation; Intent → Units (2.7); reviewing `bolt-plan.md` (2.8). |
| P3 | **Scope judgment & the Bolt plan** | 📖 + ✅ | 45 m | Sizing Units; sequencing/parallelizing Bolts; validating AI's decomposition; resisting scope creep. |

### Role Add-on — UX Designer — ~3.0 h

| # | Module | Format | Time | Key content |
| --- | --- | --- | --- | --- |
| U1 | **Stories, personas & acceptance criteria as contracts** | 📖 + 🧪 | 60 m | Writing stories the AI can build against; acceptance criteria that constrain generation; the User Stories (2.4) mob. |
| U2 | **Bringing design into the workflow** | 🎧 + 🧪 | 75 m | Where UX/mockups fit; encoding design-system + accessibility standards as **team Knowledge/Rules**. |
| U3 | **Reviewing generated UI at the gates** | 🧪 + ✅ | 45 m | Critiquing AI output against standards; feeding corrections back through the Learning Loop. |

### Role Add-on — Developer — ~4.5 h

| # | Module | Format | Time | Key content |
| --- | --- | --- | --- | --- |
| D1 | **Setup: Claude Code + GitHub (and the harness landscape)** | 🧪 | 75 m | `bun` + Claude Code (terminal + VS Code); `/aidlc` health check; GitHub remote; where Kiro/Codex/opencode fit; Cursor = alongside, not a harness. |
| D2 | **Team Knowledge & Rules** | 📖 + 🧪 | 60 m | Encoding languages/frameworks/allow-deny/security/testing as Rules + Knowledge; example code as the highest-leverage input; Sensors overview. |
| D3 | **Construction Bolts, stage by stage** | 🧪 | 75 m | Stages 3.1–3.5 per Unit; walking skeleton; ladder prompt (autonomous vs gated); claiming a Bolt via `git push`. |
| D4 | **Build, Test & the control loop** | 📖 + 🧪 + ✅ | 60 m | Build & Test (3.6), CI (3.7); Rules+Sensors; inferential vs computational verification; halting/escalation. |

### Capstone (all roles, mixed teams) — ~2.5 h

| # | Module | Format | Time | Key content |
| --- | --- | --- | --- | --- |
| X1 | **A real workshop-mode run** | 🧪 | 2.5 h | Facilitator drives Inception on a shared GitHub remote; a mixed mob then **claims parallel Construction Bolts** (`git push`), runs stages locally, and approves at gates — greenfield or brownfield. Peer-reviewed rubric. |

### Optional "Advanced / Why it works" electives (self-paced) — ~1.5 h

| # | Module | Format | Time | Key content |
| --- | --- | --- | --- | --- |
| A1 | **Inside v2: engine, conductor, agents** | 📖 + 🎧 | 45 m | Deterministic engine vs conductor; stage protocol; inline/subagent/pipeline/mob topologies; the 14 personas. |
| A2 | **Rules, Sensors & progressive autonomy** | 📖 | 45 m | The control loop and Learning Loop; hydrating checks in safe increments; adding a scope/agent/rule (config, no code). |

---

## 6. Two Pacing Options (same content, different cadence)

Total core path for a single role ≈ **11–12.5 hours** (Shared Core 5.5 + one role add-on 3.0–4.5 + Capstone 2.5). An ambidextrous learner taking **all** role add-ons ≈ 18.5 h + electives.

### Option A — Five half-days (~2.5–3 h/day)

| Day | Focus | Modules |
| --- | --- | --- |
| 1 | Foundations | C1, C2, C3 |
| 2 | Scopes, inputs & discipline | C4, C5, C6 |
| 3 | Your role, part 1 | First half of role add-on |
| 4 | Your role, part 2 | Second half of role add-on (+ elective if time) |
| 5 | Capstone | X1 + debrief/retro |

### Option B — 2.5 dedicated days (a weekend)

| Block | Focus | Modules |
| --- | --- | --- |
| Day 1 AM | Foundations | C1, C2, C3 |
| Day 1 PM | Scopes, inputs & discipline | C4, C5, C6 |
| Day 2 AM | Role add-on, part 1 | Role modules |
| Day 2 PM | Role add-on, part 2 | Role modules (+ elective) |
| Day 3 AM | Capstone | X1 + debrief |

> **Ambidextrous learners:** add the other roles' add-ons as self-paced modules after the capstone, or extend Option A to 7 half-days. The core + capstone are shared, so only the add-ons stack.

---

## 7. Content Format Options & Recommendations

The request calls for a mix of reading, interactivity, and passive watch/listen. Below are the practical options per modality with a recommendation.

### Reading (blog/article format)
- **Options:** Markdown lessons rendered as a static site; a wiki; PDF handouts; inline READMEs.
- **Recommendation:** Author every lesson as **Markdown in this repo** (`training/modules/…`) rendered via a static-site generator. It versions with the AI-DLC core it teaches, supports PRs for updates, and lets learners read in-IDE. Keep each lesson skimmable: 600–1,200 words, one diagram, a "try it" box, a 3-question check. Build the **terminology toggle** into this layer (a dual-column glossary + a "show traditional terms" switch).

### Watch / listen (passive)
- **Options:** (a) short **screencasts** (5–8 min) of real `/aidlc` runs and setup; (b) a **podcast-style episode** (~20 min) on the methodology and vocabulary for non-devs; (c) **narrated slide decks** exported to video; (d) live-recorded **brown-bag** talks.
- **Recommendation:** Produce **3–5 short screencasts** (Claude Code setup, one Inception, one Construction Bolt) plus **one podcast-style methodology episode**. Screencasts carry the most value for tool mechanics; the podcast serves PMs/UX who learn the "why" better by listening. Script from real runs so audio/video stays reproducible.

### Hands-on (interactive)
- **Options:** the built-in **`workshop` scope** against a shared GitHub repo, guided labs with checkpoints, gate-decision exercises, and the capstone.
- **Recommendation:** Make `/aidlc --scope workshop` the spine of the program. Every core and role module ends in a **lab with an auto- or peer-checkable outcome**. Provide pre-seeded **greenfield and brownfield** sample repos so learners practice both entry paths without setup friction.

### Suggested per-module default
Reading to introduce → a short watch/listen to see it in motion → a `/aidlc` lab to do it → a checkpoint to confirm. This "read-see-do-check" loop is the default authoring template.

---

## 8. Interactivity Mechanisms

| Mechanism | What it does | Where used |
| --- | --- | --- |
| **Workshop-scope labs** | Safe, provider-neutral runs on a shared GitHub repo; ships with v2 | C3–C5, all role add-ons, capstone |
| **Gate-decision drills** | Present a generated artifact; learner must critique before Approve / Request changes | C5, U3, D4 |
| **Bolt-claiming exercise** | Learner claims a Bolt by pushing `bolt-<name>` to the shared remote (first push wins) | D3, capstone |
| **Greenfield/brownfield branches** | Same lab, two seeded repos; learner picks their path | C6 onward |
| **Knowledge checks** | 3–5 question quizzes gating module completion | C2, C5, P3, D4, U3 |
| **Capstone rubric** | Peer + facilitator scoring of an end-to-end workshop run | X1 |
| **Reflection prompts** | "What would you promote into a Rule/Sensor?" ties practice to the Learning Loop | electives, capstone debrief |
| **Cohort channel** | Async Q&A + share-your-artifact (Slack/Teams/GitHub issues) | throughout |

Two design rules: (1) every lab must run on the **workshop scope + a shared repo** so no learner is blocked on cloud accounts; (2) every gate drill must reward **reading before approving**, reinforcing oversight-as-loss-function.

---

## 9. Distribution & Publishing Options

You asked for options with a recommendation. All four can host the same Markdown lessons + video links + lab pointers.

| Option | Strengths | Trade-offs | Best when |
| --- | --- | --- | --- |
| **A. GitHub-native** (repo + Pages + Wiki + Issues) | Lives beside the AI-DLC core; versioned; PR-based review; free for public repos; devs already there; labs link straight to seeded repos and the workshop remote | Weaker at completion tracking, quizzes, and reporting for non-devs; UX/PMs less comfortable in Git; **private-repo Pages needs GitHub Team/Enterprise** | You want lowest friction and a single source of truth |
| **B. Dedicated LMS** (Docebo, Cornerstone, Litmos, TalentLMS) | Enrolments, completion tracking, quizzes, certificates, manager reporting | Content drifts from the repo; another system; cost | Formal completion/compliance reporting matters |
| **C. Knowledge base** (Notion, Confluence) | Fast to author; friendly to all roles; easy embeds | Not versioned with code; limited grading; another silo | You value speed and cross-role readability over Git-native |
| **D. Video host** (internal portal / YouTube-unlisted / Vimeo) | Best for the watch/listen tier | Video only — needs a "home" from A/B/C | Always used *alongside* one of the above |

**Recommendation — a hybrid, GitHub-anchored:** (GitHub is the default host because GitLab requires VPN access internally; GitLab remains a viable internal alternative and the mechanics are identical — see the platform mapping in `modules/developer/D1`. Note the private-repo Pages caveat below.)
- **Author and version all lessons + labs in GitHub** (Option A), rendered via **GitHub Pages**. This keeps courseware in lockstep with the core it teaches and lets the community improve it via PRs. It also co-locates the shared workshop remote learners push Bolts to.
- **Host media on an internal video host** (Option D) and embed links in the lessons.
- **If completion tracking/certificates are required**, add a **thin LMS layer** (Option B) that *links out* to the GitHub lessons and only owns enrolment, quizzes, and reporting — so content never forks.

This gives devs a Git-native home, non-devs a readable rendered site, and the org optional reporting — without duplicating content.

---

## 10. Project Plan — Building the Bootcamp

### Workstreams
1. **Curriculum & content** — write lessons, labs, quizzes, capstone rubric; build the terminology toggle.
2. **Media production** — screencasts + podcast episode.
3. **Lab environment** — stand up the shared **workshop-scope** GitHub repo(s); seed greenfield/brownfield samples; write the facilitator runbook.
4. **Platform & publishing** — GitHub Pages site; media host; optional LMS shell.
5. **Pilot & iterate** — run a small cohort, gather data, revise.

### Phased timeline (indicative)

| Phase | Duration | Outcome |
| --- | --- | --- |
| **0. Align & approve** | Week 1 | This plan signed off; scope, platform decision (LMS yes/no), owners named |
| **1. Design** | Weeks 2–3 | Module specs, lab scripts, rubric; sample repos scoped; media shot-list; glossary/toggle spec |
| **2. Build core** | Weeks 4–6 | Shared Core (C1–C6) lessons + workshop-scope labs; GitHub Pages up |
| **3. Build role tracks + media** | Weeks 6–9 | PM/UX/Dev add-ons; capstone runbook; screencasts + podcast recorded |
| **4. Pilot** | Weeks 10–11 | One mixed cohort runs Option B (2.5-day); telemetry + feedback collected |
| **5. Revise & launch** | Week 12 | Fixes applied; v1.0 published; facilitators enabled |

Roughly a **12-week** effort to a polished v1; a **usable MVP** (Shared Core + Developer track + workshop labs, docs-only, no video) is achievable in **~4 weeks** if you want to pilot sooner.

### RACI (who builds it)

| Activity | Responsible | Accountable | Consulted | Informed |
| --- | --- | --- | --- | --- |
| Curriculum design | Content lead / senior dev | Program owner (you) | PM & UX leads | Team |
| Lab & workshop-repo setup | Dev + platform eng | Program owner | Security | Content lead |
| Media production | Content lead + presenters | Program owner | — | Team |
| Publishing / GitHub Pages | Platform eng | Program owner | IT | Team |
| Pilot facilitation | Facilitator(s) | Program owner | Managers | Cohort |

### Effort estimate (order of magnitude)
- Curriculum & content (incl. toggle): ~15–20 person-days
- Workshop repos + labs + facilitator runbook: ~8–12 person-days
- Media (5 screencasts + 1 podcast): ~5–8 person-days
- Publishing setup: ~2–3 person-days
- Pilot + revision: ~5 person-days
- **Total ≈ 35–48 person-days** for v1.0 (compressible for the 4-week MVP).

### Key risks & mitigations

| Risk | Mitigation |
| --- | --- |
| Content drifts from the fast-moving AI-DLC core | Version courseware **in this repo**; add a CI nudge when `core/` or `docs/` changes |
| **Training content not committed → wiped on re-clone/branch-switch** (this happened once already) | **Commit `training/` to git** (or its own branch) so a checkout can't silently erase it |
| Devs want Cursor, which isn't a shipped harness | Teach Claude Code as primary; document "Cursor alongside"; treat a custom Cursor harness as a separate, optional engineering task if demand is high |
| "Vibe coding" habits undermine the method | Make gate-decisions a **graded** part of every lab, not optional reading |
| Role tracks feel siloed | Keep the capstone a **mixed-role workshop run** so the mob dynamic is practiced as intended |
| Over-scoping v1 | Ship the 4-week MVP (Core + Dev + workshop labs) first, then layer media/LMS |
| Plan anchored to a moving version (currently pre-1.0) | Re-verify against `docs/guide` + `glossary.md` before each cohort; pin the harness version used in labs |

---

## 11. Success Metrics

Measure the program the way AI-DLC measures work — against outcomes that trace to intent.

- **Completion:** ≥ 80% of enrolled learners finish their role path within the window.
- **Capability (primary):** ≥ 90% pass the capstone rubric — i.e., can take an Intent through Inception gates and complete a Construction Bolt on the workshop scope.
- **Discipline signals:** in labs, learners read-before-approving at gates and choose sensible scope/depth ≥ 90% of the time.
- **Time-to-first-real-Bolt:** median days from finishing the bootcamp to completing a real Bolt on a live project (target: within 1 week).
- **Confidence lift:** pre/post self-assessment across the role outcomes (target: +2 on a 5-point scale).
- **Content health:** lessons updated within N days of a material `core/`/`docs/` change; MR contributions from graduates.

---

## 12. Appendix — Source Mapping & References

**Grounded in the installed v2 (this repo):**
- `docs/guide/00-introduction.md`, `04-phases-and-stages.md` — the 5 phases / 32 stages, engine/conductor, "small mob, broad agents."
- `docs/guide/05-scopes-and-depth.md` — the 9 scopes, depth, and test strategy.
- `docs/guide/workshop-mode.md` — the facilitated-training recipe (workshop scope, parallel Bolts, git-push claiming). **The backbone of the labs/capstone.**
- `docs/guide/06-agents.md` + `agents/` — the 14 personas that map to learner roles.
- `docs/guide/07-interaction-modes.md`, `09-rules-and-the-learning-loop.md` — gates, interaction modes, Rules/Sensors/Learning Loop.
- `docs/guide/glossary.md` — canonical terminology (the source for the vocabulary bridge).
- `docs/reference/*` — engine, orchestrator, stage protocol (for the advanced electives).

**External references:**
- *AI-DLC Workflows 2.0 Specification* (PDF, at `assets/…` / `dist/…`) — principles: Generate-Verify-Learn, three-compartment model, progressive autonomy. *(Note: the installed build has since grown to 5 phases / 32 stages — prefer the installed docs above where they differ.)*
- *AI-Driven Development Lifecycle — Method Definition* (white paper) — origin of the methodology and its vocabulary. *(Some v1 flavor terms, e.g. "Mob Elaboration" and "Deployment Unit," are not used in the installed v2.)*
- AWS DevOps blog: *AI-Driven Development Life Cycle: Reimagining Software Engineering* (2025).

**Next step after sign-off:** turn Section 5 into per-module specs (learning objectives, lesson draft, `/aidlc` lab script, checkpoint), starting with the Shared Core — and **commit `training/` so it survives future re-clones.**
