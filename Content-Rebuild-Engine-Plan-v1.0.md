---
title: Content Rebuild Engine — Plan
type: plan
version: v1.0
status: draft
owner: Niels Molenaar
updated: 2026-06-05
scope: SEO & Content Agentic Team
related: [Team-Roster-v2.9.1, HelloPrint-Page-Content-Model-Master, Content-Engine-Business-Overview]
---

# Content Rebuild Engine — Plan

Rebuild all our content — fresh, optimised, nothing copied — in the new Contentful space, built and run by the SEO & Content agent team, **country by country**.

## The goal

Our organic traffic fell hard after last year's migration. This plan rebuilds every page we should have, to a high quality bar, in the new setup. Two promises hold throughout: **every page is genuinely good**, and **nothing that should exist is missed**. We're done when every country is live with 100% of its pages, all checked.

## Learnings from the current Content Engine

We've built a version of this before — the **[[Content-Engine-Business-Overview|current Content Engine]]**. It writes and translates product-page copy, makes the images and icons, and publishes to Contentful. It pulled work out of spreadsheets and Trello and scaled product onboarding. It earned its place, and the new system builds on it.

**What it did well — and we keep:**

- **Icon and product-image generation** — good quality, at scale. Our strongest asset.
- **A live connection to the product catalogue** — the plumbing works.
- **The custom-instruction field** — a good way to push iterations on the content.

**What we'll do better:**

- **It runs itself.** The old one was a screen someone had to click through. The new one does the work; people steer and approve.
- **Truly local per country.** The old one barely changed per market — not the intent, the keywords, or the writing. The new one is native in all three.
- **It writes from the product data, not just connects to it.** The old one linked the catalogue to Contentful but didn't use what was in it. With the richer new catalogue, that data is the foundation of every page.
- **It remembers and improves.** Custom instructions let us iterate, but nothing was remembered — so quality never built up. The new one learns as it goes.
- **It creates, not just tweaks.** The old one could only improve an existing page from a fixed template. The new one builds a page from scratch — creative and on-goal, to our standards.
- **It checks its own quality.** The old one leaned on people to catch weak copy. The new one checks every page — unique, relevant, on-brand — before it goes live.
- **It covers everything.** The old one did product pages. The new one does every page type, and makes sure no page that should exist is missing.
- **Small changes are easy too.** The old one only paid off for big rebuilds — for small edits it was quicker to open Contentful. The new one handles small tweaks just as easily. **The goal: never edit Contentful by hand again.**
- **It analyses and recommends.** The old one didn't analyse anything. The new one spots problems and opportunities itself and proposes the fix — which is what makes it fully agentic and always improving.

**In one line:** the old engine was a manual tool that filled product pages from templates; the new one runs itself, writes truly local content from scratch, learns over time, and finds and fixes opportunities on its own — so we never touch Contentful by hand again.

## How it works

**Niels defines everything first (Plans + Fundament). Michael (our CTO) and engineering build it. The agents then run it.** The team already exists — the only genuinely new piece is the **Content Generation Overview** (a simple to-do + status list, a Google Sheet) that says what to make and where each piece stands.

We roll out **country by country** — generate the content, check it, take it live, learn from production, improve, then the next country. **Ireland is the first.** The list of what each country should have is worked out once; we build one country at a time off it, making **only the pages that country should have**.

## What we protect

- **Quality first** — the checks decide what goes live.
- **URLs stay the same** — we change one only when we must, always with a redirect.
- **Every page a country should have, exists** — nothing silently dropped.
- **No broken links** — every old address still works (kept or redirected).

## Who does what

| Who does what | |
|---|---|
| **Define — Niels** | All the planning and definitions (Plans + Fundament). With **Cornel** for how we express the brand, an **external local-language specialist** to check each country's rules, and **Frederico** to help build the overview. |
| **Build — Michael (CTO) / engineering** | The new Contentful space + website, the page blocks in code, the tools, and the agents (the Fundament + Build phases). |
| **Run — the agents** | Writing, checking, going live, and ongoing improvement. |

## Timeline

| Phase | Target | What's done |
|---|---|---|
| **1 · Plans** | **9 Jun 2026** | content-type specs · the Overview design · the agent plan (team + QA) · Helpcenter/Blog/Wiki structure plan |
| **2 · Fundament** | **12 Jun 2026** | agent-system foundation started · tone of voice per country done · agents' deeper context · H/B/W content plan · Company pages (manual) · Contentful contract closed |
| **3 · Build** | **22 Jun 2026** | full agent system · Contentful structure · QA system · current-content pipeline — built |
| **4 · Generation** | **6 Jul 2026** | per-block content for Ireland tested, generated and improved |
| **5 · Full QA & Testing** | **8 Jul 2026** | Ireland fully optimised — content complete, flows work, monitoring works, no loose ends → **first country live** |
| *After* | — | roll out the remaining countries the same way, then continuous improvement |

> The dates depend on two things outside this plan landing on time: **the content spec** and **the new Contentful + website (Michael)**.

---

## Phase 1 — Plans · Niels · by 9 Jun

Everything defined on paper before anything is built.

- **Content-type specs** — our content model turned into a spec the system can check, starting with category pages.
- **Overview design** — the layout of the Content Generation Overview (the to-do + status list; doesn't hold content, doesn't coordinate the agents — it's the shared list of what's to do and what's done, including pages that don't exist yet).
- **The agent plan** — the full agent team, how they work together, and the QA system (all below).
- **Helpcenter / Blog / Wiki structure plan** — the page architecture for those sections: which pages exist, their URLs, how they link.

### The agent team *(defined here · built in Build)*

*Make the content:*
- **SEO Lead** — runs the team, sets priorities, signs off go-live.
- **Content Writer** — writes the content.
- **Locale Specialist** — makes content native to the market.
- **Editor-in-Chief** — owns the quality check.
- **Technical SEO Engineer** — owns the overview, the technical checks, and publishing.
- **Category Expert** — gives the writer the correct product facts.
- **Compliance & Claims** — checks legal claims before anything is published.

*Research, data, coverage & monitoring:*
- **SEO Researcher** — the keywords for each country.
- **The Analyser** — our own data (visits, orders, profit) to set page priority.
- **SEO Health Specialist** — checks every page a country should have is there, plus technical health.
- **SEO Performance Watcher** — watches traffic and rankings after launch.

*Coordination:*
- **Localization Lead** — coordinates across countries.
- **Product Owner** — turns needs into clear work and tracks delivery.
- **SEO Finance Partner** — watches cost vs value.

We define and build the whole team at once; each agent starts with a solid baseline and **gets deeper context over time** to work even better.

### How the agents work together
The **agent system** runs the order (brief → write → make native → check → publish) and passes work between agents through the Overview — the Overview is the to-do + status list, the agent system does the coordinating.

### The QA system — three checks *(defined here · built in Build)*
- **Content check** — *is the page good and on-brand?* Right structure, right keywords, correct facts, well written, original (not copied), and no two pages competing for the same keyword.
- **Coverage check** — *does every page a country should have actually exist?* Compares the should-have list to what's been made, and flags anything missing.
- **Technical check** — *is the live site healthy?* No broken links, properly indexed, fast — plus watching traffic and rankings. Reuses our existing traffic-loss monitor.

---

## Phase 2 — Fundament · by 12 Jun

The groundwork in place.

- **Agent-system foundation** — Michael starts building the base of the agent system.
- **Tone of voice per country — done** — how we write, plus each market's vocabulary, competitors and local context; UK + Ireland first, then a template for the rest (Niels, with Cornel and an external local-language specialist).
- **Agents' deeper context** — give the agents their grounding: the product-catalogue data, market knowledge, and tool access (the HelloPrint SEO MCP).
- **Helpcenter / Blog / Wiki content plan** — the editorial plan for what content fills the H/B/W structure.
- **Company pages — done** — built manually, outside the engine.
- **Contentful contract — closed.**

---

## Phase 3 — Build · Michael · by 22 Jun

The full technical build.

- **Full agent system** — every agent built.
- **Contentful structure** — the page blocks in code, set up so every country has its own content with **no fall-back**.
- **QA system** — the three checks, working.
- **Current-content pipeline** — pull our current content (organised by web address, with an old→new map) so it can be a starting point.

---

## Phase 4 — Generation · by 6 Jul

Per-block content for **Ireland** is tested, generated and improved. For each block, in order (category pages → products → themed pages → help centre → blog → wiki):

1. **Get** the brief from the Overview (keywords, page goal, country rules, old content to start from).
2. **Write** it fresh (Content Writer + Locale Specialist).
3. **Check** it; if it fails, back to step 2.
4. **Publish** the passing block to the new space.
5. **Tick** it off the list.

It improves as it runs — every failed check tightens the prompts and the rules, so fewer fail over time.

---

## Phase 5 — Full QA & Testing · by 8 Jul

**Ireland is the first country fully rolled out.** Full content optimised, all flows work, the monitoring system works, no loose ends — 100% of Ireland's pages, all checks green, every link resolves, monitoring live, signed off → Ireland goes live.

---

## After 8 July

Roll out the remaining countries the same way, one at a time (US last — different products and pages), then **keep improving**: the agents spot issues and opportunities themselves and optimise continuously.

---

## Tools the agents use

Every agent works from one shared tool set — the **HelloPrint SEO MCP** — and then gets a few **extra tools** where they add value.

### Base tools — the HelloPrint SEO MCP (shared by every agent)
One shared SEO toolkit, exposed as the **HelloPrint SEO MCP**:

- **Ahrefs** — external + internal estimated search & GEO data, for analysis, performance and technical audits.
- **Google Search Console** — our real organic search data: clicks, impressions, rankings, and technical context.
- **GSC Wizard** — a helper that adds expert context to Google Search Console analysis.
- **Specifications Website** — expert context on website specifications.
- **Screaming Frog** — website-health crawler.
- **Contentful** — the content management system.
- **Datadog** — pulls Cloudflare log data.
- **Google Analytics** — real conversion data and sessions per channel.
- **Lighthouse** — technical performance data.
- **Linear** — view, edit and create development tickets.
- **Cube** — internal performance and order data (and the hub other tools connect through).

Alongside the MCP, every agent also reads the **Content Generation Overview** and the **foundations** (the spec, tone of voice per country, country rules).

### Extra tools per agent (on top of the base)
The base covers most needs. Only a few agents need anything extra — to confirm together:

| Agent | Extra tools (to confirm) |
|---|---|
| Editor-in-Chief | A copy / originality (similarity) check |
| Category Expert | The full product catalogue / PCM |
| Compliance & Claims | Claim-verification sources (eco / legal) |
| SEO Finance Partner | Agent token / cost-usage data |
| *All other agents* | — covered by the base |

---

**Next step:** start **Phase 1 — Plans** by 9 June — the content-type specs, the Overview design, the agent plan, and the Helpcenter/Blog/Wiki structure plan.
