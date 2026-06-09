# Batch 4 — Claude Design **agent‑build prompt pack** · V2 blocks (DA‑6)

**Reuse the Batch‑1 Setup prompt.** These are the **V2** blocks — none designed anywhere (gallery has stubs only). They're not in the V1 ship, so they feed the **V2 tickets** and are lowest priority — build after Batches 1–3. Label every canvas **"V2"**.

**Attach to the session:** `colors_and_type.css` · `HelloPrint-Block-Design-Gallery.html` (`#blk-b16-specs-matrix`, `#blk-b10-config-deepdive`, `#blk-reviews-blockP`, `#blk-b13-chat-help`, `#blk-person`) · `ui_kits/website/ProductDetail.jsx` · `ui_kits/website/WaterBottleConfigurator.jsx` · `preview/component-trustpilot.html` · `preview/component-option-picker.html`.

---

## ▶ DA‑6 — V2 block build prompts

### V1 · B16 — detailed specs matrix (PDP, V2)
```
Build the PDP B16 specs/pricing matrix (Mixam-style). (Batch-1 Setup applies.) START FROM gallery #blk-b16-specs-matrix.
STRUCTURE: a structured matrix — left column = spec attributes (Size, Paper/Material, Finish, Binding, Pages, Turnaround); top row = option columns; cells = value + price-per-unit where relevant. Scannable, zebra rows, sticky header row + sticky first column. Above it an H2; note "additionalProperty schema" (V2·BUILD) on canvas.
STATES (draw all): full matrix · a highlighted "recommended"/most-popular column · mobile = horizontal-scroll wrapper OR stacked per-option cards (draw the mobile pattern).
DATA: booklets — A4/A5/A6 × 130gsm/170gsm × matte/gloss × saddle-stitch/perfect-bound, prices per unit.
DONE-WHEN: full matrix + recommended column + mobile pattern drawn; labelled V2. Feeds the B16 ticket.
```

### V2 · B10 — configuration deep‑dive (PDP, V2)
```
Build the PDP B10 configuration deep-dive. START FROM gallery #blk-b10-config-deepdive; match ProductDetail.jsx / WaterBottleConfigurator.jsx attribute groups.
STRUCTURE: educational prose cards — ONE H3 sub-block per configurable attribute group (Paper, Size, Finish, Binding). Each card = H3 + small image well + 2–3 sentence explainer + a "which should I pick?" guidance line. Grid 2-up desktop.
STATES: card grid · one card expanded (if collapsible). MOBILE: single column stack.
DATA: Paper ("130gsm vs 170gsm — when to choose each"), Binding ("saddle-stitch vs perfect-bound"), etc.
DONE-WHEN: per-attribute-group cards with H3 + guidance drawn; labelled V2. Feeds the B10 ticket.
```

### V3 · B9 — product reviews (PDP, V2)
```
Build the PDP B9 product-level reviews. START FROM preview/component-trustpilot.html + gallery #blk-reviews-blockP.
STRUCTURE: aggregate header (large Trustpilot stars + score "4.6" + "based on 312 reviews" + logo) — PRODUCT-level (note: emits product-level AggregateRating, ≥20-review gate) — then a grid/carousel of review cards (avatar, name, green stars, "Verified" chip, quote, date) + "Load more reviews".
STATES (draw all): full (≥20 reviews) · BELOW threshold (<20) → block + schema both hidden (draw the "hidden" note). 
MOBILE: header stacks; cards carousel.
DONE-WHEN: aggregate header + cards + the <20 hidden state drawn; "product-level AggregateRating" note; labelled V2. Feeds the B9 ticket. (Distinct from the PLP B8 UI-only-tag reviews in Batch 1 P3 — this one DOES emit schema.)
```

### V4 · B13 — chat & help launcher (PDP, V2)
```
Build the PDP B13 chat & help launcher. START FROM gallery #blk-b13-chat-help.
STRUCTURE: a floating FAB bottom-right (56px, primary green, chat icon, subtle shadow); on click → a help panel (360px) with a search-help input + "Top articles" list (3–5 links) + contact options (chat / email). Note on canvas: "lazy-loaded after LCP, no SEO weight, not in initial critical DOM".
STATES (draw all): FAB collapsed · panel open. MOBILE: panel = bottom sheet, full-width.
DONE-WHEN: FAB + open panel + mobile bottom-sheet drawn; "lazy / no SEO weight" note; labelled V2. Feeds the B13 ticket.
```

### V5 · Person byline (PDP B‑PM / PLP·FLP B15, V2)
```
Build the Person authority byline (E-E-A-T test, V2 on every surface). START FROM gallery #blk-person.
STRUCTURE: a bordered card — round photo (56px) + name (sm/600) + jobTitle (xs faint) + a category-specific expertise sentence (the sentence lives on the per-page byline, not the Person entity) + LinkedIn link (rel="me") + a contact CTA. Note: emits Person schema (worksFor / knowsAbout / sameAs).
STATES (draw all): with photo · without photo (initials avatar) · PDP placement (near B7/specs) vs PLP/FLP placement (below grid). MOBILE: stacks, full-width.
DATA: "Sophie Bennett — Print Product Manager · 8 years in wide-format" + expertise sentence for business cards.
DONE-WHEN: byline card (with/without photo) + both placements drawn; schema note; labelled V2. Feeds the B-PM / B15 Person ticket.
```

---

## How to run / attach
1. Reuse the **Batch‑1 Setup**; attach the assets above.
2. Build order is independent (no shared dependency) — do them last, after V1 ships.
3. **Attach to the V2 tickets** (B16 / B10 / B9 / B13 / Person). The Person byline serves PDP **and** PLP/FLP — attach to all three V2 byline tickets.

## Acceptance — each V2 canvas done when
- [ ] Desktop **1340** + mobile **390**; all listed states drawn; canvas clearly labelled **V2**.
- [ ] B9 shows the **<20‑review hidden** state + the product‑level rating note (vs the PLP B8 UI‑only block).
- [ ] B13 carries the **"lazy / no SEO weight"** note; B16 the `additionalProperty` note; Person the schema note.
- [ ] Tokens only; real `<a>`; exact heading tags (B16/B10 use H2/H3; review/byline names are NOT headings); `{{shop_name}}`.

---

## ✅ Design proposal — full set (all 4 batches, local in `seofrontend/`)
| Batch | File | Canvases | Attaches to |
|---|---|---|---|
| 1 | `…_Batch1_AGENT-BUILD-PROMPTS.md` | Setup + D1–D11 (blocks) + P1–P6 (PLP) | Foundation epic + HEL‑318 |
| 2 | `…_Batch2_FLP_AGENT-BUILD-PROMPTS.md` | F1–F4 · B2b · FLP page · earned · AZ app | HEL‑318 (FLP extension); AZ blocked on catalogue API |
| 3 | `…_Batch3_PDP-refresh_AGENT-BUILD-PROMPTS.md` | R1–R5 (PDP deltas) | PDP follow‑up tickets (not closed HEL‑280) |
| 4 | `…_Batch4_V2_AGENT-BUILD-PROMPTS.md` | V1–V5 (V2 blocks) | V2 tickets |

Shared **Setup prompt** lives in Batch 1; Batches 2–4 reference it (no token duplication). Validation canvas: `D2_product-tile_validation-canvas.html`. **Nothing written to the brain.**
