# Purelane Shopify Theme — Engineering Notes

## 1. Original Prototype Technical Flaws
The reference file (`purelane-homepage.html`) provided an impressive visual design, but contained several prototype-quality technical anti-patterns that are unsuitable for a production Shopify store:

1. **Monolithic Static Structure**: All markup, CSS styling, SVG assets, and inline JavaScript were bundled into a single 1700-line static HTML file without component modularity.
2. **Hardcoded Base64 CSS Product Assets**: Product images were embedded directly into CSS variables (`--p-dish`, `--p-kitchen`) as inline base64 SVG strings. This prevents merchants from uploading real product photos or pulling live inventory from Shopify.
3. **Hardcoded Mock Product Data**: Prices, titles, reviews count, and stock status were hardcoded directly in static HTML text.
4. **Unscoped Global JavaScript**: Event listeners were bound globally without handling Shopify Theme Editor section re-rendering or section-specific lifecycle events.
5. **Accessibility Gaps**: Several interactive buttons lacked explicit `aria-label` or focus states, and decorative SVG caustics lacked proper `prefers-reduced-motion` guards.

---

## 2. Production Improvements & Architecture Changes

### What I Changed:
- **Base Theme Foundation**: Integrated Shopify Dawn as the underlying theme foundation while overlaying a custom, non-destructive Purelane asset pipeline (`assets/purelane-theme.css` and `assets/purelane-theme.js`).
- **Online Store 2.0 Modularization**: Refactored the monolithic page into 15 independent, configurable sections (`sections/purelane-*.liquid`) and reusable snippets (`snippets/card-product-purelane.liquid`, `snippets/purelane-svg-icons.liquid`).
- **Dynamic Shopify Data Integration**: Connected product cards to real Shopify `product` objects, dynamic `product.price | money`, `product.featured_image`, and collection objects.
- **Robust Edge Case Fallbacks**: Designed `card-product-purelane.liquid` to handle sold-out products (`available == false`), missing images (renders clean SVG placeholder), and long product titles (line clamping).

### Why I Changed It:
- **Merchant Editability**: Marketing teams must be able to change copy, update prices, swap images, and reorder sections directly from the Shopify Theme Editor without developer intervention.
- **Production Performance & Maintainability**: Separating styles and scripts into clean, cached theme assets improves initial load speed, eliminates code duplication, and simplifies future maintenance.

---

## 3. Shopify Architecture Decisions

| Component / Section | Shopify Implementation | Rationale |
| :--- | :--- | :--- |
| **Product Card** | `snippets/card-product-purelane.liquid` | Reused across product grid, combos, and bundle sections. Keeps markup DRY and ensures consistent edge case handling. |
| **Hero Stage Carousel** | `sections/purelane-hero.liquid` | Liquid section settings for title/CTA + product pickers for 1, 2, and 3 product slides. |
| **Product Grid** | `sections/purelane-product-grid.liquid` | Connected to Shopify `collection` picker setting. Dynamically iterates `collection.products`. |
| **Combos Rail** | `sections/purelane-combos.liquid` | Section block list (`type: combo`) allowing merchants to build custom combo bundles with savings tags and product pickers. |
| **Bundles Grid** | `sections/purelane-bundles.liquid` | Section block list (`type: tier`) supporting 2, 3, and 5 product pricing tiers with customizable feature checkmarks. |
| **Reviews Rail** | `sections/purelane-reviews-rail.liquid` | Aggregate stat settings + customizable review blocks (`type: review`). |

---

## 4. Performance Engineering Decisions

1. **Image Optimization**:
   - Product images utilize dynamic `image_url` filters with responsive `srcset` (`150w`, `300w`, `450w`) and explicit `sizes` attributes.
   - All below-the-fold images specify `loading="lazy"` to minimize initial page payload.
2. **Preventing Cumulative Layout Shift (CLS)**:
   - Image wrappers specify explicit `aspect-ratio` CSS rules matching original bottle geometries, ensuring zero vertical layout shifting as images load.
3. **Optimized Motion**:
   - Complex animations (marquee, water caustics drift, scroll parallax) use hardware-accelerated CSS properties (`transform3d`, `will-change: transform`).
   - Parallax calculations in JS are throttled using `window.requestAnimationFrame`.

---

## 5. Accessibility Engineering Decisions

1. **Semantic HTML5**: Replaced generic `div` elements with proper `<header>`, `<main>`, `<section>`, `<article>`, `<nav>`, and `<footer>` elements.
2. **Keyboard Navigation & Focus**: All buttons, links, and stage dot controls feature visible high-contrast focus rings (`:focus-visible`).
3. **Motion Sensitivity**: Comprehensive `@media(prefers-reduced-motion: reduce)` rules disable keyframe animations, infinite marquees, and water caustics transforms for users with vestibular preferences.
4. **Color Contrast**: Adjusted brand leaf accent (`#b8701c`) and heading text (`#17102b`) to achieve WCAG 2.1 AA compliant contrast against pale ground (`#f4f0fb`).

---

## 6. What I Would Do With More Time
1. **Interactive Custom Bundle Builder**: Build a dynamic slide-out bundle drawer allowing users to mix and match specific products interactively into 2, 3, or 5-item boxes with live total discount calculation.
2. **Shopify Metaobjects for Ingredients**: Connect the Sourced from Nature section to Shopify Metaobjects so ingredients can be managed centrally in Shopify Admin.
3. **AJAX Cart Drawer Integration**: Connect product cards directly to Dawn's dynamic drawer cart API for instant slide-over cart feedback without page reloads.
