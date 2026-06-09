# Batch 1 — Claude Design **agent‑build prompt pack** · DA‑1 blocks + DA‑2 PLP pages

This supersedes the v1 summary brief **for building**. It is written to be **executed by an agent in Claude Design**: paste the **Setup prompt** once to establish the design system + output contract, then run one **build prompt** per canvas. Attach the reference assets so the agent grounds in real code, not guesses.

**Attach to the Claude Design session (if it accepts files):**
- `colors_and_type.css` — the design tokens (also inlined in Setup).
- `HelloPrint-Block-Design-Gallery.html` — visual mock of every block × variation. Each build prompt says which `#blk-…` to start from.
- `ui_kits/website/<Component>.jsx` — the existing component to match/extend (named per prompt).
- `HelloPrint-Page-Content-Model-COMPLETE.md` — the spec (field models + behaviour).

---

## ▶ SETUP PROMPT (paste once per session, or prepend to each build prompt)

```
You are building production-fidelity UI for the HelloPrint storefront in Claude Design.
OUTPUT: one self-contained, responsive HTML page per canvas — inline <style>, Inter from Google Fonts,
and only minimal vanilla JS for tab/accordion/carousel/show-more toggles. No external libraries.

DESIGN SYSTEM — use verbatim; never invent sizes or colours:
:root{
  --font-sans:"Inter",system-ui,-apple-system,"Segoe UI",Roboto,sans-serif;
  --fs-h1:32px;--lh-h1:40px; --fs-h2:28px;--lh-h2:36px; --fs-h3:20px;--lh-h3:28px;
  --fs-body:16px;--lh-body:26px; --fs-sm:14px;--lh-sm:20px; --fs-xs:12px;--lh-xs:16px; --fs-micro:10px;--lh-micro:14px;
  --color-primary:#008539; --color-primary-dark:#006B2D; --color-primary-light:#00A651;
  --color-ink:#191919; --color-ink-muted:#333; --color-ink-faint:#555;
  --color-surface:#fff; --color-surface-muted:#f8f8f8; --color-border:#e5e5e5;
  --color-trustpilot:#00b67a; --color-danger:#d32f2f;
  --color-badge-teal:#00897b; --color-badge-olive:#7cb342; --color-badge-success-bg:#e8f5e9;
  --accent-400:#f59e0b;
  --radius-card:12px; --radius-card-lg:16px; --radius-pill:9999px;
  --shadow-card:0 1px 2px 0 rgb(0 0 0/.05); --shadow-card-hover:0 10px 15px -3px rgb(0 0 0/.1),0 4px 6px -4px rgb(0 0 0/.1);
  --section-py:48px; --container-wide:1340px; --header-bg:#191919;
}
TYPE: H1 32/40 w700 (-0.01em) · H2 28/36 w700 · H3 20/28 w700 · body 16/26 · sm 14/20 · xs 12/16 · micro 10/14.
BUTTONS: pill (radius 9999), padding .625rem 1.5rem, weight 600 — primary = green #008539 (hover #006B2D); secondary = white + 1px #e5e5e5.
CARDS radius 12 (lg 16). INPUTS radius 8, border #d9d9d9, focus ring #008539. CONTAINER 1340; section padding 48 (lg 64).

OUTPUT CONTRACT — every canvas:
- Two frames: DESKTOP (1340 wide) and MOBILE (390 wide), each labelled.
- Draw EVERY listed state/variant stacked, each with a small caption above it.
- Images = grey placeholder wells (#f0f0f0, 1px #e8e8e8, centred label + aspect ratio).
- Links = real <a> (green, underline on hover). Buttons = <button>. Use the EXACT heading tags specified (SEO-critical) — do not swap a styled <span> for an <h2> or vice-versa.
- SSR-shaped: ALL content in the initial DOM. "Show more"/accordion/tab hide visually only (never remove from DOM).
- A11y: visible focus ring (2px #008539), aria-current/aria-pressed/aria-expanded where noted, ≥44px touch targets on mobile.
- Brand name = {{shop_name}} placeholder (never hardcode "Helloprint").
```

---

## ▶ DA‑1 — shared block build prompts

### D1 · card‑label
```
Build the card-label badge. (Setup design system applies.)
START FROM: gallery #blk-cardlabel; match component-badges.html (.badge pill: font xs/12 w500, radius 9999, padding .25rem .5rem, optional leading icon).
STATES (draw all):
  1 Default — white fill, 1px #e5e5e5 border, ink text — "More info"
  2 Primary — fill #008539, white text — "Most Popular"
  3 Design — fill #00897b, white text — "Design service"   [⚠ spec text says #67A5B1; use #00897b unless told otherwise]
  4 Eco — fill #7cb342, white text — "Eco"
  5 Sale — Primary style — "Sale −20%"
THEN show two tile corners: (a) PDP/related tile with 2 stacked badges (top-left, 4px gap); (b) PLP tile with exactly 1 badge (the PLP max-1 rule).
DONE-WHEN: 4 colours + Sale + the 2-badge vs 1-badge tile treatments all visible; tokens only.
```

### D2 · bundleItem — product tile  *(most reused — get this right first)*
```
Build the product tile. START FROM: gallery #blk-bundleitem; extend ui_kits/website/ProductCard.jsx + component-product-card.html.
STRUCTURE (card radius 12, 1px #e5e5e5, shadow-card, overflow hidden, whole card is ONE <a>):
  - media well 1:1 (label "1:1 product"); card-label overlay top-left (max 1 here); colour SWATCH ROW bottom-left (4 circles 16px, 2px white ring) — swatch hover swaps the image via CSS sibling, NO JS src swap;
  - body padding 10px: product NAME as <span> (sm/14 w600 — NEVER <h2>/<h3>); 2 attribute highlights (xs faint); price row — From "from £0.18" (body) OR strike was-price + now-price (danger) ; delivery line (xs faint "Tomorrow if ordered before 4pm").
STATES (draw all): default · HOVER = second image shown (lifestyle/inSettingImage — note "both images in DOM, hover ≠ lazy") · with swatches · with 1 card-label · sale (strike+now) · mobile single-image (no hover).
DATA: "Premium Business Cards", attrs "400gsm · Matte laminate", from £0.18, swatches white/black/kraft/blue.
RESPONSIVE: desktop tile ~300px in a grid; mobile = 2-up, single image, name+price only.
DONE-WHEN: every state drawn; tile is a single anchor; name is a <span>; two-image hover shown.
```

### D3 · contentMedia (Block S)
```
Build the editorial content/media block. START FROM: gallery #blk-contentMedia; match ui_kits/website/Sections.jsx split layout.
STRUCTURE: 50/50 two-column (text left, media right) at desktop; heading uses titleLevel (default <h2> 28/36) + rich-text body (NO tables) + a CTA pill below.
STATES (draw all): 
  1 Single — one image beside copy (+ caption xs faint ≤2 lines), one CTA below copy
  2 Pair-beside — two stacked images (~16:9 each) level with copy, one CTA below
  3 Pair-below — two images side-by-side UNDER the copy
  4 Pair + secondary CTA — image2 + ctaSecondary set → a CTA renders under EACH image
  5 Text-only — no image, reading-width (~65ch) copy
MOBILE: single column, image above copy; caption persists.
DATA: H2 "Soft-touch laminate that feels as premium as it looks", 60-word body, CTA "Discover our collection".
DONE-WHEN: 5 layouts drawn; captions present; no tables; CTA uses the shared enum label.
```

### D4 · productCollection (Block D) — grid container
```
Build the product-grid container. START FROM: gallery #blk-productcollection; match ui_kits/website/ProductListing.jsx grid region. Tiles = the D2 tile.
STRUCTURE: optional H2 title (left) + "Show all →" link (right); then a grid of tiles.
STATES (draw all): 
  1 4-per-row (portrait tiles, equal rows)
  2 Fill-to-width (mixed rows, e.g. 3 then 4)
  3 Carousel (one row, manual ‹ › arrows, stops at ends)
  4 With a promoCard cell mixed into the grid (max 1 promo among items)
  5 Hide-hover-image variant (static tiles)
MOBILE: 2-up grid; carousel = swipe.
DATA: title "Other types of business cards", 8 tiles, "Show all".
DONE-WHEN: 4 grid modes + promo-in-grid drawn; tiles reuse D2; Show-all is a real <a>.
```

### D5 · promoCard — 3 shapes + BG carousel
```
Build the promo card in all shapes. START FROM: gallery #blk-promocard.
SHAPES (draw all):
  1 Cluster — lifestyle image bg, white overlaid title+subtitle, one CTA pill, NO discount
  2 Discount — DISTINCT promo treatment (framed panel + flash badge top-right e.g. "-20%"), title, was-price strike + now-price, CTA "Shop now"  [not a product tile]
  3 Coupon — title + code chip + "Copy code" button (buttonStyle=Copy)
THEN: a BG carousel strip = 3 promo cards in a row with ‹ › arrows (the above-grid B10 slot).
backgroundDisplayOption: show one card on primary-green bg and one on full-image bg.
MOBILE: full-width stacked; carousel swipes.
DATA: "Free delivery over £50", T&Cs in subtitle, code "PRINT20".
DONE-WHEN: 3 shapes + BG carousel + both background options drawn.
```

### D6 · video — standalone block
```
Build the standalone video block. START FROM: gallery #blk-video.
STRUCTURE: 16:9 poster well + centred round play button (56px, primary fill, white triangle); optional title (H3) + description below.
STATES (draw all): poster + play (default) · autoplay-on-scroll (muted, small "muted" pill) · click-to-play · with caption/description.
NOTE on canvas: "never on product/Block-D cards". MOBILE: full-width 16:9.
DONE-WHEN: poster/play + the 3 states drawn.
```

### D7 · rich‑text‑BE — escape hatch
```
Build the rich-text escape-hatch block. START FROM gallery #blk-rich-text-BE.
STATES (draw all):
  1 Comparison table — a REAL <table> with <th scope="col"> and <th scope="row"> (e.g. Saddle-stitched / Perfect-bound / Wire-O × Pages / Durability / Cost), header row bg surface-muted, 1px #e5e5e5 borders, zebra rows, font 12.5
  2 "Which binding suits you?" — H3 + bullet list of inline <a> links
  3 Inline-link prose — a paragraph with 2–3 inline green links
Below-grid on PLP; link budget ≈5. MOBILE: table in a horizontal-scroll wrapper.
DONE-WHEN: a genuine <table> (not divs), the linked list, and prose all drawn.
```

### D8 · usp‑block‑BB — page‑specific USPs
```
Build the page-specific USP block (distinct from the 4-USP brand bar). START FROM gallery #blk-usp-block-bb.
STRUCTURE: optional H2 + subtitle; then a 3–5 item grid (4-up desktop / 2-up mobile). Each item = semantic icon (40px, primary green) + title (styled <span> w600 — NOT a heading) + description (sm, AEO phrasing, no inline links) + optional single <a>.
DATA: 4 items — "Free design check", "Next-day delivery", "B-Corp & FSC certified", "Price-match promise".
DONE-WHEN: 4-item grid on desktop+mobile; item titles are styled spans (not <h3>); icons from one semantic set.
```

### D9 · brands‑blockC — 3 display modes
```
Build the brands block in all 3 modes. START FROM gallery #blk-brands-blockc; mode 1 extends ui_kits/website/ClientLogosStrip.jsx.
MODES (draw all):
  1 Logo strip — grayscale logos in a row, colour on hover (lowest prominence)
  2 Logo directory — grid of brand cards (logo + name), each a real <a> (this mode emits ItemList)
  3 Brand spotlight — left meta (brand name H3 + description + CTA) / right media well; optional showPrices row of mini product tiles
Toggle brandIdentity (logo vs name); optional carousel. MOBILE: strip wraps; directory 2-up; spotlight stacks.
DONE-WHEN: 3 modes drawn; directory cards are anchors; partner logos decorative (no schema) unless directory.
```

### D10 · product‑list‑Z — Link Hub
```
Build the Link Hub. START FROM gallery #blk-product-list-z (.zcols multi-column pattern).
STRUCTURE: H2 + optional intro; groups in N columns; each group = H3 heading + list of real <a> (anchor text = the NAME, never the slug).
STATES (draw all): displayType=text (columned link lists, e.g. "Shop by material / size / colour / related categories") · displayType=chips (pill links) · showDescription=on (faint description under each link, row layout) · showMore=on (each group collapses to 5 with a "Show more" toggle — collapsed items stay in DOM).
MOBILE: columns 4→2→1. DONE-WHEN: text + chips + showDescription + showMore drawn; H2 + H3 headings; anchors are names.
```

### D11 · g‑pagecard — BH + BI
```
Build the shared page card in both blocks. START FROM gallery #blk-g-pagecard; BI extends ui_kits/website/CategoryGrid.jsx.
VARIANTS (draw both):
  BH (promotional) — 1 promoCard (reuse D5 cluster) + a row of 3–4 featured page cards
  BI (subcategory index) — compact grid of page cards: catalog image well + Title as ANCHOR TEXT (~38ch, NOT an <h3>); 3-up desktop / 2-up mobile
Card = real <a>; no schema; never appended to the page ItemList. DONE-WHEN: BH + BI drawn; titles are anchor text, not headings.
```

---

## ▶ DA‑2 — PLP page build prompts

### P1 · PLP category — full page  *(the master composition)*
```
Build the full PLP (category) page, desktop 1340 + mobile 390. START FROM ui_kits/website/ProductListing.jsx (breadcrumb→H1→lede→grid). NO facet rail (that's the FLP). Compose the DA-1 blocks in this exact DOM order:
  1 USP bar — 4 brand USPs + Trustpilot rating (build from TrustBar.jsx + WelcomeBanner.jsx); sticky under header; spans only (no headings); not clickable; green checks; reserve height (CLS-safe)
  2 [existing dark global header — render greyed as context, verify-only, do not rebuild]
  3 Breadcrumb — Home › Business cards (leaf = H1)
  4 H1 (32/40) "Business card printing"
  5 Intro — 2-line lede + "Show more" (full text stays in DOM); empty → omit entirely (no spacer)
  6 BG promo carousel (D5) — above the grid, does not replace it
  7 Product grid (D4 4-per-row; tiles = D2)
  8 B9 supporting content/media (D3) — renders BEFORE B8
  9 B8 reviews (UI-only; see P3)
  10 B11 blog teaser (3 article cards) · 11 B12 related products (D4 row, image+name-only tiles) · 12 below-grid editorial: usp-block-BB (D8), brands-C (D9), rich-text-BE (D7), Link Hub (D10)
  13 B13 FAQ (see P4) · 14 [B15 PM byline — V2: draw a greyed placeholder labelled "V2"] · 15 B14 SEO text (D3 text-only, bottom)
RULES: NO links above the grid; section rhythm var(--section-py) 48px; container 1340.
MOBILE 390: single column; grid 2-up; USP + header sticky; breadcrumb horizontal-scroll; no configurator/cart (tap tile → PDP).
DONE-WHEN: full DOM order rendered desktop+mobile; above/below-grid rule respected; every section reuses its DA-1 block. Feeds HEL-318/327.
```

### P2 · PLP themed/use‑case — variant (deltas only)
```
Duplicate P1 and change ONLY: breadcrumb is self-rooted (Home › Relatiegeschenken); H1 may combine 2–3 keywords ("Corporate gifts & business merchandise"); grid is a curated use-case mix; same skeleton + below-grid stack. DONE-WHEN: themed deltas shown on desktop+mobile. Feeds HEL-318.
```

### P3 · B8 reviews (PLP, UI‑only)
```
Build the PLP reviews block. START FROM component-trustpilot.html.
STRUCTURE: H2 (a secondary keyword, e.g. "Why UK businesses choose our business cards") + 3–5 category testimonial cards (avatar + name + green stars + quote + date) rendered as static SSR cards (by tagToLoad) + a company Trustpilot strip (logo + score + count + link).
RULES: NO category-level aggregate-rating schema (UI only) — note this on the canvas; ≥20-review render gate; empty state = block omitted.
MOBILE: cards carousel/stack. DONE-WHEN: strip + 3–5 cards + empty state drawn; "no schema" noted. Feeds the new B8 ticket (replaces cancelled HEL-330).
```

### P4 · B13 FAQ (PLP)
```
Build the PLP FAQ. STRUCTURE: H2 + 8–11 Q&A in a single-open accordion; H3 per question; chevron rotates (aria-expanded); FIRST item open; ALL answers stay in the DOM when collapsed (visually hidden only) for the FAQPage mirror.
DATA: 8 business-card FAQs (turnaround, file formats, finishes, min order…). MOBILE: full-width rows, ≥44px tap targets.
DONE-WHEN: accordion with first-open + all answers in DOM drawn. Feeds the new B13 ticket (replaces cancelled HEL-333).
```

### P5 · breadcrumb states (PLP)
```
Build the breadcrumb in both states. START FROM component-breadcrumbs.html.
DESKTOP: full chain Home › Category › Sub, "›" separators, links green, current = ink non-link.
MOBILE: single line, horizontal-scroll on overflow (NOT ellipsis collapse — that's the PDP rule); full chain stays in DOM + schema.
DONE-WHEN: desktop full + mobile horizontal-scroll drawn. Feeds HEL-326.
```

### P6 · B11 blog teaser + B14 SEO text (PLP)
```
B11: H2 "Flyer printing inspiration" + 3 Page-Article cards (image well 4:3 + title <span> + Summary description + real <a>); empty → omit.
B14: bottom long-form SEO text — reuse D3 text-only at reading width, with a "Show more" after ~4 lines (text stays in DOM); may include a BE comparison table.
DONE-WHEN: both drawn desktop+mobile. Feeds B11 (new) + HEL-334.
```

---

## How to run (recommended)
1. Open a Claude Design session; **attach** the 4 reference assets; **paste the Setup prompt**.
2. Run the DA‑1 prompts **D1 → D11** first (the library), then the DA‑2 prompts **P1 → P6** (P1 reuses the D‑blocks). Build the tile **D2** earliest — everything reuses it.
3. Export/share each canvas; **attach DA‑1 to the foundation epic and DA‑2/P‑prompts to PLP epic HEL‑318** so child tickets inherit the reference.

## Acceptance — every canvas is done when
- [ ] Desktop **1340** + mobile **390** frames; **all** listed states drawn with captions.
- [ ] Design‑system tokens only; exact heading tags as specified (SEO‑critical).
- [ ] Real `<a>` for links; USP bar has no headings + not clickable; "Show more"/accordion keep text in DOM.
- [ ] PLP tile = single anchor, **max 1 card‑label**, two‑image hover both in DOM, mobile single‑image.
- [ ] Empty/degraded states drawn (intro empty, reviews <20, blog none).
- [ ] `{{shop_name}}` placeholder used; canvas names the ticket(s) it feeds.

## Attach map
| Canvases | Attach to | Inherited by |
|---|---|---|
| D1–D11 | Contentful‑foundation epic | foundation children |
| P1–P6 (+ the D‑blocks they reuse) | **PLP epic HEL‑318** | HEL‑326/327/328/329/331/332/334 + new B8/B13 |

> **One reconcile before building:** card‑label **Design** colour — spec `#67A5B1` vs design‑system `#00897b`. Prompts use `#00897b`; change globally if you rule the other way.

