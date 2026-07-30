# C3 — Setup & Your First `/aidlc`

> **Module:** C3 · **Track:** Shared Core (all roles) · **Time:** ~60 min · **Format:** 🧪 Hands-on
> **Prerequisites:** [C1 — Why AI-DLC](C1-why-aidlc.md), [C2 — Lifecycle & vocabulary](C2-lifecycle-and-vocabulary.md)

## Learning objectives

By the end of this lesson you can:

- State the two prerequisites AI-DLC needs and why `bun` must be on your `PATH`.
- Get a working AI-DLC project — by cloning the shared workshop repo (fast path) or installing from scratch (reference).
- Run `/aidlc --doctor` and read its health report.
- Launch your first workflow, watch the first **intent** auto-birth, and reach an approval gate.

## Why this matters

Setup is the one place a whole cohort can stall. Ninety percent of "it doesn't work" turns out to be `bun` not visible to Claude Code, or the workspace shell not copied. Do this lesson once, carefully, and the rest of the bootcamp is just `/aidlc`.

## Read

### The two prerequisites

AI-DLC runs *inside* **Claude Code** and its tooling runs on **`bun`**. That's the whole dependency list.

| Prerequisite | Why | Install |
| --- | --- | --- |
| **Claude Code** | The orchestrator, agents, and hooks all execute within it | `curl -fsSL https://claude.ai/install.sh \| bash` (macOS/Linux/WSL), or `brew install --cask claude-code` |
| **bun** | Runs all CLI tools + the 13 hooks (state, audit, sensors…) at ~20 ms startup | `curl -fsSL https://bun.sh/install \| bash` |

> ⚠️ **The #1 gotcha: `bun` on `PATH` for non-interactive shells.** Claude Code runs your shell *non-interactively*, so it reads `~/.zshenv` (zsh) or `~/.bashrc` (bash) — **not** `~/.zshrc`. If `which bun` works in your terminal but `/aidlc --doctor` says bun is missing, add the bun `PATH` export to the right file (`~/.zshenv` / `~/.bashrc`) and restart Claude Code.

Verify both:

```bash
command -v claude >/dev/null && echo "✓ Claude Code" || echo "✗ install Claude Code"
command -v bun    >/dev/null && echo "✓ bun"         || echo "✗ install bun"
```

### The model backend (who handles it)

The v2 distribution ships configured for **AWS Bedrock** (it pins Claude models via Bedrock inference profiles). Getting Bedrock working needs a one-time AWS-account step: enable Anthropic model access, attach IAM permissions to invoke models, provide credentials, and set your region — or use the built-in wizard (`claude` → *3rd-party platform → Amazon Bedrock*).

> 🎓 **For the bootcamp, your facilitator provisions this.** The shared workshop repo comes with Bedrock access already configured, so as a participant you normally don't touch AWS. The full account setup lives in the collapsible below for whoever prepares the shared repo (and for when you set up your own project later).

<details>
<summary><b>Reference: from-scratch install & AWS Bedrock setup</b> (facilitators / your own machine)</summary>

**Install the implementation** from a `v2` clone into your project:

```bash
git clone https://github.com/awslabs/aidlc-workflows.git
cd aidlc-workflows && git checkout v2
cp -r dist/claude/.claude/ your-project/.claude/
cp -r dist/claude/aidlc/   your-project/aidlc/     # workspace shell — a SIBLING of .claude/, not inside it
```

Copy **both** trees (or the whole `dist/claude/`): `.claude/` is the engine; `aidlc/spaces/default/memory/` is the workspace shell the engine reads. `--doctor` fails its "workspace shell ready" check if the `aidlc/` tree is missing. There is **no init/scaffold step** — the shell ships pre-built.

**AWS Bedrock (once per account):** (1) enable Anthropic model access in the Bedrock console; (2) attach IAM permissions (`bedrock:InvokeModel`, `…WithResponseStream`, `ListInferenceProfiles`, `GetInferenceProfile`); (3) provide credentials via the standard AWS chain (`aws configure`, SSO, or exported keys); (4) set `AWS_REGION` if not `us-east-1`. Keep secrets in `.claude/settings.local.json` (gitignored), never in the shared `settings.json`. Easier path: run `claude` and pick *3rd-party platform → Amazon Bedrock* to let the wizard detect it. (MCP servers in `.mcp.json` are optional — missing credentials never block a run.)

</details>

### There's no "init" — the first run births your intent

Once the distribution is in place, you **don't** run a scaffold command. The first time you run `/aidlc`, the engine **auto-births** your first **intent** into the active **space**, creating its record dir at `aidlc/spaces/<space>/intents/<YYMMDD>-<label>/` with its own `aidlc-state.md`, `audit/` trail, and stage artifacts. (Recall from C2: a *space* is a team workspace; an *intent* is the epic-level thing you're building.)

### Verify with `/aidlc --doctor`

The health check confirms everything's wired. It's **read-only** and safe to run before any intent exists.

```
/aidlc --doctor
```

It exits `0` when all checks pass, `1` on any failure, and prints the full report either way. Among its checks: `bun` present, all 13 hooks present, `settings.json` valid, the **workspace shell** present (`.claude/` + `aidlc/spaces/default/memory/`), stage-graph integrity, and that all 9 scopes walk cleanly. Example lines:

```
✓ bun installed (required for CLI tools and hooks)
✓ settings.json present
✓ AWS_AIDLC_DEFAULT_SCOPE (unset — no project default)
```

Two more you'll use often: `/aidlc --status` (read-only progress summary) and `/aidlc --version`.

### Your first workflow

With `--doctor` green, launch a tiny run. Naming a scope up front keeps it small and births the first intent:

```
/aidlc --scope poc Build a to-do list REST API with in-memory storage
```

Watch for three things you learned in C2: the **scope** banner, the **intent** auto-birthing into `aidlc/spaces/default/intents/…`, and the first **approval gate** where the conductor stops for your review. Read the artifact, then approve or request changes. That's the whole rhythm.

## 🎧 See it (7 min)

*Screencast placeholder — [C3: Zero to first gate, 7 min].* Fresh machine → install checks → clone the workshop repo → `/aidlc --doctor` (green) → `/aidlc --scope poc …` → first intent births → stop at the first gate. Includes the `bun`-on-`PATH` fix in real time.

## 🧪 Try it (20 min)

1. **Prereq check** — run the two `command -v` lines above. Fix `bun`'s `PATH` if needed (`~/.zshenv` / `~/.bashrc`).
2. **Get a project** — clone the shared **workshop repo** your facilitator provides (fast path), *or* follow the reference collapsible to install into a throwaway folder.
3. **Health check** — run `/aidlc --doctor`. Confirm it exits clean. If not, read the failing check and fix just that.
4. **First run** — `/aidlc --scope poc Build a to-do list REST API with in-memory storage`. Stop at the **first gate**. Note the intent's folder under `aidlc/spaces/default/intents/`.
5. **Look around** — open that intent's `aidlc-state.md`. Find the current stage and scope. Don't approve past the first gate — we work gates properly in C5.

✅ **Done when:** `--doctor` is green and you've reached (and paused at) your first approval gate.

## Terminology

<details>
<summary><b>Show traditional-term mapping</b></summary>

| AI-DLC term | ≈ Traditional analogue |
| --- | --- |
| Harness | The CLI/IDE you run it in (here: Claude Code) |
| Workspace shell | Project scaffolding / starter template (but pre-built — no init) |
| Space | Team workspace / project area |
| Intent | Epic / feature request |
| `--doctor` | Environment health check / linter for your setup |

</details>

## ✅ Checkpoint

<details>
<summary>1. What are AI-DLC's two prerequisites?</summary>

Claude Code (the harness it runs in) and `bun` (runs the CLI tools and hooks).
</details>

<details>
<summary>2. `which bun` works in your terminal but `--doctor` says it's missing. Why, and the fix?</summary>

Claude Code runs shells non-interactively, reading `~/.zshenv` / `~/.bashrc` — not `~/.zshrc`. Add the bun `PATH` export to the correct file and restart Claude Code.
</details>

<details>
<summary>3. After copying the distribution, what init/scaffold command do you run?</summary>

None. The workspace shell ships pre-built; the first `/aidlc` auto-births the first intent.
</details>

<details>
<summary>4. What does `/aidlc --doctor` do, and is it safe before any intent exists?</summary>

Runs a read-only health check (bun, hooks, settings, workspace shell, graph integrity, scopes). Exits 0/1 and prints the report either way. Yes — it's safe on a fresh setup and creates no files until an intent exists.
</details>

## Key takeaways

- Two prerequisites: **Claude Code + bun**; the classic failure is **bun not on the non-interactive `PATH`**.
- The distribution ships a **pre-built workspace shell** — **no init step**; the first `/aidlc` **auto-births** your intent.
- **`/aidlc --doctor`** is your green light; `--status` and `--version` round out the basics.
- Bootcamp participants use the **facilitator-provisioned workshop repo**, so AWS Bedrock is already handled.

**Next:** [C4 — Scopes, depth & inputs that work](C4-scopes-and-inputs.md) *(to be authored)* — choosing the right scope and depth, and writing an intent the AI can actually run with.
