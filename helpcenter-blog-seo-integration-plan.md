# Helloprint Content Hierarchy & SEO Integration Plan

**Version 2.8 · 02 June 2026 · Owner: Niels Molenaar · Process: Sell Products · Status: Locked, ready for build · Timeline: ASAP**

---

Every Helloprint content model — where it lives in the CMS, where it should live, what it does for the customer, and what we do with it. Followed by the structural plan for the unified Helpcenter knowledge surface and the cannibalisation discipline that holds it together.

## Headline insight

- **Contentful is the consolidation target** for editorial and commercial content. Helpcenter migrates from Elevio; Solution & Company migrates from Webflow.
- **Platform Catalog** stays the source for factual product attributes; flows to PDPs via the Content Gateway.
- **Four properties stay native:** Recruitee (Careers), Lovable (Vereniging van het Jaar + Partner Hub), the platforms themselves (YouTube & Social). Partner Hub is an explicit exception to the Contentful consolidation because the wider Supply / Partner ecosystem is already on Lovable.
- **`/learn` is Helloprint's unified knowledge hub** — the single discovery surface that ties Blog, Wiki, and Helpcenter together for top-of-funnel informational intent.
- **Editorial trees are flat at root AND article URLs are flat too** — `/blog/{slug}`, `/wiki/{slug}`, `/helpcenter/{slug}`. No editorial parent. No category/cluster segment between tree and article. Cluster/category hub pages still exist as topical aggregators (`/blog/{cluster}/`, `/helpcenter/{category}/`) but don't own child URLs. **Only exception:** Products sub-cluster keeps depth at `/blog/product/{family}/{slug}` as a structural anti-cannibalisation signal against the PLP (section 7).

## How to read this document

- **Sections 1–3** are the *what* — scope, hierarchy model, and the 13 content buckets that make up Helloprint's content ecosystem.
- **Sections 4–13** are the *how* — URL migration, sitemap, internal linking, cannibalisation, article→commercial, the `/learn` knowledge hub, tree hub specs, schema, migration playbook and references.
- **Section 14** is the *when* — V1 action plan now + V2 steps later, with sequencing and dependencies.
- Use Google Docs **commenting** to leave feedback on any paragraph, sentence, or table cell.

---

# 1. Scope & status

## Timeline framing

All migrations and locked-in changes target **ASAP execution**. Each bucket's Build plan section carries its own dependency view. Exit criterion across the plan is universal: **migrated and ready to be commercially scaled**. Commercial optimisation work starts once migration clears.

## In scope

*"Positioning and defining" each bucket = naming where the content lives (CMS), where it should live, what customer intent it serves, and the action we take on it. Done in section 3.*

- Inventory and positioning of all thirteen content buckets — CMS today, target CMS, customer intent, action
- **Helpcenter platform migration execution** (Elevio → Contentful)
- **Solution & Company platform migration execution** (Webflow → Contentful)
- **Flat editorial article URLs** — `/blog/{slug}`, `/wiki/{slug}`, `/helpcenter/{slug}` at root. No shared editorial parent. No category/cluster segment between tree and article.
- **Cluster/category hubs remain** — `/blog/{cluster}/` and `/helpcenter/{category}/` exist as topical aggregator pages but don't own child URLs.
- **`/learn` unified knowledge hub** — single landing page that ties Blog, Wiki, Helpcenter, YouTube, and social into one discovery surface. Build new in V1.
- Blog URL migration to `/blog/{slug}` (flat) — with one exception: Products sub-cluster keeps `/blog/product/{family}/{slug}` for anti-cannibalisation
- Wiki — URL structure `/wiki/{slug}` for new content creation; existing size-page migration the only direct URL move
- Helpcenter URL restructure to `/helpcenter/{slug}` — drops both the `/faq/` segment AND the category segment
- Industry / Themed / Location **URL structure** work — optimise where inconsistent. Content optimisation & scaling deferred.
- Design Templates redirect (Canva integration removed)
- Sitemap structure changes — file split, naming, operational rules
- Indexation rules per content model — defined per bucket
- Internal linking model — comprehensive per-content-model linking patterns (section 6)
- Cannibalisation discipline — `target_keywords[]` Contentful field on editorial AND commercial entries
- Hub and category-page layout for Helpcenter (Wiki / Blog / FAQ)
- Article → commercial linking commercial guidelines
- Schema and on-page requirements

## Out of scope (referenced out)

- Commercial PDP & PLP URL changes — *PDP / PLP Requirements*
- Block 11 full spec — *PLP Requirements · Block 11*
- Sitemap technical infrastructure (multi-tier index, rules engine, hreflang in head) — *PLP Requirements · §3.4*. File structure and operational rules ARE in scope.
- Indexation governance engine implementation — *PLP Requirements · §3.3 (g-url)*. Indexation rules per content model ARE in scope.
- Industry / Themed / Location content optimisation & scaling — deferred. URL structure work IS in scope.
- Print Wiki detailed editorial taxonomy — bucket scope set here, content extension beyond sizes deferred
- Product Content / Platform Catalog content model — defined in Sebastiaan's Content System Proposal

---

# 2. Site hierarchy model

Parallel trees rooted at Home. Editorial content lives in **three flat trees** at root (`/blog/`, `/wiki/`, `/helpcenter/`) with a dedicated **`/learn` hub** as the unified discovery surface.

## Four principles

**1. Content discipline — one purpose, one CMS, no cannibalisation**
Every content model serves one distinct customer intent. Editorial and commercial content live in Contentful; factual product content lives in Platform Catalog. Cannibalisation is prevented at publish time by the `target_keywords[]` field (section 7).

**2. Site structure — flat editorial roots + unified discovery hub**
Home (`helloprint.com/{locale}/`) is the only true root. Editorial trees (`/blog/`, `/wiki/`, `/helpcenter/`) live flat at root — each owns its own URL space, no shared editorial parent. The `/learn` hub is a single landing page that unifies discovery without owning any child URLs. Commercial uses flat URLs at root because the slug IS the target keyword. Topic groups within editorial clusters are anchor-only — never URLs (except Products blog sub-clusters).

**3. Locale parity at tree level**
Every tree exists in every Helloprint locale by default. Individual articles or product entries may be locale-specific.

**4. Indexability is intentional**
Every page either earns its index status or is explicitly noindex. Sitemap inclusion is gated on human-in-the-loop meta-robots approval (per PLP Requirements §3.3).

## Structural rules

> **Three rules that drop out of the principles**
>
> **1. Commercial = flat URLs at root.** Hierarchy via breadcrumbs & internal links. The slug carries the head keyword.
>
> **2. Editorial = flat trees AND flat articles.** `/blog/{slug}`, `/wiki/{slug}`, `/helpcenter/{slug}` — articles live one segment under the tree root. Cluster/category hub pages (`/blog/{cluster}/`, `/helpcenter/{category}/`) exist as topical aggregators that filter articles by tag; they don't own child URLs. **One structural exception:** Products sub-cluster keeps the deeper path `/blog/product/{family}/{slug}` because the cluster URL itself is the structural anti-cannibalisation signal against the PLP (see section 7).
>
> **3. Standalone navigation pages = `sitemap_pages_1.xml`.** Top-level pages without taxonomic children — `/learn` hub, `/about-us`, Industry/Theme L1s, Careers/Newsroom entry-points — live in the standalone-pages sitemap. They're distinct from **Landings** (commercial PLPs L1–L4) which are part of the commercial taxonomy and live in `sitemap_landings_1.xml`.

## The trees — future state

```
Home · helloprint.com / {locale} · Contentful
│
├── Commercial            Contentful · L1 → L5 PDP · flat URLs
├── Industry / Theme      Contentful · nested + flat (parked)
├── /learn                Contentful · unified knowledge hub (single landing page, no children)
├── /blog/                Contentful · /blog/{slug} flat · /blog/{cluster}/ hubs as aggregators · /blog/product/{family}/{slug} Products exception
├── /wiki/                Contentful · /wiki/{slug} · definitional content
├── /helpcenter/          Contentful (Elevio → CF) · /helpcenter/{slug} flat · /helpcenter/{category}/ hubs as aggregators · utility URLs
├── Solution & Company    Contentful (Webflow → CF) · flat leaves at root
├── Product Content       Platform Catalog · API-fed into PDPs · no own URL
└── External              Recruitee · Lovable (VvhJ + Partner Hub) · YT/Social · off-domain governed
```

## Depth profile per tree

| Tree | L1 | L2 | L3 | L4 | L5 |
|---|---|---|---|---|---|
| **Commercial** | Category Landing | Product Landing | Product Landing | Product Landing | PDP (leaf) |
| **`/learn` hub** | Single landing page · no children (unifies discovery via internal links to editorial trees) | | | | |
| **`/wiki/`** | Wiki hub | Wiki entry (flat) | themes are visual subsections only | | |
| **`/blog/`** | Blog hub | **Article (flat — most clusters)** OR Cluster aggregator page (e.g. `/blog/artwork/`) | Article in Products sub-cluster (only) e.g. `/blog/product/booklets/best-paper-weight-for-booklets` | — | — |
| **`/helpcenter/`** | Helpcenter hub | **Help article (flat)** OR Category aggregator page (e.g. `/helpcenter/design-and-upload/`) | — | — | — |
| **Industry / Theme** | Flat leaves at root | URL structure optimisation in scope; content scaling deferred | | | |
| **Solution & Company** | Flat leaves at root | no children by design | | | |
| **Product Content** | no own URL — factual product attributes flow via Platform Catalog API into PDPs. *This is where product data is stored, not where it lives as a page*; it fuels the Commercial content layer. | | | | |

## Locale parity — Helloprint locales

en-gb · nl-nl · de-de · fr-fr · es-es · it-it · be-nl · be-fr · ie-en · se-sv · us-en

## Worked example chains

**Commercial — water bottle PDP**

```
/en-gb/ → /corporate-gifts → /drinkware-printing → /printed-bottles → /printed-water-bottles → /sky650mlrecycledplasticwaterbottle
```

**`/learn` hub**

```
/en-gb/ → /learn
```

**Wiki — Bleed**

```
/en-gb/ → /wiki → /bleed
```

**Blog — Artwork article (flat)**

```
/en-gb/ → /blog → /5-bleed-mistakes-to-avoid
```

*The Artwork cluster hub at `/en-gb/blog/artwork/` exists as a topical aggregator page listing all artwork-tagged articles, but doesn't own child URLs.*

**Blog — Products sub-cluster article (the one URL exception)**

```
/en-gb/ → /blog → /product → /booklets → /best-paper-weight-for-booklets
```

*Products sub-cluster keeps depth because the URL itself is part of the anti-cannibalisation defence against the PLP — see section 7.*

**Helpcenter — Help article (flat)**

```
/en-gb/ → /helpcenter → /adding-bleed-to-your-file
```

*The Design & upload category hub at `/en-gb/helpcenter/design-and-upload/` exists as a topical aggregator page listing all design-and-upload-tagged articles, but doesn't own child URLs.*

---

# 3. Content model overview (13 buckets)

Each bucket has Overview, Performance (where signal exists), Rules, and Build plan sub-sections.

## Bucket 01 — Commercial Pages

**Status:** Indexed · **Maintain**

### Overview

- **CMS today:** Contentful
- **CMS should live:** Contentful
- **Customer intent:** PDPs & PLPs — discover, evaluate and purchase printed products. Conversion-focused.
- **Action:** **Maintain.** Slug/URL/canonical rules governed by PDP & PLP Requirements. Product attribute content (specs, dimensions, materials) moves OUT of Contentful into the Platform Catalog (bucket 12).

### Performance

- **Business value:** Revenue surface. Drives organic traffic and 100% of conversions. Conversion-focused.
- **KPIs:** Organic sessions · Organic-attributed orders · PDP/PLP indexation coverage · Ranking distribution per cluster

### Rules

- **URL pattern:** Flat at root: `/{locale}/{slug}`.
- **Cannibalisation:** `target_keywords[]` per locale, checked cross-corpus. PLP wins ranking when conflict with FAQ.
- **Indexability:** Indexed by default. Faceted nav, pagination and noindex rules per PLP Requirements.

### Build plan

- **Sequencing:** No URL migration. Block 11 deployment + FAQ creation system rollout follow Helpcenter migration.
- **Exit criterion:** N/A — Maintain bucket.

---

## Bucket 02 — Industry / Themed / Location Pages

**Status:** Indexed · **Optimise URL structure · Retire (Location)**

### Overview

- **CMS today:** Contentful
- **CMS should live:** Contentful
- **Customer intent:** Find print solutions for a specific use case, audience or location
- **Action:** **Optimise URL structure from the start.** Redirect Location pages, change URL structure for themes/industry where inconsistent, then focus on content optimisation later.

### Rules

- **URL pattern:** Target = flat at root. Currently inconsistent — nested `/industry/{vertical}/{sub-vertical}` co-exists with flat `/event-festivals-printing`, `/wedding`. Reconcile to flat.
- **Cannibalisation:** Industry/Theme L1 is the **canonical commercial destination** for use-case keywords ("wedding stationery"). Printspiration topic anchors target editorial intent ("wedding inspiration") and link OUT to Industry/Theme.

### Build plan

- **Sequencing:** Location retirement first (pre-retirement traffic audit to preserve high-traffic pages). URL structure reconciliation in V1. Content optimisation & scaling = later workstream.
- **Risks:** Migrating URL structure on indexed industry pages without traffic loss requires careful 301 mapping.

---

## Bucket 03 — Design Template Pages

**Status:** Indexed (today) · **Redirect**

### Overview

- **CMS today:** Contentful
- **CMS should live:** N/A — redirect
- **Customer intent:** Find a ready-made design template — served by Canva integration
- **Action:** **Redirect.** Many high-value template pages have already been redirected, so current traffic is low. Canva integration is the main content focus and the Contentful template integration ends this summer.

### Rules

- **URL pattern:** Currently `/{locale}/design-templates`. Post-redirect: 301 to Canva integration entry point.
- **Cannibalisation:** Redirect is itself the cannibalisation resolution against Canva integration.

### Build plan

- **Sequencing:** Summer 2026 — end of Contentful template integration. Pre-redirect audit → 1:1 301 map → ship redirect.
- **Risks:** Low remaining traffic, so low equity at risk. Mitigation: redirect to most-specific Canva entry per template type.

---

## Bucket 04 — Helpcenter / Blog & Press

**Status:** Indexed · **Migrate URLs**

### Overview

- **CMS today:** Contentful (at `/blog/category/*`)
- **CMS should live:** Contentful, at `/blog/{slug}` (flat — article one segment under tree root). Cluster hubs (`/blog/{cluster}/`) exist as topical aggregators that filter by tag.
- **Customer intent:** Editorial perspectives — design tips, ideas, masterclasses, industry insights, sustainability stories. Absorbs Newsroom (Company cluster).
- **Action:** **Migrate URLs** to flat structure. Rebuild hub and cluster aggregator templates. 7 clusters locked. **One exception:** Products sub-cluster articles keep depth at `/blog/product/{family}/{slug}` for anti-cannibalisation (section 7).

**7 clusters:** Company · Product (sub-clustered by family) · Artwork · Printspiration · HelloAcademy · Insights · Sustainability.

> **Highest-risk migration in this plan**
> Blog & Press carries significant traffic, has many internal & external fixed links, large article volume, and complex cross-tree linking. Migration to be executed very carefully — staged rollout, comprehensive 301 mapping, link audit before cutover, monitoring window extended.

> **Press URL audit (Newsroom)**
> Press content lives within Blog: Company. Historical press URLs were previously separately hosted. Migration includes a 1:1 301 audit step (see section 12) to ensure no orphan press URLs return 404.

### Performance

- **Business value:** Highest-leverage editorial surface. Captures top-of-funnel informational intent; feeds commercial via cross-tree linking.
- **KPIs:** Organic sessions to `/helpcenter/blog/*` · Blog → PDP click-through rate · Blog-attributed orders · Ranking distribution per cluster

### Rules

- **URL pattern:** Flat: `/{locale}/blog/{article-slug}` for articles in all clusters except Products. Cluster hubs at `/{locale}/blog/{cluster}/` exist as topical aggregators. **Exception:** Products sub-cluster articles live at `/{locale}/blog/product/{family}/{article-slug}` to maintain the anti-cannibalisation URL signal vs the matching PLP.

**Cluster scope:**

| Cluster | Scope | Sub-clusters? |
|---|---|---|
| Company | Brand stories, team, press, B-Corp narrative (absorbs Newsroom) | No |
| Product | Product-specific editorial per product family | **Yes** |
| Artwork | Editorial perspectives on artwork and design | No |
| Printspiration | Visual ideas, project showcases, customer stories, trends | No |
| HelloAcademy | Instructional content — tutorials, courses, video lessons (absorbs Guides) | No |
| Insights | Industry trends, market analysis | No |
| Sustainability | Sustainability editorial — eco materials, B-Corp, circular print | No |

- **Cannibalisation:** Boundary rules in section 7. Topic groups within clusters are anchor-only, never URLs (except Products sub-clusters).
- **Indexability:** Indexed by default. Articles < 200 words noindex'd until expanded.

### Build plan

- **Sequencing:** ASAP. URL migration runs alongside Helpcenter platform migration and Wiki migration.
- **Risks:** Migration equity loss if internal links not updated wholesale. Vereniging van het Jaar inbound links updated during migration.
- **Exit criterion:** Migrated and ready to be commercially scaled — all old URLs 301'd, new sitemap submitted, Block 11 deployed on eligible PLPs.

---

## Bucket 05 — Helpcenter

**Status:** Indexed · **Platform migration done · URL migration TBD**

### Overview

- **CMS today:** Contentful (platform migration from Elevio complete)
- **CMS should live:** Contentful, at `/helpcenter/{slug}` (flat — article one segment under tree root). Category hubs (`/helpcenter/{category}/`) exist as topical aggregators that filter by tag.
- **Customer intent:** Strictly customer questions and HowTo about the Helloprint process — how to upload, how to order, how to pay, how to track. Help them complete a purchase. **Not a commercial surface.**
- **Action:** **Platform migration:** ✓ Done (Elevio → Contentful complete). **Still to do:** URL migration (`/cs/*` → `/helpcenter/{slug}`) + category aggregator pages built as topical hubs. Schema differentiates QAPage (single-question) and HowTo (step-by-step) per article — section 11.

### Performance

- **Business value:** Self-serve support that reduces tickets and helps customers complete their purchase. Process-help focus, not a commercial surface. Attribution is hard; KPIs lighter than other buckets.
- **KPIs:** Organic sessions to `/helpcenter/faq/*` · FAQ → PDP click-through · Reduction in support tickets for FAQ topics

### Rules

- **URL pattern:** Flat: `/{locale}/helpcenter/{article-slug}`. Numeric IDs dropped, descriptive slugs only. Category hubs at `/{locale}/helpcenter/{category}/` exist as topical aggregators that filter articles by category tag. Article slugs must not collide with category slugs or with utility URLs (`contact`, `quote`).

**Helpcenter categories (locked) — exist as hub aggregator pages at `/helpcenter/{category}/`:**

| Category | Process scope |
|---|---|
| Ordering | Placing and configuring an order |
| Design & upload | Preparing artwork and uploading to Helloprint |
| Payment & invoicing | Paying and getting invoices |
| Delivery & tracking | Shipping and tracking |
| Account & other | Account, password, settings, catch-all |

- **Cannibalisation:** FAQ scope is strictly platform-process. When conflict with PLP, **PLP wins ranking**. FAQ inline on PLP is truncated with "Read full answer" link to destination.
- **Indexability:** Indexed by default. Articles < 200 words noindex'd.

### Build plan

- **Sequencing:** ASAP. Platform migration off Elevio is the gating dependency.
- **Exit criterion:** All articles migrated to Contentful, old URLs 301'd, FAQ creation system live on PLPs/PDPs.

---

## Bucket 06 — Solution & Company Pages

**Status:** Indexed · **Migrate platform (V1, blocked by Contentful design)**

### Overview

- **CMS today:** Webflow
- **CMS should live:** **Contentful**
- **Customer intent:** B2B solution evaluation + brand and trust signal review
- **Action:** **V1 in scope.** Migrate Webflow → Contentful so all content sits in one CMS. **Blocked by Contentful design redesign** — the current Webflow block design needs to be redesigned for a scalable Contentful structure before migration can start. Execution sequenced after the design lands. Fix reseller locale inconsistency along the way.

### Rules

- **URL pattern:** Flat at root: `/business-solutions`, `/reseller-solutions`, `/nonprofits`, `/rfp`, `/printmanagement`, `/book-a-demo`, `/merch`, `/about-us`, `/our-culture`, `/our-promises`, `/sustainability`, `/always-a-perfect-design`.
- **Cannibalisation:** Light. `/uk/reseller-solutions` vs `/en-gb/reseller-solutions` = locale duplicate; pick one canonical and 301 the other.

### Build plan

- **Sequencing:** V1. Blocked by Contentful design redesign. Once the new scalable Contentful block design lands, migration can run in parallel with other V1 work.
- **Risks:** Migrating Webflow block design 1:1 into Contentful without redesigning produces a structure that doesn't scale. Redesign first, then migrate.
- **Exit criterion:** Contentful block design ready, pages migrated with URL parity, reseller locale fix shipped.

---

## Bucket 07 — Transactional, Legal & System Pages

**Status:** Mostly noindex · **Split & reorganise**

### Overview

- **CMS today:** Mixed — template translations in Contentful, app pages rendered by storefront, Elevio embedding for legal
- **CMS should live:** Split: system pages → **system space** (commercetools / storefront app); helpcenter-formatted utility (contact, quote) → URL fits helpcenter; legal pages → Contentful
- **Customer intent:** Complete transactional flows (system); request contact / quote (helpcenter-formatted); read legal terms
- **Action:** **Split & reorganise** into three sub-buckets. Move template translations Contentful → commercetools. Legal pages stay indexed and accessible.

> **Open question — system space rendering for contact & quote**
> Contact and quote URLs follow the helpcenter format (`/helpcenter/contact`, `/helpcenter/quote`) for UX consistency. **Can they be rendered from the system space** (i.e. not the Contentful-backed Helpcenter renderer), or must helpcenter URLs always be rendered by the Helpcenter system? Technical workstream to resolve.

### Rules

**Sub-buckets:**

| Sub-bucket | URLs | Indexability | Rendered by |
|---|---|---|---|
| **System** | `/my-account`, `/authentication`, `/basket`, `/empty` | Noindex / robots-disallowed | System space (storefront app) |
| **Helpcenter-formatted utility** | `/helpcenter/contact`, `/helpcenter/quote` | Noindex | TBD — system space or Helpcenter renderer |
| **Legal** | `/terms-and-conditions`, `/cookie-statement`, `/privacy-policy` | Indexed (minimal SEO weight) | Contentful |

- **Template translations:** Template-level translation strings move from Contentful to commercetools to align with where transactional UI is rendered.

### Build plan

- **Sequencing:** Resolve the system-space-vs-helpcenter-renderer question first (technical workstream). System pages remain noindex throughout. Legal stays as-is. Template translations move owned by commerce platform team.

---

## Bucket 08 — Careers & Jobs

**Status:** External · **Maintain**

### Overview

- **CMS today:** Helloprint Recruitee
- **CMS should live:** Helloprint Recruitee
- **Customer intent:** Find and apply for roles + employer-brand search
- **Action:** **Confirm** on-domain entry-point page exists; deep-link to Recruitee.

### Rules

- **URL pattern:** On-domain entry: `/{locale}/careers` or `/jobs` (TBD). External ATS: Recruitee.
- **Indexability:** On-domain entry indexed; Recruitee pages indexed on Recruitee's domain.

### Build plan

- **Sequencing:** Audit current footer link → confirm canonical on-domain entry-point.

---

## Bucket 09 — Vereniging van het Jaar

**Status:** External · **Maintain**

### Overview

- **CMS today:** Lovable
- **CMS should live:** Lovable
- **Customer intent:** Campaign-specific. From Helloprint's perspective: drives authority via inbound links into the Helloprint blog (which lives on the Helloprint domain).
- **Action:** **Maintain external hosting.** Ensure inbound links from VvhJ → Helloprint blog land on correct (post-migration) URLs. Direct links pass 100% equity vs. ~85–90% via 301s.

### Rules

- **URL pattern:** External domain.
- **Indexability:** Indexed on own domain.

### Build plan

- **Sequencing:** Coordinate with blog & wiki URL migration.

---

## Bucket 10 — YouTube & Social Media

**Status:** External · **v2 generation layer**

### Overview

- **CMS today:** Native platforms: YouTube, Facebook, X, LinkedIn, Instagram
- **CMS should live:** Native platforms (hosting stays). Generation layer for content production = v2.
- **Customer intent:** **YouTube is most relevant** because of HelloAcademy content — embeddable from Blog and Commercial. Other channels (FB, X, LinkedIn, IG) are top-of-funnel discovery, less internally linked.
- **Action:** Hosting remains on the native channel. Build internal linking from Blog (especially HelloAcademy, Artwork, Printspiration) and commercial PDPs to relevant YouTube videos with `VideoObject` schema. v2: generation/posting integration layer.

### Rules

- **URL pattern:** External — native platform URLs.
- **Indexability:** Indexed on native platforms.

### Build plan

- **Sequencing:** Embed policy ships v1. Generation/posting integration layer = v2.

---

## Bucket 11 — Helpcenter / Wiki

**Status:** Indexed · **Migrate URLs**

### Overview

- **CMS today:** Contentful — flat root URLs (e.g. `/nl-nl/a7-formaat`)
- **CMS should live:** Contentful — at `/wiki/{slug}` (flat root, no editorial parent) with new hub
- **Customer intent:** Strictly "what is X?" definitional content — sizes, design concepts, materials, finishing, file types
- **Action:** Mostly **new content creation**. Only existing size pages migrate URLs. **Set URL structure correctly from the start** so the taxonomy scales quickly as new entries are added. Build `/wiki/` hub.

### Performance

- **Business value:** Captures definitional informational long-tail volume. Existing size pages already generate organic traffic.
- **KPIs:** Organic traffic to `/helpcenter/wiki/*` · Wiki → PDP click-through · Coverage of "what is X" head terms

### Rules

- **URL pattern:** Flat root: `/{locale}/wiki/{slug}`. Slug = head informational keyword.
- **Strict scope:** Strictly "what is X?" definitional. No comparisons, no angles, no opinions. Comparisons live in Blog.
- **Cannibalisation:** Three-way boundary in section 7: Wiki = WHAT, FAQ = HOW, Blog = WHY. Only Wiki owns the bare concept slug.
- **Indexability:** Indexed by default. Minimum 200 words.

### Build plan

- **Sequencing:** Structure first (URL pattern + hub layout), then size-page migration, then new content creation pipeline. Parallel with Blog and FAQ migrations.
- **Exit criterion:** URL structure correct and scalable, hub live, existing size pages migrated, new content pipeline ready for taxonomy expansion (design concepts, materials).

---

## Bucket 12 — Product Content (Platform Catalog)

**Status:** Surfaces in PDPs · **Govern via Platform Catalog**

### Overview

- **CMS today:** **Platform Catalog** — managed by Platform team; supplier input via Partners Hub
- **CMS should live:** Platform Catalog
- **Customer intent:** Customers consume this content as part of the PDP — factual product attributes (specs, dimensions, materials, print specs) needed to decide. **Not a page itself** — input that fuels PDPs.
- **Action:** **Govern via Platform Catalog.** Factual product data is stored in the Platform Catalog (not Contentful), flows via Content Gateway into the PDP commercial content layer. Per Sebastiaan's Content System Proposal.

### Rules

**Two boundary heuristics:**

1. **1:1 with a catalog row or one-of-many on a page?** Row → Platform Catalog. Paragraph → Contentful.
2. **Same for every merchant or differs per merchant?** Same → Platform Catalog. Per-merchant → Merchant Catalog or Contentful.

- **Images split:** Catalog / spec shots → Platform Catalog. Marketing photography → Contentful.
- **Override boundary:** Factual Content cannot be overridden per merchant at the Platform level.

### Build plan

- **Sequencing:** Owned by Platform team. Not gating the SEO frontend, but PDP quality depends on it.

---

## Bucket 13 — Partner Hub

**Status:** External · **Maintain (exception to Contentful consolidation)**

### Overview

- **CMS today:** Lovable — `partners.helloprint.com`
- **CMS should live:** Lovable. **Explicit exception** to the Contentful consolidation: the wider Supply / Partner ecosystem (onboarding, partner-facing systems) is already built on Lovable, so the Partner Hub stays where it sits.
- **Managed by:** Supply team
- **Customer intent:** (Prospective) suppliers and partners evaluating and entering the Helloprint partner ecosystem
- **Action:** **Maintain.** Make sure the main overview pages are discoverable in organic search so partners searching the web can find us; wire up internal linking from the Helloprint domain to feed authority into the subdomain.

### Rules

- **URL pattern:** External subdomain — `partners.helloprint.com/*`. Off-domain governed.
- **Indexability:** Main overview / landing pages indexed so partners can find the Partner Hub via search. Deeper application / authenticated flows noindex.
- **Cannibalisation:** Low. Partner Hub targets supplier/partner intent — distinct from any Helloprint commercial or editorial corpus.

### Build plan

- **Sequencing:** Owned by Supply team. Not gating the SEO frontend.
- **Internal linking from Helloprint domain:**
  - **Footer** — add Partner Hub link under "Work Together" so it surfaces site-wide.
  - **Solution & Company / proposition pages** — link from relevant pages (e.g. `/business-solutions`, `/reseller-solutions`, `/printmanagement`, `/about-us`) where partner relevance fits the narrative.
  - **Blog (Company / Insights)** — inline link where editorial content references the partner ecosystem.

---

# 4. URL migration

Three editorial URL trees + one new unified hub.

## The new URL structure

```
/{locale}/learn                                ← unified knowledge hub (new build)
/{locale}/blog/                                ← blog hub
/{locale}/blog/{cluster}/                      ← cluster aggregator (7 hubs — no child URLs)
/{locale}/blog/{article-slug}                  ← blog article (flat, all clusters except Products)
/{locale}/blog/product/{family}/               ← Products sub-cluster aggregator (per product family)
/{locale}/blog/product/{family}/{article-slug} ← Products sub-cluster article (the URL exception)
/{locale}/wiki/                                ← wiki hub
/{locale}/wiki/{slug}                          ← wiki entry
/{locale}/helpcenter/                          ← helpcenter hub
/{locale}/helpcenter/{category}/               ← category aggregator (5 hubs — no child URLs)
/{locale}/helpcenter/{article-slug}            ← help article (QAPage or HowTo, flat)
/{locale}/helpcenter/contact                   ← contact form (noindex)
/{locale}/helpcenter/quote                     ← quote request (noindex)
```

**Key changes from v2.7:**

- **Article URLs go flat under tree root.** `/blog/{slug}` instead of `/blog/{cluster}/{slug}`. `/helpcenter/{slug}` instead of `/helpcenter/{category}/{slug}`.
- **Cluster/category hubs survive as topical aggregators** that filter articles by tag, but no longer own child URLs in their path.
- **One structural exception:** Products sub-cluster keeps its depth (`/blog/product/{family}/{slug}`) because the URL pattern itself is one of the strongest anti-cannibalisation signals against the matching PLP. Defended in section 7.

**Why flat:** matches modern competitor patterns (Stripe, Intercom, Notion, Mailchimp, Shopify, Canva all use flat article URLs). Brings article keyword one segment closer to root. Articles aren't locked into a single category at URL level when they span topics. Cluster/category restructuring doesn't break URLs.

## Helpcenter migration (from Elevio)

Category aggregator pages keep their slugs at `/{locale}/helpcenter/{category}/`. **Articles migrate to a flat path** at `/{locale}/helpcenter/{article-slug}` — no category segment in the article URL.

| Current | New |
|---|---|
| `/en-gb/cs` | `/en-gb/helpcenter/` |
| `/en-gb/cs/categories/84-ordering` | `/en-gb/helpcenter/ordering/` *(aggregator hub)* |
| `/en-gb/cs/categories/88-design` | `/en-gb/helpcenter/design-and-upload/` *(aggregator hub)* |
| `/en-gb/cs/categories/87-payment-and-invoice` | `/en-gb/helpcenter/payment-and-invoicing/` *(aggregator hub)* |
| `/en-gb/cs/categories/86-delivery` | `/en-gb/helpcenter/delivery-and-tracking/` *(aggregator hub)* |
| `/en-gb/cs/categories/85-general` | `/en-gb/helpcenter/account/` *(aggregator hub)* |
| `/en-gb/cs/articles/391-i-don-t-see-all-my-designs-on-the-print-proof` | `/en-gb/helpcenter/missing-designs-on-print-proof` *(flat article)* |

> **Reserved slugs at `/helpcenter/`** — `contact`, `quote`, and the five category slugs (`ordering`, `design-and-upload`, `payment-and-invoicing`, `delivery-and-tracking`, `account`) are reserved. Article slugs must avoid collision with all of these.

## Blog migration

Cluster aggregator pages keep their slugs at `/{locale}/blog/{cluster}/`. **Articles in 6 of 7 clusters migrate to a flat path** at `/{locale}/blog/{article-slug}`. **Products sub-cluster articles keep depth** at `/{locale}/blog/product/{family}/{article-slug}` (the structural exception).

| Current | New |
|---|---|
| `/en-gb/blog/` | `/en-gb/blog/` *(hub stays)* |
| `/en-gb/blog/category/artwork` | `/en-gb/blog/artwork/` *(aggregator hub)* |
| `/en-gb/blog/category/printspiration` | `/en-gb/blog/printspiration/` *(aggregator hub)* |
| `/en-gb/blog/category/booklets` | `/en-gb/blog/product/booklets/` *(Products sub-cluster aggregator)* |
| `/en-gb/blog/category/bleed` | 301 → `/en-gb/wiki/bleed` |
| *Existing article in Artwork cluster (e.g. `5-bleed-mistakes-to-avoid`)* | `/en-gb/blog/5-bleed-mistakes-to-avoid` *(flat — cluster carried by tag, not URL)* |
| *Existing article in Products/Booklets sub-cluster* | `/en-gb/blog/product/booklets/best-paper-weight-for-booklets` *(keeps depth, exception)* |
| *Any `/blog/category/{topic}` not above* | 301 to Wiki if topic exists in Wiki, else to relevant blog cluster aggregator |

> **Article slug collision rules** — article slugs must not collide with cluster slugs (`artwork`, `printspiration`, `company`, `product`, `helloacademy`, `insights`, `sustainability`). The `product` slug is also a reserved path prefix for the Products sub-cluster.

## Wiki migration

| Current | New |
|---|---|
| `/nl-nl/a7-formaat` | `/nl-nl/wiki/a7-formaat` |
| `/nl-nl/c6-envelop-formaat` | `/nl-nl/wiki/c6-envelop-formaat` |
| *(new — hub)* | `/nl-nl/wiki/` |

## `/learn` hub — new build

Single landing page per locale at `/{locale}/learn`. No content migration; built fresh per section 9 spec. Lives in `sitemap_pages_1.xml` alongside other standalone navigation pages.

## Locale slug translation

| Slug | en-gb / ie-en / us-en | nl-nl / be-nl | de-de | fr-fr / be-fr | es-es | it-it | se-sv |
|---|---|---|---|---|---|---|---|
| `/learn` | `/learn` | `/leren` | `/lernen` | `/apprendre` | `/aprender` | `/imparare` | `/lara` |
| `/blog` | `/blog` | `/blog` | `/blog` | `/blog` | `/blog` | `/blog` | `/blog` |
| `/wiki` | `/wiki` | `/wiki` | `/wiki` | `/wiki` | `/wiki` | `/wiki` | `/wiki` |
| `/helpcenter` | `/helpcenter` | `/helpcentrum` | `/hilfecenter` | `/centre-d-aide` | `/centro-de-ayuda` | `/centro-assistenza` | `/hjalpcenter` |

Blog and Wiki stay universal across locales (the tokens "blog" and "wiki" are widely-understood loanwords with consistent SEO value across markets). Learn and Helpcenter translate. Decision rationale: translation adds local-language SEO weight where the term genuinely varies; preserving English where the term is already universal avoids fragmenting brand recall.

## Slug & URL conventions

| Rule | Value |
|---|---|
| Casing | Lowercase only. Capitalised requests 301 to lowercase. |
| Word separator | Hyphen `-`. |
| Trailing slash | With slash for category/hub. Without for leaves. |
| Max slug length | 60 characters per segment. |
| Numeric IDs | Never. |
| Locale handling | Slugs translated per locale. |
| Locale root | Bare `helloprint.com/` geo-redirects; root excluded from indexing. |
| Locale parity | Per tree, not per article. |

---

# 5. Sitemap architecture

Six sitemap files per locale, on top of the canonical technical spec in PLP Requirements §3.4.

## Structure

### Design principle

Each sitemap isolates URLs sharing **indexation behaviour at meaningful scale**. Two splits earn their keep:

- **Commercial:** Landings (L1–L4) vs. PDPs (L5). Different schema, cadence, volume, and PDP indexation drop-off.
- **Editorial:** One sitemap per tree (Blog / Wiki / Helpcenter). Different schemas and cadences.

Within each editorial tree, hub + categories + articles live together — the hub-vs-articles split is structural-only and doesn't add observability.

### File structure

```
sitemap.xml                              ← per-locale index
├── sitemap_landings_1.xml               ← Commercial L1–L4 (all PLPs / landings)
├── sitemap_products_1.xml               ← Commercial L5 / PDPs (leaves)
├── sitemap_blog_1.xml                   ← Blog hub + 7 clusters + Products sub-clusters + articles
├── sitemap_wiki_1.xml                   ← Wiki hub + entries
├── sitemap_helpcenter_1.xml             ← Helpcenter hub + 5 categories + articles
└── sitemap_pages_1.xml                  ← /learn hub + Solution & Company + Industry/Theme L1s + Careers/Newsroom entry-points
                                              (standalone navigation pages — distinct from Landings which are commercial PLPs)
```

> **"Pages" vs "Landings" — terminology clarification**
>
> `sitemap_landings_1.xml` holds commercial Product Listing Pages (PLPs) L1–L4. These are part of the commercial taxonomy and drive conversion.
>
> `sitemap_pages_1.xml` holds standalone navigation pages without taxonomic children: the `/learn` hub, Solution & Company pages, Industry/Theme L1s, Careers/Newsroom entry-points.
>
> **Note on crawler behaviour:** Google and Bing do *not* differentiate sitemap files by filename — they crawl every URL listed regardless of which file. The "Pages" vs "Landings" naming is a **human observability concern** (how easily our team can diagnose indexation per content type), not a crawler concern. Naming inherited from PLP §3.4 for human consistency with the canonical spec; rename in v2 if observability proves harder than expected.

### What goes in each editorial sitemap

**`sitemap_wiki_1.xml`**
- `/wiki/` — wiki hub
- `/wiki/{slug}` — every Wiki entry
- Low churn (definitional, rarely changes). Will likely never need to shard.

**`sitemap_blog_1.xml`**
- `/blog/` — blog hub
- `/blog/{cluster}/` — 7 cluster pages
- `/blog/product/{family}/` — Products sub-cluster pages
- `/blog/{cluster}/{slug}` — every Blog article
- Highest volume; medium-to-high churn. Shards via `_2`, `_3` when crossing 50,000 URLs.

**`sitemap_helpcenter_1.xml`**
- `/helpcenter/` — helpcenter hub
- `/helpcenter/{category}/` — 5 category pages
- `/helpcenter/{category}/{slug}` — every help article
- Medium churn (process updates).

### The `/learn` hub URL

Lives in `sitemap_pages_1.xml` alongside other flat navigation entry-points (`/about-us`, etc.). The `/learn` hub is a single landing page with no child URLs — its job is internal linking to the three editorial trees, plus social, YouTube, and curated content. Full spec in section 9.

## Inheritance from PLP Requirements §3.4

### Multi-tier index structure

- **Master sitemap index** at `helloprint.com/sitemap.xml`. Lists every active per-locale sitemap index. Declared in `robots.txt`.
- **Per-locale sitemap index** at `helloprint.com/{locale}/sitemap.xml`. Lists the six type-specific sitemaps.
- **Type-specific sitemaps** — the six files documented above.

### Active locale reconciliation

A per-locale sitemap index ships only if the locale has at least one approved `index, follow` URL.

## Mechanics

### Rules-driven inclusion / removal (§3.3 g-url)

- **Rule SITEMAP-IN** — URL enters the sitemap autonomously when meta-robots evaluates to `index, follow`. **No human-in-the-loop blocker for ADDING individual URLs** — the page auto-enters the sitemap and serves immediately. Review happens after the fact (see "Daily report" below).
- **Rule SITEMAP-OUT** — URL leaves the sitemap on a `noindex` flip, URL deletion, or new redirect entry. If a previously approved URL was rejected in review, the next sitemap regeneration removes it.

### Daily report — review without blocking

After every sitemap generation (daily 03:00 CET), an end-of-day report fires to the content team listing every new URL added that day and every URL removed. The report:

- Stays in the report queue every single day until the content team marks the URL **approved** or **rejected**.
- If **rejected** → the next sitemap regeneration removes the URL (via Rule SITEMAP-OUT triggered by an editorial noindex flip).
- If **approved** → drops off the report queue. The URL was already serving from the moment it entered the sitemap, so approval is confirmation, not gating.
- **Escalation:** pages stuck in the report queue beyond a defined threshold (e.g. 7 days) escalate to other systems or people, ensuring no URL goes unreviewed indefinitely while it's already serving.

### Sitemap entry format

- `<lastmod>` emitted on every entry. **For editorial content (Wiki / Blog / FAQ):** most recent of content-block change or meta-robots flip. **For commercial PDPs:** add price-driven cache invalidation when product data changes meaningfully (per PLP §3.4 — debated whether this should trigger lastmod; included for catalog freshness). Never crawl time.
- `<changefreq>` and `<priority>` **not emitted**. Google ignores them.
- Hreflang lives in the page's `<head>`, **NOT** in the sitemap (per PLP §3.4B).

### Regeneration cadence

- Daily backstop regen at 03:00 CET.
- Event-triggered regen on Contentful publish, meta-robots approval flip, URL deletion, price-driven cache invalidation.

### Submission

Master sitemap index registered with Google Search Console (GSC) and Bing Webmaster Tools. One-time submission; subsequent updates picked up via daily regen + lastmod signals.

### Other operational rules

- Shard suffix `_1` reserved. Files > 50,000 URLs shard to `_2`, `_3`…
- Contact/quote pages are noindex — excluded from all sitemaps.
- Image sitemap entries deferred to v2 per PLP §3.4.

## Monitoring

Three complementary alerts inherited from PLP §3.4 — applied across all six sitemaps:

1. **Drop-off alert.** Any URL in yesterday's sitemap but not today's is flagged in a daily Google Sheet export to the SEO Lead. Payload: URL, locale, previous and current meta-robots state, likely cause.
2. **Post-regen sitemap crawler.** After every regen, crawler walks the master sitemap index and every per-locale sitemap. Checks each URL for: HTTP status; actual meta-robots header value vs. Contentful's stored value (flag drift); canonical URL emitted by the storefront (cross-checked against the URL being crawled); hreflang block presence.
3. **Stale-content alert.** Any URL with `lastmod` > 90 days triggers an optimisation review in a weekly digest grouped by locale and content type.

## Generation guardrails — block sitemap serving on suspicious change

Most individual URL additions auto-publish without blocking (see "Daily report" above). But three categories of change DO block sitemap serving until a human approves — these protect against bulk anomalies and missing critical pages:

- **5%+ increase in one run.** If a regenerated sitemap adds more than 5% URLs vs. the previous version (per file), **block**: the new sitemap is held and not served until the SEO Lead approves. Prevents accidental mass URL injection.
- **5%+ decrease in one run.** If a regenerated sitemap removes more than 5% URLs vs. the previous version (per file), **block** the same way.
- **Top 100 per locale missing.** Each locale has a manually maintained **Top 100 list** of must-have PDPs/PLPs (representative across product families — e.g. `/standardflyers`, `/banners`, `/spectruma5hardcovernotebook`, plus equivalents per product line). If any URL from the Top 100 is missing from the regenerated sitemap, **block**. SEO Lead maintains each locale's Top 100 quarterly.

All three guardrails sit between regeneration and serving. When triggered, the previous sitemap stays live until approval.

---

# 6. Internal linking rules

Per-content-model linking patterns — outbound and inbound, mechanisms, rules. Keyword discipline (cannibalisation) is governed in section 7.

> **Two distinct "help" surfaces — disambiguation**
>
> **Helpcenter articles (bucket 05)** — standalone help articles at `/helpcenter/{slug}` (flat). Customer-process focused (FAQ + HowTo schema). Treated as editorial content.
>
> **FAQ content block** — a UI element on commercial pages (PLPs, PDPs, industry/theme pages, sometimes solution & company). Contains Q&A specific to that page. Each Q&A may link to its Helpcenter article destination via "Read full answer →" when relevant. The block is governed by the FAQ creation system (bucket 01).
>
> Throughout this section, "Helpcenter" refers to the destination tree (`/helpcenter/{slug}` flat articles + `/helpcenter/{category}/` aggregator hubs); "FAQ block" refers to the on-page UI element on commercial pages.

## Five linking principles

**1. Editorial articles link to commercial where contextually relevant**
Blog and FAQ articles typically carry at least one inline contextual link to a relevant PDP/PLP, because they sit closer to commercial intent. Wiki entries link to commercial *only when the concept directly relates to a product* — pure definitional content (e.g. "What is bleed") doesn't need a forced commercial link; cross-tree linking to Blog and FAQ is sufficient. Article → commercial guidelines in section 8; cross-tree linking is the universal pattern (principle 2).

**2. Cross-tree linking is mandatory — Wiki ↔ Blog ↔ FAQ for any single topic**
For any topic with multiple content surfaces (e.g. "bleed" has a Wiki entry, multiple Blog articles, and an FAQ entry), each surface links to its two siblings. Six link directions per topic.

**3. Commercial pages receive editorial, return only via Block 11**
PDPs and PLPs receive inbound links from editorial freely. Outbound linking from commercial to editorial happens ONLY through governed mechanisms: Block 11 (Blog teaser, per PLP Requirements) and FAQ creation system (truncated FAQ inline with link to destination). No inline commercial-body links to editorial outside these mechanisms.

**4. Topic groups are anchor-only; canonical destinations live at Industry/Theme L1**
Blog cluster aggregator pages have anchor subsections per topic (e.g. `/blog/printspiration/#weddings`) — never URLs. Each anchor subsection links OUT to the matching Industry/Theme L1 (`/wedding`) as the canonical commercial destination. Prevents anchor cannibalisation against Industry/Theme.

**5. Relevance over count — avoid spam**
No hard "min 1, max N" rules on most internal linking. Internal links exist where they are *highly relevant* for the reader. A Wiki entry on "bleed" doesn't need a forced commercial link if no specific product is meaningfully related. A FAQ on a generic process doesn't need a forced Blog link if no Blog article adds context. The discipline is editorial judgment, not link counts. Spammy outbound or inbound linking weakens authority signals — relevance wins.

## The Wiki / Blog / FAQ triangle — six link directions per topic

```
            WIKI
        (WHAT is X?)
          /     \
         /       \
        /         \
       /           \
      /    PDP /    \
     /     PLP      \
    /     (BUY)      \
   v        ↑         v
  BLOG  ←——————→   FAQ
 (WHY)             (HOW on HP)
```

For every topic, six cross-tree link directions: Wiki↔Blog, Wiki↔FAQ, Blog↔FAQ. Plus all three → commercial. Editorial returns are governed (Block 11 only).

## Per content model — internal linking patterns

For each content model: outbound links it sends, inbound links it receives, and the mechanism behind each.

### 01 — Commercial Pages (PDPs / PLPs)

*Customer is in buying mode — page must convert. Editorial links are governed by Block 11 + FAQ creation system; no free-form editorial links from commercial body content.*

**Outbound**

| Target | Mechanism | Rule |
|---|---|---|
| Blog | Block 11 (Blog teaser) | All PLPs. PDPs only when ranking benefit or extreme relevance — top 100 per market as test ceiling. Avoid spam. |
| Helpcenter FAQ | FAQ block (UI element) with "Read full answer →" link | FAQ block on the commercial page surfaces relevant Q&A. When the answer needs the full detail (Helpcenter destination), link via "Read more". Linked Q&A reflects a specific process for that product. |
| Wiki | Inline editorial in specific content blocks centred on the definition | Only where the Wiki concept is highly relevant to the page (e.g. /silverfoilbusinesscards links to /wiki/foil-printing). General concepts like "bleed" usually don't earn a commercial-body link. Also surfaceable from design-guidelines content blocks. |
| Related commercial pages | "Customers also viewed", "Similar products", cross-sell modules | Driven by product taxonomy and cross-sell logic. Links to relevant PLPs and complementary PDPs. |
| Breadcrumbs | Hardcoded UI | Home → Category Landing → Product Landing → PDP. BreadcrumbList schema. |

**Inbound**

| Source | Mechanism | Rule |
|---|---|---|
| Blog articles | Inline editorial + end-of-article Featured products block | Where contextually relevant; not a hard count rule. Section 8 commercial guidelines apply. |
| Helpcenter FAQ entries | Inline editorial | Where the customer journey leads naturally to a commercial page. No hard count. |
| Wiki entries | Inline editorial | Only when the concept is product-specific (e.g. silver foil → silver-foil products). Not for generic concepts. |
| Industry/Theme L1 | Featured products grid + extended Block 11 | Industry pages are commercial too — surface theme-relevant products prominently. |
| Solution & Company | Inline editorial | Occasionally, where proposition copy needs a specific commercial example. Often points to `/all-products` rather than specific PLPs/PDPs. |
| Homepage | Hardcoded blocks + header USPs | Featured commercial blocks and category surfacing in the global header. |
| Footer / global nav | Hardcoded UI | Category landings reachable from header mega-nav and footer. |

### 02 — Industry / Themed / Location L1 Pages

*Audience-segmented landings closer to conversion than blog. Heavy commercial linking allowed; editorial linking via extended Block 11.*

**Outbound**

| Target | Mechanism | Rule |
|---|---|---|
| Commercial PDPs/PLPs | Featured products grid + inline editorial | Surface products relevant to the theme/industry use case. Prefer linking to existing standard PLPs/PDPs over creating theme-specific URLs. |
| Blog | Extended Block 11 | Tag-matching extended in two directions: theme-tagged articles AND product-relevant-to-theme articles. |
| FAQ block (UI element) | FAQ block on the industry page | Theme-relevant Q&A surfaces inline. Linked to Helpcenter FAQ destination via "Read full answer" only when customer needs the full process detail. |
| Wiki | Inline editorial | Sparingly — only where a Wiki concept is directly relevant to the theme. |

> **Theme-specific URLs vs. standard URLs — rule**
> Create theme-specific product URLs (e.g. `/wedding-business-cards`) only when search volume justifies a dedicated indexable page. Otherwise, surface theme-specific content as a block on the Industry/Theme page itself and link to the standard commercial URL (e.g. `/business-cards-printing`). Avoids URL proliferation that dilutes equity.

**Inbound**

| Source | Mechanism | Rule |
|---|---|---|
| Blog Printspiration topic anchors | Inline editorial | **Canonical commercial destination.** Every Printspiration topic anchor (#weddings, #festivals, etc.) links to the matching Industry/Theme L1. |
| Other Blog clusters | Inline editorial | Where a Blog article is theme-relevant. |
| Commercial pages (content blocks) | Inline content block | When a theme/industry is extremely relevant to the commercial page. |
| Footer / global nav | Hardcoded UI | "Solutions for your industry" footer module surfaces all Industry L1s. |

### 03 — Design Templates

*Sunsetting via 301 redirect to Canva integration. No active linking pattern for v1.*

### 04 — Helpcenter / Blog & Press

*Highest-volume editorial surface. Every Blog article links to Wiki + FAQ + commercial. Cluster pages surface comprehensive topic groups with cross-references.*

**Outbound — from a single Blog article**

| Target | Mechanism | Rule |
|---|---|---|
| Wiki | Inline editorial | 1+ inline link to the relevant Wiki entry ("Not sure what X is? See definition"). |
| FAQ | Inline editorial | 1+ inline link to the relevant FAQ entry ("How to do X on Helloprint"). |
| Commercial PDP/PLP | Inline editorial + automated Featured Products block | **Required.** Min 1, max 3 inline (section 8). Plus automated end-of-article tag-driven Featured Products block. |
| Other Blog articles (within cluster) | Tag-driven Related Articles module | Default 4 related articles, end of body. Tag-driven from V1 (automation layer in V1 — section 14). |
| Industry/Theme L1 | Inline editorial | For Printspiration articles specifically — every topic anchor on the cluster page links to the matching Industry/Theme L1. |

**Outbound — from Blog cluster page**

| Target | Mechanism | Rule |
|---|---|---|
| All articles in cluster | Full grid, grouped by topic | Comprehensive — every article tagged with cluster appears, no pagination, grouped by topic via tags (section 10). |
| Wiki + FAQ cross-references per topic group | Hardcoded UI block | Each topic group on the cluster page shows the matching Wiki entry + matching FAQ entry as supporting cards. |
| Sibling Blog cluster pages | Footer module | "Browse other clusters" surfaces all 7 clusters. |
| Industry/Theme L1 (Printspiration only) | Anchor subsection CTA | Each topic anchor (#weddings, etc.) links to the matching Industry/Theme L1. |

**Inbound**

| Source | Mechanism | Rule |
|---|---|---|
| Commercial PLPs | Block 11 | All PLPs carry Block 11 with tag-driven Blog cards. |
| Commercial PDPs (selected) | Block 11 | Up to top 100 per market as a test ceiling, OR highly specific PDPs with a directly relevant Blog article. Not a must — only where ranking benefit exists or relevance is extreme. Avoid spam. |
| FAQ blocks on commercial pages | Inline content block link | FAQ content blocks on commercial pages can link to a relevant Blog article when the answer would benefit from extended editorial perspective. More common than Helpcenter-FAQ-to-Blog (below). |
| Helpcenter FAQ entries | Inline editorial | Only when extremely relevant for that specific FAQ. Not a hard rule. Same restraint as Wiki below. |
| Industry/Theme L1 | Extended Block 11 | Theme-tagged + product-relevant-to-theme. |
| Wiki entries | Inline editorial | Only when a relevant Blog article adds clear context (e.g. perspective, common mistakes). No hard rule. |
| Solution & Company | Inline editorial | Sustainability page → Blog Sustainability; About → Blog Company. Light frequency. |
| Footer / global nav | Hardcoded UI | Top-right Helpcenter link → Helpcenter hub → Blog hub. |
| Vereniging van het Jaar (external) | External backlinks | Specifically created blogs around VvhJ topics, hosted on Helloprint domain. Updated to new URLs during migration. |

**Products sub-cluster pages** follow the same pattern but with editorial/commercial discipline (80/20 ratio) per section 7.

### 05 — Helpcenter / FAQ

*Customer is solving a Helloprint platform problem. FAQ entries are short Q&A; links are focused and minimal.*

**Outbound — from a single FAQ entry**

| Target | Mechanism | Rule |
|---|---|---|
| Transactional flow (system pages) | Inline CTA | **Primary.** Most FAQ entries help customers complete a Helloprint process — links to the matching flow (my-account, basket, /helpcenter/contact, /helpcenter/quote, etc.) are the main outbound. |
| Wiki | Inline editorial | Where highly relevant for definitional context. Not a hard rule — many Helloprint-specific processes don't have a print-related definition to link to. |
| Blog | Inline editorial | Where a Blog article adds clear perspective. Not a hard rule. |
| Commercial PDP/PLP | Inline editorial | Where the FAQ leads naturally to commercial intent. Not a hard rule — many process FAQs don't need a commercial link. |
| Other FAQ entries (same category) | Related Questions module | Tag-driven within-category, automated from V1. |

**Outbound — from FAQ category page**

| Target | Mechanism | Rule |
|---|---|---|
| All FAQs in category | Full list, grouped by topic | Comprehensive, no pagination, grouped by tag. |
| Wiki + Blog cross-references per topic | Hardcoded UI block | Each topic group surfaces matching Wiki entry + Blog articles as supporting cards. |
| Sibling FAQ categories | Footer module | "Browse other categories" surfaces all 5. |

**Inbound**

| Source | Mechanism | Rule |
|---|---|---|
| Commercial PDPs/PLPs | FAQ creation system (truncated inline) | FAQ surfaced on PLP/PDP with first 1–2 sentences + "Read full answer →" link. |
| Wiki entries | Inline editorial | Wiki → FAQ for "how to do this on Helloprint". |
| Blog articles | Inline editorial | Blog → FAQ for procedural follow-up. |
| Footer / global nav | Hardcoded UI | Top-right Helpcenter link + footer "Resources" section. |

### 06 — Solution & Company Pages

*B2B and brand-narrative pages. Light editorial linking; mostly outbound to commercial proposition pages.*

**Outbound**

| Target | Mechanism | Rule |
|---|---|---|
| Contact / Quote | CTA buttons | **Primary outbound.** Solution & Company pages drive customers to contact / quote frequently as the conversion path for B2B propositions. |
| General Helloprint pages | Inline editorial | Often links to broad surfaces like `/all-products` rather than specific PDPs/PLPs — these pages are broader proposition pages, not commercial pages themselves. |
| Commercial PDPs/PLPs | Inline editorial + product showcases | Occasionally — only when the proposition specifically references a commercial offering. Less frequent than other outbound. |
| Blog (Company / Sustainability / Insights) | Inline editorial | Occasionally, where editorial supports the brand narrative. Not a frequent outbound. |

**Inbound**

| Source | Mechanism | Rule |
|---|---|---|
| Footer (every page) | Hardcoded UI | "Who We Are" + "Work Together" footer columns. |
| Blog Company / Sustainability / Insights | Inline editorial | Editorial content references brand-positioning pages. |

### 07 — Transactional, Legal & System Pages

*Noindex transactional flows + indexed legal pages. Not SEO surfaces themselves but receive many inbound links from editorial and commercial where the customer needs to take a process action.*

**Outbound**

- System pages, contact, quote — link onward via hardcoded UI (CTA flows, confirmation paths). No SEO outbound linking.
- Legal pages — minimal outbound, mostly to other legal pages.

**Inbound — significant**

| Source | Target | Mechanism |
|---|---|---|
| Commercial PDPs/PLPs | /helpcenter/contact, /helpcenter/quote | CTA buttons + inline contextual links — common process for customers asking about pricing or custom orders. |
| Industry/Theme pages | /helpcenter/contact, /helpcenter/quote | "Get a quote for your event" CTAs. |
| Solution & Company pages | /helpcenter/contact, /helpcenter/quote | Primary outbound from B2B proposition pages. |
| Helpcenter FAQ entries | /helpcenter/contact, /my-account, /helpcenter/quote | Primary outbound — FAQs help customers complete a process and link to the relevant transactional flow. |
| Wiki entries | /my-account, /helpcenter/contact | Occasionally — when a Wiki concept ties to a self-service action (e.g. "How invoicing works" → /my-account). |
| Blog articles | /helpcenter/contact, /helpcenter/quote | Where the article specifically guides the customer to start a process. |
| Header / footer / global nav | All transactional + legal pages | Hardcoded UI. |

### 08 — Careers & Jobs

*External ATS (Recruitee). On-domain entry-point page captures employer-brand search.*

**Outbound (on-domain entry-point)**
- → Recruitee (external) — deep-link to roles listing
- → Solution & Company "About us" + "Our culture" for context

**Inbound**
- ← Footer (every page)
- ← Blog Company cluster — where careers/team stories are referenced
- ← Social media accounts and posts — LinkedIn especially, drives candidate traffic

### 09 — Vereniging van het Jaar (external)

*External campaign site. Helloprint's interest = inbound backlinks from VvhJ into Helloprint blog.*

**Outbound (from VvhJ → Helloprint)**
- VvhJ blog content links to Helloprint blog articles (managed externally; updated to new URLs during migration)

**Inbound (from Helloprint → VvhJ)**
- Homepage commercial content block when actively promoting VvhJ (not standard)
- From other Helloprint blogs back to VvhJ where editorially relevant
- Footer/about reference (light)

### 10 — YouTube & Social

*External platforms. Embed pattern brings video into Helpcenter articles; native platforms drive top-of-funnel awareness.*

**Outbound (on-domain articles → YouTube)**
- YouTube videos embedded in HelloAcademy / Artwork / Printspiration articles with `VideoObject` schema + transcript
- Embedded on commercial PDPs/PLPs when video is highly relevant and high quality (e.g. product demo)
- YouTube channel link in footer

**Inbound (from social → Helloprint)**
- Social posts deep-link to PDPs, blog articles, Industry/Theme L1s
- YouTube descriptions link to relevant blog articles + commercial pages

### 11 — Helpcenter / Wiki

*Definitional reference content. Each Wiki entry is concise; cross-tree linking concentrated at end of body or in a "Learn more" callout.*

**Outbound — from a single Wiki entry**

| Target | Mechanism | Rule |
|---|---|---|
| Helpcenter FAQ | Inline editorial | **Primary** cross-tree link. Where a Helpcenter FAQ explains a Helloprint process tied to the concept. Not a hard rule. |
| Blog | Inline editorial | **Primary** cross-tree link. Where a Blog article adds perspective on the concept. Not a hard rule. |
| Commercial PDP/PLP | Inline editorial | **Secondary.** Only when the concept is highly product-specific (e.g. /wiki/silver-foil → silver-foil PDPs). Generic concepts like /wiki/bleed don't need forced commercial links. |
| Related Wiki entries | Tag-driven Related Concepts module | Where conceptually related, automated from V1. |

**Outbound — from Wiki hub**

| Target | Mechanism | Rule |
|---|---|---|
| All Wiki entries grouped by theme | Theme-grouped grid | Visual subsections (Sizes, Design concepts, Materials, Finishing, File types). |
| Blog cluster anchors | Per-theme cross-reference card | "Editorial perspectives on [theme]" → /blog/artwork/#design. |
| Helpcenter category anchors | Per-theme cross-reference card | "Helpcenter articles on [theme]" → /helpcenter/design-and-upload/. |

**Inbound**

| Source | Mechanism | Rule |
|---|---|---|
| Blog articles | Inline editorial | Where the concept is highly relevant to the article. No hard rule. |
| Helpcenter FAQ entries | Inline editorial | Where the concept clarifies the FAQ. No hard rule. |
| Commercial PDPs / design guidelines content blocks | Inline editorial in specific content blocks | From product-specific design guidelines blocks on commercial pages (e.g. silver foil PDP → /wiki/foil-printing). Avoid spammy linking. |
| Footer / global nav | Hardcoded UI | Top-right Helpcenter link → Helpcenter hub → Wiki hub. |

All inbound is relevance-gated. Inbound from design guidelines and other editorial sources is welcome but must be highly relevant — spammy linking weakens authority signals.

### 12 — Product Content (Platform Catalog)

*Backend factual content. No direct linking surface — factual attributes flow into PDPs via Content Gateway and then participate in PDP linking patterns above.*

## Cross-tree linking grid (editorial reference template)

Primary and secondary linking targets per content surface. "Primary" = where the surface most often links out to; "Secondary" = additional contextual targets where relevant. All linking is relevance-gated (principle 5).

| Source | Primary targets | Secondary targets |
|---|---|---|
| Blog: Company | Solution & Company pages | — |
| Blog: Product / {family} | Matching PLP/PDP | Parent commercial L1 + Wiki: Materials |
| Blog: Artwork | Wiki: Design concepts + Helpcenter FAQ: Design & upload | Design-heavy PDPs & PLPs |
| Blog: Printspiration | Industry/Theme L1 page + occasion-relevant PDPs | Wiki: Sizes, Materials |
| Blog: HelloAcademy | Helpcenter FAQ + Wiki hub + YouTube | Relevant PDPs / PLPs (e.g. Design Services PLP) |
| Blog: Insights | Solution & Company pages | Recruitee / Jobs entry-point |
| Blog: Sustainability | Recycled/eco PDPs & `/corporate-gifts` | Solution: Sustainability |
| FAQ: Ordering | Transactional flows: basket, checkout, /my-account | Wiki + Blog: HelloAcademy / Artwork (where relevant) |
| FAQ: Design & upload | Transactional flows: upload tool, /helpcenter/quote, /helpcenter/contact | Wiki: Design + Blog: Artwork |
| FAQ: Delivery & tracking | Transactional flows: /my-account (order tracking) | Wiki + Blog (where relevant) |
| FAQ: Payment & invoicing | Transactional flows: /my-account (invoices), /helpcenter/quote | Wiki + Blog (where relevant) |
| FAQ: Account & other | Transactional flows: /my-account, /helpcenter/contact | Wiki + Blog (where relevant) |
| Wiki: Sizes | Helpcenter FAQ + Blog: Artwork / Product | Format-specific PDPs (where directly relevant) |
| Wiki: Design concepts | Helpcenter FAQ: Design & upload + Blog: Artwork | Design-heavy PDPs (only when concept is product-specific, e.g. silver foil) |
| Wiki: Materials | Helpcenter FAQ + Blog: Product / Sustainability | Material-specific PDPs (only when concept is product-specific) |

## Global navigation patterns

### `/learn` top-right link

Static link to `/learn` on every page (header top-right). Universal entry-point to the unified knowledge hub, which then routes onward to Blog, Wiki, Helpcenter, YouTube, and social. Context-aware widget = v2 backlog. Full hub spec in section 9.

### Footer modules

- **Who We Are** — About, Culture, Promises, Sustainability, Blog
- **Our Products** — Top commercial L1s
- **Work Together** — B2B Solutions, Reseller, RFP, Print Management, Book a Demo, Partner Hub
- **Resources & Support** — Learn, Blog, Wiki, Helpcenter, Contact, Quote
- **Social Media** — YouTube, Facebook, X, LinkedIn, Instagram

### Breadcrumbs (every page except Home)

Rendered visibly + shipped as `BreadcrumbList` JSON-LD. Format: Home → [Path segments] → Current page.

### Mega-nav (header)

Product taxonomy mega-menu reachable from header. Lists all commercial L1s + featured products per category.

---

# 7. Cannibalisation rules

Keyword discipline that keeps the unified Helpcenter from competing with itself or with commercial. Enforced via a Contentful field at publish.

## Definition

Cannibalisation = two indexable pages targeting the same designated target keyword (per locale).

## The Contentful field — `target_keywords[]`

Every indexable Contentful entry — Wiki, Blog article, FAQ, Blog cluster page, FAQ category page, commercial PDP, commercial PLP, Industry/Theme L1, Solution & Company page — carries a required field: **`target_keywords[]`**, per locale.

- **Required at publish.** Empty field blocks publish.
- **Per locale.** Each locale variant carries its own keyword list.
- **Multi-value, uncapped.** If relevant, it's relevant.
- **Lives on commercial too.** Not just editorial — PDPs, PLPs, Industry/Theme, Solution & Company all carry this field so the cross-content-type check covers the full corpus.

> **v1 prerequisite — commercial target_keywords[] field**
> The `target_keywords[]` field must exist on commercial Contentful entries (PDPs, PLPs, Industry/Theme, Solution & Company) for the cross-content-type cannibalisation check to cover the full corpus. If this field doesn't already exist on commercial entries, building it is a v1 prerequisite — Contentful schema work owned by the commerce platform team. Tracked in section 13 References.

## Cross-content-type check

When a new entry publishes or a target keyword changes, the system validates against the entire indexable corpus (commercial + editorial + industry/theme + solution & company).

## Enforcement — soft warning, editor review

1. Writer sees a **soft warning**: "This keyword is also targeted by [list]."
2. Writer can resolve or request **editor override** with justification.
3. Editor reviews; approve or reject back to writer.

## Resolution recommendations (to content team)

| Action | When to recommend |
|---|---|
| **Merge** | Same primary keyword, same angle — combine into one canonical version |
| **Delete** | Same primary keyword, lower-quality duplicate — remove the weaker version. **Always enforce a 301 redirect** from the deleted URL to the surviving canonical page; never 404 a deleted page. |
| **Re-target** | Topic overlap but distinct angles — change one's primary keyword |
| **Canonical / 301** | One page should consolidate equity into the other |
| **Accept** | Distinct content but unavoidable overlap — document the exception |

## The four-frame boundary

| Content type | Frame | Slug pattern | Example for "bleed" |
|---|---|---|---|
| Wiki | **WHAT** — definitional | Bare concept noun | `/wiki/bleed` |
| Blog | **WHY** — perspective, comparisons, angles | The angle, never the bare topic | `/blog/5-bleed-mistakes-to-avoid` |
| Helpcenter | **HOW (on Helloprint)** — platform-specific procedural | The procedural question | `/helpcenter/adding-bleed-to-your-file` |
| Commercial | **BUY** — convert | Brand/product slug | `/luxury-business-cards` |

## Multi-tag — one URL, many discovery surfaces

An article lives at one URL. Tags determine where it surfaces beyond its URL home: Blog cluster topic groups, Wiki hub themes, FAQ category sections, Industry/Theme Block 11. Same article, one canonical, many surfaces. No min/max.

## Topic groups — anchor-only, never URLs

Topic groups on Blog cluster pages are visual subsections with HTML anchors — never their own URLs. Each anchor subsection links OUT to the matching Industry/Theme L1 as the canonical commercial destination.

Exception: Products is the only Blog cluster with URL sub-clusters.

## Commercial vs. editorial keyword discipline

- **Blog never targets commercial head terms.**
- **If a Blog article ranks for a PLP head keyword, re-target the Blog article.**
- **PLP always wins.** When PLP and FAQ overlap, PLP is the destination.
- **FAQ inline on PLPs is truncated** with link to full destination.

## Products sub-cluster discipline — PLP vs. Blog (the 17-layer defence)

The Products sub-cluster sits closer to commercial intent than any other editorial surface, so it gets the most layered cannibalisation defence in the plan. The URL pattern itself is layer 1; the remaining 16 layers each independently reinforce the editorial/commercial boundary so the sub-cluster page never competes with its matching PLP for commercial intent.

| # | Layer | PLP | Blog Products sub-cluster |
|---|---|---|---|
| 1 | **URL pattern** | Flat at root: `/booklets-printing` | Deeper path: `/blog/product/booklets/{slug}` — the URL itself signals "editorial about booklets, not the booklets product" |
| 2 | **Schema** | `Product` + `Offer` | `CollectionPage` + `ItemList` (NEVER Product) |
| 3 | **Title tag** | "Booklets Printing \| Helloprint" — commercial | "Booklet design guides & tips \| Helloprint" — editorial |
| 4 | **H1** | "Booklets Printing" | "Booklet guides, tips & inspiration" |
| 5 | **Meta description** | Commercial pitch + price/CTA | Editorial summary, no commercial language |
| 6 | **Target keywords** | "booklets printing", "print booklets" — commercial | "booklet design guide", "booklet paper weight" — informational long-tail only |
| 7 | **Hero CTA** | Configurator + price + "Order now" | Soft "Browse all booklet products" link only — no buttons, no price |
| 8 | **Configurator** | Yes | Never |
| 9 | **Price indicators** | Yes | Never |
| 10 | **Product cards** | Yes — full grid | Never — only article cards |
| 11 | **Editorial/commercial ratio** | ~10/90 commercial-leaning | ~80/20 editorial-leaning (maximum 20% commercial) |
| 12 | **Page layout** | Product grid, faceted nav, filters, breadcrumbs | Article cards, editorial hierarchy, reading-first design |
| 13 | **Outbound link to neighbour** | Block 11 (Blog teaser) → relevant sub-cluster articles | Prominent CTA → "Shop booklets at /booklets-printing" with commercial anchor text |
| 14 | **Inbound link from neighbour** | Receives editorial inbound from sub-cluster | Receives equity from PLP via Block 11 (not equal billing) |
| 15 | **Canonical** | Self-canonical | Self-canonical (NOT canonical to PLP — they serve different intents) |
| 16 | **Content body** | Specs, dimensions, ordering process, USPs | Tutorials, comparisons, inspiration, how-tos |
| 17 | **Indexability** | Indexed | Indexed (separate target keyword cluster) |

**Built-in safety net — `target_keywords[]` cross-corpus check.** If a sub-cluster article tries to claim "booklets printing" as a target keyword, the system blocks publish because the PLP already claims it. This is the editorial layer's automatic catch.

**Five most important layers** — if editorial bandwidth is constrained, prioritise these:

1. **Schema** (CollectionPage not Product) — single strongest signal to Google
2. **Target keywords discipline** — informational vs commercial keyword separation
3. **Hero treatment** — sub-cluster has NO configurator and NO price; PLP has both
4. **H1 + title tag** — informational vs commercial language is unmistakable
5. **Editorial/commercial ratio** — sub-cluster 80/20 editorial; PLP 10/90 commercial

## Comparison content placement

"CMYK vs RGB", "Matte vs gloss" — always Blog, never Wiki. Cluster depends on primary frame:

- **Artwork** — design-concept comparisons
- **Product / {family}** — product-specific comparisons
- **HelloAcademy** — educational comparisons

## Worked example — "Bleed"

```
Wiki        → /wiki/bleed                                            [target_keywords: "bleed", "what is bleed"]
Blog        → /blog/5-bleed-mistakes-to-avoid                        [target_keywords: "bleed mistakes"]   (flat — Artwork cluster carried by tag)
Blog        → /blog/product/business-cards/bleed-on-business-cards   [target_keywords: "business card bleed"]   (Products sub-cluster exception — keeps depth)
Helpcenter  → /helpcenter/adding-bleed-to-your-file                  [target_keywords: "how to add bleed"]   (flat — Design & upload category carried by tag)
Commercial  → /luxury-business-cards                                 (mentions bleed; not a target keyword)
```

---

# 8. Article → commercial guidelines

Editorial guidelines for linking from articles to commercial pages. Relevance-driven (per section 6 principle 5) — these are guidelines, not enforced counts.

| Aspect | Guideline |
|---|---|
| **Link frequency** | Blog: typically 1–3 contextual links per article where naturally relevant. FAQ: 1–2 where the process leads to commercial intent. Wiki: 0–2 only when the concept is product-specific (e.g. silver foil). No forced minimums. |
| **Anchor text** | Contextual and natural. Generic anchors ("click here", "this product") avoided. Branded anchors ("at Helloprint") capped at 1 per article to keep authority flowing through topical anchors. |
| **Target precedence** | Most-specific PDP → L4 → L3 → L2 PLP → L1 Category Landing. Never homepage. Never search URL. |
| **Indexability gate** | Target page must be indexed. Never link to a `noindex` page. |
| **Tiebreaker** | When multiple indexed pages match, choose highest combined SEO + commercial value (traffic × orders). |
| **Placement** | Inline mid-body links preferred where they fit the narrative. End-of-article "Featured products" block additive where relevant. |
| **Link directive** | All internal commercial links pass equity. Never `rel="nofollow"`. |
| **Mechanism mix** | Inline editorial links + (optionally) automated end-of-article "Featured products" block where the article is product-tagged. |
| **Anti-cannibalisation** | Don't link to commercial pages that compete on the article's `target_keywords[]`. |
| **Avoid spam** | Better to under-link than to over-link. Spammy outbound weakens the article's authority signal more than missing a link costs. |

---

# 9. The `/learn` knowledge hub

`/learn` is the single landing page that unifies discovery across Blog, Wiki, Helpcenter, YouTube, and Helloprint's social channels. It is a content page in its own right — not a thin link aggregator — designed to capture top-of-funnel informational intent and distribute equity into the editorial trees.

## Function

The hub does four jobs simultaneously:

1. **Captures broad informational queries** ("printing resources", "learn printing", "printing guide", "how to print") that don't fit cleanly inside any one tree.
2. **Concentrates external link equity** at a single high-relevance node, then redistributes it via contextual outbound links to children with topically-rich anchors.
3. **Acts as the topical pillar** of a pillar + cluster authority structure — the three editorial trees are the clusters; `/learn` is the pillar.
4. **Provides a single navigable destination** for customers and crawlers asking "where do I learn about Helloprint?" — one URL to remember, share, and link to.

## URL, schema, sitemap

- **URL:** `/{locale}/learn` (translated per locale — `/leren`, `/lernen`, `/apprendre`, `/aprender`, `/imparare`, `/lara`; see section 4)
- **Schema:** `CollectionPage` + `WebSite` + `SearchAction` + `BreadcrumbList`, with one `ItemList` per topic pillar (`mainEntity` array)
- **Sitemap:** lives in `sitemap_pages_1.xml` as a standalone navigation page
- **Primary keyword target:** `printing resources` / `learn printing` (locale-equivalent)
- **Indexability:** indexed by default; canonical to the locale-specific URL

## Page composition — what's actually on the page

The hub is structured around **customer intent topics**, not CMS taxonomy. Inside each topic pillar, content is pulled from across all three editorial trees (Blog + Wiki + Helpcenter), demonstrating the cross-tree linking model that section 6 describes.

```
1. Hero + intro                                    (300-word substantive intro)
2. Sticky topic-jump nav                           (anchors to pillars)
3. Topic pillar 1 — Designing for print            (deep dive · ~8 curated items)
4. Topic pillar 2 — Paper, materials & sustainability (deep dive · ~6-8 items)
5. Topic pillar 3 — Inspiration by occasion        (deep dive · ~8 items)
6. Most popular blogs                              (curated, 5-6 items, rotates monthly)
7. Watch & learn — YouTube                         (3-5 embedded videos from HelloAcademy)
8. Browse the trees                                (3 gateway cards: Blog · Wiki · Helpcenter)
9. Cross-tree spotlight — "This week"              (Wiki + Blog + Helpcenter triplet on one topic)
10. Follow us — social channels                    (YouTube, Instagram, LinkedIn, Facebook, X)
11. Unified search                                 (across all three editorial trees)
12. CTA strip                                      (Contact · Quote)
```

Total: ~2,500 words of editorial content + ~40 curated outbound links across pillars. Editorial-to-link ratio: ~60/40. The volume is intentional — Google penalises thin-link aggregator pages; a substantive hub passes the "would this exist if Google didn't exist" test.

### Block 1 — Hero + intro

- **H1:** primary keyword target (e.g. "Printing made clear" / "Learn printing with Helloprint")
- **Intro paragraph:** ~300 words of substantive editorial content — not "browse our resources" filler. Demonstrates expertise on print as a domain. Reads as the start of a real article, not a directory landing.
- **Search bar:** unified search across all three editorial trees, surfaced above the fold.

### Blocks 3-5 — Topic deep-dive pillars

Three pillars, each linking outward to specific subcategories on Wiki, Blog, and Helpcenter. The pillars are chosen for maximum customer intent overlap with Helloprint's commercial surface and editorial volume.

**Pillar 1: Designing for print**
*Target intent: "I don't know enough about print files yet"*
*100-word editorial intro per pillar — not just a header.*

| Linked item | Tree | Subcategory |
|---|---|---|
| What is bleed? | Wiki | Design concepts |
| CMYK explained | Wiki | Design concepts |
| DPI and print resolution | Wiki | Design concepts |
| 5 bleed mistakes to avoid | Blog | Artwork |
| CMYK vs RGB — when each makes sense | Blog | Artwork |
| Why your print looks different from your screen | Blog | Artwork |
| Adding bleed to your file | Helpcenter | Design & upload |
| Print-ready PDF checklist | Helpcenter | Design & upload |

**Pillar 2: Paper, materials & sustainability**
*Target intent: "What should I print on?"*

| Linked item | Tree | Subcategory |
|---|---|---|
| Paper weight explained (gsm) | Wiki | Materials |
| Matte vs gloss finish | Wiki | Materials |
| Recycled paper options | Wiki | Materials |
| Sustainable print: B-Corp standards at Helloprint | Blog | Sustainability |
| Choosing the right paper for booklets | Blog | Product |
| Eco-friendly printing FAQs | Helpcenter | Account |
| Material selection: a customer guide | Blog | HelloAcademy |

**Pillar 3: Inspiration by occasion**
*Target intent: "Show me ideas for my use case"*

| Linked item | Tree | Subcategory |
|---|---|---|
| Wedding stationery inspiration | Blog | Printspiration |
| Festival & event print ideas | Blog | Printspiration |
| Branded merch ideas | Blog | Printspiration |
| Seasonal campaign inspiration | Blog | Printspiration |
| Customer stories — events | Blog | Printspiration |
| Industry/Theme L1: weddings | Commercial | Industry L1 |
| Industry/Theme L1: events & festivals | Commercial | Industry L1 |
| Helpcenter — event delivery & tracking | Helpcenter | Delivery & tracking |

Editorial discipline within pillars: each linked item carries a 1-2 sentence original description (not pulled from target's meta description), contextual anchor text (not "click here"), and the title shown is the article's actual H1 or a contextual phrase.

### Block 6 — Most popular blogs

Curated grid of 5-6 highest-traffic Blog articles in the last 30 days. Editorial layer (manual curation) overlays automated traffic data. Rotates monthly. Drives discovery of proven content.

### Block 7 — Watch & learn (YouTube)

3-5 embedded YouTube videos from HelloAcademy and other clusters. Each embed carries:
- `VideoObject` JSON-LD with duration, thumbnail, description
- Transcript visible below the embed (accessibility + SEO)
- Outbound link to the relevant Blog article that contextualises the video
- Outbound link to Helloprint's YouTube channel

This block doubles as the YouTube channel's primary on-domain promotion — driving subscribers + watch-time signals while keeping the embed page topical.

### Block 8 — Browse the trees (gateway cards)

Three cards, each leading to one tree hub:

- **Blog** — "Editorial perspectives, design tips, ideas, inspiration." → `/blog/`
- **Wiki** — "Quick definitions for the print terms that matter." → `/wiki/`
- **Helpcenter** — "Step-by-step answers to your Helloprint process questions." → `/helpcenter/`

Generic in description but the cards themselves are visually rich — preview tile, brief value prop, "browse all →" CTA.

### Block 9 — Cross-tree spotlight ("This week")

Editorial pick that demonstrates the cross-tree linking model. Format:

> **This week: bleed**
> Read the [definition](/wiki/bleed) · See [common mistakes](/blog/5-bleed-mistakes-to-avoid) · Follow [the step-by-step fix](/helpcenter/adding-bleed)

Rotates weekly. Each spotlight uses one topic and shows its Wiki + Blog + Helpcenter triplet. Reinforces the WHAT/WHY/HOW boundary visually.

### Block 10 — Follow us (social channels)

Direct outbound links to Helloprint's social accounts. Each renders as a branded icon block with channel name and short hook ("Behind the scenes on Instagram", "Print tips on YouTube").

- YouTube
- Instagram
- LinkedIn
- Facebook
- X (formerly Twitter)
- Vereniging van het Jaar (light reference, where editorially relevant)

Outbound links are `rel="noopener"` (no `nofollow` — these are owned channels and we want them to receive equity).

### Block 11 — Unified search

Single search input scoped across `/blog/*`, `/wiki/*`, `/helpcenter/*`. Results page groups by tree (Blog / Wiki / Helpcenter) with type indicators. Implements `SearchAction` schema so Google can render a sitelinks search box for the hub in SERPs.

### Block 12 — CTA strip

Two CTAs at the bottom:
- **Need direct help? → /helpcenter/contact**
- **Quoting a large order? → /helpcenter/quote**

Catches users who arrived top-of-funnel but realise they want to talk to a human.

## How the hub avoids being penalised

The hub passes the "would this exist if Google didn't exist" test. Specific guardrails:

| Risk | Guardrail |
|---|---|
| **Thin content** | Minimum 1,500 words of unique editorial content (excluding link card descriptions). The hub IS a long-form authority piece, not a directory. |
| **Doorway page** | Each topic pillar has its own substantive ~100-word editorial intro. The page provides genuine reading value before any link block. |
| **Auto-generated aggregator** | Featured selections are editorially curated, not template-generated. Rotates monthly. |
| **Topic dilution** | One primary keyword target — "printing resources" or locale equivalent. Subtopics target their own related queries within their pillar. |
| **Exact-match keyword stuffing** | Primary keyword used naturally — once in H1, once in intro, sparsely throughout. |
| **Spammy anchor text** | Contextual anchor text using the target article's actual title or a natural phrase. No "click here", no exact-match keyword anchors on every link. |
| **Orphan structure** | Hub linked from homepage hero, header top-right, footer "Resources & Support" column, AND contextually from 5-10 high-traffic articles per tree ("for a broader view, see our [Learn hub](/learn)"). |
| **Low engagement** | Editorial quality must justify the hub's existence to users, not just crawlers. Dwell time, scroll depth, click-through to trees tracked monthly. |

## Internal linking topology

**Into the hub:**
- Homepage — feature in primary nav block
- Header — `/learn` link top-right (replaces the old `/helpcenter` static link)
- Footer — "Resources & Support" column: Learn · Blog · Wiki · Helpcenter · Contact · Quote
- Within trees — contextual mentions in 5-10 high-traffic articles per tree

**Out of the hub:**
- ~40 contextual links to specific articles across the three trees (distributed across the 3 pillars + Most popular + Cross-tree spotlight)
- 3 "Browse all in [tree]" links to Blog hub, Wiki hub, Helpcenter hub
- 5-6 outbound links to social channels (`rel="noopener"`, no `nofollow`)
- 1 search box → unified search results
- 2 CTAs → Contact / Quote

This is the topology that makes the hub a real topical authority node, not a thin aggregator.

## Maintenance cadence

| Activity | Cadence | Reason |
|---|---|---|
| Featured items rotate (popular blogs, YouTube embeds, cross-tree spotlight) | Monthly | Freshness signal via lastmod; encourages return visits |
| Pillar intros reviewed | Quarterly | Editorial accuracy; avoid stale content claims |
| New articles surfaced into pillars | At publish | If a new Wiki/Blog/Helpcenter article fits a pillar, editor adds it |
| Word count audit | Quarterly | Ensure edits haven't dropped editorial content below 1,500 words |
| Search behaviour audit | Monthly | Add high-frequency missing terms to a pillar |
| Topic pillar review (add/remove pillars) | Annually | Customer intent evolves; pillars should match the most-searched topics |

## Build dependencies

- Helpcenter URL migration complete (so cross-tree spotlight URLs resolve)
- Blog URL migration complete (same)
- Wiki URL structure live with at least size pages migrated (same)
- 6 hub blocks (1, 8, 10, 11, 12) are structural; blocks 3-5, 6, 7, 9 require editorial content selection before launch
- YouTube channel content selection (3-5 videos with full transcripts) — Supply / Marketing dependency
- Social channel link audit — confirm all 5 accounts are active

---

# 10. Hub & category page specs

Shared layout pattern for tree hubs (`/blog/`, `/wiki/`, `/helpcenter/`) and cluster/category aggregator pages (`/blog/{cluster}/`, `/helpcenter/{category}/`).

> **What aggregator hubs do in v2.8** — since articles live flat under tree roots (`/blog/{slug}`, `/helpcenter/{slug}`), the cluster/category hubs no longer own child URLs in their URL path. Instead they're **topical aggregator pages**: each hub queries articles tagged with its cluster/category and renders the curated list. The article URL doesn't include the cluster — the cluster relationship is carried by tag and surfaced on the hub.

## Shared layout pattern

1. **Hero** — H1, intro paragraph (~150 words), search/filter
2. **Sticky topic-jump nav** — anchor links to each topic group
3. **Topic groups** — visual subsections with HTML anchor:
   - H2 = topic name
   - Cross-references to the OTHER two content types for the same topic
   - All entries of the primary content type for this page, fully listed (no pagination, no truncation)
4. **End-of-page** — Featured commercial products (Block 11), CTA to contact/quote, link to sibling hubs

Blog cluster pages list Blog articles primarily. FAQ category pages list FAQ entries primarily. Wiki hub lists Wiki entries primarily. The cross-references are supporting context.

## Tag-driven topic-group rendering

```
1. GET all entries of primary content type WHERE cluster/category = this page
2. GROUP BY topic_tag
3. For each topic_tag group:
   ├── H2 = topic display name
   ├── Fetch 1 sibling Wiki entry WHERE topic_tag matches → render card
   ├── Fetch 1+ sibling FAQ entries WHERE topic_tag matches → render card(s)
   └── List ALL entries of primary type in this group (no pagination)
```

## Editorial overlay

- **Pin priority topics** to the top of the page
- **Custom display name** for a topic (override the tag's literal name)
- **Featured entry per topic** — pin one card to lead position

## Edge cases

| Scenario | Behaviour |
|---|---|
| Topic has primary content but no sibling Wiki | "WHAT" block shows placeholder with editorial flag |
| Topic has primary content but no sibling FAQ | "HOW" block falls back to "Need platform help? → /helpcenter/contact" |
| Topic has Wiki + FAQ but NO primary content | Topic doesn't appear on this page; appears on the other two hubs |
| Article tagged with multiple topics | Appears in multiple topic groups. Encouraged. |

---

# 11. Schema & on-page requirements

JSON-LD per page type, breadcrumbs everywhere, self-canonicals by default.

| Page type | Required schema |
|---|---|
| **`/learn` hub** | `CollectionPage` + `WebSite` + `SearchAction` + `BreadcrumbList` + `ItemList` per topic pillar |
| Wiki entry | `DefinedTerm` or `Article` + `BreadcrumbList` |
| Wiki hub | `WebSite` + `SearchAction` + `BreadcrumbList` |
| Blog article | `Article` + `BreadcrumbList` + author byline |
| Blog article with video | `Article` + `VideoObject` + `BreadcrumbList` |
| Blog cluster page (and sub-cluster) | `CollectionPage` + `BreadcrumbList` + `ItemList` |
| Blog hub | `WebSite` + `SearchAction` + `BreadcrumbList` |
| Helpcenter article (single-question) | `QAPage` + `BreadcrumbList` + `Article` |
| Helpcenter article (step-by-step) | `HowTo` + `BreadcrumbList` + `Article` |
| Helpcenter category page | `CollectionPage` + `BreadcrumbList` + `ItemList` |
| Helpcenter hub | `WebSite` + `SearchAction` + `BreadcrumbList` |

## On-page requirements (publishing gate)

- Minimum 200 words; aim for 400–800 on volume informational queries
- Visible last-updated date
- Author byline — "Helloprint Content Team"
- At least one image / diagram; embed YouTube where relevant with `VideoObject` schema
- Self-canonical to the locale-specific URL
- Breadcrumb rendered visibly + shipped as `BreadcrumbList` JSON-LD
- "Was this helpful?" feedback widget on FAQ entries
- `target_keywords[]` field populated per locale (publishing gate)

---

# 12. Migration & redirects

The migration is the highest-risk step.

## Six-step migration playbook

1. **1:1 301 redirects** from every old URL. No catch-all. No 302s. No chains.
2. **Update internal links wholesale** — direct links pass 100% equity; redirects pass ~85–90%.
3. **Update controllable external backlinks** — VvhJ updates blog links to new URLs.
4. **Audit historical press URLs** — 1:1 301s into Blog: Company.
5. **Submit new sitemap to GSC** immediately on launch.
6. **Permanent redirect retention.**

## Deleted-content fallback

301 to a new article, the article's category, or the relevant product category. Never 404.

## Monitoring window

4–8 weeks post-launch. Flag anything > 20% ranking loss.

---

# 13. References out

| Topic | Owned by |
|---|---|
| Block 11 — Blog/inspiration teaser on PLPs (full spec) | PLP Requirements · Block 11 |
| Technical SEO infrastructure — sitemap, hreflang, redirects (canonical spec) | PLP Requirements · §3.4 |
| Indexation governance — rules-driven engine, meta-robots approval, audit trail | PLP Requirements · §3.3 (g-url) |
| Commercial URL slug format, faceted nav, pagination, canonicals, hreflang | PDP / PLP Requirements |
| `target_keywords[]` field on commercial Contentful entries (Contentful schema) | Commerce platform team — v1 prerequisite |
| Tag schema design and optimisation | Tag Schema Workstream — **V1 prerequisite** (automation layer depends on it) |
| FAQ creation system on PLPs/PDPs | FAQ System Spec |
| Industry / Themed / Location URL reconciliation | Separate workstream |
| Print Wiki editorial taxonomy extension (design + materials) | Separate workstream |
| Helpcenter platform migration (Elevio → Contentful) | Technical workstream |
| Solution & Company platform migration (Webflow → Contentful) | Technical workstream |
| Product Content / Platform Catalog content model | Sebastiaan's Content System Proposal |

---

# 14. Action plan & V2 steps

V1 = everything needed for the structure to scale. V2 = optimisation on top of the foundation, with timelines and dependencies.

## V1 — Action plan now

Goal: get the foundational structure in place so content can be scaled and optimised in V2. Every item below is required for V1 launch.

> **Sequencing**
> **1. System migrations** → **2. URL migrations** → **3. Sitemap inclusion (staging first)** → **4. Production cutover**. Page templates, schema, target_keywords field run in parallel with the migrations.

### 1 · System migrations

| Action | What it means | Status |
|---|---|---|
| **Helpcenter platform migration** (Elevio → Contentful) | Move all helpcenter content out of Elevio into the unified Contentful instance under the new Helpcenter content model | ✅ Done |
| **Solution & Company platform migration** (Webflow → Contentful) | Move all Solution & Company pages out of Webflow into Contentful. **Blocked by** Contentful design — current block design needs redesign for scalable Contentful structure before migration can start. Required for V1 so all content sits in one CMS. | TBD · blocked by Contentful design |

### 2 · URL migrations & redirects

| Action | What it means | Status |
|---|---|---|
| **Helpcenter URL migration** | `/cs/*` → `/helpcenter/{article-slug}` (flat — drops both `/faq/` segment AND category segment). Category aggregator hubs built at `/helpcenter/{category}/`. 1:1 301 mapping. | TBD |
| **Blog URL migration** | `/blog/category/*` → `/blog/{article-slug}` flat for 6 clusters. Cluster aggregator hubs at `/blog/{cluster}/`. **Products sub-cluster keeps depth**: `/blog/product/{family}/{slug}` (anti-cannibalisation exception per section 7). | TBD |
| **Wiki URL migration** | Existing flat-root size pages (e.g. `/nl-nl/a7-formaat`) → `/wiki/{slug}`. New Wiki hub built. URL structure ready for taxonomy expansion in V2. | TBD |
| **Industry/Theme URL reconciliation** | Reconcile the inconsistent mix of nested `/industry/{vertical}/{sub-vertical}` and flat `/event-festivals-printing` etc. to flat-at-root. URL structure only; content scaling = V2. | TBD |
| **Location pages retirement** | Pre-retirement traffic audit to preserve high-traffic Location pages worth keeping. Retire the rest with 301s to the best-fit destination. | TBD |
| **Design Templates redirect** | `/{locale}/design-templates` 301 to Canva integration entry point. Timed with summer Canva-integration end. | TBD |
| **Reseller locale fix** | `/uk/reseller-solutions` 301 to `/en-gb/reseller-solutions` (canonical). | TBD |
| **All fixes, inconsistencies & checks** | Pre-migration audit: internal links to old URLs, sitemap entries, hreflang references, redirect chains. Fix everything before cutover so direct links pass 100% equity. | TBD |

### 3 · Sitemap & crawler infrastructure

| Action | What it means | Status |
|---|---|---|
| **Build new sitemap infrastructure** | Code the per-locale sitemap generator that produces the six-file structure documented in section 5. | TBD |
| **Six-file sitemap structure per locale** | `sitemap_landings_1`, `sitemap_products_1`, `sitemap_blog_1`, `sitemap_wiki_1`, `sitemap_helpcenter_1`, `sitemap_pages_1` (the latter includes the new `/learn` hub). | TBD |
| **Daily report system** (post-regen) | End-of-day report after each sitemap regeneration listing new URLs added + URLs removed. Persistent queue until each URL is approved or rejected by content team. Escalation if stuck > 7 days. | TBD |
| **Generation guardrails** | Three block conditions: 5%+ increase in one run · 5%+ decrease in one run · any Top 100 per locale missing. When triggered, hold the new sitemap and require SEO Lead approval before serving. | TBD |
| **Top 100 list definition per locale** | SEO Lead defines the Top 100 must-have PDPs/PLPs per locale (representative across product families). Same list used for sitemap guardrails. Quarterly maintenance. | TBD |
| **Submit new sitemaps to GSC + Bing** | Register master sitemap index in Google Search Console and Bing Webmaster Tools. One-time submission; subsequent updates picked up via daily regen + lastmod signals. | TBD |

### 4 · Contentful schema

| Action | What it means | Status |
|---|---|---|
| **target_keywords[] field** | Add the `target_keywords[]` field (per locale, multi-value) to ALL indexable Contentful entry types — Wiki, Blog article, FAQ, Blog cluster page, FAQ category page, commercial PDP, commercial PLP, Industry/Theme L1, Solution & Company page. Field exists in V1; cannibalisation check system that uses it = V2. | TBD |
| **Basic publishing field validation** | Contentful's native required-field validation on critical fields (slug, target_keywords, breadcrumb metadata, schema fields). Custom validation rules (200-word check, etc.) = V2. | TBD |

### 5 · Page templates & layouts

| Action | What it means | Status |
|---|---|---|
| **`/learn` unified hub** | Build the unified knowledge hub per section 9 spec: hero + 3 topic pillars + popular blogs + YouTube embeds + 3 tree gateways + cross-tree spotlight + social channels + unified search + CTAs. Editorial content per pillar (~1,500 words minimum) curated by content team. Schema: CollectionPage + ItemList per pillar. Lives in `sitemap_pages_1.xml`. | TBD |
| **Wiki hub + entry templates** | Build `/wiki/` hub with theme-grouped subsections (Sizes, Design concepts, Materials, etc.) + Wiki entry template (DefinedTerm/Article schema, breadcrumb, related entries). | TBD |
| **Blog templates** | Build `/blog/` hub, cluster pages (7), Products sub-cluster pages, article template. Topic-group rendering on cluster pages is **tag-driven automated from V1** (see section 5 · Page templates). | TBD |
| **Helpcenter templates** | Build `/helpcenter/` hub, category pages (5), Helpcenter article template (QAPage / HowTo schema, "Was this helpful?" widget). | TBD |
| **Tag schema (taxonomy)** | The underlying tag taxonomy — which tags exist, hierarchy, governance. Foundation for everything else in the automation layer. Owned by Tag Schema Workstream (section 13). | TBD |
| **Auto-assigning tags to content** | AI / rules that read a new entry at publish and assign the right tags automatically — writers don't have to think about it. Depends on tag schema being live. | TBD |
| **Tag-driven within-tree linking** | Related-content modules (blog→blog, wiki→wiki, faq→faq) auto-populated from tags. Replaces editorial-curated v1 fallback. | TBD |
| **Tag-driven topic-group rendering on cluster pages** | Blog cluster pages and Helpcenter category pages auto-group content by tag (per the rendering pseudo-code in section 10), instead of editorial-curated. Editorial overlay (pin priority topics, custom display name, featured entry per topic) still applies. | TBD |

### 6 · Schema & on-page foundation

| Action | What it means | Status |
|---|---|---|
| **Schema markup per page type** | JSON-LD schema implementations per page type (see section 11): DefinedTerm, Article, QAPage, HowTo, CollectionPage, BreadcrumbList, WebSite + SearchAction, VideoObject (for video embeds). | TBD |
| **Self-canonicals, breadcrumbs, hreflang in `<head>`** | Every page emits a self-canonical to its locale-specific URL, a BreadcrumbList JSON-LD, and hreflang annotations in the page `<head>` (NOT in sitemap, per PLP §3.4B). | TBD |

### 7 · Editorial governance

| Action | What it means | Status |
|---|---|---|
| **Publish this plan as canonical reference** | Lock the document as the source of truth for the content team. The 7 Blog clusters, 5 FAQ categories, Wiki strict scope, four-frame boundary, cross-tree linking grid, slug conventions — all become editorial rules. | TBD |
| **Brief content team** | Walk-through session covering: the 12 buckets, the WHAT/WHY/HOW boundary, slug conventions per content type, target_keywords field usage, where to put what content. | TBD |

### 8 · Migration monitoring

| Action | What it means | Status |
|---|---|---|
| **Continuous health & traffic monitoring** | Automatic systems running: drop-off alert (URL falls out of sitemap), post-regen sitemap crawler (HTTP status, meta-robots drift, canonical drift, hreflang anomalies), stale-content alert (lastmod > 90 days). All inherited from PLP §3.4. | TBD |
| **4-8 week migration monitoring window** | Ahrefs ref-domain stability, GSC crawl errors, ranking movement post-cutover. Flag anything > 20% ranking loss. | TBD |

## V2 — Steps for later

Optimisation on top of the V1 foundation. Each item carries a timeline indication and dependency.

| V2 step | Timeline | Dependencies |
|---|---|---|
| ~~Automation layer~~ — **moved to V1** (tag schema + auto-tagging + tag-driven within-tree linking + tag-driven topic-group rendering all ship in V1) | — | — |
| **Cannibalisation check system** — soft warning + editor review workflow comparing new entries' `target_keywords[]` against the full corpus | After V1, similar pattern as PDP/PLP commercial check | target_keywords[] field live (V1) |
| **Custom editorial publishing gates** (word-count check, target-keyword presence check, etc.) | Bundled with cannibalisation check system | target_keywords[] field live + custom validation tooling |
| **Block 11 manual deployment to commercial PDPs** — Top 100 per market is a guideline, not strict; only deploy where ranking benefit or extreme relevance exists | After V1, when editorial bandwidth allows | Block 11 spec live on PLPs; editorial selection capacity |
| **FAQ creation system / content integration** — inline FAQ blocks on PLPs/PDPs with "Read full answer" to Helpcenter destinations. Not a separate system; content integration on existing content models. | After V1, content integration approach | Helpcenter URL migration live |
| **Internal linking patterns enforced editorially** — train and document workflow for editors to apply the cross-tree linking matrix consistently | After V1, when editorial team scales | This plan as canonical reference (V1) |
| **Print Wiki taxonomy extension** to design concepts and materials | No hard commercial priority; only after commercial optimisations done | First inventory existing definitional content scattered across blog/help — could be quick-converted |
| **Image sitemap** | After new Platform Catalog is live | Platform Catalog migration · CDN URLs stable · Image and alt-text quality (prioritised separately, more important than the sitemap itself) |
| **Location pages rebuild** (safer PSEO approach) | Wait for healthy SEO signals after V1 before testing | V1 traffic recovery confirmed; PSEO approach defined |
| **Context-aware help widget** (replace static `/helpcenter` link) | Part of UX optimisation track | Integrated with Anna |
| **Behavioural help pop-ups** | Part of UX optimisation track | Integrated with Anna · Depends on context-aware widget |
| **Social content integration / generation layer** — AI-powered marketing focus | Most important marketing focus. Can run in parallel with V1 (not frontend-dependent) | Independent of SEO frontend |
| **Add category back into Helpcenter article URLs** — if flat `/helpcenter/{slug}` proves harder to navigate than expected, optionally introduce `/helpcenter/{category}/{slug}` based on real behavioural data | After 4-8 week post-migration monitoring window | V1 flat structure live + measurable customer behaviour data |
| **Industry/Theme content scaling** — content optimisation of existing pages, then expansion | After V1 URL structure work + after other commercial optimisations land | V1 URL structure reconciliation complete |
