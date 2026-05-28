---
inclusion: fileMatch
fileMatchPattern: ['assets/**']
---

# Folder 6: assets/ — CSS + JS + SVG (113 files)

## Role

Assets **rang aur bijli** hain — har woh file jo browser mein download hoti hai. CSS = look, JS = behavior, SVG = icons.

## Distribution

- **JS Files**: 75 (modules + custom elements)
- **SVG Icons**: 33 (centralized icon system)
- **CSS Files**: 3 (base.css, overflow-list.css, template-giftcard.css)
- **JSON**: 1 (jsconfig.json)
- **TypeScript Defs**: 1 (global.d.ts)

## Import Maps System (Horizon's Modern JS)

```html
<script type="importmap">
{
  "imports": {
    "@theme/component": "{{ 'component.js' | asset_url }}",
    "@theme/utilities": "{{ 'utilities.js' | asset_url }}",
    "@theme/events": "{{ 'events.js' | asset_url }}",
    "@theme/dialog": "{{ 'dialog.js' | asset_url }}",
    "@theme/morph": "{{ 'morph.js' | asset_url }}"
  }
}
</script>
```

**Use in JS**:
```javascript
import { Component } from '@theme/component';
import { eventBus } from '@theme/events';
```

## CORE JavaScript Files (13) — Modulepreloaded

These are preloaded for ALL pages.

| File | Role | Severity |
|------|------|----------|
| `component.js` | **Base web component class** — all components extend | CRITICAL |
| `utilities.js` | Helper functions (header height, scroll, etc.) | CRITICAL |
| `events.js` | Custom event bus — components communicate | CRITICAL |
| `performance.js` | IntersectionObserver, lazy loading | HIGH |
| `focus.js` | Focus management — keyboard nav, modal trap | HIGH (a11y) |
| `morph.js` | Smooth DOM updates without page reload | HIGH |
| `scrolling.js` | Scroll utilities (sticky, animations) | MEDIUM |
| `section-renderer.js` | Section re-rendering via AJAX | HIGH |
| `section-hydration.js` | Lazy section initialization | MEDIUM |
| `money-formatting.js` | Price formatting (currency, decimals) | MEDIUM |
| `view-transitions.js` | Page transition animations | LOW |
| `popover-polyfill.js` | Popover API polyfill (older browsers) | LOW |
| `theme-editor.js` | Theme Editor support (Customizer only) | LOW |

## HEADER JavaScript Files (5)

| File | Role |
|------|------|
| `header.js` | Sticky, transparent, height calc |
| `header-menu.js` | Desktop nav, mega menu |
| `header-drawer.js` | Mobile drawer slide |
| `header-actions.js` | Cart/account/search button behavior |
| `announcement-bar.js` | Marquee scroll animation |

## PRODUCT JavaScript Files (15) — Revenue Critical

| File | Role | Severity |
|------|------|----------|
| `product-form.js` | **Form submit, AJAX cart add** | CRITICAL — no sales without |
| `product-card.js` | Hover image swap, quick add | HIGH |
| `product-price.js` | Dynamic price update on variant | HIGH |
| `product-inventory.js` | Stock update on variant | MEDIUM |
| `product-sku.js` | SKU update on variant | LOW |
| `product-title-truncation.js` | Long title truncation | LOW |
| `product-custom-property.js` | Engraving validation | LOW |
| `product-recommendations.js` | AJAX fetch related | MEDIUM |
| `product-hotspot.js` | Hotspot click → popup | MEDIUM |
| `variant-picker.js` | **Variant change cascade** | CRITICAL — wrong variants without |
| `sticky-add-to-cart.js` | Sticky ATC bar on scroll | LOW |
| `fly-to-cart.js` | ATC animation | LOW |
| `price-per-item.js` | Per-item price calc | LOW |
| `volume-pricing.js` | Tiered pricing display | LOW |
| `volume-pricing-info.js` | Pricing tooltip | LOW |

## CART JavaScript Files (6) — Revenue Critical

| File | Role |
|------|------|
| `cart-drawer.js` | Slide-in cart panel |
| `cart-icon.js` | Cart badge count update |
| `cart-note.js` | Order notes field |
| `cart-discount.js` | Apply discount code |
| `component-cart-items.js` | **Quantity change, remove (AJAX)** — CRITICAL |
| `component-cart-quantity-selector.js` | Cart-specific +/- |

## MEDIA JavaScript Files (5)

| File | Role |
|------|------|
| `media.js` | Video/3D model component |
| `media-gallery.js` | **Product gallery — thumbs, zoom, swipe** — HIGH |
| `video-background.js` | Background video autoplay |
| `drag-zoom-wrapper.js` | Image drag pan in zoom |
| `zoom-dialog.js` | Full-screen image zoom modal |

## UI Component JavaScript Files (14)

| File | Role |
|------|------|
| `dialog.js` | Modal/dialog system |
| `floating-panel.js` | Tooltip, dropdown positioning |
| `anchored-popover.js` | Element-anchored popups |
| `slideshow.js` | **SHARED!** Carousel engine (slideshow + carousel + search) |
| `layered-slideshow.js` | Parallax slideshow |
| `marquee.js` | Continuous scroll animation |
| `jumbo-text.js` | Scroll-triggered text animation |
| `comparison-slider.js` | Before/after drag slider |
| `show-more.js` | "Show More" expand button |
| `overflow-list.js` | Horizontal overflow handling |
| `accordion-custom.js` | Accordion expand/collapse |
| `auto-close-details.js` | Auto-close `<details>` |
| `copy-to-clipboard.js` | Copy text button |
| `rte-formatter.js` | Rich text content formatting |

## SEARCH JavaScript Files (3)

| File | Role |
|------|------|
| `predictive-search.js` | Live search (300ms debounce) |
| `search-page-input.js` | Search page input |
| `results-list.js` | Results list rendering |

## COLLECTION JavaScript Files (4)

| File | Role |
|------|------|
| `facets.js` | **AJAX filtering — no page reload** — HIGH |
| `paginated-list.js` | Infinite scroll/pagination |
| `paginated-list-aspect-ratio.js` | Image ratio in pagination |
| `collection-links.js` | Horizontal scroll, active state |
| `blog-posts-list.js` | Blog pagination |

## QUICK ADD JavaScript Files (2)

| File | Role |
|------|------|
| `quick-add.js` | Quick Add system |
| `quick-order-list.js` | Bulk order (B2B) |

## UTILITY JavaScript Files (6)

| File | Role |
|------|------|
| `localization.js` | Country/language switcher |
| `local-pickup.js` | Store pickup availability |
| `gift-card-recipient-form.js` | Gift card recipient validation |
| `qr-code-generator.js` | QR code generation |
| `qr-code-image.js` | QR code canvas drawing |
| `recently-viewed-products.js` | LocalStorage history |

## CSS Files (3)

### `base.css` — MAIN STYLESHEET
- Reset + grid + typography + buttons + forms + utilities + responsive + components
- HAR page pe load
- Bina iske website plain ugly HTML
- Loaded via `snippets/stylesheets.liquid`

### `overflow-list.css`
- Overflow list component CSS
- Preloaded
- Used by: header menu overflow

### `template-giftcard.css`
- Gift card page-specific CSS
- Only loaded on gift card pages

## SVG Icons (33 files)

All accessed via `{% render 'icon', icon_name: 'cart' %}` (centralized through `snippets/icon.liquid`).

| Icon | File |
|------|------|
| Account | `icon-account.svg` |
| Add to Cart | `icon-add-to-cart.svg` |
| Arrow | `icon-arrow.svg` |
| Available (✓) | `icon-available.svg` |
| Caret | `icon-caret.svg` |
| Cart | `icon-cart.svg` |
| Checkmark | `icon-checkmark.svg` |
| Checkmark Burst | `icon-checkmark-burst.svg` |
| Chevron Left | `icon-chevron-left.svg` |
| Chevron Right | `icon-chevron-right.svg` |
| Close (X) | `icon-close.svg` |
| Delete (trash) | `icon-delete.svg` |
| Discount | `icon-discount.svg` |
| Double Chevron | `icon-double-chevron.svg` |
| Error | `icon-error.svg` |
| External | `icon-external.svg` |
| Filter | `icon-filter.svg` |
| Filter Close | `icon-filters-close.svg` |
| Grid Default | `icon-grid-default.svg` |
| Grid Dense | `icon-grid-dense.svg` |
| Info | `icon-info.svg` |
| Inventory | `icon-inventory.svg` |
| Menu (hamburger) | `icon-menu.svg` |
| Minus | `icon-minus.svg` |
| One Col Mobile | `icon-one-col-mobile.svg` |
| Orders | `icon-orders.svg` |
| Pause | `icon-pause.svg` |
| Play | `icon-play.svg` |
| Plus | `icon-plus.svg` |
| Reset | `icon-reset.svg` |
| Search | `icon-search.svg` |
| Shopify | `icon-shopify.svg` |
| Unavailable (X) | `icon-unavailable.svg` |

**SVG Best Practice**: Use `fill="currentColor"` so CSS can change color via `color` property.

## Dev Configuration Files (2)

### `jsconfig.json`
- VS Code/IDE TypeScript checking
- `@theme/*` path aliases for autocomplete
- Development time only

### `global.d.ts`
- TypeScript type definitions
- Shopify globals (Shopify.country, Theme.routes)
- Type safety for IDE

## Web Component Pattern

```javascript
import { Component } from '@theme/component';

class MyFeature extends Component {
  connectedCallback() {
    super.connectedCallback();
    this.init();
  }

  init() {
    // setup logic
    this.button = this.querySelector('button');
    this.button.addEventListener('click', this.handleClick.bind(this));
  }

  handleClick() {
    // event handling
  }

  disconnectedCallback() {
    super.disconnectedCallback();
    // cleanup
  }
}

customElements.define('my-feature', MyFeature);
```

## Asset Loading Pattern

```liquid
{# In section liquid #}
<script src="{{ 'my-feature.js' | asset_url }}" type="module"></script>

{# Image with CDN #}
{{ image | image_url: width: 800 | image_tag: ... }}

{# CSS in stylesheet block (preferred) #}
{% stylesheet %}
  /* Section CSS here */
{% endstylesheet %}
```

## JS Severity Tiers

### CRITICAL (Store stops working)
- `product-form.js` → Add to Cart DEAD
- `variant-picker.js` → Variants DEAD
- `header.js` → Navigation DEAD
- `component-cart-items.js` → Cart DEAD

### HIGH IMPACT (Major features break)
- `facets.js` → Collection filters DEAD
- `predictive-search.js` → Live search DEAD
- `media-gallery.js` → Product images broken
- `header-drawer.js` → Mobile menu DEAD

### MEDIUM IMPACT (Section-level break)
- `slideshow.js` → Slideshows + Carousels stop
- `marquee.js` → Marquee text static
- `product-recommendations.js` → Recs don't load
- `announcement-bar.js` → Announcements static

### LOW IMPACT (Minor feature loss)
- `cart-note.js` → Order notes don't work
- `collection-links.js` → Scroll behavior gone
- `product-inventory.js` → Stock count stale

## Asset IF-THEN Logic

```
IF: base.css delete
THEN: Plain HTML — ugly text everywhere

IF: component.js delete
THEN: ALL custom elements break (foundation gone)

IF: product-form.js missing
THEN: Add to Cart dead = ZERO SALES

IF: facets.js missing
THEN: Filters work via page reload (slow but functional)

IF: slideshow.js missing
THEN: Multiple carousels break (slideshow + carousel + search resource)

IF: SVG file missing but referenced
THEN: Empty space where icon should be (silent fail)

IF: hardcoded fill in SVG (not currentColor)
THEN: CSS color won't change icon color

IF: External image URL (not Shopify CDN)
THEN: No auto-resize, no WebP, slower load

IF: Image without lazy loading (above fold OK, below NO)
THEN: All images load on page load = SLOW

IF: Asset filename typo in liquid
THEN: 404 in console, feature broken

IF: Module type missing in script tag
THEN: Import statements fail
```
