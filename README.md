# SEO & Content — Document Hub (shareable site)

This folder is a **ready-to-publish static website**. Put it on GitHub Pages and you get a
public URL that renders the HTML and that **anyone with the link can open — no login**.

## What's in here
- `index.html` — the hub (links to all four documents)
- `HelloPrint-Page-Content-Model-COMPLETE.html` — full specs
- `Team-Roster-v2.9.1.html` — team roster
- `helpcenter-blog-seo-integration-plan.html` — content hierarchy
- `.nojekyll` — tells GitHub Pages to serve the files as-is

The **Content Rebuild Engine — Action Plan** stays in Google Docs; the hub links straight to it.
All three local pages carry a `noindex` tag, so they won't appear in search results — but anyone with the URL can read them.

---

## Publish to GitHub Pages (~3 minutes, one-time)

> The repo must be **public** for "anyone with the link" to work. (GitHub Pages on a *private*
> repo requires viewers to be logged in with repo access — that would defeat the point.)
> Do **not** reuse the brain repo — that would expose the whole vault. Make a new repo.

### Option A — no terminal (browser only)
1. On github.com, create a new **public** repo, e.g. `seo-content-hub` (under your account or the Helloprint org).
2. In the new repo: **Add file → Upload files** → drag in everything from this folder (including the hidden `.nojekyll`) → **Commit changes**.
3. Repo **Settings → Pages** → Source: **Deploy from a branch** → Branch: `main` / `/ (root)` → **Save**.
4. Wait ~1 minute. Your site is live at `https://<owner>.github.io/seo-content-hub/`.

### Option B — command line
```bash
cd seo-content-hub
git init -b main
git add .
git commit -m "SEO & Content document hub"
# create an EMPTY public repo on github.com first, then:
git remote add origin https://github.com/<owner>/seo-content-hub.git
git push -u origin main
```
Then do step 3 above (Settings → Pages → main / root → Save).

---

## Sharing
Send people this link: `https://<owner>.github.io/seo-content-hub/`

## Updating a document later
Replace the file in the repo (re-upload or `git push`); Pages redeploys automatically in ~1 minute.

## To make it private again
Delete the repo, or set it to private (the Pages site stops serving publicly). To remove a single
doc, delete that file from the repo.
