# AI Workflow Documentation — Purelane Shopify Theme Assignment

## 1. AI Tools Used
- **Antigravity AI Coding Assistant**: Powered by Google DeepMind's Gemini 3.6 Flash model. Used for structural analysis, Shopify Liquid section schema generation, CSS tokenization, vanilla JS module refactoring, and documentation drafting.
- **Ripgrep & System Tools**: Used for workspace search, file inspection, and JSON syntax validation.

---

## 2. Tasks Delegated to AI
1. **Reference Analysis**: Extracting design system tokens, typography scales, glassmorphism gradients, and animation keyframes from `purelane-homepage.html`.
2. **Boilerplate & Schema Generation**: Writing Shopify Online Store 2.0 section schemas (`sections/purelane-*.liquid`) with configurable settings, block lists, presets, and sensible defaults.
3. **Snippet Modularization**: Creating reusable snippets (`snippets/card-product-purelane.liquid` and `snippets/purelane-svg-icons.liquid`).
4. **Interactive JS Refactoring**: Converting prototype inline scripts into a modular vanilla JS file (`assets/purelane-theme.js`) with Theme Editor safety hooks.
5. **QA & Documentation**: Generating `REFERENCE_ANALYSIS.md`, `QA_CHECKLIST.md`, `ENGINEERING_NOTES.md`, and `README.md`.

---

## 3. How AI-Generated Code Was Reviewed
- **Visual Inspection**: Verified line-heights, letter-spacing, padding, border radii, and color contrast against `purelane-homepage.html`.
- **Shopify Online Store 2.0 Compatibility**: Ensured all section files contain valid JSON schemas (`{% schema %}`), proper presets, valid liquid filters (`| money`, `| image_url`), and clean section wrappers.
- **Edge Case Audit**: Checked that every product card handles sold-out inventory (`product.available == false`), missing images (`featured_image == nil`), and long product titles (line clamping).
- **Code Cleanliness**: Verified zero debug logs, zero hardcoded base64 SVGs in place of real product images, and proper accessibility attributes (`aria-hidden`, `aria-label`).

---

## 4. Where AI Initially Produced Weak or Incorrect Output
1. **Base64 SVG Duplication**: The initial AI draft attempted to copy the raw base64 SVG strings from the prototype CSS variables (`--p-dish`, `--p-kitchen`) directly into Liquid templates rather than connecting cards to dynamic Shopify product images.
2. **Hardcoded Price Strings**: Early schema defaults used raw text strings (`"₹200"`) inside product cards instead of utilizing Shopify Liquid money filters (`{{ product.price | money }}`).
3. **Brittle Global JS Listeners**: AI initially wrote global `DOMContentLoaded` event listeners without hooks for Shopify Theme Editor events (`shopify:section:load`), causing animations to break when sections were reordered or re-rendered in the customizer.

---

## 5. How Issues Were Identified & Corrected
- **Identification**: Reviewed code against Shopify Dawn architectural standards and assignment section rules (Section 7: Real Shopify Data & Section 14: Theme Editor Safety).
- **Corrections Applied**:
  - Replaced prototype base64 CSS SVGs with `snippets/card-product-purelane.liquid`, rendering `product.featured_image` dynamically with fallback SVG logic when an image is missing.
  - Implemented standard Liquid price expressions (`{{ product.price | money }}`) and compare price discount calculations.
  - Wrapped JavaScript initializations in section-scoped functions attached to both DOM readiness and `shopify:section:load` / `shopify:section:select` events.

---

## 6. Manual Engineering Judgment Applied
- **V2 Light Mode Color Tokens**: Preserved the prototype's refined light botanical palette (V2 Brand Light Mode) while adjusting accent contrast (`#b8701c`) for WCAG 2.1 AA compliance.
- **Performance vs. Visual Fidelity**: Retained the custom underwater SVG caustics filter (`#wf` fractalNoise + displacement map) but added `will-change: transform` and `prefers-reduced-motion` overrides so low-power devices and users with motion sensitivity experience fast, accessible page loads.
- **Merchant UX Design**: Structured section schemas logically with clear group headers, setting IDs, sensible defaults, and intuitive block pickers.

---

## 7. Systematized Workflow for 20 Similar Projects
If building 20 similar merchant homepages:
1. **Standardized Section Generator**: Create a CLI generator tool that converts raw HTML sections into Shopify OS 2.0 JSON schema section templates automatically.
2. **Modular Asset Layer**: Maintain a core design token library (`purelane-theme.css`) separated from Shopify functional overrides.
3. **Automated Liquid & Theme Linting**: Integrate continuous integration (CI) running `@shopify/theme-check` to catch Liquid errors and schema mismatches automatically before committing.
