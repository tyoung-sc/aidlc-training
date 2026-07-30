# Publishing the Bootcamp to GitHub Pages

This folder is a self-contained GitHub Pages site: `index.md` is the home page, `_config.yml` configures rendering, and `modules/` holds the lessons. The `<details>` terminology toggles and quiz answers render as working dropdowns on GitHub Pages with no extra work.

Target setup (your choices): **its own new repo**, **private for now**.

---

## ⚠️ Read first: private repos need a paid plan

**GitHub Pages on a *private* repo requires GitHub Team or Enterprise.** On the Free plan, Pages only works on **public** repos. Before you start, confirm the Security Compass org's plan:

- **Org has Team/Enterprise →** proceed below; you can publish privately.
- **Free plan →** either (a) make this one repo public (the content is courseware, not proprietary code — but that's your call), or (b) skip Pages for now and read the Markdown directly in the repo (GitHub renders `.md` and the `<details>` toggles in the file view too, just without the themed site).

---

## Step 1 — Create the repo

On github.com (in the Security Compass org or your account), create a new **private** repo, e.g. `aidlc-training`. Don't initialize it with a README (we'll push one).

## Step 2 — Push this folder as the repo root

From a copy of **this `training/` folder** (its contents become the repo root):

```bash
cd path/to/training
git init
git add .
git commit -m "AI-DLC bootcamp: initial content + Pages site"
git branch -M main
git remote add origin git@github.com:<org>/aidlc-training.git
git push -u origin main
```

## Step 3 — Set the baseurl (project sites only)

A project site publishes at `https://<org>.github.io/aidlc-training/`. For the theme's CSS/assets to resolve under that subpath, set `baseurl` in `_config.yml`:

```yaml
baseurl: "/aidlc-training"
```

Leave it `""` only if you use a custom domain or a `<org>.github.io` root site. Page-to-page links are relative, so they work either way — this only affects theme assets.

## Step 4 — Enable Pages

Repo **Settings → Pages**:

- **Source:** *Deploy from a branch*
- **Branch:** `main` · **Folder:** `/ (root)`
- Save. First build takes a minute or two; the page URL appears at the top when it's live.

(No GitHub Actions workflow is needed — the classic branch build renders Jekyll for you. The default Pages plugins `jekyll-relative-links` and `jekyll-optional-front-matter` — already referenced in `_config.yml` — make our `.md` cross-links and front-matter-less lessons work.)

## Step 5 — (Enterprise) restrict who can see it

On GitHub Enterprise you can set **Pages visibility** to private so only org members with repo access can view the site (Settings → Pages → *Visibility*). On Team, the site is served but access still follows repo permissions per your org config — confirm with your admin.

## Step 6 — Verify

Visit the published URL and check:

- The home page lists all modules and links open correctly.
- Inside a lesson, the **"Show traditional-term mapping"** and **checkpoint answer** dropdowns expand.
- Cross-links between lessons (e.g. C1 → C2) work.

---

## Optional upgrade: a nicer docs theme

`minima` is clean but plain. For a **sidebar + built-in search**, switch to **just-the-docs**:

1. In `_config.yml`, replace `theme: minima` with:
   ```yaml
   remote_theme: just-the-docs/just-the-docs
   plugins:
     - jekyll-remote-theme
     - jekyll-relative-links
     - jekyll-optional-front-matter
   ```
2. Add front matter to each lesson for sidebar nav/order, e.g.:
   ```yaml
   ---
   title: "C1 — Why AI-DLC"
   parent: "Shared Core"
   nav_order: 1
   ---
   ```
   (This is the one place that needs per-file edits; the lessons render fine without it, they just won't populate the sidebar.)

## Notes

- The `developer/D1` **file slug** still ends `-gitlab` for link stability; the page itself is GitHub-default. Harmless, but if you ever want it clean, rename the file and update the 7 inbound links.
- `references/` and any PDFs are excluded from the build (see `_config.yml`) so drafts/source docs aren't published.
- To move off GitHub later, the same folder publishes on GitLab Pages or any static host — the content is plain Markdown.
