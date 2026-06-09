# Batch 3 — Claude Design **agent‑build prompt pack** · PDP refresh (DA‑5)

**Reuse the Batch‑1 Setup prompt** (design system + output contract). **Context:** the PDP **already shipped** (epic HEL‑280 Done) on the *initial* design — so these canvases are **deltas against the live PDP**: re‑skin the blocks the new spec changed + add the two missing slots. They feed **PDP follow‑up tickets** (the spec deltas can't edit Done tickets), not HEL‑280 itself.

**Attach to the session:** `colors_and_type.css` · `HelloPrint-Block-Design-Gallery.html` (`#blk-b7-product-description`, `#blk-b17-pros-green`, `#blk-b14-seo-text`, `#blk-contentMedia`, `#blk-cardlabel`) · `ui_kits/website/ProductDetail.jsx` (the shipped PDP to match) · the PDP Claude Design on HEL‑280 (the *initial* reference to diff against) · `product` + `surface-PDP` from the spec.

**Two PDP rules to call out:** alt text now reads from the **Asset `Description`** (not the page title); **B17 Pros & Cons relocated to the bottom of B7** per v0.34, and **Green Claim is V2** (Pros ship V1 only).

---

## ▶ DA‑5 — PDP refresh build prompts

### R1 · card‑label on the PDP (related grid B12)
```
Build the PDP related-products row showing the NEW card-label model. (Batch-1 Setup applies.) START FROM the D2 tile + gallery #blk-cardlabel; match ui_kits/website/ProductDetail.jsx related shelf.
DELTA vs live PDP: tiles previously used the legacy 3-colour attributeLabel → now use the merged 4-colour cardLabel (Default / Primary / Design #00897b / Eco #7cb342). On the PDP/related shelf badges may stack to MAX 2 (vs PLP max 1) — show a 2-badge tile and a 1-badge tile. Alt text reads Asset.Description (note).
STRUCTURE: "Other types of [product]" H2 + a 4-tile row (reuse D2 tile).
DONE-WHEN: related row with the 4-colour model + the max-2 stacking shown; alt-source note present. Feeds PDP follow-up P2.
```

### R2 · contentMedia on the PDP (B7 description)
```
Build the PDP B7 product-description block with the NEW contentMedia capabilities. START FROM gallery #blk-contentMedia + #blk-b7-product-description; match ProductDetail.jsx description region.
DELTA: B7 keeps its existing copy (V1·KEEP) but gains the new Block-S layouts. Draw it in: Single (image beside copy) and Pair-below (two images under copy), each with caption; show the "Pros & Cons relocated to the foot of B7" block beneath (per v0.34). Tables are NOT allowed here → if a spec/comparison table is needed, note "use rich-text-BE".
DONE-WHEN: B7 with the new layouts + Pros&Cons-at-foot drawn desktop+mobile. Feeds PDP follow-up (contentMedia re-skin).
```

### R3 · B15 SEO‑text slot (the gap from cancelled HEL‑306)
```
Build the PDP B15 SEO-text block. START FROM gallery #blk-b14-seo-text; it is a contentMedia (migrated Block S) instance rendered at the PDP bottom, above the schema.
STRUCTURE: H2 + long-form body at reading width (~65ch) + "Show more" after ~4 lines (text stays in DOM). May embed a rich-text-BE comparison table.
BEHAVIOUR (note on canvas): CONDITIONAL render — only when the page clears a per-locale search-volume threshold (⚠ threshold value is an SEO-ops input, likely ≥20/mo — confirm); author-positioned. Draw two states: rendered (above threshold) and "not rendered / below threshold → block omitted".
DONE-WHEN: rendered + omitted states + show-more drawn. Feeds PDP follow-up P1 (B15 was cancelled in HEL-306).
```

### R4 · B17 in‑context USPs (Pros V1 + Green Claim V2 stub)
```
Build the PDP B17 in-context USP line. START FROM gallery #blk-b17-pros-green; ProductDetail.jsx info column.
PLACEMENT: between B4 intro and B5 configurator (info column, above the configurator).
STATES (draw all): Pros list (b17-2, V1 — 3–5 ticked pro points, green check icons); Green Claim (b17-3) as a V2 STUB clearly labelled "V2" (eco/sustainability claim row, greyed). One B17 component, not two; no standalone "Sustainable production" hero block.
DONE-WHEN: Pros list (V1) + Green Claim stub (V2-labelled) drawn in the info column; placement note present. Feeds PDP follow-up (B17).
```

### R5 · PDP delta‑overlay (placement map)
```
Build a single annotated PDP page (desktop) that places the four refreshed/added zones in context, so reviewers see WHERE each delta lands. Reuse the shipped ProductDetail.jsx layout greyed, and highlight + label only: (1) B17 in-context USPs between B4 and B5, (2) B7 description new layouts + Pros&Cons-at-foot, (3) B12 related grid with the 4-colour cardLabel, (4) B15 SEO-text slot near the bottom. Add callout pins "R1…R4" linking to the prompts above.
DONE-WHEN: one PDP overview with the 4 delta zones pinned + labelled. Feeds the PDP follow-up epic overview.
```

---

## How to run / attach
1. Reuse the **Batch‑1 Setup**; attach the assets above (esp. the **initial PDP Claude Design** to diff against).
2. Build order: **R1 → R4 → R5** (R5 composes the rest). The shared blocks (card‑label, contentMedia) are already in DA‑1 — these are PDP‑context applications.
3. **Attach the canvases to the PDP follow‑up tickets (P1–P4), not the closed HEL‑280.** R5 → the PDP follow‑up epic overview.

## Acceptance — each canvas done when
- [ ] Desktop **1340** + mobile **390**; all listed states drawn.
- [ ] Shows the **delta vs the shipped PDP**, not a from‑scratch redesign.
- [ ] card‑label uses the 4‑colour model (PDP max 2); alt‑source note (`Asset.Description`).
- [ ] B15 shows rendered **and** omitted states + the threshold note; B17 Green Claim is clearly **V2‑labelled**, Pros ship V1.
- [ ] Tokens only; real `<a>`; exact heading tags; `{{shop_name}}`.
