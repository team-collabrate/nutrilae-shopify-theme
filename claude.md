# Nutrilae Shopify Store — Claude Code Project Instructions

Full PRD: `nutrilae-shopify-prd.md` (same repo/folder). Read it before starting any task — this file is a working summary, not a replacement.

## What this project is

Nutrilae is a new D2C retail brand selling 40 baked-goods SKUs (cakes, muffins, buns, bread) across Tamil Nadu, backed by an existing wholesale bakery. This is a **fresh retail brand and site** — the wholesale company's identity, clients, and operations must never appear on it. Reference site for layout/UX patterns: eatwholy.com (running Dawn, theme_store_id 887).

## Store & theme status

- Shopify **Basic plan**, store already created, no theme installed yet.
- **Base theme: Dawn** (confirmed as eatwholy.com's underlying theme via its `Shopify.theme` object — its visible internal label "Gokwik <> 15th April" is just a dev/app label, not a different theme).
- Fork Dawn, connect via GitHub, use Shopify CLI for local dev — standard Shopify theme workflow.

## Non-negotiable coding rules (see PRD Section 12a for full detail)

- Never edit `theme.liquid`, `password.liquid`, or anything in `layout/`. New functionality goes in a new section or snippet.
- No inline styles — each section gets its own CSS file in `assets/`, loaded via `asset_url | stylesheet_tag`. Follow Dawn's existing BEM naming.
- Every section schema setting needs a human-readable label, a realistic (non-lorem-ipsum, Nutrilae-relevant) default, and an info field where a merchant might need guidance.
- Run `shopify theme check` after every change.
- Be surgical: one change at a time, no refactors, no renamed CSS classes, no changed schema IDs unless explicitly asked.
- Before building anything new, read an existing similar file in `sections/`/`snippets/` and match its structure.

## Brand direction

- **Tone: playful & bold**, same energy as Wholy's confident, punchy voice — but Nutrilae must NOT reuse Wholy's actual colors, fonts, badge-row look, sticky-bar style, or speech-bubble callout design. Those get fresh Nutrilae-specific treatments once brand assets exist.
- **Brand assets (logo, palette, fonts) are not yet supplied — this is a blocking item.** Do not invent or lock in a palette/typography and start theming. Flag this loudly if asked to start visual/theming work before assets or an approved direction exists.
- Wholy's Dawn-native `card__badge` component and its multi-color-scheme mechanism (not its specific colors) are reasonable structural patterns to build Nutrilae's own badge/scheme system on top of.

## Product catalog

- 40 SKUs, full list with categories/sizes/prices in PRD Section 6. QSR/frozen items (samosas, rolls, sandwiches, burgers, puffs) are explicitly excluded — cakes/buns/breads/muffins only.
- **5 SKUs have no final price yet** (Brioche Bun, 3 Sandwich Breads, Sourdough) — flagged TBD in the PRD. Do not seed the catalog with placeholder/guessed prices; confirm all 40 prices first (this applies to the already-priced 35 too, per PRD Section 11).
- Each product needs: title, category, variant/size, price, placeholder image (consistent aspect ratio, alt text from title), ingredients (where available), claim badges, shelf life + storage instructions.
- Use **metafields** for claims/badges, ingredients, shelf-life, storage — not hardcoded per-page content — so they render consistently across cards, product pages, and filters.
- Claim badges (No Palm Oil, No Trans Fat, Eggless, etc.) are pulled from a wholesale sheet and **not yet confirmed accurate for Nutrilae's own formulation** — don't publish these as final marketing claims without a real confirmation step.
- Product data is store data, not theme code — GitHub→Shopify sync only pushes theme files. Catalog seeding is a separate step (CSV import via Admin, or Admin API script) that needs to happen independently of the theme build.

## Site structure

Home / Our Products (dropdown by category) / Our Story / Contact Us / Track Your Order, search + cart icons, sticky top promo bar. Homepage: promo bar → hero → category showcase → bestsellers grid → trust/claims strip → brand story teaser → testimonials (placeholder) → footer. Full homepage section list in PRD Section 4.

Product page needs: title/price/size/quantity selector, claim badge row, ingredients, shelf life/storage, image gallery, Add to Cart + Buy Now, related products (same category), optional nutrition block.

## Functional scope (v1)

In scope: category browsing/filtering, claim/badge filtering, first-order discount coupon, Track Your Order, cake customization (custom message as a cart line-item property on eligible cakes — not a variant explosion).
Not in scope for v1: wishlist, reviews display (build the component now via Judge.me even with no real reviews yet), subscriptions (build subscription-ready structure, launch later), loyalty program beyond the first-order coupon, Tamil language (English-only for v1).

## Payments & delivery

- **Razorpay, online payment only — no COD.**
- Delivery covers all of Tamil Nadu from launch, via a **hybrid model**: own fleet for near/local orders, third-party partner(s) for farther orders, split by distance. The exact distance threshold, named partner, and delivery SLA/cutoff-time logic are **still undecided — do not hardcode a specific threshold or partner**; build the pincode-checker/routing logic so these are easily configurable once decided.

## Apps & tracking (v1)

Plan for: email marketing (e.g. Klaviyo/Shopify Email), reviews (Judge.me), subscriptions (Shopify Subscriptions/Recharge), inventory sync (source system on the wholesale side not yet identified — build with a generic, sync-ready product/variant structure). Add GA4 and Meta Pixel, basic Product structured data, and per-page SEO titles/descriptions driven by product/category title.

## Open items — do not silently assume these away

1. Brand assets (logo/palette/fonts) — blocking for all visual/theming work.
2. Final retail price on all 40 SKUs (5 currently unpriced).
3. Confirmation that wholesale-sheet claim badges are accurate for Nutrilae's own formulation.
4. Delivery distance threshold, named logistics partner(s), and SLA/cutoff logic.
5. Inventory sync source system (which wholesale-side system to sync with).

When any of these blocks a specific task, say so explicitly rather than guessing a default and proceeding.
