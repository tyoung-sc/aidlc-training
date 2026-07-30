<!--
LESSON TEMPLATE (all modules follow this shape):
  1. Front matter block: module id, track, time, format, prerequisites
  2. Learning objectives (3–5, verb-first)
  3. Why this matters (hook, ≤1 short para)
  4. Read (the core content — 600–1,200 words, one diagram)
  5. See it (a short video/screencast placeholder)
  6. Try it (a hands-on box — even if tiny)
  7. Terminology toggle (collapsible traditional-term mapping)
  8. Checkpoint (3–5 questions with collapsible answers)
  9. Key takeaways + what's next
Keep AI-DLC terms primary; pair with a traditional analogue on first use.
-->

# C1 — Why AI-DLC: Reimagine, Don't Retrofit

> **Module:** C1 · **Track:** Shared Core (all roles) · **Time:** ~45 min · **Format:** 📖 Read + 🎧 Watch
> **Prerequisites:** none — this is the starting point.

## Learning objectives

By the end of this lesson you can:

- Explain what problem AI-DLC is trying to solve, and why "reimagine rather than retrofit" is its founding choice.
- Distinguish **AI-assisted** development from the **AI-driven** approach AI-DLC takes.
- Describe how AI-DLC "reverses the conversation direction" and where humans stay in control.
- Name the benefits the methodology is optimizing for — and the one habit that makes or breaks them.

## Why this matters

Most teams bolt an AI assistant onto their existing process and get a faster version of the same handoffs. AI-DLC starts from a different premise: if AI can do the planning, decomposition, and drafting, the *process itself* should change — not just the typing speed. Understanding that premise is what separates teams who get real leverage from teams who get a fancier autocomplete.

## Read

### Two ways teams use AI today — and why both underdeliver

Organizations tend to apply AI to software in one of two ways. In **AI-assisted** development, AI enhances discrete tasks — code completion, test generation, documentation — while humans still do the intellectual heavy lifting and carry work through every stage by hand. In **AI-autonomous** development, AI is expected to turn a one-line request straight into a finished application with no one in the loop. The first underuses AI; the second overtrusts it. Both tend to produce disappointing results on velocity *or* quality.

AI-DLC takes a third path: **AI-driven** development with human oversight. AI systematically creates detailed plans, actively asks for the context and decisions only humans can provide, and defers the critical calls to people. You get AI's speed on the undifferentiated work and human judgment exactly where it's needed.

### Reimagine, don't retrofit

Traditional methods — Scrum, Kanban, a classic SDLC — were designed for *human-driven, long-running* work. Their rituals (multi-week sprints, standups, effort estimation) assume the bottleneck is human throughput over weeks. When AI compresses that work into hours or days, many of those rituals stop earning their keep, and forcing AI into them "reinforces outdated inefficiencies." AI-DLC's founding move is to redesign the workflow around AI as a **central collaborator**, not to retrofit AI into a process built for a slower era. The often-quoted line: we want *automobiles, not faster horse-drawn carriages.*

### Reverse the conversation direction

Here's the shift learners feel most immediately. In a normal AI chat, **you** initiate: you ask, it answers. In AI-DLC, the **AI initiates and directs** — it breaks a high-level intent into stages and tasks, proposes options and trade-offs, and asks *you* clarifying questions at the right moments. Your job flips from *driver of every keystroke* to **approver and decision-maker**.

The white paper's analogy is Google Maps: you set the destination (the intent), the system proposes the route (task decomposition and recommendations), and you stay in control — moderating, overriding, and confirming as you go. You don't hand-draw the route; you also don't blindly follow it into a lake.

```
  Traditional AI chat                 AI-DLC
  ───────────────────                 ──────
  Human ──asks──▶ AI                  AI ──plans, proposes, asks──▶ Human
  Human ◀─answers── AI                Human ──validates, decides──▶ AI
  (human drives every step)           (AI drives; human approves at gates)
```

### What AI-DLC is optimizing for

The methodology is explicit about the outcomes it chases:

- **Velocity** — AI rapidly generates and refines requirements, designs, code, and tests, turning weeks of work into hours or days.
- **Innovation** — with the heavy lifting handled, people spend their time on creative, high-value problems.
- **Quality** — continuous clarification means you build what you actually intended, with organizational standards and comprehensive tests applied consistently, and traceability from requirement to deployment.
- **Market responsiveness** — short cycles let you adapt to feedback quickly.
- **Developer experience** — less repetitive toil, more problem-solving and business context.

### The one habit that makes it work

Every one of those benefits depends on a single discipline: **human oversight at the gates is a "loss function."** AI-DLC pauses at decision points so you can catch and prune errors *early*, before they compound downstream. Approving an artifact without reading it doesn't save time — it quietly ships a mistake into every stage that builds on it. Throughout this bootcamp you'll hear one rule repeated: **never vibe code.** Read before you approve.

## 🎧 See it (5 min)

*Screencast placeholder — [C1: From "faster autocomplete" to AI-driven, 5 min].* A side-by-side: the same feature request handled as an AI-assisted task versus an AI-driven `/aidlc` run, ending on a gate where the human overrides a proposed decision.

## 🧪 Try it (5 min)

No setup required yet. On paper or in a scratch doc:

1. Take a feature you shipped recently. Write it as a one-line **intent** (e.g., *"Add saved-payment methods to checkout"*).
2. List three questions a good collaborator would ask you *before* writing any code.
3. Mark which of those three are **decisions only a human should make** (business rules, trade-offs, risk) versus things AI could reasonably propose.

That instinct — knowing which calls are yours — is the core skill AI-DLC formalizes.

## Terminology

<details>
<summary><b>Show traditional-term mapping</b></summary>

| AI-DLC framing | ≈ Traditional analogue |
| --- | --- |
| Intent | Epic / feature request |
| AI-driven development | (new — sits between "AI-assisted" and "fully autonomous") |
| Approver at a gate | Reviewer / sign-off |
| "Reverse the conversation" | (new — AI leads planning instead of the human) |

These pairings are scaffolding. The rendered lessons will keep this toggle available on every page; the AI-DLC term stays primary because the tool prints it on screen.

</details>

## ✅ Checkpoint

<details>
<summary>1. What's the difference between "AI-assisted" and "AI-driven" development?</summary>

AI-assisted: AI enhances discrete tasks while humans do the heavy lifting and carry work through each stage. AI-driven: AI plans and directs the workflow, proposing options and asking for decisions, with humans approving at gates.
</details>

<details>
<summary>2. In AI-DLC, who initiates the conversation, and what is the human's primary role?</summary>

The AI initiates and directs; the human is the approver/decision-maker — validating, selecting options, and confirming at junctures.
</details>

<details>
<summary>3. Why does AI-DLC "reimagine rather than retrofit" existing methods?</summary>

Traditional methods assume human-driven, multi-week cycles. AI compresses that work into hours/days, so their rituals lose value; forcing AI into them reinforces old inefficiencies. Automobiles, not faster carriages.
</details>

<details>
<summary>4. Why is "read before you approve" the load-bearing habit?</summary>

Gates act as a loss function that prunes errors early. Approving without reading passes mistakes to every downstream stage — negating the velocity and quality benefits.
</details>

## Key takeaways

- AI-DLC is **AI-driven with human oversight** — a deliberate middle path between assistant and autopilot.
- It **redesigns the workflow** around AI rather than retrofitting AI into old rituals.
- The AI leads; **you approve.** Google Maps, not a self-driving car with no steering wheel.
- Every benefit hinges on **reading before approving.**

**Next:** [C2 — The lifecycle & the vocabulary bridge](C2-lifecycle-and-vocabulary.md), where we map the 5 phases, meet the agent personas, and learn the terms the tool will put in front of you.
