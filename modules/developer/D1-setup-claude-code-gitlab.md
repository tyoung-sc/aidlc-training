# D1 — Setup: Claude Code + Git (and the Harness Landscape)

> **Module:** D1 · **Track:** Developer add-on · **Time:** ~75 min · **Format:** 🧪 Hands-on
> **Prerequisites:** Shared Core [C1–C6](../shared-core/C1-why-aidlc.md)

## Learning objectives

By the end of this lesson you can:

- Confirm a working Claude Code + `bun` setup and where AI-DLC's other harnesses fit.
- Explain how AI-DLC uses **plain git** and wire a project to a shared remote.
- Describe how `aidlc/` artifacts are versioned and what to commit vs. ignore.
- Position Cursor/VS Code correctly (alongside, not a harness).

> 📌 **Git platform note.** This bootcamp uses **GitHub** as the default host, but AI-DLC's git usage is **plain git** — nothing platform-specific. Everything works identically on GitLab (the internal alternative, which requires VPN). Where a platform term differs, use this mapping:
>
> | GitHub (default) | GitLab (alternative) |
> | --- | --- |
> | Pull Request (PR) | Merge Request (MR) |
> | GitHub Actions (`.github/workflows/`) | `.gitlab-ci.yml` |
> | GitHub Pages | GitLab Pages |
> | Repository | Project |
>
> The AI-DLC mechanics (branch, push, remote, Bolt claiming) don't change between them.

## Why this matters

Setup that "mostly works" costs the whole team hours later. This lesson gets your environment rock-solid, and — more importantly for a developer — clarifies that AI-DLC drives *ordinary git*, so you already know 90% of the version-control story. The only new idea is *which files* AI-DLC writes and how the team shares them.

## Read

### Prerequisites (recap from C3, developer depth)

You need **Claude Code** and **`bun`** — that's it. Re-confirm:

```bash
command -v claude >/dev/null && echo "✓ Claude Code" || echo "✗ install Claude Code"
command -v bun    >/dev/null && echo "✓ bun"         || echo "✗ install bun"
/aidlc --doctor
```

Remember the classic failure: `bun` must be on the **non-interactive** shell `PATH` (`~/.zshenv` / `~/.bashrc`, not `~/.zshrc`), because Claude Code runs your shell non-interactively.

### The harness landscape

AI-DLC ships from one harness-neutral core, rendered onto several CLI harnesses: **Claude Code** (our primary), **Kiro CLI**, **Kiro IDE**, **Codex CLI**, and **opencode**. They all run the same engine and stages; only invocation and some native affordances differ (`/aidlc` on Claude Code/Kiro, `$aidlc` on Codex). For the bootcamp you only need Claude Code — but know the others exist so you can meet a teammate on their tool.

**Cursor / VS Code:** Cursor is **not** a shipped v2 harness. Use Claude Code's terminal or its **VS Code integration**; you can keep Cursor open as an editor alongside, but AI-DLC runs through Claude Code. (Building a custom Cursor harness is possible but out of scope here.)

### AI-DLC uses plain git

There's no AI-DLC-specific version-control system. Work is branches you push to a shared **remote**; reviews are MRs/PRs; the workshop **Bolt-claiming** mechanic (D3) is literally `git fetch` then `git push` of a `bolt-<name>` branch — first push wins. If you know git, you know this. Wire a project to your remote the usual way:

```bash
git init            # if new
git remote add origin <your-remote-url>
git push -u origin main
```

The base branch you branch Bolts from is decided by your team's affirmed **way of working** (from Practices Discovery, 2.2) — trunk-based teams branch off `main`, gitflow off `develop`. Don't guess it; read it from space memory (D2).

### What AI-DLC writes, and what to version

After setup your project has two AI-DLC trees:

- **`.claude/`** — the engine (stages, agents, hooks, settings). Committed so the team shares one version.
- **`aidlc/`** — the workspace: `spaces/<space>/memory/` (Rules), `knowledge/`, `codekb/`, and per-intent `intents/<YYMMDD>-<label>/` records (requirements, designs, state, audit).

The **intent records and space memory are the durable, shareable output** — commit them so the team (and the workshop) build from the same artifacts. Keep secrets out of shared config: put `AWS_PROFILE`, API keys, etc. in `.claude/settings.local.json` (gitignored). A stray `.aidlc-recovery.md` and hook-health dirs are local-only.

> 🔑 **Lesson from this bootcamp's own history:** artifacts that aren't committed can be wiped by a re-clone or branch switch. If it matters, commit it.

## 🧪 Try it (25 min)

1. **Verify** — run the three commands above; get `/aidlc --doctor` green (fix `bun` PATH if needed).
2. **Wire a remote** — point your workshop project at the shared remote; confirm `git remote -v`.
3. **Inspect the trees** — list `.claude/` and `aidlc/`; open one intent record under `aidlc/spaces/default/intents/`.
4. **Branch check** — find your team's base branch in `aidlc/spaces/<space>/memory/` (`## Way of Working`). Create a throwaway `bolt-demo` branch off it and push it; then delete it.
5. **Secrets hygiene** — confirm no secrets live in `.claude/settings.json`; note what belongs in `settings.local.json`.

✅ **Done when:** `--doctor` is green, your remote is wired, and you've pushed and removed a `bolt-demo` branch off the correct base.

## Terminology

<details>
<summary><b>Show traditional-term mapping</b></summary>

| AI-DLC term | ≈ Traditional analogue |
| --- | --- |
| Harness | The CLI/IDE AI-DLC runs in |
| Shared remote | `origin` / the team's central repo |
| `bolt-<name>` branch | Feature branch for one Bolt |
| Way of working | Branching + testing conventions |
| `.claude/` | The tool's engine/config |
| `aidlc/` | The project's artifacts + memory |

</details>

## ✅ Checkpoint

<details>
<summary>1. What are the two prerequisites, and the classic setup failure?</summary>

Claude Code + bun. The classic failure is bun not being on the non-interactive shell PATH (~/.zshenv / ~/.bashrc).
</details>

<details>
<summary>2. Is Cursor a supported harness? What do developers use?</summary>

No. Use Claude Code (terminal or VS Code integration), optionally with Cursor open as an editor alongside.
</details>

<details>
<summary>3. What kind of git does AI-DLC use, and how do you claim a Bolt?</summary>

Plain git — no platform-specific features. You claim a Bolt by pushing a `bolt-<name>` branch to the shared remote (first push wins).
</details>

<details>
<summary>4. Which AI-DLC trees should be committed, and where do secrets go?</summary>

Commit `.claude/` (engine) and the `aidlc/` intent records + space memory. Secrets go in `.claude/settings.local.json` (gitignored), never in shared `settings.json`.
</details>

## Key takeaways

- Two prerequisites (**Claude Code + bun**); Cursor is alongside, not a harness.
- AI-DLC drives **plain git** — branch, push, remote; Bolt claiming is just `git push`.
- **Commit** `.claude/` and the `aidlc/` records/memory; keep **secrets** in `settings.local.json`.
- Read your **base branch** from affirmed practices; don't guess.

**Next:** [D2 — Team Knowledge & Rules](D2-knowledge-and-rules.md) — encoding your stack, standards, and guardrails so generation follows house style.
