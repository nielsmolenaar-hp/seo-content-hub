# SEO & Content — Document Hub (shareable site)

A **ready-to-publish static website**. On GitHub Pages it gives a public URL that renders the
HTML and that **anyone with the link can open — no login**. Each document is included as a
rendered **HTML page** and as **Markdown source**.

## What's in here
- `index.html` — the hub (links every document, HTML + Markdown)
- `HelloPrint-Page-Content-Model-COMPLETE.html` / `.md` — full specs (Markdown is the source of truth)
- `Team-Roster-v2.9.1.html` / `.md` — team roster
- `Content-Rebuild-Engine-Plan-v1.0.html` / `.md` — content engine rebuild plan
- `helpcenter-blog-seo-integration-plan.html` / `.md` — content hierarchy
- `HelloPrint-Block-Design-Gallery.html` — block & variation gallery (visual companion, HTML only)
- `Design-Brief_Batch1_AGENT-BUILD-PROMPTS.md` — Batch 1: shared blocks + PLP pages (DA-1 / DA-2)
- `Design-Brief_Batch2_FLP_AGENT-BUILD-PROMPTS.md` — Batch 2: FLP filter chrome (DA-3 / DA-4)
- `Design-Brief_Batch3_PDP-refresh_AGENT-BUILD-PROMPTS.md` — Batch 3: PDP refresh (DA-5)
- `Design-Brief_Batch4_V2_AGENT-BUILD-PROMPTS.md` — Batch 4: V2 blocks (DA-6)
- `README.md`, `.nojekyll`

In the hub, **Open page** links to the rendered HTML on the Pages site; **Markdown** links to the
`.md` rendered on GitHub (`github.com/<owner>/<repo>/blob/main/<file>.md`). All HTML pages carry a
`noindex` tag, so they won't appear in search results — but anyone with the URL can read them.

> The Markdown links assume the repo is `nielsmolenaar-hp/seo-content-hub` on branch `main`.
> If you fork or rename, update the `blob/main` links in `index.html`.

---

## Publish to GitHub Pages

The repo already exists at **github.com/nielsmolenaar-hp/seo-content-hub**. To update it with this
full set, replace the files (re-upload all, or `git push`), then enable Pages if you haven't:

**Web UI:** repo → **Add file → Upload files** → drag in everything from this folder → **Commit**.
**CLI:**
```bash
cd seo-content-hub
git init -b main
git add .
git commit -m "SEO & Content hub — HTML + Markdown, all docs"
git remote add origin https://github.com/nielsmolenaar-hp/seo-content-hub.git
git push -u origin main      # use --force only if replacing existing history
```

Then: **Settings → Pages → Deploy from a branch → `main` → `/ (root)` → Save.**
Live at `https://nielsmolenaar-hp.github.io/seo-content-hub/` within ~1 minute.

## Notes
- The repo must stay **public** for anyone-with-link access.
- `.nojekyll` is a hidden file; Finder may hide it on drag-and-drop. It's optional here (no filenames
  start with `_`), but the CLI push includes it automatically.
- To update a doc later: replace its file(s) and re-deploy (Pages rebuilds in ~1 min).
