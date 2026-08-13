# Troopod AI Product Engineer Assignment — Purelane Shopify Theme

## Overview
This repository contains a production-oriented Shopify Online Store 2.0 implementation of the **Purelane** homepage, completed for the AI Product Engineer role at Troopod. 

The implementation transforms the primary visual source of truth (`purelane-homepage.html`) into a fully editable, accessible, performant, and responsive Shopify theme built upon a clean installation of Shopify Dawn.

---

## Objective
The primary objective of this assignment is to demonstrate:
- **Pixel Accuracy**: Reproducing the visual output, typography (`Outfit` + `Inter`), light botanical brand palette, glassmorphic UI, and ambient underwater caustics from `purelane-homepage.html`.
- **Shopify Liquid Expertise & OS 2.0 Architecture**: Refactoring prototype HTML into modular Shopify Liquid sections (`sections/purelane-*.liquid`), reusable snippets (`snippets/card-product-purelane.liquid`), and JSON templates (`templates/index.json`).
- **Merchant Editability**: Providing rich section schemas, settings, block pickers, and presets so marketing teams can edit content without touching code.
- **Edge Case Defensive Engineering**: Gracefully handling sold-out inventory, missing product images, long titles, and dynamic pricing.
- **Production Quality**: Implementing WCAG 2.1 AA accessibility, fluid responsive breakpoints (375px to 1440px+), optimized asset delivery, clean Git commit history, and transparent AI workflow documentation.

---

## Tech Stack
- **E-Commerce Platform**: Shopify Online Store 2.0
- **Base Theme Foundation**: Shopify Dawn
- **Templating**: Shopify Liquid
- **Styling**: Vanilla CSS3 (Custom Design Tokens, Glassmorphism, CSS Grid, Flexbox, Animations)
- **Logic & Interactions**: Vanilla JavaScript (ES6+, IntersectionObserver, `requestAnimationFrame`)
- **Data & Configuration**: Shopify JSON Templates & Section Schemas

> **Constraint Compliance**: Zero external JS/UI frameworks (no React, Vue, Tailwind, Bootstrap, or jQuery). Native Shopify functionality is used throughout.

---

## Implemented Sections

### Priority 0 (P0) Required Sections
1. **Hero Section (`sections/purelane-hero.liquid`)**: Display title ("Clean That Lasts"), botanical divider, badge rail, primary/secondary CTA buttons, and interactive 1 -> 2 -> 3 product stage carousel with live price tag update.
2. **Shop / Product Grid (`sections/purelane-product-grid.liquid`)**: Responsive grid (`shelf`) rendering product cards with ratings, prices, discount badges, and Add to Cart forms.
3. **Best-Selling Combos (`sections/purelane-combos.liquid`)**: Horizontal touch rail (`comborail`) displaying pre-built bundle cards, 3-product item stack, savings tags ("You save ₹398"), and flag badges.
4. **Bundles (`sections/purelane-bundles.liquid`)**: Tiered 3-card pricing grid (Starter, Most Popular, Whole Home), thumbnail rows (`tierpix`), flat unit price breakdown, and feature checkmark lists.
5. **Reviews Rail (`sections/purelane-reviews-rail.liquid`)**: Header with aggregate review statistics (4.8 rating, 8,000+ reviews, 12 lakh+ homes) and infinite auto-scrolling customer review marquee cards.

### Priority 1 (P1) Supporting Sections
6. **Header & Progress Rail (`sections/purelane-header.liquid`)**: Floating glass navigation pill with logo, menu links, search/account/cart icons, mobile menu burger, ambient background scenes/water caustics canvas, and desktop progress dot rail.
7. **Sourced from Nature (`sections/purelane-ingredients.liquid`)**: 5-column grid showcasing plant ingredients (Coconut, Orange peel, Soap nut, Neem, Lemongrass) with custom SVG botanical art.
8. **Pillars (`sections/purelane-pillars.liquid`)**: 3-column feature glass cards ("Less scrubbing", "Clean ingredients", "Safe around everyone").
9. **Proof & Product Rotator (`sections/purelane-proof.liquid`)**: Split proof section with copy, circular stat rings (99.9%, 0%, 100%, 4.8), and automatic product rotator carousel ("Why it works").
10. **Full Range Shelf (`sections/purelane-full-range.liquid`)**: Horizontal sliding lineup displaying the complete bottle shelf.
11. **Why Bundles Beat Buying Single (`sections/purelane-why-bundles.liquid`)**: 4-column value proposition grid.
12. **Bundle Categories (`sections/purelane-bundle-categories.liquid`)**: 4-column category card grid (Kitchen, Bathroom, Laundry, Hard water).
13. **Trust Bar (`sections/purelane-trust-bar.liquid`)**: 4-column feature bar (Plant derived, Recyclable, Safe for kids & pets, Made in India).
14. **Newsletter Signup (`sections/purelane-newsletter.liquid`)**: Glass card with ₹100 off offer and email signup form.
15. **Footer (`sections/purelane-footer.liquid`)**: Multi-column footer with brand copy, quick links, contact info, and copyright statement.
16. **Sticky Mobile CTA (`sections/purelane-sticky-cta.liquid`)**: Fixed bottom bar on mobile ("Pick any 3, pay ₹499").

---

## Architecture & Code Structure

```
├── assets/
│   ├── purelane-theme.css          # Purelane design tokens, glassmorphic styles & responsiveness
│   └── purelane-theme.js           # Vanilla JS for scroll reveal, scene crossfade, hero stage & rotators
├── config/
│   ├── settings_schema.json        # Shopify Theme Editor global settings schema
│   └── settings_data.json          # Theme default values
├── layout/
│   └── theme.liquid                # Master layout including purelane assets
├── sections/
│   ├── purelane-hero.liquid
│   ├── purelane-product-grid.liquid
│   ├── purelane-combos.liquid
│   ├── purelane-bundles.liquid
│   ├── purelane-reviews-rail.liquid
│   ├── purelane-header.liquid
│   ├── purelane-ingredients.liquid
│   ├── purelane-pillars.liquid
│   ├── purelane-proof.liquid
│   ├── purelane-full-range.liquid
│   ├── purelane-why-bundles.liquid
│   ├── purelane-bundle-categories.liquid
│   ├── purelane-trust-bar.liquid
│   ├── purelane-newsletter.liquid
│   ├── purelane-footer.liquid
│   └── purelane-sticky-cta.liquid
├── snippets/
│   ├── card-product-purelane.liquid # Reusable product card with edge case fallbacks
│   └── purelane-svg-icons.liquid    # Reusable SVG icon set
├── templates/
│   └── index.json                  # OS 2.0 homepage template sequence
├── REFERENCE_ANALYSIS.md           # Prototype visual analysis & architectural mapping
├── ENGINEERING_NOTES.md            # Technical improvements, performance & accessibility rationale
├── QA_CHECKLIST.md                 # Complete verification matrix across devices & edge cases
└── AI_WORKFLOW.md                  # Comprehensive AI usage, review & correction log
```

---

## Merchant Editability
Every section provides rich Shopify Theme Editor schemas (`{% schema %}`):
- **Editable Content**: Headings, subheadings, button labels, button links, banner copy, fine print, and footer legal text.
- **Dynamic Pickers**: Shopify `collection` pickers for the product grid, `product` pickers for the hero stage and combos rail, and `image_picker` for custom thumbnails.
- **Block Reordering**: Merchants can add, remove, and reorder hero badges, combo cards, pricing tiers, review cards, ingredients, and trust badges directly in the Shopify Theme Editor interface.

---

## Edge Cases Handling
1. **Sold-Out Product (`available == false`)**: Renders a "Sold out" badge, disables the "Add to cart" button, and prevents checkout submission.
2. **Missing Product Image**: Displays a clean, styled SVG bottle fallback image so grid geometry never collapses.
3. **Long Product Titles**: Clamped using `-webkit-line-clamp: 2` and truncated at 60 characters to prevent height blowout.
4. **Varied Pricing**: Price output uses Shopify Liquid `money` filters and computes discount percentages dynamically.

---

## Responsive Design
- Supported Breakpoints: **375px**, **390px**, **414px**, **768px**, **1024px**, **1280px**, **1440px+**.
- Mobile Optimizations: Touch-scrollable combo rail, mobile badge strip, compressed section vertical rhythm (`--sec-y: 22px`), 2-column product grid, and fixed bottom sticky CTA bar.

---

## Accessibility & Performance
- **Accessibility**: Full semantic HTML5 tags (`<header>`, `<main>`, `<section>`, `<article>`, `<nav>`, `<footer>`), visible focus rings (`:focus-visible`), informative alt text, AAA/AA color contrast, and `@media(prefers-reduced-motion: reduce)` overrides disabling all marquee keyframe animations and water caustics drift.
- **Performance**: Zero external UI framework bloat, lazy-loaded images (`loading="lazy"`), explicit `aspect-ratio` containers to prevent Cumulative Layout Shift (CLS), and hardware-accelerated CSS transforms.

---

## AI Workflow
AI was utilized as an engineering accelerator for boilerplate schema generation, prototype CSS tokenization, and documentation drafting. All AI output was systematically reviewed against Shopify Dawn standards and corrected where necessary (e.g. converting hardcoded base64 SVGs into dynamic Shopify Liquid product objects and adding Theme Editor re-render event hooks).

Detailed AI workflow documentation is available in [AI_WORKFLOW.md](file:///d:/AIAssignment/AI_WORKFLOW.md).

---

## QA & Verification
Complete QA testing has been conducted across visual accuracy, responsive breakpoints, functional behavior, accessibility, and performance.

Refer to [QA_CHECKLIST.md](file:///d:/AIAssignment/QA_CHECKLIST.md) for the complete verification checklist.

---

## Assignment Notes & Technical Documentation
For in-depth explanations of technical prototype refactoring, architectural choices, Shopify Liquid decisions, performance optimizations, and accessibility details, see [ENGINEERING_NOTES.md](file:///d:/AIAssignment/ENGINEERING_NOTES.md) and [REFERENCE_ANALYSIS.md](file:///d:/AIAssignment/REFERENCE_ANALYSIS.md).
