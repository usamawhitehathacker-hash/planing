---
inclusion: always
---

# IF-THEN Cascade — Dependency Impact Reference

## Critical Files Severity Tiers

### Tier 11/10 — CATASTROPHIC (Don't Even Touch!)

| File | Result If Deleted |
|------|-------------------|
| `snippets/image.liquid` | ALL images on entire website gone |
| `layout/theme.liquid` | Site completely broken |
| `config/settings_schema.json` (invalid JSON) | Customizer crashes entirely |
| `locales/en.default.json` | All translations show raw keys |
| `sections/_blocks.liquid` | ALL block rendering fails everywhere |

### Tier 10/10 — CRITICAL (Store Stops Working)

| File | Result If Deleted |
|------|-------------------|
| `snippets/button.liquid` | ALL buttons gone |
| `assets/product-form.js` | Add to Cart DEAD = ZERO sales |
| `assets/variant-picker.js` | Wrong variants in cart |
| `assets/component-cart-items.js` | Cart broken |
| `blocks/_cart-summary.liquid` | NO checkout button = NO revenue |
| `sections/main-cart.liquid` | Cart page dead |
| `assets/header.js` | Navigation dead |
| `sections/header.liquid` | No navigation on any page |

### Tier 9/10 — HIGH IMPACT

| File | Result If Deleted |
|------|-------------------|
| `snippets/icon.liquid` | ALL SVG icons gone |
| `snippets/product-card.liquid` | 6+ sections broken |
| `assets/component.js` | All custom elements break |
| `assets/facets.js` | Collection filters dead |
| `assets/predictive-search.js` | Live search dead |
| `assets/media-gallery.js` | Product gallery broken |
| `assets/header-drawer.js` | Mobile menu dead |
| `blocks/_product-media-gallery.liquid` | Product page images gone |
| `assets/base.css` | Site looks plain ugly |

### Tier 7/10 — MEDIUM IMPACT

| File | Result If Deleted |
|------|-------------------|
| `assets/slideshow.js` | Slideshow + carousel + search resource broken |
| `assets/marquee.js` | Marquee text static |
| `assets/product-recommendations.js` | Recs don't load |
| `assets/announcement-bar.js` | Announcements static |
| `snippets/pagination-controls.liquid` | Blog + collection + search affected |
| `sections/header-group.json` | Header inconsistent across pages |
| `sections/footer-group.json` | Footer inconsistent |

### Tier 5/10 — LOW IMPACT

| File | Result If Deleted |
|------|-------------------|
| `assets/cart-note.js` | Order notes don't work |
| `assets/collection-links.js` | Scroll behavior gone |
| `assets/product-inventory.js` | Stock count stale |
| `assets/product-sku.js` | SKU stays static |
| `sections/divider.liquid` | No visual separator option |

## File Change → Cascade Impact

### Layer 1: Layout Changes (HUGE Impact)

```
IF: layout/theme.liquid changes
THEN: ALL pages affected
- Header/footer/CSS/JS load break possible
- {{ content_for_header }} removal breaks Shopify apps
- {{ content_for_layout }} removal breaks all pages
- Modulepreload removal slows entire site
```

### Layer 2: Section Group Changes

```
IF: sections/header-group.json changes
THEN: Header on ALL pages affected
- Section order changes everywhere
- Section removal hides feature site-wide

IF: sections/footer-group.json changes
THEN: Footer on ALL pages affected
- Email signup, links, social — all sites updated
```

### Layer 3: Template Changes

```
IF: templates/index.json changes
THEN: Only home page affected (template-specific)
- Add/remove sections from home only
- Block configurations specific to home

IF: templates/product.json changes
THEN: Default product layout affected
- Custom product templates (product.special.json) unaffected

IF: Section type in template wrong
THEN: "Could not find section template X" error
- Section file MUST exist with exact filename
```

### Layer 4: Section Changes

```
IF: sections/header.liquid delete
THEN: Header gone on every page
- Customer can't navigate anywhere
- Logo, search, cart, account all gone
- ZERO usability

IF: sections/product-information.liquid delete
THEN: Product page broken
- 15-20 connected blocks fail
- ZERO sales from product pages
- Most complex section in theme

IF: sections/main-cart.liquid delete
THEN: /cart page dead
- Customer can't review before checkout
- ZERO revenue (no checkout flow)

IF: sections/main-collection.liquid delete
THEN: Collection pages broken
- Filters, sorting, pagination dead
- Customer can't browse products

IF: Section schema invalid JSON
THEN: Customizer crashes for that section
- Merchant can't edit that section's settings
```

### Layer 5: Block Changes (Powerful — Used Everywhere)

```
IF: blocks/text.liquid delete
THEN: ALL text blocks gone
- Every section that uses text blocks broken
- Almost every section affected

IF: blocks/button.liquid delete (PUBLIC block)
THEN: Manual button placement broken
- Sections still have buttons (via snippet)
- BUT: merchant can't add custom buttons

IF: blocks/_cart-summary.liquid delete
THEN: Cart page checkout button GONE
- ZERO revenue
- 11/10 severity

IF: blocks/filters.liquid delete
THEN: Collection filters gone
- -30% to -50% conversion drop
- Customer browsing crippled

IF: blocks/_product-media-gallery.liquid delete
THEN: Product images gone on product page
- Customer can't see product
- ZERO sales
```

### Layer 6: Snippet Changes (DANGEROUS — Shared!)

```
IF: snippets/product-card.liquid changes
THEN: 6+ sections automatically updated
- sections/product-list.liquid
- sections/product-recommendations.liquid
- sections/search-results.liquid
- sections/main-collection.liquid
- sections/section-rendering-product-card.liquid
- blocks/product-recommendations.liquid

IF: snippets/image.liquid delete
THEN: ALL images on entire website gone
- 20+ snippets/sections use it
- 11/10 severity — DON'T DELETE

IF: snippets/button.liquid delete
THEN: ALL buttons gone
- 15+ sections affected
- 10/10 severity

IF: snippets/icon.liquid delete
THEN: ALL SVG icons gone
- Cart icon, search icon, menu icon, arrows
- Centralized icon system broken
- 9/10 severity

IF: snippets/pagination-controls.liquid changes
THEN: 3 places affected
- main-blog (blog page numbers)
- main-collection (collection page numbers)
- search-results (search page numbers)

IF: snippets/slideshow.liquid changes
THEN: 3 places affected
- sections/slideshow.liquid
- sections/carousel.liquid
- sections/predictive-search.liquid (resource carousel)

IF: snippets/scripts.liquid changes
THEN: ALL JavaScript modules affected
- Import map central
- Asset loading broken if mistyped
```

### Layer 7: Asset Changes

```
IF: assets/component.js delete
THEN: ALL custom elements break
- Foundation file for all components
- 11/10 severity

IF: assets/product-form.js delete
THEN: Add to Cart DEAD on entire site
- Form submission broken
- ZERO sales
- 11/10 severity

IF: assets/variant-picker.js delete
THEN: Variant selection broken
- Customer selects "Red" but Blue added to cart
- Wrong variant orders → returns/refunds
- 10/10 severity

IF: assets/facets.js delete
THEN: Filters work via page reload (slow but functional)
- AJAX filtering dies
- Bad UX but not broken
- 8/10 severity

IF: assets/header.js delete
THEN: Header behavior gone
- Sticky header doesn't work
- Mobile menu may break
- 9/10 severity

IF: assets/base.css delete
THEN: Site looks plain ugly
- No styling, raw HTML
- 11/10 severity (unusable)

IF: Asset filename typo in liquid
THEN: 404 in console, feature broken
- Console error: "Failed to load resource"
- Silent fail in some cases

IF: SVG file missing but referenced
THEN: Empty space where icon should be
- icon.liquid graceful fail (no error)
```

### Layer 8: Config Changes

```
IF: config/settings_schema.json invalid JSON
THEN: Customizer crashes ENTIRELY
- Merchant can't customize anything
- 11/10 severity — IMMEDIATE FIX NEEDED

IF: config/settings_data.json deleted
THEN: All merchant customizations lost
- Falls back to defaults
- Logo, colors, fonts reset

IF: Setting ID changed in schema
THEN: Saved data lost for that setting
- Don't rename — only add new IDs

IF: Range step rule violated
THEN: "Setting must be a step in the range" error
- Customizer can't save that setting
```

### Layer 9: Locale Changes

```
IF: locales/en.default.json delete
THEN: ALL fallback translations gone
- Sites show raw keys like "actions.add_to_cart"
- 11/10 severity

IF: Translation key missing in locale
THEN: Falls back to en.default.json
- Multilingual sites get mixed languages

IF: Hardcoded English in liquid
THEN: French/German customers see English
- Not translatable
- Bad UX international

IF: Schema label hardcoded (no t: prefix)
THEN: Customizer shows English to all merchants
- Multilingual admin broken
```

## Critical Path (Customer's Purchase Journey)

**NEVER break these files** — they're on the revenue path:

```
Home → Collection → Product → Cart → Checkout

Required Files:
├── layout/theme.liquid (every page)
├── sections/header.liquid (navigation)
├── sections/main-collection.liquid (browsing)
├── sections/product-information.liquid (product view)
├── blocks/buy-buttons.liquid (purchase action)
├── assets/variant-picker.js (variant selection)
├── assets/product-form.js (cart add)
├── sections/main-cart.liquid (review)
├── blocks/_cart-summary.liquid (checkout button)
├── assets/component-cart-items.js (cart management)
└── snippets/cart-summary.liquid (totals display)
```

Break ANY of these = LOST REVENUE

## Mobile-Critical Files (60-70% Traffic)

```
Mobile Experience Files:
├── snippets/header-drawer.liquid + assets/header-drawer.js
│   (Hamburger mobile menu)
├── assets/component-cart-items.js
│   (Mobile cart drawer)
├── snippets/quick-add.liquid + assets/quick-add.js
│   (Mobile-friendly cart add)
└── Responsive CSS in assets/base.css
    (Layout breakpoints)
```

## Performance-Critical Files

```
Performance Files (Core Web Vitals):
├── assets/performance.js (lazy loading)
├── assets/section-hydration.js (lazy section init)
├── snippets/image.liquid (lazy + srcset)
├── assets/component.js (modulepreload)
├── snippets/scripts.liquid (import maps)
└── assets/morph.js (smooth DOM updates)
```

## Common Cascade Scenarios

### Scenario: Modify product-card snippet

```
Action: Change product-card.liquid styling
Cascade:
├── sections/product-list.liquid → Cards updated
├── sections/main-collection.liquid → Cards updated
├── sections/product-recommendations.liquid → Cards updated
├── sections/search-results.liquid → Cards updated
└── blocks/product-recommendations.liquid → Cards updated

Test Required: All 5 contexts!
```

### Scenario: Update slideshow.js

```
Action: Fix bug in slideshow.js
Cascade:
├── sections/slideshow.liquid → Hero slideshow affected
├── sections/carousel.liquid → Content carousels affected
└── sections/predictive-search.liquid → Resource carousel affected

Test Required: All 3 carousels!
```

### Scenario: Range step violation

```
Action: Add { min: 0, max: 500, step: 1, default: 100 } in schema
Result:
├── Customizer crashes
├── Merchant can't edit ANY setting in section
├── Theme load may fail
└── Severity: 9/10

Fix: { min: 0, max: 500, step: 5, default: 100 }
     (500/5 = 100 steps, default 100 = 0 + 20×5 ✓)
```

### Scenario: Color picker check (common bug)

```
Action: {% if section.settings.text_color != blank %}
Result:
├── Always TRUE (color picker never blank)
├── Custom color logic always applies
└── Default theme colors never used

Fix: Use checkbox toggle pattern
     {% if section.settings.use_custom_color %}
       color: {{ section.settings.text_color }};
     {% endif %}
```

## Decision Framework

When asked to delete/modify a file, ask:

1. **Is it on critical path?** (header, product, cart) → Extra caution
2. **Is it shared?** (snippets/product-card.liquid) → Test all usages
3. **Severity tier?** (11/10 vs 5/10) → Higher tier = more testing
4. **Performance impact?** (LCP, CLS, FCP) → Verify Core Web Vitals
5. **Mobile affect?** → Test on mobile FIRST
6. **Multilingual?** → Verify locale files
7. **Customizer impact?** → Test in editor

## Recovery Procedures

### If Customizer Crashes

1. Check `config/settings_schema.json` for invalid JSON
2. Verify range rules: `(max-min)/step ≤ 100`
3. Check default values on valid step
4. Validate JSON with online tool
5. Revert last change if needed

### If Site Looks Broken

1. Check `assets/base.css` exists
2. Check `snippets/stylesheets.liquid` references valid CSS
3. Browser console for 404 errors
4. Verify `layout/theme.liquid` intact

### If Cart Doesn't Work

1. Check `assets/product-form.js` exists
2. Check `assets/component-cart-items.js` exists
3. Verify `blocks/_cart-summary.liquid` exists
4. Verify `sections/main-cart.liquid` schema

### If Filters Don't Work

1. Check `assets/facets.js` exists
2. Check `blocks/filters.liquid` in collection schema
3. Verify product tags/options set in admin
