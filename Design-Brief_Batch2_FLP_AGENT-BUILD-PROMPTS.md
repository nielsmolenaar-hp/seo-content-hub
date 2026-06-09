# Batch 2 — Claude Design **agent‑build prompt pack** · FLP filter chrome (DA‑3 + DA‑4)

Same machinery as Batch 1: **reuse the Batch‑1 Setup prompt** (design system + output contract) — paste it once, then run the prompts below. The FLP **page itself is a PLP** (build P1 from Batch 1 and drop these in); the prompts here are the **filter‑specific chrome** + the AZ authoring tool.

**Attach to the session:** `colors_and_type.css` · `HelloPrint-Block-Design-Gallery.html` (`#blk-filter-engine-az`) · **`ui_kits/website/DrinkwareFacets.jsx`** (FacetSection · FacetRow · ColorFacet · AppliedChips · DrinkwareSearch — the real facet widgets to extend) · `ui_kits/website/DrinkwarePLP.jsx` (facet+grid page layout) · `filter-engine-AZ` + `surface-FLP` from the spec.

**Two FLP rules that shape these designs (call out on every canvas):**
- **Destination‑only indexation → the five‑state facet contract:** a facet value renders as **(a)** a real `<a>` when it's an *earned* indexable filter (its own page), **(b)** a `<button>` when selectable but not earned (client `pushState`, query‑param URL, no page identity), **(c)** a `<span aria-disabled="true">` when its count is **0**, **(d)** a **loading** skeleton while facets resolve from the catalogue API, **(e)** a **selected** state (checked / ring) that also shows as a chip in F2.
- **DOM order on FLP is B8 reviews → B9 supporting** (the reverse of the PLP). Perf budget is looser (LCP ≤2.5s); F2 uses `position:sticky` (not fixed). **AZ build is gated on the Merchant‑Catalogue API contract** — note it; the *design* is not blocked.

---

## ▶ DA‑3 — FLP filter chrome build prompts

### F1 · filter panel — all five states
```
Build the FLP left-rail filter panel. (Batch-1 Setup applies.) START FROM ui_kits/website/DrinkwareFacets.jsx (FacetSection, FacetRow, ColorFacet) + gallery #blk-filter-engine-az.
STRUCTURE: a 260px left rail of collapsible FacetSections. Each section = uppercase title (13/700, letter-spacing .04em) + count + optional "Clear" + chevron (aria-expanded). Section body = rows.
FACET TYPES (draw each): checkbox list with right-aligned count (e.g. Material, Type); colour swatch grid (28px circles, selected = ring #008539 + check); price buckets; "Show more" toggle when >6 values (collapsed values stay in DOM).
FIVE VALUE STATES — draw all, clearly labelled:
  a EARNED  → real <a href="/printed-water-bottles-aluminium"> (this facet is its own indexable page)
  b NON-EARNED → <button> (selectable; updates query URL via pushState; no page identity)
  c ZERO-RESULT → <span aria-disabled="true"> greyed, count 0, not clickable
  d LOADING → 5 skeleton shimmer rows (facets resolving from catalogue API)
  e SELECTED → checked row / filled swatch ring (also appears as a chip in F2)
MOBILE 390: panel becomes a full-screen drawer opened by a "Filters (3)" button; sticky "Show N results" footer button.
DONE-WHEN: collapsible sections + checkbox/colour/price facets + ALL FIVE value states + show-more + mobile drawer drawn. Note "store keys, resolve labels live" + the API gate. Feeds the FLP F1 ticket.
```

### F2 · controls strip + applied chips
```
Build the FLP results controls strip. START FROM ui_kits/website/DrinkwareFacets.jsx → AppliedChips.
STRUCTURE (full-width bar above the grid, becomes sticky-compressed on scroll):
  - left: result count "248 products"
  - centre: AppliedChips — each active filter as a pill (green-tint bg, label "Material: Aluminium", X button) + a "Clear all" text button
  - right: Sort dropdown (Relevance / Price ↑ / Price ↓ / Bestselling / Newest) + per-page selector (24 / 48 / 96)
STATES (draw all): no filters (chips row hidden, just count + sort) · with 3 chips · sticky-compressed (shorter bar, count + sort only, chips collapse to "3 filters ▾").
MOBILE: count + "Filters (3)" button (opens F1 drawer) + sort icon; chips scroll horizontally.
DONE-WHEN: chips + clear-all + sort + per-page + sticky-compressed + mobile drawn. Feeds the FLP F2 ticket.
```

### F3 + F4 · pagination / load‑more + empty state
```
Build two canvases.
F3 PAGINATION: a "Load more" primary-pill button (centred) under the grid, with a result-progress line "Showing 48 of 248"; BELOW it a crawlable numbered page graph (‹ 1 2 3 … 6 ›) as real <a> links. Note on canvas: "pages 2+ = noindex,follow; page 1 keeps ItemList".
F4 EMPTY STATE: HTTP 200 page (parent chrome stays) — centred illustration well + "No products match these filters" + a single "Clear all filters" primary button + 3–4 suggested popular categories as <a> chips. Note: "200 not 404; keeps breadcrumb + intro".
MOBILE: both full-width. DONE-WHEN: load-more + numbered graph + empty state drawn with the index notes. Feeds the FLP F3/F4 tickets.
```

### B2b · category taxonomy tree
```
Build the FLP category taxonomy tree (FLP-only, left rail above F1). START FROM gallery #blk-filter-engine-az (tree mock).
STRUCTURE: path-aware accordion scoped to the CURRENT L1 bucket only. Levels indent; current node bold + ink; ancestors are links; siblings + children are real <a>. Expanded branch on the current path; other branches collapsed (CSS-hidden, NOT lazy — all branch URLs in the initial SSR DOM). Chevrons rotate (aria-expanded). No SiteNavigationElement schema (note).
STATES: collapsed (only L1 + current path) · expanded current branch · a deep path (L1›L2›L3 current).
MOBILE: collapses into the filter drawer as the first section.
DONE-WHEN: path-aware accordion with all branches as crawlable anchors in DOM drawn. Feeds the FLP B2b ticket.
```

### FLP‑PAGE · integrated filter listing page
```
Build the full FLP page = the PLP (Batch-1 P1) + filter chrome. START FROM ui_kits/website/DrinkwarePLP.jsx + Batch-1 P1.
LAYOUT (desktop 1340): USP bar → header(greyed) → breadcrumb (earned filter = extra leaf) → H1 (bare-noun category, e.g. "Printed water bottles") → intro → F2 controls strip → [ left rail: B2b tree + F1 panel | right: product grid (D2 tiles) ] → F3 load-more → below-grid editorial in FLP order: **B8 reviews BEFORE B9 supporting** → B11 → B12 → B13 FAQ → B14 SEO text.
MOBILE 390: H1+intro, "Filters (n)" + Sort row, grid 2-up, F1+B2b in a drawer; below-grid stacks.
NOTE: looser perf budget (LCP ≤2.5s); F2 position:sticky; cache = whole-page + VAT-toggle key.
DONE-WHEN: integrated facet-rail + grid + FLP-ordered below-grid drawn desktop+mobile. Feeds the FLP page ticket (under HEL-318).
```

### EARNED · earned‑filter destination page
```
Build an earned-filter destination page (a curated, indexable filter view). It is a normal PLP/FLP whose URL is the filter (e.g. /printed-water-bottles-aluminium).
DELTAS vs the base FLP: breadcrumb adds the filter as a LEAF (Approach C: Home › Drinkware › Water bottles › Aluminium); H1 + intro are HAND-AUTHORED for the earned filter ("Aluminium water bottles"); the matching F1 facet shows as SELECTED + as a chip; self-canonical, index,follow (note on canvas).
DONE-WHEN: filter-as-leaf breadcrumb + bespoke H1/intro + pre-selected facet state drawn. Feeds the earned-filter routing ticket.
```

---

## ▶ DA‑4 — AZ Contentful editor app (internal authoring tool)

### AZ‑APP · filterConfig editor
```
Build the AZ "filterConfig" custom editor app — an INTERNAL Contentful authoring UI (not a storefront page). Plain admin styling on the design system tokens; this is a form/builder, not marketing.
PANELS (draw all):
  1 Categories — key picker (chips "material:aluminium") with a "resolve preview" showing the live label/count pulled from the catalogue (note: store KEYS, resolve labels live)
  2 preFilters — server-applied AND/OR rule rows
  3 shownFilters — a reorderable list (drag handles) of facets with show/hide toggles + custom title override
  4 attributesInDescription — pick MAX 2, author-ordered (enforce the cap visually)
  5 printrunPreselected — single value picker (catalogue-validated)
  6 indexableFilters — table: [ filter combination ] → [ destination pageHomeModular (required) ] + "readability-rule slug" preview; this is the earned-filter declaration
STATE: a "catalogue API not connected" banner (the build is gated on the Merchant-Catalogue API contract) + a disabled "Resolve" button.
DONE-WHEN: all 6 config panels + the API-gate banner drawn. Feeds the AZ ticket (blocked-by the Merchant-Catalogue API contract).
```

---

## How to run / attach
1. Reuse the **Batch‑1 Setup prompt**; attach the assets listed above (esp. `DrinkwareFacets.jsx`).
2. Build order: **F1 → F2 → F3/F4 → B2b → FLP‑PAGE → EARNED → AZ‑APP**. F1 first (everything else references its five states).
3. **Attach the finished canvases to the FLP work under PLP epic HEL‑318** (FLP = a PLP extension per the scope decision) so the F1–F4 / B2b / AZ tickets inherit the reference. The AZ ticket stays **blocked‑by the Merchant‑Catalogue API contract**.

## Acceptance — each FLP canvas is done when
- [ ] Desktop **1340** + mobile **390**; all listed states drawn.
- [ ] F1 shows **all five value states** (earned `<a>` / non‑earned `<button>` / zero `<span aria-disabled>` / loading / selected).
- [ ] Earned facets are real `<a>`; non‑earned are `<button>`; zero‑result not clickable — the destination‑only indexation contract is visible.
- [ ] Below‑grid order on the FLP page is **B8 → B9** (reverse of PLP).
- [ ] AZ editor shows the **API‑gate banner**; `indexableFilters` rows require a destination.
- [ ] Tokens only; real `<a>` for all crawlable links; `{{shop_name}}` placeholder.
