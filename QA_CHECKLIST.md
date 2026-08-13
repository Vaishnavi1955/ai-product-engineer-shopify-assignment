# Purelane Shopify Theme — QA Checklist

## VISUAL PIXEL ACCURACY
- [x] **Hero Section**: Heading typography ("Clean That Lasts"), botanical rule SVG divider, badge rail, CTA buttons, and 1 -> 2 -> 3 product carousel stage with live price tag update match `purelane-homepage.html`.
- [x] **Shop / Product Grid**: 2-column mobile / 4-column desktop layout (`shelf`), glass product cards (`shot`), discount badges (`33% off`), star ratings (`★ 4.8`), and Add to Cart buttons match reference.
- [x] **Best-Selling Combos**: Horizontal touch rail (`comborail`), 3-product item stack with plus icons, savings tags ("You save ₹398"), and flag badges match reference.
- [x] **Bundles Grid**: 3-tier card pricing grid (Starter, Most popular, Whole home), thumbnail rows (`tierpix`), unit price breakdown, and feature checklists match reference.
- [x] **Reviews Rail**: Aggregate review header statistics (4.8 rating, 8,000+ reviews, 12 lakh+ homes) and infinite auto-scrolling marquee cards match reference.
- [x] **Typography**: Google Fonts `'Outfit'` (800 display, 700 headings) and `'Inter'` (400, 500, 600) applied correctly with fluid font scaling.
- [x] **Colors**: V2 Brand Light Mode tokens applied (`#f4f0fb` background, `#4b3a8f` brand ink, `#b8701c` amber accent, `#17102b` heading surface).
- [x] **Glassmorphism**: Backdrop blur (`24px`) and glass shadows (`0 22px 54px rgba(58,44,112,.13)`) match reference.

---

## RESPONSIVE BREAKPOINTS
- [x] **375px (Mobile Small)**: Tested fluid scaling, zero horizontal body overflow, 2-column product grid, touch combo rail scrolling, and sticky bottom CTA bar.
- [x] **390px (Mobile Standard)**: Verified badge strip layout, hero image aspect ratios, and compact padding (`--sec-y: 22px`).
- [x] **414px (Mobile Large)**: Verified card heights, line clamping, and text wrapping.
- [x] **768px (Tablet Portrait)**: Verified 2-to-3 column grid transitions, ingredients 5-column wrap, and header controls.
- [x] **1024px (Tablet Landscape)**: Nav menu links display, desktop progress rail hides mobile elements, side-by-side proof layout activates.
- [x] **1280px (Desktop)**: Progress dot rail on right margin, full 4-column product grid, hero 600px copy column width.
- [x] **1440px (Desktop Widescreen)**: Max container width bounded cleanly at 1180px (`--maxw`).

---

## FUNCTIONAL & SHOPIFY DATA
- [x] **Product Links**: Product card links navigate cleanly to dynamic `product.url`.
- [x] **Collection Integration**: Product grid loads dynamically from Shopify collection objects.
- [x] **Cart Action**: "Add to cart" buttons submit product variant ID via POST form / AJAX cart drawer.
- [x] **Theme Settings**: Merchant settings for titles, subheadings, prices, badges, and CTA links populate dynamically.
- [x] **Section Reordering**: Sections can be added, removed, or reordered inside Shopify Theme Editor without JS errors.
- [x] **Block Config**: Blocks can be added/removed for hero badges, combo items, bundle tiers, and reviews.

---

## REQUIRED EDGE CASES
- [x] **Sold-out Product**: Products with `available == false` display a "Sold out" pill badge, disable the button, and prevent cart submission.
- [x] **Missing Image**: Products without a featured image render a clean SVG bottle placeholder so grid layout never breaks.
- [x] **Long Title**: Titles longer than 60 characters are truncated and CSS clamped (`-webkit-line-clamp: 2`) preventing card height blowout.
- [x] **Different Prices**: Price display adapts dynamically using Shopify `money` filters and calculates exact discount percentages (`save_pct`).
- [x] **Different Images**: Dynamic `srcset` generates responsive image sizes (`150w`, `300w`, `450w`).
- [x] **Empty/Optional Content**: Sections render graceful default presets if section settings or blocks are empty.

---

## ACCESSIBILITY (WCAG 2.1 AA)
- [x] **Keyboard Navigation**: All interactive elements (buttons, links, stage dots) receive visible focus rings (`:focus-visible`).
- [x] **Semantic HTML**: Structural elements use `<header>`, `<main>`, `<section>`, `<article>`, `<nav>`, `<footer>`, and proper `<h1>`-`<h3>` heading hierarchy.
- [x] **Alt Text**: Informative alt attributes on product images and `aria-hidden="true"` on decorative ambient SVGs.
- [x] **Reduced Motion**: Full `@media(prefers-reduced-motion: reduce)` support instantly disables marquee animations, water caustics drift, and scroll blur transitions.
- [x] **Color Contrast**: Darkened accent (`#b8701c`) and surface headings (`#17102b`) achieve AAA/AA contrast against pale ground (`#f4f0fb`).

---

## PERFORMANCE & CODE QUALITY
- [x] **Zero External Framework Dependencies**: Built strictly using Vanilla JS, CSS3, HTML5, Liquid, and Dawn architecture.
- [x] **Zero Console Errors**: Clean JS execution with event throttling via `requestAnimationFrame`.
- [x] **Asset Optimization**: CSS animations hardware-accelerated (`transform3d`, `will-change`); images lazy loaded (`loading="lazy"`).
- [x] **No Layout Shifts**: Containers specify explicit aspect ratios (`aspect-ratio: 0.6387`) preventing cumulative layout shift (CLS).
