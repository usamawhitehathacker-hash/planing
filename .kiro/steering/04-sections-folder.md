---
inclusion: fileMatch
fileMatchPattern: ['sections/**']
---

# Folder 3: sections/ — Major Visual Components (42 files)

## Role

Sections **kamre ka saman** hain (sofa, TV, table). Customer JO actually DEKHTA hai. Merchant Customizer mein drag, drop, reorder, customize kar sakta hai.

## 10 Categories Distribution

```
sections/ (42 files)
├── HEADER SECTIONS (3)      → Website ka TOP area
├── FOOTER SECTIONS (3)      → Website ka BOTTOM area
├── HERO/BANNER SECTIONS (3) → First Impression / Visual Impact
├── PRODUCT SECTIONS (8)     → Products dikhana / sell karna
├── COLLECTION SECTIONS (4)  → Categories / Groups dikhana
├── CONTENT SECTIONS (8)     → Text, media, custom content
├── BLOG SECTIONS (3)        → Blog system
├── SEARCH SECTIONS (4)      → Search functionality
├── CART SECTION (1)         → Shopping cart
└── PAGE/UTILITY (5)         → Static pages + errors + internal
```

## Standard Section Template

```liquid
{%- liquid
  assign section_id = section.id
  assign color_scheme = section.settings.color_scheme
-%}

<div
  id="section-{{ section_id }}"
  class="section section-[name] color-{{ color_scheme }}"
  {{ section.shopify_attributes }}
>
  {%- for block in section.blocks -%}
    {%- case block.type -%}
      {%- when 'text_block' -%}
        <div class="block block-text" {{ block.shopify_attributes }}>
          {{ block.settings.content }}
        </div>
      {%- when '@app' -%}
        {% render block %}
    {%- endcase -%}
  {%- endfor -%}
</div>

{% stylesheet %}
  /* Scoped CSS */
{% endstylesheet %}

{% schema %}
{
  "name": "t:names.section_name",
  "tag": "section",
  "class": "section-name",
  "settings": [],
  "blocks": [{ "type": "@app" }],
  "presets": [{ "name": "Section Name" }]
}
{% endschema %}
```

## CATEGORY 1: HEADER SECTIONS (3 files)

### `header-group.json` (Section Group)
**Type**: JSON file (not liquid)  
**Role**: Header sections ka order maintain  
**Connections**: custom.liquid, header-announcements.liquid, header.liquid  
**Called by**: `layout/theme.liquid` via `{% sections 'header-group' %}`

```json
{
  "type": "header",
  "name": "Header",
  "sections": {
    "custom": { "type": "custom" },
    "announcements": { "type": "header-announcements" },
    "header": { "type": "header" }
  },
  "order": ["custom", "announcements", "header"]
}
```

### `header.liquid` (MOST COMPLEX)
**Role**: Logo + Menu + Search + Cart + Account  
**Handles**: Desktop, mobile, mega menu, sticky, transparent, multi-level  
**Connections**: 12-15+ files (see architecture overview)

### `header-announcements.liquid`
**Role**: Marquee scrolling promotional messages  
**Connections**: `blocks/_announcement.liquid`, `assets/announcement-bar.js`

## CATEGORY 2: FOOTER SECTIONS (3 files)

### `footer-group.json`
Same pattern as header-group.json — order maintain karta hai.

### `footer.liquid`
**Role**: Email signup + menus + text columns + social  
**Blocks**: group, text, email-signup, menu, social-links

### `footer-utilities.liquid`
**Role**: Bottom bar — copyright, policies, payment icons  
**Blocks**: footer-copyright, footer-policy-list, social-links, payment-icons

## CATEGORY 3: HERO/BANNER SECTIONS (3 files)

### `hero.liquid`
**Role**: Single full-width banner with text overlay + CTA  
**Best For**: Clean, fast-loading hero with one strong message  
**Blocks**: text, button, _image, video  
**Snippets**: background-media, overlay  
**CRITICAL**: Hero image `loading="eager"` (NEVER lazy)

### `slideshow.liquid`
**Role**: Multi-slide carousel with auto-rotate + arrows + dots  
**Blocks**: _slide  
**Snippets**: slideshow, slideshow-controls, slideshow-arrows  
**Assets**: `slideshow.js` (SHARED with carousel.liquid!)

### `layered-slideshow.liquid`
**Role**: Premium parallax/depth effect slideshow  
**Best For**: High-end luxury stores  
**Blocks**: _layered-slide  
**Assets**: layered-slideshow.js  
**WARN**: Mobile performance issue — disable parallax on mobile

## CATEGORY 4: PRODUCT SECTIONS (8 files) — REVENUE CRITICAL!

### `product-information.liquid` (HEART OF STORE)
**MOST COMPLEX SECTION** — 15-20+ connections  
**Role**: Complete product page — gallery + title + price + variants + cart + description  
**Handles**: Multiple images, video, 3D, variant selection, dynamic pricing, inventory, quantity  
**Connections** (see architecture overview for full map)  
**CRITICAL**: Without this section + product-form.js + variant-picker.js = ZERO SALES

### `product-list.liquid`
**Role**: Product grid for home/custom pages (NOT collection page)  
**Blocks**: _product-card, _product-list-content, _product-list-text, _product-list-button  
**Snippets**: product-grid, product-card

### `product-recommendations.liquid`
**Role**: "You may also like" — Shopify AI-powered  
**API**: Shopify Recommendations API (AJAX lazy load)  
**Revenue**: 10-30% from cross-selling

### `product-hotspots.liquid`
**Role**: Lifestyle image with clickable product dots  
**Best For**: Fashion, home decor, lookbooks  
**Blocks**: _hotspot-product

### `featured-product.liquid`
**Role**: Single product highlight (without product page navigation)

### `featured-product-information.liquid`
**Role**: Detailed featured product info panel (carousel format)

### `quick-order-list.liquid`
**Role**: Bulk ordering for B2B/wholesale  
**Assets**: quick-order-list.js, component-cart-quantity-selector.js

### `section-rendering-product-card.liquid` (INTERNAL)
**Role**: AJAX product card renderer (programmatic)  
**Used By**: Quick add, search results, infinite scroll  
**WARN**: Don't delete — breaks quick-add and search

## CATEGORY 5: COLLECTION SECTIONS (4 files)

### `main-collection.liquid` (CRITICAL FOR SALES)
**Role**: Collection page main view — grid + filters + sorting + pagination  
**Blocks**: filters  
**Snippets**: product-grid, sorting, list-filter, price-filter, pagination-controls  
**Assets**: facets.js (AJAX filtering!), paginated-list.js  
**CRITICAL**: Without facets.js, every filter click = full page reload (BAD UX)

### `main-collection-list.liquid`
**Role**: `/collections` page — ALL collections grid (auto-generated)  
**Snippets**: collection-card, editorial-collection-grid

### `collection-list.liquid`
**Role**: Custom collection cards (merchant manually picks) — for any page  
**Blocks**: _collection-card, _collection-card-image  
**Use**: Home page "Shop by Category"

### `collection-links.liquid`
**Role**: Horizontal collection nav — quick category switch  
**Assets**: collection-links.js (scroll behavior, active state)

## CATEGORY 6: CONTENT SECTIONS (8 files)

### `media-with-content.liquid`
**Role**: Image/Video + Text side-by-side  
**Most Versatile** — used everywhere  
**Blocks**: _content, _image, video, text, button

### `carousel.liquid`
**Role**: Content cards horizontal carousel (testimonials, features)  
**Blocks**: _carousel-content, _card  
**Snippets**: slideshow (SHARED with slideshow.liquid)  
**Assets**: slideshow.js (SHARED — change once = both affected!)

### `marquee.liquid`
**Role**: Continuously scrolling text ticker  
**Blocks**: _marquee  
**Assets**: marquee.js  
**A11Y**: `@media (prefers-reduced-motion: reduce)` mandatory

### `custom-liquid.liquid`
**Role**: Raw Liquid code section — full developer freedom  
**No dependencies** — sandbox

### `custom.liquid`
**Role**: Flexible custom section with blocks support  
**THIS IS WHERE HORIZON USES CUSTOM ANNOUNCEMENT BAR** in header-group!

### `divider.liquid`
**Role**: Horizontal line separator  
**Standalone** — no dependencies

### `logo.liquid`
**Role**: Brand logo standalone display  
**Blocks**: logo

### `section.liquid` (SWISS ARMY KNIFE)
**Role**: Generic flexible section — all-purpose  
**Blocks**: group, text, image, button, video

## CATEGORY 7: BLOG SECTIONS (3 files)

### `main-blog.liquid`
**Role**: Blog posts listing with pagination  
**Blocks**: _blog-post-card  
**Snippets**: editorial-blog-grid, pagination-controls (SHARED!)  
**Assets**: blog-posts-list.js

### `main-blog-post.liquid`
**Role**: Single article — title + image + body + comments  
**Blocks**: _blog-post-content, _blog-post-featured-image, _blog-post-info-text  
**Snippets**: blog-comment-form

### `featured-blog-posts.liquid`
**Role**: Blog promotion section (carousel/grid for home page)  
**Blocks**: _featured-blog-posts-card, _featured-blog-posts-image, _featured-blog-posts-title

## CATEGORY 8: SEARCH SECTIONS (4 files)

### `search-header.liquid`
**Role**: Search results page top — input + query display  
**Blocks**: _search-input  
**Assets**: search-page-input.js

### `search-results.liquid`
**Role**: Search results display — products + pages + articles  
**Snippets**: product-card, resource-list, pagination-controls (all SHARED!)

### `predictive-search.liquid`
**Role**: Live search suggestions (instant results while typing)  
**Snippets**: predictive-search-products-list, predictive-search-resource-carousel  
**Assets**: predictive-search.js  
**API**: `/search/suggest.json` (300ms debounce)

### `predictive-search-empty.liquid`
**Role**: "No results found" with suggestions  
**Snippets**: predictive-search-empty-state

## CATEGORY 9: CART SECTION (1 file)

### `main-cart.liquid` (REVENUE CRITICAL)
**Role**: Cart page — items + quantities + totals + checkout  
**Blocks**: _cart-title, _cart-products, _cart-summary  
**Snippets**: cart-products, cart-summary, cart-items-component  
**Assets**: component-cart-items.js (AJAX!), cart-note.js  
**CRITICAL**: Without `_cart-summary` block = NO CHECKOUT BUTTON = NO REVENUE

## CATEGORY 10: PAGE/UTILITY SECTIONS (5 files)

### `main-page.liquid`
**Role**: Generic page content (About, FAQ)  
**Blocks**: page-content, page

### `main-404.liquid`
**Role**: "Page not found" friendly error  
**Best Practice**: Add search + popular links to recover customers

### `password.liquid`
**Role**: Password form for closed store

### `password-footer.liquid`
**Role**: Minimal footer for password page

### `_blocks.liquid` (INTERNAL SYSTEM FILE)
**Role**: Centralized block rendering for ALL sections  
**Used By**: Every section that uses blocks  
**CRITICAL**: Delete = ALL block rendering breaks across theme = 11/10 SEVERITY

## Section Schema Range Rule (CRITICAL)

```
FORMULA: (max - min) / step ≤ 100

✅ min: 0, max: 100, step: 4 → 25 steps ✓
✅ min: 0, max: 200, step: 4 → 50 steps ✓
❌ min: 0, max: 500, step: 1 → 500 steps ✗ CRASH

ALSO: default value MUST be valid step from min
✅ min: 30, max: 60, step: 5, default: 35 ✓
❌ min: 30, max: 60, step: 5, default: 33 ✗
```

## Section IF-THEN Cascade

```
IF: header.liquid delete → poori site ka navigation gone
IF: footer.liquid delete → no email signup, links, social
IF: product-information.liquid delete → product page broken = ZERO sales
IF: main-cart.liquid delete → cart page dead = no checkout
IF: main-collection.liquid delete → product browsing broken
IF: _blocks.liquid delete → ALL sections with blocks crash
IF: header-group.json se section remove → poori site se gayab
IF: Section schema mein invalid JSON → Customizer crash
```
