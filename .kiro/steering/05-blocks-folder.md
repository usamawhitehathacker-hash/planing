---
inclusion: fileMatch
fileMatchPattern: ['blocks/**']
---

# Folder 4: blocks/ — Customizer Building Blocks (91 files)

## Role

Blocks **saman ke parts** hain (cushion, drawer, lamp). Sections ke andar ke chote configurable units. Merchant Customizer mein drag/drop/reorder kar sakta hai.

## Public vs Private Convention (CRITICAL!)

```
text.liquid           → PUBLIC (no underscore)
_heading.liquid       → PRIVATE (underscore prefix)
```

| | PUBLIC | PRIVATE |
|---|--------|---------|
| Visibility | Customizer mein dikhta | Customizer mein nahi dikhta |
| Sections | Any compatible section | Specific sections only |
| Control | Merchant controls | Developer controls |
| Settings | More exposed | Limited/none |
| Use | "Add this anywhere" | "Internal use" |
| Examples | text, button, image, video, product-card | _heading, _content, _image, _header-logo |

## Why Horizon Uses Separate Blocks Folder

**Old themes**: Blocks defined inside section file (500+ lines per section)  
**Horizon**: Blocks alag files mein → clean, organized, REUSABLE

**Benefit**: Ek block 10 sections mein use ho sakta hai

## 23 Block Categories (91 files total)

### CATEGORY 1: Header Blocks (2)

| File | Type | Role |
|------|------|------|
| `_header-logo.liquid` | PRIVATE | Logo render — image or text fallback |
| `_header-menu.liquid` | PRIVATE | Navigation menu desktop + mobile |

### CATEGORY 2: Text/Content Blocks (5)

| File | Type | Role |
|------|------|------|
| `text.liquid` | PUBLIC | Universal text block (MOST USED!) |
| `_heading.liquid` | PRIVATE | Heading with H1-H6 SEO control |
| `_inline-text.liquid` | PRIVATE | Small inline text (labels, captions) |
| `_content.liquid` | PRIVATE | Content wrapper WITH styling |
| `_content-without-appearance.liquid` | PRIVATE | Content wrapper WITHOUT styling |

### CATEGORY 3: Button/Link Blocks (2)

| File | Type | Role |
|------|------|------|
| `button.liquid` | PUBLIC | Universal button (15+ sections use!) |
| `popup-link.liquid` | PUBLIC | Link that opens modal/popup |

**Button Styles**: primary, secondary, outline, text/link

### CATEGORY 4: Image/Media Blocks (4)

| File | Type | Role |
|------|------|------|
| `image.liquid` | PUBLIC | Image with srcset + lazy load |
| `_image.liquid` | PRIVATE | Image for specific sections |
| `video.liquid` | PUBLIC | YouTube/Vimeo/Shopify video |
| `_media-without-appearance.liquid` | PRIVATE | Raw media output |

### CATEGORY 5: Product Blocks (12) — REVENUE CRITICAL

| File | Type | Role |
|------|------|------|
| `product-title.liquid` | PUBLIC | Product H1 title |
| `price.liquid` | PUBLIC | Price with sale/compare display |
| `variant-picker.liquid` | PUBLIC | Size/Color selector |
| `add-to-cart.liquid` | PUBLIC | Simple ATC button |
| `buy-buttons.liquid` | PUBLIC | ATC + Buy Now + dynamic checkout |
| `accelerated-checkout.liquid` | PUBLIC | Shop Pay/Apple Pay/Google Pay |
| `quantity.liquid` | PUBLIC | +/- quantity selector |
| `product-description.liquid` | PUBLIC | Description text |
| `product-custom-property.liquid` | PUBLIC | Engraving/personalization |
| `product-inventory.liquid` | PUBLIC | "Only X left!" stock |
| `sku.liquid` | PUBLIC | SKU display |
| `review.liquid` | PUBLIC | Star rating from metafields |

### CATEGORY 6: Product Card Blocks (4)

| File | Type | Role |
|------|------|------|
| `product-card.liquid` | PUBLIC | Manual card placement |
| `_product-card.liquid` | PRIVATE | Auto-generated in grids |
| `_product-card-gallery.liquid` | PRIVATE | Card image with hover swap |
| `_product-card-group.liquid` | PRIVATE | Card text wrapper |

### CATEGORY 7: Product Container Blocks (3)

| File | Type | Role |
|------|------|------|
| `_product-details.liquid` | PRIVATE | Right side info panel |
| `_product-media-gallery.liquid` | PRIVATE | Left side image gallery |
| `swatches.liquid` | PUBLIC | Color swatches on cards |

### CATEGORY 8: Product List Blocks (3)

| File | Type | Role |
|------|------|------|
| `_product-list-content.liquid` | PRIVATE | List header wrapper |
| `_product-list-text.liquid` | PRIVATE | List heading text |
| `_product-list-button.liquid` | PRIVATE | "View All" button |

### CATEGORY 9: Collection Blocks (10)

| File | Type | Role |
|------|------|------|
| `collection-card.liquid` | PUBLIC | Manual collection card |
| `_collection-card.liquid` | PRIVATE | Auto in collection grids |
| `_collection-card-image.liquid` | PRIVATE | Card image |
| `_collection-image.liquid` | PRIVATE | Collection page hero |
| `_collection-info.liquid` | PRIVATE | Card text info |
| `_collection-link.liquid` | PRIVATE | Quick nav link |
| `collection-title.liquid` | PUBLIC | Collection page H1 |
| `_inline-collection-title.liquid` | PRIVATE | Inline compact title |
| `featured-collection.liquid` | PUBLIC | Collection picker for product list |
| `filters.liquid` | PUBLIC | Filter sidebar (CRITICAL!) |

### CATEGORY 10: Blog Blocks (9)

| File | Type | Role |
|------|------|------|
| `_blog-post-card.liquid` | PRIVATE | Blog list card |
| `_blog-post-content.liquid` | PRIVATE | Article body |
| `_blog-post-description.liquid` | PRIVATE | Post excerpt |
| `_blog-post-featured-image.liquid` | PRIVATE | Article hero image |
| `_blog-post-image.liquid` | PRIVATE | Card thumbnail |
| `_blog-post-info-text.liquid` | PRIVATE | Date/author/tags |
| `_featured-blog-posts-card.liquid` | PRIVATE | Promo card |
| `_featured-blog-posts-image.liquid` | PRIVATE | Promo card image |
| `_featured-blog-posts-title.liquid` | PRIVATE | Promo card title |

### CATEGORY 11: Cart Blocks (3) — REVENUE CRITICAL

| File | Type | Role |
|------|------|------|
| `_cart-title.liquid` | PRIVATE | "Your Cart" heading + count |
| `_cart-products.liquid` | PRIVATE | Items list |
| `_cart-summary.liquid` | PRIVATE | Totals + checkout button |

**CRITICAL**: Delete `_cart-summary` = NO CHECKOUT = NO REVENUE

### CATEGORY 12: Layout Blocks (3)

| File | Type | Role |
|------|------|------|
| `group.liquid` | PUBLIC | Container — flexbox row/column |
| `spacer.liquid` | PUBLIC | Empty space (px/percentage) |
| `_divider.liquid` | PRIVATE | Horizontal line separator |

### CATEGORY 13: Footer Blocks (4)

| File | Type | Role |
|------|------|------|
| `footer-copyright.liquid` | PUBLIC | "© 2025 Store Name" |
| `footer-policy-list.liquid` | PUBLIC | Privacy/Terms/Refund links |
| `_footer-social-icons.liquid` | PRIVATE | Social media icons |
| `payment-icons.liquid` | PUBLIC | Visa/MC/PayPal trust icons |

### CATEGORY 14: Social Blocks (2)

| File | Type | Role |
|------|------|------|
| `social-links.liquid` | PUBLIC | All platforms group |
| `_social-link.liquid` | PRIVATE | Individual platform link |

### CATEGORY 15: Form Blocks (3)

| File | Type | Role |
|------|------|------|
| `contact-form.liquid` | PUBLIC | Contact form fields |
| `contact-form-submit-button.liquid` | PUBLIC | Form submit button |
| `email-signup.liquid` | PUBLIC | Newsletter signup |

### CATEGORY 16: Special Feature Blocks (8)

| File | Type | Role |
|------|------|------|
| `accordion.liquid` | PUBLIC | FAQ collapsible panels |
| `_accordion-row.liquid` | PRIVATE | Single Q&A item |
| `comparison-slider.liquid` | PUBLIC | Before/After slider |
| `jumbo-text.liquid` | PUBLIC | Animated oversized text |
| `_marquee.liquid` | PRIVATE | Marquee text item |
| `_slide.liquid` | PRIVATE | Slideshow slide |
| `_layered-slide.liquid` | PRIVATE | Parallax slide |
| `_carousel-content.liquid` | PRIVATE | Carousel settings |
| `_card.liquid` | PRIVATE | Generic content card |

### CATEGORY 17: UI Utility Blocks (5)

| File | Type | Role |
|------|------|------|
| `icon.liquid` | PUBLIC | Icon display |
| `logo.liquid` | PUBLIC | Logo block |
| `custom-liquid.liquid` | PUBLIC | Raw Liquid code |
| `page.liquid` | PUBLIC | Page embed |
| `page-content.liquid` | PUBLIC | Page rich content |

### CATEGORY 18: Navigation Blocks (2)

| File | Type | Role |
|------|------|------|
| `menu.liquid` | PUBLIC | Footer/sidebar menu |
| `follow-on-shop.liquid` | PUBLIC | Shop app integration |

### CATEGORY 19: Search Blocks (1)

| File | Type | Role |
|------|------|------|
| `_search-input.liquid` | PRIVATE | Search page input |

### CATEGORY 20: Announcement Blocks (1)

| File | Type | Role |
|------|------|------|
| `_announcement.liquid` | PRIVATE | Single marquee message |

### CATEGORY 21: Hotspot Blocks (1)

| File | Type | Role |
|------|------|------|
| `_hotspot-product.liquid` | PRIVATE | Image clickable dot |

### CATEGORY 22: Featured Product Blocks (4)

| File | Type | Role |
|------|------|------|
| `_featured-product.liquid` | PRIVATE | Featured wrapper |
| `_featured-product-gallery.liquid` | PRIVATE | Mini gallery |
| `_featured-product-price.liquid` | PRIVATE | Price display |
| `_featured-product-information-carousel.liquid` | PRIVATE | Info carousel |

### CATEGORY 23: Quick Order Blocks (1)

| File | Type | Role |
|------|------|------|
| Quick order list blocks | PRIVATE | B2B bulk order |

## Block Schema Pattern

```json
{
  "type": "text_block",
  "name": "Text",
  "limit": 5,
  "settings": [
    {
      "type": "richtext",
      "id": "content",
      "label": "Content"
    }
  ]
}
```

**Section schema with blocks**:
```json
"blocks": [
  { "type": "text_block" },
  { "type": "@app" }
],
"max_blocks": 10,
"presets": [{ "name": "...", "blocks": [{"type": "text_block"}] }]
```

## CRITICAL Rule: shopify_attributes

**Every block root element MUST have**:
```liquid
<div {{ block.shopify_attributes }}>
  <!-- block content -->
</div>
```

**Without it**: Block can't be selected/highlighted in Customizer editor.

## Block IF-THEN Logic

```
IF: button.liquid delete kiya
THEN: SAARE buttons across theme gone (15+ sections affected)
→ SEVERITY: 10/10

IF: image.liquid block delete
THEN: Manual image placement gone

IF: _cart-summary delete
THEN: NO CHECKOUT BUTTON = NO REVENUE

IF: _product-media-gallery delete
THEN: Product page images gone = no sales

IF: filters block delete from collection
THEN: Customer can't filter = -30 to -50% conversion

IF: shopify_attributes missing
THEN: Block not selectable in editor

IF: Block type in section schema doesn't match block file
THEN: "Block type not found" error

IF: max_blocks limit cross
THEN: Customizer prevents adding more

IF: Block nesting >16 levels
THEN: Layout breaks (Shopify enforced limit)
```

## Block Render Pattern

In section liquid file:
```liquid
{%- for block in section.blocks -%}
  {%- case block.type -%}
    {%- when 'text' -%}
      <div {{ block.shopify_attributes }}>
        {{ block.settings.content }}
      </div>
    {%- when 'button' -%}
      {% render 'button', label: block.settings.label, url: block.settings.url %}
    {%- when '@app' -%}
      {% render block %}
  {%- endcase -%}
{%- endfor -%}
```

## Best Practices

1. **PUBLIC blocks** for merchant freedom (text, button, image)
2. **PRIVATE blocks** (`_prefix`) for internal section structure
3. **`shopify_attributes` mandatory** on every block root
4. **`{% render block %}`** for `@app` block type (Shopify Apps integration)
5. **Limit settings** — too many = overwhelming for merchant
6. **Default values** — always provide sensible defaults
7. **Block nesting** — max 16 levels (use `group.liquid` carefully)
