# D2 — Team Knowledge & Rules

> **Module:** D2 · **Track:** Developer add-on · **Time:** ~60 min · **Format:** 📖 Read + 🧪 Hands-on
> **Prerequisites:** [D1 — Setup](D1-setup-claude-code-gitlab.md)

## Learning objectives

By the end of this lesson you can:

- Encode your stack, standards, and constraints as **team Knowledge** and **Rules**.
- Explain the **five-layer rule chain** (org → team → project → phase → stage) and how it resolves.
- Use **allow/deny lists** and **example code** to steer code generation.
- Describe how **Sensors** give a deterministic second opinion.

## Why this matters

Out of the box, the AI writes reasonable-but-generic code. The difference between "we spend every review fixing style and stack drift" and "generated code lands in our conventions" is whether you've encoded your standards. This is the single highest-leverage thing a developer does in AI-DLC — and it pays off on every future run.

## Read

### Two ways to shape the AI: Knowledge and Rules

- **Knowledge** = reference material agents *read* at stage start (your stack docs, patterns, examples). Two tiers: methodology knowledge ships with the framework; **team knowledge** is yours, under `aidlc/knowledge/`.
- **Rules** = persistent *behavioral* instructions ("always…", "never…") that shape how agents work, resolved into every relevant stage.

Use Knowledge to *inform* and Rules to *constrain*.

### Team Knowledge: teach the AI your stack

Drop your standards into Tier-2 knowledge so the relevant agent loads them:

```
aidlc/knowledge/
├── aidlc-shared/              # every agent sees this (org-wide conventions)
└── aidlc-developer-agent/     # loaded when the developer agent generates code
```

For the developer agent, the highest-value contents are your **languages/frameworks**, project structure, and — most valuable of all — **example code** showing canonical patterns for an endpoint, a function, a test, and an IaC snippet. One or two real examples do more to align generation than paragraphs of prose, because the AI has a concrete pattern to follow instead of inventing one.

### Rules: the five-layer chain

Rules live as plain-Markdown files in the active space's memory layer:

```
aidlc/spaces/<active-space>/memory/
├── org.md          # framework + org-wide defaults (trunk-based dev, testing posture…)
├── team.md         # your team's affirmed practices
├── project.md      # this project's specialization
└── phases/
    ├── inception.md
    └── construction.md   # e.g. rules that apply to every Construction stage
```

They resolve through a **strict-additive** chain: **org → team → project → phase → stage**. "Strict-additive" means every applicable rule appears in the agent's context — nothing is silently overridden. The chain resolves **once** at workflow start. Files use topical headings like `## Way of Working`, `## Testing Posture`, `## Code Style`, `## Deployment`. You can hand-edit them, and the **Learning Loop** also writes to them (D4). Conflicts are caught at admission time, when a rule is written — not at runtime.

> Recall from C2/D1: Practices Discovery (2.2) affirms `## Way of Working` (branching, testing posture) into `team.md`/`project.md`. That's the same mechanism you're using here, just authored deliberately.

### Allow/deny lists steer generation

The most effective Rules for code quality are explicit **allow and deny lists** — and a denial is far stronger when it names the *reason* and the *alternative*:

> **Prohibited:** `moment` (bundle size + maintenance mode) — **use** `date-fns`.
> **Required:** all HTTP handlers validate input with our `zod` schemas.
> **Required:** structured logging via `@acme/logger`; never `console.log` in shipped code.

Without the reason and substitute, the AI may honor the prohibition but make a poor replacement choice. With them, it substitutes intelligently.

### Sensors: a deterministic second opinion

**Rules** are the *feedforward* half of a control loop; **Sensors** are the *feedback* half — deterministic checks that fire on writes to a stage's outputs and record advisory results (they never block your workflow). Some verification is a judgment call best left to an LLM rule (most code-review heuristics); some must be **deterministic** and belong in a Sensor (a linter, a type-check, "no endpoint without auth"). You'll wire the two together in D4; for now, know that a Rule you find yourself checking by hand is often a candidate to back with a Sensor.

## 🧪 Try it (25 min)

On the workshop repo:

1. **Add developer knowledge** — create `aidlc/knowledge/aidlc-developer-agent/patterns.md` with one real **example endpoint** and one **example test** in your stack.
2. **Write allow/deny Rules** — in `project.md` under `## Code Style` / dependencies, add two prohibitions *with reason + alternative* and one "required" rule.
3. **Confirm the chain** — note which files contribute (org/team/project/phase) for a Construction stage. Are your rules all present (strict-additive)?
4. **Run Code Generation (3.5)** on a small Unit and check: did the generated code follow your example pattern and honor your deny list?
5. **Spot a Sensor candidate** — pick one Rule you'd rather verify deterministically and describe the check.

✅ **Done when:** generated code visibly follows your example pattern and respects at least one deny-list rule.

## Terminology

<details>
<summary><b>Show traditional-term mapping</b></summary>

| AI-DLC term | ≈ Traditional analogue |
| --- | --- |
| Team Knowledge | Your engineering handbook / patterns docs |
| Rule | Coding standard / lint policy (as prose) |
| Five-layer chain | Cascading config (org → project) |
| Allow/deny list | Approved/prohibited dependencies |
| Sensor | CI linter / type-check / policy check |
| `## Way of Working` | Team working agreements |

</details>

## ✅ Checkpoint

<details>
<summary>1. What's the difference between Knowledge and Rules?</summary>

Knowledge is reference material agents read (stack docs, examples); Rules are persistent behavioral constraints resolved into stages. Knowledge informs; Rules constrain.
</details>

<details>
<summary>2. What is the highest-value Knowledge for the developer agent?</summary>

Example code — canonical patterns for an endpoint, function, test, and IaC snippet. Concrete examples align generation better than prose.
</details>

<details>
<summary>3. What does "strict-additive" mean in the rule chain?</summary>

Every applicable rule across org → team → project → phase appears in the agent's context; nothing is silently overridden. Conflicts are caught when a rule is written, not at runtime.
</details>

<details>
<summary>4. Why include the reason and alternative in a deny-list rule?</summary>

Without them the AI may honor the prohibition but pick a poor substitute. With them it substitutes intelligently.
</details>

<details>
<summary>5. Rules vs. Sensors — which is deterministic?</summary>

Sensors are deterministic feedback checks (linters, type-checks); Rules are feedforward prose guidance. Judgment-call checks stay as Rules; zero-tolerance checks become Sensors.
</details>

## Key takeaways

- Encode your stack as **team Knowledge** (esp. **example code**) and your standards as **Rules**.
- Rules resolve **org → team → project → phase → stage**, strict-additive, once at start.
- **Allow/deny lists with reasons + alternatives** are the strongest code-quality lever.
- **Sensors** back the rules you'd otherwise check by hand — deterministically.

**Next:** [D3 — Construction Bolts, stage by stage](D3-construction-bolts.md) — running 3.1–3.5, the walking skeleton, the ladder prompt, and claiming a Bolt.
