# Submission Notes — Purelane Shopify Theme Assignment

**Candidate**: Vaishnavi Phad  
**Store**: `purelane-1yyn4ybh.myshopify.com`  
**Development Theme ID**: `144968974387`  
**Theme Name**: `Development (3e695a-Vaishnavi)`  

---

### 1. What I Built
I converted the provided Purelane HTML design prototype into a production-ready Shopify Online Store 2.0 theme built on Shopify Dawn.

Key components implemented:
- **Five Required Assignment Sections**:
  1. **Hero** (`purelane-hero.liquid`): Fully dynamic heading, subhead, CTA buttons, plant promise badge rail, and an interactive 3-stage bottle switcher with real-time price changes.
  2. **Product Grid / Shop Shelf** (`purelane-product-grid.liquid`): Bestseller cards connected to Shopify catalog objects with sale tags, reviews, and fallback handling.
  3. **Best-Selling Combos** (`purelane-combos.liquid`): Interactive combo rail featuring multi-item bottle stacks with plus icons, savings pills, and bundle links.
  4. **Bundles** (`purelane-bundles.liquid`): 2, 3, and 5 product bundle builder cards with calculated discount pricing.
  5. **Reviews Rail** (`purelane-reviews-rail.liquid`): Smooth CSS marquee testimonial track with star ratings and verified buyer tags.
- **Supporting Purelane Sections**: Header with announcement ticker & mobile drawer, Key Ingredients, Brand Pillars, Social Proof with carousel rotator, Full Range Shelf, Why Bundles comparison, Bundle Categories, Trust Bar, Newsletter, Footer, and Sticky Mobile CTA.
- **Subpage JSON Templates**: About Us (`page.about.json`), Contact (`page.contact.json`), Shipping Policy (`page.shipping.json`), Privacy Policy (`page.privacy.json`), Terms of Service (`page.terms.json`), and Refund Policy (`page.refund.json`).

---

### 2. What I Changed from the Prototype & Why
- **Modularized Static HTML into Liquid Sections**: Split monolithic HTML into reusable Online Store 2.0 sections with JSON schema settings so merchants can add, remove, and reorder sections from the Shopify Theme Editor.
- **Integrated Real Shopify Commerce Data**: Replaced hardcoded text and static numbers with native Liquid variables (`product.title`, `product.price`, `product.compare_at_price`, `product.available`, `routes.cart_add_url`, `routes.search_url`).
- **Standardized Image Architecture**: Replaced fragile base64 CSS custom properties with native Shopify CDN `image_url` / `image_tag` pipelines and created [`snippets/purelane-product-icon.liquid`](file:///d:/AIAssignment/snippets/purelane-product-icon.liquid) with inline botanical vector SVGs for fallbacks.
- **Preserved Dawn Infrastructure**: Retained Dawn's cart drawer, predictive search, product detail templates, collection templates, customer account system, and accessibility scaffolding rather than rebuilding them.

---

### 3. How Shopify Data is Handled
- **Dynamic Cards**: [`snippets/card-product-purelane.liquid`](file:///d:/AIAssignment/snippets/card-product-purelane.liquid) checks for `card_product.featured_image` and outputs responsive image tags with srcset and lazy loading. If no catalog image exists, it maps the product handle to the corresponding botanical SVG illustration.
- **Inventory & Pricing**: Sold-out products display explicit badges (`Sold out`), disable add-to-cart buttons, and compare-at prices calculate dynamic discount percentages (`% off`).
- **AJAX Cart Integration**: Product cards and bundle buttons dispatch standard POST requests to `/cart/add.js` and trigger Dawn's cart drawer to update item count and open without page reloads.

---

### 4. How Merchant Editing Works
All 16 Purelane sections include comprehensive Shopify schema settings:
- Merchants can customize headline copy, buttons, links, pricing, reviews, and promotional pills directly in Shopify Customize.
- Every section includes `presets` allowing merchants to add multiple instances or re-add sections to any Online Store 2.0 page template.

---

### 5. QA & Verification Performed
- **Shopify Remote Build**: All theme files pushed to remote Shopify servers with 0 Liquid syntax errors (`ca0b417` and `33d7087`).
- **Theme Editor Stacking & Visibility Fix**: Diagnosed and resolved the Theme Editor iframe canvas issue where fixed background layers inside header groups sat at `z-index: 4` over `<main id="MainContent">`. Content and images now render cleanly in the Theme Editor preview.
- **Responsive Layout**: Tested across desktop (1366px), tablet (768px), and mobile (375px) viewports.
- **Commerce Flows**: Tested Add to Cart, cart drawer opening, product links, and navigation routing.

---

### 6. AI Workflow
- AI tools were utilized for boilerplate liquid section generation, schema declaration mapping, and initial prototype analysis.
- Human engineering was essential for diagnosing Shopify Theme Editor iframe sandboxing, solving SVG intrinsic aspect-ratio sizing, reorganizing stacking context layers in `layout/theme.liquid`, and testing commerce workflows.
- All code was tested and verified rather than blindly trusted.

---

### 7. Known Limitations & What I Would Improve
- **Lighthouse Profiling**: Perform deeper Core Web Vitals optimizations on low-end mobile hardware.
- **Structured Metafields**: Connect custom Shopify product metafields for dynamic ingredient breakdowns and lab certifications.
- **Automated Bundle Cart API**: Server-side Shopify Functions/Scripts for automatic bundle tier discount application.

---

### 8. Deployment Status
- **Development Store**: `purelane-1yyn4ybh.myshopify.com`
- **Development Theme ID**: `144968974387`
- **Status**: Uploaded, compiled, and verified on Shopify development environment.
- **Theme Editor URL**: `https://admin.shopify.com/store/purelane-1yyn4ybh/themes/144968974387/editor`

---

### 9. GitHub Status
- **Local Branch**: `master` (All changes committed cleanly)
- **Latest Commit**: `33d7087` (`chore: finalize Purelane Shopify assignment`)
- **Remote**: Ready for remote push once repository URL is provided.
