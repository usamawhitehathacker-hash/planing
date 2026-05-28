---
inclusion: fileMatch
fileMatchPattern: ['locales/**']
---

# Folder 8: locales/ — Translations (51 files)

## Role

Locales **translation book** hain — same code, different languages. 30+ languages auto-supported.

## File Structure

```
locales/
├── 24 storefront translation files (xx.json)
├── 24 customizer label files (xx.schema.json)
└── 3 misc files
```

## Files Breakdown

### Storefront Translation Files (`xx.json`)

| Code | File | Language |
|------|------|----------|
| en | `en.default.json` | English (DEFAULT — fallback) |
| fr | `fr.json` | French |
| de | `de.json` | German |
| es | `es.json` | Spanish |
| it | `it.json` | Italian |
| ja | `ja.json` | Japanese |
| ko | `ko.json` | Korean |
| zh-CN | `zh-CN.json` | Chinese (Simplified) |
| zh-TW | `zh-TW.json` | Chinese (Traditional) |
| pt-BR | `pt-BR.json` | Portuguese (Brazil) |
| pt-PT | `pt-PT.json` | Portuguese (Portugal) |
| nl | `nl.json` | Dutch |
| da | `da.json` | Danish |
| sv | `sv.json` | Swedish |
| nb | `nb.json` | Norwegian (Bokmål) |
| fi | `fi.json` | Finnish |
| pl | `pl.json` | Polish |
| cs | `cs.json` | Czech |
| tr | `tr.json` | Turkish |
| th | `th.json` | Thai |
| bg | `bg.json` | Bulgarian |
| el | `el.json` | Greek |
| hr | `hr.json` | Croatian |
| hu | `hu.json` | Hungarian |
| id | `id.json` | Indonesian |
| lt | `lt.json` | Lithuanian |
| ro | `ro.json` | Romanian |
| ru | `ru.json` | Russian |
| sk | `sk.json` | Slovak |
| sl | `sl.json` | Slovenian |
| vi | `vi.json` | Vietnamese |

### Customizer Label Files (`xx.schema.json`)

| Code | File |
|------|------|
| en | `en.default.schema.json` |
| fr | `fr.schema.json` |
| de | `de.schema.json` |
| es | `es.schema.json` |
| it | `it.schema.json` |
| ja | `ja.schema.json` |
| ko | `ko.schema.json` |
| zh-CN | `zh-CN.schema.json` |
| zh-TW | `zh-TW.schema.json` |
| pt-BR | `pt-BR.schema.json` |
| pt-PT | `pt-PT.schema.json` |
| nl | `nl.schema.json` |
| da | `da.schema.json` |
| sv | `sv.schema.json` |
| nb | `nb.schema.json` |
| fi | `fi.schema.json` |
| pl | `pl.schema.json` |
| cs | `cs.schema.json` |
| tr | `tr.schema.json` |
| th | `th.schema.json` |

## `.json` vs `.schema.json` (CRITICAL DIFFERENCE!)

| Type | Translates | Who Sees |
|------|------------|----------|
| `xx.json` | Storefront text — "Add to cart", "Search", "Sold out" | **Customer** (storefront) |
| `xx.schema.json` | Customizer labels — "Background color", "Section width" | **Merchant** (admin) |

## Translation Structure

```json
// en.default.json
{
  "general": {
    "search": {
      "search": "Search",
      "placeholder": "Search store",
      "no_results": "No results found"
    },
    "currency": {
      "title": "Currency"
    }
  },
  "actions": {
    "add_to_cart": "Add to cart",
    "remove": "Remove",
    "checkout": "Checkout",
    "buy_now": "Buy it now"
  },
  "products": {
    "product": {
      "vendor": "Vendor",
      "sold_out": "Sold out",
      "on_sale": "Sale",
      "from_lowest_price_html": "From {{ lowest_price }}"
    }
  },
  "sections": {
    "header": {
      "menu": "Menu",
      "cart": "Cart"
    }
  }
}
```

## Using Translations in Liquid

```liquid
{# Basic translation #}
{{ 'actions.add_to_cart' | t }}

{# With variables #}
{{ 'products.product.from_lowest_price_html' | t: lowest_price: product.price_min }}

{# In schema labels (use t: prefix) #}
{
  "type": "text",
  "id": "heading",
  "label": "t:sections.hero.heading_label"
}

{# In settings #}
"name": "t:names.section_name"
```

## How Translations Work

```
Code: {{ 'actions.add_to_cart' | t }}

en.default.json: "actions": { "add_to_cart": "Add to cart" }
fr.json:         "actions": { "add_to_cart": "Ajouter au panier" }
de.json:         "actions": { "add_to_cart": "In den Warenkorb" }
ja.json:         "actions": { "add_to_cart": "カートに追加" }
es.json:         "actions": { "add_to_cart": "Agregar al carrito" }

Output depends on:
1. Customer's selected language (currency selector)
2. Shopify Markets language settings
3. Default fallback to en.default.json if missing
```

## Storefront Translation Examples

```json
{
  "general": {
    "404": {
      "title": "Page not found",
      "subtext": "The page you requested does not exist.",
      "link": "Continue shopping"
    },
    "accessibility": {
      "skip_to_content": "Skip to content",
      "close": "Close",
      "next_page": "Next page"
    }
  },
  "products": {
    "product": {
      "add_to_cart": "Add to cart",
      "added_to_cart": "Added to cart",
      "low_stock_html": "Only {{ count }} left in stock!",
      "size_chart": "Size chart",
      "share": "Share",
      "view_full_details": "View full details"
    }
  },
  "cart": {
    "general": {
      "title": "Your cart",
      "empty": "Your cart is empty",
      "continue_browsing": "Continue browsing",
      "subtotal": "Subtotal",
      "checkout": "Checkout"
    }
  },
  "blogs": {
    "article": {
      "comments": "{{ count }} comments",
      "post_a_comment": "Post a comment",
      "share_article": "Share this article"
    }
  }
}
```

## Schema Translation Examples

```json
// en.default.schema.json
{
  "names": {
    "hero_section": "Hero banner",
    "product_list": "Product list",
    "main_cart": "Main cart",
    "footer": "Footer"
  },
  "settings": {
    "color": "Color",
    "background_color": "Background color",
    "font_size": "Font size",
    "padding_top": "Top padding",
    "padding_bottom": "Bottom padding"
  },
  "sections": {
    "hero": {
      "heading_label": "Heading",
      "description_label": "Description",
      "button_label": "Button text"
    }
  }
}
```

## Best Practices

### ALWAYS Use Translation Keys

❌ **Bad** (hardcoded):
```liquid
<button>Add to Cart</button>
```

✅ **Good** (translatable):
```liquid
<button>{{ 'actions.add_to_cart' | t }}</button>
```

### ALWAYS Add Keys to en.default.json

When adding new text, add key to en.default.json FIRST:
```json
{
  "sections": {
    "my_new_section": {
      "heading": "Welcome to our store"
    }
  }
}
```

Then use:
```liquid
{{ 'sections.my_new_section.heading' | t }}
```

### Schema Labels Use `t:` Prefix

```json
{
  "type": "text",
  "id": "heading",
  "label": "t:sections.my_new_section.heading_label",
  "default": "t:sections.my_new_section.heading_default"
}
```

### Variables in Translations

```json
{
  "products": {
    "low_stock_html": "Only {{ count }} left in stock!",
    "from_price": "From {{ price }}"
  }
}
```

```liquid
{{ 'products.low_stock_html' | t: count: variant.inventory_quantity }}
{{ 'products.from_price' | t: price: product.price_min }}
```

### `_html` Suffix for HTML Content

If translation contains HTML, use `_html` suffix:
```json
{
  "promo": {
    "limited_time_html": "<strong>Limited time only!</strong> Save 20%"
  }
}
```

## IF-THEN Logic

```
IF: en.default.json missing key
THEN: Translation shows raw key like "sections.announcement.text"
→ UGLY for customer

IF: en.default.json delete
THEN: ALL fallback translations gone → site shows raw keys everywhere
→ SEVERITY: 11/10 — DON'T DELETE

IF: Customer's locale file missing translation
THEN: Falls back to en.default.json (English)
→ Multilingual sites get mixed languages

IF: Hardcoded English in liquid
THEN: French/German customers see English text
→ Bad UX for international stores

IF: en.default.schema.json missing label
THEN: Customizer shows raw key like "sections.hero.heading_label"
→ Merchant confused

IF: Translation key typo
THEN: Customer sees the typo'd key
→ Test all translations after adding

IF: Variable in translation but not passed
THEN: Shows {{ count }} literal in output
→ Always pass variables: `t: count: 5`

IF: Schema label in liquid (not t: prefix)
THEN: Customizer shows hardcoded English to all merchants
→ Use t: prefix in schema labels
```

## Adding New Language Support

1. Create `xx.json` (storefront)
2. Create `xx.schema.json` (customizer)
3. Translate all keys from en.default
4. Test in Shopify admin → Languages
5. Customer language selector picks it up

## Localization in JS

```javascript
// Theme.translations object available globally
const text = Theme.translations.actions.add_to_cart;
```

## Critical Reminders

1. **NEVER delete `en.default.json`** — fallback for all
2. **`en.default.schema.json` separate file** for Customizer labels
3. **Use `{{ 'key' | t }}` always** — no hardcoded text
4. **`_html` suffix** for HTML content in translations
5. **Variables**: `{{ 'key' | t: variable: value }}`
6. **Schema labels**: `"label": "t:settings.color"`
7. **30+ languages** automatically supported
8. **Right-to-left languages** (Arabic, Hebrew) need extra CSS handling
