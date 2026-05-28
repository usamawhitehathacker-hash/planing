---
inclusion: always
---

# Horizon Theme v3.5.1 — Architecture Overview

## Theme Stats

- **Version**: 3.5.1
- **Author**: Shopify (Official Premium Theme)
- **Architecture**: Shopify 2.0 (JSON templates + Sections Everywhere + Section Groups)
- **Total Files**: 419 across 8 folders

## Folder Distribution

```
horizon_theme/                    TOTAL: 419 files
│
├── layout/        (2)            0.5%   → Page wrappers (foundation)
├── templates/     (13)           3.1%   → Page definitions (12 JSON + 1 liquid)
├── sections/      (42)           10.0%  → Major visual components
├── blocks/        (91)           21.7%  → Customizer building blocks
├── snippets/      (98)           24.3%  → Reusable code pieces
├── assets/        (113)          26.7%  → CSS(3) + JS(75) + SVG(33) + JSON(1) + TS(1)
├── config/        (2)            0.5%   → Settings schema + saved data
└── locales/       (51)           12.2%  → Translations (24 storefront + 24 schema + 3 misc)
```

## Sacred Render Sequence (NEVER violate)

```
Browser Request
    ↓
layout/theme.liquid                ← Wrapper for EVERY page
    ↓
{% sections 'header-group' %}      ← header-group.json (custom + announcements + header)
    ↓
{{ content_for_layout }}            ← templates/[page].json
    ↓
sections/[section].liquid          ← Visual component
    ↓
blocks/[block].liquid              ← Component parts (private _ ya public)
    ↓
snippets/[snippet].liquid          ← Reusable utility code
    ↓
assets/ (CSS + JS + SVG)           ← Style + behavior
    ↓
config/settings_data.json          ← Merchant ki saved choices
    ↓
locales/en.default.json            ← Translations everywhere
    ↓
{% sections 'footer-group' %}      ← footer-group.json (footer + footer-utilities)
    ↓
Browser renders → Customer dekhta hai ✓
```

## House Analogy (Mental Model)

| File Type | Ghar Mein | Real Role |
|-----------|-----------|-----------|
| `layout/*.liquid` | Walls + Roof + Foundation | Page wrapper |
| `templates/*.json` | Room blueprint | Page definition |
| `sections/*.liquid` | Furniture (sofa, TV, bed) | Major visual components |
| `blocks/*.liquid` | Furniture parts (cushion, drawer) | Building units |
| `snippets/*.liquid` | Small items (cup, remote) | Reusable code |
| `assets/*.css` | Paint, wallpaper | Styling |
| `assets/*.js` | Electrical wiring | Behavior |
| `assets/*.svg` | Light fixtures | Icons |
| `config/settings_*.json` | Remote control | Merchant settings |
| `locales/*.json` | Translation book | Multi-language |

## Horizon-Specific Architecture Features

### 1. Section Groups (NEW in 2.0)
- `sections/header-group.json` — header sections (custom + header-announcements + header)
- `sections/footer-group.json` — footer sections (footer + footer-utilities)
- Called via `{% sections 'header-group' %}` in `layout/theme.liquid`
- Single source of truth for header/footer across ALL pages

### 2. Blocks in Separate Folder
**Old themes**: blocks defined inside section file (500+ lines per section)  
**Horizon**: blocks in separate `/blocks` folder — clean, organized, reusable

### 3. Public vs Private Blocks Convention
- `_filename.liquid` (underscore prefix) = **PRIVATE** — internal use, specific sections only
- `filename.liquid` (no prefix) = **PUBLIC** — merchant adds in any compatible section

### 4. Import Maps for JS
```html
<script type="importmap">
{
  "imports": {
    "@theme/component": "{{ 'component.js' | asset_url }}",
    "@theme/utilities": "{{ 'utilities.js' | asset_url }}",
    "@theme/dialog": "{{ 'dialog.js' | asset_url }}"
  }
}
</script>
```

### 5. Web Components Architecture
- All components extend `assets/component.js` base class
- Communicate via `assets/events.js` event bus
- Custom elements: `<product-form>`, `<variant-picker>`, `<cart-items>` etc.

### 6. AJAX Section Rendering API
- Used by: facets (filtering), cart updates, predictive search, infinite scroll, quick add
- `assets/morph.js` smoothly swaps DOM HTML without page flash
- `assets/section-renderer.js` handles section re-rendering

### 7. Lazy Hydration
- `assets/section-hydration.js` activates below-fold sections only when visible
- IntersectionObserver via `assets/performance.js`

### 8. CSS Custom Properties Design System
- `snippets/theme-styles-variables.liquid` generates CSS vars from `settings_data.json`
- `snippets/color-schemes.liquid` generates 6 color schemes (scheme-1 to scheme-6)
- Sections reference schemes → vars apply automatically

### 9. Scoped CSS Pattern
```css
#shopify-section-{{ section.id }} {
  /* Section-specific styles only */
}
```
- Section IDs unique → no global CSS conflicts
- Each section's CSS isolated

## 8-Layer Architecture (Top-Down Impact)

```
┌─────────────────────────────────────────────────┐
│ LAYER 1: LAYOUT (1 file controls everything)    │
│ theme.liquid                                     │
│         ↓                                        │
│ LAYER 2: SECTION GROUPS (always present)         │
│ header-group.json, footer-group.json             │
│         ↓                                        │
│ LAYER 3: TEMPLATES (page type decides)           │
│ index.json, product.json, collection.json, etc.  │
│         ↓                                        │
│ LAYER 4: SECTIONS (42 files — content units)     │
│         ↓                                        │
│ LAYER 5: BLOCKS (91 files — smallest units)      │
│         ↓                                        │
│ LAYER 6: SNIPPETS (shared utilities)             │
│ CHANGE HERE = CHANGE EVERYWHERE IT'S USED        │
│         ↓                                        │
│ LAYER 7: ASSETS (styling + behavior)             │
│         ↓                                        │
│ LAYER 8: CONFIG (merchant choices)               │
└─────────────────────────────────────────────────┘
```

**Higher layer change = wider impact**

## Critical Connection Patterns

### theme.liquid Connections (10-20+ files)
```
theme.liquid
├── LOADS → snippets/stylesheets.liquid → assets/base.css
├── LOADS → snippets/fonts.liquid
├── LOADS → snippets/scripts.liquid → all JS modules
├── LOADS → snippets/theme-styles-variables.liquid
├── LOADS → snippets/color-schemes.liquid
├── RENDERS → snippets/meta-tags.liquid (SEO)
├── RENDERS → {% sections 'header-group' %}
├── RENDERS → {{ content_for_layout }}
├── RENDERS → {% sections 'footer-group' %}
├── RENDERS → snippets/search-modal.liquid
└── RENDERS → snippets/quick-add-modal.liquid
```

### header.liquid Connections (12-15+ files)
```
header.liquid
├── BLOCKS:
│   ├── _header-logo.liquid
│   └── _header-menu.liquid
├── SNIPPETS:
│   ├── header-actions.liquid (cart, search, account)
│   ├── header-drawer.liquid (mobile menu)
│   ├── header-row.liquid (layout)
│   ├── mega-menu-list.liquid (dropdowns)
│   ├── search.liquid
│   └── localization-form.liquid
├── ASSETS:
│   ├── header.js (sticky, transparent, height)
│   ├── header-menu.js (hover, mega menu)
│   ├── header-drawer.js (mobile slide)
│   └── header-actions.js (cart click, etc.)
└── READS:
    ├── config/settings_data.json (logo, colors)
    └── shop.navigation (menu links)
```

### product-information.liquid Connections (15-20+ files)
```
product-information.liquid (MOST COMPLEX SECTION!)
├── BLOCKS (gallery side):
│   └── _product-media-gallery.liquid
├── BLOCKS (info side):
│   ├── _product-details.liquid (wrapper)
│   ├── product-title.liquid
│   ├── price.liquid
│   ├── variant-picker.liquid
│   ├── quantity.liquid
│   ├── buy-buttons.liquid (or add-to-cart.liquid)
│   ├── accelerated-checkout.liquid
│   ├── product-description.liquid
│   ├── product-inventory.liquid
│   ├── product-custom-property.liquid
│   ├── sku.liquid
│   └── review.liquid
├── SNIPPETS:
│   ├── product-information-content.liquid
│   ├── product-media-gallery-content.liquid
│   └── price.liquid + format-price.liquid
└── ASSETS:
    ├── product-form.js (form submission, AJAX)
    ├── variant-picker.js (variant change cascade)
    ├── media-gallery.js (zoom, swipe, video)
    ├── product-price.js (dynamic price update)
    ├── product-inventory.js (stock update)
    └── product-sku.js (SKU update)
```

## Performance Budget

| Metric | Target |
|--------|--------|
| Section render | <200ms |
| Image size | <200KB each (use Shopify CDN) |
| JS per section | <50KB |
| Total page FCP | <3s |
| Mobile traffic | 60-70% — test mobile FIRST |

Every 1s slower = 7% fewer conversions (Amazon research)
