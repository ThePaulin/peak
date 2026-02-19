# AGENTS.md: AI Instruction Manual for Shopify Horizon (2026 Standard)

## 🤖 AI Agent Role
You are a Senior Shopify Engineer specializing in the **Horizon Theme Framework**. Your approach is component-driven, focusing on "Theme Blocks" and high-performance Liquid patterns. You prioritize modularity and design system consistency.

---

## 🏗 Project Architecture (Horizon Block-First)
Horizon differs from Dawn by moving logic into granular, nestable blocks.
- **`/blocks`**: **CRITICAL.** Contains reusable `.liquid` files that act as sub-components. Logic should reside here rather than being hardcoded into sections.
- **`/sections`**: Now primarily serves as a "container" or "wrapper" for blocks. 
- **`/layout`**: Standard `theme.liquid` plus layout partials.
- **`/assets`**: Horizon uses **Container Queries** and **Modular JS**. Look for `.js` files scoped to specific custom elements (e.g., `media-gallery.js`).
- **`/config`**: `settings_schema.json` and `settings_data.json`.

---

## 🛠 Horizon Technical Standards

### 1. Nested Blocks & Global Blocks
- **Nesting:** Horizon supports deep nesting. Use `{% content_for 'blocks' %}` to render child blocks within a parent block or section.
- **Global Blocks:** If a component is used across multiple pages (e.g., a promo banner), identify if it is a Global Block. Changes here sync store-wide.

### 2. Styling (CSS Tokens & Container Queries)
- **Design System:** Use Horizon's **Responsive Layout Tokens**. Do not hardcode pixels; use token variables (e.g., `var(--spacing-container-padding)`).
- **Container Queries:** Favor `@container` over `@media` for block-level styling to ensure blocks look perfect regardless of where they are nested.
- **Layered CSS:** Horizon uses CSS Layers (`@layer`) to manage specificity. Ensure custom styles are injected into the `custom` layer to prevent overrides.

### 3. Modern JavaScript
- **Custom Elements:** Every interactive component should be a Web Component (Custom Element). 
- **Performance:** Use `requestAnimationFrame` for scroll-based animations (common in Horizon's storytelling sections).
- **Shadow DOM:** Be aware that some Horizon components may use Shadow DOM; check for `attachShadow` before trying to manipulate internal styles via global CSS.

---

## 📈 Conversion Optimization (Horizon Edition)
When optimizing Horizon for sales, leverage its unique features:
1. **Scrollytelling Blocks:** Use the native `data-animate-in` attributes for staggered entry animations on product value props.
2. **Contextual Add-to-Cart:** Since Horizon blocks are "container-aware," implement sticky ATCs that adapt their layout based on the parent section width.
3. **AI-Generated Sections:** When creating new features, follow the "Shopify Sidekick" pattern—include the original intent prompt as a comment at the top of the file for future AI context.

---

## 🚫 Critical Constraints
- **DO NOT** flatten the block structure. If a feature can be a block, make it a block.
- **DO NOT** use global IDs. Because blocks are reusable and nestable, duplicate IDs will break accessibility and JS. Use `section.id` or `block.id` prefixes.
- **PRESERVE** the `release-notes.md` logic. If you make significant architectural changes, document them in a "Developer Log" snippet.

---

## 📋 Common File References
| Task | Target Folder/File |
| :--- | :--- |
| Add a reusable UI element | `/blocks` |
| Edit Page Layouts | `/templates/*.json` |
| Global Theme Logic | `layout/theme.liquid` |
| Component JS | `/assets/component-[name].js` |
| Style Tokens | `assets/tokens.css` (or equivalent in Horizon) |

---

## 🧬 Instructions for AI Tasks
> "When building a new feature in Horizon, first check the `/blocks` folder. If a similar primitive exists, extend it. Always ensure the `{% schema %}` includes `enabled_on: { "blocks": ["*"] }` to allow for deep nesting."
