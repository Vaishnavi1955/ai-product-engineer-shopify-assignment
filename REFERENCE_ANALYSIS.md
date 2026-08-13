# Purelane Homepage — Reference Analysis & Architectural Mapping

## Executive Summary
This document provides a comprehensive visual, structural, and technical breakdown of `purelane-homepage.html`, which serves as the primary visual source of truth for the Purelane Shopify theme implementation. The goal is to faithfully replicate the visual aesthetics, interactions, and responsive design of the prototype while refactoring its underlying static structure into a modular, production-ready Shopify Online Store 2.0 theme built upon Shopify Dawn.

---

## 1. Visual Aesthetics & Design System Tokens

### 1.1 Color Palette (Brand Light Mode - V2 Active Tokens)
The prototype implements a light, sunlit botanical aesthetic with glassmorphism and subtle background scenes:

| Token Name | Hex / Value | Usage Description |
| :--- | :--- | :--- |
| `--ink` | `#f4f0fb` | Primary page background ground color (pale lavender/mint tint) |
| `--deep` | `#e2daf3` | Secondary container depth fill |
| `--brand` | `#4b3a8f` | Primary brand deep purple/teal ink accent |
| `--brand-lt` | `#6b55b8` | Lighter brand shade |
| `--paper` | `#241a3d` | Main body text color |
| `--paper-2` | `rgba(36,26,61,0.78)` | Secondary body text & subtitles |
| `--paper-3` | `rgba(36,26,61,0.56)` | Muted copy & fine labels |
| `--accent` | `#b8701c` | Secondary warm amber accent (darkened for light contrast) |
| `--accent-2` | `#c9761d` | Bright leaf/amber accent for badges, dots, and highlights |
| `--surface` | `#17102b` | Primary heading text color |
| `--g-bg` | `linear-gradient(158deg, rgba(255,255,255,.80), rgba(236,230,247,.56) 58%, rgba(222,212,240,.50))` | Glass card gradient fill |
| `--g-line` | `rgba(75,58,143,0.16)` | Subtle glass border line |
| `--g-shadow` | `0 22px 54px rgba(58,44,112,.13)` | Glass card elevation shadow |
| `--g-inset` | `inset 0 1px 0 rgba(255,255,255,.92)` | Top edge glass highlight stroke |

### 1.2 Typography
- **Headings / Display**: `'Outfit'`, sans-serif (Google Fonts, weights 500, 600, 700, 800)
- **Body & Controls**: `'Inter'`, sans-serif (Google Fonts, weights 400, 500, 600, 700)

#### Scale Breakdown:
- `.d1`: `clamp(48px, 8.6vw, 112px)` — Heavy uppercase title, line-height `0.87`, letter-spacing `-0.018em`
- `.d2`: `clamp(30px, 4.6vw, 54px)` — Section heading uppercase, line-height `0.94`
- `.d3`: `clamp(21px, 2.5vw, 30px)` — Feature title, weight `700`, line-height `1.04`
- `.d4`: `clamp(16px, 1.6vw, 19px)` — Subheading / badge label
- `.lede`: `clamp(15px, 1.35vw, 17.5px)` — Subtitle prose max-width `44ch`
- `.kicker`: `11px`, weight `700`, letter-spacing `0.22em`, uppercase

### 1.3 Layout & Spacing System
- Max Container Width (`--maxw`): `1180px` centered with `18px` side padding (`0 14px` on mobile)
- Border Radius (`--r`): `26px` for primary glass cards; `16px` (`--r-sm`) for sub-cards; `999px` for buttons & pills
- Section Vertical Rhythm (`--sec-y`): `34px` on desktop, `22px` below 760px breakpoint

---

## 2. Inventory & Analysis of Homepage Sections

### Priority 0 (P0) Required Sections

#### 01. Hero Section (`purelane-hero.liquid`)
- **Visual Description**: Full-height or high-impact hero (`min-height: 100svh`) with display heading "Clean That Lasts", plant-powered badge rail, CTA buttons ("Shop now", "How it works"), and a stage showcasing single, double, and triple product arrangements (`hs1`, `hs2`, `hs3`) with interactive dots and live price tag updating dynamically (₹200 -> ₹349 -> ₹499).
- **Merchant Controls Needed**: Heading, subheading, primary button label/link, secondary button label/link, badge list (text & icon), product selections for hero carousel (1, 2, 3 products stage with prices and discount tags).

#### 02. Shop / Product Grid (`purelane-product-grid.liquid`)
- **Visual Description**: Responsive grid (`shelf` 2-column mobile, 4-column desktop) rendering product cards with image glass stage (`shot`), pill badge ("Best seller", "Top rated", "New"), title, star rating, current price, original price, discount percentage badge, and an "Add to cart" button.
- **Merchant Controls Needed**: Collection picker, products limit, grid columns count, badge customization per product (or dynamic via tags/metafields), section title & subtitle.

#### 03. Best-Selling Combos (`purelane-combos.liquid`)
- **Visual Description**: Horizontal touch-scrollable rail (`comborail`) displaying pre-built bundle cards ("Kitchen essentials", "Laundry care bundle", "Complete home bundle", etc.). Cards feature a top tray showing a 3-item product stack (+ divider icons), discount badge ("You save ₹398"), flag ("Most popular"), price comparison (₹499 vs ₹897), description, and "Shop bundle" action.
- **Merchant Controls Needed**: Section title/kicker/subtitle, collection/product selection for combos, customizable savings text, flag text, and CTA links.

#### 04. Bundles (`purelane-bundles.liquid`)
- **Visual Description**: Tiered pricing grid (`tiers` 3-column) offering 3 tiers: Starter (2 Products - ₹349), Most Popular (3 Products - ₹499), Whole Home (5 Products - ₹799). Each card displays product preview thumbnails (`tierpix`), item count, flat price per product, feature bullet points with checkmarks, and "Build this box" primary/secondary buttons.
- **Merchant Controls Needed**: Section heading, tier blocks (tier name, quantity, price, compare price, price per product label, features list, highlight/best value toggle, button label/link).

#### 05. Reviews Rail (`purelane-reviews-rail.liquid`)
- **Visual Description**: Header with aggregate rating ("4.8 from 8,000+ reviews", "Loved by 12 lakh+ homes") followed by an infinite auto-scrolling marquee rail (`revrail` / `revtrack`) featuring review glass cards with star rating, review title, body text, customer name, verified buyer checkmark, and product tag. Pauses on hover/focus.
- **Merchant Controls Needed**: Aggregate rating text & total review count, review blocks (rating, title, quote, reviewer name, product purchased, verified status).

---

### Priority 1 (P1) Supporting Sections

1. **Global Header & Navigation (`header.liquid` / `purelane-header.liquid`)**:
   - Floating glass pill navigation (`navpill glass`) with logo, main menu links, search/account/cart icons with cart badge count, and mobile burger menu toggle. Includes a fixed right-side progress dot rail (`rail`) syncing active sections on scroll.
2. **Sourced from Nature / Ingredients (`purelane-ingredients.liquid`)**:
   - 5-column grid showcasing plant ingredients (Coconut, Orange peel, Soap nut, Neem, Lemongrass) with custom SVG botanical art, title, and benefit descriptions.
3. **Pillars / How It Works (`purelane-pillars.liquid`)**:
   - 3-column glass cards ("Less scrubbing", "Clean ingredients", "Safe around everyone") with feature icons, copy, and button links.
4. **Proof & Product Rotator (`purelane-proof.liquid`)**:
   - Split layout with copy ("Tough on grime. Gentle on everything else."), circular stat rings (999.9% Germ kill, 0% Sulphates, 100% Plant based, 4.8 Rating), and an automatic product rotator card (`rot`) cycling through product images and captions.
5. **The Full Range Shelf (`purelane-full-range.liquid`)**:
   - Horizontal sliding product lineup (`rangerow`) displaying all product bottles on a single shelf with "Swipe to see the full shelf" hint.
6. **Why Bundles Beat Buying Single (`purelane-why-bundles.liquid`)**:
   - 4-column benefit grid (Save up to 45%, One flat price, Curated by experts, Free shipping always) with circular gradient icons.
7. **Bundle Categories (`purelane-bundle-categories.liquid`)**:
   - 4-column image card grid linking to Kitchen, Bathroom, Laundry, and Hard Water bundles.
8. **Trust Bar (`purelane-trust-bar.liquid`)**:
   - 4-column trust feature bar (Plant derived formulas, Recyclable packaging, Safe for kids & pets, Made in India).
9. **Newsletter Signup (`purelane-newsletter.liquid`)**:
   - Glass card with offer "Get ₹100 off your first bundle", email input, and submit button.
10. **Footer & Mobile Sticky CTA (`footer.liquid` / `purelane-sticky-cta.liquid`)**:
    - Multi-column footer with brand statement, quick links, contact info, copyright, and mobile fixed bottom bar ("Pick any 3, pay ₹499" CTA).

---

## 3. Interactive Behaviors & Motion Specifications

1. **Background Scenes & Ambient Water Caustics**:
   - Fixed background container (`.scenes`) with linear gradient depth layers (`s1`-`s4`) crossfading seamlessly based on scroll depth (`data-scene="1"` through `4`).
   - SVG water caustics overlay (`.water`) utilizing dual `<feTurbulence>` & `<feDisplacementMap>` filters for organic liquid lighting. Driven by subtle parallax script listening to scroll & mousemove.
   - Prefers-reduced-motion check disables transform animations and forces opacity to 1 instantly.
2. **Scroll Reveal (`.rv`)**:
   - Elements start at `opacity: 0`, `transform: translateY(30px)`, `filter: blur(7px)`.
   - IntersectionObserver triggers `.rv.in` adding smooth reveal transition with staggered delays (`.rv-d1` through `.rv-d5`).
3. **Hero Stage Carousel**:
   - Auto-rotates every 3.8s between 1, 2, and 3 product configurations.
   - Updates price tag (`ptag`) smoothly. Pauses on hover or when out of viewport.
4. **Infinite Reviews Marquee**:
   - CSS animation `marq 52s linear infinite` looping duplicated review track seamlessly. Pauses on `:hover` and `:focus-within`.

---

## 4. Technical Refactoring: Prototype vs. Shopify Native Architecture

| Prototype Implementation (Do NOT Copy) | Shopify Native Production Architecture (Implement) |
| :--- | :--- |
| Hardcoded base64 inline SVG strings for product bottles (`--p-dish`, `--p-kitchen`, etc.) | Real Shopify `product.featured_image` & `image_url` output with responsive `srcset` |
| Static SVG code inside product cards (`shot svg`) | Standard Liquid product card snippet (`snippets/card-product.liquid`) accepting dynamic `product` objects |
| Hardcoded HTML product titles, ratings, and prices (`₹200`, `₹299`) | Liquid dynamic attributes (`product.title`, `product.price \| money`, `product.compare_at_price \| money`, `product.metafields.reviews.rating`) |
| Massive 1700-line single static HTML file | Modular Shopify Online Store 2.0 JSON templates (`templates/index.json`) & reusable sections (`sections/purelane-*.liquid`) |
| Unscoped global JavaScript event listeners | Section-scoped vanilla JS modules initializing cleanly and remaining robust during Shopify Theme Editor reorders/re-renders |
| Hardcoded button links (`href="#shop"`) | Shopify Theme Editor setting URL pickers (`type": "url"`) |
