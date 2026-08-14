# Purelane — Shopify Theme

## Overview

This project converts the Purelane design prototype (`purelane-homepage.html`) into a production-ready Shopify Online Store 2.0 theme built on a clean Dawn foundation.

The implementation focuses on:
- Pixel-level visual fidelity to the brand design system
- Full merchant customizability via the Shopify Theme Editor
- Dynamic Shopify catalog, collection, and pricing data
- Reusable Online Store 2.0 Liquid sections and JSON templates
- Responsive layout across viewports (375px to ultra-wide)
- Accessibility, performance, and reduced-motion support
- Theme Editor lifecycle resilience and dynamic re-rendering

---

## Assignment Scope

### Required P0 Sections
1. **Hero** (`sections/purelane-hero.liquid`): Dynamic heading, subheadings, CTA links, promise badge rail, and an interactive 3-stage bottle switcher with price tags.
2. **Shop / Product Grid** (`sections/purelane-product-grid.liquid`): Dynamic product cards powered by Shopify collections with fallback catalog archetypes.
3. **Best-Selling Combos** (`sections/purelane-combos.liquid`): Multi-product combo stacks with plus separators, savings callouts, and bundle direct actions.
4. **Bundles** (`sections/purelane-bundles.liquid`): Tiered bundle builder (2, 3, and 5 bottle sets) with unit pricing and discount calculations.
5. **Reviews Rail** (`sections/purelane-reviews-rail.liquid`): Marquee customer testimonial ticker with rating summaries and verified buyer tags.

### Additional P1 Supporting Sections
- **Global Navigation & Mobile Drawer** (`sections/purelane-header.liquid`)
- **Key Ingredients Strip** (`sections/purelane-ingredients.liquid`)
- **Brand Pillars** (`sections/purelane-pillars.liquid`)
- **Social Proof & Rotator** (`sections/purelane-proof.liquid`)
- **Full Range Shelf** (`sections/purelane-full-range.liquid`)
- **Why Bundles Comparison** (`sections/purelane-why-bundles.liquid`)
- **Bundle Categories** (`sections/purelane-bundle-categories.liquid`)
- **Trust Bar** (`sections/purelane-trust-bar.liquid`)
- **Newsletter Signup** (`sections/purelane-newsletter.liquid`)
- **Footer System** (`sections/purelane-footer.liquid`)
- **Mobile Sticky CTA Bar** (`sections/purelane-sticky-cta.liquid`)

---

## Tech Stack

- **Platform**: Shopify Online Store 2.0
- **Base Theme**: Dawn (v15.0+)
- **Templating**: Liquid, JSON Templates (`index.json`, `page.*.json`, section groups)
- **Styling**: Vanilla CSS with custom properties (`assets/purelane-theme.css`)
- **Logic**: Vanilla JavaScript with Theme Editor event binding (`assets/purelane-theme.js`)
- **Data**: Native Shopify Product, Collection, Cart, and Routes Liquid APIs
- **Version Control**: Git

---

## Implementation Details

### Dynamic Catalog Integration
- Product cards in [`snippets/card-product-purelane.liquid`](file:///d:/AIAssignment/snippets/card-product-purelane.liquid) read directly from Shopify product objects: `product.title`, `product.price`, `product.compare_at_price`, `product.available`, `product.url`, and `product.featured_image`.
- Calculated discounts (`save_pct`) and review rating metafields dynamically render when catalog items are linked.
- Sold-out products display explicit status badges and disable add-to-cart triggers safely.
- Long product titles are clamped using `-webkit-line-clamp` so card layouts remain aligned.

### Image Pipeline & Botanical Vector Fallbacks
- Real Shopify product photography uses standard `image_url` and `image_tag` pipelines with responsive widths (`150, 300, 400`), explicit aspect ratios, and `loading: 'lazy'`.
- [`snippets/purelane-product-icon.liquid`](file:///d:/AIAssignment/snippets/purelane-product-icon.liquid) provides standalone inline SVG illustrations for all 14 product archetypes (`kitchen`, `tap`, `dish`, `floor`, `laundry`, `toilet`, `handwash`, `metal`, `wm`, `eraser`, etc.), guaranteeing rendering across unpopulated development stores.

### Cart & Commerce Workflows
- Add-to-cart buttons connect directly to native Shopify routes (`routes.cart_add_url`) with AJAX submission and integration into Dawn's slide-out cart drawer.
- Navigation links use dynamic route references (`routes.root_url`, `routes.all_products_collection_url`, `routes.cart_url`, `routes.search_url`).

---

## Dawn Integration

Dawn's underlying commerce infrastructure was preserved:
- Product details and variant selection templates (`templates/product.json`, `sections/main-product.liquid`)
- Collection filtering and search infrastructure (`sections/main-collection-product-grid.liquid`, `sections/main-search.liquid`)
- Cart drawer and cart page systems (`snippets/cart-drawer.liquid`, `sections/main-cart-items.liquid`)
- Customer account, authentication, and policy pages
- Predictive search scripts and accessibility helpers

Purelane section architecture and custom properties were layered cleanly over Dawn rather than rebuilding core commerce primitives from scratch.

---

## Merchant Editing (Theme Editor)

Merchants can customize the storefront directly in Shopify Theme Editor:
- **Hero**: Title lines, highlight word, body copy, CTA button labels and URLs, slide pricing, comparison amounts, and badge items.
- **Reviews Rail**: Marquee speed, aggregate rating score, review count, and individual review cards (stars, quote, author, product tag).
- **Combos & Bundles**: Custom titles, savings pills, item lists, bundle pricing, and product selection.
- **Header & Footer**: Announcement ticker toggle, brand titles, menu selections, social links, and policy links.

---

## Performance & Accessibility

- **Responsive Sizing**: Explicit `width` and `height` attributes with `aspect-ratio` to eliminate Cumulative Layout Shift (CLS).
- **Lazy Loading**: `loading: 'lazy'` for below-the-fold images and `loading: 'eager'` for the Hero product stage.
- **Reduced Motion**: Full support for `prefers-reduced-motion: reduce` in both CSS transitions and JavaScript parallax loops.
- **Keyboard Navigation**: Distinct focus rings (`:focus-visible`), standard semantic landmark tags (`<header>`, `<main>`, `<section>`, `<footer>`), and valid ARIA attributes (`aria-label`, `aria-hidden`).

---

## Theme Editor Reliability

During development, specific Theme Editor rendering edge cases were diagnosed and resolved:
1. **Stacking Context Isolation**: Moved `.scenes` canvas from `purelane-header.liquid` to the root `<body>` in `layout/theme.liquid`, preventing Dawn's `.shopify-section-group-header-group` (`z-index: 4`) from trapping main content underneath.
2. **Hero Viewport Alignment**: Centered Hero content vertically (`align-items: center`, `min-height: clamp(580px, 85svh, 840px)`) to render immediately within initial viewport height without requiring scroll.
3. **SVG Flexbox Sizing**: Replaced unconstrained `height: 100%; width: auto` with standard SVG `viewBox`, `preserveAspectRatio`, and parent aspect-ratio declarations to avoid width collapse.
4. **Lifecycle Synchronization**: Bound `shopify:section:load`, `shopify:section:select`, `shopify:section:reorder`, and `shopify:block:select` events to re-run layout routines when merchants customize sections.

---

## QA & Validation

- **Shopify Remote Compiler**: Theme pushed and compiled on remote Shopify servers with 0 Liquid syntax errors.
- **Storefront Rendering**: Verified across desktop (1366px), tablet (768px), and mobile (375px) viewports.
- **Cart & Navigation**: Verified live add-to-cart actions, cart drawer opening, and route links.
- **Theme Editor**: Verified all 16 Purelane sections load and render their copy and visuals in Shopify Customize.

---

## Project Structure

```text
├── assets/
│   ├── purelane-theme.css       # Core brand stylesheet & responsive rules
│   ├── purelane-theme.js        # Scroll reveal, rotators, and editor events
│   └── base.css                 # Dawn foundational styles
├── layout/
│   ├── theme.liquid             # Master layout with root canvas layer
│   └── password.liquid          # Password protection layout
├── sections/
│   ├── purelane-hero.liquid     # Hero section with interactive stage
│   ├── purelane-product-grid.liquid # Bestseller product shelf
│   ├── purelane-combos.liquid   # Multi-item combo stacks
│   ├── purelane-bundles.liquid  # Tiered bundle sets
│   ├── purelane-reviews-rail.liquid # Marquee testimonial ticker
│   ├── purelane-header.liquid   # Navigation bar & mobile drawer
│   ├── purelane-footer.liquid   # Footer navigation & copyright
│   └── ...                      # Additional supporting sections
├── snippets/
│   ├── purelane-product-icon.liquid # Inline botanical SVG illustrations
│   ├── purelane-svg-icons.liquid    # UI icon system
│   └── card-product-purelane.liquid # Dynamic product card component
└── templates/
    ├── index.json               # Homepage Online Store 2.0 section manifest
    ├── product.json             # Product detail template
    └── page.*.json              # Subpage templates (about, contact, policies)
```

---

## AI Workflow

- **AI Assistance**: AI tools were utilized for initial code structure scaffolding, liquid section schema generation, and exploratory test runs.
- **Engineering & Review**: Human engineering and review was required to resolve Shopify Theme Editor iframe sandboxing, stacking context layering, SVG intrinsic aspect-ratio sizing, and Dawn commerce integration.
- **Validation**: All AI-assisted code was validated against Shopify Liquid specifications, Theme Check diagnostics, and live browser rendering.

---

## Future Improvements

1. **Custom Metafields**: Integration of structured Shopify product metafields for custom ingredient breakdowns and laboratory certifications.
2. **Predictive Search Dropdown**: Direct Purelane visual styling layered onto Dawn's predictive search modal.
3. **Automated Bundle Cart API**: Server-side script integration for automated discount calculation when users bundle 3+ individual products.

---

## Local Setup

1. Clone this repository:
   ```bash
   git clone <repository-url>
   cd AIAssignment
   ```
2. Authenticate with Shopify CLI:
   ```bash
   shopify auth login --store purelane-1yyn4ybh.myshopify.com
   ```
3. Start local development server:
   ```bash
   shopify theme dev --theme 144968974387 --store purelane-1yyn4ybh.myshopify.com
   ```
4. Open the generated local preview URL (`http://127.0.0.1:9292`).

---

## Deployment

To push code changes to the development theme:
```bash
shopify theme push --theme 144968974387 --store purelane-1yyn4ybh.myshopify.com
```

To publish as the live store theme:
```bash
shopify theme publish --theme 144968974387 --store purelane-1yyn4ybh.myshopify.com
```
