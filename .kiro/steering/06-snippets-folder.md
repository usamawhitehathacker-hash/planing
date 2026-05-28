---
inclusion: fileMatch
fileMatchPattern: ['snippets/**']
---

# Folder 5: snippets/ — Reusable Code Pieces (98 files)

## Role

Snippets **chote reusable code pieces** hain. Function jo har jagah call ho. **DRY Principle**: Ek baar likho, har jagah use karo.

## Why Snippets Power-AND-Danger

**Power**: Change one snippet → updates everywhere it's used  
**Danger**: One mistake → multiple sections break

**Example**: `snippets/product-card.liquid` is used by:
- sections/product-list.liquid
- sections/product-recommendations.liquid
- sections/search-results.liquid
- sections/main-collection.liquid
- sections/section-rendering-product-card.liquid
- blocks/product-recommendations.liquid

Change product-card.liquid → ALL 6+ places auto-update!

## Snippet Calling Syntax

```liquid
{% render 'snippet-name', variable: value, setting: true %}
```

- File extension `.liquid` NOT included
- **Sandboxed**: outer variables NOT accessible — pass explicitly
- Safe — snippet can't accidentally break things

## Snippets vs Blocks

| Snippet | Block |
|---------|-------|
| `{% render 'name' %}` | Customizer drag/drop |
| Customizer mein NAHI dikhta | Customizer mein dikhta |
| Developer ke liye | Merchant ke liye |
| Code organization | Visual builder |

## 12 Categories (98 files)

### CATEGORY 1: Global Setup Snippets (7)

| File | Role |
|------|------|
| `stylesheets.liquid` | Loads all CSS — `assets/base.css`, `assets/overflow-list.css` |
| `scripts.liquid` | Import map + 70+ JS modules |
| `fonts.liquid` | Google/Shopify font files |
| `meta-tags.liquid` | SEO meta tags (title, description, og:image, canonical) |
| `theme-styles-variables.liquid` | CSS custom properties from settings |
| `color-schemes.liquid` | 6 color schemes CSS generated |
| `theme-editor.liquid` | Customizer editor support (design mode only) |

### CATEGORY 2: Header Snippets (6)

| File | Role |
|------|------|
| `header-actions.liquid` | Cart icon, account, search buttons (right side) |
| `header-drawer.liquid` | Mobile slide-in menu |
| `header-row.liquid` | Header layout row |
| `mega-menu-list.liquid` | Mega menu dropdown content |
| `menu-font-styles.liquid` | Menu typography CSS |
| `submenu-font-styles.liquid` | Dropdown typography CSS |

### CATEGORY 3: Product Snippets (24)

| File | Role |
|------|------|
| `product-card.liquid` | **MOST USED!** Product card (collection, search, home, recs) |
| `product-grid.liquid` | Grid layout for products |
| `product-media.liquid` | Single product media item |
| `product-media-gallery-content.liquid` | Full gallery layout |
| `product-media-gallery-content-styles.liquid` | Gallery CSS |
| `product-information-content.liquid` | Product info panel |
| `product-badges-styles.liquid` | Sale/Sold Out badges CSS |
| `price.liquid` | Price display logic |
| `format-price.liquid` | Price formatting (cents → dollars + currency) |
| `add-to-cart-button.liquid` | ATC button HTML |
| `buy-buttons-styles.liquid` | Buy buttons CSS |
| `quantity-selector.liquid` | +/- quantity component |
| `variant-main-picker.liquid` | Variant picker logic |
| `variant-swatches.liquid` | Color swatches |
| `swatch.liquid` | Individual swatch |
| `strikethrough-variant.liquid` | Sold out variant strikethrough |
| `quick-add.liquid` | Quick add system |
| `quick-add-modal.liquid` | Quick add modal |
| `quick-add-styles.liquid` | Quick add CSS |
| `quick-add-modal-styles.liquid` | Modal CSS |
| `tax-info.liquid` | "Tax included" info |
| `unit-price.liquid` | Per-unit price display |
| `volume-pricing-info.liquid` | Bulk pricing tiers |
| `sku.liquid` | SKU display component |

### CATEGORY 4: Cart Snippets (4)

| File | Role |
|------|------|
| `cart-bubble.liquid` | Cart count badge |
| `cart-items-component.liquid` | Cart items list |
| `cart-products.liquid` | Cart products render |
| `cart-summary.liquid` | Subtotal + checkout button |

### CATEGORY 5: Collection Snippets (4)

| File | Role |
|------|------|
| `collection-card.liquid` | Collection card component |
| `editorial-collection-grid.liquid` | Bento layout for collections |
| `editorial-product-grid.liquid` | Bento layout for products |
| `editorial-blog-grid.liquid` | Bento layout for blog |

### CATEGORY 6: Search Snippets (6)

| File | Role |
|------|------|
| `search.liquid` | Search button/icon (header) |
| `search-modal.liquid` | Full-screen search overlay |
| `predictive-search-styles.liquid` | Live search dropdown CSS |
| `predictive-search-products-list.liquid` | Product results in search |
| `predictive-search-resource-carousel.liquid` | Pages/articles in search |
| `predictive-search-empty-state.liquid` | "No results" message |

### CATEGORY 7: UI Component Snippets (10)

| File | Role |
|------|------|
| `button.liquid` | **CRITICAL!** Universal button render |
| `checkbox.liquid` | Custom styled checkbox |
| `icon.liquid` | **CRITICAL!** SVG icon renderer (any name) |
| `icon-or-image.liquid` | Icon or custom image |
| `image.liquid` | **MOST CRITICAL!** Responsive image (srcset, lazy, alt) |
| `media.liquid` | Image/video/3D detector |
| `video.liquid` | Video embed (YouTube/Vimeo/Shopify) |
| `background-media.liquid` | Background image/video |
| `overlay.liquid` | Color overlay for text readability |
| `link-featured-image.liquid` | Mega menu hover image |

### CATEGORY 8: Slideshow Snippets (6)

| File | Role |
|------|------|
| `slideshow.liquid` | Carousel wrapper (SHARED with carousel section!) |
| `slideshow-slide.liquid` | Individual slide |
| `slideshow-controls.liquid` | Dots/counter |
| `slideshow-arrows.liquid` | Prev/Next arrows |
| `slideshow-arrow.liquid` | Single arrow SVG |
| `slideshow-styles.liquid` | Slideshow CSS |

### CATEGORY 9: Layout/Spacing Snippets (12)

| File | Role |
|------|------|
| `section.liquid` | Section wrapper component |
| `group.liquid` | Group/container wrapper |
| `divider.liquid` | Horizontal line render |
| `spacing-style.liquid` | Margin/padding CSS generator |
| `spacing-padding.liquid` | Padding-only CSS |
| `gap-style.liquid` | Gap CSS for flex/grid |
| `size-style.liquid` | Width/height CSS |
| `typography-style.liquid` | Font CSS generator |
| `layout-panel-style.liquid` | Product page panel layout |
| `border-override.liquid` | Border CSS override |
| `bento-grid.liquid` | 12-item asymmetric grid |
| `grid-density-controls.liquid` | Grid view toggle |

### CATEGORY 10: Filter/Sort Snippets (5)

| File | Role |
|------|------|
| `list-filter.liquid` | Checkbox filter group |
| `price-filter.liquid` | Price range slider |
| `filter-remove-buttons.liquid` | Active filter remove |
| `sorting.liquid` | Sort dropdown |
| `pagination-controls.liquid` | **SHARED!** Page numbers (blog + collection + search) |

### CATEGORY 11: Resource/List Snippets (6)

| File | Role |
|------|------|
| `resource-list.liquid` | Generic resource list |
| `resource-list-carousel.liquid` | Carousel mode |
| `resource-card.liquid` | Generic resource card |
| `resource-image.liquid` | Resource featured image |
| `overflow-list.liquid` | Horizontal overflow with "More" |
| `card-gallery.liquid` | Product card hover image swap |

### CATEGORY 12: Utility Snippets (8)

| File | Role |
|------|------|
| `skip-to-content-link.liquid` | A11Y skip link |
| `text.liquid` | Text render with typography |
| `jumbo-text.liquid` | Animated oversized text |
| `accordion-custom-component.liquid` | Custom accordion HTML |
| `localization-form.liquid` | Country/language selector |
| `password-layout-styles.liquid` | Password page CSS |
| `gift-card-recipient-form.liquid` | Gift card to-recipient form |
| `gift-card-recipient-form-styles.liquid` | Form CSS |

### CATEGORY 13: Image Size Utility Snippets (4)

| File | Role |
|------|------|
| `util-autofill-img-size-attr.liquid` | Auto-calculate image sizes attribute |
| `util-mega-menu-img-sizes-attr.liquid` | Mega menu image sizes |
| `util-product-grid-card-size.liquid` | Grid card image size |
| `util-product-media-sizes-attr.liquid` | Product gallery image sizes |

## CRITICAL Snippets (Don't Delete!)

### `image.liquid` — 11/10 SEVERITY
- Used by 20+ locations
- Delete = ALL images on entire website gone
- Includes: srcset, lazy load, alt, width/height (CLS prevention), Shopify CDN

### `button.liquid` — 10/10 SEVERITY
- Used by 15+ sections/blocks
- Delete = ALL buttons across theme gone
- Includes: primary/secondary/outline/text styles, sizes, full-width

### `icon.liquid` — 9/10 SEVERITY
- Centralized SVG icon system
- Reads from 33 SVG files in assets/
- Delete = ALL icons gone (cart, search, menu, arrows)

### `product-card.liquid` — 9/10 SEVERITY (Shared)
- 6+ sections depend on it
- Change once = all updates
- Test all 6 contexts after changes

### `pagination-controls.liquid` — Shared
- Used by main-blog, main-collection, search-results
- Modify with care

## image.liquid Pattern (MEMORIZE)

```liquid
{%- if image != blank -%}
  {{
    image
    | image_url: width: 800
    | image_tag:
      loading: 'lazy',
      alt: image.alt | default: product.title | escape,
      width: image.width,
      height: image.height,
      sizes: '(min-width: 990px) 50vw, 100vw',
      widths: '300, 600, 900, 1200',
      class: 'img-responsive'
  }}
{%- endif -%}
```

## button.liquid Parameters

```liquid
{% render 'button',
   label: "Shop Now",
   url: "/collections/all",
   style: "primary",       // primary/secondary/outline/text
   size: "medium",          // small/medium/large
   full_width: false,
   icon: "arrow",           // optional SVG icon name
   new_tab: false,
   disabled: false
%}
```

## icon.liquid Parameters

```liquid
{% render 'icon',
   icon_name: 'cart',       // matches assets/icon-cart.svg
   size: 24,
   class: 'icon--header',
   color: 'currentColor'    // inherits text color
%}
```

## Snippet IF-THEN Logic

```
IF: image.liquid delete
THEN: ALL images gone = website broken (11/10 severity)

IF: button.liquid delete
THEN: ALL buttons gone = no CTAs = 10/10 severity

IF: icon.liquid delete
THEN: ALL SVG icons gone

IF: product-card.liquid modify
THEN: 6+ places affected (test all)

IF: pagination-controls.liquid modify
THEN: blog + collection + search affected

IF: snippets/scripts.liquid se import map remove
THEN: ALL JS modules fail to load

IF: slideshow.liquid snippet modify
THEN: hero slideshow + content carousel + predictive resource carousel ALL affected

IF: snippet name typo in render
THEN: "Could not find asset snippets/X.liquid" — page crash

IF: snippets/cart-summary.liquid delete
THEN: Cart page summary gone = no checkout button visible
```

## Best Practices

1. **Sandboxed** — pass all variables explicitly
2. **Default fallbacks** — `image.alt | default: product.title`
3. **Nil checks** — `{% if collection != blank %}`
4. **Search before modifying** — check all usages
5. **Test all contexts** after shared snippet change
6. **DRY principle** — if duplicating code, extract to snippet
7. **Naming** — descriptive (`product-card-gallery` not `pcg`)
8. **Icon system** — use `{% render 'icon' %}` not direct SVG
9. **Image rendering** — always via `{% render 'image' %}` for responsive
10. **Performance** — inline CSS for hidden modals (predictive-search-styles)
