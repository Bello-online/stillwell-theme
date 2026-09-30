# Stillwell theme

Shopify theme for **Stillwell** (hbuq8y-mk.myshopify.com), a Canadian supplement brand with a short catalogue and a plain, anti-hype voice. Tagline direction: *Fewer bottles. Better ones.*

The theme is a fork of Shopify Dawn 16.0.0 with a shared conversion layer and Stillwell-specific templates, settings and styling on top. Everything a merchant can edit is in the theme editor; nothing is hard-coded into Liquid.

## Brand

- Voice: calm, evidence-led, honest. "Supports", never "cures". No countdown timers, no fake stock counters, no superlatives.
- Policies baked into the copy: free standard shipping over $60 (flat $9.95 below), 30-day returns even if opened, return shipping covered, no restocking fees, third-party tested every batch, ships from Canada.
- Canadian English, sentence case.

### Palette (config/settings_data.json, `color_schemes`)

| Scheme | Use | Background | Text | Button | Button label |
| --- | --- | --- | --- | --- | --- |
| scheme-1 | Default, light | #F7F5F0 | #1F2A24 | #2F6B4F | #FFFFFF |
| scheme-2 | Muted panel, cards | #ECE7DC | #1F2A24 | #2F6B4F | #FFFFFF |
| scheme-3 | Deep green bands, footer, announcement | #1F3D30 | #F7F5F0 | #C8A96A | #1F2A24 |
| scheme-4 | Sage (newsletter) | #DCE5DD | #1F2A24 | #1F3D30 | #F7F5F0 |
| scheme-5 | Gold accent (sale badge) | #C8A96A | #1F2A24 | #1F2A24 | #F7F5F0 |

### Type and shape

- Headings: Lora 500 (`lora_n5`), scale 105.
- Body: Raleway 400 (`raleway_n4`), scale 100.
- Buttons: radius 6, no border. Cards: standard, radius 8, no border, scheme-2. Media radius 8. Page width 1400. Cart: drawer.

## What is custom

Conversion layer (shared across our Dawn forks):

- `sections/trust-bar.liquid` - icon + heading + text strip, up to 6 items.
- `sections/testimonials.liquid` - star-rated quotes with a "verified" label.
- `sections/comparison-table.liquid` - us vs. them table, text or check marks per cell.
- `sections/stats-strip.liquid` - large-value stat band.
- `snippets/sticky-atc.liquid` + `assets/sticky-atc.js/.css` - sticky add-to-cart bar on product pages (theme setting: Conversion > Show sticky add-to-cart bar).
- `snippets/free-shipping-bar.liquid` - progress bar in the cart drawer (theme settings: Conversion > Free shipping threshold, set to 60).
- `assets/cro.css` - styles for the above. `assets/custom.css` - Stillwell brand refinements only.

Stillwell-specific custom sections (own markup and CSS, no Dawn section reuse):

- `sections/stillwell-hero.liquid` + `assets/section-stillwell-hero.css` - split editorial hero. Desktop is a 5/7 grid: text panel (eyebrow, Lora h1, short paragraph, primary + secondary button, three-item trust line with check icons) on the section colour scheme, image full-bleed to the viewport edge with a soft fade into the panel colour. Mobile stacks the image (4:3) above the text. Settings: `image`, `image_position` (left/right), `eyebrow`, `heading`, `text`, `button_label`/`button_link`, `button_label_2`/`button_link_2`, `trust_1..trust_3`, `color_scheme`, `padding_top`/`padding_bottom`. The homepage references `shopify://shop_images/stillwell-hero.jpg` from the store's Files; a placeholder SVG renders when no image is set.
- `sections/supplement-facts.liquid` + `assets/section-supplement-facts.css` - label-style facts panel with a "why it is in here" column. Semantic table (`caption`, `thead`, `scope`), zebra rows, tabular-nums amounts; stacked cards with inline labels under 750 px. Settings: `heading`, `intro`, `serving`, `servings_per`, `footnote`, `show_disclaimer`, `disclaimer`, `color_scheme`, padding. Blocks (`row`, max 16): `ingredient`, `amount`, `dv`, `why`. The `% daily value` column only renders when at least one row has a value. **Metafield fallback:** when a product template instance has no rows, the section renders the product's `custom.supplement_facts` rich text metafield instead, so the merchant can fill facts per product without editing the template. The rows in `templates/product.json` are illustrative placeholders and must be replaced with the real label (or removed so the metafield takes over).
- `sections/routine-builder.liquid` + `assets/section-routine-builder.css` - "Build a routine, not a shelf". Blocks (`slot`, max 4): `time_label`, `heading`, `text`, `collection` (card image is the collection image or its first product's image; card and button link to the collection), optional `product` shown as a "Start with:" title and price, `button_label`. Settings: `heading`, `subheading`, `color_scheme`, `card_color_scheme` (default scheme-2, top rule in the scheme's button colour), padding. Hover lift is disabled under `prefers-reduced-motion`.

Stillwell-specific:

- `config/settings_data.json` - palette, fonts, radii, cart drawer, predictive search with price, footer brand text, conversion settings. The `Stillwell` preset mirrors `current`.
- `sections/header-group.json` - single announcement message (shipping and returns), sticky header on scroll up, `main-menu`.
- `sections/footer-group.json` - brand info, `footer` menu, shipping note, newsletter, payment icons, policy links, scheme-3.
- `templates/index.json` - Stillwell hero, trust bar, routine builder, Bestsellers, shop by goal, "How we choose", stats, testimonials, comparison, FAQ, newsletter.
- `templates/product.json` - stacked gallery on the left with sticky info, eyebrow, title, price, variant buttons, quantity, buy buttons with dynamic checkout, three reassurance icons, description, three collapsible tabs, share; then supplement facts, related products, testimonials, trust bar.
- `templates/collection.json` - banner with description, 3-column grid with vertical filters and quick add, trust bar.
- `templates/page.json` and `templates/page.faq.json` - page body plus trust bar. Dawn's `main-page` cannot split a page body into accordion rows, so the FAQ page renders as normal prose; if you want an accordion FAQ, add a Collapsible content section in the editor and paste the questions in as rows.
- `.github/workflows/theme-check.yml` - runs Theme Check on push and pull request to `main`, failing on errors.

## Local development

Requires Shopify CLI 3.x or later and a staff or collaborator account on the store.

```sh
shopify theme dev --store hbuq8y-mk.myshopify.com
```

Then open the preview URL the CLI prints. `shopify theme check --fail-level error` runs the same lint as CI.

## Connecting the repo in Shopify admin

1. Push this repo to GitHub (branch `main`).
2. In Shopify admin go to **Online Store > Themes > Add theme > Connect from GitHub**.
3. Authorize the GitHub account, pick this repository and the `main` branch.
4. Shopify pulls the theme and keeps it in sync with the branch. Changes made in the theme editor are committed back to `main`, so pull before you edit locally.
5. Preview, then **Publish** when the merchant is ready.

## What the merchant still needs to add

- Logo (Theme settings > Logo) and favicon.
- Hero image for the homepage banner (the text box is dark so it reads without one, but a calm lifestyle or product photo is expected).
- Images for the three "How we choose" rows and the three collection cards (collection images are pulled from each collection).
- Real customer testimonials to replace the placeholder quotes on the homepage and product template. The placeholders are illustrative and should not go live.
- Supplement facts on every product: replace the placeholder rows in the Supplement facts section with the real label, or clear the rows and fill the `custom.supplement_facts` rich text metafield per product. The "What's in it" collapsible tab still holds a note to the merchant and can be removed once the panel is filled.
- Social links (Theme settings > Social media) and any payment methods not yet enabled at checkout.
- Confirm the `footer` menu contains FAQ, Shipping, Returns, Track order and Contact, and that shop policies are filled in so the policy links render.
