# Perch theme

Shopify theme for **Perch** (hbuq8y-mk.myshopify.com), a one-product store selling the Perch induction speaker stand: a Bluetooth 5.4 speaker, a folding phone and tablet stand and an RGB ambient light ring in one 482 g unit, fulfilled through CJdropshipping (SKU CJSJ312825001AZ).

The theme is a fork of Shopify Dawn 16.0.0 with a shared conversion layer and Perch-specific sections. The repository is connected to the store through Shopify's GitHub integration; pushes to `main` sync to the `stillwell-theme/main` theme in the store's theme library. The repository keeps its original name so the connection does not have to be redone.

## Design

| Scheme | Used for | Background | Text | Button | Button label |
| --- | --- | --- | --- | --- | --- |
| scheme-1 | Base, hero, FAQ | #0E1016 | #F2F0EA | #8B7CF6 | #0E1016 |
| scheme-2 | Cards, trust bar, product, footer | #161923 | #F2F0EA | #8B7CF6 | #0E1016 |
| scheme-3 | Stats band (light contrast) | #F2F0EA | #0E1016 | #0E1016 | #F2F0EA |
| scheme-4 | Newsletter | #221E3F | #F2F0EA | #F2F0EA | #0E1016 |
| scheme-5 | Announcement bar, badges | #8B7CF6 | #0E1016 | #0E1016 | #F2F0EA |

Fonts: Archivo 700 for headings, Inter 400 for body. Radii 8 to 12 px. One accent colour, violet, used sparingly.

## Perch sections

- `sections/perch-hero.liquid` + `assets/section-perch-hero.css`: full-bleed image with gradient overlay, eyebrow, headline, price-aware primary button (reads the product price), trust line.
- `sections/perch-features.liquid` + `assets/section-perch-features.css`: numbered feature cards with stroke icons from `snippets/icon-perch.liquid`; has an anchor id so the hero button can scroll to it.
- `sections/perch-scenes.liquid` + `assets/section-perch-scenes.css` + `assets/perch-scenes.js`: horizontal scroll-snap track of 3:2 scene cards (Bedside, Desk, Tablet, Any device).
- `sections/spec-sheet.liquid` + `assets/section-spec-sheet.css`: spec cards plus a "What's in the box" panel.

Shared conversion layer (identical across the three stores): `trust-bar`, `testimonials`, `comparison-table`, `stats-strip` sections, `sticky-atc` and `free-shipping-bar` snippets, `assets/cro.css`. Brand-only tweaks live in `assets/custom.css`.

## Templates

- `templates/index.json`: hero, trust bar, features (anchor `how-it-works`), featured product with buy box, scenes, spec sheet, stats, testimonials, comparison, FAQ, newsletter.
- `templates/product.json`: main product (eyebrow, title, price, buy buttons, reassurance, summary list, description, in-the-box, specs, shipping tabs), features, spec sheet, testimonials, trust bar. No related products: there is one product.
- `templates/page.faq.json`: page body plus trust bar.
- Dawn's collection, search, cart, blog and 404 templates are kept so nothing 404s, but the navigation does not link to collections.

## Images

Referenced as `shopify://shop_images/<name>` and uploaded to the store's Files: `perch-logo.png`, `perch-favicon.png`, `perch-hero-2.jpg`, `perch-scene-bedside-2.jpg`, `perch-scene-desk-2.jpg`, `perch-scene-tablet-2.jpg`, `perch-scene-devices-2.jpg`, `perch-studio-2.jpg`. All product imagery is built from the supplier's real renders (cutout composited on dark backgrounds, lifestyle shots cropped to 3:2); sources live in the workspace under `media/perch/`. Earlier AI-generated images showed the wrong product shape and were retired.

## Validation rules Shopify enforces on sync

Theme check does not catch these; a rejected file is silently dropped and the template 404s.

1. Liquid inside a text or textarea value in a JSON template may use at most one filter. Anything longer goes in a `custom_liquid` block.
2. A range setting must offer at least three values.
3. Rich text defaults in schemas and rich text values in JSON templates must start with `<p>`.

## Store checklist

- Navigation `main-menu`: Perch (product), How it works (/#how-it-works), FAQ, Contact. `footer`: FAQ, Shipping & delivery, Returns & warranty, Track your order, Contact, About.
- Pages: About, FAQ, Shipping & delivery, Returns & warranty, Track your order, Contact.
- Product `perch-speaker-stand-with-ambient-light` active, all other products archived.
- Shop policies filled in so the footer policy links render.
- Replace the example testimonials with real reviews before publishing.
