# HelloPrint — Page Content Model (complete)

*Single-file consolidation of the multi-page model — Master hub + surfaces + content types + global contracts. Generated from the canonical markdown on 2026-06-09. The per-page files under `content-types/`, `contracts/`, `surfaces/` remain the source of truth; this file is the assembled read-through (mirrors `HelloPrint-Page-Content-Model-COMPLETE.html`).*


## Contents


**Overview**

- HelloPrint Page Content Model — Master (hub)

**Surfaces**

- Surface — PDP (Product Detail Page)
- Surface — PLP (Product Listing Page)
- Surface — FLP (Filter Listing Page)

**Content types**

- product (PDP page entry)
- pageHomeModular (PLP / FLP page entry)
- contentMedia (Block S — Content / Media)
- rich-text-BE (Block BE — Rich text)
- blog-teaser-AJ (Block AJ — Blog / inspiration teaser, B11)
- productCollection (Block D — Product Collection)
- bundleItem (product grid / related tile)
- card-label (merged tile label)
- product-list-Z (Block Z — Link Hub)
- Promo Card (promoCard)
- Promo Code (promoCode)
- Customer Reviews (homeBlockTypeP — Block P)
- General FAQ (homeBlockTypeV + faqItem — Block V)
- Video (video)
- Person (person)
- g-pagecard — shared page card (BH + BI)
- USP Block (Block BB) — page-specific on-page USPs
- Block C — Brands block (b17)
- Block AH — in-page section nav
- Block AZ — Filter engine (filterConfig on pageHomeModular)

**Global contracts**

- g-url — URL structure & indexation rule-engine
- g-meta — Title, description, canonical, hreflang & per-locale meta-robots
- g-schema — JSON-LD structured-data stack (no CollectionPage)
- g-uspbar — USP bar above the H1
- g-keywords-scoring — target_keywords & cannibalisation / content scoring
- g-tech-seo — sitemap, redirects & hreflang reciprocity
- g-mobile — mobile-first, content parity, performance & touch
- cache — Cloudflare edge, event-driven purge & cache-key tuple
- breadcrumb — the Contentful walker & BreadcrumbList schema

---



# ▌Overview


---


*(type: hub · surfaces: [PDP, PLP, FLP] · status: draft)*


# HelloPrint Page Content Model — Master (hub)

**The single canonical source of truth for the HelloPrint page content model across PDP, PLP and FLP.** This hub is the navigable index; each content type, contract and surface has its own complete detail page (linked below). It consolidates five source documents — they now **freeze as history**; all future edits land here.

**Authority layering.** The **Requirements docs are the basis** (full behaviour) → the **Variation Catalogs add the content-model detail** → **the locked decisions (reconciliation log below) are the final overrides**. Where sources disagree, the **newer doc + the decisions win**. Reconciled against the **documents** only — not the live site (old setup).

**Structure.** `Page-Content-Model/` = this hub + `content-types/` (one page per Contentful content type) + `contracts/` (the global g-* rules) + `surfaces/` (PDP/PLP/FLP page maps). Everything cross-linked.

**Labels.** Every rule & field carries two axes — **phase** (`V1` now · `V2` later + the only home for A/B tests · `MIXED`) and **type** (`BUILD` engineering punch-list · `GUIDELINE` commercial scoring card · `KEEP` preserve existing behaviour). Each detail page opens with a label summary; Part E carries the phase per block.

---

## Part A — Page-type map

**The page entry type differs by surface; the block library + contracts are shared.**

| | PDP | PLP | FLP |
|---|---|---|---|
| **Page entry** | **`product`** ([[product]]) | **`pageHomeModular`** ([[pageHomeModular]]) | **`pageHomeModular`** + the AZ filter block |
| What it is | one product (configurator) | a category / listing | a PLP narrowed by facets |
| Becomes itself by | the configurator (B5) | a product grid ([[productCollection]]) | a `Content Blocks` entry incl. [[filter-engine-AZ]] (the `filterConfig` block; **defined**) |
| Modular blocks field | **`Content Blocks`** | **`Content Blocks`** (was `bodyBlocks`) | **`Content Blocks`** |
| H1 | product name (no verb) | category keyword (verb + cluster rules) | bare-noun category (+ earned-filter modifier) |
| Hub/leaf | always a **leaf** | hub or leaf | leaf of a PLP; earned variants are leaves |
| Taxonomy parent | `Direct Main Category` (single ref) | `parentCategory` (self-ref) | `parentCategory` (+ parent-FLP ref, *to define*) |
| Page schema | `Product` + `Offer`/`AggregateOffer` | `WebPage` + `BreadcrumbList` + `ItemList` | same as PLP |

- **Shared = the modular block library ([[#Content models]]) + the global contracts ([[#Global contracts]]).** Only the top-level page entry differs.
- **No separate `Category` content type** — a category node *is* a `pageHomeModular`. **Earned-filter variants** = separate **unique-content** `pageHomeModular` destinations (`parentCategory` ref; declared in the parent FLP's AZ `indexableFilters` — destination-only, see [[filter-engine-AZ]]).

---

## Content models

Grouped index — each links to its complete detail page.

**Page entries:** [[product]] (PDP) · [[pageHomeModular]] (PLP/FLP)

**Editorial:** [[contentMedia]] (Block S → B7/B15 · B9) · [[rich-text-BE]] (freeform escape hatch, all surfaces) · [[blog-teaser-AJ]] (B11)

**Product grid & tiles:** [[productCollection]] (Block D → B5/B12) · [[bundleItem]] · [[card-label]] (merged labels) · [[product-list-Z]] (Link Hub — link list at scale)

**Promo:** [[promoCard]] (B6/B10 BG) · [[promoCode]]

**Trust / FAQ / media / authority:** [[reviews-blockP]] (B8/B9) · [[faq-blockV]] (B11/B13) · [[video]] (standalone) · [[person]] (PM byline, B15/B-PM)

**Media primitive:** [[asset]] (image/gif — `Title` internal · `Description` = alt · `File`; the single alt-text source for every image field)

**Navigation & on-page:** [[g-pagecard]] (BH/BI) · [[usp-block-BB]] · [[brands-blockC]] (b17) · [[in-page-nav-AH]] (Block 1)

**Filter engine (FLP) — defined:** [[filter-engine-AZ]] (`homeBlockTypeAZ` → `filterConfig` JSON block on [[pageHomeModular]]; store-keys/resolve-live; destination-only indexation)

---

## Global contracts

The requirements basis, defined once with per-surface deltas:

[[g-url]] · [[g-meta]] · [[g-schema]] · [[g-uspbar]] · [[g-keywords-scoring]] (incl. the cannibalisation scorer + b9-11 H2 rule) · [[g-tech-seo]] · [[g-mobile]] (FLP looser budget) · [[cache]] · [[breadcrumb]]

## Surface maps

[[surface-PDP]] · [[surface-PLP]] · [[surface-FLP]] — page entry, DOM order, block list per surface.

---

## Part E — Block-inventory verdicts

**M** Maintain · **M+** optimised · **V1/V2** phase · **—** not on surface · **Kill** removed.

| Block / type | PDP | PLP | FLP |
|---|---|---|---|
| USP bar ([[g-uspbar]], 4 USPs) | M | M | M |
| In-page nav ([[in-page-nav-AH]]) | global header (keep) | M | M (no jumps V1) |
| Breadcrumb ([[breadcrumb]]) | M | M | M |
| Taxonomy tree (B2b) | — | — | M (FLP-only, V1) |
| H1 + intro | M | M | M |
| Content/Media ([[contentMedia]], S) | M+ (B7·B15) | M+ (B9) | M+ (B9) |
| Product collection ([[productCollection]], D) | M (B12) | M (B5+B12) | M (B5) |
| Bundle item ([[bundleItem]]) | M | M | M |
| Card label ([[card-label]]) | M | M (1/tile) | M |
| Promo card ([[promoCard]]) | M (B6) | M (B10 BG V1) | M (B6 V2) |
| Reviews ([[reviews-blockP]]) | V2 (B9) | M (B8 V1) | M (B8 V1) |
| FAQ ([[faq-blockV]]) | M (B11) | M (B13) | M (B13) |
| Video ([[video]]) | M (+hero gallery) | M | M |
| Asset ([[asset]], Title/Description/File) | M | M | M |
| Productmanager ([[person]]) | V2 (B-PM) | V2 (B15) | V2 (B15) |
| Page cards ([[g-pagecard]], BH/BI) | — | M | M |
| Variant/use-case sub-grid (B7, [[g-pagecard]]) | — | V2 | V2 (shop-by-attribute) |
| USP Block ([[usp-block-BB]]) | — | M+ | inherit |
| Brands ([[brands-blockC]], b17) | — | M+ | inherit |
| Blog teaser ([[blog-teaser-AJ]], B11) | M+ | M+ | M |
| Rich text ([[rich-text-BE]], escape hatch) | M | M | M |
| Link Hub ([[product-list-Z]]) | — | M+ — **defined** | M+ — **defined** (also homepage + category hubs) |
| Filter engine ([[filter-engine-AZ]]) | — | — | M+ — **defined** (V1; build gated on catalogue API) |
| Configurator (B5) | M (V1 engine) | — | — |
| **B17 Pros & Green Claim** | M (Pros V1 KEEP · Green Claim V2) | — | — |
| Specs + Design tabs (B8) | M (V1·KEEP) | — | — |
| Specs matrix (B16) | V2 new | — | — |
| Config deep-dive (B10) | V2 new | — | — |
| Chat & Help (B13, lazy chunk) | V2 | — | — |
| SEO text (B14) | M (B15) | M | M |
| **Killed (all surfaces)** | A · AI · AL(→B10) · AT · BC · BD(→B16) · W · AG · AW · AA · L · Y · BF · N · BA · BJ · T · U · AC(→H1/introParagraph) · G(→[[usp-block-BB]]) | | |

---

## Part F — Change log

- **PDP Req v0-34** — v0.6 BUILD/GUIDELINE split; v0.7 b9-11 H2 rule; v0.9 url-11/12; v0.16 B5 configurator; v0.17 B8→B16→B10 + B16 matrix; v0.20 per-locale meta-robots; v0.25 B17 Pros/Green-Claim; v0.28 +B5 rows + KEEP tag + anti-cannibalisation→GUIDELINE; mobile round (content-parity gate); v0.34 Seb context (removed price/pre-set blocks; Pros&Cons near B7).
- **PLP Req v1-13** — v1.5 BUILD set; v1.7 mobile; v1.12 Parent Category publish-blocker + meta-robots flip; v1.13 8 OPs closed, B8→V1, locked.
- **FLP Req v0-15** — earned-filter via CF entries; v0.6 F3 pagination v2 + B11 re-added + **no CollectionPage** (OP-47); v0.7 B8 Surface A/B; v0.12 F1 five-state contract; v0.18 B5 swatch swap + delivery + labels.
- **PDP Catalog v0.20** — Bundle/Promo/Code locked; attributeLabel; Video v2; §8 USP dropped V1; no Block D card video.
- **PLP Catalog v1.5** — v1.1 field models (AH/AJ/BI/BB/C); kills AC+G. v1.2 Block C lock + dedup SHOULD + per-shop→locale. v1.3 kill N/AI/BA/BJ + rescue Z+AZ (FLP). v1.4 Block S caption + media-pair. v1.5 BE returns.
- **This master** — v0.1 single-file synthesis (2026-06-04) → **v0.2 multi-page canonical**: split into hub + 20 content-type + 9 contract + 3 surface pages (parallel build); audit-corrected (PDP=`product`; USP=4; `Content Blocks` rename; Person modelled; B17 restored; FLP budget delta; breadcrumb V1 soft-warn; PLP B9-before-B8; target_keywords union shape; contentMedia→B7·B15).
- **Block Gallery v2** (2026-06-04) — visual render of every block × variation (`outputs/HelloPrint-Block-Design-Gallery.html`, 30 blocks). Added B10 Config deep-dive, B6 in-grid card, B7 variant/use-case sub-grid, B7 product description, B8 Specs+Design tabs, B13 Chat & Help. Two design corrections synced back here: promoCard **discount card = distinct promo treatment** (flash badge + framed panel, not a [[bundleItem]] tile); [[contentMedia]] **Pair-beside images reduced to ≈16:9** so the stacked pair sits level with the copy. Verdict-matrix rows added for B8 / B13 / B7 sub-grid.
- **Block S revision** (2026-06-04) — [[contentMedia]] images are no longer links: dropped `imageDestination`/`imageSecondaryDestination`, added **`ctaSecondary`** with image-pairing (both `imageSecondary` + `ctaSecondary` → each CTA renders under its image; else CTA(s) below the copy). Alt text moved off the block onto a new **[[asset]]** content type (`Description` = alt · `Title` = internal · `File` = image/gif; all localized) — the single alt source for every image field.
- **Alt-from-Asset propagation** (2026-06-04) — the [[asset]] `Description` = alt rule now applies to **every** image-bearing block (bundleItem, promoCard, g-pagecard, brands, video poster, person, product-list-Z, pageHomeModular, product `catalogImage`, reviews background). Resolves a conflict in [[product]] (Seb-Q1 alt-text rewire) which targeted Asset→`Title`: **overridden to Asset→`Description`** (`Title` is internal-only).
- **Block Z locked** (2026-06-05) — [[product-list-Z]] as-is model locked against live Contentful field IDs (`imageTile` not `image`; `prestaContentKey`, `showAllText`/`showAllLink` added; `shouldShowPerShop` removal pending). Z-1/2/3 resolved.
- **Block Z redesigned → Link Hub** (2026-06-08) — [[product-list-Z]] rewritten as a flexible Link Hub (link list at scale, customers + crawlers; homepage + category hubs primary, also PLP/FLP). Block settings `displayType (text|chips) · showDescription · showMore (collapse >5) · columns · groupBySection`; new types **`linkGroup`** (manual | rule source) + **`linkItem`** (label · description · polymorphic target · thumbnail). **Rule sourcing** for at-scale lists (all blogs/helpcenter/wiki/products per subcategory) — `targetType · scope · sort · limit · pinned[]`, label/description read live from targets, empty result hides the group. Targets: subcategory/theme (`pageHomeModular`) · product · brand (`homeBlockTypeC`) · blog (`Page Article`) V1; helpcenter/wiki V2 (manual V1). **Localized** (per-market curation). Anchor = name-not-slug; no schema; H2 + H3 headings; `showMore` resolves the old per-column show-all (Z-4). `bundleGroup` kept as a V1 manual-compat source (~1006 entries); migration owned by content-generation.
- **Block AZ defined + g-url §FLT reconciled** (2026-06-08) — [[filter-engine-AZ]] redesigned (was PARKED): `filterConfig` JSON block on [[pageHomeModular]] (no new page type); **Merchant Catalogue = SSoT** (store keys, resolve labels/counts/products live → config non-localized); fields `categories`·`preFilters`·`shownFilters`·`attributesInDescription`·`printrunPreselected`·`indexableFilters`; **destination-only indexation** (indexable ⟺ unique-content destination ⟺ crawlable link; combinations hand-curated; per-locale via INDEX-1); **readability-rule slug**; **safety net** (engine-owned state · in-session warning incl. agents · 301→core PLP · weekly + OP-56). Algolia + migration out of scope. [[g-url]] §FLT relaxed to match. Build gated on the Merchant-Catalogue API contract.

---

## Part G — Reconciliation / conflict log

Every place the five docs disagreed, and the locked resolution.

| # | Conflict | Resolution |
|---|---|---|
| 1 | **PDP page entry** — master v0.1 said `pageHomeModular` | **`product`** (PLP/FLP = `pageHomeModular`); shared block library + contracts, not the entry type |
| 2 | meta-robots default — PLP req `noindex,follow` · PLP catalog `noindex,nofollow` · PDP per-locale | **`noindex, follow`** default, per-locale field (rule-engine flips qualifiers to index) |
| 3 | Page schema root — PLP `CollectionPage` vs FLP v5 | **Drop `CollectionPage`** → WebPage + BreadcrumbList + ItemList (PLP/FLP); PDP Product/Offer |
| 4 | `attributeLabel` (3 colours) vs PCM Highlight Labels (4) | **One [[card-label]] model**, colours Default/Primary/Design/**Eco**; Most Popular=manual · New=auto<3mo · rest=feed |
| 5 | `Person` referenced, not modelled | **New combined [[person]]** type, all surfaces; expertise sentence on the per-page byline |
| 6 | `faqItem` name collision | canonical Block V leaf = **`faqItem`**; legacy flat → `questionAndAnswer` |
| 7 | productCollection array name | **`items`**, accepts `bundleItem` + `promoCard` |
| 8 | Video on grid cards | **no card video** anywhere; Video standalone, **may be in the PDP hero gallery** |
| 9 | `cta` enum — S=5, D=4 | **one shared `cta` enum** |
| 10 | Anti-cannibalisation (b9-11 duplicated) | lives in the **content-scoring mechanism** ([[g-keywords-scoring]]), once |
| 11 | Block BE — PDP killed (→B16) vs PLP retains | **shared freeform escape hatch, all surfaces, never default**; B16 = separate PDP structured matrix |
| 12 | **USP-bar count — PDP 4 vs PLP/FLP 3** | **4** (as-built; PLP/FLP "3 locked" superseded) |
| 13 | **Reviews — PLP category-level AggregateRating vs FLP "no category-pooled" policy** | **drop the category AggregateRating schema**; show category-relevant reviews via a **tag** (UI only); company rating only |
| 14 | **Content-blocks field name** — `bodyBlocks` vs `Content Blocks` | unify to **`Content Blocks`** on both entry types |
| 15 | **No separate `Category` type** (FLP assumed one) | category node = a `pageHomeModular` |
| 16 | **FLP perf budgets** looser than PDP/PLP | FLP delta: LCP ≤2.5s · INP ≤200ms · CLS ≤0.1 (see [[g-mobile]]) |
| 17 | **Breadcrumb hard-fail** | **V2**; V1 soft-warn + legacy fallback (hard-fail new pages V1) |
| 18 | **PLP DOM order** | **B9 supporting before B8 reviews** (FLP = B8 before B9) |
| 19 | **`target_keywords` shape** | union `{keyword, search_volume, intent_tag, priority, locale}`; no hard cap |
| 20 | **PDP B17** (Pros & Green Claim) omitted in v0.1 | **restored** — Pros V1 KEEP above configurator; Green Claim V2 |
| 21 | **FLP filter engine — PCM vs Algolia source of truth** (was parked) | **Merchant Catalogue = SSoT** (products/taxonomy/attributes); Contentful owns the page (`filterConfig` on [[pageHomeModular]], store keys/resolve live); **destination-only indexation**; Algolia out of scope (platform-catalogue proposal). See [[filter-engine-AZ]] |
| 22 | **Earned-filter URL shape — auto hyphen-suffix vs curated** | curated unique-content destinations use the **readability rule** (primary-keyword/H1 in the locale's natural word order); the auto hyphen-suffix-against-parent rule is relaxed. [[g-url]] §FLT reconciled |

**Open / parked:** the **FLP filter engine** ([[filter-engine-AZ]]) is now **defined** — build gated on the **Merchant-Catalogue API contract** (open ticket, awaits the new product-catalogue system). Card-label "1 badge/tile vs 2" PLP render rule — confirm. `Person.knowsAbout` typing (ref vs string) — build-time.

---

*v0.2 — canonical multi-page model. Hub + content-types/ + contracts/ + surfaces/. Built from PDP Req v0-34 · PLP Req v1-13 · FLP Req v0-15 · PDP Catalog v0.20 · PLP Catalog v1.5, reconciled per the log above. Owner: Niels Molenaar · 2026-06-04. Next: host the folder as a multi-page site (GitHub Pages build); unpark the FLP filter engine.*



# ▌Surfaces


---


*(type: surface · surfaces: [PDP] · status: draft)*


# Surface — PDP (Product Detail Page)

> **Labels (per §8 — DOM blocks):** V1·BUILD ×6 (USP bar, B1 breadcrumb, B4 intro field, B14 schema, URL serialiser, META robots field) · V1·KEEP ×3 (NAV verify-only, B17 Pros, B8 specs) · V1·GUIDELINE ×4 (g-url, g-meta tuning, B12 related, B15 conditional render copy) · MIXED ×4 (B3 hero, B4, B5 configurator, B11 FAQ) · V2 ×6 (B16, B10, B9 reviews, B-PM, B13 chat, B17 Green Claim). Each block tagged `[V1/V2 · BUILD/GUIDELINE/KEEP]` in the DOM table below.

The leaf product page. Page entry = **[[product]]** (NOT `pageHomeModular`). A PDP is always a **leaf**, never a hub/parent. It carries the configurator (B5) and the `Product` JSON-LD stack (B14) — both PDP-exclusive. Reference page: `helloprint.com/en-gb/booklets`.

## Page entry & scalar fields

Entry type: **[[product]]**. Taxonomy parent = `Direct Main Category` (single ref → canonical parent PLP). Key scalars (full model in [[product]]):

- `Url` (per-locale, **no verb**, flat single slug, hyphen-suffix for indexable variants) · `Slug` (cross-locale internal id)
- `meta_title` · `meta_description` · per-locale **meta-robots** (default `noindex, follow`, §3.1) · `canonical` (self, normalised)
- `introParagraph` (B4) · `Description` (B7) · `Pros` / `Pros & Cons` (B17/B7) · Product Keys Specs / Submission specs / templates (B8)
- custom-quantity rules (B5) · `target_keywords` (single source) · `catalogImage` / `productVideo` · Highlight Labels
- `Content Blocks` (renamed from `bodyBlocks`) — the modular block library

## DOM order

Top → bottom (PDP Req §3 "Page contents"). Blocks link to their content-type pages.

| # | Block | What | Content type | Phase · type |
|---|---|---|---|---|
| 1 | URL | URL structure | [[g-url]] | **[V1·GUIDELINE]** · url-11 serialiser [V1·BUILD] · url-12 whitelist [V2·BUILD] |
| 2 | META | Head tags (title/desc/robots/canonical/hreflang) | [[g-meta]] | **[V1·GUIDELINE]** · meta-20 per-locale robots field [V1·BUILD] |
| 3 | NAV (sticky) | Global header anchor nav | (existing header `11m02r7Z2mnj5KDda56HsH`) | **[V1·KEEP]** (verify-only, no new build) |
| 4 | USP bar | **4** brand USPs + Trustpilot, above H1 | [[g-uspbar]] | **[V1·BUILD]** (all 9 rows; NEW SSR component) |
| 5 | B1 Breadcrumb | Taxonomy path + BreadcrumbList | [[breadcrumb]] | **[V1·BUILD]** (walker b1-16/17/19) |
| 6 | B2 H1 | Product name, **no verb**, buyer-language | [[product]] (from `target_keywords`) | **[V1·GUIDELINE]** · b2-19 keyword field [V2·BUILD] |
| 7 | B3 Hero | Gallery 1:1 1500×1500 AVIF/WebP; product video V2 | [[video]] (hero gallery) | **[MIXED]** · gallery [V1·BUILD] · product video b3-18 [V2·BUILD] |
| 8 | B4 Intro | `introParagraph`; **empty → omitted entirely** | [[product]] (`introParagraph`) | **[MIXED]** · field+conditional render [V1·BUILD] · authoring [V2·GUIDELINE] |
| 9 | **B17 In-context USPs** | **Pros (b17-2) + Green Claim (b17-3)** — between B4 and B5 (§3.20) | [[product]] (`Pros`) | **[MIXED]** · Pros [V1·KEEP] · Green Claim [V2·BUILD] · enrichment b17-6 [V2·BUILD] |
| 10 | B5 Configurator + bulk | Conversion engine; AggregateOffer/hasVariant | [[product]] (native section) | **[MIXED]** · 19 rows [V1·BUILD] · 6 KEEP rows [V1·KEEP] · b5-36/44/45 [V2·BUILD] |
| 11 | B7 Product description | Visual + tab integration only; **Pros & Cons at B7 bottom** | [[contentMedia]] | **[V1·KEEP]** (existing copy preserved, visual only) |
| 12 | B8 Specs + Design | Separate tabs (Specs · Design Guidelines) | [[product]] (specs fields) | **[MIXED]** · existing block [V1·KEEP] · additionalProperty + missing schema fields [V2·BUILD] |
| 13 | B16 Detailed specs matrix | Mixam-style structured spec/pricing matrix | (B16 — new, V2) | **[V2·BUILD]** (entire block; b16-7/16-19 anti-cannib = [V2·GUIDELINE]) |
| 14 | B10 Config deep-dive | Educational prose cards per attribute group | (B10 — new, V2) | **[V2]** · b10-1→8 [V2·GUIDELINE] · b10-9/10 [V2·BUILD] |
| 15 | B9 Reviews | Trustpilot product-level; ≥20-review gate; AggregateRating | [[reviews-blockP]] | **[V2·BUILD]** (entire block) |
| 16 | B11 FAQ | Q+A, H3 per Q, FAQPage schema mirror | [[faq-blockV]] | **[MIXED]** · Q+A HTML + FAQPage schema [V1·BUILD] · coverage bins/sourcing/link rules [V2·GUIDELINE] |
| 17 | B12 Related products | 4 siblings, "Other types of [product]" | [[productCollection]] | **[V1·GUIDELINE]** (existing Block D; no BUILD) |
| 18 | PM (B-PM) | Product-manager byline (E-E-A-T test) | [[person]] | **[V2·BUILD]** (test; 6 rows; Person schema) |
| 19 | B15 SEO text | Conditional (above search-volume threshold); position manual | [[contentMedia]] (migrated Block S) | **[MIXED]** · conditional render b15-1 [V1·BUILD] · position b15-2 [V1·GUIDELINE] |
| 20 | B13 Chat & Help | Lazy-loaded after LCP; no SEO weight | — | **[V2·BUILD]** |
| 21 | B14 Product Schema | `Product` JSON-LD (SEO backbone) | [[g-schema]] | **[V1·BUILD]** (all 17 rows; deploy-blocking validation) |

> Page-flow callout (PDP Req): B8 → B16 → B10 → B9 → B11. The numbering (B16/B10/B9) is documentation index, not source-doc order — the DOM order above is authoritative.

## Blocks

- **USP bar** → [[g-uspbar]] — exactly **4** brand USPs (PDP "4" is correct, §3.11); Trustpilot company-level `AggregateRating` in `Organization`; SSR, no headings, not clickable, CLS-safe.
- **B1 Breadcrumb** → [[breadcrumb]] — walker reads `Direct Main Category`; leaf label = H1 (product name, no verb).
- **B3 Hero / video** → [[video]] — video may sit in the PDP hero gallery (§3.7 — do NOT say "never a hero"); author-positioned via `productVideo`.
- **B4 Intro** → `introParagraph` on [[product]]; empty by default → block not rendered (no `<p>`, no spacer).
- **B17** → [[product]] `Pros` (V1) + Green Claim (V2); see §3.20 nuance below.
- **B5 Configurator** → native [[product]] section (not a Content Block).
- **B7 Description / B15 SEO text** → [[contentMedia]] (Block S). B7 = mid-page description (existing copy preserved); B15 = conditional SEO text.
- **B9 Reviews** → [[reviews-blockP]] (`homeBlockTypeP`); product-level Trustpilot, ≥20-review AggregateRating (V2).
- **B11 FAQ** → [[faq-blockV]] (`homeBlockTypeV` + `faqItem`); FAQPage schema exact DOM mirror.
- **B12 Related** → [[productCollection]] (Block D); 4 same-category siblings.
- **PM** → [[person]]; emits `Person` schema; category expertise sentence on the per-page byline.
- **B14 Schema** → [[g-schema]].

## Surface-specific rules

- **No-verb URL + H1 (url-3 / b2-7).** Print-intent verbs live on PLPs only. Breadcrumb leaf = product name, no verb. The PDP is always a leaf — none of the PLP cluster/combining-keyword rules, themed-PLP H1 exception, or hub framing apply.
- **B17 nuance (§3.20).** v0.34 relocated **Pros & Cons to the bottom of B7** and dropped the standalone hero placement; the in-context B17 line (Pros + Green Claim) still renders between B4 and B5 (info column, above the configurator). Pros (b17-2) = `[V1·KEEP]`; Green Claim (b17-3) = `[V2·BUILD]` re-source (carries a stale KEEP tag in the source doc — treat as V2). One B17 component, not two (Seb-Q13 removed the standalone "Sustainable production" block). Represented, never silently dropped.
- **Configurator / variant strategy (B5).** Parent-PDP-only authority. Configurator variants & query URLs `noindex,follow` self-canonical by default; only whitelist (url-12, V2) variants flip to indexable hyphen-suffix PDPs (`/booklets-a5-gloss`), self-canonical. Silent `replaceState` URL transitions; no internal link graph to parameter URLs. `Product.offers` → `AggregateOffer`; `hasVariant`/`isVariantOf` whitelist-only; schema fixed at SSR pre-set price (configurator changes do NOT update schema).
- **Schema (§3.2).** `Product` + `Offer`/`AggregateOffer` + `aggregateRating` (product-level, ≥20) + FAQPage (mirror B11) + BreadcrumbList (mirror B1). Drift = build fail; CI deploy-blocking. No `CollectionPage`. `speakable`/`mainEntity` = V2.
- **Anti-cannibalisation.** The b9-11 PDP↔PLP H2 rule (PLP H2 = action verb; PDP H2 = product-distinguishing attribute) lives in [[g-keywords-scoring]] — GUIDELINE, no CI gate.
- **Performance.** PDP budgets = LCP ≤2.0s · INP ≤150ms · CLS ≤0.05 (see [[g-mobile]]). Mobile content parity (mob-35) — no `display:none` on SEO-bearing elements.

## Sources

- PDP Req v0-34 §3 (DOM order / Page contents), §3.20 (B17 In-context USPs), §B5 (configurator/variant strategy), §B14 + g-meta (schema, no-verb URL), g-uspbar (4 USPs)
- PDP Catalog v0.20 (block→content-type mapping; Block D / S / P / V; video placement)
- _BUILD-BRIEF §2 (PDP entry = product, leaf), §3.1/3.2/3.7/3.11/3.17/3.20

Related: [[product]] · [[surface-PLP]] · [[surface-FLP]] · [[contentMedia]] · [[productCollection]] · [[reviews-blockP]] · [[faq-blockV]] · [[video]] · [[person]] · [[breadcrumb]] · [[g-url]] · [[g-meta]] · [[g-schema]] · [[g-uspbar]] · [[g-mobile]] · [[g-keywords-scoring]]


---


*(type: surface · surfaces: [PLP] · status: draft)*


# Surface — PLP (Product Listing Page)

> **Labels (per §8 — DOM blocks):** V1·BUILD ×8 (USP bar, B2 breadcrumb walker, B3 H1, B4 intro, B5 grid, B9 supporting, B13 FAQ, page schema) · V1·KEEP ×1 (B1 nav verify-only) · MIXED ×4 (B8 reviews, B11 blog, B12 related, B14 SEO text — V1 manual / V2 auto) · V2 ×3 (B6 in-grid card, B7 sub-grid, B15 PM) · BG promo = V1 manual / V2 auto. Each block tagged `[V1/V2 · BUILD/GUIDELINE/KEEP]` in the DOM table.

The category / themed listing page. Page entry = **[[pageHomeModular]]**. Two variants share one skeleton: **product-category PLP** (e.g. *visitekaartjes drukken*) and **themed/use-case PLP** (e.g. *relatiegeschenken*). Taxonomy parent = `parentCategory` (self-ref). A PLP may be a hub/parent.

## Page entry & scalar fields

Entry type: **[[pageHomeModular]]**. Key scalars (full model in [[pageHomeModular]]):

- `Title` → **H1** (primary `target_keywords`; verb when uniquely owned; cluster rule) · `Slug` (cross-locale id)
- `curl`/URL (per-locale, verb-conditional: main/themed hubs no verb, sub-category PLPs with own volume = verb) · `meta_title` (3-slot V1) · `meta_description` (breadth + price CTA)
- `robots_content` (per-locale, default `noindex, follow`, §3.1) · `canonical` (self + override) · `parentCategory` (publish-blocker)
- `introParagraph` (B4, optional/empty by default) · `target_keywords` (single source) · `catalogImage`
- Page Name (was searchName) · Search Settings (was excludeFromSearch) · `analyticsPageTypeVariation` (reporting only)
- `Content Blocks` (renamed from `bodyBlocks`)

## DOM order

Top → bottom (PLP Req §4 §B-block DOM order). **Note the §3.18 rule: B9 supporting renders BEFORE B8 reviews on the PLP** (the FLP order is the reverse — do not copy it here).

| # | Block | What | Content type | Phase · type |
|---|---|---|---|---|
| 1 | USP bar | **4** brand USPs + Trustpilot, above H1 | [[g-uspbar]] | **[V1·KEEP]** (existing live USP bar + Trustpilot; CLS-safe SSR fix [V1·BUILD]) |
| 2 | B1 Sticky anchor nav | 6 grouped buckets + in-page jumps | (header `11m02r7Z2mnj5KDda56HsH`) | **[V1·KEEP]** (existing MENU header; verification only) |
| 3 | B2 Breadcrumb | Full taxonomy path + BreadcrumbList | [[breadcrumb]] | **[V1·BUILD]** (NEW walker + Parent Category publish-blocker) |
| 4 | B3 H1 | Highest-priority commercial keyword; combinable cluster | [[pageHomeModular]] (`Title`) | **[V1·BUILD]** · cluster/copy discipline [V1·GUIDELINE] |
| 5 | B4 Intro | `introParagraph`; optional, empty by default | [[pageHomeModular]] (`introParagraph`) | **[V1·BUILD]** (structure) · copy [V1·GUIDELINE] |
| 6 | **BG promo cards (B10)** | Promo carousel **above the grid** (Home/broad/hub) when ≥1 active — does NOT replace the grid | [[promoCard]] (`homeBlockTypeBG`) | **[V2·BUILD]** (Block BG block is `data-version v2`; existing carousel shell = [V1·KEEP]) |
| 7 | B5 Product grid | Curated PDP tiles; first commercial block; real `<a>` per tile | [[g-pagecard]] / `bundleItem` | **[V1·BUILD]** (two-image DOM cap V1) · auto discount label + hover photography + master migration [V2·BUILD] |
| 8 | B6 In-grid promo/editorial card | One tile-width card inside the grid | [[promoCard]] | **[V2·BUILD]** (`data-version v2`; op-001) |
| 9 | B7 Variant/use-case sub-grid | One intent axis; ≥500 combined volume floor | [[g-pagecard]] | **[V2·BUILD]** (`data-version v2`; op-002; sole earned-filter promotion surface) |
| 10 | **B9 Supporting text + visual** | 2-column; adjacent topic ≥500 vol; **BEFORE B8 (§3.18)** | [[contentMedia]] (Block S) | **[V1·BUILD]** (maps to existing Block S) |
| 11 | B8 Reviews | Trustpilot category widget; ≥20-review render gate | [[reviews-blockP]] | **[MIXED]** · manual SSR [V1·BUILD] · automated collection [V2·BUILD] |
| 12 | B11 Blog/inspiration teaser | Tag-driven; E-E-A-T; empty → omit | [[blog-teaser-AJ]] | **[MIXED]** · manual selection [V1·GUIDELINE] · tag-driven auto + quality gate [V2·BUILD] |
| 13 | B12 Related products | Top 5 same-category cross-sell | [[productCollection]] (Block D) | **[MIXED]** · existing Block D manual [V1·KEEP] · Algolia auto [V2·BUILD] |
| 14 | B13 FAQ | 8–11 Q+A across 8 bins; FAQPage mirror | [[faq-blockV]] | **[V1·BUILD]** · real-signal agent sourcing [V2·BUILD] · coverage/answer discipline [V1·GUIDELINE] |
| 15 | B15 PM authority | Product-manager byline (E-E-A-T test) | [[person]] | **[V2·BUILD]** (fully V2 — content + build + Algolia) |
| 16 | B14 SEO text | Conditional (search-volume gated); bottom, above schema | [[contentMedia]] / [[rich-text-BE]] | **[V1·BUILD]** (conditional render) · LLM-pipeline copy criteria [V1·GUIDELINE] |
| 17 | Page schema | `Organization`+`WebSite`+`SearchAction`+`WebPage`+`BreadcrumbList`+`ItemList` | [[g-schema]] | **[V1·BUILD]** (integrity hard-fail; drift soft-warn V1 → hard-fail V2) |

> **Below-grid editorial blocks** (after B5): B9 Supporting, B8 Reviews, B11 Blog, B12 Related, [[usp-block-BB]] (USP Block), [[brands-blockC]] (Brands), [[rich-text-BE]] (BE freeform), [[product-list-Z]] (Z text-link list), B13 FAQ, B15 PM, B14 SEO text. Linked-image pairs (Block S) and any link-bearing editorial sit below the grid (§B4 no-links-above-grid).

## Blocks

- **USP bar** → [[g-uspbar]] — **4** brand USPs (the PLP/FLP "3 locked" is superseded by §3.11); company-level Trustpilot `AggregateRating`.
- **B2 Breadcrumb** → [[breadcrumb]] — walker reads `parentCategory`; themed PLPs self-rooted (Home › Relatiegeschenken).
- **BG promo** → [[promoCard]] (`homeBlockTypeBG`) — renders **above** the grid (V1, not a replacement). Discount cards Homepage-only.
- **B5 grid** → product tiles. The card component is [[g-pagecard]] (shared with BH/BI nav) / `bundleItem`; one badge per tile (PLP B5 delta — max 1, §3.3); two-state image (catalog + hover).
- **B9 Supporting** → [[contentMedia]] (Block S). H2 carries a secondary keyword; renders before B8.
- **B8 Reviews** → [[reviews-blockP]] — category-relevant via a `tag` (UI-only, NO category-level schema, §3.12); ≥20-review threshold to render.
- **B11 Blog** → [[blog-teaser-AJ]] (`homeBlockTypeAJ`).
- **B12 Related** → [[productCollection]] (Block D) — related *products*. Subcategory/related page-card nav (BI) is decoupled (BH+BI share [[g-pagecard]]).
- **B13 FAQ** → [[faq-blockV]].
- **USP Block / Brands / BE / Z** → [[usp-block-BB]] · [[brands-blockC]] · [[rich-text-BE]] · [[product-list-Z]] — all below-grid editorial.
- **B15 PM** → [[person]]. **B14 SEO text** → [[contentMedia]] / [[rich-text-BE]] for hand-built tables.

## Surface-specific rules

- **H1 verb + cluster (B3).** PLP H1 carries the action verb when uniquely owned (scorer-enforced); may combine 2–3 closely-related keywords only when ALL: secondary ≥60% of primary volume, same intent, would otherwise create a thin sibling. Max 3 (preferred pair). The PDP never combines.
- **Schema (§3.2).** NO `CollectionPage`. Sitewide `Organization`+`WebSite`+`SearchAction` + `WebPage` + `BreadcrumbList` + `ItemList` (one ListItem per B5 tile; B12 cross-sell appends to the same ItemList; B11 blog = separate article ItemList). ItemList **only on indexable canonical URLs**; omit on pages 2+, empty-state, non-earned filter. Spam guardrail: every schema field maps to visible DOM. See [[g-schema]].
- **Index rules.** INDEX-1 flips qualifying pages to `index,follow` (volume ≥20, keywords filled, no cannibalisation, grid ≥4 tiles, FAQ ≥5 or SEO text, URL compliant, locale authored). See [[g-meta]].
- **Reviews schema (§3.12).** Drop the category-level `AggregateRating` schema; show category-relevant reviews via a `tag` (Trustpilot widget, UI-only). Only company-level rating (USP bar / `Organization`) emits schema.
- **DOM-order delta (§3.18).** B9 supporting BEFORE B8 reviews. FLP is the reverse.
- **Performance.** PLP budgets = LCP ≤2.0s · INP ≤150ms · CLS ≤0.05 (see [[g-mobile]]). No configurator / cart on mobile — tap tile → PDP.

## Sources

- PLP Req v1-13 §2 (B1–B15 + g- blocks + themed variant), §4 (§B-block DOM order with the B9-before-B8 note)
- PLP Catalog v1.5 (page-field decisions; BG above grid; below-grid editorial blocks; B12/BI decoupling; reviews tag)
- _BUILD-BRIEF §2 (PLP entry = pageHomeModular), §3.1/3.2/3.3/3.11/3.12/3.18

Related: [[pageHomeModular]] · [[surface-PDP]] · [[surface-FLP]] · [[contentMedia]] · [[productCollection]] · [[reviews-blockP]] · [[faq-blockV]] · [[blog-teaser-AJ]] · [[promoCard]] · [[g-pagecard]] · [[usp-block-BB]] · [[brands-blockC]] · [[rich-text-BE]] · [[product-list-Z]] · [[person]] · [[breadcrumb]] · [[g-meta]] · [[g-schema]] · [[g-uspbar]] · [[g-mobile]] · [[g-keywords-scoring]]


---


*(type: surface · surfaces: [FLP] · status: draft)*


# Surface — FLP (Filter Listing Page)

> **Labels (per §8 — DOM blocks):** V1·BUILD ×11 (USP bar, B2 breadcrumb, B2b taxonomy tree, B3 H1, B4 intro, F1 filter panel, F2 controls, B5 grid, F3 pagination, B13 FAQ, B14 SEO text, F4 empty-state, page schema — F1–F4 render-only consuming PARKED AZ) · V1·KEEP ×1 (B1 nav verify-only) · MIXED ×3 (B8 reviews, B11 blog, B12 related) · V2 ×3 (B6 in-grid card, B7 sub-grid deferred, B15 PM) · AZ filter-engine model = **PARKED** (§3.23). Each block tagged `[V1/V2 · BUILD/GUIDELINE/KEEP]` in the DOM table.

A faceted category listing page. Page entry = **[[pageHomeModular]]** (same as the PLP). An **FLP is a PLP** whose `Content Blocks` include the AZ "Advanced Pre-filters" filter engine ([[filter-engine-AZ]] — **PARKED**, §3.23). The base FLP H1 is a **bare-noun category** (e.g. `/printed-water-bottles`). There is **NO separate `Category` content type** — taxonomy nodes are `pageHomeModular` entries.

It **inherits the PLP below-grid blocks** (B8/B9/B11/B12/B13/B14/B15 + USP Block / Brands / BE / Z) and adds the FLP-only filter chrome: the B2b category-taxonomy tree, the F1 filter panel, the F2 controls strip, F3 pagination, and the F4 empty-state. **F1–F4 + the grid selection are render-only** (they consume AZ), NOT Contentful content-blocks.

## Page entry & scalar fields

Entry type: **[[pageHomeModular]]** (+ the AZ block in `Content Blocks`). Same scalars as the PLP (see [[pageHomeModular]]):

- `Title` → **H1** (base FLP = bare-noun category; earned-filter URL H1 hand-authored per its keywords) · `Slug`
- `curl`/URL (per-locale, flat kebab-case, **bare-noun**, no verb) · `meta_title` · `meta_description`
- `robots_content` (per-locale, default `noindex, follow`, §3.1) · `canonical` (self) · `parentCategory` (publish-blocker)
- `introParagraph` · `target_keywords` · `catalogImage` · Page Name · Search Settings · `analyticsPageTypeVariation`
- `Content Blocks` — **includes the AZ filter engine** ([[filter-engine-AZ]])

## DOM order

Top → bottom (FLP Req "FLP page contents"). **The FLP order is B8 reviews BEFORE B9 supporting** (the reverse of the PLP, §3.18 — do not copy the PLP order here).

| # | Block | What | Content type | Phase · type |
|---|---|---|---|---|
| 1 | USP bar | **4** brand USPs + Trustpilot, above H1 | [[g-uspbar]] | **[V1·KEEP]** · CLS-safe widget contract (FLP rows) [V2·BUILD] |
| 2 | B1 Sticky anchor nav | Global bucket nav | (header `11m02r7Z2mnj5KDda56HsH`) | **[V1·KEEP]** (existing header; verification only) |
| 3 | B2 Breadcrumb | Taxonomy path; earned filter = leaf | [[breadcrumb]] | **[V1·BUILD]** (mandatory SSR; schema mirror; Approach C) |
| 4 | **B2b Category taxonomy tree** | Path-aware accordion, within-bucket FLP nav; all branches crawlable `<a>` in SSR | [[pageHomeModular]] nodes (no separate Category type) | **[V1·BUILD]** (FLP-only; SSR'd crawlable tree) |
| 5 | B3 H1 | Bare-noun base; earned-filter H1 per its keywords | [[pageHomeModular]] (`Title`) | **[V1·BUILD]** · earned-filter copy [V1·GUIDELINE] |
| 6 | B4 Intro | `introParagraph`; show-more; unique per indexed URL | [[pageHomeModular]] (`introParagraph`) | **[V1·BUILD]** (structure) · copy [V1·GUIDELINE] |
| 7 | **F1 Filter panel** | Faceted nav (render-only, consumes AZ); SSR `<a>`/`<button>` per earned-state | [[filter-engine-AZ]] (PARKED) | **[V1·BUILD]** (render-only; AZ model PARKED §3.23) |
| 8 | **F2 Controls strip** | Count · chips · sort · per-page; sticky compressed bar | (render-only) | **[V1·BUILD]** (render-only) |
| 9 | B5 Product grid | 24 default, 4×N; real `<a>` per card → PDP | [[g-pagecard]] / `bundleItem` | **[V1·BUILD]** · auto label + hover photography [V2·BUILD] |
| 10 | B6 Promo/editorial card | One cell-width card (replaces a product, never adds) | [[promoCard]] | **[V2·BUILD]** |
| 11 | **F3 Pagination / load-more** | "Load more" + crawlable numbered graph; pages 2+ `noindex,follow` | (render-only) | **[V1·BUILD]** (render-only; LOCKED v0.6 OP-46) |
| 12 | B7 Shop-by-attribute sub-grid | Per-attribute deep-dive | [[g-pagecard]] | **[V2·BUILD]** (DEFERRED v0.8; authoring + render both V2) |
| 13 | **B8 Reviews** | Trustpilot Org (A) + category widget (B, UI-only no schema); **BEFORE B9** | [[reviews-blockP]] | **[MIXED]** · Surface A+B [V1·BUILD] · Surface C per-card [V2·BUILD] |
| 14 | B9 Supporting text + visual | 2-column; ≥500 vol gate | [[contentMedia]] (Block S) | **[V1·BUILD]** · hand-authored copy [V1·GUIDELINE] |
| 15 | B11 Blog/inspiration teaser | Tag-driven; variant pages only if variant-tagged | [[blog-teaser-AJ]] | **[MIXED]** · manual selection [V1·GUIDELINE] · tag-driven auto [V2·BUILD] |
| 16 | B12 Related sibling categories | Peer PLPs/FLPs (not earned variants) | [[productCollection]] (Block D) | **[MIXED]** · existing Block D manual [V1·KEEP] · dynamic [V2·BUILD] |
| 17 | B13 FAQ | Unique per indexed URL; 8 bins; FAQPage mirror | [[faq-blockV]] | **[V1·BUILD]** · hand-authored copy [V1·GUIDELINE] |
| 18 | B14 SEO text | Unique per indexed URL; bottom, above schema | [[contentMedia]] / [[rich-text-BE]] | **[V1·BUILD]** · hand-authored copy [V1·GUIDELINE] |
| 19 | B15 PM (V2 test) | Product-manager byline; `Person` schema | [[person]] | **[V2·BUILD]** (cohort-vs-control test) |
| 20 | **F4 Empty state** | HTTP 200 + parent chrome + single "Clear all filters" CTA (render-only) | (render-only) | **[V1·BUILD]** (render-only; OP-45) |
| 21 | Page schema | Sitewide + BreadcrumbList + ItemList (indexable canonical only) | [[g-schema]] | **[V1·BUILD]** (g-schema v5; no CollectionPage) |

> The "Blog (dropped)" note in the FLP contents list is superseded — B11 was **re-added v0.6** and renders per the PLP §b11 rules (variant pages only carry variant-tagged blogs).

## Blocks

- **B2b taxonomy tree** → built from `pageHomeModular` taxonomy nodes (same entries the [[breadcrumb]] walker reads — single source of truth; no separate Category model, §2). Within the **current L1 bucket only**; path-aware accordion; every branch URL is a crawlable `<a>` in the initial SSR HTML (closed branches CSS-hidden, never lazy-loaded). No `SiteNavigationElement` schema.
- **F1 / F2 / F3 / F4** → render-only consumers of [[filter-engine-AZ]] (AZ "Advanced Pre-filters"); **PARKED** (§3.23). F1 facet values render as `<a>` (earned) or `<button>` (non-earned) or `<span aria-disabled>` (zero-result). F3 pages 2+ drop BreadcrumbList + ItemList.
- **B5 grid** → [[g-pagecard]] / `bundleItem` cards; colour-swatch swap (CSS sibling `<img>`, no JS src swap); labels overlay max 2; card metadata from AZ "Attributes in description" (V1 manual, max 2).
- **B8 Reviews** → [[reviews-blockP]] — Surface A (Org widget) + Surface B (category widget, **UI-only, no schema**, §3.12). Surface C (per-card ratings) = V2.
- **B9 / B11 / B12 / B13 / B14 / B15** → inherited from the PLP: [[contentMedia]] · [[blog-teaser-AJ]] · [[productCollection]] · [[faq-blockV]] · [[person]]. Each indexed URL (base + each earned variant) carries unique B4/B9/B13/B14 content.

## Surface-specific rules

- **Filter engine PARKED (§3.23).** [[filter-engine-AZ]] (AZ `homeBlockTypeAZ` + `filterSettings`) is the only Contentful piece; everything F1–F4 is render-only. Capture-as-is, flag everything PARKED pending the product-catalog-system decision. AZ known fields: `taxonomy · facetsToDisplay→filterSettings[] · advancedPreFilters→filterSettings[] · attributesInDescription→filterSettings[] · printrunPreselected · algoliaIndex`; `filterSettings`: `filterType (bool) · facet · title · filterDisplayType · filterCategory`. Facet values + counts from PCM / Algolia.
- **Earned-variant routing PARKED.** Earned filters are separate [[pageHomeModular]] entries with a parent-FLP ref + applied-facets ref (**to define** — parked). Their existence IS the earned-state signal. Slug = hyphen-suffix against the parent FLP (`/printed-water-bottles-aluminium`), self-canonical `index,follow`. Non-earned state = client-side `pushState` query-param URL (200, no separate page identity). See [[g-url]].
- **Schema (§3.2, FLP g-schema v5).** NO `CollectionPage`. Sitewide `Organization`+`WebSite`+`SearchAction` + `BreadcrumbList` + `ItemList`. ItemList **only on canonical + indexable URLs** (root, earned-filter, page 1); omit on pages 2+, empty-state, non-earned filter. Minimal Product embedding (url/name/image only) — spam guardrail. See [[g-schema]].
- **DOM-order delta (§3.18).** FLP = B8 reviews before B9 supporting. The PLP is the reverse.
- **Performance — FLP budget is LOOSER (§3.16).** LCP ≤2.5s · INP ≤200ms · CLS ≤0.1 (Moto G4 / throttled 4G) vs PDP/PLP LCP ≤2.0s · INP ≤150ms · CLS ≤0.05. Stated in [[g-mobile]]. Sticky F2 bar uses `position: sticky` (not `fixed`) to avoid disturbing LCP detection.
- **Cache.** Whole-page Cloudflare cache + stale-while-revalidate; cache-key = URL + locale + currency + segment + VAT; event-driven purge. See [[cache]].

## Sources

- FLP Req v0-15 (FLP page contents / DOM order; §B2b taxonomy tree; F1 filter panel + AZ field shape; F2 controls; F3 pagination; F4 empty state; g-schema v5; g-mobile CWV budgets; B12 peer PLPs)
- PLP Req v1-13 (inherited below-grid blocks B8/B9/B11/B12/B13/B14/B15)
- _BUILD-BRIEF §2 (FLP = PLP whose Content Blocks include AZ; no Category type; earned variants), §3.2/3.12/3.16/3.18/3.23

Related: [[pageHomeModular]] · [[surface-PLP]] · [[surface-PDP]] · [[filter-engine-AZ]] · [[contentMedia]] · [[productCollection]] · [[reviews-blockP]] · [[faq-blockV]] · [[blog-teaser-AJ]] · [[g-pagecard]] · [[promoCard]] · [[person]] · [[breadcrumb]] · [[g-url]] · [[g-schema]] · [[g-uspbar]] · [[g-mobile]] · [[cache]] · [[g-keywords-scoring]]



# ▌Content types


---


*(id: product · type: content-type · surfaces: [PDP] · status: draft)*


# product (PDP page entry)

> **Labels:** V1·BUILD ×6 (meta-robots field, target_keywords field, Content Blocks rename, productVideo, breadcrumb-walker reads, alt-text rewire) · V1·KEEP ×3 (Pros, Pros & Cons → B7, B8 specs source) · V1·GUIDELINE ×5 (Url, meta_title, meta_description, canonical, Description) · V2·BUILD ×4 (alwaysShow, B16 matrix-config, GP-bias weighting, url-12 whitelist) · REMOVED ×1 (shouldShowPerShop). Axes per §8: **Phase** V1/V2/MIXED · **Type** BUILD/GUIDELINE/KEEP.

The Contentful entry type for a **Product Detail Page**. It carries the product-data fields, the page-level SEO scalars, and a **`Content Blocks`** field that references the shared modular block library. It also hosts the configurator (B5) and emits `Product` JSON-LD (B14).

**Critical:** the PDP page entry is `product`, **NOT `pageHomeModular`** (that is the PLP/FLP entry — see [[pageHomeModular]]). A PDP is always a **leaf**, never a hub/parent.

## How it works in Contentful

An SEO author opens (or creates) a `product` entry. The product-data fields (`presetPath`, quantity rules, `Pros`, specs, `catalogImage`) drive the configurator and the static commercial surface; the SEO scalars (`Url`, `Slug`, `meta_title`, `meta_description`, per-locale meta-robots, `canonical`, `target_keywords`) drive indexation and head tags; the `Content Blocks` field (renamed from `bodyBlocks`, §3.13) holds an author-curated, ordered list of modular blocks (the same library `pageHomeModular` references). Taxonomy parent = **`Direct Main Category`** (single ref), which the breadcrumb walker reads.

The page renders in a fixed DOM order (see [[surface-PDP]]); the configurator is a native section, not a Content Block. H1, meta title and meta description are sourced from the `target_keywords` set, not authored as free template literals (b2-12).

## Field model

| field | type | localized? | phase/type | notes |
|---|---|---|---|---|
| `Url` | String (slug) | yes (per-locale) | `[V1·GUIDELINE]` | Per-locale URL slug. **No verb** (verbs only on PLPs, url-3/b2-7). Flat single product slug — never a sub-folder hierarchy (`/booklets/a5/gloss` forbidden). ≤75 chars. Hyphen-suffix for indexable variants (`/booklets-a5-gloss`). url-11 hyphen-serialiser enablement = `[V1·BUILD]`. |
| `Slug` | String | no | `[V1·BUILD]` | **Canonical cross-locale internal identifier** — same across all markets, language-agnostic, **not crawler-facing** (the per-locale `Url` carries the SEO). Kept separate from `Url` (Niels; reversed the v0.6 merge proposal). New CMS field. |
| `meta_title` | String | yes | `[V1·GUIDELINE]` | Pattern `[product name] [verb] | HelloPrint [country-code]`; ≤60 chars (target 55); unique; country code in suffix only. Sourced from `target_keywords`. |
| `meta_description` | String | yes | `[V1·GUIDELINE]` | From-price / lead time / USP; ≤155 chars; primary + secondary keyword; most important info in first 110 chars. Concrete CTA. |
| meta-robots (per-locale) | Enum | yes (per-locale) | `[V1·BUILD]` | **NEW locale-aware field (meta-20).** Storefront emits matching `<meta name="robots">`. **Default `noindex, follow`** (§3.1); index rule-engine flips qualifying pages to `index,follow`. Per-locale value itself = `[V1·GUIDELINE]` (Needs-Content, SEO ops). |
| `canonical` | String/URL override | yes (per-locale) | `[V1·GUIDELINE]` | Self-canonical by default, normalised (HTTPS, no-www, no trailing slash, lowercase, tracking params stripped). Editable per-locale override. Never used to consolidate cannibalising siblings (meta-12). Normalisation/build-time validation = `[V1·BUILD]`. |
| `Direct Main Category` | Link to Entry (`pageHomeModular`) | no | `[V1·BUILD]` | **Single reference → canonical parent PLP.** Breadcrumb walker reads this and walks each parent's `parentCategory` up to the locale Homepage entry (b1-16/b1-17). Missing / non-terminating chain = build failure for NEW pages in V1 (§3.17); hard-fail = `[V2·BUILD]`. |
| `introParagraph` | RichText | yes | `[MIXED]` | **NEW (B4, HEL-294).** Field + conditional render = `[V1·BUILD]`; content authoring = `[V2·GUIDELINE]`. Customer-facing intro under H1. Optional, **empty by default → block not rendered at all** (no empty `<p>`, no spacer). Show-more behaviour. Maps to B4 — NOT Block S. |
| `Description` | RichText / Block S | yes | `[V1·KEEP]` | Body copy beneath the configurator (B7 product description). Existing copy preserved in V1 (visual + tab integration only, no rewrite). Authored via [[contentMedia]] in `Content Blocks`. |
| custom-quantity rules | Object (min · max · increment) | — | `[V1·BUILD]` | Per product category (b5-22). E.g. Booklets min 25 / max 50,000 / inc 1; Cards min 50 / max 100,000 / inc 50. Drives configurator quantity validation. |
| `Pros` | String[] | yes | `[V1·KEEP]` | KEEP — drives B17 Pros lines (b17-2, V1). Locale-aware. V2: superseded by product-feed USP enrichment (b17-6) = `[V2·BUILD]`. |
| `Pros & Cons` | field | yes | `[V1·KEEP]` | Source for the Pros & Cons rendered at the **bottom of B7** (Seb-Q3, relocated out of the hero column). Cons retained at field level here (note: the catalog dropped Cons from `productBullet`). |
| Product Keys Specs | field | yes | `[V1·KEEP]` | **B8 Specifications** source (Seb-Q12); existing block replicated, visuals redesigned. |
| Submission specs | field | yes | `[V1·KEEP]` | **B8 Design Guidelines** source (Seb-Q12). |
| templates | field | yes | `[V1·KEEP]` | **B8 Design Guidelines templates** source (Seb-Q12). |
| `target_keywords` | Array `{keyword, search_volume, intent_tag, priority, locale}` | per-locale | `[MIXED]` | **Single source of truth (§3.19).** Field as locale-aware array (b2-19) = `[V2·BUILD]` (manual curation OK in V1); usage as single source feeding H1/Meta/FAQ/B14/scorer = `[V1·GUIDELINE]`. `search_volume` read-only from Ahrefs (weekly). `priority` is load-bearing. No hard cap. |
| `Content Blocks` | Array, Link to Entry (polymorphic block library) | — | `[V1·BUILD]` | **Renamed from `bodyBlocks` (§3.13).** Author-curated, ordered. References the shared modular blocks ([[contentMedia]] · [[productCollection]] · [[faq-blockV]] · [[reviews-blockP]] · [[video]] · [[rich-text-BE]] · [[person]] etc.). |
| Highlight Labels | Multi-Link → `attributeLabel` | — | `[V1·KEEP]` | Card/tile labels (see [[card-label]]). Keep with 4 brand-token colours; merged label model (§3.3). Auto-source for non-editorial label types = `[V2·BUILD]`. |
| `catalogImage` | Link to Asset | yes | `[V1·KEEP]` | Canonical product image (chain `catalogImage → productImages[0]`). Feeds `Product.image` + Shopping feed. |
| `productVideo` | Link to Entry (`video`) | optional | `[V2·BUILD]` | **NEW (b3-18).** Author-positioned hero-gallery video reference (NOT hard-coded position 2). See §3.7 — video may sit in the PDP hero gallery. |
| `presetPath` | String | yes, optional | `[V1·KEEP]` | Configurator preset path; resolves to qty + total + per-piece price (from Mongo) (b5-19). |
| `productBullet` / `infoIcons[]` | Multi-Link | — | `[V2·BUILD]` | USP / Info icon column (B17 / §11). §8 USP & Pros **dropped from V1** → V2 platform-catalog-driven (`productBullet` tone field is the V2 home). |
| `alwaysShow` | String[] | — | `[V2·BUILD]` | **V2 (b5-45).** Product-template-level list of attributes that always render regardless of option count. |
| B16 `matrix-config` | field | — | `[V2·BUILD]` | **V2 (b16-9).** Editorial selection of which combinations render per matrix per product family. |
| GP-bias per-attribute weighting | config | — | `[V2·BUILD]` | **V2 (b5-44).** For the recommendation engine. |
| url-12 indexation whitelist | model (Attribute Group · Value · Product Family) | — | `[V2·BUILD]` | Default `noindex`; only explicit entries flip a variant to `index`. Keyed per family. Starts empty; deferred to V2. |
| ~~`shouldShowPerShop`~~ | — | — | REMOVED | **REMOVED** — per-shop visibility → language/locale level (§3.15). |

> **Alt-text rewire (Seb-Q1)** `[V1·BUILD]`**:** the legacy `Product` content type hardcodes the page title into `<img alt>` (alt-text spam). Must be rewired to read **Asset → Title** (as `PCM Product` already does correctly). Affects every asset on the page.

## Per-surface usage & deltas

- **PDP only.** `product` is the PDP page entry exclusively. It carries the configurator (B5) and the `Product` JSON-LD stack (B14) that no other surface emits. See [[surface-PDP]] for the full DOM order.
- The **configurator (B5)** is the conversion engine (19 V1 BUILD rows) `[V1·BUILD]` (MIXED block; V2 rows b5-36/b5-44/b5-45): URL-state sync, hydration, indexable-variant transition, `AggregateOffer`/`hasVariant` schema, custom-quantity, sticky cart panel, anti-dilution. KEEP sub-rows: b5-1/b5-19/b5-27/b5-33/b5-35/b5-37 = `[V1·KEEP]`. It is a native section, not a Content Block.
- **B17 (In-context USPs — Pros & Green Claim)** sits between B4 and B5: Pros (b17-2) = `[V1·KEEP]`; Green Claim (b17-3) = `[V2·BUILD]`; Pros & Cons relocated to the bottom of B7. See [[surface-PDP]].

## Requirements behaviour

- **Indexation (url-5/6/7).** Crucial PDPs (first 12 of any PLP they sit on) always `index,follow`. Non-crucial PDP falls back to `noindex,follow` when ALL hold: (1) combined+primary keyword volume < 20/month, (2) not in first 12 of any PLP, (3) revenue < €10,000 in last 6 months. Configurator variants & query URLs not indexed unless on the Contentful indexation whitelist (url-12, V2). Strong variant demand → hyphen-suffix dedicated PDP, self-canonical.
- **Schema (B14, §3.2).** Emits `Product` + `Offer`/`AggregateOffer` (lowPrice/highPrice/offerCount; `hasVariant`/`isVariantOf` whitelist-only) + `aggregateRating` (product-level, ≥20 reviews) + FAQPage (mirror of B11) + BreadcrumbList (mirror of B1). Schema fixed at SSR pre-set price — configurator changes do NOT update schema (b5-21). Drift between displayed and structured data = build failure; CI validation deploy-blocking. See [[g-schema]].
- **Breadcrumb walker (§3.17).** Reads `Direct Main Category` (single ref), walks parents' `parentCategory` to the locale Homepage entry. Hard-fail for NEW pages in V1; soft-warn + legacy fallback for existing.
- **Mobile content parity (mob-35).** No `display:none` on SEO-bearing elements (H1, H2/H3, breadcrumb, B4, B17 Pros/Green Claim, B7, B8, B11 Q+A, B15, B12 tile names, B14 JSON-LD, alt text). Same DOM mobile + desktop.
- **Empty states.** `introParagraph` empty → B4 omitted entirely. Sustainable-production standalone block removed; one B17 component, not two (Seb-Q13).
- **Voice.** Forbidden vocabulary (elevate / transform / unlock / experience / discover); no em-dashes; `{{shop_name}}` template variable, never hardcode "Helloprint" (multi-brand: Helloprint / Drukzo / WLS).

## Decisions (locked)

- **§2** — PDP entry = `product` (NOT `pageHomeModular`); PDP is always a leaf, never a hub; taxonomy parent = `Direct Main Category` (single ref).
- **§3.13** — the modular-blocks field is `Content Blocks` (rename `bodyBlocks` → `Content Blocks`); author-curated.
- **§3.1** — meta-robots per-locale, default `noindex, follow` (Niels overrides the PLP-catalog `nofollow` correction).
- **§3.19** — `target_keywords` shape `{keyword, search_volume, intent_tag, priority, locale}`; `priority` load-bearing; read-only `search_volume`; no hard cap.
- **§3.20** — B17 (Pros V1 / Green Claim V2); Pros & Cons relocated to B7 bottom; standalone hero placement dropped — represented in [[surface-PDP]], not silently dropped.
- **§3.3 / §3.2 / §3.17** — Highlight Labels (merged card-label model, 4 colours); Product JSON-LD stack; breadcrumb walker.

## Open points

- Per-locale meta-robots value is **Needs-Content** (SEO ops decides per locale). The index rule-engine that flips `noindex,follow` → `index,follow` is defined in [[g-meta]] / the index rules, not here.
- url-12 indexation whitelist (Attribute Group · Value · Product Family) deferred to V2.
- §8 USP & Pros descoped from V1 (HEL-295); V2 platform-catalog-driven. `productBullet` tone field (USP · Pro · Info; Cons dropped) is the V2 home.

## Sources

- PDP Req v0-34 §2 (Product content type fields), §4 (page-level scalars), §3 (DOM order)
- PDP Catalog v0.20 §4 (Sebastiaan's 14 page-field columns; Slug stays separate; introParagraph; Description)
- _BUILD-BRIEF §2 (page-entry model), §3.1/3.2/3.3/3.13/3.17/3.19/3.20

Related: [[surface-PDP]] · [[pageHomeModular]] · [[contentMedia]] · [[productCollection]] · [[faq-blockV]] · [[reviews-blockP]] · [[video]] · [[person]] · [[card-label]] · [[g-url]] · [[g-meta]] · [[g-schema]] · [[breadcrumb]] · [[g-keywords-scoring]]


---


*(id: pageHomeModular · type: content-type · surfaces: [PLP, FLP] · status: draft)*


# pageHomeModular (PLP / FLP page entry)

> **Labels:** V1·BUILD ×7 (Title→H1, Slug, robots_content field, parentCategory publish-blocker, target_keywords field, Content Blocks rename, per-page overrides) · V1·GUIDELINE ×6 (curl/URL, meta_title, meta_description, canonical, Page Name, Search Settings) · MIXED ×1 (introParagraph) · V1·KEEP ×1 (catalogImage) · NEUTRAL ×1 (analyticsPageTypeVariation — reporting only) · KILLED ×6 (topBlock, searchImage, searchUsp, searchTags, Visual Options) + REMOVED ×1 (shouldShowPerShop). Axes per §8: **Phase** V1/V2/MIXED · **Type** BUILD/GUIDELINE/KEEP.

The Contentful entry type for **listing pages** — both the **PLP** (product-category and themed/use-case landing pages) and the **FLP** (filter listing pages). It carries the page-level SEO scalars and a **`Content Blocks`** field referencing the shared modular block library. Taxonomy parent = **`parentCategory`** (self-ref to another `pageHomeModular`).

A **FLP is a PLP** whose `Content Blocks` include the AZ "Advanced Pre-filters" filter engine ([[filter-engine-AZ]], PARKED). There is **NO separate `Category` content type** — a category/taxonomy node IS a `pageHomeModular` (the FLP doc's "Category" assumption is resolved here, not built). See [[surface-PLP]] and [[surface-FLP]].

## How it works in Contentful

An author opens (or creates) a `pageHomeModular`. The `Title` field is repurposed as the **customer-facing H1** (must satisfy the §B3 keyword/cluster/uniqueness contract — not free-form copy); the internal-identification role moves to the universal `Slug`. SEO scalars (`curl`/URL, `meta_title`, `meta_description`, `robots_content`, `canonical`, `target_keywords`) drive indexation and head tags. `parentCategory` (single ref) feeds the breadcrumb walker. The `Content Blocks` field (renamed from `bodyBlocks`, §3.13) holds the author-curated ordered list of modular blocks. The page renders in a fixed DOM order (see [[surface-PLP]] / [[surface-FLP]]).

Every page is governed by the autonomous index rule-engine (INDEX-1 / NOINDEX rules), which runs daily and flips qualifying pages between `noindex,follow` and `index,follow`.

## Field model

| field | type | localized? | phase/type | notes |
|---|---|---|---|---|
| `Title` → **H1** | String | yes | `[V1·BUILD]` | **Repurposed as the single page H1** (first header in DOM). Must satisfy §B3: primary `target_keywords`, cluster rule (combine ≤3 only when secondary ≥60% of primary, same intent, avoids thin sibling), uniqueness. Replaces killed Block AC's H1 role. Cluster/copy discipline = `[V1·GUIDELINE]`. |
| `Slug` | String | no | `[V1·BUILD]` | **NEW shared cross-locale internal identifier** (PDP parity) — stable, same across markets, **not crawler-facing**. Takes the CMS-housekeeping role the old internal `Title` had. |
| `curl` / URL | String (slug) | yes (per-locale) | `[V1·GUIDELINE]` | Per-locale flat kebab-case slug under `/{lang}-{country}/`; ≤75 chars; no folder paths. **Verb conditional**: main categories + themed hubs = no verb (`/visitekaartjes`); sub-category PLPs with own volume = verb (`/visitekaartjes-drukken`). Explicitly authored per locale (else PRES-8693 fallback). FLP base = bare-noun. Pipeline rejection of non-compliant new URLs = `[V1·BUILD]`. |
| `meta_title` | String | yes | `[V1·GUIDELINE]` | V1 3-slot `[Primary] | HelloPrint [cc]`; 4-slot USP slot + Selection Engine + USP library = `[V2·BUILD]`. ≠ H1; unique (hard fail on duplicate). |
| `meta_description` | String | yes | `[V1·GUIDELINE]` | From-price / lead-time / USP; ≤155 chars; primary + secondary keyword; first 110 chars load-bearing. PLP CTA = breadth + price ("Compare 5 binding types from £12") — not the PDP conversion CTA. |
| `robots_content` (meta-robots) | Enum | yes (per-locale) | `[V1·BUILD]` | **Per-locale required field** (pipeline rejects publish if any active locale missing). **Default `noindex, follow`** (§3.1; Niels overrides the PLP-catalog `nofollow` correction). No fallback to parent locale (PRES-8693 chain does NOT apply). Per-locale value itself = `[V1·GUIDELINE]` (Needs-Content). |
| `canonical` | String/URL override | yes (per-locale) | `[V1·GUIDELINE]` | Self-canonical by default + editable per-locale override; normalised. Never to sibling/hub/parent. Normalisation + build-time validation (resolves 200, matches sitemap) = `[V1·BUILD]`. |
| `parentCategory` | Link to Entry (`pageHomeModular`) | no | `[V1·BUILD]` | **Self-ref single reference** to the taxonomy node one level above; names localised by the walker. **Contentful publish-blocker** for NEW PLPs (V1). Feeds the breadcrumb walker (chain → locale Homepage entry). |
| `introParagraph` | RichText | yes | `[MIXED]` | **NEW (B4, HEL-294; shared with PDP).** Field + structure = `[V1·BUILD]`; content = `[V1·GUIDELINE]`. Customer-facing description under H1. Optional, empty by default; visible 2 lines mobile / 4 desktop with show-more (full text always in DOM); ~100 words max; never contains links. Replaces killed Block AC's description role. |
| `target_keywords` | Array `{keyword, search_volume, intent_tag, priority, locale}` | per-locale | `[V1·BUILD]` | **Single source of truth (§3.19).** Field + read-only Ahrefs/GSC write + scorer/index-engine consumption all V1 BUILD on the PLP (unlike PDP's V2 field). Feeds H1 / Meta / B8 H2 / B11 / B13 FAQ / B14 SEO text / schema + index rule-engine. 1 primary + 1–5 secondaries (cap 6; beyond → split). `priority` load-bearing. Composition cap = `[V1·GUIDELINE]`. |
| `catalogImage` | Link to Asset | yes | `[V1·KEEP]` | Always Contentful; chain `catalogImage → images[0] → bundleItem.photo`; two-state default + hover. Card-image fallback when this PLP is linked as a card. |
| **Page Name** (was `searchName`) | String | yes | `[V1·GUIDELINE]` | Renamed. Short human label for the on-site search bar (no SEO keywords unless needed), e.g. "Labels on Roll". Also the card-title fallback. Author-selected V1; V2 from Product Catalog System = `[V2·BUILD]`. |
| **Search Settings** (was `excludeFromSearch`) | Enum (2) | — | `[V1·GUIDELINE]` | Renamed. Include in Search / Exclude in Search (on-site bar; **independent of Google meta-robots**; Exclude reserved for test/internal/staging, reason logged). |
| `analyticsPageTypeVariation` | Enum | — | `[V1·GUIDELINE]` [inferred] | **Analytics / reporting only — NOT logic.** Values: Main Category Page · Category Landing Page · Industry Page · Themed Page · Filter Landing Page. Every `pageHomeModular` has uniform block eligibility — no page-type gating in V1. (Maps to the doc's "page-type flag" — non-logic, reporting; conservative GUIDELINE inference.) |
| `Content Blocks` | Array, Link to Entry (polymorphic block library) | — | `[V1·BUILD]` | **Renamed from `bodyBlocks` (§3.13).** Author-curated, ordered. References the shared modular blocks ([[contentMedia]] · [[productCollection]] · [[reviews-blockP]] · [[faq-blockV]] · [[usp-block-BB]] · [[brands-blockC]] · [[blog-teaser-AJ]] · [[product-list-Z]] · [[rich-text-BE]] · [[person]] · [[filter-engine-AZ]] etc.). FLP = a `pageHomeModular` whose Content Blocks include AZ. |
| per-page overrides | fields | — | `[V1·BUILD]` | `meta_robots_override`, `sitemap_inclusion_override`, `redirect_destination_override` (90-day expiry unless renewed). |
| ~~`topBlock` (Head/Top/Center/Right)~~ | — | — | KILLED | **KILLED** — legacy layout / module slots. |
| ~~`searchImage`~~ | — | — | KILLED | **KILLED** — always show the catalog image. |
| ~~`searchUsp`~~ | — | — | KILLED | **KILLED** — no USP shown in search. |
| ~~`searchTags`~~ | — | — | KILLED | **KILLED** — Algolia NeuralSearch matches from indexed fields + AI synonyms (V2); nothing replaces tags in V1. |
| ~~`shouldShowPerShop`~~ | — | — | REMOVED | **REMOVED** — per-shop visibility → language/locale level (§3.15); hide via empty localized content. |
| ~~Visual Options~~ | — | — | KILLED | **KILLED** — Center without sidebar · background-on-page · Hide breadcrumb · Hide header notification bar. |

## Per-surface usage & deltas

- **PLP.** The base listing page. DOM order: USP bar → B1 nav → B2 breadcrumb → B3 H1 → B4 intro → [BG promo above grid] → B5 grid → B7 sub-grid → **B9 supporting (BEFORE B8 reviews, §3.18)** → B8 reviews → B11 blog → B12 related → B13 FAQ → B15 PM → B14 SEO text → schema. See [[surface-PLP]].
- **FLP.** Same entry + the AZ filter engine ([[filter-engine-AZ]], PARKED). Adds the B2b category-taxonomy tree, F1 filter panel / F2 controls before the grid, F3 pagination after, F4 empty-state at end (F1–F4 render-only). DOM order is **B8 before B9** (do not copy onto the PLP). Inherits the PLP below-grid blocks. See [[surface-FLP]].
- **Earned-filter variants (FLP, PARKED).** Each earned filter is a **separate `pageHomeModular` entry** of the same FLP content type with a parent reference to the base FLP. Its existence IS the earned-state signal. **To define (parked):** the parent-FLP ref + the applied-facets ref (variant ← facet ← parent chain). Carries its own `target_keywords` set; scorer-cleared before publish.

## Requirements behaviour

- **Index rule-engine (autonomous, daily 09:00 CET review).** `INDEX-1` `index,follow` when ALL: volume ≥20/month; `target_keywords` filled (primary + ≥1 secondary); no cannibalisation flag; grid ≥4 tiles; FAQ ≥5 OR SEO text present; URL g-url compliant; locale URL explicitly authored. `NOINDEX-1` otherwise. `NOINDEX-2` overrides INDEX-1 for nav-only pages with no volume that would cannibalise. `NOINDEX-NOFOLLOW` for admin/transactional. SITEMAP-IN/OUT, HREFLANG-IN, REDIRECT-ADD follow. See [[g-meta]] / [[g-tech-seo]].
- **Schema (§3.2).** NO `CollectionPage`. Listing pages emit sitewide `Organization`+`WebSite`+`SearchAction` + `WebPage` + `BreadcrumbList` + `ItemList` (ItemList only on indexable canonical URLs; omit pages 2+/empty-state/non-earned filter). See [[g-schema]].
- **Breadcrumb (§3.17).** Walker reads `parentCategory` (single ref), walks to the locale Homepage entry; the same walker as the PDP (polymorphic — PLP/FLP has `parentCategory`, no `Direct Main Category`).
- **Mobile.** Same DOM mobile + desktop; no `m.` subdomain, no AMP; same JSON-LD/hreflang/canonical/meta-robots across viewports. PLP has no configurator/cart panel (tap tile → PDP).
- **Voice / multi-brand.** Forbidden vocabulary; no em-dashes; `{{shop_name}}` template variable.

## Decisions (locked)

- **§2** — PLP + FLP entry = `pageHomeModular`; taxonomy parent = `parentCategory` (self-ref); **no separate `Category` content type**; FLP = a PLP whose Content Blocks include AZ; earned-filter variants = separate `pageHomeModular` entries (parent-FLP ref + applied-facets ref — to define, parked).
- **§3.13** — `Content Blocks` (rename `bodyBlocks`); author-curated.
- **§3.1** — meta-robots per-locale, default `noindex, follow` (overrides PLP-catalog nofollow correction).
- **§3.19** — `target_keywords` shape; `priority` load-bearing; read-only `search_volume`.
- **Page-field decisions (PLP catalog v1.5):** Title→H1, Slug = cross-locale id, introParagraph = description, Page Name (was searchName), Search Settings (was excludeFromSearch), analyticsPageTypeVariation = reporting only. **Killed:** topBlock, searchImage, searchUsp, searchTags.

## Open points

- **FLP-parked:** earned-variant parent-FLP ref + applied-facets ref to define; full AZ filter-engine model parked pending the product-catalog-system decision ([[filter-engine-AZ]]).
- The B2b taxonomy tree's data source is described in the FLP doc as a "Category" content type — **resolved per §2 to be `pageHomeModular` nodes** (same entries the breadcrumb walker reads); no separate model is built.

## Sources

- PLP Req v1-13 §1 (g-url, meta-robots, index rules), §3 (page-level scalar fields), §B (block DOM order)
- PLP Catalog v1.5 (page-field decisions: Title→H1, Slug, introParagraph, Page Name, Search Settings, killed fields)
- FLP Req v0-15 (FLP-as-PLP, earned-filter Contentful entries, B2b taxonomy data source)
- _BUILD-BRIEF §2 (page-entry model, no Category type), §3.1/3.13/3.19

Related: [[surface-PLP]] · [[surface-FLP]] · [[product]] · [[contentMedia]] · [[productCollection]] · [[reviews-blockP]] · [[faq-blockV]] · [[usp-block-BB]] · [[brands-blockC]] · [[blog-teaser-AJ]] · [[product-list-Z]] · [[filter-engine-AZ]] · [[g-url]] · [[g-meta]] · [[g-schema]] · [[breadcrumb]] · [[g-keywords-scoring]]


---


*(id: contentMedia · type: content-type · surfaces: [PDP, PLP, FLP] · status: draft)*


# contentMedia (Block S — Content / Media)

> **Labels:** V1·BUILD ×6 · V1·GUIDELINE ×10 · V2 ×1. Block scope = **V1·BUILD** (PLP/FLP Block 9 renders the two-column block; PDP B7 visual+tab integration is V1·BUILD·KEEP). The new fields (`imageAlt`/`Caption`/`Destination`, `imageSecondary*`, `mediaLayout`) are **V1·BUILD**; the content discipline (length, voice, in-setting imagery, CTA anti-cannibalisation, ≥500 ship gate) is **V1·GUIDELINE**. In-setting hover-photography content-fill is **V2** `[inferred from PLP B5 hover-photography V2]`.

The editorial workhorse: a localized heading + rich-text copy beside one or two images. The supporting-content block used for product descriptions (PDP) and topical/adjacent-keyword authority (PLP/FLP). Renamed from `homeBlockTypeS`.

## How it works in Contentful

A `contentMedia` entry sits in the page's `Content Blocks` field (on `product` for the PDP, `pageHomeModular` for PLP/FLP). The author writes a `title` (the block H2/H3), `content` (rich text — copy only, **no tables**), and adds one image (`image`) or a media pair (`image` + `imageSecondary`) governed by `mediaLayout`. An optional CTA (shared enum) and per-image destinations turn images into crawlable links. It renders as a two-column image+copy section that collapses to a single column on mobile.

The block is additive and backward-compatible: with only `image` + `content` set and `mediaLayout = Single`, it reproduces the legacy single-image block exactly.

## Field model

| field | type | localized? | notes | phase/type |
|---|---|---|---|---|
| `name` | String | no | Admin label, not rendered | V1·BUILD |
| `title` | String | yes | Visible block heading · supports `<br>` | V1·BUILD |
| `titleLevel` | Enum | — | H2 · H3 · Span (was `titleFormatH1H6`; H1 + H4–H6 dropped) | V1·BUILD |
| `content` | RichText | yes | Line breaks · bold · headings · italic · quote · ordered/numbered list. **NO tables, NO media-insert** (tables → [[rich-text-BE]]). Internal links via CF-entry picker (Product · Page · URL); external via Target URL | V1·BUILD |
| `image` | Link to Asset | yes | Single main visual (was `brandedImage`) | V1·BUILD |
| `imageAlt` | String | yes | **NEW — required (guideline).** a11y + image SEO; distinct from caption. Empty → fallback caption → linked product name + content warning | V1·BUILD (field) · V1·GUIDELINE (required-content) |
| `imageCaption` | String | yes, optional | **NEW.** Visible caption under the image; plain text, ~100-char cap (≤2 lines), no inline links; replaces text baked into the pixel | V1·BUILD |
| `imageDestination` | Link to Entry (Product · Page · URL) | optional | **NEW.** Makes the image a real crawlable `<a>` (caption = anchor context); empty → illustrative; honours `noCrawlLinks` for nofollow | V1·BUILD |
| `imageSecondary` | Link to Asset | yes, optional | **NEW.** Second image; presence + `mediaLayout ≠ Single` triggers the pair | V1·BUILD |
| `imageSecondaryAlt` | String | yes | **NEW — required when `imageSecondary` set.** Same rules as `imageAlt` | V1·BUILD (field) · V1·GUIDELINE (required-content) |
| `imageSecondaryCaption` | String | yes, optional | **NEW.** Same rules as `imageCaption` | V1·BUILD |
| `imageSecondaryDestination` | Link to Entry | optional | **NEW.** Independent destination for the 2nd image | V1·BUILD |
| `mediaLayout` | Enum (3) | — | **NEW.** Single *(default)* · Pair beside text · Pair below text | V1·BUILD |
| `cta` | Enum (5) | — | Shop now · Discover our collection · Design now · Read more · Custom (shared enum — see [[g-keywords-scoring]]/decisions; was `ctaButtonOptions`). Block S is the only consumer carrying all 5 (Discover our collection = green outline, S only) | V1·BUILD |
| `customButtonText` | String | yes | Only when `cta = Custom` (was `buttonText`) | V1·BUILD |
| `destination` | Link to Entry | — | CTA destination — Product · Page · URL | V1·BUILD |
| `visualOptions` | Multi-select (5) | — | Flip image and text · Hide image on mobile · 2-Column Text · Section collapsible · Section collapsible on mobile (truncate after 2 lines mobile / 4 lines desktop, inline "Show more") | V1·BUILD |
| ~~`shouldShowPerShop`~~ | — | — | **REMOVED** — per-shop visibility moves to language/locale level (§3.15); hide in a locale via empty localized content → empty-state omit | V1·BUILD (removal) |
| ~~`videoUrl` / `videoPlaceholder`~~ | — | — | **REMOVED** → standalone [[video]] block | V1·BUILD (removal) |
| ~~`contentRight` / `rightImage` / `contentSteps`~~ | — | — | **REMOVED** — single `image` + `mediaLayout` pair replaces; steps → ordered list in `content` | V1·BUILD (removal) |
| ~~`buttonStyle` / `fontSize` / `originalEntryId`~~ | — | — | **REMOVED** — colour now driven by `cta` enum; single typography scale; 14 legacy visualOption flags dropped | V1·BUILD (removal) |

**`mediaLayout` (NEW — §3.14).** Equal **50/50** always; mobile always collapses to one column (heading → copy → image → image); both images share one aspect + per-image focal point; **cap = 2** (not a gallery). When `Pair beside text` stacks two images in one half they render at a **reduced (≈16:9) size** so the stacked pair sits level with the copy rather than overrunning it. `Flip image and text` applies to Single + Pair-beside (no-op for Pair-below); `Hide image on mobile` hides both.

| value | desktop | best for |
|---|---|---|
| **Single** *(default)* | one image beside copy (`Flip image and text` sets L/R) | standard editorial section |
| **Pair beside text** | two **smaller** images (≈16:9) stacked in the media half so the pair sits level with the copy, not towering; copy fills the other half | detail + context · front/back |
| **Pair below text** | short copy full-width; two images side-by-side beneath, larger | before/after · colourways/finish |

## Per-surface usage & deltas

- **PDP** → maps to **B7** (Product description) and **B15** (SEO text, migrated as existing Block S). NOT B4 — the PDP intro is the native `introParagraph` field, not Block S. PDP has no above-grid link restriction; the block sits mid-page. B7 in V1 is visual + tab integration only (existing copy preserved, no rewrite) `[V1·BUILD·KEEP]`; Pros & Cons relocated to the bottom of B7 (see [[surface-PDP]] B17 nuance) `[V1·BUILD·KEEP]`. PDP B15 SEO-text rendering = `[V1·BUILD]`; its generated copy = `[V1·GUIDELINE]`.
- **PLP** → maps to **B9** (Supporting text + visual) `[V1·BUILD]`. Ships when an adjacent topic ≥ 500 monthly volume not already covered `[V1·GUIDELINE]`; max 2 stacked (each clears ≥500 + adjacency) `[V1·GUIDELINE]`; H2 carries a secondary keyword `[V1·GUIDELINE]`. **Linked-image pairs count as links → the block sits below the product grid** (§B4 no-links-above-grid) `[V1·BUILD]`. PLP DOM order: B9 supporting renders **before** B8 reviews `[V1·BUILD]`.
- **FLP** → maps to **B9**, same model as PLP `[V1·BUILD]`; FLP DOM order is B8 before B9 (do not copy the FLP order onto the PLP) `[V1·BUILD]`.

## Requirements behaviour

- **SSR** `[V1·BUILD]`**.** Block and both images server-rendered; no client fetch. Images AVIF > WebP, lazy + async, width/height declared, srcset `[V1·BUILD]`; PLP/FLP image always in-setting/lifestyle, never a flat cut-out, no text in image, source max 1200×800 rendered ≤ 600px desktop; alt = natural-language `[V1·GUIDELINE]`.
- **Content length** `[V1·GUIDELINE]`**.** PLP/FLP supporting text 80–150 words (max 200); first sentence stand-alone extractable `[AEO · SHOULD · V1·GUIDELINE]`. Text fed from the product feed so characteristics stay real `[V1·GUIDELINE]`.
- **CTA.** Optional; real crawlable `<a>`, descriptive anchor `[V1·BUILD]`; anti-cannibalisation + high-converting-target rules (never to a sibling PLP, never to lower-intent/informational pages) `[V1·GUIDELINE]`. De-dup is a SHOULD, not build-enforced ([[g-keywords-scoring]]) `[V1·GUIDELINE]`.
- **Clickable images** `[V1·BUILD]`**.** Per-image destinations are **independent** — the win is variant routing (Matte → matte product, Gloss → gloss product) as two distinct crawlable `<a>` with the caption as anchor context. Don't link both images to the same destination (that's the block CTA's job) `[V1·GUIDELINE]`.
- **Boundary vs Block D** `[V1·GUIDELINE]`**.** Pair images stay illustrative — no price, no per-image buy button. Two priced products with buy buttons = [[productCollection]] (Block D), not Block S.
- **Tables forbidden** `[V1·BUILD]`**.** `content` cannot hold tables; comparison/spec tables go to [[rich-text-BE]]. (PDP also has the structured B16 spec/pricing matrix — separate from BE.)
- **Empty / degraded** `[V1·BUILD]`**.** `mediaLayout = Pair` but no `imageSecondary` → render Single; both images empty → **text-only** full-width reading-width copy (a supported state, not a new field); caption empty → omit the line; `imageAlt` empty → fallback caption → product name + content warning.
- **Schema.** **No schema** — clickable images never become `ItemList` / `Product` nodes ([[g-schema]]) `[V1·BUILD]`.
- **Voice** `[V1·GUIDELINE]`**.** PLP §b14 voice + banned-words apply to copy.

## Decisions (locked)

- **§3.14** — `contentMedia` gains `imageAlt` (required guideline), `imageCaption`, `imageDestination`, `imageSecondary` (+ `Alt`/`Caption`/`Destination`), `mediaLayout` (Single · Pair beside text · Pair below text; 50/50; mobile single-column; cap 2). `content` still forbids tables (use [[rich-text-BE]]). Maps to PDP B7·B15 (NOT B4 = `introParagraph`), PLP/FLP B9. Linked-image pairs → below-grid on PLP. No schema.
- **§3.8** — one shared `cta` enum (Shop now · Discover our collection · Design now · Read more · Custom). Block S is the only block carrying all 5 (Discover our collection is S-only).
- **§3.15** — per-shop visibility → language/locale level; `shouldShowPerShop` dropped; hide via empty localized content → empty-state omit.
- **§3.7** — no video on the block (video is the standalone [[video]] body block).

## Open points

- Final field IDs for the new fields confirmed in the Seb code review (catalog note).
- The b9-11 PDP↔PLP H2 rule (PLP H2 = action verb; PDP H2 = product-distinguishing attribute) lives in [[g-keywords-scoring]], not restated here — GUIDELINE, no CI gate.

## Sources

- PDP Catalog v0.20 §1.1 (`contentMedia` field model, removed fields, `--color-design` token)
- PLP Catalog v1.5 §Block S + §3.14 (caption + alt, media pair, `mediaLayout`, deliberately-not-taken list)
- PDP Req v0-34 §B7 (product description V1 scope; Pros & Cons → B7 bottom)
- PLP Req v1-13 §B9 (supporting text behaviour, ≥500 floor, ≤2 stacked, below-grid)
- FLP Req v0-15 §B9

Related: [[productCollection]] · [[rich-text-BE]] · [[video]] · [[g-schema]] · [[g-keywords-scoring]] · [[surface-PDP]] · [[surface-PLP]] · [[surface-FLP]]


---


*(id: homeBlockTypeBE · type: content-type · surfaces: [PDP, PLP, FLP] · status: draft)*


# rich-text-BE (Block BE — Rich text)

> **Labels:** V1·BUILD ×4 · V1·GUIDELINE ×4. Catalog verdict = *Maintain — returns (was Kill)*. The block (the `richText` field rendering real `<table>`/`<th scope>`, inline links, SSR, no schema, below-grid placement on PLP) is **V1·BUILD**. The **escape-hatch discipline** — use only as last resort, role/boundary vs S/V/B14/B16, link budget (≈ max 5), heading hygiene, voice/banned-words — is **V1·GUIDELINE** (commercial/content discipline, not a CI gate).

The freeform-editorial **escape hatch**: the one block that renders rich text **with real tables** and inline links. Used **only as a last resort** when the structured blocks can't express the content — above all **comparison / spec tables** with per-cell product links. NEVER the default. Un-killed (was Kill on the PDP) because live usage proves the table need; [[contentMedia]] `content` and B14 SEO text both forbid tables.

## How it works in Contentful

A `homeBlockTypeBE` entry holds a single `richText` field — the whole block body: headings, paragraphs, ordered/unordered lists, **tables**, hyperlinks (Product · Page · URL) and marks (bold/italic/underline). It is SSR'd in full. The author reaches for it only when nothing structured fits: a binding/material/spec comparison table (e.g. Saddle-Stitched · Perfect-Bound · Wire-O with per-cell links), a "which X should I pick" linked list, or custom editorial.

## Field model

| field | type | localized? | notes | phase/type |
|---|---|---|---|---|
| `name` | String | no | Admin / entry label | V1·BUILD |
| `richText` | RichText | yes | Headings · paragraphs · ordered/unordered lists · **tables** · hyperlinks (Product · Page · URL) · bold/italic/underline. The whole block body. Tables render as real `<table>` / `<th scope>` | V1·BUILD |
| ~~`shouldShowPerShop`~~ | — | — | **REMOVED** (§3.15 language/locale level; hide via empty localized content) | V1·BUILD (removal) |

**Create-new:** none. **No schema** — table content is never emitted as `ItemList` / `Product`.

## Per-surface usage & deltas

- **All surfaces** (PDP, PLP, FLP). Shared `homeBlockTypeBE` `[V1·BUILD]`.
- **PLP delta** — BE carries links → it sits **below the product grid** (§B4 no-links-above-grid) `[V1·BUILD]`; author-positioned in the bottom editorial zone, near B14 `[V1·GUIDELINE]`. **PDP has no above-grid restriction** (mid-page allowed) `[V1·BUILD]`.
- Static / legal pages may use BE, but those pages are built later and are **out of scope** here `[V1·GUIDELINE]`.

## Requirements behaviour

- **Role + boundary** `[V1·GUIDELINE]`**.** Use BE for: spec & comparison **tables**; "which [binding/material]" linked lists; flexible editorial the structured blocks can't carry. **Not** for: structured bottom-of-page SEO copy (→ B14); copy-beside-image editorial (→ [[contentMedia]]); FAQ (→ [[faq-blockV]]); promos (→ [[promoCard]] / B6 / B10). **Tables are the killer capability — nothing else has them.**
- **vs B16** `[V1·GUIDELINE]`**.** On the PDP, `B16` is a **separate structured** spec/pricing matrix (Mixam-style, attribute-level tabs) — it is **not** a BE replacement and BE is not a B16 replacement. Use B16 for the structured PDP spec matrix; use BE for hand-built editorial tables.
- **Heading hygiene** `[V1·GUIDELINE]`**.** `richText` may contain H2/H3 but they must fit the page heading graph (one H1 only; no competing stacked H2s).
- **Internal links.** Real crawlable `<a>` `[V1·BUILD]`; inherit the B14 link budget (≈ max 5; anti-cannibalisation SHOULD — never link a sibling PLP/FLP competing for the hub keyword) `[V1·GUIDELINE]`. See [[g-keywords-scoring]].
- **Voice + banned-words** apply (PLP §b14) `[V1·GUIDELINE]`.
- **SSR** `[V1·BUILD]`**.** Rendered in full, no lazy-load.
- **Tables.** Real `<table>` / `<th scope>` for a11y `[V1·BUILD]`.
- **Schema.** **No schema** ([[g-schema]]) — a hand-built table must not become structured data `[V1·BUILD]`.

## Decisions (locked)

- **§3.10** — Block BE is the freeform-editorial **last-resort escape hatch**, NEVER the default. All surfaces; tables. Use only when S/V/B14/B16 can't express it. `B16` (PDP) is a separate structured spec/pricing matrix, not a BE replacement. Static/legal pages may use BE but are built later (out of scope). Fields: `name · richText` (RichText incl. tables/hyperlinks/marks). No schema; real `<table>`/`<th scope>`; below-grid on PLP.
- **§3.15** — `shouldShowPerShop` removed.

## Open points

- Confirm the comparison-table is the primary intended role (catalog open point).
- Confirm the link-budget + heading-hygiene guardrails above.
- Confirm any RichText feature to disable (e.g. embedded assets / media).

## Sources

- PLP Catalog v1.5 §Block BE (un-kill, field model, role/boundary, guardrails, PLP placement)
- BUILD-BRIEF §3.10 (escape-hatch framing, vs B16, out-of-scope static/legal)
- PLP Req v1-13 §B14 (link budget, voice, banned words inherited)

Related: [[contentMedia]] · [[faq-blockV]] · [[g-schema]] · [[g-keywords-scoring]] · [[surface-PDP]] · [[surface-PLP]] · [[surface-FLP]]


---


*(id: homeBlockTypeAJ · type: content-type · surfaces: [PDP, PLP] · status: draft)*


# blog-teaser-AJ (Block AJ — Blog / inspiration teaser, B11)

> **Labels:** V1·BUILD ×4 · V1·GUIDELINE ×6 · V2 ×2. Catalog verdict = *Maintain — optimised (PLP + PDP)*. Block scope = **V1·BUILD** (renders the slots; SSR; ItemList schema; re-point `Content Blocks` → Page Article). **Selection is the V1/V2 split:** **V1 = author-selected/manual** `[V1·GUIDELINE]`; **V2 = tag-driven auto + weekly quality gate** `[V2·BUILD]`. Per-card content, H2 wording, anti-cannibalisation, contextual-or-omit destination = **V1·GUIDELINE**.

The **B11** blog / inspiration teaser: surfaces the most authoritative blog posts that support the page's topical authority and AEO E-E-A-T. A block H2 + intro + a set of article cards, each linking to a **Page Article**. Shared content type — the same model applies on the **PDP and the PLP**.

## How it works in Contentful

A `homeBlockTypeAJ` entry sits in the page's `Content Blocks`. The author writes a unique, page-specific `Title` (the block H2) + `Description`, optionally sets a `Destination` (a "Read more" to the relevant Article Category), and fills `Content Blocks` with links to **Page Article** entries. Each card's image + title are sourced **directly from the Page Article** (single source of truth); a new `Summary description` field on Page Article supplies the card line. V1 is author-selected; V2 is tag-driven auto + a quality gate.

## Field model

| field | type | localized? | notes | phase/type |
|---|---|---|---|---|
| `Name` | String | no | Internal entry label | V1·BUILD |
| `Title` | String | yes | Block **H2** — must be **unique & page-specific**: topic keyword + an inspiration verb, locale-tuned (e.g. "Business-card printing inspiration"). Question-form headings rejected. No global default ("Get inspired by our blogs") | V1·BUILD (field) · V1·GUIDELINE (unique-per-page H2 content) |
| `Title Format` | Enum | — | Heading level — default **H2** · options H2 / H3 / Span | V1·BUILD |
| `Description` | String/RichText | yes | Short, **page-specific** intro to this category's blogs (no global default) | V1·BUILD (field) · V1·GUIDELINE (unique-per-page content) |
| `Destination` | Link to Entry | optional | Category-level "Read more" target → the relevant **Article Category**; **if none, drop the CTA** (no auto-fallback to the generic blog) | V1·BUILD (field) · V1·GUIDELINE (contextual-or-omit) |
| `Content Blocks` | Array, Link → **Page Article** | — | The article cards. **Re-pointed** from `bundleItem` → Page Article; image + title sourced from Page Article | V1·BUILD |
| ~~`CTA Button`~~ | — | — | **REMOVED** (constant "Read more") | V1·BUILD (removal) |
| ~~`CTA Text`~~ | — | — | **REMOVED** (constant) | V1·BUILD (removal) |
| ~~`Content Blocks – Title Format`~~ | — | — | **REMOVED** — cards are non-heading link text (the block owns the single H2; heading hygiene) | V1·BUILD (removal) |
| ~~`Should show per shop`~~ | — | — | **REMOVED** (§3.15 language/locale level) | V1·BUILD (removal) |

**New / re-pointed (content-model work)**

| field / source | what it is | verdict | phase/type |
|---|---|---|---|
| `Summary description` | **NEW on Page Article.** Localized, one sentence summarising the blog's angle — rendered on the AJ card | Create new (on Page Article) | V1·BUILD (slot) · V1·GUIDELINE (content fills in parallel) |
| image + title | Sourced **directly from Page Article** — not duplicated on AJ | Re-point to Page Article | V1·BUILD |

## Per-surface usage & deltas

- **PDP** → B11. Same optimisation as the PLP (catalog explicitly mirrors it to the PDP) `[V1·BUILD]`.
- **PLP** → B11. Author-selected `[V1·GUIDELINE]`; tag-driven auto + quality gate `[V2·BUILD]`.
- Not an FLP block in this scope (FLP B11 = `cond gate`, inherits the PLP model where present) `[V1·BUILD]` `[inferred]`.

## Requirements behaviour

- **Selection + V1/V2.** V1 author-selected `[V1·GUIDELINE]`; V2 tag-driven auto + a weekly quality gate (organic traffic + backlinks + freshness + on-page quality, no override) `[V2·BUILD]`.
- **Anti-cannibalisation.** Exclude posts whose primary keyword = the page's primary keyword (the [[g-keywords-scoring]] scorer; blog-vs-PLP-primary is part of the cross-surface scoring). Locale only `[V1·GUIDELINE]`.
- **Destination — contextual-or-omit.** Point "Read more" at the relevant Article Category; if none, **drop the CTA** rather than auto-falling-back to the generic blog (generic repeated links = low-value boilerplate). Article cards still link to their specific Page Articles. **No relevant articles → the block does not render (omit)** `[V1·GUIDELINE]` (empty-state omit render = `[V1·BUILD]`).
- **Per-card.** Title no truncation (CMS short-title fallback); excerpt = the `Summary description`, smart-truncated ~120 chars; last-updated date locale format; author byline (E-E-A-T, AEO SHOULD); hero/featured image `[V1·GUIDELINE]`. Whole card is a single `<a>`; title = styled span, **not** an `<h3>` `[V1·GUIDELINE]`.
- **Layout.** 3 cards desktop (4:3), mobile 1-up. SSR. AVIF/WebP, srcset, width/height, lazy + async `[V1·GUIDELINE]` (rendering tech, MUST; SSR-into-initial-HTML = `[V1·BUILD]`).
- **Schema.** Each card = one **`ListItem`** in a **page-level, article-scoped `ItemList`** (position / name / url); **no per-card `Article` schema**. This ItemList is **separate** from the B5/B12 product ItemList — see [[g-schema]] `[V1·BUILD]`.

## Decisions (locked)

- **§3.9** — anti-cannibalisation (exclude posts matching the page primary keyword) lives in [[g-keywords-scoring]], applied here, not duplicated.
- **§3.15** — `Should show per shop` removed.
- AJ is shared PLP + PDP — mirror the optimisation on both. `Summary description` is a new **Page Article** field (content-model work); V1 ships the slots, content fills in parallel.

## Open points

- Page Article content type itself (`Summary description` field) is content-model work to confirm in the Batch 2.x code review; AJ ships the slot.

## Sources

- PLP Catalog v1.5 §Block AJ (field model, re-point to Page Article, Summary description, contextual-or-omit destination, schema)
- PLP Req v1-13 §B11 (selection, quality gate, anti-cannibalisation, per-card, ItemList ListItem schema)
- PDP Catalog v0.20 §Block AJ (PDP parity — same field model)

Related: [[productCollection]] · [[g-schema]] · [[g-keywords-scoring]] · [[surface-PDP]] · [[surface-PLP]]


---


*(id: productCollection · type: content-type · surfaces: [PDP, PLP, FLP] · status: draft)*


# productCollection (Block D — Product Collection)

> **Labels:** V1·BUILD ×7 · V1·BUILD·KEEP ×4 · V1·GUIDELINE ×3 · V2 ×2. Block scope = **V1·BUILD** (catalog verdict *Maintain*). The grid `<a>`, two-state image DOM, `items` accepting [[bundleItem]] + [[promoCard]], `noCrawlLinks`, and the pricing-consistency contract are **V1·BUILD** (live pricing read-path = **KEEP**). The **Hide Discount** visualOption + the auto discount-label automation are **V2** (product-data dependency). B12 selection priority is **V1·GUIDELINE** (Algolia auto = **V2**).

The product-grid container: a localized heading + a grid of product tiles ([[bundleItem]]) and at most one [[promoCard]]. The conversion surface — it powers the PLP/FLP main grid (B5) and the related-products shelf (B12). Renamed from `homeBlockTypeD`.

## How it works in Contentful

A `productCollection` entry sits in the page's `Content Blocks` field. The author writes `title` + optional `description`, picks `productsPerRow` and `imageSource`, sets `visualOptions`, and fills `items` with up to 16 entries — any mix of [[bundleItem]] and a single [[promoCard]] (a CF validator rejects a 2nd promo). It renders as a responsive grid (mobile always 2-up); cards are real crawlable `<a>` to PDPs unless `noCrawlLinks` is set.

## Field model

| field | type | localized? | notes | phase/type |
|---|---|---|---|---|
| `name` | String | no | Admin label | V1·BUILD |
| `title` | String | yes | Block heading | V1·BUILD |
| `titleLevel` | Enum | — | H2 · H3 · Span (was `titleFormatH1H6`) | V1·BUILD |
| `bundleItemTitleLevel` | Enum | — | H3 · H4 · Span (was `itemtitleFormatH1H6`) | V1·BUILD |
| `description` | RichText | yes, optional | Same HTML rules as [[contentMedia]] `content`; below title, above grid, full-width, always shown | V1·BUILD |
| `items` | Array, Link to Entry | — | **Accepts [[bundleItem]] AND [[promoCard]]** (renamed from `products`). Max 16 total · max 1 Promo Card (CF custom validator) | V1·BUILD |
| `imageSource` | Enum | — | Catalog image (default) · Bundle item image (override) | V1·BUILD |
| `productsPerRow` | Enum | — | 2 · 3 · 4 · 5 · Fill to full width | V1·BUILD |
| `visualOptions` | Multi-select (7) | — | see table below | MIXED (V1·BUILD + Hide Discount V2) |
| `showAllText` | String | yes | Show-all button label (top-right); renders only if both `showAllText` + `showAllLink` set | V1·BUILD |
| `showAllLink` | Link to Entry | — | Product · Page · URL | V1·BUILD |
| `cta` | Enum (4) | — | Shop now · Design now · Read more · Custom (shared enum, §3.8). **No "Discover our collection"** here — that value is [[contentMedia]]-only. Block-level uniform — every card renders the same CTA | V1·BUILD |
| `customButtonText` | String | yes | Only when `cta = Custom` | V1·BUILD |
| `noCrawlLinks` | Boolean (default crawlable) | — | Block-level default (was `makeNonCrawlableLink`) · `rel="nofollow"` on each `<a>` (cards + Show-All) · [[bundleItem]] overrides per-card. NOT page-level noindex | V1·BUILD |

**visualOptions (7)**

| flag | behaviour | phase/type |
|---|---|---|
| Hide prices | Hide the price line on every card · overrides [[bundleItem]] `pricesVisualOptions` | V1·BUILD |
| Hide descriptions | Hide `highlights` text on every card | V1·BUILD |
| Show as carousel | Horizontal carousel · manual arrows · 1-at-a-time · stop at end (no loop) · overrides Fill | V1·BUILD |
| Show as carousel on desktop only | Carousel desktop · grid mobile | V1·BUILD |
| Section collapsible on mobile | Show-More on `description` (2-line mobile / 4-line desktop) | V1·BUILD |
| Hide Discount | Hide the auto-discount badge · default OFF · V2 dependency on the product-data structure | **V2·BUILD** |
| **Hide hover-over image** `NEW · PLP` | Suppress the in-setting / hover image for every card in this block. Default OFF (hover shows where an in-setting image resolves) | V1·BUILD |

**Removed visualOptions (12).** Show recommended price · Popout center product · Hide title · image-thumb / landscape / square / portrait toggles (aspect now auto from `productsPerRow`) · Show as block · Center title · Display style · Extra vertical spacing · Default. Per-card "Hide title" dropped — every card always shows its title.

**`Fill to full width` layout map.** 1 = width-of-2 + 1 empty · 2 = 2 · 3 = 3 · 4 = 4 · 5 = 5 · 6 = 3+3 · 7 = 3+4 · 8 = 4+4 · 9 = 5+4 · 10 = 5+5 · 11 = 3+4+4 · 12 = 4+4+4 · 13 = 4+4+5 · 14 = 4+5+5 · 15 = 5+5+5 · 16 = 4+4+4+4.

**Image aspect by `productsPerRow`.** 2/row ≈ 4:3 landscape (largest) · 3/row ≈ 1:1 · 4/row ≈ 3:4 portrait · 5/row ≈ 1:1 (smallest) · Fill = mixed · Mobile = always 2/row, ~3:4 portrait (Fill does not apply on mobile).

## Per-surface usage & deltas

- **PDP** → maps to **B12** (related products) `[V1·BUILD]`. `cta` = 4 values (no "Discover our collection"). [[bundleItem]] `noCrawlLinks` is a per-card override of the block-level default `[V1·BUILD]`. **No card video** — Block D cards are static-image only `[V1·BUILD]`.
- **PLP** → maps to **B5** (main product grid) `[V1·BUILD]` and **B12** (related products, auto-priority) `[V1·BUILD]`. New PLP visualOption **Hide hover-over image** `[V1·BUILD]`. B12 = `productCollection`; it is **decoupled** from `homeBlockTypeBI` (the page-card navigation block / [[g-pagecard]]) — no shared schema, no shared dedup graph `[V1·BUILD]`. The render-all-`subitems[]` behaviour belongs to BI, not B12. Author-selected `[V1·GUIDELINE]`; Algolia `[V2]`.
- **FLP** → maps to **B5** (the visual results grid) `[V1·BUILD]`. Distinct from [[product-list-Z]] (the crawlable text-link directory) — both render on an FLP (Z lower, for SEO linking) `[V1·BUILD]`.

## Requirements behaviour

- **B5 grid (PLP/FLP).** Not a hero — a curated grid, the first commercial block; tile count typically 8–20 (more on themed hubs), no pagination; all tiles same topic (split into a 2nd grid with its own H2 if a different sub-group); first tile = bestseller (sales-weighted, monthly refresh); first row ≥ 70% cluster sales (flags < 50%); unavailable products dropped; no duplicate PDPs in the grid `[V1·GUIDELINE]` (these are commercial-curation rules; the grid `<a>` wrapper itself = `[V1·BUILD]`).
- **Two-state image** `[V1·BUILD]`**.** Catalog default + in-setting hover, both SSR as separate `<img>`, swapped via CSS `:hover` (never JS `src`). Hover never eager / never `fetchpriority=high`. Mobile = one image per tile (`<picture>` disables hover on `(hover:none)`; the in-setting image becomes the default). Image source always Contentful via `catalogImage → images[0] → bundleItem.photo`; both missing → tile logged but the page still ships (graceful degrade). DOM capability ships V1; lifestyle hover-photography content-fill = `[V2]`.
- **Pricing consistency** `[V1·BUILD·KEEP]`**.** PLP tile = PDP = product feed (one pre-set pricing path); caching never causes drift, else uncached `[V1·BUILD]`. Promotional pricing was/now both SSR `[V1·BUILD·KEEP]`; auto discount-label overlay (was−now)/was bucketed to nearest 5%, < 2.5% hidden — `[V2·BUILD]` automation (Hide Discount controls it).
- **B12 related products.** Top 5 same-main-category cross-sell, never cross-category; ranked by commercial priority (volume × margin × stocked range); hub → own children, sub-PLP → walk up to parent main-category siblings; **< 3 same-category products → omit the block** (no padding, no cross-category fallback) `[V1·GUIDELINE]` (priority/selection ranking; Algolia auto-selection = `[V2]`). Related tile = image + product name only (no price/CTA/badge — "explore more", not "compare to buy") `[V1·BUILD]`; anchor = product name verbatim `[V1·GUIDELINE]`. Appends to the page-level ItemList (position/name/url/image, **no offers**) — see [[g-schema]] `[V1·BUILD]`.
- **Empty / degraded** `[V1·BUILD]`**.** `items` empty → render headless (frame + title + description, no grid); `title` empty → render anyway; bundle image missing + `imageSource = Bundle item image` → fall back to catalog image; Hide prices + Hide descriptions both ON → minimal card (image + title + CTA); `showAllText` or `showAllLink` empty → button omitted.
- **Links.** De-dup across blocks is a SHOULD ([[g-keywords-scoring]]), not build-enforced `[V1·GUIDELINE]`.

## Decisions (locked)

- **§3.6** — `items` (renamed from `products`) accepts [[bundleItem]] **and** [[promoCard]] (max 16, max 1 promo).
- **§3.7** — no video on product-grid cards on any surface.
- **§3.8** — shared `cta` enum; Block D uses the 4-value subset (no "Discover our collection").
- **§3.3** — card labels via [[card-label]] (cap 2 at the model; PLP B5 renders max 1 badge per tile).
- `noCrawlLinks` block-level default, [[bundleItem]] per-card override.

## Open points

- Final Linear / field binding for `homeBlockTypeBI` vs Block D confirmed in the Batch 2.x code review (the BI page-card nav is decoupled — [[g-pagecard]]).
- Block-D-naming note (`products`→`bundleItems`) is superseded by the locked `items` (it carries promoCards too).

## Sources

- PDP Catalog v0.20 §1.2 (`productCollection` field model, visualOptions, Fill map, empty states)
- PLP Catalog v1.5 §Block D + §3.6 (Hide hover-over image, B12↔BI decoupling, Hide Discount)
- PLP Req v1-13 §B5 (grid behaviour, two-state image, pricing consistency) + §B12 (related products)
- PDP Req v0-34 §B12

Related: [[bundleItem]] · [[promoCard]] · [[card-label]] · [[g-pagecard]] · [[g-schema]] · [[contentMedia]] · [[surface-PLP]] · [[surface-FLP]] · [[surface-PDP]]


---


*(id: bundleItem · type: content-type · surfaces: [PDP, PLP, FLP] · status: draft)*


# bundleItem (product grid / related tile)

> **Labels:** V1·BUILD ×8 · V1·BUILD·KEEP ×2 · V1·GUIDELINE ×4 · V2 ×1. All fields/behaviour are **V1·BUILD** (the tile `<a>`, image resolution chain, `inSettingImage` hover, destination resolution, two-state SSR image, ItemList contribution). The pricing/image read-path that already exists live = **KEEP**. The per-tile commercial discipline (price-line reference quantity, differentiator slots) is **V1·GUIDELINE**. `promoDiscount` auto-render is **V2** (controlled by [[productCollection]] *Hide Discount*).

A single product tile inside a [[productCollection]] grid (B5) or related-products shelf (B12). It is a thin display wrapper over a `product` entry: it reads card data from the linked product and lets the author override the title, image, highlights, labels, preset path and destination.

## How it works in Contentful

A `bundleItem` links to exactly one `product` (single for all locales — the data source + default destination). The renderer pulls the card name, image and price from that product unless the author overrides them. Labels ([[card-label]], max 2 at the model) stack top-left; `inSettingImage` provides the hover image. Destination resolves `page` → `url` → the product's canonical URL. The tile renders as a single crawlable `<a>` (product name = anchor) unless `noCrawlLinks` is set.

## Field model

| field | type | localized? | notes | phase/type |
|---|---|---|---|---|
| `itemName` | String | en only | Admin label | V1·BUILD |
| `product` | Link → `product` | no | **SINGLE for all locales** · data source + default destination | V1·BUILD |
| `name` | String | yes, optional | Card title override · fallback = Product catalog name | V1·BUILD |
| `photo` | Link to Asset | yes | Default (catalog) image · renderer crops to row aspect · fallback = Product `catalogImage` | V1·BUILD |
| `inSettingImage` | Link to Asset | yes, optional | **NEW · PLP** — the hover / in-setting image. Empty → 2nd image from the Product's `Product Images`. Default shows; suppressed by [[productCollection]] *Hide hover-over image* | V1·BUILD (slot) · V2 (lifestyle photography content-fill) |
| `highlights` | String | yes, optional | Plain string, dash-prefixed bullets · hidden by [[productCollection]] *Hide descriptions* | V1·BUILD |
| `labels` | Multi-link → [[card-label]] | — | Max 2 · stacked top-left · priority = order. (Was multi-link → `attributeLabel`, now the merged [[card-label]] model.) | V1·BUILD |
| `bundleItemPresetPath` | String | yes, optional | Configurator preset override · empty = Product `presetPath` | V1·BUILD |
| `pricesVisualOptions` | Enum (3) | — | From Price · Display total pieces price · Display total pieces price + piece price | V1·BUILD |
| `page` | Link → `page` | optional | Destination override (precedence over Product URL) | V1·BUILD |
| `url` | String | optional | Destination override (used when `page` empty) | V1·BUILD |
| `noCrawlLinks` | Boolean (default crawlable) | — | Per-card override of [[productCollection]]'s block-level default (was `makeNonCrawlableLink`) | V1·BUILD |

**Removed fields**

| field | why | phase/type |
|---|---|---|
| `photoPortrait` | Single `photo` + renderer crop replaces | V1·BUILD (removal) |
| `customPricePath` | Redundant — `bundleItemPresetPath` covers it | V1·BUILD (removal) |
| `labeltext` | Consolidated into `labels` ([[card-label]]) | V1·BUILD (removal) |
| `promoDiscount` | Auto-render from product promo data · controlled by [[productCollection]] *Hide Discount* · V2 | **V2·BUILD** |
| `designWithCanva` | Auto-detected from product-data Canva/Design eligibility (not a CF field) | V1·BUILD (removal) |
| `slug` | Bundle Items aren't independently navigable | V1·BUILD (removal) |
| `crowdIn` · `excludeFromWls` | Move to tag / space-based architecture | V1·BUILD (removal) |
| `visualOptions` (per-card) | 'Hide prices' etc. move to the [[productCollection]] block level | V1·BUILD (removal) |
| Per-locale `product` override | Single product all locales · create separate Bundle Items per locale if needed | V1·BUILD (removal) |

## Per-surface usage & deltas

- **PDP** → B12 related tiles `[V1·BUILD]`. Single `product` for all locales (separate bundle items per market); `noCrawlLinks` per-card override restored (v0.19) `[V1·BUILD]`.
- **PLP** → B5 grid tiles + B12 related tiles `[V1·BUILD]`. New `inSettingImage` (hover) → fallback to Product `Product Images` 2nd image; default shows, toggled by [[productCollection]] *Hide hover-over image* `[V1·BUILD]`. Default-image chain: `catalogImage → images[0] → bundleItem.photo` `[V1·BUILD]`.
- **FLP** → B5 grid tiles (same as PLP) `[V1·BUILD]`.

## Requirements behaviour

- **Tile = real `<a>` to the PDP** with the product name as anchor; single anchor wrap; SSR `[V1·BUILD]`. No H2/H3 inside tiles (name = styled span/p) `[V1·GUIDELINE]`.
- **Per-tile elements (B5).** Image · name · 2–3 slot-based differentiators (fixed slot = same dimension across the grid, concrete, ~3–6 words, differ per tile) · price-for-quantity + next-day line · optional badge ([[card-label]], one per tile crawler-readable span) `[V1·GUIDELINE]` (differentiator content discipline; the badge `<span>` render = `[V1·BUILD]`).
- **Price line.** "[from-price] for [reference quantity]", locale-tuned; reference quantity preference 100 → 1000 → 10 → 1 → 5000 → 500 → 250, locked per grid, consistent across tiles `[V1·GUIDELINE]`. `pricesVisualOptions` selects the shape `[V1·BUILD]`.
- **Pricing consistency** `[V1·BUILD·KEEP]`**.** Tile = PDP = product feed (one pre-set pricing path); never drift.
- **Image.** Product photo clean/neutral bg, portrait, master 1500×1500, AVIF + WebP, srcset, width/height declared; source always Contentful (no PIM fallback) `[V1·BUILD]` (master-file + alt-text discipline = `[V1·GUIDELINE]`). Two-state: catalog default + in-setting hover, both SSR; catalog = canonical `Product.image` + Shopping feed; hover never eager `[V1·BUILD]`. Mobile: hover off, one image per tile via `<picture>` `[V1·BUILD]`. Image resolution: `photo` override (when `imageSource = Bundle item image`) → Product `catalogImage` → Product `productImages[0]` → placeholder (build-time warning) `[V1·BUILD]`. Existing AVIF/WebP CDN pipeline reuse = `[V1·BUILD·KEEP]`.
- **Destination resolution** `[V1·BUILD]`**.** `page.curl` (+ locale prefix) → `url` → `product.slug` (canonical PDP URL). Card data always from `product`.
- **B12 related tile** `[V1·BUILD]`**.** Image + product name **only** (no description/price/delivery/CTA/discount/badge); appends to the page-level ItemList ([[g-schema]]), no offers.
- **Schema** `[V1·BUILD]`**.** Tile contributes to the page-level ItemList (B5 + B12) via [[g-schema]]; the `bundleItem` itself emits no standalone schema.

## Decisions (locked)

- **§3.3** — `labels` references the merged [[card-label]] model (replaces `attributeLabel`); cap 2 at the model, PLP B5 renders max 1 badge per tile.
- **§3.7** — no video on tiles on any surface.
- **§3.6** — `bundleItem` is one of the two entry types accepted by [[productCollection]] `items` (the other is [[promoCard]]).
- `inSettingImage` (NEW · PLP) feeds the hover image; default-image chain `catalogImage → images[0] → bundleItem.photo`.

## Open points

- Final CF field IDs / Linear binding confirmed in the Batch 2.x code review.

## Sources

- PDP Catalog v0.20 §1.3 (`bundleItem` field model, removed fields) + §1.12 (Product Entity Data Contract)
- PLP Catalog v1.5 §Bundle Item (+ `inSettingImage`, image resolution order)
- PLP Req v1-13 §B5 (tile contract, price line, two-state image) + §B12 (related tile)

Related: [[productCollection]] · [[card-label]] · [[promoCard]] · [[g-pagecard]] · [[g-schema]] · [[surface-PLP]] · [[surface-FLP]] · [[surface-PDP]]


---


*(id: cardLabel · type: content-type · surfaces: [PDP, PLP, FLP] · status: draft)*


# card-label (merged tile label)

> **Labels:** V1·BUILD ~×6 · V1·BUILD·KEEP ×1 · V1·GUIDELINE ×2 · V2 ×1. The merged model itself (fields, colour enum, `Secondary → Primary` migration, crawlable `<span>`, no schema, cap/stacking, max-1-badge render) is **V1·BUILD**; old-`attributeLabel`-consumer compatibility = **KEEP**. **Source per label type** is split: *Most Popular* = hand-authored **V1·GUIDELINE** (the only editorial label); *New* = auto (< 3 months) **V1·BUILD**; *Eco/Sale/bestseller/etc.* = product feed, **V1·GUIDELINE** (manual in PCM) **→ V2·BUILD** (auto from feed).

The single reusable label shown on a product tile (e.g. *Most Popular*, *New*, *Eco*, *Sale*, *Including Frame*). **One merged model** that replaces both the legacy `attributeLabel` content type and the PCM "Highlight Labels" surface — the two had diverged on colour enums (3 vs 4) and are now reconciled into one.

## How it works in Contentful

A `card-label` is a reusable entry linked from a [[bundleItem]] `labels` field (and from configurator step labels / B16, which stay backward-compatible). It carries the visible `title` and a `colour`. Labels stack top-left on the tile; the model caps at 2, **but PLP B5 renders max 1 badge per tile** (delta). Each label renders as a crawler-readable `<span>`. The *source* of a label depends on its type (see below) — only "Most Popular" is hand-authored.

## Field model

| field | type | localized? | notes | phase/type |
|---|---|---|---|---|
| `name` | String | en only | Admin label (e.g. "LABEL - Including Banner Frame") | V1·BUILD |
| `title` | String | yes | Visible label text (Most Popular · New · Eco · Sale · Including Frame · Free Next-Day Delivery …) | V1·BUILD (field) · source-per-type varies — see table below |
| `colour` | Enum (4) | — | **Default** (black text / white fill / grey outline) · **Primary** (green `#008539`) · **Design** (blue `#67A5B1`) · **Eco** (eco-green). Was `backgroundColor` (3 values); **Eco added** to reconcile with Highlight Labels | V1·BUILD |
| ~~`shouldShowPerShop`~~ | — | — | **REMOVED** (PDP + PLP both lose it; §3.15 language/locale level) | V1·BUILD (removal) |

**Colours (4).** Default · Primary (green) · Design (blue) · Eco (eco-green). **Migration:** live `Default → Default`, **`Secondary → Primary`**. The legacy `attributeLabel` 3-value enum (Default · Primary · Design) gains **Eco**; the PCM Highlight Labels 4-colour set (Default · Primary · Secondary · Eco) maps `Secondary → Primary` and keeps `Design`.

## Source per label type (§3.3)

| label type | source | phase/type |
|---|---|---|
| **Most Popular** | hand-authored in Contentful (the **only** editorial label) | **V1·GUIDELINE** (editorial) |
| **New** | auto — product launched < 3 months ago | **V1·BUILD** (auto) |
| **Eco · Sale · Bestseller · etc.** | product feed | **V1·GUIDELINE** (manual in PCM) → **V2·BUILD** (auto from feed) |

## Per-surface usage & deltas

- **PDP** → B12 related tiles (and shared by configurator step labels / B16). Cap 2 at the model `[V1·BUILD]`.
- **PLP** → B5 grid tiles + B12. Cap 2 at the model, **but B5 renders max 1 badge per tile** (delta — confirm priority = first in the `labels` order) `[V1·BUILD]`.
- **FLP** → B5 grid tiles. On the FLP card the labels render as an overlay on the top-left of the media well (not below the body) `[V1·BUILD]`.

## Requirements behaviour

- **Stacking + priority** `[V1·BUILD]`**.** Up to 2 labels stack top-left, priority = order in [[bundleItem]] `labels`. PLP shows only the first.
- **Crawlable** `[V1·BUILD]`**.** Each label is a real `<span>` in the DOM (badge text crawler-readable), one per tile on B5.
- **No schema** `[V1·BUILD]`**.** Labels are display-only; they do not emit `ItemList` / `Product` / `Offer` nodes.
- **Backward compatibility** `[V1·BUILD·KEEP]`**.** Other consumers of the old `attributeLabel` (configurator step labels, B16) stay backward-compatible — the merged model is a superset (the colour enum only adds `Eco`).

## Decisions (locked)

- **§3.3** — ONE merged card-label model. Colours: **Default · Primary (green) · Design (blue) · Eco (eco-green)** [4]. Cap = 2 at the model; **PLP B5 renders max 1 badge per tile**. Source per type: Most Popular = hand-authored (the only editorial one); New = auto (< 3 months); Eco/Sale/bestseller = product feed (V1 manual in PCM → V2 auto). Migration: live `Secondary → Primary`. This page **replaces** `attributeLabel` and the PCM Highlight Labels surface.
- **§3.15** — `shouldShowPerShop` removed (language/locale level).

## Open points

- Confirm PLP B5 "max 1 badge" picks the first label in priority order vs a colour-weighted rule (catalog flagged "confirm").
- Final field ID for `colour` (was `backgroundColor`) confirmed in the Seb code review.

## Sources

- PDP Catalog v0.20 §1.6 (`attributeLabel` field model, Secondary→Primary migration) + §12 Highlight Labels (4-colour set)
- PLP Catalog v1.5 §Attribute Label (PLP deltas, cap-1 note)
- BUILD-BRIEF §3.3 (merged model, colours, cap, source-per-type)

Related: [[bundleItem]] · [[productCollection]] · [[g-schema]]


---


*(id: homeBlockTypeZ · type: content-type · surfaces: [Homepage, Hub, PLP, FLP] · status: defined)*


# product-list-Z (Block Z — Link Hub)

> **Labels:** Redesign of the old "List of products" block into a flexible **Link Hub**. Structure (block + groups + items, crawlable `<a>`, SSR, no schema, `displayType`, `showMore`, `showDescription`, manual/rule sourcing) = **V1·BUILD**. Content discipline (anchor-text = name-not-slug, heading hygiene, de-dup, curated copy) = **V1·GUIDELINE**. Rule-mode targets **blog · product · subcategory · theme · brand = V1·BUILD**; **helpcenter · wiki = V2** (manual/rich-text in V1 until a purpose-built field/type exists). `bundleGroup` retained as a V1 manual-compat source.

Block Z is a configurable **Link Hub** — an overview of links **at scale** to subcategories, products, theme pages, brands, blogs, helpcenter/wiki articles or other lists, placed on **main / hub pages** (homepage, category hubs) and also on PLPs/FLPs. It serves **customers** (wayfinding) **and crawlers** (PageRank distribution + discovery). It is **NOT the visual product grid** (that is [[productCollection]] / B5). Each group is a `linkGroup`; each link a `linkItem`. (Baymard frames this as an intermediary-category navigational hub; the print-to-order vertical is explicitly in scope.)

## How it works in Contentful

A `homeBlockTypeZ` block owns one H2 (`title`) + optional `intro`, a `displayType` (text or chips), and the visibility toggles `showDescription` and `showMore`. It references an ordered set of **`linkGroup`** entries. Each group has a heading (optionally linked), an optional header image, and a **`source`**: either **manual** (a curated list of `linkItem`s) or **rule** (a live query — "all blogs under this subcategory", etc.). In rule mode the anchor label + description are read **live from the target entries**, so exhaustive lists ("all wiki articles") never get hand-authored. The block is **localized** — curated links genuinely differ per market, and rule mode resolves per locale automatically (NL blogs on NL pages). *(This is the opposite of [[filter-engine-AZ]], which is non-localized because it stores universal catalogue keys.)*

## Field model — `homeBlockTypeZ` (the block)

| field | type | localized? | notes | phase/type |
|---|---|---|---|---|
| `name` | Symbol | no | Admin label (internal) | V1·BUILD |
| `title` | Symbol | yes | Section heading (**H2**) · Title Format H2 / H3 / Span | V1·BUILD |
| `intro` | Text / RichText | yes | Optional short intro under the H2 (context / SEO) | V1·BUILD (slot) · copy V1·GUIDELINE |
| `displayType` | Enum (`text` \| `chips`) | no | How links render: text list or chips/pills. **No tiles/carousel.** Descriptions render in text mode; chips are label-only → `showDescription` + chips falls back to text rows | V1·BUILD |
| `showDescription` | Boolean | no | Render each link's description (text mode) | V1·BUILD |
| `showMore` | Boolean | no | Collapse each group to the first **5** links + an in-place "Show more" expander (no navigation) | V1·BUILD |
| `columns` | Integer | no | Desktop column count for the groups | V1·BUILD |
| `groupBySection` | Boolean | no | Render groups under section headings vs one flat set | V1·BUILD |
| `groups[]` | Array · Link → `linkGroup` (legacy `bundleGroup` accepted) | yes | Ordered link-groups. New entries = `linkGroup`; legacy `bundleGroup` accepted as a V1 manual-compat source | V1·BUILD |

**Superseded from the as-is model:** `categories[]` → `groups[]`; `showAsTile` → `displayType`; `showAllText` / `showAllLink` → **removed** (the in-place `showMore` replaces the block-level "Show all"; a "see fuller page" link is the group's `headingLink`); `shouldShowPerShop` → **removed** (locale-level, §3.15).

## Field model — `linkGroup` (new — the section/column)

| field | type | localized? | notes | phase/type |
|---|---|---|---|---|
| `name` | Symbol | no | Admin label (internal) | V1·BUILD |
| `heading` | Symbol | yes | Group heading (**H3** or styled, not a stacked H2) · optional link via `headingLink` | V1·BUILD (field) · heading hygiene V1·GUIDELINE |
| `headingLink` | Link → Entry | optional | Group-title destination (axis / hub / "see all" fuller page) | V1·BUILD |
| `image` | Link → Asset | optional | Optional group header image; alt from the linked [[asset]] (`Description`) | V1·BUILD |
| `source` | Enum (`manual` \| `rule`) | no | How items populate | V1·BUILD |
| `items[]` | Array · Link → `linkItem` | yes (manual mode) | Curated, ordered links | V1·BUILD |
| `rule` | object (see Rule source) | no (rule mode) | A live query that resolves the link set | V1·BUILD · helpcenter/wiki targets V2 |

## Field model — `linkItem` (new — per-link, manual mode)

| field | type | localized? | notes | phase/type |
|---|---|---|---|---|
| `label` | Symbol | yes | Anchor text — the product / page / filter **name, not the raw slug** (the live `/standardflyers`-style slug links are the defect to fix) | V1·BUILD (field) · name-not-slug V1·GUIDELINE |
| `description` | Text | yes | One line, rendered when `showDescription` is on (text mode) | V1·BUILD (slot) · copy V1·GUIDELINE |
| `target` | Link → Entry (**polymorphic**) | — | Destination — see Targets below | V1·BUILD |
| `thumbnail` | Link → Asset | optional | Optional icon / thumbnail; alt from the linked [[asset]] (`Description`) | V1·BUILD |

## Rule source (`linkGroup.rule`)

| key | shape | notes | phase/type |
|---|---|---|---|
| `targetType` | enum | subcategory · theme · product · brand · blog · helpcenter · wiki | V1·BUILD (subcat/theme/product/brand/blog) · helpcenter/wiki V2 |
| `scope` | selector | what to pull: children-of-subcategory · tagged-with · related-to. **Default = the subcategory of the host page** | V1·BUILD |
| `sort` | enum | popularity · alphabetical · newest · manual | V1·BUILD |
| `limit` | integer | max items (pairs with `showMore` showing 5 first) | V1·BUILD |
| `pinned[]` | Array · Link → Entry | optional hand-picked links pinned on top; the rule fills the rest | V1·BUILD |

In rule mode the `label` = the target's name field and `description` = the target's excerpt/summary, **read live** from each target entry. **Empty rule result → the group is hidden.**

## Targets (polymorphic)

| targetType | Contentful type | label source | description source |
|---|---|---|---|
| subcategory / theme | [[pageHomeModular]] | `Title` (H1) | `introParagraph` |
| product | `product` | product name | — |
| brand | brand entries (via [[brands-blockC]] `homeBlockTypeC`) | brand name | — |
| blog | `Page Article` | Article title | `Summary description` ([[blog-teaser-AJ]]) |
| helpcenter | rich text (V1) → dedicated field/type (V2) | — (manual V1) | — |
| wiki | rich text (V1) → dedicated field/type (V2) | — (manual V1) | — |

Exact name/description field IDs per type are read from live Contentful entries at build (the four V1 targets are already modelled in the brain). `helpcenter`/`wiki` are valid `targetType` values now but **manual-only in V1**; rule-mode listing for them waits on the purpose-built field/type (V2).

## Display & settings · mobile contract

- **text** — vertical link list, grouped under headings when `groupBySection`; descriptions shown when `showDescription`.
- **chips** — wrapping pill list; label-only (turning on `showDescription` with chips falls back to text rows).
- **showMore** — each group renders its first **5** links and tucks the rest behind an in-place "Show more" expander (resolves the old per-column show-all residual, Z-4).
- **Mobile** — text lists reflow; chips wrap; with `showDescription` on they reflow to stacked title + description rows; groups stack single-column; popular rows can render as a horizontal chip strip. Block owns one **H2**, group headings are **H3**.

## Use cases

- Current: shop-by-attribute (material / size / colour), sibling-category linking, subcategory navigation.
- Added: theme / seasonal / collection links; featured brands; cross-category "you may also need"; popular / trending / top-seller links; related-searches clusters; buying-guide / editorial / inspiration links; A-Z index.
- Rule-mode at scale: **list of all blogs · all helpcenter articles · all wiki articles · all products and subcategories — per subcategory** (these are exhaustive and never hand-authored, which is why rule sourcing exists).

## Per-surface usage & deltas

- **Homepage + category hubs** → primary surface: the curated/rule-driven Link Hub directing customers and crawl to the most important destinations `[V1·BUILD]`.
- **PLP** → below the visual grid (it carries links → §B4 no-links-above-grid) `[V1·BUILD]`.
- **FLP** → the crawlable internal-linking / "shop by [axis]" surface, rendering lower; the visual results grid is B5 ([[productCollection]]). **Both render on an FLP** — Z is the text-link directory, B5 is the grid; Z is **not** the legacy grid replaced by B5 (Z-2) `[V1·BUILD]`.

## Requirements behaviour

- **Anchor text.** MUST render the product / filter / page **name** as anchor text — never the raw slug (Z-3) `[V1·GUIDELINE]`.
- **Crawlable.** Each link a real `<a>` to the canonical URL; group title links to the axis / hub where relevant; all SSR `[V1·BUILD]`.
- **Heading hygiene.** Block owns one H2; group headings = H3 or styled text, never stacked H2s `[V1·GUIDELINE]`.
- **De-dup.** Feeds the internal-link graph + cannibalisation scorer ([[g-keywords-scoring]]); de-dup = SHOULD guideline, not build-enforced `[V1·GUIDELINE]`.
- **Schema.** **No schema** — a text-link directory, never `Product` / `ItemList` ([[g-schema]]) `[V1·BUILD]`.
- **Localization.** Block Z **is localized** — manual groups/items authored per locale; rule mode resolves per locale automatically. (Contrast: [[filter-engine-AZ]] is non-localized.) `[V1·BUILD]`

## Migration & compatibility

- **Keep the `homeBlockTypeZ` ID** — the block evolves in place; existing references keep working.
- **`bundleGroup` is retained as a V1 manual-compat `groups[]` source** so the ~1006 live `bundleGroup` entries keep rendering; new hubs author `linkGroup` / `linkItem`. As-is `bundleGroup` field IDs (verified live 2026-06-05): `name · title · link · items[] · imageTile · slug · prestaContentKey`; `homeBlockTypeZ` as-is: `name · title · categories[] · showAsTile · showAllText · showAllLink · shouldShowPerShop`. `prestaContentKey` is legacy and dropped from the new `linkGroup`/`linkItem` types.
- **Migration `bundleGroup` → `linkGroup`/`linkItem`** is owned by the content-generation engine (out of scope here).

## Decisions (locked)

- **Block Z = a Link Hub** — block + `linkGroup`s + `linkItem`s; crawlable `<a>`, SSR, no schema; for customers + crawlers; primary on homepage + category hubs, also PLP/FLP. Supersedes the as-is "List of products" model.
- **Block settings** — `title · intro · displayType (text|chips) · showDescription · showMore (collapse >5) · columns · groupBySection · groups[]`.
- **`linkGroup`** — `heading · optional headingLink · optional image · source (manual|rule) · items[] | rule`.
- **`linkItem`** — `label (name-not-slug) · description · polymorphic target · optional thumbnail`.
- **Rule source** — `targetType · scope (default = host-page subcategory) · sort · limit · pinned[]`; label/description read live from targets; empty result hides the group.
- **Targets** — subcategory/theme (`pageHomeModular`), product (`product`), brand (`homeBlockTypeC`), blog (`Page Article`) are V1; helpcenter + wiki are V2 (manual V1).
- **Localized** (per-market curation; rule resolves per locale). **Anchor = name, not slug.** **No schema.** **One H2 / H3 group headings.**
- **Z-1/Z-2/Z-3/Z-4 resolved** — field model locked; Z↔B5 split confirmed; anchor=name; per-column show-all = `showMore`.
- **§3.15** — `shouldShowPerShop` removed (locale-level).

## Open points

- **helpcenter / wiki dedicated field/type** — rule-mode listing for these is V2 (manual / rich-text in V1) until the purpose-built field exists.
- **Target name/description field IDs** — confirm exact IDs per target type from live Contentful at build (the four V1 targets are modelled; the picker reads them live).

## Sources

- Block Z redesign co-definition (Niels, 2026-06-08) — Link Hub goal, displayType text/chips, showDescription, showMore≤5, `linkGroup`/`linkItem`, rule sourcing, targets, localization, mobile contract.
- PLP Catalog v1.5 §Block Z + BUILD-BRIEF §3.22 — as-is field model, anchor-text fix, Z↔B5 split, below-grid, no schema.
- Ecommerce link-hub research — Baymard (intermediary category page: subcategory tiles, brands, cross-category, editorial; print-to-order vertical), Break The Web (homepage-as-hub, related-collections, sender/receiver internal linking).
- Contentful live read (space `wm1n7oady8a5`/master, 2026-06-05) — as-is `homeBlockTypeZ` + `bundleGroup` field IDs (for the compat layer).

Related: [[productCollection]] · [[filter-engine-AZ]] · [[pageHomeModular]] · [[blog-teaser-AJ]] · [[brands-blockC]] · [[asset]] · [[g-schema]] · [[g-keywords-scoring]] · [[surface-FLP]] · [[surface-PLP]]


---


*(id: promoCard · type: content-type · surfaces: [PDP, PLP, FLP] · status: draft)*


# Promo Card (promoCard)

> **Labels:** V1·BUILD ×6 · V1·GUIDELINE ×5 · V2·BUILD ×2 · MIXED ×1. **Phase split:** PLP/FLP **BG carousel (B10) = V1**; PDP **B6 in-grid = V2 on PLP/FLP / V1 on PDP**; FLP in-grid B6 = V2. **Per §8** every field/rule carries a phase + type tag inline.

A special card placed inside a [[productCollection]] grid (and inside the PLP/FLP promo-cards carousel) that surfaces a CTA, a coupon, or a "design online" prompt. It renders in the visual slot of a product tile but is not a product. Polymorphic — one content type, three authoring shapes.

## How it works in Contentful

A `promoCard` entry is referenced from one of two places:
- **In-grid** — added to a [[productCollection]] `items[]` array, occupying one tile slot. **Max 1 promoCard per Block D grid** (CF custom validator; publish fails if two). This is the PDP **B6** in-grid card.
- **In a carousel** — referenced from a `homeBlockTypeBG` (Block BG) `Items[]` array, which renders the PLP/FLP **B10** promo-cards carousel above the product grid. BG/BH share the card model (see [[product-list-Z]] / `homeBlockTypeBH` for the page-card nav variant).

Three authoring shapes, driven by `buttonStyle`:
1. **Standard CTA promo** — headline + subtitle + button to a product/page/URL.
2. **Coupon-code promo** — adds a linked [[promoCode]] and a **Copy button** that copies the code to the clipboard (no destination).
3. **Design-online promo** — Design-now button (blue) routing to the design tool (replaces the killed Canva block AT).

The renderer reads `image` at the row's `productsPerRow` aspect; `backgroundDisplayOption` decides whether the card is a green panel (optional overlay image) or a full-bleed image; `buttonStyle` picks both the button colour and the destination-resolution path.

## Field model

| field | type | localized? | phase/type | notes |
|---|---|---|---|---|
| `name` | String | no | V1·BUILD | Admin label, not rendered |
| `title` | String | yes | V1·BUILD | Headline; supports `<br>` |
| `subtitle` | RichText | yes | V1·BUILD | **Upgraded from plain string (v0.18)**; [[contentMedia]] `content` HTML rules; auto bottom spacing to the promo code. T&Cs body lives here, NOT on [[promoCode]] |
| `image` | Link to Asset | asset-level localizable, optional | V1·BUILD | Renders at the row's `productsPerRow` aspect |
| `imageFocalPoint` | Enum | — | V1·BUILD | Crop focal point (center / top / bottom / left / right) |
| `backgroundDisplayOption` | Enum (2) | — | V1·BUILD | **Primary colour** (green `--color-primary`, optional overlay image, top greyed for WCAG-AA legibility) · **Full image** |
| `buttonStyle` | Enum (4) | — | V1·BUILD | **NEW v0.18.** Shop now (green) · Design now (blue `--color-design`) · Read more (default) · **Copy button** (copies `promoCode.code` to clipboard; no destination) |
| `buttonText` | String | yes, optional | V1·BUILD | **NEW v0.18.** Defaults per style: Shop now→"Shop now", Design now→"Design now", Read more→"Read more", Copy button→"Copy and claim" |
| `destinationProduct` | Link → `product` | optional | V1·BUILD | Only when `buttonStyle` ≠ Copy button (first in the 3-way chain) |
| `destinationPage` | Link → `pageHomeModular` | optional | V1·BUILD | Used when `destinationProduct` empty |
| `destinationUrl` | String | optional | V1·BUILD | Used when product + page both empty |
| `promoCode` | Link → [[promoCode]] | optional | V1·BUILD | **Required when `buttonStyle` = Copy button** |
| ~~`ctaButton`~~ | ~~Link to Entry~~ | — | V1·BUILD (remove) | **Removed** — replaced by inline `buttonStyle` + `buttonText` + 3-way destination |
| ~~`shouldShowPerShop`~~ | — | — | V1·BUILD (remove) | **Removed** — per §15, visibility is locale-level (empty localized content → omit) |

**Destination resolution (CTA shapes):** `destinationProduct` → `destinationPage` → `destinationUrl`. Not evaluated for the Copy-button shape.

## Per-surface usage & deltas

- **PDP — B6 in-grid (inside Block D `items`). [V1·BUILD]** Max 1 per grid. Position is author discipline (not enforced) **[V1·GUIDELINE]**: ideally first row on the right (last position of row 1; carousel = second card of the first slide; mobile = position 2).
- **PLP / FLP — B10 promo-cards carousel (Block BG `homeBlockTypeBG`). [V1·BUILD]** V1, manual. Two card uses within BG:
  - **Cluster card [V1·GUIDELINE]** — lifestyle image (not the Shopping-feed canonical), action-led headline ≤10 words, one benefit sentence 12–25 words, **no discount label**, CTA "See collection" / "Shop [cluster]" → a PLP.
  - **Discount card [V1·BUILD]** — Homepage-only. Catalog image (= `Product.image` + feed image), headline = product name ≤6 words, was/now both SSR from the pre-set price path, auto discount label `(was−now)/was` 5%-bucketed in a real `<span>` top-left, CTA "Shop now"/"Bestel nu" or "Copy and claim" + code for a coupon card. **Rendered as a distinct promo treatment [V1·GUIDELINE]** — framed promo panel + a discount **flash badge** + emphasised now-price — so it reads as a promotion, not a plain [[bundleItem]] catalog tile, even though it reuses the catalog image + was/now.
  - Each card carries its own headline level (Title Format H2/H3/Span) — BG has no block-level heading. **[V1·BUILD]** Discount-card mode (single-SKU → PDP + `Product`/`Offer` JSON-LD vs sub-category → no Product JSON-LD, "vanaf -15%") is set by `promo.scope`, never editorially **[V1·BUILD]**.
  - The **B6 in-grid card on PLP/FLP is V2·BUILD**; the **BG carousel (B10) is V1·BUILD**. FLP V1 grids are 24 products with **no promo card [V1·KEEP]**; FLP B6 in-grid is a **V2·BUILD** Block AZ filter-setting (slot 4, replaces a product — never a 25th cell).
- **`homeBlockTypeBH` [V1·BUILD]** requires exactly one `promoCard` plus a `subitems[]` page-card set (see [[g-pagecard]]); same card model.

## Requirements behaviour

- **Crawlable: [V1·BUILD]** card heading is a styled span (not a heading tag), subtext, and CTA in a single real `<a>` with descriptive anchor; SSR. Promo code shown as **real text, never an image**.
- **CTA targeting (B6/B10): [V1·GUIDELINE]** never to the same PLP URL; always to a higher-converting page (PLP / PDP / transactional), never informational/lower-intent; same-domain only; no UTM on same-domain links.
- **Banned copy: [V1·GUIDELINE]** no fake urgency / countdowns / "Limited time only" / "Don't miss out" / fake scarcity.
- **Activation (BG): [V1·BUILD]** the carousel renders only when ≥1 active promo card exists for page × locale; per-card date window respected; locale-scoped; **event-driven cache** (not TTL) — see [[cache]]. Outside the window the card is removed server-side and the product grid rebalances.
- **Image source: [V1·GUIDELINE]** brand-green default with top greyed for legibility; full-image variant min 800×800. Discount-card pricing obeys the one-pre-set-path consistency contract (tile = PDP = ad feed) **[V1·BUILD]**.
- **No schema of its own [V1·BUILD]** — a discount card in single-SKU mode contributes a `Product`/`Offer` node via the destination product; otherwise none.

## Decisions (locked)

- **§6** — [[productCollection]] `items` accepts `bundleItem` AND `promoCard`; max 16 total, **max 1 promoCard** (CF validator).
- **§8** — shared `cta` enum (`Shop now · Discover our collection · Design now · Read more · Custom`); the promoCard `buttonStyle` enum exposes Shop now / Design now / Read more plus the promoCard-specific **Copy button**.
- **§3 (card label)** — distinct from the merged [[card-label]] model; promoCard styling uses `backgroundDisplayOption`, not the badge colours.
- **§15** — `shouldShowPerShop` dropped; locale-level visibility via empty localized content.
- **§7** — no video on promo cards (cards are static-image only).

## Open points

- BG page-scope is an **editorial guideline in V1** (not field-gated); `PageTypeVariation` is analytics-only. A page-type flag formally gates BG eligibility per PLP Req §3, but the catalog (2026-06-02) downgrades it to editorial — flagged.
- PLP catalog tags B6 in-grid as V2 and BG (B10) as V1; the BG header's `data-version=v2` is a documented doc error (treated as v1).

## Sources

- PDP Catalog v0.20 §1.4 (promoCard v2 field model; max-1 validator; position rule).
- PLP Catalog v1.5 — "Promo Card · promoCard → B6 + B10", "Block BG (Promo Cards Carousel)", "Block BH".
- PLP Req v1.13 §B6 (in-grid promo/editorial card), §B10 (BG promo cards block).
- FLP Req v0.15 §6 (promo card = V2 Block AZ filter setting; V1 grid = 24 products).

Related: [[promoCode]] · [[productCollection]] · [[g-pagecard]] · [[card-label]] · [[surface-PDP]] · [[surface-PLP]] · [[surface-FLP]] · [[cache]]


---


*(id: promoCode · type: content-type · surfaces: [PDP, PLP, FLP] · status: draft)*


# Promo Code (promoCode)

> **Labels:** V1·BUILD ×3 · V1·GUIDELINE ×1 (`code` real-text rule). Whole entity is V1 (rides on the V1 BG carousel coupon card; also reused by the V2 in-grid B6 coupon card). Per §8 every field/rule carries a phase + type tag.

A small, reusable entity holding a discount code, its display name, and an optional expiry date. It is linked from a [[promoCard]] Copy button; multiple cards can share one code.

## How it works in Contentful

A `promoCode` entry exists independently and is referenced by a [[promoCard]] whose `buttonStyle = Copy button`. The renderer prints the `code` in a chip on the card and copies it to the clipboard on click (button label defaults to "Copy and claim"). If `expiryDate` is set, an "Expires on [localized date]" line renders below the chip; if empty, the line is omitted.

It is a thin display/offer entity — the **terms & conditions body stays on the linked promoCard `subtitle`**, not here. Other offer-engine fields (max discount, per-user limits) remain on the model as-is and are out of scope for the content model.

## Field model

| field | type | localized? | phase/type | notes |
|---|---|---|---|---|
| `name` | String | en only | V1·BUILD | Admin label, not rendered |
| `code` | String | yes | V1·BUILD | The code string (e.g. `BOOKLETS10`); rendered in the chip and copied to the clipboard |
| `expiryDate` | Date | optional | V1·BUILD | **NEW v0.18.** Set → "Expires on [localized date]" line below the chip (replaces the older "Use code [X]" line); empty → line omitted. The "Expires on" label is localized at the renderer level (no field) |
| *(offer-engine fields)* | — | — | V1·KEEP | Max discount / per-user limits etc. kept as-is in v2; not part of the content model — preserve existing offer-engine behaviour |

## Per-surface usage & deltas

- **All surfaces** via the [[promoCard]] Copy-button shape:
  - **PDP — coupon promoCard inside a [[productCollection]] (B6) grid. [V1·BUILD]**
  - **PLP / FLP** — coupon promoCard inside the **Block BG carousel (B10) [V1·BUILD]** ("Copy and claim" + code), or the **in-grid B6 card [V2·BUILD]**.
- No per-surface field difference. One code can be reused across multiple promoCards and surfaces.

## Requirements behaviour

- **Real text, never an image [V1·GUIDELINE]** — the code must be crawler-visible text in the DOM.
- **SSR [V1·BUILD]** — rendered server-side as part of the parent promoCard; clipboard copy is the only client behaviour.
- **No schema of its own [V1·BUILD]**.

## Decisions (locked)

- **§15** — no per-shop field; a code is gated per locale through its parent promoCard's localized content.
- Linked exclusively from the [[promoCard]] Copy-button (`buttonStyle = Copy button` requires a `promoCode`).

## Open points

- None outstanding for the content-model surface. Offer-engine field set (limits/T&C) is owned outside this model.

## Sources

- PDP Catalog v0.20 §1.5 (promoCode v2; `expiryDate` new; T&C stays on promoCard subtitle).
- PLP Catalog v1.5 — "Promo Code · promoCode → B6 / B10 discount cards".

Related: [[promoCard]] · [[productCollection]] · [[surface-PLP]] · [[surface-FLP]]


---


*(id: homeBlockTypeP · type: content-type · surfaces: [PDP, PLP, FLP] · status: draft)*


# Customer Reviews (homeBlockTypeP — Block P)

> **Labels:** V1·BUILD ×5 · V1·GUIDELINE ×2 · V2·BUILD ×2 · MIXED ×1. **Phase split:** PLP/FLP **B8 = V1** (manual + SSR); PDP **B9 = V2** (product-level widget + schema). Company-level `AggregateRating` ships **V1** via the USP bar; the **category-relevant-by-tag** widget + **schema-CI guardrail** are **V1·BUILD**. Per §8 every field/rule carries a phase + type tag.

A Trustpilot review block that surfaces category-relevant testimonials. The reviews are pulled by a tag so the block can show reviews from the right product category — but the block does **not** emit its own category-level rating schema.

## How it works in Contentful

A `homeBlockTypeP` entry is referenced from the page's `Content Blocks`. Editorial picks the category tag (`tagToLoad`) that the Trustpilot widget filters on; the storefront renders the matching reviews server-side. Desktop is a 3-up carousel, mobile 1-up. The widget is cached server-side (last-good) and is CLS-safe.

The key content-model decision (§3.12) is that this block shows category-relevant reviews as a **UI-only Trustpilot widget** — it does **not** emit `AggregateRating` schema at the category level. Only the company-level rating (the [[g-uspbar]] / `Organization` schema) emits a rating. This avoids Google's "category-pooled rating isn't a valid specific item" rule.

## Field model

| field | type | localized? | phase/type | notes |
|---|---|---|---|---|
| `name` | String | no | V1·BUILD | Admin label |
| `title` | String | yes | V1·BUILD | E.g. "What our happy customers say"; supports `<br>` |
| `titleLevel` | Enum | — | V1·BUILD | H2 · H3 · Span (renamed from `titleFormatH1H6`) |
| `contentAlignment` | Enum | — | V1·BUILD | left · center ("right" dropped if unused) |
| `backgroundImage` | Link to Asset | optional | V1·BUILD | Behind the carousel |
| `tagToLoad` | String | yes, optional | MIXED | The category Trustpilot tag the widget filters on. **V1·GUIDELINE: manual** (editorial picks the tag). **V2·BUILD: auto-driven** from the linked product/category; manual = fallback |
| `visualOptions` | Multi-select | — | MIXED | Carousel **[V1·BUILD]** (only live value); grid variant is **V2·BUILD** |
| ~~`shouldShowPerShop`~~ | — | — | V1·BUILD (remove) | **Removed** (§15 — locale-level visibility) |
| ~~`crowdIn`~~ | — | — | V1·BUILD (remove) | **Removed** (tag/space architecture) |

## Per-surface usage & deltas

- **PDP — B9 (V2·BUILD).** Product-level reviews; the whole B9 block is V2 on the PDP. H2 "Why [country] customers choose [product]" **[V2·GUIDELINE]**. Trustpilot product-level widget **[V2·BUILD]**.
- **PLP — B8 (V1·BUILD, manual + SSR).** Category Trustpilot block. Editorial selects testimonials by category tag, pastes the tag into Contentful **[V1·GUIDELINE]**; storefront emits static SSR HTML **[V1·BUILD]**. H2 locked = **"Why [Country] customers choose [category-with-action-verb]" [V1·GUIDELINE]** (category always carries the verb). V2 = automated Product Reviews collection (live API, continuous refresh) **[V2·BUILD]**.
- **FLP — B8.** Two SSR'd surfaces, schema governed separately from UI (locked v0.7):
  - **Surface A — Organization-level Trustpilot widget [V1·BUILD]** (UI only; rating schema already lives sitewide in `Organization`, no FLP-specific schema). Reuses the existing PLP/PDP widget **[V1·KEEP]**.
  - **Surface B — category-scoped Trustpilot widget filtered to this category [V2·BUILD]**, rendered as a "Why [Country] customers choose [category]" block. **UI-only, NO schema.** Prerequisite: Trustpilot reviews must be categorised by product type (data-side integration; without it Surface B can't render).
- **DOM order delta (§18) [V1·BUILD]:** on the **PLP, B9 supporting renders BEFORE B8 reviews**; on the **FLP, B8 reviews render before B9 supporting**. Don't copy FLP's order onto the PLP.

## Requirements behaviour

- **SSR [V1·BUILD]** into the DOM, never lazy-loaded (closes the live-page gap where the H2 renders but the body is empty). Trustpilot widget server-side cached (last-good ≤24h), hydrates after LCP, never blocks the LCP candidate.
- **≥20-review threshold [V1·GUIDELINE]** — on PLP/FLP the block (and any category rating node) is omitted entirely below 20 category-level reviews. No padding with brand-level or sibling-PDP quotes.
- **CLS-safe [V1·BUILD]** — reserved width/height on first paint; if Trustpilot API + cache are both down the widget hides entirely (never zero stars, never a skeleton); logged.
- **Visible aggregate [V1·BUILD]** (stars + score + count + link, SSR) plus 3–5 crawlable testimonials in HTML; each quote carries name + date (ideally role + company) **[V1·GUIDELINE]**; category-specific not generic; locale-filtered.
- **Schema:** the only review/rating schema sitewide is the **company-level `AggregateRating` nested in `Organization` (emitted by [[g-uspbar]]) — V1·BUILD**. The PDP B9 block emits a **product-level `aggregateRating` on the `Product` node (≥20 reviews) — V2·BUILD**. The PLP/FLP review block emits **no category-level AggregateRating** — UI widget only **[V1·BUILD]**. **Schema-CI parity / deploy-block guardrail = V1·BUILD.** See [[g-schema]].

## Decisions (locked)

- **§12 (Reviews)** — drop the category-level `AggregateRating` schema; still show category-relevant reviews via `tagToLoad` (UI-only widget). Company-level rating only emits schema. `tagToLoad` V1 manual → V2 auto. PDP B9 (V2) / PLP·FLP B8 (V1). ≥20-review threshold to render on PLP/FLP.
- **§11 (USP bar)** — the company-level Trustpilot `AggregateRating` lives in [[g-uspbar]] / `Organization`; the widget and schema hide together if the source is down.
- **§2 (Schema)** — three distinct rating scopes, never reused: brand-level (USP bar / `Organization`), category-level (this block — UI only, no schema), product-level (PDP `Product`, ≥20).
- **§15** — `shouldShowPerShop`/`crowdIn` dropped.

## Open points

- PDP B9 is V2 as a block, but the **company-level** rating it depends on ships V1 via the USP bar; only the **product-level** B9 widget/schema is deferred to V2.
- Surface B (FLP) is blocked on Trustpilot category-metadata integration (engineering-owned).

## Sources

- PDP Catalog v0.20 §1.8 (Block P v2 field model; 120 entries; carousel).
- PDP Req v0.34 (B9 product reviews V2, ≥20, AggregateRating product-level; usp-6 Organization rating).
- PLP Catalog v1.5 — "Block P · homeBlockTypeP → B8", "Block 8 — Reviews".
- PLP Req v1.13 §B8 (V1 manual + SSR; H2 lock; category AggregateRating threshold) — superseded on the category-schema point by §3.12.
- FLP Req v0.15 §8 (Surface A + Surface B; UI-only category widget; no FLP schema).

Related: [[g-uspbar]] · [[g-schema]] · [[surface-PDP]] · [[surface-PLP]] · [[surface-FLP]] · [[g-keywords-scoring]]


---


*(id: homeBlockTypeV · type: content-type · surfaces: [PDP, PLP, FLP] · status: draft)*


# General FAQ (homeBlockTypeV + faqItem — Block V)

> **Labels:** V1·BUILD ×7 · V1·GUIDELINE ×5 · V2·BUILD ×1 · V2·GUIDELINE ×1. **Phase split:** **SSR + FAQPage exact-mirror + CI parity gate = V1·BUILD** (all surfaces); the **8 coverage bins + answer/word/internal-link discipline = V1·GUIDELINE**; PDP "coverage bins / real-signal sourcing" enrichment = V2. Per §8 every field/rule carries a phase + type tag.

An accordion of question-and-answer pairs that is also the page's primary AEO surface. `homeBlockTypeV` is the container; each Q&A is a `faqItem` leaf. The visible Q&A and the `FAQPage` JSON-LD are an exact mirror of each other.

## How it works in Contentful

A `homeBlockTypeV` entry is referenced from `Content Blocks`. It holds an ordered `faqItems[]` list, each a `faqItem` leaf with a `question` (one AEO-friendly sentence) and an `answer` (RichText, 30–50 words, first sentence stand-alone). The container carries the block title and the accordion display options. The renderer builds the visible accordion AND the `FAQPage` schema from the same `faqItems` — a build-time parity gate fails on drift. If `faqItems` is empty the whole section is omitted and no `FAQPage` node is emitted.

## Field model

### `homeBlockTypeV` (container)

| field | type | localized? | phase/type | notes |
|---|---|---|---|---|
| `name` | String | no | V1·BUILD | Admin label |
| `title` | String | yes | V1·BUILD | E.g. "Frequently asked questions"; supports `<br>` |
| `titleLevel` | Enum | — | V1·BUILD | H2 · H3 · Span (renamed from `titleFormatH1H6`) |
| `faqItems` | Multi-Link → `faqItem` | — | V1·BUILD | Ordered list; B11/B13 expect **8–11** items **[V1·GUIDELINE on the count]** |
| `visualOptions` | Multi-select (4) | — | V1·BUILD | Collapsible · Collapsible on mobile · Show in two column · Show title inside block |
| ~~`shouldShowPerShop`~~ | — | — | V1·BUILD (remove) | **Removed** (§15 — locale-level visibility) |

### `faqItem` (leaf — canonical Q&A pair)

| field | type | localized? | phase/type | notes |
|---|---|---|---|---|
| `name` | String | no | V1·BUILD | Admin label |
| `question` | String | yes | V1·BUILD | One sentence, AEO-friendly **[V1·GUIDELINE on phrasing]** |
| `answer` | RichText | yes | V1·BUILD | [[contentMedia]] `content` HTML rules; 30–50 words; first sentence stand-alone for AI Overviews; internal links via the CF entry picker **[V1·GUIDELINE on word count/AEO/link rules]** |

**Name collision resolved (§5):** the canonical FAQ leaf is `faqItem` with `question` + `answer`. The **legacy flat `faqItem`** (3,264 entries, separate Q/A entries paired by array position via an `isQuestion` boolean) is deprecated → migrate to `questionAndAnswer`, then archive after a grace period. The PDP catalog used the name `faqItem` for both schemas; this model keeps `faqItem` as the new Q+A leaf and renames the legacy model `questionAndAnswer`. See Open points.

## Per-surface usage & deltas

- **PDP — B11.** **V1·BUILD:** Q+A in HTML, H3 per question, collapsed by default, `FAQPage` schema, AEO. **V2:** coverage bins, real-signal sourcing **[V2·BUILD]**, 8–11 count, 30–50-word answers, internal-link rules **[V2·GUIDELINE]**. The PDP FAQ is per-SKU detail.
- **PLP — B13. [V1·BUILD]** Category-level orientation. **8 coverage bins [V1·GUIDELINE]** (orientation/decision · comparison across category · material/paper/finish overview · pricing range · lead time/delivery range · file preparation overview · returns & reprint policy · eco/sustainability) plus **2–3 free-form slots [V1·GUIDELINE]** from weekly real signals (GSC, PAA, CS tickets, forums, competitor FAQs). H2 = "Veelgestelde vragen over [category]" / "FAQ about [category]" **[V1·GUIDELINE]**.
- **FLP — B13. [V1·BUILD]** Same 8 bins **[V1·GUIDELINE]**; each indexed URL carries **unique** FAQ content (no sharing across indexed URLs) **[V1·GUIDELINE]**; filter-axis questions may link to attribute URLs or bestseller PDPs but must NOT duplicate the B7 attribute deep-dive **[V1·GUIDELINE]**.
- **Indexation contribution (PLP/FLP) [V1·BUILD]:** B13 ≥5 entries (or B14 present) is one of the INDEX-1 conditions — see [[g-meta]].

## Requirements behaviour

- **SSR [V1·BUILD]** — full Q+A in the DOM regardless of expand state; never JSON-LD only.
- **Single-open accordion [V1·BUILD]** on mobile + desktop; first question open by default; desktop 2-column if "Show in two column", else 1-column; mobile always 1-column.
- **FAQPage JSON-LD = exact DOM mirror [V1·BUILD]**, emitted server-side; build-time parity gate (drift = fail). B14 SEO text is excluded from `FAQPage`.
- **Empty state [V1·BUILD]** — empty `faqItems` → omit the section AND emit no `FAQPage` node.
- **Answer rules [V1·GUIDELINE]** — 30–50 words; first sentence stand-alone extractable (AEO); customer phrasing; no fluff.
- **Anti-cannibalisation [V1·GUIDELINE]** — no question contains the exact hub keyword; PLP FAQs don't repeat PDP FAQs; no overlap with B9/B14 (scorer flags). See [[g-keywords-scoring]].
- **Internal linking [V1·GUIDELINE]** — 2–4 links; priority child PDPs → sub-category PLPs → use-case landing → CS/help; never a sibling PLP.

## Decisions (locked)

- **§5** — FAQ leaf = `faqItem` (`question` + `answer`); legacy flat `faqItem` deprecates → `questionAndAnswer`.
- **§2 (Schema)** — `FAQPage` is the exact DOM mirror; empty → omit + no schema; spam guardrail (schema maps to visible DOM); CI validation deploy-blocking. PDP `FAQPage` is a sub-node of the `Product` schema.
- **§15** — `shouldShowPerShop` dropped; per-shop FAQs dropped.

## Open points

- The legacy `faqItem` → `questionAndAnswer` migration (3,264 entries) and 4-week archive grace are operational, not blocking the content model.

## Sources

- PDP Catalog v0.20 §1.7 (Block V v2; faqItem sub-schema; 922 entries), §1.10 (legacy faqItem deprecation).
- PDP Req v0.34 (B11 FAQ; FAQPage exact-mirror; AEO answer rules).
- PLP Catalog v1.5 — "Block V · homeBlockTypeV + faqItem → B13".
- PLP Req v1.13 §B13 (8 bins, 2–3 free-form, single-open, FAQPage mirror, internal-link cap).
- FLP Req v0.15 §13 (SSR FAQ; unique per indexed URL; filter-axis questions).

Related: [[g-schema]] · [[g-keywords-scoring]] · [[contentMedia]] · [[surface-PDP]] · [[surface-PLP]] · [[surface-FLP]]


---


*(id: video · type: content-type · surfaces: [PDP, PLP, FLP] · status: draft)*


# Video (video)

> **Labels:** V1·BUILD ×8 · V1·GUIDELINE ×2 · V2·BUILD ×2 · MIXED ×1. **Phase split:** the **`video` block + `VideoObject` JSON-LD + autoplay/perf behaviour = V1·BUILD** (all surfaces; PLP/FLP default V1-available); **transcript / VTT captions + WebM + extended-length pilot = V2·BUILD**; PDP **hero-gallery product video = V2 (MIXED on the B3 hero)**. Per §8 every field/rule carries a phase + type tag.

A standalone body block that renders a single video (external URL or direct upload) with a `VideoObject` JSON-LD node. It supports autoplay-on-scroll behaviour and may sit in the PDP hero gallery, but it is **never rendered on a product-grid card**.

## How it works in Contentful

A `video` entry is added to `Content Blocks` and author-positioned in the body flow. It accepts either an external `videoUrl` (YouTube/Vimeo) or an uploaded `videoFile` (MP4/GIF); when both are set the uploaded `videoFile` wins. A `description` (50–200 words) feeds the `VideoObject` JSON-LD. `visualOptions` chooses autoplay-on-scroll vs click-to-play; mobile is always click-to-play. On PDP it can also be placed in the hero gallery via the product-level `productVideo` field (not a hard-coded position).

## Field model

| field | type | localized? | phase/type | notes |
|---|---|---|---|---|
| `name` | String | yes | V1·BUILD | **Promoted to localized in v0.20.** Admin + visible title |
| `description` | RichText | yes | V1·BUILD | **NEW v0.20.** 50–200 words **[V1·GUIDELINE on length/AEO]**; feeds `VideoObject` description; AEO-friendly |
| `videoUrl` | String | yes, optional | V1·BUILD | External YouTube / Vimeo URL |
| `videoFile` | Link to Asset | optional | MIXED | **NEW v0.20.** MP4 (soft 8 MB / hard 25 MB) or GIF (soft 2 MB / hard 5 MB) **[V1·BUILD]**. **Wins over `videoUrl` when both set.** WebM optional **[V2·BUILD]** |
| `thumbnail` | Link to Asset | optional | V1·BUILD | Poster-frame override; empty = auto-extract first frame (or YouTube thumbnail) |
| `loop` | Boolean | — | V1·BUILD | **NEW v0.20.** Default OFF for MP4; GIFs always loop natively (flag ignored) |
| `visualOptions` | Enum (2) | — | V1·BUILD | **NEW v0.20.** "Autoplay on scroll" (default) · "Click to play" |
| ~~`videoPlaceholder`~~ | — | — | V1·BUILD (remove) | **Removed** → `thumbnail` + auto first-frame |

## Per-surface usage & deltas

- **PDP** — standalone body video block (author-positioned in `Content Blocks`) **[V1·BUILD]**, AND may sit in the **PDP hero gallery** via the product-level `productVideo` field (not hard-coded to position 2) **[V2·BUILD — MIXED on the B3 hero]**. **NOT** rendered on Block D / [[productCollection]] cards (v0.20 lock: cards are static-image only) **[V1·BUILD]**.
- **PLP / FLP** — author-positioned body block (category/use-case explainer or inspiration video) **[V1·BUILD]**, best on broad/industry/themed pages, occasional support on category PLPs **[V1·GUIDELINE]**. **Not a hero, not on product tiles, not on Block D / BI cards. [V1·BUILD]** PLP catalog default = V1-available (existing shared type, low cost to enable); flip to V2 to defer.

## Requirements behaviour

- **Autoplay-on-scroll (desktop): [V1·BUILD]** muted autoplay when ≥50% in viewport (IntersectionObserver), lazy-load, honours `prefers-reduced-motion` (static poster, no autoplay). Sound muted by default in both modes; an unmute overlay is always rendered.
- **Mobile (≤768px): [V1·BUILD]** always click-to-play (poster + play button) regardless of the authored option.
- **Performance: [V1·BUILD]** lazy-loaded, zero LCP cost below the fold; **above-fold autoplay videos must be ≤500 KB compressed** (mobile LCP budget — see [[g-mobile]]).
- **VideoObject JSON-LD (auto-emitted at build time): [V1·BUILD]** `name` · `description` · `thumbnailUrl` · `uploadDate` = `sys.publishedAt` (refreshes on every content edit) · `duration` (auto from `videoFile` metadata or the YouTube API) · `contentUrl`/`embedUrl`. Transcript/VTT captions deferred to **V2·BUILD**. See [[g-schema]].
- **File caps: [V1·BUILD]** MP4 H.264 1080p soft 8 MB / hard 25 MB; GIF soft 2 MB / hard 5 MB (warning at soft, publish-block at hard). Prefer MP4 over GIF for new content **[V1·GUIDELINE]**.

## Decisions (locked)

- **§7** — no video on product-grid cards on any surface; `video` is a standalone body block and **MAY sit in the PDP hero gallery** (do not say "never a hero").
- **§2 (Schema)** — `VideoObject` must map to a visible video (spam guardrail); drift = build fail; CI validation deploy-blocking.
- **§15** — no per-shop field; locale-level visibility via empty localized content.

## Open points

- WebM support and transcript/VTT captions are V2.
- Extended video length/quality testing (Lighthouse + engagement pilot) is a V2 deferral.

## Sources

- PDP Catalog v0.20 §1.9 (Video v2: description / videoFile / loop / visualOptions; VideoObject; no Block D card video; hero gallery via productVideo).
- PDP Req v0.34 (B3 hero MIXED — product video V2; §14 video; mob ≤500 KB above-fold autoplay).
- PLP Catalog v1.5 — "Content-type logic — Video block (migrated)".

Related: [[productCollection]] · [[g-schema]] · [[g-mobile]] · [[surface-PDP]] · [[surface-PLP]] · [[surface-FLP]]


---


*(id: person · type: content-type · surfaces: [PDP, PLP, FLP] · status: draft)*


# Person (person)

> **Labels:** V2·BUILD ×6 · V2·GUIDELINE ×4. **Phase split:** the **whole `Person` content type + byline block is a V2 test on every surface** (PDP B-PM / PLP·FLP B15) — config-driven on/off, cohort-vs-control. The **`Person` schema + LinkedIn `rel="me"` build** and the **cohort/control A/B test** are both V2. (No V1 rows — the brief's "Person schema + rel=me [V1·BUILD]" refers to the *engineering pattern being build-not-guideline*; its phase is V2 because the whole block is a V2 test. Flagged in Open points.) Per §8 every field/rule carries a phase + type tag.

A NEW combined content type holding one canonical identity for a product manager / expert. It powers the E-E-A-T authority byline (the "Productmanager" test) across all surfaces. There is **one Person entity** per individual; the category-specific expertise sentence and contact CTA do NOT live on the Person — they live on the per-page byline block that references it.

## How it works in Contentful

A `person` entry holds the stable identity: name, job title, headshot, LinkedIn URL, and the categories they know about. A per-page **byline block** (PDP B-PM / PLP·FLP B15) references one `person` and adds the page-specific copy: the category-specific expertise sentence and the contact CTA. So one product manager who covers several categories is a single `person` entry, surfaced with different expertise sentences on each page — this is deliberate, an anti-cannibalisation pattern (one canonical identity, varying surface copy). The PM hub lives at `/cs/team/`. The byline emits `Person` JSON-LD built from the `person` identity fields.

## Field model

### `person` (canonical identity)

| field | type | localized? | phase/type | notes |
|---|---|---|---|---|
| `name` | String | no | V2·BUILD | Person's full name |
| `jobTitle` | String | yes | V2·BUILD | Role / category title (e.g. "Booklets Product Manager") |
| `image` | Link to Asset | optional | V2·BUILD | Real headshot, consistent style; no stock photos **[V2·GUIDELINE]** |
| `linkedIn` | String (URL) | no | V2·BUILD | LinkedIn profile; authority anchor — link rendered with `rel="me"` (and used as schema `sameAs`) |
| `knowsAbout` | Multi-ref / list | — | V2·BUILD | The categories this person is an expert in; drives schema `knowsAbout` (category noun) |

### Per-page byline (lives on the referencing block, NOT on `person`)

| field | type | localized? | phase/type | notes |
|---|---|---|---|---|
| `person` | Link → `person` | — | V2·BUILD | The canonical identity referenced by this page's byline |
| expertise sentence | RichText / String | yes | V2·GUIDELINE | **Category-specific**, written for this page's category — not a generic bio; authored per page × locale |
| contact CTA | String / Link | yes | V2·GUIDELINE | Page-specific "ask the expert" / contact prompt |

> The split is the §3.4 decision: identity on `person` (one entity), category-specific sentence + CTA on the byline (varies per page).

## Per-surface usage & deltas

- **PDP — B-PM (Product Manager), V2 test.** 6 BUILD rows **[V2·BUILD]**; E-E-A-T test; `Person` schema + LinkedIn `rel="me"` **[V2·BUILD]**; config-driven on/off **[V2·BUILD]**. Same PM appears on the cluster's PDPs.
- **PLP — B15 (Productmanager), fully V2.** H2 = "Questions? We're happy to help" / "Meet your product manager" **[V2·GUIDELINE]**. Position between FAQ (B13) and SEO text (B14), or under SEO text **[V2·BUILD]**. One PM may cover multiple categories (same Person entity, category-specific surface).
- **FLP — B15, V2 cohort-vs-control test [V2·BUILD].** Inherits PLP §B15 verbatim; **no FLP-specific delta**. Block sits between B14 SEO text and the empty-state safety net in the FLP DOM order.
- Across surfaces this is a **V2 test [V2·BUILD]** — config-driven on/off per page or per category; cohort vs control tracked weekly (Brand Radar SoV, top-15 keyword count, organic revenue, AI-citation); promotion criterion **≥5% SoV lift over control** across an 8-week window **[V2·GUIDELINE]**.

## Requirements behaviour

- **Real person only [V2·GUIDELINE]** — name + photo + category-specific role + LinkedIn; no stock photos, no anonymised "customer service team".
- **LinkedIn = authority anchor [V2·BUILD]** — link carries `rel="me"` to mark identity (AEO).
- **Category-specific expertise sentence [V2·GUIDELINE]** per page; no keyword stuffing.
- **One PM, multiple categories [V2·BUILD]** — same `Person` entity in schema (one canonical identity); the rendered expertise sentence + contact CTA are category-specific per page.
- **Person schema: [V2·BUILD]** `name` · `jobTitle` · `worksFor` (HelloPrint / `{{shop_name}}`) · `knowsAbout` (page's category noun) · `sameAs` (LinkedIn URL) · `image`. Emitted only when the byline is enabled on the page. See [[g-schema]].
- **Mobile: [V2·BUILD]** compact byline; LinkedIn touch target ≥44px.

## Decisions (locked)

- **§4 (Person)** — NEW combined content type, all surfaces (PDP B-PM / PLP·FLP B15; V2 test). Identity fields on `person`: `name · jobTitle · image · linkedIn` (`sameAs`, `rel="me"`) `· knowsAbout`. The category-specific expertise sentence + CTA live on the per-page byline block, not on `person` (one canonical identity; sentence varies per page). Emits `Person` schema.
- **§2 (Schema)** — `Person` sub-schema rendered only when the PM block is enabled; `knowsAbout` = category noun; must map to a visible byline (spam guardrail).
- **§15** — no per-shop field; locale-level visibility via empty localized content / config on/off.

## Open points

- Test scope, **cohort/control selection [V2·BUILD]**, and the 8-week decision window are operational, not content-model blockers.
- Whether `knowsAbout` references taxonomy nodes ([[pageHomeModular]] category entries) or a free string list is to be confirmed at build (requirements describe it as "category noun").
- **Label note [inferred]:** the brief lists "Person schema + rel=me [V1·BUILD]" on the *type* axis (it is a real BUILD component, not a guideline), but the **phase** of the whole `Person`/byline block is **V2** on every surface (cohort-vs-control test). This page therefore tags the schema build as **V2·BUILD** — the only reading consistent with PDP Req B-PM "V2 test", PLP Req §B15 "fully V2", and FLP Req §15 "V2". Flagged so it isn't mistaken for a V1-shipping component.

## Sources

- PDP Req v0.34 (B-PM Product Manager test; new `Person` content type — name, role/jobTitle, photo, LinkedIn, product expertise; Person schema + rel="me").
- PLP Req v1.13 §B15 (Productmanager authority test; one PM multiple categories; Person schema fields; /cs/team/ hub).
- FLP Req v0.15 §15 (Productmanager byline; inherits PLP §B15; one canonical Person, category-specific sentence + CTA per page).

Related: [[g-schema]] · [[pageHomeModular]] · [[surface-PDP]] · [[surface-PLP]] · [[surface-FLP]]


---


*(id: g-pagecard · type: content-type · surfaces: [PLP, FLP] · status: draft)*


# g-pagecard — shared page card (BH + BI)

**Labels:** V1·BUILD ×5 · V1·GUIDELINE ×3 · V2 ×1 · KEEP ×3 (`Name`/`Link`/`Title` maintained = KEEP-as-BUILD). Source: PLP-Catalog v1.5 (BH/BI/g-pagecard mostly V1, "maintain"; Algolia auto-selection of `subitems[]` = V2) + PLP-Req v1-13 §Block 1.

The single, shared **page-card** component that links a card to a **page** (a PLP/FLP or related category) — used by [[in-page-nav-AH]]-adjacent navigation blocks **Block BH** (promotional, high on the page) and **Block BI** (subcategory / related index, low on the page), and reused inside [[brands-blockC]] when its right-side media mode is `page-cards`. A page card is *navigation*, never a product tile — it carries no price, no badge, no CTA, no schema.

## How it works in Contentful

`g-pagecard` is not a top-level body block; it is the repeated card entity referenced by the `subitems[]` (BH/BI) and `media=page-cards` (Block C) fields. One card = one link to a canonical page URL. The author supplies a `Link` (the destination) and optionally a `Title` (the visible anchor text); the **image is always the linked entity's catalog image** (sourced, never authored on the card). Both BH and BI render the *same* card markup — the current horizontal design (name + arrow on the left, fixed image well on the right). Only the surrounding visualisation differs: BH renders larger cards beside a required promo card; BI renders a compact grid. Rendered SSR as a real crawlable `<a>`.

## Field model

| Field | Type | Localized? | Notes | phase/type |
|---|---|---|---|---|
| `Name` | Short text | No | Page-card admin / entry label. **Maintain.** | V1·KEEP |
| `Link` | Reference / URL | No | The canonical URL the card points to — a real crawlable `<a>`. **Maintain.** | V1·BUILD (crawlable-anchor) |
| `Title` (optional) | Short text | Yes | Card label / anchor text = the page or category name; renders as **link text, not an H3**. 2-line max, ~38-char cap. **Maintain (optional).** | V1·KEEP · char-cap V1·GUIDELINE |
| `Image` | — | — | **Removed** — always sourced from the linked entity's catalog image; not authored on the card. | V1·BUILD |
| `Highlight labels` | — | — | **Removed.** | V1·BUILD |
| `Should show per shop` | — | — | **Removed** — per-shop visibility moves to language/locale level (§3.15). | V1·BUILD |

## Per-surface usage & deltas

- **PLP** — used by **Block BH** (promo card + featured page cards, high) and **Block BI** (subcategory & related-category index, low). Also reusable inside **Block C** brand spotlight when `media=page-cards`. [V1·BUILD] BI renders **all** `subitems[]` (cap removed) in V1; **Algolia auto-selection of which page cards to surface = [V2]** (V1 = author-selected/hand-authored).
- **FLP** — same component is available; FLP internal linking is primarily carried by the crawlable text-link list [[product-list-Z]] and the filter panel anchors fed by [[filter-engine-AZ]], so g-pagecard sees lighter use here. [V1·BUILD]
- **PDP** — not used (PDPs are leaves and do not carry page-card navigation). [V1·BUILD]
- **BH vs BI split:** BH = promotional + featured (high prominence). BI = exhaustive subcategory / related index (low prominence). Identical card, different surrounding visualisation. [V1·BUILD]

## Requirements behaviour

- **Crawlable link.** Each card is a real crawlable `<a>` to the canonical URL; anchor text = page / category name (the `Title`, rendered as link text, **not** an H3). SSR'd. [V1·BUILD] (crawlable-anchor) · 2-line max + ~38-char cap = [V1·GUIDELINE].
- **Image.** Always the linked entity's catalog image — object-fit contain on a soft-neutral well, AVIF/WebP + srcset, lazy; `alt` = page / product name. Never authored on the card. [V1·BUILD]
- **No schema.** g-pagecard emits **no `Product` / `ItemList` schema** and must **never** append to the page-level `ItemList`. It is navigation, not a product offer. See [[g-schema]]. [V1·BUILD]
- **Feeds the scorer.** Page-card links feed the internal-link graph and the cannibalisation / content scorer ([[g-keywords-scoring]]) like any other internal link. [V1·GUIDELINE] (scorer-feed)
- **Decoupled from B12.** g-pagecard navigation is **not** related products. B12 (related *products*) = [[productCollection]] / Block D, auto-priority; BI page cards are hand-authored. Different content jobs — **no shared schema, no shared de-dup graph** (per PLP-Catalog §B12/BI decoupling). [V1·BUILD]
- **Empty state.** A card with no resolvable `Link` is skipped; a host block whose card set is empty in a locale does not render there (skip + reflow). For BH, `subitems` is required in ≥1 locale (any), with no fallback. [V1·BUILD]
- **Internal-link de-dup.** Avoiding duplicate links to the same destination is a **commercial guideline (SHOULD)**, not build-enforced (PLP-Catalog softens the old hard "first-occurrence-wins" MUST). [V1·GUIDELINE]

## Decisions (locked)

- **§3.15** — `Should show per shop` dropped; visibility is language/locale level (hide via empty localized content → empty-state omit).
- **§3.2 / g-schema** — no `Product`/`ItemList` schema from page cards; never append to the page `ItemList`.
- **Card trims to `Name · Link · optional Title`** (image always catalog-sourced; highlight labels + per-shop removed). per-shop dropped.

## Open points

- **Binding (PLP-Catalog).** Final field / Linear binding for `homeBlockTypeBI` vs Block D to be confirmed in the Batch 2.x code review. Exact CF field IDs for the shared card to confirm in Batch 2.x.

## Sources

- PLP-Block-Variations-Catalog v1.5 — §Content-type logic — Block BH; §Block BI (page-card navigation, "Shared page card — g-pagecard"); §Block C (image requirements, `media=page-cards`).
- PLP-Req v1-13 — §Block 1 (L1/L2/L3 crawl rules, page-card crawl parity); §Block 12 (B12/BI decoupling).
- _BUILD-BRIEF §3.15 (per-shop → locale), §3.2 (schema).

Related: [[surface-PLP]] · [[surface-FLP]] · [[productCollection]] · [[brands-blockC]] · [[in-page-nav-AH]] · [[g-schema]] · [[g-keywords-scoring]] · [[card-label]]


---


*(id: homeBlockTypeBB · type: content-type · surfaces: [PDP, PLP, FLP] · status: draft)*


# USP Block (Block BB) — page-specific on-page USPs

**Labels:** all V1 (PLP-Catalog "Maintain — optimised"; no V2 in this block). V1·BUILD ×6 (icon set, fields, placement, removals, SSR, no-schema) · V1·GUIDELINE ×4 (counts, content/AEO voice, item links, internal-link de-dup SHOULD) · KEEP ×2 (`Title`/`Subtitle` maintained). Source: PLP-Catalog v1.5 §USP Block (BB).

Block BB (`homeBlockTypeBB`), re-used as the **page-specific on-page USP block** — "why [this category] with us". An optional block heading + optional intro + a grid of USP items (icon + title + description + a single optional link). It **absorbs the killed Block G** USP list (§3.21) and matches the MOO / Ocean Bottle patterns.

**Three distinct USP surfaces — keep them apart:** (1) [[g-uspbar]] = the global brand USP bar above the H1 (sitewide, exactly 4 brand USPs); (2) the Contentful **USP library** = the meta-title USP slot (SERP, see [[g-meta]]); (3) **this block** = page-specific on-page USPs. BB must **not** duplicate `g-uspbar`.

## How it works in Contentful

A `homeBlockTypeBB` entry in the page's `Content Blocks`. The author writes an optional `Title` (block heading) + optional `Subtitle` (intro), then a list of `Items[]`. Each item carries an `Icon` (from a pre-defined semantic icon set, with optional upload override), an item `Title` (styled text, **not** a heading), a `Description`, and a single optional `Link`. Author sets the column count; the row is always full-width with items flexing to fill (same logic as the Block 5 grid / bundle items). Renders SSR, below the product grid.

## Field model

**Block-level**

| Field | Type | Localized? | Notes | phase/type |
|---|---|---|---|---|
| `Title` | Short text | Yes | Block heading — **optional**. Title Format H2 / H3 / Span (default **H2**). When present, the block owns one heading. | V1·KEEP · heading hygiene V1·BUILD |
| `Subtitle` | Short text | Yes | Short block intro under the title — optional. | V1·KEEP |
| block `CTA` | — | — | **Removed** — USP items + the page's own CTAs suffice; no block-level CTA. | V1·BUILD |
| `Should show per shop` | — | — | **Removed** — language/locale level (§3.15). | V1·BUILD |

**Per-item (`Items[]`) — min 3 / max 5**

| Field | Type | Localized? | Notes | phase/type |
|---|---|---|---|---|
| `Icon` | Reference / asset | No | From a **pre-defined semantic icon set** (e.g. Design→brush, Cheap→euro, Fast delivery→truck, Sustainable→leaf), with **optional upload override**; empty → standard "USP" fallback. Decorative → `alt=""`. | V1·BUILD (icon set) |
| `Title` (item) | Short text | Yes | The USP label — **styled text, not a heading** (changed from H3). | V1·BUILD |
| `Description` | Short text | Yes | The USP detail — concise; first sentence extractable (AEO). **No inline links.** | V1·GUIDELINE (AEO voice) · no-inline-links V1·BUILD |
| `Link` (item) | Reference / URL | No | A **single dedicated optional Link** — "learn more" to a relevant info / guarantee / category page; crawlable `<a>`, descriptive anchor. **Not** a product-card surface (products live in B5 / B12). | V1·BUILD (crawlable-anchor) · target choice V1·GUIDELINE |

## Per-surface usage & deltas

- **PLP** — page-specific USP block; **always below the product grid (B5)**, author-positioned among the below-grid editorial blocks. [V1·BUILD]
- **FLP** — same shared block; below the grid. [V1·BUILD]
- **PDP** — shared content type, same model; the on-page page-specific USP block (distinct from the PDP's `g-uspbar` 4 brand USPs). [V1·BUILD]
- No per-surface field difference; placement is uniformly below-grid because the per-item links would otherwise breach the §B4 "no links above the grid" rule on PLP/FLP.

## Requirements behaviour

- **Placement.** Always below the product grid (never above — B4 no-links-above-grid rule). Author-positioned within the below-grid zone; skip on focused sub-PLPs unless useful. [V1·BUILD] (below-grid enforcement) · author judgement [V1·GUIDELINE]
- **Counts.** **Min 3 / max 5 items.** Columns author-set; full-width row, items flex to fill; 1-up on mobile. Empty → no render. [V1·GUIDELINE] (count discipline) · empty-state omit [V1·BUILD]
- **Icons.** Pre-defined named semantic icon set; optional custom upload override; empty → standard "USP" fallback. Icons are decorative → empty `alt` (fixes the empty-alt issue flagged for `homeBlockType*`). [V1·BUILD]
- **Heading hygiene.** When present, the block owns one heading (Title Format H2/H3/Span, default H2). Item titles are styled text, **not** H3. [V1·BUILD]
- **Content / AEO.** Page-specific benefits, concise, first sentence extractable; voice / banned-words apply ([[g-keywords-scoring]]); no marketing fluff. [V1·GUIDELINE]
- **Links.** Only the per-item `Link` field carries links (non-product targets); none inline in the description. Internal-link de-dup is a **commercial guideline (SHOULD)**, not build-enforced. [V1·BUILD] (single-link-field) · de-dup [V1·GUIDELINE]
- **No schema.** BB emits no schema (see [[g-schema]]). [V1·BUILD]
- **SSR.** All items server-rendered. [V1·BUILD]

## Decisions (locked)

- **§3.21** — BB **absorbs Block G** (USP list, killed on all surfaces → routed here).
- **§3.11** — distinct from [[g-uspbar]] (exactly 4 brand USPs, sitewide). BB is page-specific and must not duplicate it.
- **§3.15** — `Should show per shop` dropped; locale-level visibility.
- **§3.2** — no schema.

## Open points

- Exact Contentful field IDs to confirm in Batch 2.x.

## Sources

- PLP-Block-Variations-Catalog v1.5 — §Content-type logic — USP Block (Block BB): three-USP-surface separation, block + per-item field model, pre-defined icon set, placement & counts, internal-link de-dup SHOULD.
- _BUILD-BRIEF §3.21 (Block G killed → BB), §3.11 (USP bar = 4 brand USPs), §3.15, §3.2.

Related: [[g-uspbar]] · [[g-meta]] · [[surface-PLP]] · [[surface-FLP]] · [[surface-PDP]] · [[g-schema]] · [[g-keywords-scoring]]


---


*(id: homeBlockTypeC · type: content-type · surfaces: [PDP, PLP, FLP] · status: draft)*


# Block C — Brands block (b17)

**Labels:** all V1 (PLP-Catalog "Maintain — optimised · b17 locked"; three display modes all V1; no V2 in this block). V1·BUILD ×8 (display modes, spotlight media, new fields, image contracts, linking, schema, SSR, removals) · V1·GUIDELINE ×3 (counts, description char cap, de-dup exempt) · KEEP ×5 (`title`/`name`/`brands[]`/`colorTheme`/`titlePosition`). Source: PLP-Catalog v1.5 §Block C (Brands · b17); BC-1/BC-2/BC-3 locked 2026-06-04.

Block C (`homeBlockTypeC`), re-scoped from a "trusted by" logo strip to a **multi-mode Brands block** over a single `brands[]` list. Three display modes (all V1) render the same list at different prominence. Reuses existing components — [[g-pagecard]], the Block 5 / [[productCollection]] (Block D) bundle-item tile, and the BG carousel — with no bespoke orientation. Per-brand Destination. Renders on **any** Page (Home Modular) and the PDP. **Block 17** (`b17`) — locked.

## How it works in Contentful

A `homeBlockTypeC` entry in `Content Blocks`. One `brands[]` list + a `displayMode` switch selects the template; the same brand items render in all three modes. The author sets block-level visual options (`brandIdentity`, `media`, `showPrices`, `showDescriptions`, `carousel`, `colorTheme`, `titlePosition`) and a per-brand `Destination`. Multiple Brands blocks per page are allowed. All items SSR'd; below the product grid.

**Display modes** (one switch, three templates over the same `brands[]`):

| Mode | What it is | Prominence | phase/type |
|---|---|---|---|
| **Logo strip** | Many small greyscale logos in a row (carousel-aware). Subtle social proof. Link optional per brand. | Lowest | V1·BUILD |
| **Logo directory** | Full-colour logo tiles (no product image), each a real link to the brand's page. Navigable brand index. | Medium | V1·BUILD |
| **Brand spotlight** | Few brands, each a rich card (left meta + right media). Merchandising / routes into the assortment. Uniform cards (no featured-wide). | Highest | V1·BUILD (spotlight media) |

**Brand spotlight structure** — **Left (meta):** brand identity (`brandIdentity` = Logo | Name, block-level; falls back to Name when no logo) + optional description + CTA. Brand name is styled text, **not a heading**. Description optional, hidden when empty, **max 120 chars**. CTA shown only when the brand's Destination is set; fixed line "Shop the range" (locale-translated). **Right (media) — one type per block, no mixing** (`media` = in-setting | page-cards | bundle-items): in-setting image · Page Cards (2–4, reuse [[g-pagecard]]) · Bundle Items (2–4, reuse the Block 5 / Block D tile).

## Field model

| Field | Type | Localized? | Notes | phase/type |
|---|---|---|---|---|
| `title` | Short text | No | Internal name. **Keep.** | V1·KEEP |
| `name` | Short text | Yes | Localised block heading. **Keep.** | V1·KEEP |
| `brands[]` | References | — | Brand items (logo · name · description · Destination · right-side content). **Keep.** | V1·KEEP |
| `colorTheme` | Enum | No | Theme (neutral / greyscale for the strip). **Keep.** | V1·KEEP |
| `titlePosition` | Enum | No | Existing. **Keep.** | V1·KEEP |
| `displayMode` | Enum | No | `logo-strip` · `logo-directory` · `brand-spotlight`. **New.** | V1·BUILD |
| `brandIdentity` | Enum | No | `Logo` · `Name` (block-level; fallback to Name when no logo). **New.** | V1·BUILD |
| `media` | Enum | No | `in-setting` · `page-cards` · `bundle-items` (spotlight; **one type, no mixing**). **New.** | V1·BUILD (spotlight media) |
| `showPrices` | Bool | No | **Default OFF.** Bundle Items only — reveals the from-price (same reference quantity as Block 5, pricing-consistency contract). *Inverse of Block D.* **New.** | V1·BUILD |
| `showDescriptions` | Bool | No | **Default OFF.** Bundle Items only — reveals the bundle-item description (product feed). **New.** | V1·BUILD |
| `carousel` | Bool | No | Reuse BG / Block D mechanics (≥4 → carousel w/ arrows+dots, no autoplay, keyboard+ARIA; 3 → static row; mobile ≤760px vertical stack; `prefers-reduced-motion` gated). **New.** | V1·BUILD |
| per-brand `Destination` | Reference / URL | No | Product / Page (Home Modular) / external URL / **none** (display-only). **New.** | V1·BUILD |
| per-brand `description` | Short text | Yes | Optional, ≤120 chars, hidden when empty (spotlight). **New / confirm.** | V1·BUILD · ≤120-char V1·GUIDELINE |
| `Should show per shop` | — | — | **Removed** — language/locale level (§3.15). | V1·BUILD |

The standalone "image yes/no" toggle is subsumed by `displayMode` + `media`. Logos are localisable assets (default single asset unless a locale override is set).

## Per-surface usage & deltas

- **PLP / FLP** — Brands block on any Page (Home Modular); author-positioned **below the product grid** (b17). Multiple blocks per page allowed. [V1·BUILD]
- **PDP** — shared content type, same model (the PDP equivalent of the brands showcase). [V1·BUILD]
- No per-surface field difference. De-dup is **exempt** on all surfaces (distinct showcase). [V1·GUIDELINE]

## Requirements behaviour

- **Image contracts (four contexts).** Brand logo: SVG preferred (PNG fallback), object-fit contain, `alt` = brand name; greyscale in logo-strip, full-colour in directory + spotlight; transparent bg. Page-card image (`media=page-cards`): reuse [[g-pagecard]] — catalog image, alt = page/product name. Bundle-item image (`media=bundle-items`): reuse Block 5 / Block D — chain catalogImage → images[0] → bundleItem.photo, two-state (catalog + hover), mobile hover off, alt = product name. In-setting image (`media=in-setting`): one ~4:3 image (~1600px max), AVIF/WebP + srcset, lazy (eager only if page LCP), alt describes the scene. [V1·BUILD]
- **Linking & Destination.** Per-brand Destination = Product / Page (Home Modular) / external URL / **none** (display-only). Logo-directory tiles link to the brand's Page; no Destination → display-only. Linked logos/tiles/cards are real `<a>`; logo = `<img>` with alt = brand name. External URLs: `rel="nofollow"`, new tab. In the spotlight the brand logo and each right-side card link **independently**. Links feed the internal-link graph + cannibalisation scorer ([[g-keywords-scoring]]) like BI. [V1·BUILD] (render) · scorer-feed [V1·GUIDELINE]
- **Schema.** `Brand { name, logo, url }` **only for brands we sell** (directory + spotlight with a brand-page Destination); **directory mode** wraps them in an `ItemList` of `Brand` items. Partner / non-selling logos: **no commercial schema** — decorative `<img>` + `alt` only (optional `Organization` `sameAs` only for a documented partnership; **default none**). **Never** emit `Product` / `Offer`; **never** append to the page-level `ItemList`. A trust-strip logo must not imply we sell that organisation's products. See [[g-schema]]. [V1·BUILD]
- **Counts.** Logo strip ≥4 · Logo directory ≥6 (no hard max) · Brand spotlight 1–6. All items SSR'd. [V1·GUIDELINE] (count discipline) · SSR [V1·BUILD]
- **De-dup: exempt.** Brands-block items are not subject to page-level de-dup (distinct showcase; may also appear elsewhere) — consistent with de-dup being a soft guideline. [V1·GUIDELINE]
- **Empty state.** A brand with no logo+name, or a spotlight below its media minimum, is skipped; nothing renders → block omitted. [V1·BUILD]
- **Placement.** Author-positioned, **below the product grid (B5)** — brand logos / cards are links, so the §B4 no-links-above-the-grid rule applies; free placement within the below-grid zone. [V1·BUILD] (below-grid enforcement) · author judgement [V1·GUIDELINE]

## Decisions (locked)

- **§3.2 / [[g-schema]]** — no `CollectionPage`; `Brand`/`ItemList` only for sold brands; partner logos decorative; never `Product`/`Offer`; never append to page `ItemList`. Spam guardrail (schema maps to visible DOM).
- **§3.15** — `Should show per shop` dropped; locale-level visibility.
- **BC-1 (locked 2026-06-04)** — partner `Organization` schema **default none**; per-brand `Organization` `sameAs` only for a documented partnership.
- **BC-2 (locked)** — block number **b17**.
- **BC-3 (locked)** — on-page slot author-positioned, **below the product grid**.

## Open points

- Exact Contentful field IDs / final binding to confirm in Batch 2.x (per-brand `description` flagged "Add / confirm").

## Sources

- PLP-Block-Variations-Catalog v1.5 — §Content-type logic — Block C (Brands block · b17): display modes, spotlight structure, visual options, field model, four image contexts, linking & Destination, schema, counts & governance, BC-1/BC-2/BC-3 locked.
- _BUILD-BRIEF §3.2 (schema), §3.15 (per-shop → locale).

Related: [[g-pagecard]] · [[productCollection]] · [[bundleItem]] · [[surface-PLP]] · [[surface-FLP]] · [[surface-PDP]] · [[g-schema]] · [[g-keywords-scoring]]


---


*(id: homeBlockTypeAH · type: content-type · surfaces: [PDP, PLP, FLP] · status: draft)*


# Block AH — in-page section nav

**Labels:** all V1 (PLP-Catalog "Maintain — re-scoped"; PLP-Req §Block 1; no V2 in this block). V1·BUILD ×6 (jump-nav anchors, sticky/desktop-only, SSR, no-dead-anchors, no-schema, conditional-target, removals) · V1·GUIDELINE ×2 (hard cap 8, order-mirrors-sections) · KEEP ×2 (`Name`/`Anchor Items` maintained). Note: the bucket catalogue nav split out to **`g-catnav`** is out of scope here. Source: PLP-Catalog v1.5 §Block AH; PLP-Req v1-13 §Block 1.

Block AH (`homeBlockTypeAH`) = **Block 1, a standalone in-page section nav** — anchor jumps **only**. It is **not** merged with the catalogue category nav (the six grouped buckets), which is a separate static element specced as `g-catnav`. AH is sticky, sits below the intro and above the product grid, and is **desktop-only** (markup + section `id`s are kept on mobile for crawl parity).

This block splits the old "Block 1 = bar + jumps" (PLP-Req §Block 1) into two: the **jumps = AH** (this block), the **buckets = `g-catnav`** (static catalogue nav, with the L1/L2/L3 crawl rules).

## How it works in Contentful

A `homeBlockTypeAH` entry in `Content Blocks`. It trims to two fields: `Name` (admin label) + `Anchor Items` (the hand-authored jump list). Each anchor item carries a label + the target on-page section it links to, rendered as an in-page `<a href="#id">`. The jump list stays **hand-authored** — auto-derivation is rejected because it would force a "short name" on every block. Sticky on scroll; SSR'd.

## Field model

| Field | Type | Localized? | Notes | phase/type |
|---|---|---|---|---|
| `Name` | Short text | No | Admin / entry label. **Maintain.** | V1·KEEP |
| `Anchor Items` | List | Yes | The hand-authored jump list — each item = a label + the target section it links to (in-page `<a href="#id">`). **Maintain.** | V1·KEEP · jump-nav anchors V1·BUILD |
| `CTA button text` | — | — | **Removed.** | V1·BUILD |
| `Visual options` | — | — | **Removed.** | V1·BUILD |
| `Should show per shop` | — | — | **Removed** — language/locale level (§3.15). | V1·BUILD |

Trims to **Name + Anchor Items**; no new field.

## Per-surface usage & deltas

- **PLP / FLP** — sticky in-page section nav, below intro / above grid, desktop-only. On the FLP, the F1 panel's own "Filter products by:" H2 and the B2b taxonomy tree are separate UI; AH lists the page's content sections (not the facet panel). [V1·BUILD]
- **PDP** — shared content type; same in-page jump nav for PDP sections. [V1·BUILD]
- **Catalogue category nav is NOT this block.** The six grouped buckets (+ All Products / Merch / Quotations) = global nav, specced as **`g-catnav`** — **static** (not sticky), carrying the L1/L2/L3 crawl rules from PLP-Req §Block 1. [V1·BUILD] (split out of scope here)

## Requirements behaviour

- **Guardrails (build / preview).** No dead anchors · in-page-only `<a href="#id">` · **hard cap 8 items** · order **mirrors the on-page section order** · **reviews excluded**. Eligible targets: product blocks, video, B9 content, FAQ, blog. [V1·BUILD] (no-dead-anchors, reviews-excluded) · cap-8 + order-mirrors-sections [V1·GUIDELINE]
- **Anchor jumps are real `<a href="#…">`** (not JS-only handlers) — crawlable, giving Google a page outline. [V1·BUILD] (jump-nav)
- **Sticky + desktop-only.** Sticky on scroll; rendered desktop-only, but the markup and section `id`s are retained on mobile so the crawl parity / outline is identical across viewports. [V1·BUILD]
- **Server-rendered.** Bar + anchor list present in raw HTML before JS executes. [V1·BUILD]
- **No schema.** AH emits no schema; the visible anchors carry the crawl signal (see [[g-schema]]). [V1·BUILD]
- **Conditional targets follow the slot.** Where a section's slot is conditional (e.g. BG vs Block 5), AH lists whichever slot renders — the anchor-nav surface follows the slot conditional automatically. [V1·BUILD]

## Decisions (locked)

- **§3.15** — `Should show per shop` dropped; locale-level visibility (AH, BG, BH, USP Block, B9/Block S and Promo Card all dropped per-shop; HEL-331).
- **§3.2** — no schema; visible anchors carry the signal.
- **Catalogue nav split** — buckets → static `g-catnav` (not this block); jumps → AH. per-shop dropped.

## Open points

- `g-catnav` (the static catalogue category nav) is a separate element, not part of this content type; its full L1/L2/L3 spec lives with the surface / Block 1 documentation. (Not in scope for this page.)

## Sources

- PLP-Block-Variations-Catalog v1.5 — §Content-type logic — Block AH (in-page section nav): two-field trim, guardrails (hard cap 8, reviews excluded, order mirrors sections), catalogue-nav-is-g-catnav note, per-shop → locale (HEL-331).
- PLP-Req v1-13 — §Block 1 (sticky anchor nav: anchor jumps real `<a href="#…">`, server-rendered, same DOM on mobile/desktop; the bucket nav that becomes g-catnav).
- _BUILD-BRIEF §3.15, §3.2.

Related: [[surface-PLP]] · [[surface-FLP]] · [[surface-PDP]] · [[g-schema]] · [[faq-blockV]] · [[video]] · [[blog-teaser-AJ]]


---


*(id: homeBlockTypeAZ · type: content-type · surfaces: [FLP] · status: defined)*


# Block AZ — Filter engine (`filterConfig` on `pageHomeModular`)

> **Labels:** TWO layers. **(a) The AZ filter-config model** is now **DEFINED** (the parked gate is resolved — see below) and **build-ready in shape**, but the build is **gated on the Merchant-Catalogue API contract** (open ticket — the new product-catalogue system). Config fields = **`[V1·BUILD]` (build-gated)**. **(b) The render-only F1–F4 contract** is **`[V1·BUILD]` ×10+** (five-state panel, controls strip, pagination v2, empty state, SSR, earned-anchor resolver, mobile drawer) · **`[V1·GUIDELINE]`** (which combinations earn a destination, `attributesInDescription` max-2 curation, slug readability) · **`[V1·KEEP]`** (earn criteria + KW governance inherit PLP). **Algolia is out of scope** (platform-catalogue proposal). **Migration is out of scope** (content-generation engine).

> **STATUS — gate resolved.** The old `[PARKED]` state (pending the "PCM/Algolia" decision) is **lifted**. The decision: the **Merchant Catalogue is the single source of truth** for products, taxonomy and attributes; **Contentful owns the page**. Algolia no longer lives in Contentful-side logic. The config model below is final; only the catalogue API contract that feeds it remains an open build ticket.

Block AZ is the **FLP filter engine** — configuration, not a rendered block. It is a **field/block placed on a [[pageHomeModular]]** (it does **not** introduce a new page type — page URL, meta, titles and editorial copy stay on `pageHomeModular`). It defines which catalogue products surface on a Filter Listing Page × filter state and which facets show. The render surfaces F1 (filter panel), F2 (controls strip), B5 (grid), F3 (pagination) and F4 (empty state) all **consume** AZ; none of them is a Contentful block.

## Core principle — store keys, resolve labels live

Block AZ stores only **stable catalogue keys** (category keys, `attribute:value` keys) plus the indexation map. It **never stores a human-readable label** ("Stainless Steel"), a swatch, a count, or a product record — every label, available value, product and count is fetched **live from the Merchant Catalogue** at build/render time.

This is what makes renames safe: rename "Stainless Steel" → "Stainless steel (304)" in the catalogue and the stored key `material:stainless-steel` is untouched — only the displayed label changes, everywhere, automatically. A filter rename can never break a page, because the page never stored the name.

Two consequences that shape the whole model: **(1)** the config is **not localized** — keys are identical across countries; labels resolve per locale from the catalogue. Different filter setups per country = a **separate Block AZ**, never a localized field. **(2)** the facet-value sub-type from the old model (label · swatch · slugFragment · sortOrder authored in Contentful) **dissolves** — those come from the catalogue; only `order` survives, in `shownFilters`.

## How it works in Contentful

A Block AZ entry carries two things: an `internalName` (editor identifier) and a single **`filterConfig` JSON field** holding the whole filter definition, rendered by a **custom Contentful App** (cascading dropdowns sourced live from the catalogue — see "Editor app"). One JSON object rather than separate fields, because the app needs cross-awareness: the chosen categories determine which attributes are even available to pre-filter, show, tag, or index.

The block is **page-bound and 1:1 with its host `pageHomeModular`** — it produces URLs and indexation only through that page (the page owns the routable slug). An AZ entry not placed on a page is an **inert draft** (no base URL, no indexation); an AZ referenced by more than one page is flagged (its indexation would fork). See "Indexation safety net".

## Field model — Block AZ (`homeBlockTypeAZ`)

| field | type | localized? | notes | phase/type |
|---|---|---|---|---|
| `internalName` | Symbol | No | Editor-facing identifier (e.g. "Water bottles — NL filters"). **Not a URL** — the host `pageHomeModular` owns the routable slug. `sys.id` is the machine key for references. | V1·BUILD |
| `filterConfig` | JSON (custom-app appearance) | No | The whole filter definition; **catalogue keys only**, labels/counts/products resolve live. Sub-structure below. | V1·BUILD (build-gated on catalogue API) |

`filterConfig` sub-structure:

| key | shape | notes | phase/type |
|---|---|---|---|
| `categories` | `[string]` | Catalogue category keys (live dropdown). **Multiple categories = OR** (footballs OR shirts). | V1·BUILD |
| `preFilters` | `[{attribute, values[]}]` | Locked, server-applied, **not removable by the visitor**. **Across entries = AND** (blue AND plastic); **values within one entry = OR** (white OR blue). | V1·BUILD |
| `shownFilters` | `[{attribute, order}]` | The interactive facets exposed to the visitor; show/hide + display order. A pre-filtered attribute is usually dropped here (editor choice). | V1·BUILD |
| `attributesInDescription` | `[attribute]` · **max 2, author-ordered** | The B5 product-card metadata. **Catalogue-selected keys** (no free text), cascades from the chosen categories. If a product lacks the attribute, the line is hidden. | V1·BUILD (slot) · max-2 + curation V1·GUIDELINE |
| `printrunPreselected` | quantity (catalogue-validated) | Default print-run/quantity context. **Validated against Merchant-Catalogue availability** — unavailable quantities can't be chosen. | V1·BUILD |
| `indexableFilters` | `[{ filters:[{attribute,value}], destination }]` · `destination` = ref → `pageHomeModular` (**required**) | The combination → unique-content destination map. See "Indexation model". A combination is indexable **only** when it has a destination; no destination = query parameter (noindex). Hand-curated allowlist; combinations are never auto-generated. | V1·BUILD (engine) · which combos earn = V1·GUIDELINE |

**Removed / migrated from the old model:** `taxonomy` → `categories`; `advancedPreFilters` → `preFilters`; `facetsToDisplay` → `shownFilters`; `filterSettings[]` facet-value sub-type → **dissolved** (labels/swatches/values resolve live from the catalogue; only `order` survives); `algoliaIndex` → **removed** (Algolia out of scope); `slug` → **removed** (the host `pageHomeModular` owns the URL); `Should show per shop` → **removed** (locale-level, §3.15). **Create-new:** `internalName`, `indexableFilters`, the `filterConfig` JSON field + its custom app.

## preFilters vs shownFilters

| | `preFilters` | `shownFilters` |
|---|---|---|
| What it does | Locks the page to a fixed selection | Exposes interactive facets to the visitor |
| Visitor can change it? | **No** — always applied | **Yes** — visitor toggles values |
| Example | "Stainless Steel Water Bottles" locked to `material:stainless-steel` | capacity, colour, brand, delivery-date to refine on |
| Defined where | Contentful (editor) | Contentful (editor) |

A pre-filtered attribute is usually dropped from `shownFilters` (you don't show a colour facet on a page locked to orange). Editor choice, not a rule — if left in, the frontend renders it as a fixed/locked chip, not an open facet.

## Example pages, mapped

| Page | `categories` | `preFilters` | `shownFilters` (example) |
|---|---|---|---|
| Water Bottles | `[water-bottles]` | — | capacity, colour, material, brand, delivery-date |
| Stainless Steel Water Bottles | `[water-bottles]` | `material=[stainless-steel]` | capacity, colour, brand, delivery-date |
| Blue Plastic Water Bottles | `[water-bottles]` | `colour=[blue]`, `material=[plastic]` | capacity, brand, delivery-date |
| Worldcup | `[footballs, shirts]` | — | colour, brand, delivery-date |
| Worldcup NL | `[footballs, shirts]` | `colour=[orange]` | brand, delivery-date, size |
| Worldcup UK | `[footballs, shirts]` | `colour=[white, blue]` | brand, delivery-date, size |

Cross-category pre-filtering (Worldcup pages filter footballs **and** shirts on one colour) works because **colour is a global attribute** the catalogue applies per category (§8.1 resolved — global attribute).

## Indexation model — destination-only

**One rule:** a filter variant is indexable **only if it is a dedicated `pageHomeModular` with its own unique content** (unique H1, intro, title/meta, and a genuinely different product set). Everything else is a **query parameter, and query parameters are always non-indexable.** There is no thin/generated variant tier.

So two states only:

- **Unique-content destination** → `index,follow`, clean path URL, self-canonical, in the sitemap, and the **only** thing that gets a crawlable `<a>`. It is its own `pageHomeModular` (with its own AZ pre-filtering the combination) and carries its own per-locale meta-robots.
- **Query parameter** → everything else → always `noindex`, excluded from the sitemap, never exposed as a crawlable `<a>`. Sort / pagination / view-mode are always query parameters.

**`crawlable link ⟺ indexable destination ⟺ unique content`** — one and the same set, defined explicitly in `indexableFilters`. An entry maps a filter combination to a destination `pageHomeModular` (destination **required**); F1 renders a crawlable `<a>` only for combinations that have one, and every other facet value is a query-param control. Combinations are **hand-curated** (no auto-generation of attribute combinations → no index bloat).

**Which combinations earn a destination** (gate — inherits g-url's earn criteria): (1) cluster keyword ≥ 100 monthly searches in the target market, (2) ≥ 5 products surface, (3) demand is stable (not a one-off spike), (4) the page carries genuinely unique content vs the parent. Condition 4 is non-negotiable — no destination without unique content.

**Per locale, by construction.** Because each destination is a real `pageHomeModular` with its own meta-robots field, indexation is decided **per locale** by the existing INDEX-1 rule-engine ([[g-url]]) — a combination can index in NL (demand) and stay `noindex` in a small market (no demand). The allowlist makes a combination *eligible*; the per-locale engine decides if it actually indexes. No "index everywhere" force.

### Commercial guidelines — destination URLs

- **Flat, hyphenated, no folder paths.** `/blue-water-bottles`, never `/water-bottles/blue` (path-segment-after-slash is forbidden, [[g-url]]). Locale-prefixed, ≤ 75 chars.
- **Editorially curated.** A destination is a real PLP, so its slug is hand-authored, not machine-composed.
- **Readability rule (commercial guideline).** The slug mirrors the **primary keyword / H1 phrase in that locale's natural word order** — which means attribute-before-noun in EN/NL/DE and attribute-after-noun in FR/ES/IT/PT:
  - EN `/stainless-steel-water-bottles` · NL `/rvs-drinkflessen`
  - FR `/gourdes-en-acier-inoxydable` · ES `/botellas-de-agua-de-acero-inoxidable`
  - It is **not** a global "prefix" or "suffix" rule — word order is language-specific. Ships with a documented per-locale convention + worked examples, review-enforced (it's editorial, not a build rule).
- Query-param URLs follow [[g-url]] State A: `noindex,follow`, canonical → parent, excluded from the sitemap, never a crawlable `<a>`.

> **g-url §FLT reconciliation (flagged).** g-url currently locks the **hyphen-suffix-against-parent** slug shape (`/printed-water-bottles-aluminium`) — that was the convention for *auto-generated* variants, which this model removes. For editorially-curated destinations, §FLT should relax to the readability rule above. This requires a paired edit to [[g-url]] §FLT (see Open points).

## Indexation safety net

Indexation decisions feed off AZ, so a careless block edit must never silently deindex live pages. Net (all reusing existing machinery):

- **The indexation engine owns the live state, AZ is the input.** g-url already stores per-locale meta-robots and re-evaluates on a **daily autonomous run**. Removing/replacing a block (or an `indexableFilters` entry) **proposes a demotion** reconciled on the next run — it does not evaporate indexation at render. State has inertia; flapping (earn→unearn→earn) doesn't thrash. *Because destinations are real self-owned pages, removing the parent AZ usually loses the internal link, not the destination's own indexation — far less fragile than a generated tier.*
- **In-session warning gate — always, including agents.** Actor-agnostic: removing/replacing a block or deleting `indexableFilters` entries that back live-indexed destinations raises an impact-sized warning ("defines N indexed pages driving X visits / €Y") before it takes effect. For agents it surfaces in the proposal/approval step. **Never a hard block** (avoids blocking unrelated changes).
- **Publish-time confirmation** when a publish would drop currently-indexed destinations.
- **Graceful demotion — redirect to the core PLP as standard.** When a destination genuinely stops indexing (page unpublished/removed), its URL **301s to the nearest earned ancestor, defaulting to the core PLP** (`/water-bottles-blue` → `/water-bottles`). Never a silent 404. Engine-driven after the grace window; reversible (re-publishing restores it); the URL drops from the sitemap and F1/internal hrefs recompute to query-param form.
- **Weekly overview message** (Slack → SEO Lead) of indexation changes (variants added/removed, demotions + redirects, blocks removed/replaced, high-impact warnings), complementing the **daily OP-56 diff** that flags any earned URL that lost its AZ backing since yesterday. Reporting only, never gating.

## The custom editor app

`filterConfig` is edited via a Contentful App (field appearance), scaffolded with `@contentful/create-contentful-app` against `FieldAppSDK`. It: (1) fetches **categories** from the catalogue → multi-select; (2) once categories are chosen, fetches the **union of attributes** for those categories; (3) configures **preFilters** (attribute → value(s)); (4) configures **shownFilters** (tick to expose, drag to order); (5) picks **attributesInDescription** (max 2, from the same attribute set) and **printrunPreselected** (from catalogue availability); (6) builds **indexableFilters** (pick attribute-value(s), attach a `pageHomeModular` destination via an entry-picker); (7) writes everything back as **keys** via `sdk.field.setValue()`; (8) on load, resolves stored keys → live labels, flagging any stale key with a visible warning. New catalogue categories/attributes appear automatically the next time the field is opened — no sync job.

## Rename & change resilience

Every stored key resolves to one of three states: **Valid** (resolves → render normally), **Renamed** (resolves; only the label differs → new label flows through automatically, no action), **Removed/invalid** (no longer in the catalogue → resolver skips it, page still renders with what's valid; editor app shows a warning). Optional admin health-check scans all entries for stale references ("category X deleted; N pages reference it").

## Render flow

1. Request hits the page URL → fetch the `pageHomeModular` + its AZ `filterConfig`.
2. Call the Merchant Catalogue with `categories` + `preFilters` → product list.
3. Call the catalogue's facets endpoint with `shownFilters` → render F1 with live labels + counts.
4. Visitor-applied filters layer on top of `preFilters` in the same query; pre-filters are always-on and not removable.

## Per-surface usage & deltas

- **FLP only.** AZ is the defining marker of an FLP: a [[pageHomeModular]] carrying a `filterConfig` block. It does not render on standard / sub / hub / themed PLPs or PDPs.
- **Render-only consumers (NOT Contentful blocks)** — `[V1·BUILD]` per FLP-Req v0-15:
  - **F1 filter panel** — reads `shownFilters`; renders facet values in the five-state HTML contract; crawlable `<a>` only when a destination exists in `indexableFilters`, otherwise `<button>`; counts SSR'd inline from the catalogue.
  - **F2 controls strip** — count · per-page · sort (Row A) · applied chips · Clear all (Row B).
  - **B5 grid** — the product slice for the current result-set + filter state; card metadata from `attributesInDescription`.
  - **F3 pagination** — "Load more" + crawlable numbered `<a>` graph; pages 2+ = `noindex,follow`, self-canonical, BreadcrumbList + ItemList dropped.
  - **F4 empty state** — HTTP 200, canonical → parent FLP, grid replaced by a single "Clear all filters" CTA.

## Requirements behaviour (render-only; consumes AZ)

- **SSR.** F1 + all facet values/counts SSR'd into the initial HTML on every state (base / query-param / destination); never injected post-load. Mobile combined "Subcategories and filters" drawer keeps anchors in the accessibility tree via `inert`. `[V1·BUILD]`
- **Five-state contract.** Per facet value: destination exists → `<a href>` to the destination URL; otherwise `<button>` (query-param). Zero-result intersection → `<span aria-disabled>`. Applied → `aria-current`/`aria-pressed`. `[V1·BUILD]`
- **Schema.** Indexable destination + base FLP page 1 emit `Organization`+`WebSite`+`SearchAction`+`WebPage`+`BreadcrumbList`+`ItemList` (ItemList only on indexable canonical URLs; omit on pages 2+, empty state, query-param states). **No `CollectionPage`**, no `SiteNavigationElement`. See [[g-schema]]. `[V1·BUILD]`
- **Meta / robots.** Indexed URLs (base + destinations) carry hand-authored meta. Query-param states inherit the canonical's meta, `noindex,follow`. See [[g-meta]] · [[breadcrumb]] · [[g-url]]. `[V1·BUILD]`
- **Single-select per axis; combination not click-order.** Earned slug depth soft-capped at 2 (deeper → query-param, canonical to nearest earned ancestor). Sort/pagination/view always non-indexable. `[V1·BUILD]`
- **Cache.** Catalogue resolution binds to the event-driven [[cache]] contract (Cache-Tag taxonomy, purge on triggering events). SSR-vs-build-time resolution rides with the catalogue system (open ticket).

## Decisions (locked)

- **Gate resolved** — Merchant Catalogue = single source of truth (products/taxonomy/attributes); Contentful owns the page. Supersedes the old `[PARKED]` "PCM/Algolia" state. **Algolia out of scope** (platform-catalogue proposal).
- **No new page type** — AZ is a `filterConfig` block on [[pageHomeModular]]; page fields (slug/meta/title/copy/hero) stay on the page.
- **Store keys, resolve labels live** — never store labels, swatches, counts or products. Config **not localized**; per-country differences = a separate Block AZ.
- **Three lists + semantics** — `categories` (OR) · `preFilters` (AND across / OR within) · `shownFilters` (show/hide + order) cover all six example pages.
- **`attributesInDescription`** — catalogue-selected keys, max 2, author-ordered, cascades from categories.
- **`printrunPreselected`** — own field, validated against catalogue availability.
- **Indexation = destination-only** — indexable ⟺ unique-content destination `pageHomeModular` ⟺ crawlable link; everything else = query parameter (noindex). Combinations hand-curated; `indexableFilters` requires a destination. Per-locale via INDEX-1.
- **Destination URL** — flat hyphenated, no folder path, editorially curated; **readability rule** (primary-keyword/H1 phrase in the locale's natural word order).
- **Safety net** — engine owns live state; in-session warning gate always (incl. agents); never hard-block; graceful demotion 301 → core PLP; weekly overview + daily OP-56 diff.
- **AZ is page-bound, 1:1 with its host page; off-page AZ is inert.** Page owns the routable slug; AZ carries `internalName` only.
- **Migration** — owned by the content-generation engine (out of scope here).
- **§3.2 / [[g-schema]]** — no `CollectionPage`; ItemList only on indexable canonical URLs. **§3.15** — `Should show per shop` dropped. **§3.19** — `target_keywords` shape; destinations carry their own set.

## Open points / build prerequisites

- **[OPEN TICKET] Merchant-Catalogue API contract** — gates the build (awaits the new product-catalogue system): endpoints/payloads for list-categories, attributes-per-category, values-per-attribute, product-list (categories+preFilters), facets+counts (shownFilters), printrun availability; plus the key-format/namespacing (`material:stainless-steel`).
- **[OPEN TICKET] Resolution timing + caching** — build-time vs render-time, against the [[cache]] contract; rides with the catalogue system.
- **[DONE 2026-06-08] [[g-url]] §FLT reconciled** — relaxed the auto hyphen-suffix-against-parent rule for editorially-curated destinations to the readability rule; State A/B/C reconciled to destination-only (no generated/thin tier); earned signal = unique-content destination declared in `indexableFilters`. Applied inline; pending Niels's git commit.
- **[V2]** in-grid promo card (B6); Model B dynamic filter variants; feed-driven `attributesInDescription` (drops the manual max-2).

## Sources

- `filter-pages-contentful-plan` (Sebastiaan/Niels, Jun 2026) — store-keys/resolve-live principle, `categories`/`preFilters`/`shownFilters` + combine semantics, example-page mapping, custom app, rename resilience, render flow, §8.1 (global attribute), curated-vs-generated.
- `variant-indexing-scope-v0` (Niels) — destination-only indexation; crawlable ⟺ indexable ⟺ unique content; no thin/generated tier; query params always non-indexable.
- FLP-Req v0-15 — §F1–F4 render contract, §g-flt earned-filter governance, OP-56.
- [[g-url]] §FLT — earned-filter URL/indexation rules, INDEX-1 per-locale engine, warning gates (cross-checked; paired edit flagged).
- Contentful live read (space `wm1n7oady8a5`/master) + _BUILD-BRIEF §3.2/3.15/3.19.

Related: [[surface-FLP]] · [[pageHomeModular]] · [[product-list-Z]] · [[g-url]] · [[g-schema]] · [[g-meta]] · [[breadcrumb]] · [[g-keywords-scoring]] · [[cache]] · [[promoCard]]



# ▌Global contracts


---


*(type: contract · surfaces: [PDP, PLP, FLP] · status: draft)*


# g-url — URL structure & indexation rule-engine

The contract that governs every page URL: slug shape, locale prefix, normalisation, and the per-locale indexation rule-engine that decides `index,follow` vs `noindex,follow`. Indexation is the load-bearing part — it lives here, not per-block.

**Labels:** V1·GUIDELINE ×9 (slug/indexation conventions) · V1·BUILD ×6 (per-locale meta-robots field, slug serialiser plumbing, filter-as-entry model) · V2·BUILD ×1 (variant indexation whitelist population). Source split: PLP demotes the URL-structure rows to GUIDELINE (commercial scoring card); the same rows on the PDP are `MUST·GUIDELINE`; the field/serialiser/whitelist engineering rows are `TECH·MUST·NEW·BUILD`. FLP URL rows = `[BUILD · V1]` / `[KEEP · V1]`.

## Rule

### URL structure (all surfaces) `[V1·GUIDELINE]`
- **Locale prefix mandatory** on every URL: `/{lang}-{country}/…` — including the default market (no locale-less root URLs even for NL). Keeps hreflang clean. `[V1·GUIDELINE]`
- **Flat kebab-case slug at root** — no folder hierarchy. `/brochure-and-booklet-printing`, never `/promotional-printing/brochure-and-booklet-printing`. Hierarchy lives in the breadcrumb + `BreadcrumbList` schema ([[breadcrumb]]), not the path. `[V1·GUIDELINE]`
- Words separated by single hyphens. Base URL ≤ 75 characters. `[V1·GUIDELINE]`
- A URL already in the sitemap is reused — no new URL without reason. `[V1·GUIDELINE]`
- **Verb in the slug:** PDP slug has **no verb** (e.g. `/booklets`, not `/booklets-printing`). PLP/FLP base slug is a **bare noun** category (`/visitekaartjes`, `/printed-water-bottles`); the verb can live in the title/H1 if it has search volume, not in the slug. Sub-category PLP slugs already carry the verb where it is part of the category name. `[V1·GUIDELINE]` (FLP bare-noun slug = `[V1·BUILD]` per FLP §URL)
- **Hyphen-separation enablement (PDP/PLP V1 plumbing):** the current routing layer does not yet emit multi-word hyphen-separated slugs; engineering builds the slug serialiser + redirect map. Open ticket-readiness questions (normalisation rule, migration set, redirect ownership, per-locale handling, conflict tie-break, authoring UX) resolved before implementation. `[V1·BUILD]` (url-11, `TECH·MUST·NEW·BUILD`) — the commercial hyphen guideline it enables is `[V1·GUIDELINE]`.
- **Existing non-compliant URLs are NOT migrated** (the rules apply to new URLs only; live non-compliant slugs keep their path — no traffic-driven migration). `[V1·BUILD]` (PLP url row `MUST·BUILD`; FLP "guideline applies to new URLs only" `[BUILD · V1]`).

### Per-locale meta-robots — the field `[V1·BUILD]`
- Meta-robots is a **per-locale Contentful field** on each `product` / `pageHomeModular` entry. Storefront reads the locale-specific value at render and emits `<meta name="robots">`. A page can be `index,follow` on `/nl-nl/` and `noindex,follow` on `/en-us/` from the same entry. `[V1·BUILD]` (PDP meta-20 + PLP `TECH·MUST·BUILD`)
- **Default value = `noindex, follow`** (locked §3.1). The rule-engine flips qualifying pages to `index,follow`; nothing ships indexed by default. `[V1·GUIDELINE]` (the default value is a content/SEO convention; the field that carries it is the BUILD above)
- Required field — the publish pipeline rejects any active locale with an empty meta-robots value. Pre-launch backfill: export every existing page × locale, SEO Lead fills each, re-import. Every NEW page × locale carries it from creation. `[V1·BUILD]` (PLP `TECH·MUST·BUILD`)
- See [[g-meta]] for where the value is emitted in the head, and [[g-tech-seo]] for the sitemap/hreflang gating that follows from it.

### Indexation rule-engine (per locale, autonomous) `[V1·GUIDELINE]`
Rules execute autonomously per page × locale on the daily run — no human gate per change (changes logged, warning-gated for high-impact pages, see below). A per-page Contentful override (`meta_robots_override`, `sitemap_inclusion_override`, `redirect_destination_override`) always wins over a rule outcome. Re-evaluates on material signal change; an already-live `index,follow` page can flip back to `noindex,follow`. `[V1·GUIDELINE]` (PLP rule rows all `MUST·v0.34·GUIDELINE`; the config exceptions file + sitemap-inclusion mechanism it drives is `[V1·BUILD]`)

**`INDEX-1` — `index, follow` when ALL hold (PLP/FLP):** `[V1·GUIDELINE]`
1. Combined primary + secondary keyword volume ≥ 20/month in this locale (Ahrefs + GSC).
2. Unique content — passes the cannibalisation scorer against siblings (see [[g-keywords-scoring]]).
3. No cannibalisation flag against sibling PLPs in this locale.
4. The locale-specific `target_keywords` set is filled.
5. URL compliant against the §URL-structure rules above (kebab, locale prefix, ≤ 75 chars, slug-order).
6. The locale URL field is explicitly authored in Contentful (not fallback-generated, per PRES-8693).

**`NOINDEX-1` — `noindex, follow`** when any INDEX-1 condition fails (e.g. volume < 20/month, cannibalisation flag, empty `target_keywords`). `[V1·GUIDELINE]`

**`NOINDEX-2` — explicit `noindex, follow` (override of INDEX-1)** when ALL hold: page exists for navigation only (not commercial entry), AND it would cannibalise an existing topic cluster (e.g. orientation/size sub-pages for Perfect Bound Brochures). `[V1·GUIDELINE]`

**`NOINDEX-NOFOLLOW`** — admin / system / transactional / session-state URLs (`/cart`, `/checkout`, `/my-account`, `/orders`, `/upload`). `[V1·GUIDELINE]`

**PDP indexation (URL rule-set):** base PDP is `index,follow` when it has SEO search volume / traffic / revenue relevance. Crucial PDPs — the **first 12 products of any PLP** — are always indexed. A non-crucial PDP falls back to `noindex,follow` only when **all three** hold: (1) combined + primary keyword volume < 20/month, (2) not in the first 12 of any PLP it lists on, (3) revenue < €10,000 in the last 6 months. Re-indexing is proposed by the responsible agent and confirmed with the Performance Lead before flipping back. `[V1·GUIDELINE]` (PDP url-5/url-6 `MUST·UPDATED·GUIDELINE`)

**Brand-new pages:** no `noindex` cooldown. A new page × locale that satisfies INDEX-1 on its first daily run flips to `index,follow` on day 1, enters the sitemap, and joins siblings' hreflang. `[V1·GUIDELINE]`

**Warning gates (surfaced in-session, not next-morning):** meta-robots flip on a page with > 1,000 monthly organic visits OR > €10,000 attributed revenue (last 6 months); sitemap removal of a previously-indexed URL. The rule may still be correct, but impact warrants human review. `[V1·GUIDELINE]` (the daily-review queue that surfaces them = `[V1·BUILD]`)

### PDP variant URLs — hyphen-suffix + whitelist `[MIXED]`
- **Default (everything):** variant attributes live in query parameters on the parent slug — `/en-gb/booklets?size=a5&appearance=gloss&material=90s` → self-canonical to itself **with the full query string**, `noindex, follow`. Consolidation is via sitemap + internal-link discipline, never a canonical hop. `[V1·GUIDELINE]` (PDP url-9 `TECH·MUST·UPDATED·GUIDELINE`)
- **Indexable variant:** defining attributes hyphen-appended to the slug — `/en-gb/booklets-a5-gloss` → `index,follow`, self-canonical. Remaining attributes stay as queries (those query URLs are self-canonical to themselves, `noindex, follow`). The slug is always a single product slug, **never a sub-folder hierarchy** (no `/booklets/a5/gloss`). `[V1·GUIDELINE]`
- **Whitelist:** a variant is indexable only when explicitly added to the Contentful indexation whitelist, keyed on the **(Attribute Group, Value, Product Family)** triple. Default for any tuple is `noindex` — only whitelisted tuples flip. So *Gloss Coated* under Booklets > Material can index while the same value under Stickers > Material stays `noindex`. Reviewed quarterly by SEO. Routing reads the whitelist at build time. `[V1·BUILD]` for the whitelist content-model (url-12, `TECH·MUST·NEW·BUILD`); quarterly review = `[V1·GUIDELINE]`.
- V1: the whitelist starts **empty** — the hyphen-suffix slug serialiser (url-11) ships as plumbing but no-ops until SEO ops adds entries (url-12, treated as V2 population). url-11 must not block on url-12. `[V2·BUILD]` (populating the whitelist is V2; the serialiser plumbing is V1·BUILD per §URL above).

### Filter URL governance (PLP & FLP) `[MIXED]`
Filter pages follow the same logic as PDP variants — query-param + canonical-to-parent by default, promoted to an **editorially-curated, unique-content destination PLP** only when demand is earned. **Destination-only — there is no thin/generated indexed tier:** indexable ⟺ a unique-content destination ⟺ a crawlable link (see [[filter-engine-AZ]]).
- **State A (filter applied, NOT earned, default):** `/printing-cottonbags?colour=black` → `noindex, follow`, canonical → `/printing-cottonbags`. `[V1·GUIDELINE]`
- **State B (earned single filter):** a **curated unique-content destination PLP** — `/printing-cottonbags-black` → `index,follow`, self-canonical, in the sitemap, the only state that gets a crawlable `<a>`. Its slug is editorially authored per the **readability rule** below (not auto-composed). `[V1·GUIDELINE]`
- **State C (second filter on an earned first, NOT earned):** `/printing-cottonbags-black?days=1` → `noindex, follow`, canonical → `/printing-cottonbags-black`. `[V1·GUIDELINE]`
- **Mint an earned destination PLP only when ALL 4 hold:** (1) cluster keyword ≥ 100 monthly searches in the target market, (2) ≥ 5 products surface under the filter, (3) demand is stable (not a one-off seasonal spike), (4) the page carries **genuinely unique** intro/content vs the parent (**non-negotiable — no destination without unique content**). Below threshold → query-param, canonical to parent. `[V1·GUIDELINE]` ("earned" criteria; FLP marks them `[KEEP · V1]` — inherits PLP)

### FLP earned-filter specifics `[MIXED]`
- **Earned destination slug = flat kebab, editorially curated, readability-ruled.** Slugs are **flat hyphenated, never a folder path** — forbidden: `/printed-water-bottles/aluminium` (path-segment-after-slash) `[V1·BUILD]`. Because a destination is a real curated PLP, its slug follows the **readability rule: the primary-keyword / H1 phrase in the locale's natural word order** — attribute-before-noun in EN/NL/DE (`/stainless-steel-water-bottles`, `/rvs-drinkflessen`), attribute-after-noun in FR/ES/IT/PT (`/gourdes-en-acier-inoxydable`). This **relaxes** the former auto hyphen-suffix-against-parent + template-ordered composition (that was for generated variants, now removed). Documented per-locale convention + examples, review-enforced. `[V1·GUIDELINE]`
- **Earned-filter variants are separate, unique-content `pageHomeModular` destinations** with a `parentCategory` reference to the base FLP, **declared in the parent FLP's Block AZ `indexableFilters` (combination → destination, destination required)** — see [[filter-engine-AZ]]. The published unique-content destination IS the earned-state signal — no manifest, no recommender flag, no build-time whitelist. The build reads `indexableFilters` / the destination entry when computing F1 hrefs, breadcrumb leaves, schema and sitemap: destination exists → crawlable `<a>` to the destination URL; otherwise → State-A query-param URL (`noindex`, no crawlable link). `[V1·BUILD]` (FLP `MUST·BUILD·[BUILD · V1]`)
- **Earned (indexed) slug depth — soft cap at 2 filters** (GUIDELINE). `/printed-water-bottles-black-stainless-steel`. Deeper combos stay query-param + canonical to nearest earned ancestor. `[V1·GUIDELINE]` (FLP `SHOULD·[BUILD · V1]` — soft cap, reviewed per case)
- Earned slug resolves on the filter **combination**, not click order (black-then-steel = steel-then-black). Query-param depth is unlimited but always `noindex, follow`, canonical to nearest earned ancestor. `[V1·BUILD]` (FLP `MUST·TECH·[BUILD · V1]`); V1 slug-ordering = whichever combination has an authored entry, with per-template deterministic ordering rules `[V2·BUILD]` (FLP OP-05 `V2 RULES·[BUILD · V2]`).
- Query-param composition (client-side `history.pushState`): alphabetic parameter ordering, lowercased authored slug fragments as values, single-select per axis (no comma-joined / repeated values). `[V1·BUILD]` (FLP `MUST·BUILD·[BUILD · V1]`)
- Sort / pagination / view-mode parameters are always non-indexable — canonical to default-sort, page-1, default-view. `[V1·BUILD]` (FLP `MUST·TECH·[BUILD · V1]`)
- Earned filter URLs are **slug-only — no ID suffix** (the slug+ID redirect-safety pattern is NOT adopted). Slug renames use standard 301s per [[g-tech-seo]]. `[V1·BUILD]` (FLP `MUST·TECH·[BUILD · V1]`)

### Sitemap & internal-link discipline (all surfaces) `[V1·BUILD]`
The XML sitemap contains only clean indexable URLs — never query URLs, never `noindex` pages. Internal links from menu, breadcrumb, Related products, footer and FAQ point to clean slugs only (no query strings, no tracking parameters). See [[g-tech-seo]]. `[V1·BUILD]` (PDP `TECH·MUST·NEW·GUIDELINE` for the discipline; the sitemap-gen mechanism is BUILD — owned by [[g-tech-seo]])

## Per-surface deltas
- **PDP:** no-verb slug; first-12 crucial-PDP override; hyphen-suffix variants gated by the (Attribute Group, Value, Product Family) whitelist; query URLs self-canonical + `noindex, follow`.
- **PLP:** bare-noun base slug; INDEX-1 / NOINDEX-1 / NOINDEX-2 rule-engine; earned filters mint via the 4-condition gate.
- **FLP:** inherits PLP URL + indexation verbatim; adds the earned-filter-as-curated-unique-content-destination model (readability-rule slug, declared in AZ `indexableFilters`). Filter-engine block (AZ) is **defined** — see [[filter-engine-AZ]].

## V1/V2
- **V1:** per-locale meta-robots field + emission; indexation rule-engine (PLP/FLP) and PDP 3-condition fallback; flat kebab slugs; hyphen-suffix slug serialiser plumbing (url-11); filter State A–C; FLP earned-filter-as-entry model.
- **V2:** populating the PDP variant indexation whitelist (url-12); per-template multi-filter slug ordering rules.

## Open points
- §3.1 override applied: default is `noindex, follow` (Niels overrides the PLP-catalog `nofollow` correction). The PLP-doc `NOINDEX-NOFOLLOW` state is retained only for admin/system/transactional URLs.
- PRES-8693 (per-locale URL authoring vs fallback chain) is tracked but out of V1/V2 build scope; INDEX-1 condition 6 depends on explicit authoring once it lands.
- FLP filter-engine (AZ) is **defined** — see [[filter-engine-AZ]] (Merchant Catalogue = SSoT, destination-only indexation, readability-rule slug, non-localized config; Algolia out of scope). The earned-filter URL contract above is reconciled to that model (2026-06-08 edit). AZ build is gated on the Merchant-Catalogue API contract (open ticket).

## Sources
- PDP Req v0-34 — §g-url (url-1 to url-12), §g-meta canonical rows, §B14 schema cross-refs.
- PLP Req v1-13 — §g-url (per-locale meta-robots, INDEX-1/NOINDEX-1/2, SITEMAP/HREFLANG/REDIRECT rules, filter pages), §g-meta canonical contract.
- FLP Req v0-15 — §URL, §FLT (earned-filter slug shape, Contentful-entry earned state, redirects).

Related: [[g-meta]] · [[g-schema]] · [[g-tech-seo]] · [[g-keywords-scoring]] · [[breadcrumb]] · [[cache]] · [[filter-engine-AZ]] · [[surface-PDP]] · [[surface-PLP]] · [[surface-FLP]]


---


*(type: contract · surfaces: [PDP, PLP, FLP] · status: draft)*


# g-meta — Title, description, canonical, hreflang & per-locale meta-robots

The SERP-framing contract: `<title>`, meta description, the canonical tag, hreflang, the head-emitted `<meta name="robots">` value, and URL normalisation. Title/description rules are GUIDELINE (commercial scoring); canonical/hreflang/robots emission is BUILD.

**Labels:** V1·BUILD ×7 (canonical self-ref + normalisation, cross-locale, hreflang emission + inclusion gate, meta-robots emission, build-time canonical-resolves check) · V1·GUIDELINE ×9 (title/description authoring, char counts, CTA, anti-cannibalisation copy, PLP 3-slot title) · V2 ×2 (PLP 4-slot title + USP-library Selection Engine; commercial title/desc/schema-field optimisation across all PDPs). Source split: PDP canonical/hreflang rows = `TECH·MUST·NEW·GUIDELINE` (doc files them under Guidelines but they are the head-emission contract — treated as BUILD per the build-brief axis); PDP title/desc rows = `MUST·GUIDELINE`; PLP canonical/hreflang/robots-emission = `[BUILD]`, PLP title/desc = `[GUIDELINE]`.

## Rule

### Per-locale meta-robots (head emission) `[V1·BUILD]`
- The per-locale meta-robots **field** is defined in [[g-url]] (default `noindex, follow` §3.1; flipped by the rule-engine). This contract owns its **emission**: the storefront reads the locale-specific value and renders `<meta name="robots" content="…">` in the head, byte-identical mobile + desktop (see [[g-mobile]]). `[V1·BUILD]` (PLP `TECH·MUST·BUILD` storefront read+emit)
- meta-robots and canonical are **orthogonal** — `noindex` controls indexation; canonical declares URL identity. Both are always emitted, even on `noindex` pages (AI crawlers GPTBot/ClaudeBot/PerplexityBot often ignore `noindex` but respect canonical). `[V1·GUIDELINE]` (PDP meta-13 `TECH·AEO·MUST·NEW·GUIDELINE`)

### Canonical `[MIXED]`
- **Self-canonical by default, everywhere.** Every page emits `<link rel="canonical" href="{this-page-absolute-URL}">` pointing to itself — never to a sibling, hub or parent. `[V1·GUIDELINE]` (PDP meta-11 `TECH·MUST·NEW·GUIDELINE`; the emission engine itself = V1·BUILD)
- **Never used to consolidate cannibalising siblings.** Cannibalisation is fixed by `noindex` or by differentiating content (PDP B7/B11/B15 generated on unique per-page signals), or — on PLP/FLP — by the cannibalisation scorer ([[g-keywords-scoring]]). Never a canonical hop. `[V1·GUIDELINE]` (PDP meta-12)
- **Self-canonical applies on `noindex` pages too.** `[V1·GUIDELINE]` (PDP meta-13)
- **Cross-locale:** each locale self-canonicals; hreflang declares siblings. Never canonical cross-locale. `[V1·GUIDELINE]` (PDP meta-14)
- **Variant / filter URLs:** hyphen-suffix earned slugs self-canonical to themselves (`/booklets-a5-gloss` → itself, never to `/booklets`). Query-state URLs are self-canonical **with the full query string** AND `noindex, follow` on PDPs; on PLP/FLP a non-earned filter query URL canonicals to the parent earned slug or hub (per the filter State A/C rules in [[g-url]]). `[V1·GUIDELINE]` (PDP meta-15/meta-16)
- **Normalisation:** every emitted canonical is HTTPS only · **no-www** (`helloprint.com`) · **no trailing slash** (except homepage root) · lowercase · tracking parameters stripped (`utm_*`, `gclid`, `fbclid`, `msclkid`, `mc_eid`, `ref_*`). The canonical that ships is always the normalised form regardless of how the URL was entered. `[V1·BUILD]` (PDP meta-18 `TECH·MUST·NEW·GUIDELINE` — the normaliser is build work)
- **Build-time validation (PLP/FLP):** every emitted canonical must resolve HTTP 200 AND (if `index,follow`) appear in the locale sitemap. A canonical pointing to a 404, a 301, or a non-sitemap URL fails the build. `[V1·BUILD]` (PLP canonical-resolves build check)

### Hreflang `[V1·BUILD]`
- Emitted in the **`<head>` only**, never in the sitemap (single source of truth, easier to debug). `[V1·BUILD]`
- Format `lang-CC` (lowercase language, uppercase country): `hreflang="nl-NL"`, `hreflang="en-GB"`. Matches the URL locale prefix. `[V1·BUILD]`
- **Self-reference** in every block, alongside sibling-locale alternates. `[V1·BUILD]`
- **Inclusion gate:** a locale appears in a page's hreflang only when its locale URL field is **explicitly authored** AND that locale is `index, follow`. `noindex` locales are excluded from every sibling's hreflang; a flip up/down regenerates every sibling's block on the next render. `[V1·BUILD]` (PLP `HREFLANG-IN` rule; emission is build, the rule is GUIDELINE-authored but enforced in the build)
- `x-default` — **homepage only**, points to the root domain (`https://helloprint.com/`). All other pages omit `x-default` until the planned Rest-of-World shop launches. `[V1·GUIDELINE]`
- **Reciprocity validation** is owned by [[g-tech-seo]] (asymmetric hreflang fails the build at PR review). `[V1·BUILD]` (cross-ref — see [[g-tech-seo]])

### Title `[MIXED]`
- **PDP pattern:** `[product name] [verb] | HelloPrint [country-code]`. Primary keyword = `[product name + verb]`. Max 60 chars, target 55. Country code only in the title suffix, never the description. Title is unique — not identical to the hub or any other PDP. `[V1·GUIDELINE]` (PDP meta-1..5 `MUST·GUIDELINE`)
- **PLP pattern (4-slot):** `[Primary keyword slot] | [Commercial USP slot] | HelloPrint [country-code]`. Length target 50–60 chars; the USP slot truncates first if over budget, primary keyword and brand never trim. The primary-keyword slot format is `[Optional modifier] [Category] [Verb]`; the verb appears even on a verb-less slug **if the verb has search volume**. The USP slot is filled by a Selection Engine reading a fixed 7-entry Contentful USP library (eligibility + priority) — never hand-typed, never scraped from page text; falls back to the 3-slot `[Primary] | HelloPrint [country]` if nothing qualifies. Within-title de-duplication: skip a USP sharing a meaningful token with the primary slot. `[V2·GUIDELINE]` for the 4-slot USP-driven title + Selection Engine; the **3-slot fallback ships V1** `[V1·GUIDELINE]`.
- **FLP titles are hand-authored per indexed URL** (base + earned filters) — no render-time template composition. Non-earned (query-param) states inherit the canonical's title verbatim. `[V1·GUIDELINE]` (FLP §META)
- Separator: pipe ` | ` only. No emojis/special characters. Capitalisation locale-tuned: title case for EN, sentence case for NL/DE/FR/ES/IT/PT (matches H1). `[V1·GUIDELINE]`
- Title + meta + H1 reinforce each other but are **never identical strings** (H1 owns on-page, title/meta own SERP framing). H1 ↔ title keyword overlap on the primary keyword is expected and allowed. `[V1·GUIDELINE]` (PDP meta reinforcement `SHOULD·NEW·GUIDELINE`)

### Meta description `[V1·GUIDELINE]`
- Carries from-price, lead time, or a USP — concrete, never generic. Max 155 chars. Contains primary + secondary keyword. Most important info in the **first 110 chars** (mobile SERP cutoff). `[V1·GUIDELINE]` (PDP meta-6..10 `MUST·GUIDELINE`)
- **CTA is concrete and scalable** — references a feature, not the product ("See your options", "Order from 50 pieces" — not "Order now"). **PLP CTA** combines catalogue breadth + a from-price ("Compare 5 binding types from £12", "Browse 12 booklet formats from £0.18/page"). FLP inherits the PDP meta-6..10 description discipline verbatim. `[V1·GUIDELINE]`
- Anti-cannibalisation: sibling PLPs (and a PLP vs its PDPs/variants) must lead with a distinct angle (page count, binding, use case, material, modifier). Checked against the Contentful `target_keywords` set, never by hand-curation. Two near-identical SERP previews fail the build. Modifier keywords (cheap/eco/luxe/premium) only when in this page's `target_keywords` with the matching intent tag. `[V1·GUIDELINE]` (anti-cannibalisation is a content discipline — no CI gate per §3.9; the `target_keywords`-based check is run through the scorer in [[g-keywords-scoring]])

## Per-surface deltas
- **PDP:** simple `[name] [verb] | HelloPrint [CC]` title; conversion-framed scalable CTA; variant/query canonical with full query string + `noindex, follow`.
- **PLP:** 4-slot USP-driven title (V2 for the USP slot; 3-slot in V1); breadth+price CTA; build-time canonical-resolves-200-and-in-sitemap check.
- **FLP:** hand-authored title + description per indexed URL (no template composition); non-earned states inherit canonical's meta; earned-filter canonical = self, non-earned canonical = nearest earned ancestor / parent.

## V1/V2
- **V1:** canonical (self-canonical, normalisation, cross-locale), hreflang emission + inclusion gate, per-locale meta-robots emission, PDP & FLP title/description authoring, PLP 3-slot title.
- **V2:** PLP 4-slot title with the Contentful USP-library Selection Engine (Phase 1 scraper is throwaway); commercial title/description/schema-field optimisation across all PDPs.

## Open points
- PLP "title uses 3 slots in V1, 4-slot is V2" — the 4-slot pattern and its 7-entry USP library are documented here but flagged V2.
- Dynamic USP slots follow the page cache-invalidation contract (price/delivery/Trustpilot-bound, event-driven; static USPs 24h TTL) — see [[cache]].

## Sources
- PDP Req v0-34 — §g-meta (meta-1..20), canonical/hreflang/normalisation rows.
- PLP Req v1-13 — §g-meta (4-slot title, USP library + selection engine, description, canonical contract, anti-cannibalisation).
- FLP Req v0-15 — §META (hand-authored per indexed URL, non-earned inheritance), §TECH hreflang.

Related: [[g-url]] · [[g-schema]] · [[g-tech-seo]] · [[g-uspbar]] · [[g-keywords-scoring]] · [[g-mobile]] · [[cache]]


---


*(type: contract · surfaces: [PDP, PLP, FLP] · status: draft)*


# g-schema — JSON-LD structured-data stack

The structured-data contract for every page. Schema is build-time output of the same product service that powers checkout/render. **Drift between displayed and structured data = build failure.** §3.2 is the controlling decision: there is **no `CollectionPage`** anywhere.

**Labels:** all-BUILD contract — schema emission is engineering output. V1·BUILD ×10 (full v5 listing stack, PDP Product/Offer/aggregateRating/FAQPage/Breadcrumb, sitewide Organization/WebSite, spam guardrail, CI integrity validation deploy-blocking) · V2·BUILD ×5 (PDP reviews + product `aggregateRating` activation, PDP `speakable`/`mainEntity`, `SearchAction` FLP, drift-detection hard-fail flip PLP/FLP, deferred `CollectionPage`/`Product.material` enhancements). **Surface-differing label:** schema **CI validation** = PDP deploy-blocking `[V1·BUILD]` (PDP B14 `TECH·MUST·BUILD`), whereas the PLP/FLP source filed it **SOFT-WARN V1 → hard-fail V2** — §3.2 promotes integrity validation to deploy-blocking in V1, drift hard-fail still flips V2. Almost every PDP B14 field row is `TECH·MUST·GUIDELINE` (the field-mapping is content-shaped) but the emitter that produces them is BUILD; the hard requirements (`hasMerchantReturnPolicy`/`inLanguage`/`dateModified`/`shippingDetails`/CI-validation) are explicitly `TECH·MUST·BUILD`.

## Rule

### Sitewide layer (every page) `[V1·BUILD]`
`Organization` + `WebSite` + `SearchAction` emit sitewide. `Organization` carries the **company-level `AggregateRating`** (Trustpilot, brand scope) — see [[g-uspbar]]. `SearchAction` (sitelinks search box) is **V2 on the FLP** `[V2·BUILD]`; **PLP marks it SHOULD** `[V1·BUILD]` (`TECH·SHOULD·GUIDELINE`).

### Listing pages (PLP / FLP) — the v5 stack `[V1·BUILD]`
Per §3.2 the listing root is **NOT `CollectionPage`**. The stack is:
`Organization` + `WebSite` + `SearchAction` (sitewide) + **`WebPage`** + **`BreadcrumbList`** + **`ItemList`**.

- **`WebPage` root fields:** `@type: WebPage`, `name`, `url`, `inLanguage`, `isPartOf` (the locale `WebSite` `@id`), `mainEntityOfPage` (`@id` = canonical URL). **`audience` is dropped** (§3.2 / OP-77) — never emit it; not required for AEO / rich-result eligibility. `[V1·BUILD]` (supersedes the PLP `CollectionPage` root which was `TECH·MUST·GUIDELINE`)
- **`ItemList` — render only on URLs that are canonical AND indexable:** root PLP/FLP, earned filter / sub-category PLP, page 1 of a pagination set (the bare URL). **Omit `ItemList`** on: pages 2+, empty-state URLs, non-earned (canonical-to-parent) filter URLs. `[V1·BUILD]` (FLP §JSON v5 OP-47 `[BUILD · V1]`)
- **`ItemList` structure:** single block scoped to the current filter state. `numberOfItems` = filtered total; `itemListElement` is an array of `ListItem` with `position` (absolute across pages — page 1 = 1–24, page 2 = 25–48) and a minimal `Product` (`url`, `name`, `image` only). Product-grid tiles (Block 5) and cross-sell tiles (Block 12, no `offers` — no price displayed) append to the **same** `ItemList`. `itemListOrder` = `ItemListOrderDescending` (order is meaningful — bestseller-first). The blog-teaser block (AJ) emits a **separate** top-level `ItemList` scoped to Article destinations (`name`, `url`, `position` only), never merged with the product list. `[V1·BUILD]` (PLP `TECH·MUST·BUILD` for the Block-12-append + drift rows; the `mainEntity`/`itemListOrder` field rows are `TECH·MUST·GUIDELINE`)
- **`BreadcrumbList`** mirrors the visible breadcrumb exactly (full path, every level), labels matching the HTML labels exactly. See [[breadcrumb]]. `[V1·BUILD]`
- **`FAQPage`** when an FAQ block is present (Q+A mirror of visible HTML); FLP `FAQPage` carries `isPartOf` → the FLP `WebPage` `@id`. `[V1·BUILD]`; FLP `FAQPage isPartOf` = `SHOULD, V1-if-scope` `[V1·BUILD]` (FLP OP-68).
- **No category-level `AggregateRating`** (§3.12) — the old PLP/FLP CollectionPage rating is dropped. Category-relevant Trustpilot reviews still render (UI-only, via a category `tag`) but emit **no schema**. Only the company-level rating (Organization) emits. `[V1·BUILD]` (supersedes the PLP `AggregateRating at category level` `TECH·MUST·BUILD` row — §3.12 drops it)
- **Listing page is never `Product`** — the build rejects a `Product` root on any PLP/FLP route. `[V1·BUILD]` (PLP `TECH·MUST·GUIDELINE` — enforced as a build reject)

### Product pages (PDP) `[V1·BUILD]`
`Product` + `Offer` / `AggregateOffer` + `aggregateRating` + `FAQPage` (sub-schema) + `BreadcrumbList` (sub-schema, inside the `Product` JSON-LD via the `breadcrumb` field — one `Product` entity per PDP). `[V1·BUILD]` (PDP B14 = "all 17 rows ship in V1")
- **`Product` fields:** `@type: Product`, `name` (page H1), `category`, `description` (meta description), `image`, `brand` (HelloPrint), `sku` (slug), `inLanguage` (locale), `dateModified` (last published), `hasMerchantReturnPolicy`, `shippingDetails`. `[V1·BUILD]` — field-mapping rows are `TECH·MUST·GUIDELINE`; `hasMerchantReturnPolicy`/`inLanguage`/`dateModified`/`shippingDetails` are `TECH·MUST·BUILD`.
- **`Offer`:** `price` = pre-set path price, `priceCurrency` = locale currency, `priceValidUntil` = current date. `AggregateOffer` / `hasVariant` / `isVariantOf` are **whitelist-only** (§3.2) — emitted only for whitelisted indexable variants (per the (Attribute Group, Value, Product Family) whitelist in [[g-url]]). `[V1·BUILD]` (PDP offer row `TECH·MUST·GUIDELINE`; whitelist gating ties to url-12)
- **`aggregateRating`** at **product level** via Trustpilot, **≥ 20 reviews** threshold; distinct from the brand-level Organization rating. PDP reviews block is V2. `[MIXED]` — the schema field is `[V1·BUILD]` (PDP b14-9 `TECH·MUST·GUIDELINE`) but activation rides the **PDP reviews block = V2** `[V2·BUILD]`.
- Three rating scopes never reuse schema: company-level (Organization, USP bar) · product-level (PDP) · and the dropped category-level (gone per §3.12). `[V1·BUILD]`

### Spam guardrail (Google policy — primary reason for the v5 reset) `[V1·BUILD]`
**Every schema field on a `Product` or `ItemList` must correspond to content visibly rendered on the page / product card.** Markup of invisible content is a structured-data spam violation (manual action → loss of rich-result eligibility). This is why `ItemList` Products stay minimal (`url`/`name`/`image`) and `material`/`color`/`additionalProperty`/`offers`/`aggregateRating`/`brand`/`sku`/`gtin` are **omitted unless visibly rendered**. Card-level inline microdata (`itemscope` `Product` + `itemprop` name/image/url) is a visible-content backstop alongside the JSON-LD. `[V1·BUILD]` (FLP §JSON v5 spam guardrail `[BUILD · V1]`)

### Drift = build fail · CI gate is deploy-blocking `[MIXED]`
- No drift between displayed and structured data — prices, delivery lines, ratings, breadcrumb labels, FAQ answers, `ItemList` order/names in JSON-LD must match the rendered HTML exactly. Drift = build failure. `[V1·BUILD]` on PDP (B14 drift `TECH·MUST·BUILD`); **PLP/FLP drift detection = SOFT-WARN V1 → hard-fail V2** `[V2·BUILD]` (PLP JSON-LD dashboard row).
- Schema validated against schema.org + Google Rich Results **in CI; validation failure blocks deploy** (§3.2). PDP ships this hard-fail in V1; PLP/FLP V1 was soft-warn-on-drift / hard-fail-on-integrity in the source docs — §3.2 makes CI validation deploy-blocking; drift hard-fail flips in V2 per the PLP/FLP labels (see Open points). `[V1·BUILD]` integrity validation (deploy-blocking, §3.2) · `[V2·BUILD]` drift hard-fail flip (PLP/FLP).

### Top anti-patterns (forbidden) `[V1·BUILD]`
`index, follow` on pages 2+ (they are `noindex, follow`) · canonical pages 2+ to the parent · `ItemList`/`BreadcrumbList` on non-canonical URLs (pages 2+, empty-state, non-earned filter) · Products in `ItemList` not visibly rendered · padded Product fields · breadcrumb leaf for a filter on a non-earned URL. `[V1·BUILD]` (FLP §JSON v5 anti-patterns `[BUILD · V1]`)

## Per-surface deltas
- **PDP:** `Product` + `Offer`/`AggregateOffer` (whitelist variants) + product-level `aggregateRating` (≥20) + `FAQPage` + `BreadcrumbList` (sub-schema inside Product). `speakable`/`mainEntity` = SHOULD, **V2** on PDP.
- **PLP:** `WebPage` + `BreadcrumbList` + `ItemList` (+ separate Article `ItemList`) + `FAQPage`; no `CollectionPage`, no category `AggregateRating`, no `audience`.
- **FLP:** same v5 stack as PLP; `ItemList` only on indexable canonicals (omit on pages 2+/empty-state/non-earned filter); filter state appears in schema only where it appears in the canonical URL; `speakable` + `mainEntity` (→ ItemList) + `FAQPage isPartOf` = SHOULD, V1-if-scope.

### Schema-stack summary (PLP/FLP)
| URL class | Robots | Canonical | BreadcrumbList | ItemList |
|---|---|---|---|---|
| Root PLP / FLP | `index, follow` | self | renders, ends at category | renders, unfiltered |
| Earned filter PLP | `index, follow` | self | renders, filter as leaf | renders, filtered |
| Pagination page 2+ | `noindex, follow` | self (with page param) | omitted | omitted |
| Non-earned filter URL | — | parent PLP | omitted | omitted |
| Empty-state URL | — | parent PLP | omitted | omitted |

## V1/V2
- **V1:** full v5 listing stack, PDP Product/Offer/aggregateRating/FAQPage/Breadcrumb, sitewide Organization/WebSite, spam guardrail, CI integrity validation deploy-blocking. FLP `speakable`/`mainEntity`/`FAQPage isPartOf` if in scope.
- **V2:** PDP reviews block + product-level `aggregateRating` activation; PDP `speakable`/`mainEntity`; `SearchAction` (FLP); drift-detection hard-fail flip (PLP/FLP); deferred enhancements (`CollectionPage` + `about`/concept URIs, `Product.material`/`color`/`additionalProperty`, Wikidata `sameAs`, `AggregateOffer` at ItemList level) — all only when their content is visibly rendered.

## Open points
- **§3.2 supersedes the PLP/FLP source docs' `CollectionPage` root** (PLP §g-schema TL;DR + FLP v0.5) — applied: `WebPage`-rooted, no `CollectionPage`, no category `AggregateRating`, `audience` dropped. The PLP source's `about`/`provider`/`potentialAction`/`mainEntityOfPage` CollectionPage fields are deferred (concept-URI knowledge graph is V2+).
- CI gate: §3.2 says "CI validation deploy-blocking" — applied as integrity hard-fail in V1 deploy-blocking; drift hard-fail follows the PLP/FLP V2 flip. Stated so the reconciliation is explicit.

## Sources
- PDP Req v0-34 — §B14 (Product JSON-LD field list, FAQPage/BreadcrumbList sub-schema, CI validation), §B9 (product-level AggregateRating), §USP (Organization AggregateRating).
- PLP Req v1-13 — §g-schema (entity set, ItemList/Article ItemList, AggregateRating scopes, drift rules) — CollectionPage superseded by §3.2.
- FLP Req v0-15 — §JSON v5 (OP-47 no-CollectionPage, ItemList render/omit, spam guardrail, anti-patterns, summary table), OP-68 (speakable/mainEntity/FAQPage isPartOf), OP-77 (WebPage root, audience dropped).

Related: [[g-uspbar]] · [[breadcrumb]] · [[g-url]] · [[g-meta]] · [[g-keywords-scoring]] · [[surface-PDP]] · [[surface-PLP]] · [[surface-FLP]]


---


*(id: 5npd8GXwWN930LLX254v4a · type: contract · surfaces: [PDP, PLP, FLP] · status: draft)*


# g-uspbar — USP bar above the H1

A slim, supportive brand-trust strip above the H1: a fixed set of brand USPs plus the company-level Trustpilot widget. Same content, same lock, sitewide and identical across PDP / PLP / FLP. Maps to the content-model block [[usp-block-BB]].

**Labels:** mostly V1·BUILD with a KEEP backbone (verify the existing live widget, don't reinvent) — PDP "all 9 USP rows ship in V1". V1·BUILD ×7 (4 USPs from the Contentful entry, SSR, no headings/non-clickable, position, mobile two-row wrap, Trustpilot widget, Organization AggregateRating) of which the Trustpilot widget + 3-USP backbone are `[V1·KEEP]` (existing component, reuse) · V1·GUIDELINE ×3 (position, compact-bar padding, click target, no-headings — content/UX conventions) · V2·BUILD ×1 (PLP/FLP CLS-safe contract + failure-mode + AggregateRating field-completeness flip to hard-fail). Surface split: PDP ships the full CLS contract + Organization AggregateRating in V1 (`TECH·MUST·UPDATED·BUILD`); the PLP filed AggregateRating **field-completeness as SOFT-WARN V1 → hard-fail V2**, and the Trustpilot widget as `[KEEP]` (existing integration, verify-survives-rebuild).

## Rule

### Exactly 4 brand USPs (§3.11) `[V1·BUILD]`
- The bar carries **exactly 4 brand USPs** in a fixed order. The PDP's "4" is correct; the PLP/FLP "3 locked" is **superseded** by §3.11. The source PLP/FLP three locked USPs are *Best Price Guaranteed · Always a Perfect Design · 100% Satisfaction Guarantee* — the 4th brand USP is sourced from the same Contentful Block G entry; do not author per page. `[V1·BUILD]` (PDP usp-4 `MUST·UPDATED·BUILD`; PLP "3 locked" was `TECH·MUST·LOCKED·KEEP·BUILD` — superseded to 4)
- **Source = Contentful Block G / "Locale Brand USPs" entry `5npd8GXwWN930LLX254v4a`** (locale-aware, read-only). Translated 1:1 per locale, never reordered, never replaced with shipping / facility / climate variants. `[V1·KEEP]` (PLP: "3-USP backbone exists today; reuse component"; content-ops translation = `[V1·GUIDELINE]` Needs-Content)
- Each USP is a styled span with a leading green checkmark before the label. **No headings inside the bar** (spans/paragraphs only), **no decorative emojis**, **not clickable** (except the Trustpilot widget). The bar is supportive, never heroic — must not push the H1 below the fold. `[V1·GUIDELINE]` (PLP no-headings `TECH·MUST·GUIDELINE`; not-clickable on PDP = `MUST·UPDATED·BUILD`)
- **Server-rendered, no client-side fetch** — crawlers see all 4 USPs + the Trustpilot score/count in raw HTML on first paint. `[V1·BUILD]` (PLP `TECH·MUST·BUILD`)

### Position `[V1·GUIDELINE]`
- Directly under the global header / sticky anchor nav. On the **PDP**: header → menu nav → breadcrumb → **USP bar** → H1. On **PLP/FLP**: first on-page element after the global navigation, above the breadcrumb (per the PLP source) → resolve to the surface DOM-order pages [[surface-PLP]] / [[surface-FLP]]. `[V1·GUIDELINE]` (PLP/PDP position `MUST·GUIDELINE`)

### Trustpilot widget — company-level AggregateRating `[MIXED]`
- Widget locked to the right (`margin-left:auto`), never wraps below the USP row on desktop. Structure: Excellent label · 5-square star block (last star half between bands) · "[review-count] reviews on" linked to the locale Trustpilot page · "★ Trustpilot" wordmark. `[V1·KEEP]` (PLP `TECH·MUST·KEEP·LOCKED·BUILD` — verify existing widget survives the rebuild, don't reinvent; External Integration = Trustpilot, in place)
- **Schema = `AggregateRating` nested in `Organization` (company-level, brand scope)** — distinct from product-level (PDP) and the dropped category-level (§3.12). Required fields: `ratingValue`, `bestRating` ("5"), `worstRating` ("1"), `reviewCount` (integer). FLP adds `aggregateType`. See [[g-schema]]. `[V1·BUILD]` on PDP (usp `TECH·MUST·UPDATED·BUILD`); **PLP field-completeness = SOFT-WARN V1 → hard-fail V2** `[V2·BUILD]`.
- **Click target** opens the locale Trustpilot page for HelloPrint (e.g. `trustpilot.com/review/helloprint.com` with the locale parameter) in a new tab. `[V1·GUIDELINE]` (PLP/PDP `MUST·GUIDELINE`)

### CLS-safe / never blocks LCP `[MIXED]`
- Widget reserves width + height in HTML (placeholder dimensions match the rendered widget pixel-for-pixel) so layout does not shift when JS hydrates. `[V1·BUILD]` on PDP (`TECH·MUST·UPDATED·BUILD`); **PLP CLS-safe contract rides V2** `[V2·BUILD]` (PLP `TECH·MUST·v0.34·BUILD`).
- SSR first paint shows the **last-cached Trustpilot score (≤ 24h old)** — never a loading skeleton, never zero stars. Interactive widget hydrates **after LCP**; the LCP candidate (first product tile / hero) is never blocked by the widget script. `[V1·BUILD]` (PDP); PLP/FLP `[V2·BUILD]`.
- Dynamic score follows the page cache-invalidation contract (≤24h cache) — see [[cache]]. `[V1·BUILD]`

### Failure mode (widget + schema hide together) `[MIXED]`
- If the Trustpilot API is unreachable AND the cached score has expired beyond 24h, the **entire widget hides** — never renders zero stars, never a loading skeleton, never a stock "Excellent" string. The slot collapses cleanly and the bar reflows. `[V1·BUILD]` on PDP; **PLP failure-mode = `[V2·BUILD]`** (`TECH·MUST·v0.34·GUIDELINE` in PLP, rides the PLP V2 CLS rollout).
- **When the widget hides, the `AggregateRating` schema block is also omitted** (never emit placeholder/default values — spam-policy compliance). The hide event is logged to the daily monitoring stream. `[V1·BUILD]` (PDP) / `[V2·BUILD]` (PLP/FLP).

### Mobile `[V1·BUILD]`
- All 4 USPs visible on mobile — the bar wraps to two rows on narrow viewports rather than hiding any USP (Trustpilot keeps its canonical styling). PLP/FLP additionally cap the bar height (≤ 56 px) and may horizontal-scroll the brand-USP list so it never pushes the first product row out of the first viewport; Trustpilot score + count stay visible without scrolling. See [[g-mobile]]. `[V1·BUILD]` (PDP usp-9 `MUST·UPDATED·BUILD`; PLP mobile `TECH·MUST·GUIDELINE`)

### Setup audit `[V1·GUIDELINE]`
- The CLS-safe contract is verified on **every surface** that renders the widget — homepage, every locale's PLP/PDP/FLP, checkout, contact pages — not just new pages. Same widget structure sitewide; no per-surface variants. `[V1·GUIDELINE]` (PLP v1.13 `TECH·MUST·GUIDELINE` — QA audit pass, not a build)

## Per-surface deltas
- **PDP:** all 9 USP rows ship V1; bar sits above the H1, below the breadcrumb.
- **PLP:** position above the breadcrumb; compact bar (14px vertical padding, 28px gap on desktop); CLS contract + failure mode (V1 verify-existing-widget / KEEP).
- **FLP:** inherits PLP §g-uspbar verbatim; the CLS / failure-mode / AggregateRating additions ride the PLP V2 rollout.

## V1/V2
- **V1:** 4 brand USPs from the Contentful entry, SSR, no headings/clickability, position, mobile two-row wrap, Trustpilot widget verify (KEEP existing). PDP ships full CLS contract + Organization AggregateRating in V1.
- **V2:** PLP/FLP CLS-safe contract + failure mode + AggregateRating field-completeness flip to hard-fail (rides PLP V2).

## Open points
- §3.11 supersedes the PLP/FLP "3 locked USPs" — applied: exactly 4. The 4th brand USP must be present in the Contentful Block G entry `5npd8GXwWN930LLX254v4a`; the source docs only name three by string — the 4th is sourced from the entry, not invented here.

## Sources
- PDP Req v0-34 — §USP (4 USPs, Trustpilot AggregateRating in Organization, CLS-safe, failure mode, mobile, click target).
- PLP Req v1-13 — §g-uspbar (3 locked USPs [superseded], compact bar, SSR, no headings, CLS-safe, failure mode, AggregateRating fields, setup audit).
- FLP Req v0-15 — §USP (inherits PLP; CLS contract, failure-mode widget+schema hide together, AggregateRating brand-level only, no product-level).

Related: [[usp-block-BB]] · [[g-schema]] · [[g-mobile]] · [[cache]] · [[reviews-blockP]] · [[surface-PDP]] · [[surface-PLP]] · [[surface-FLP]]


---


*(type: contract · surfaces: [PDP, PLP, FLP] · status: draft)*


# g-keywords-scoring — target_keywords & cannibalisation / content scoring

One Contentful `target_keywords` set per page × locale is the single source of truth for commercial intent. Every downstream block reads from it, and the cannibalisation / content-scoring mechanism reads from it. Defined once here; per-block rows just reference this contract — never re-state it.

**Labels:** V1·BUILD ×2 (the `target_keywords` Contentful field + Ahrefs/GSC read-only weekly integration; the scorer runs at build time) · V1·GUIDELINE ×6 (intent_tag taxonomy, priority/no-cap discipline, single-source feed, the scorer-as-discipline, PDP↔PLP H2 rule, cluster rule). **Phase/Type nuance:** the cannibalisation scorer is **GUIDELINE in V1** (a content discipline — no CI deploy gate per §3.9 / PLP/FLP source labels) and becomes a **build-pipeline hard-gate in V2** `[V2·BUILD]`. The PDP source phrases the verb-noun primary-keyword overlap as a build-time hard-fail, but §3.9 + the engineering principle "anti-cannibalisation is a content discipline — no CI gates" demote enforcement to GUIDELINE in V1; the PDP `target_keywords` + Ahrefs field is `TECH·SHOULD·NEW·BUILD` (V2 priority).

## Rule

### `target_keywords` — the field (§3.19) `[MIXED]`
- **One field per page × locale**, on both `product` (PDP) and `pageHomeModular` (PLP/FLP). Array of entries with the shape **`{keyword, search_volume, intent_tag, priority, locale}`** (the richer PLP shape; `priority` is load-bearing for primary vs secondary). `[V1·BUILD]` (PLP g-keywords field; PDP b2-19 = `TECH·SHOULD·NEW·BUILD`, V2 priority — content authors curate manually in the V1 window)
- Same Contentful entry carries **different keyword sets per locale** — "booklet printing" on en-GB, "boekjes drukken" on nl-NL — never inferred from translation. `[V1·GUIDELINE]`
- **`search_volume`** is **read-only**, written only by the integration (Ahrefs API / scheduled CSV, **weekly refresh**; plus GSC click+impression where the page is live). Editorial cannot hand-edit it. `[V1·BUILD]` (Ahrefs/GSC integration; External Integration = Ahrefs — V2 priority on the PDP, V1 on PLP)
- **`intent_tag`** ∈ {commercial, orientation, use-case, modifier, informational}. Drives which block surfaces the keyword: commercial+orientation → H1 + META; use-case+modifier → SEO-text H3s; informational → blog + FAQ themes. `[V1·GUIDELINE]`
- **`priority`** ordinal: primary · secondary-1 · secondary-2 · … H1 always uses primary; META uses primary in slot 1; SEO-text reaches for secondaries in priority order. `[V1·GUIDELINE]`
- **No hard cap on count** at the model (§3.19 overrides the PLP "1 primary + 1–5 secondaries / hard cap 6" guideline — see Open points; the SEO Lead still splits over-broad sets). Quarterly refresh by the SEO Lead: adjust priorities to Ahrefs/GSC shifts, retire entries below the INDEX-1 threshold (combined < 20/month per [[g-url]]). `[V1·GUIDELINE]`
- **Single source feeding** H1 / Meta / FAQ / SEO-text (B14/B15) / Person `knowsAbout` / schema / the scorer. Hand-curated per-page or per-block keyword choices are forbidden — they break the single-source contract. `[V1·GUIDELINE]` (the H1-sourced-from-keyword-set enforcement on PDP is `TECH·MUST·NEW·GUIDELINE`)

### The cannibalisation / content-scoring mechanism `[MIXED]`
- **Runs at build time, every page × locale.** Reads each page's `target_keywords` and compares against every sibling in the same locale (sibling = same parent or same hub cluster). Detects overlap on three axes: (a) verb-noun pairs, (b) primary-keyword exact-match, (c) full-phrase matches across the array. `[V1·GUIDELINE]` → `[V2·BUILD]` (the scorer is a content discipline / GUIDELINE in V1; becomes a build-pipeline hard-gate in V2)
- **Outcome:** zero overlap → pass · partial overlap → warning logged · full overlap → result depends on the gate (below). `[V1·GUIDELINE]`
- **Hard-fail:** any two siblings sharing the same **verb-noun pair on their primary keyword** (full primary-keyword match) → both pages fail the build until resolved, regardless of secondary differences. Applies across surfaces — a PDP claiming "booklet printing" while a sibling PLP also targets it fails the build. `[V1·GUIDELINE]` → `[V2·BUILD]` (PDP source phrases this as `TECH·MUST·NEW·GUIDELINE`/build-time check; §3.9 + the "no CI gate" engineering principle keep it GUIDELINE in V1, build-gated in V2)
- **Soft-warn:** sibling shares a **secondary** keyword (not primary) → warning logged to the daily review; does not block publish. SEO Lead decides accept (deliberate cluster) vs actionable (split it off). `[V1·GUIDELINE]`
- **New-sibling re-evaluation:** a new page authored with an overlapping primary / verb-noun pair fails the build on **both** the new and the existing page. Resolution: split · merge · rename · accept (one wins, the other goes `noindex` via the rule engine in [[g-url]]). Logged in the quarterly cycle. `[V1·GUIDELINE]` → `[V2·BUILD]` (PDP "future-proof against later PLP launches" `TECH·MUST·NEW·GUIDELINE`)
- **Cross-surface scoring:** the scorer also compares rendered **H2 strings** across PLP↔PDP for the same noun stem, **blog primary keywords** vs PLP primary (blog excluded from the teaser if it matches), and **meta-title sameness** across PLPs — all reading the same `target_keywords` source. `[V1·GUIDELINE]`

### The PDP↔PLP H2 rule (b9-11) — §3.9 `[V1·GUIDELINE]`
- **PLP/FLP reviews H2 = an action verb** — "Why {country} customers choose {primary keyword}". `[V1·GUIDELINE]`
- **PDP reviews H2 = a product-distinguishing attribute** — the PDP H2 **must carry a distinguishing token the PLP H2 doesn't**, so the two don't cannibalise on the shared noun stem. `[V1·GUIDELINE]`
- This is part of the cannibalisation mechanism (it runs through the scorer's cross-surface check) and lives **here, once** — not duplicated on each block. It is a **GUIDELINE, with no CI gate** (§3.9). Compare with the verb-noun primary-keyword hard-fail above, which IS build-blocking. `[V1·GUIDELINE]` (explicitly no CI gate in either phase per §3.9)

### What stays PDP-only / PLP-only (do not generalise) `[V1·GUIDELINE]`
- **Cluster / combining-keywords rule is PLP-only:** the 60%/40% volume thresholds, the three combination patterns (verb-pair / noun-pair / modifier-pair) — only combining keywords that are both in the set — the max-3 cap and the re-evaluation triggers. **PDPs never roll up two intent-aligned variants on one H1** (a PDP names one product). The cluster rule does not apply to the PDP. `[V1·GUIDELINE]`
- **PDP H1 verb rule (b2-7)** stays for backwards-compat (PDPs without a parent PLP carrying the verb); enforcement is now the build-time verb-noun check, not per-H1 manual review. `[V1·GUIDELINE]` (PDP b2-7 `MUST·UPDATED·GUIDELINE`)

## Per-surface deltas
- **PDP:** `target_keywords` on the `product` entry; verb-noun primary hard-fail; H2 = product-distinguishing attribute; cluster rule does NOT apply.
- **PLP:** `target_keywords` on `pageHomeModular`; full scorer incl. cluster rule for the H1; feeds INDEX-1 (volume + cannibalisation flag) in [[g-url]].
- **FLP:** inherits PLP §KW + PDP cannibalisation scorer verbatim. **Delta:** each earned-filter variant entry carries its **own** `target_keywords` set independent of the parent FLP; the scorer compares earned-variant primary KWs against parent FLP + sibling variants at build time; earned-variant minting requires scorer clearance before publish.

## V1/V2
- **V1:** `target_keywords` field + Ahrefs/GSC integration (read-only weekly volume); the scorer runs at build time. Per PLP/FLP source labels, the cannibalisation scorer is **GUIDELINE in V1**.
- **V2:** the scorer becomes a **build-pipeline hard-gate** (PLP/FLP). The PDP↔PLP H2 differentiation stays GUIDELINE (no CI gate) in both phases per §3.9.

## Open points
- §3.19 "no hard cap on count" supersedes the PLP §g-keywords "hard cap of 6 entries" guideline — applied. The SEO Lead may still split an over-broad set, but the model imposes no fixed cap.
- §3.9 confirms the b9-11 H2 rule is GUIDELINE-only (no CI gate), even though the source PLP rows phrase the cross-surface H2 check as running "through the scorer". Applied: the verb-noun *primary-keyword* overlap is the build-blocking gate; the H2 distinguishing-token rule is advisory.

## Sources
- PLP Req v1-13 — §g-keywords (target_keywords shape, intent_tag/priority, Ahrefs+GSC read-only, the scorer hard-fail/soft-warn/re-evaluation, cross-surface scoring, downstream block reads).
- PDP Req v0-34 — build-time cannibalisation enforcement (verb-noun uniqueness, future-proofing, cluster-rule kept PLP-only), b2-7 H1 verb rule.
- FLP Req v0-15 — §KW (inherits PLP+PDP verbatim; earned-filter variant own keyword set + scorer clearance).

Related: [[g-url]] · [[g-meta]] · [[g-schema]] · [[faq-blockV]] · [[reviews-blockP]] · [[person]] · [[rich-text-BE]] · [[surface-PDP]] · [[surface-PLP]] · [[surface-FLP]]


---


*(type: contract · surfaces: [PDP, PLP, FLP] · status: draft)*


# g-tech-seo — sitemap, redirects & hreflang reciprocity

Crawler-facing infrastructure: the XML sitemap, the redirect map, and hreflang reciprocity. All gated on the indexation rule-engine in [[g-url]]. A post-regen crawler walks every sitemap and reports HTTP status + drift daily.

**Labels:** all-BUILD contract (crawler-facing infrastructure is engineering output). V1·BUILD ×13 (master + per-locale sitemap indexes, `lastmod`, 03:00 regen + event-triggered, SITEMAP-IN/OUT, Sheet→Cloudflare redirects with approval gate + 301-target validation, hreflang reciprocity build-gate, drop-off alert, stale-content weekly digest, FLP `sitemap_plp_root` + `sitemap_plp_governed`) · V2·BUILD ×3 (image sitemap entries, post-regen crawler hreflang-reciprocity automation [FLP marks the crawler V2], FLP `sitemap_filters` Model B, long-term redirect source-of-truth consolidation). FLP sitemap rows = `[KEEP · V1]` where they inherit PLP §g-tech-seo §3.4a verbatim, `[BUILD · V1]` for the FLP-specific child sitemaps / drop-off / crawler, `[BUILD · V2]` for `sitemap_filters`. The PLP source labels every row in this section `[BUILD]`.

## Rule

### Sitemap `[V1·BUILD]`
- **Master sitemap index at `helloprint.com/sitemap.xml`**, declared in `robots.txt`, listing every active per-locale sitemap index (`helloprint.com/{locale}/sitemap.xml`). Submitted once to GSC + Bing Webmaster Tools; updates are picked up via daily regen + `lastmod` (no per-change ping). `[V1·BUILD]` (FLP inherits PLP §3.4a `[KEEP · V1]`)
- **Active-locale reconciliation:** the index ships only locales that are (a) in the active-locale list and (b) have ≥ 1 approved `index,follow` URL. `[V1·BUILD]`
- **Contents = clean indexable URLs only** — never query URLs, never `noindex` pages. Internal links (menu, breadcrumb, Related, footer, FAQ) point to clean slugs only, no query strings, no tracking params (PDP discipline, applies sitewide). `[V1·BUILD]` (PDP discipline `TECH·MUST·NEW·GUIDELINE`; enforced by the sitemap-gen build)
- **`lastmod` on every entry, sitemap-wide** — set to the most recent of: content-block change · meta-robots flip · price-driven cache invalidation ([[cache]]). **`changefreq` and `priority` are NOT emitted** (Google ignores them; fewer fields = fewer ways to lie). *(FLP exception: an optional 0.9/0.5 Class A/B `priority` override exists for orphan governance.)* `[V1·BUILD]` (FLP `MUST·TECH·BUILD·[KEEP · V1]`)
- **Regeneration:** daily backstop at **03:00 CET** + **event-triggered** on every Contentful publish, every meta-robots approval flip, every URL deletion, and every price-driven cache invalidation that affects URL availability. The daily regen catches anything the event chain dropped. `[V1·BUILD]`
- **SITEMAP-IN / SITEMAP-OUT** rules (defined in [[g-url]]): a URL enters on `index,follow` + URL-compliance + the regen; leaves on meta-robots flip to `noindex`, emptied locale URL field, Contentful deletion, or a new redirect-map entry. `[V1·BUILD]` (PLP `SITEMAP-IN`/`SITEMAP-OUT` rules authored as GUIDELINE, enforced in the build)
- **New-URL gating:** a new page × locale enters the sitemap only after the rule-engine flips it `index,follow` (a recommendation alone never pushes a URL in). `[V1·BUILD]`
- **Drop-off alert (FLP):** when the new sitemap URL count falls below ~80% of the previous day, an alert goes to the ops channel — critical for catching mass-deindexation from earned-filter churn. `[V1·BUILD]` (FLP-specific)
- **Post-regen crawler:** walks every sitemap URL (FLP: within 30 min of regen) checking HTTP status + meta-robots drift + canonical drift + hreflang reciprocity; daily digest to the SEO governance channel. `[MIXED]` — the daily crawler is `[V1·BUILD]`; FLP marks the **hreflang-reciprocity automation in the crawler as V2** `[V2·BUILD]`.
- **Stale-content alert:** weekly digest of every approved `index,follow` URL whose `lastmod` > 90 days, grouped by locale + content type; owned by the SEO Lead, reviewed with the indexation cycle. Covers PDP, PLP, FLP base + earned-filter variants. `[V1·BUILD]`
- **Hreflang is NOT in the sitemap** — emitted in the `<head>` only (single source; see [[g-meta]]). Sitemap entries carry no `xhtml:link` blocks. `[V1·BUILD]`
- Image sitemap entries are deferred to V2. `[V2·BUILD]`

### Redirects `[V1·BUILD]`
- **Source of truth = Google Sheet (editorial authoring, version-tracked) → Cloudflare edge (enforcement).** A sync job pushes Sheet → Cloudflare on save with a **manual approval gate**. Long-term direction is to consolidate (likely Contentful) — out of V1 scope. See [[cache]] for the Cloudflare edge layer. `[V1·BUILD]`; consolidation into Contentful = `[V2·BUILD]` (out of V1 scope).
- **301 by default, single hop, no chains.** A weekly chain-detection report (Monday 09:00 CET) exports A→B→C chains for flattening within 30 days. 302 only with an explicit flag. `[V1·BUILD]`
- **Never redirect to a `noindex` page** — a 301 target must be `index,follow` at the moment of the redirect (redirecting to `noindex` wastes the equity transfer). The build validates every 301 target against the destination's current meta-robots state; mismatches block the Cloudflare sync. `[V1·BUILD]`
- **Tracking-parameter strip on the destination** — a redirect from a URL carrying `?utm_*` / `?gclid` / `?fbclid` emits the destination without those params (canonical normalisation applies to the target). `[V1·BUILD]`
- **Hreflang update on redirect** — when `/old-slug` 301s to `/new-slug`, every sibling locale's hreflang block regenerates to point at `/new-slug`; no live page may carry hreflang to a URL that 301s. `[V1·BUILD]`
- **Sitemap update on redirect** — the redirected URL leaves the sitemap on the next regen; the destination stays if already approved indexed. `[V1·BUILD]`
- **Out-of-stock decision tree:** temporary OOS → PDP stays 200, indexed, in sitemap (flag set for SEO-Lead review). Long-term OOS / discontinued → PDP 301s to a documented replacement product or the parent PLP, removed from index (meta-robots → `noindex`) and sitemap. Decision owner = SEO Lead, surfaced via the daily review. `[MIXED]` — the redirect mechanism is `[V1·BUILD]`; the per-PDP decision (which target) is `[V1·GUIDELINE]` (SEO Lead).
- **Audit trail:** every redirect add/modify/remove is logged with timestamp, author, source URL, destination, type (301/302), reason, and Cloudflare sync timestamp; reviewed quarterly. `[V1·BUILD]`
- **FLP earned-filter unpublish:** when an earned filter loses earned status, the destination is decided case-by-case by the SEO Lead and entered manually — **no automated default redirect**. `[V1·GUIDELINE]` (manual SEO-Lead decision; FLP §TECH)

### Hreflang reciprocity `[V1·BUILD]`
- **Reciprocity validation — no orphan hreflang.** Every hreflang link in a page's `<head>` must have a matching return-link on the target page. Asymmetric hreflang (page A says "B is my Dutch alternate" but B doesn't link back) **fails the build at PR review**. `[V1·BUILD]`
- `noindex` locales are excluded from every page's hreflang; a flip `index,follow → noindex,follow` regenerates every sibling's block to drop that locale (and the reverse on a flip up). `[V1·BUILD]`
- **Earned-filter hreflang (PLP/FLP):** an earned-filter slug emits hreflang only between locales where the **same earned filter has been minted and approved indexed** — never to the parent PLP in another locale. If earned in nl-NL but not de-DE, the page emits hreflang only for the locales where the earned slug exists. `[V1·BUILD]`
- Self-reference in every block; format `lang-CC`; `x-default` homepage only. (Field shape + emission live in [[g-meta]]; this contract owns the reciprocity build-gate.) `[V1·BUILD]`

## Per-surface deltas
- **PDP:** clean-slug sitemap + internal-link discipline; out-of-stock redirect tree; query/`noindex` URLs never in the sitemap.
- **PLP:** full sitemap regen + SITEMAP-IN/OUT; Sheet→Cloudflare redirects; hreflang reciprocity build-gate.
- **FLP:** three child sitemaps per locale under `sitemap-index.xml` — `sitemap_plp_root_{locale}` (root categories), `sitemap_plp_governed_{locale}` (Model A dedicated filter pages, V1), `sitemap_filters_{locale}` (reserved for Model B variants, V2, not generated until Model B ships). Earned-filter URLs ride the same pipeline. Drop-off alert + 30-min post-regen crawler; earned-filter unpublish = manual redirect.

## V1/V2
- **V1:** master + per-locale sitemap indexes, `lastmod`, 03:00 regen + event-triggered, SITEMAP-IN/OUT, Sheet→Cloudflare redirects with approval gate + 301-target validation, hreflang reciprocity build-gate, drop-off alert (FLP), stale-content weekly digest. FLP `sitemap_plp_root` + `sitemap_plp_governed`.
- **V2:** image sitemap entries; post-regen crawler hreflang-reciprocity automation (FLP marks the crawler V2); FLP `sitemap_filters` (Model B); long-term redirect source-of-truth consolidation into Contentful.

## Open points
- Redirect-map long-term source of truth (Sheet → likely Contentful) is out of V1/V2 build scope.
- FLP Model A vs Model B serving architecture is decided per-locale (only one active at a time); Model B variants (separate `pageHomeModular` earned-filter entries) and their `sitemap_filters` are V2 — tied to the parked filter-engine ([[filter-engine-AZ]]).

## Sources
- PLP Req v1-13 — §g-tech-seo (sitemap index, lastmod, regen, new-URL gating, redirect Sheet→Cloudflare, never-redirect-to-noindex, tracking strip, hreflang reciprocity, earned-filter hreflang, out-of-stock).
- FLP Req v0-15 — §TECH (three child sitemaps, Model A/B, drop-off alert, 30-min crawler, reciprocity, earned-filter unpublish manual redirect, Class A/B priority override).
- PDP Req v0-34 — §g-url/§g-meta sitemap & internal-link discipline (clean indexable URLs only).

Related: [[g-url]] · [[g-meta]] · [[g-schema]] · [[cache]] · [[breadcrumb]] · [[filter-engine-AZ]] · [[surface-PLP]] · [[surface-FLP]]


---


*(type: contract · surfaces: [PDP, PLP, FLP] · status: draft)*


# g-mobile — mobile-first, content parity, performance & touch

Mobile is the crawl + measurement surface (Googlebot Smartphone is the default crawler). The contract: one DOM across viewports, full content parity (no `display:none` on SEO-bearing elements), performance budgets, and touch/input rules. Budgets differ by surface (§3.16).

**Labels:** all-BUILD contract (mobile-first is engineering output). V1·BUILD ×7 (single responsive site, viewport meta, content-parity CI gate, performance budgets + Lighthouse CI, touch/input contract, image pipeline, mob-parity schema/hreflang/canonical) · V2·BUILD ×2 (PDP `SpeakableSpecification`; Search Console mobile-usability + CWV field-data alert routing — deferred ops follow-up) + FLP page-size experiment = a **commercial GUIDELINE** `[V2·GUIDELINE]`. **Surface-differing label:** the **performance-budget CI gate is deploy-blocking BUILD on PDP/PLP** (PDP mob `TECH·MUST·NEW·BUILD`), but the **PLP source demoted its own Lighthouse/WebPageTest/CrUX checks to a commercial GUIDELINE** (`[V1·GUIDELINE]` — SEO Lead samples live PLPs, no CI gate); reconciled — the PDP CI gate is the canonical deploy-blocking enforcement, PLP rides it where the same template ships. Most PDP mob rows are `TECH·MUST·NEW·BUILD` or `TECH·AEO·MUST·NEW·BUILD`; touch-target / viewport-meta rows that are accessibility-guidance carry `TECH·A11Y·NEW·GUIDELINE`.

## Rule

### Mobile-first & single responsive site `[V1·BUILD]`
- **One DOM, one render path, CSS reflows only.** No separate mobile site (`m.helloprint.com` forbidden), no `/mobile/` path prefix, no UA-based routing / device detection for layout or content, no "redirect to mobile" 302s, **no AMP** (`<link rel="amphtml">` never emitted). The existing `nl-BE`/`fr-BE`/`en-IE`/`en-US` locale-fallback chain (PRES-8693) is locale fallback, not adaptive serving. `[V1·BUILD]` (PDP mob `TECH·AEO·MUST·NEW·GUIDELINE` for the no-adaptive-serving discipline; enforced as a build/architecture rule)
- **Canonical viewport meta**, emitted once by the layout template on every page: `<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">`. No `user-scalable=no`, no `maximum-scale=1` (pinch-zoom must never be blocked — WCAG). Build-time check fails the deploy if the string drifts. `[V1·BUILD]` (PDP mob-13 `TECH·MUST·NEW·BUILD`; the pinch-zoom rule is `TECH·A11Y·NEW·GUIDELINE`)
- **First-viewport contract** uses `dvh`/`svh`, never bare `vh` (iOS Safari URL-bar collapse). Test baseline 375 px; also 360 / 414 / 768 px. Honour `safe-area-inset` (`viewport-fit=cover`), `prefers-reduced-motion`, and a graceful landscape degrade. `[V1·BUILD]` (PDP mob-10/mob-11 `TECH·MUST·NEW·BUILD`; `prefers-reduced-motion` = `TECH·A11Y·NEW·GUIDELINE`)

### Content parity — no `display:none` on SEO-bearing elements `[V1·BUILD]`
- **Build-time check fails the deploy when any SEO-bearing element is hidden via `display:none` on the mobile breakpoint** (or removed from the DOM via JS, or fetched via JS after first paint). `[V1·BUILD]` (PDP mob-35 `TECH·AEO·MUST·NEW·BUILD`)
- **SEO-bearing element list:** H1 · all H2/H3 headings · breadcrumb chain (+ BreadcrumbList schema) · intro paragraph body · in-context USPs / Pros / Green Claim (PDP B17) · product-description prose · specifications · FAQ questions AND answers (incl. collapsed answer text) · SEO text (incl. text behind "Show more") · related-product tile names + slugs · product / page JSON-LD · AggregateRating widget text · canonical / hreflang / robots meta · every `<img alt>` · internal anchor link text. `[V1·BUILD]`
- **Allowed collapse mechanisms (content stays in DOM):** `height:0; overflow:hidden` · `visibility:hidden` · `aria-hidden` + CSS visibility · transform/opacity for animation. **Forbidden:** `display:none` · DOM removal · `fetch()`-on-mount or client-render-only components for indexable content. Hydration may only attach behaviour to existing DOM, never add SEO-bearing content. `[V1·BUILD]` (PDP mob-36 `TECH·AEO·MUST·NEW·BUILD`)
- **SEO surface byte-identical mobile + desktop** — schema, canonical, hreflang, meta-robots, structured data render identically across viewports; drift is a mobile-first-indexing hazard ([[g-schema]], [[g-meta]]). A CI script parses the SSR HTML and asserts every SEO-bearing element is present with non-empty content per PR; failure blocks the deploy. `[V1·BUILD]` (PDP `TECH·AEO·MUST·NEW·GUIDELINE` for parity / `TECH·AEO·MUST·NEW·BUILD` for the CI assertion; PLP mob-parity `TECH·MUST·NEW v1.7·BUILD`)
- DOM order is verified against raw HTML (CSS Grid/Flexbox `order` reorders visually only, never moves semantic content past its rank). Tab UIs collapse to a vertical accordion on mobile (same DOM). `[V1·BUILD]` (PDP `TECH·MUST·NEW·GUIDELINE` verify-order; tab→accordion `TECH·MUST·NEW·BUILD`)

### Performance budgets (§3.16 — surface-specific) `[MIXED]`
| Metric | PDP / PLP | FLP (looser delta) |
|---|---|---|
| LCP | ≤ 2.0 s | ≤ 2.5 s |
| INP | ≤ 150 ms | ≤ 200 ms |
| CLS | ≤ 0.05 | ≤ 0.1 |
| TTFB | ≤ 250 ms cached / ≤ 600 ms uncached | (inherits) |
| FCP | ≤ 1.5 s | (inherits) |
| Initial JS bundle | ≤ 250 KB gzip | (inherits) |
| First-viewport image bytes | ≤ 400 KB | (inherits) |

Measured on the canonical 375 px viewport, lab + field (CrUX where available), **Moto G4 / throttled 4G** (matches Google's synthetic profile).
- **PDP/PLP:** the budget is a **deploy-blocking CI gate** (Lighthouse CI per PR; device profile Moto G4 / slow-4G; failures on Performance/Accessibility/SEO block the PR). CrUX field data is the indexed ranking metric. `[V1·BUILD]` (PDP mob-19 `TECH·MUST·NEW·BUILD`, deploy-blocking)
- **FLP:** the looser LCP ≤ 2.5s · INP ≤ 200ms · CLS ≤ 0.1 budget reflects the heavier filter/grid surface. The FLP page-size experiment (24→36→48) runs a 4-week CWV monitoring window and rolls back if vitals degrade. `[V1·BUILD]` for the looser budget (FLP §MOB) · `[V2·GUIDELINE]` for the page-size experiment (commercial / SEO-ops decision).
- *(Note: the PLP source demoted its Lighthouse/WebPageTest/CrUX checks to a commercial GUIDELINE — SEO Lead runs them across sample live PLPs, no CI deploy gate. The PDP CI gate is the canonical deploy-blocking enforcement; PLP rides the PDP gate where the same template ships.)* — **surface-differing label:** PDP CWV = deploy-blocking `[V1·BUILD]`; PLP perf checks demoted to `[V1·GUIDELINE]`.
- **Image loading:** LCP element loads eager (`fetchpriority="high"` + AVIF `<link rel="preload">` in head, **Contentful Image API** URLs — see [[cache]]); everything else `loading="lazy"` + `decoding="async"`. `srcset` + per-breakpoint `sizes`; `width`/`height` always declared (CLS). On PLP/FLP grids: row-1 (2 tiles on 375 px) eager, first tile `fetchpriority="high"`; **hover-image swap disabled on mobile** (`<picture>` media rules → one image per tile — the biggest LCP risk on a 2-up grid). Critical CSS inlined (≤14 KB gzip); fonts `font-display:swap` + preload + subset; JS lazy-chunks (chat, reviews, lightbox) excluded from the initial bundle; long-task discipline (no task > 50 ms) for the INP gate. `[V1·BUILD]` (PDP mob-20/21 + mob image rows `TECH·MUST·NEW·BUILD`; LCP-eager/srcset are `TECH·MUST·GUIDELINE`)

### Touch & input `[V1·BUILD]`
- **Touch targets ≥ 44 × 44 px AND ≥ 8 px spacing** between adjacent targets (WCAG 2.5.8; 24×24 + 24-spacing is the absolute floor). Applies to configurator tiles, Add-to-cart, breadcrumb segments, FAQ chevrons, USP-bar Trustpilot, PM LinkedIn link, gallery arrows, related-product CTAs, menu bucket entries, anchor pills. `[V1·BUILD]` (PDP mob-24 `TECH·A11Y·NEW·GUIDELINE` for the size rule — "new build work, not KEEP"; spacing mob-31 `TECH·A11Y·NEW·GUIDELINE`)
- `touch-action: manipulation` on interactive controls (removes the 300 ms tap delay). Hover is never the only affordance (reachable via `:focus-visible` / tap). Form inputs render at **`font-size ≥ 16 px`** (prevents iOS auto-zoom); `inputmode` + `autocomplete` tokens on every input. `[V1·BUILD]` (PDP mob-25/27/28 `TECH·MUST·NEW·BUILD`; hover-not-only-affordance = `TECH·A11Y·NEW·GUIDELINE`)
- No intrusive interstitials (Google penalty) — no fixed/sticky element at z-index > 100 covering > 30% of the mobile viewport in the first second after navigation. Chat widget (V2) is floating-action-button only, never auto-opens. `[V1·BUILD]` (PDP mob `TECH·AEO·MUST·NEW·GUIDELINE`; chat widget itself V2)

## Per-surface deltas
- **PDP:** first viewport = breadcrumb + H1 + hero (≤ 200–250 px) + intro (visible 2 lines) + start of configurator. Sticky bottom **purchase bar** (mobile-only, ≤ 64 px, respects `safe-area-inset-bottom`, hides on virtual-keyboard open via `VisualViewport`). i-button = full-screen modal on mobile. DOM order H1 → img → intro → configurator. CI budget gate deploy-blocking.
- **PLP:** first viewport = USP bar (≤ 56 px) + breadcrumb + H1 + 2-line intro + ≥ 2 product tiles. **No sticky bottom cart panel** (tap a tile → PDP). Sticky anchor nav hidden < 600 px (hamburger + bucket panels, same crawlable links). Breadcrumb single-line, horizontal-scroll on overflow (never wrap, never ellipsis-truncate; full chain in DOM + schema). mob-parity: same JSON-LD / hreflang / canonical / meta-robots across viewports.
- **FLP:** inherits PLP mobile; **looser CWV budget** (§3.16); combined "Subcategories and filters" mobile drawer (SSR'd, no client fetch); F2 controls strip compresses; sticky F2 bar uses `position: sticky` (not `fixed`) so it doesn't interfere with LCP detection on the first product tile; B2b taxonomy tree is a mobile drawer (branches crawlable in initial HTML).

## V1/V2
- **V1:** single responsive site, viewport meta, content-parity CI gate, performance budgets + Lighthouse CI (PDP/PLP deploy-blocking; FLP looser), touch/input contract, image pipeline, mob-parity.
- **V2:** PDP `SpeakableSpecification`; Search Console mobile-usability + CWV field-data alert routing (deferred ops follow-up); FLP page-size experiments are a commercial guideline.

## Open points
- §3.16 applied: PDP/PLP = LCP ≤2.0s · INP ≤150ms · CLS ≤0.05; FLP looser = ≤2.5s · ≤200ms · ≤0.1. Stated explicitly above.
- Source tension: the PDP doc makes the perf budget a deploy-blocking CI gate; the PLP doc demoted its own perf checks to a commercial GUIDELINE (no CI gate). Reconciled: PDP CI gate is the deploy-blocking enforcement; PLP perf is verified via SEO-Lead sampling unless it rides the PDP template gate. Noted, not silently merged.

## Sources
- PDP Req v0-34 — §Mobile (viewport, dvh/svh, safe-area, content parity + SEO-bearing list, perf budgets CI gate, touch/input, sticky purchase bar, mobile-first indexing, Contentful Image API).
- PLP Req v1-13 — §mob-viewport / §mob-dom / §mob-perf / §mob-input / §mob-parity (first viewport, no sticky cart, breadcrumb horizontal-scroll, hover-swap disabled, schema/hreflang/canonical parity, Lighthouse demoted to guideline).
- FLP Req v0-15 — §MOB (LCP ≤2.5s · INP ≤200ms · CLS ≤0.1 Moto G4/4G, sticky F2 position:sticky, filters drawer, B2b mobile tree, page-size experiment).

Related: [[g-schema]] · [[g-meta]] · [[g-uspbar]] · [[cache]] · [[breadcrumb]] · [[surface-PDP]] · [[surface-PLP]] · [[surface-FLP]]


---


*(type: contract · surfaces: [PDP, PLP, FLP] · status: draft)*


# cache — Cloudflare edge, event-driven purge & cache-key tuple

The caching contract. Pages render fast from the Cloudflare edge, but **caching is never the cause of drift**: every event that can change output triggers a purge of the dependent fragments. TTL is a safety net, never the primary mechanism. Images are served from the Contentful Image API, not a separate CDN.

**Labels:** all-BUILD contract (caching is engineering infrastructure). V1·BUILD ×6 (Cloudflare edge caching, event-driven purge on all listed events, cache-key tuple, TTL=0 fallback for non-guaranteeable fragments, Cache-Tag selective purge / FLP whole-page + SWR, Contentful Image API) · V2·BUILD ×1 (FLP per-tile ESI fragment composition via Cloudflare Workers — conditional on telemetry). Source: the FLP §Cloudflare OP-66 rows are `MUST·BUILD·[BUILD · V1]`; the ESI V2-revisit row is `V2·[BUILD · V1]` framed as the V2 escape hatch. PLP cache rows sit inside §B5 price / §BG / §g-meta freshness as `[BUILD]`.

## Rule

### Edge caching (Cloudflare) `[MIXED]`
- Page responses are cached at the **Cloudflare edge**. **FLP V1 architecture (OP-66):** whole-page cache with Stale-While-Revalidate — `Cache-Control: max-age=300, stale-while-revalidate=86400`. Users never see a slow uncached response; cache freshness within ~5 min of invalidation; a transient 1–2 s inconsistency window is acceptable. Per-tile ESI fragment composition is deferred to V2 (Cloudflare Workers) unless hit rate degrades below 85% (or catalogue > 50K products, or per-card invalidation latency tightens). `[V1·BUILD]` whole-page + SWR (FLP OP-66 `MUST·BUILD·[BUILD · V1]`) · `[V2·BUILD]` per-tile ESI escape hatch.
- The redirect map is also enforced at the Cloudflare edge (authored in a Google Sheet, synced with a manual approval gate) — see [[g-tech-seo]]. `[V1·BUILD]`

### Cache-key tuple `[V1·BUILD]`
- The cache key includes **URL + locale + currency + customer segment (B2C / B2B)** so segments never share the wrong fragment. The FLP adds **VAT-toggle state** to the tuple. Price-bound fragments (Block 5 grid / pre-set path), promo cards (BG) and the page itself all sit on the same key. `[V1·BUILD]` (FLP OP-66 cache-key + VAT-toggle `[BUILD · V1]`)
- The product-rating fragment cache key **includes the page type** so a PDP product-level rating can't render on a PLP (and vice versa) — see [[g-schema]] (three rating scopes, no reuse). `[V1·BUILD]`

### Event-driven purge (never TTL-first) `[V1·BUILD]`
- **Every event that can change the pre-set-path output triggers a cache purge of every dependent fragment.** TTL is a safety net only. `[V1·BUILD]`
- **Cache-purging events (non-exhaustive):** price update · promotion start / end / edit · VAT or tax-rule change · currency-rate update · margin / cost re-pricing · SKU availability change. The same event drives the auto product-order rebalance (an expired/paused/unpublished promo card reflows the grid on the same invalidation event, so the grid never renders mid-state) and the sitemap event-triggered regen ([[g-tech-seo]]). `[V1·BUILD]`
- **If event-driven invalidation cannot be guaranteed for a fragment, that fragment is uncached (TTL = 0).** Better a live render than a wrong price — a stale tile risks a Google Merchant Center landing-page price-mismatch flag, feed disapproval, and stopped ad spend, a cost always higher than the latency. `[V1·BUILD]`
- **Cache-Tag taxonomy for selective purge (FLP OP-66):** every FLP response is tagged with `flp-{slug}`, `locale-{xx-XX}`, and `pdp-{pcmId}` (one tag per visible product in the grid). Cloudflare API purges by tag on triggering events. `[V1·BUILD]` (FLP OP-66 `MUST·BUILD·[BUILD · V1]`)
- **Promo / BG activation is event-driven, not TTL-bound** — adding/removing/changing a promo card's date window publishes a cache-invalidation event purging every BG fragment for the affected page × locale × currency × segment; discount labels are removed automatically the moment a promotion ends. `[V1·BUILD]`
- **USP / meta freshness ([[g-meta]], [[g-uspbar]]):** dynamic USPs (price-, delivery-, Trustpilot-bound) invalidate on source-change events — same event-driven contract as Block 5 price. Static USPs (templates, eco, custom sizes) get a 24h TTL (no live source to bind to). If a dynamic source is unavailable at render, that USP is dropped from the eligible set rather than rendering a half-template. The Trustpilot widget shows the **last-cached score ≤ 24h** on SSR; if API + cache are both unavailable the widget and its schema hide together. `[V1·BUILD]` (dynamic-USP invalidation; the 4-slot USP Selection Engine that consumes it is V2 per [[g-meta]])

### Images — Contentful Image API `[V1·BUILD]`
- **Contentful is both the asset store and the image CDN — no separate image-CDN procurement.** Image URLs in `srcset` / `<link rel="preload">` are Contentful Image API URLs (`https://images.ctfassets.net/…?fm=avif&w=600&q=80`), with AVIF transcoding + per-breakpoint resize via URL params. Center-crop / pad transforms handle non-square masters (e.g. PDP 1:1 gallery). See [[g-mobile]] for the LCP/preload contract. `[V1·BUILD]` (PDP Contentful Image API `TECH·MUST·NEW·BUILD`)

## Per-surface deltas
- **PDP:** price pre-set path is the canonical event-driven fragment; query/variant URLs are cacheable on the same key but never share segments; hero AVIF preloaded from the Contentful Image API.
- **PLP:** Block 5 grid + BG promo cards on the (URL, locale, currency, segment) key; rating fragment carries page type; lastmod feeds on price-driven invalidation.
- **FLP:** whole-page cache + SWR (`max-age=300, stale-while-revalidate=86400`); cache-key adds VAT-toggle state; Cache-Tag taxonomy (`flp-`, `locale-`, `pdp-`) for selective purge; ESI per-tile composition is the V2 escape hatch.

## V1/V2
- **V1:** Cloudflare edge caching, event-driven purge on all listed events, the cache-key tuple, TTL=0 fallback for non-guaranteeable fragments, Cache-Tag selective purge (FLP whole-page + SWR), Contentful Image API.
- **V2:** FLP per-tile ESI fragment composition (Cloudflare Workers) if hit rate < 85% / catalogue > 50K / latency tightens; redirect-map source-of-truth consolidation (out of scope here, see [[g-tech-seo]]).

## Open points
- FLP V1 deliberately chooses whole-page cache over per-tile ESI for operational simplicity; the V2 flip is conditional on telemetry. PDP/PLP fragment-level vs whole-page caching is not separately locked in the source docs beyond the event-driven + cache-key contract — captured as the shared rule above.

## Sources
- PLP Req v1-13 — §B5 price pre-set path (caching never causes drift, purge events, TTL=0 fallback, cache key locale/currency/segment), §BG (event-driven activation, (URL,locale,currency,segment) key), §g-meta cache & freshness, §g-schema rating-fragment page-type key.
- FLP Req v0-15 — §Cloudflare (OP-66 whole-page + SWR `max-age=300, stale-while-revalidate=86400`, cache-key + VAT-toggle, Cache-Tag taxonomy, ESI V2 conditions).
- PDP Req v0-34 — Contentful Image API (asset store + image CDN, AVIF/resize URL params, center-crop/pad), hero AVIF preload.

Related: [[g-tech-seo]] · [[g-meta]] · [[g-uspbar]] · [[g-mobile]] · [[g-schema]] · [[productCollection]] · [[promoCard]] · [[surface-FLP]]


---


*(type: contract · surfaces: [PDP, PLP, FLP] · status: draft)*


# breadcrumb — the Contentful walker & BreadcrumbList schema

The breadcrumb is the hierarchy signal. With flat slugs at root (no folder paths — [[g-url]]), the breadcrumb + its `BreadcrumbList` schema are the **only** structural signal of how categories nest. A single build-time Contentful walker, reused on PDP, PLP and FLP, resolves the chain. Treat as build-blocking, not cosmetic.

**Labels:** V1·BUILD ×6 (the Contentful walker, `Direct Main Category` single-ref + `parentCategory` fields, localised-name resolution + empty-name build fail, `BreadcrumbList` emission, missing-reference hard-fail for NEW pages, mobile collapse / horizontal-scroll) · V1·GUIDELINE ×4 (chain shape, leaf = H1, no-verb PDP leaf, position, canonical-taxonomy discipline — content/SEO conventions) · V2·BUILD ×1 (missing-reference + drift checks flip to hard-fail for EVERY page after the existing-page backfill — §3.17). **Surface-differing label:** the missing-reference gate is **soft-warn + legacy fallback for existing pages in V1 but hard-fails NEW pages in V1** (§3.17) — the PDP source phrases it as a flat hard build failure (`TECH·MUST·NEW·BUILD`), reconciled to the §3.17 phased gate. PDP B1 walker = `TECH·MUST·UPDATED·BUILD`; the chain-shape / leaf / no-verb rows = `MUST·UPDATED·GUIDELINE` / `MUST·NEW·GUIDELINE`; PLP B2 "breadcrumb is the hierarchy signal" = `TECH·MUST·v0.3·GUIDELINE`.

## Rule

### The walker (single resolver, build-time) `[V1·BUILD]`
- Runs at **build time, not request time**; output cached at page level. `[V1·BUILD]`
- Polymorphic input by page type:
  - **PDP (`product`):** reads the **`Direct Main Category`** reference (a **single** reference, enforced in Contentful field config — every PDP has exactly one canonical parent). `[V1·BUILD]` (PDP B1 walker `TECH·MUST·UPDATED·BUILD`; FLP OP-13 single polymorphic walker `[BUILD · V1]`)
  - **PLP / FLP (`pageHomeModular`):** reads its **`parentCategory`** (self-ref to another `pageHomeModular`); no `Direct Main Category`. `[V1·BUILD]` (PLP B2 walker)
- From the start node the walker walks each parent's `parentCategory` reference up the chain, **terminating at the locale Homepage entry** (each locale has its own dedicated Homepage entry — the chain terminus). `[V1·BUILD]`
- Output = an ordered list of `(URL, locale-localised category name)` tuples feeding **both** the visible HTML breadcrumb **and** the `BreadcrumbList` JSON-LD. `[V1·BUILD]`

### Chain shape & labels `[V1·GUIDELINE]`
- Chain mirrors the canonical taxonomy: *Home › Category › Sub-category › [leaf]*. `[V1·GUIDELINE]` (PDP b1 `MUST·UPDATED·GUIDELINE`)
- **Leaf label = the page's H1**, read from the rendered page at build time (source of truth is the H1 element in code, not a separate breadcrumb-label field) — an editorial H1 fix propagates to every breadcrumb pointing at it without a separate edit. `[V1·GUIDELINE]` (PDP b1-3 `MUST·UPDATED·GUIDELINE`)
- **PDP leaf = product name only, no print-intent verb** ("Stapled Booklets", not "Stapled Booklets Printing") — matches the verb-less PDP H1/URL ([[g-url]]). The H1 expands the leaf slightly without parroting it verbatim. `[V1·GUIDELINE]` (PDP `MUST·NEW·GUIDELINE`)
- **Locale-localised names — no English fall-throughs.** The walker reads the locale-specific name on each parent (en-GB / nl-NL / de-DE / fr-FR / es-ES / it-IT / pt-PT). The visible breadcrumb on `/nl-nl/` shows Dutch names; the `BreadcrumbList` `name` carries the same Dutch strings. **An empty localised name field on a parent fails the build** — never fall back to the English string in a non-English locale. `[V1·BUILD]` (the empty-name build-fail is a build gate; the localised-name convention is `MUST·NEW·GUIDELINE` on PDP)

### Position & schema `[MIXED]`
- **Position (PDP):** header → menu nav → **breadcrumb** → USP bar → H1. Never below the hero. (PLP/FLP order resolves on the surface DOM pages [[surface-PLP]] / [[surface-FLP]].) `[V1·GUIDELINE]` (PDP b1 position `MUST·UPDATED·GUIDELINE`)
- **`BreadcrumbList` schema emitted at build time, an exact mirror of the visible breadcrumb** — every level, labels matching the HTML exactly. **Drift = build failure** (same rule as the displayed-vs-structured-data gate in [[g-schema]]). `[V1·BUILD]` (PDP b1-5 `TECH·MUST·GUIDELINE` for the mirror rule; the drift=build-failure gate is BUILD — note PLP/FLP drift detection flips hard-fail in V2 per [[g-schema]])
- On the **PDP**, `BreadcrumbList` is a **sub-schema inside the `Product` JSON-LD** (one `Product` entity per PDP, with the `breadcrumb` field referencing the `BreadcrumbList`), not a separate top-level entity. On PLP/FLP it is a top-level entity in the v5 stack. `[V1·BUILD]` (PDP `TECH·MUST·NEW·GUIDELINE`; the emission is BUILD)

### Hard-fail gate (§3.17) `[MIXED]`
- **Hard-fail (missing-reference) is V2.** A page whose `Direct Main Category` / `parentCategory` reference is missing, or whose chain does not terminate at the locale Homepage, is a hard build failure **in V2**. `[V2·BUILD]`
- **V1 = soft-warn + legacy fallback** for existing pages (the legacy fallback breadcrumb still renders; `BreadcrumbList` drift is soft-warn). **For NEW pages in V1 the missing-reference check hard-fails** — new pages must carry a valid reference from creation. The drift + missing-reference checks flip to hard-fail for every page after the existing-page backfill sprint completes. `[V1·BUILD]` (new-page hard-fail in V1; PDP source phrases as flat `TECH·MUST·NEW·BUILD`, reconciled to §3.17 phased gate) → `[V2·BUILD]` (every-page flip).

### Canonical-taxonomy discipline (PDP edge cases) `[V1·GUIDELINE]`
- **PDPs in non-canonical contexts keep their canonical taxonomic breadcrumb.** A PDP listed inside an earned filter view (`/printing-cottonbags-black-nextday`) still breadcrumbs via its real product-tree parent (*Home › Promotional Printing › Cotton bags printing › [PDP]*), not via the filter page. Same for a themed / use-case PLP — a powerbank PDP under `/relatiegeschenken` breadcrumbs via *Corporate Gifts › Drinkware › Powerbank*, not via the theme. Earned filters and themed hubs are refinement / cross-cut views, not taxonomic parents — prevents breadcrumb explosion. `[V1·GUIDELINE]` (PDP non-canonical-context rows `TECH·MUST·NEW·GUIDELINE`)
- **FLP filter state in the breadcrumb (Approach C):** an earned filter URL renders the filter as an extra leaf (*… › Water Bottles › Aluminium*); a non-earned (query-param) state keeps the parent breadcrumb (canonical-aligned). Schema mirrors the HTML exactly per state. A **PDP** sitting under an earned filter in the FLP grid still points its parent leaf to the **base PLP**, never to the earned-filter URL (prevents filter URLs accumulating false inbound-link signal). `[V1·BUILD]` (FLP §2 Approach-C resolver is build work; the canonical-alignment discipline is GUIDELINE)
- **Non-indexable PDP variant URLs** (query-param state) inherit the canonical PDP's breadcrumb (showing the canonical leaf "Booklets", not the live config combination). `[V1·GUIDELINE]` (PDP `MUST·NEW·GUIDELINE`)

### Mobile `[V1·BUILD]`
- **PDP:** middle segments collapse visually to "…" when the chain doesn't fit one line; full chain stays in the DOM (schema unaffected). `[V1·BUILD]` (PDP mob-breadcrumb b1-19 `TECH·MUST·NEW·BUILD`)
- **PLP/FLP:** single line, `white-space:nowrap; overflow-x:auto` — never wrap to two rows, never ellipsis-truncate; all items tappable (≥ 44 px); full chain in DOM + schema regardless of which segments are scrolled out of view. `[V1·BUILD]`
- See [[g-mobile]].

## Per-surface deltas
- **PDP:** walker starts from `Direct Main Category` (single ref); leaf = product name, no verb; `BreadcrumbList` nested inside `Product` JSON-LD; mobile collapse to "…"; canonical-taxonomy discipline for filter/themed contexts.
- **PLP:** walker starts from `parentCategory`; top-level `BreadcrumbList`; breadcrumb is the primary hierarchy signal under flat URLs; mobile horizontal-scroll.
- **FLP:** same walker; Approach-C filter-state-as-leaf for earned filters only; PDP-under-filter still points to base PLP; mobile drawer / horizontal-scroll.

## V1/V2
- **V1:** walker built; `Direct Main Category` (single-ref) + `parentCategory` fields; localised-name resolution (empty localised name fails the build); `BreadcrumbList` emitted; **missing-reference hard-fail for NEW pages; soft-warn + legacy fallback for existing pages**; drift soft-warn.
- **V2:** missing-reference + drift checks flip to hard-fail for **every** page after the existing-page backfill sprint.

## Open points
- §3.17 applied: hard-fail walker = V2; V1 soft-warns existing pages (legacy fallback) but hard-fails NEW pages. The PDP source phrases missing-reference as a flat hard build failure — reconciled to the §3.17 phased gate (new pages hard-fail in V1, existing pages soft-warn until backfill).

## Sources
- PDP Req v0-34 — §B1 (walker reads `Direct Main Category`, chain to locale homepage, leaf = H1, no-verb leaf, build-time BreadcrumbList, missing-reference build failure, localised names, PDP-as-leaf, variant + non-canonical-context rules, BreadcrumbList inside Product).
- PLP Req v1-13 — §B2 (walker reads `Parent Category`, locale-localised names fail build on empty, breadcrumb = hierarchy signal, BreadcrumbList drift = build failure, V1 soft-warn + legacy fallback for existing PLPs / hard-fail new).
- FLP Req v0-15 — §2 (Approach-C filter-state leaf, PDP points to base PLP), §2b + OP-13 (single polymorphic walker, `Direct Main Category` single reference enforced).

Related: [[g-schema]] · [[g-url]] · [[g-mobile]] · [[pageHomeModular]] · [[product]] · [[surface-PDP]] · [[surface-PLP]] · [[surface-FLP]]
