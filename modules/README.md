# AI-DLC Bootcamp — Modules

Lesson content for the [AI-DLC Adoption Bootcamp](../aidlc-bootcamp-plan.md). Each lesson is standalone Markdown, rendered via GitHub Pages, and follows one template so learners get a predictable rhythm and authors have a checklist.

## Folder layout

```
modules/
  shared-core/      C1–C6  (all roles)
  pm/               P1–P3  (Product Manager add-on)
  ux/               U1–U3  (UX Designer add-on)
  developer/        D1–D4  (Developer add-on)
  capstone/         X1
  electives/        A1–A2
```

## Lesson template

Every lesson uses this shape (see `shared-core/C1-why-aidlc.md` as the reference implementation):

1. **Front-matter block** — module id, track, time, format, prerequisites.
2. **Learning objectives** — 3–5, verb-first.
3. **Why this matters** — one short hook paragraph.
4. **Read** — the core content, ~600–1,200 words, with **one diagram**.
5. **🎧 See it** — a short screencast placeholder (title + 1-line description).
6. **🧪 Try it** — a hands-on box; keep it doable even before setup where possible.
7. **Terminology** — a collapsible `<details>` "Show traditional-term mapping" (the toggle).
8. **✅ Checkpoint** — 3–5 questions, each answer in a collapsible `<details>`.
9. **Key takeaways + Next** — bullets and a link to the following lesson.

## Conventions

- **AI-DLC term primary, traditional analogue alongside** on first use. The tool prints AI-DLC terms, so learners must recognize them; the toggle keeps the Agile mapping one click away.
- **Ground every claim in the installed v2 docs** (`docs/guide/`, `docs/reference/`, `glossary.md`) — not the older release layout or the 2.0 spec PDF, which differ. Prefer the installed docs where they conflict.
- **Labs run on the `workshop` scope** against a shared GitHub repo (`/aidlc --scope workshop`).
- Use plain Markdown that renders on GitHub Pages. The `<details>` element gives real, dependency-free toggles for both terminology and quiz answers.
- **Git platform: GitHub is the named default** (GitLab requires VPN internally and stays a viable alternative), **but write core git mechanics platform-neutrally** (branch / push / remote — AI-DLC uses plain git). Isolate the few platform-specific nouns behind the mapping callout in `developer/D1`: Pull Request↔Merge Request, GitHub Actions↔`.gitlab-ci.yml`, GitHub Pages↔GitLab Pages, Repository↔Project. Switching hosts is a find-and-replace on those terms, not a rewrite.
- **Note:** the `developer/D1` file slug still ends `-gitlab` (cosmetic only — the page title and content are GitHub-default). Renaming it would break inbound links across modules, so it's left as-is.

## Status

| Module | File | Status |
| --- | --- | --- |
| C1 Why AI-DLC | `shared-core/C1-why-aidlc.md` | ✅ drafted |
| C2 Lifecycle & vocabulary | `shared-core/C2-lifecycle-and-vocabulary.md` | ✅ drafted |
| C3 Setup & first `/aidlc` | `shared-core/C3-setup.md` | ✅ drafted |
| C4 Scopes, depth & inputs | `shared-core/C4-scopes-and-inputs.md` | ✅ drafted |
| C5 Interaction discipline | `shared-core/C5-interaction-discipline.md` | ✅ drafted |
| C6 Greenfield vs. brownfield | `shared-core/C6-greenfield-vs-brownfield.md` | ✅ drafted |
| **Shared Core** | `shared-core/` | ✅ **complete (C1–C6)** |
| **P1–P3 (PM add-on)** | `pm/` | ✅ **complete** |
| **U1–U3 (UX add-on)** | `ux/` | ✅ **complete** |
| **D1–D4 (Developer add-on)** | `developer/` | ✅ **complete** |
| **X1 (Capstone)** | `capstone/` | ✅ **complete** |
| **A1–A2 (Electives)** | `electives/` | ✅ **complete** |
| **ALL MODULES** | — | ✅ **complete (18 lessons)** |
