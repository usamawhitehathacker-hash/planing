---
inclusion: fileMatch
fileMatchPattern: ['config/**']
---

# Folder 7: config/ — Settings System (2 files)

## Role

Config files **merchant ka remote control** hain. Theme Customizer ka backbone.

## Files

| # | File | Role |
|---|------|------|
| 1 | `settings_schema.json` | "Kya options available hain?" (structure/blueprint) |
| 2 | `settings_data.json` | "Merchant ne kya choose kiya?" (saved values) |

## File 1: settings_schema.json

### Role
Theme Customizer ka **blueprint** — defines kya buttons exist on the remote. Merchant ko kya control milega.

### Structure

```json
[
  {
    "name": "theme_info",
    "theme_name": "Horizon",
    "theme_version": "3.5.1",
    "theme_author": "Shopify",
    "theme_documentation_url": "https://...",
    "theme_support_url": "https://..."
  },
  {
    "name": "Logo and Favicon",
    "settings": [
      {
        "type": "image_picker",
        "id": "logo",
        "label": "Logo image"
      },
      {
        "type": "range",
        "id": "logo_height",
        "min": 12,
        "max": 100,
        "step": 4,
        "default": 32,
        "unit": "px",
        "label": "Logo height"
      }
    ]
  },
  {
    "name": "Colors",
    "settings": [
      {
        "type": "color_scheme_group",
        "id": "color_schemes",
        "definition": [
          {
            "type": "color",
            "id": "background",
            "label": "Background"
          }
        ],
        "role": {
          "background": {
            "solid": "background"
          }
        }
      }
    ]
  }
]
```

### Horizon Settings Groups (8 categories)

| Group | Controls | Examples |
|-------|----------|----------|
| **Logo & Favicon** | Store branding | logo, inverse_logo, favicon, logo_height |
| **Colors** | 6 color schemes | scheme-1 to scheme-6 (each with bg/text/heading/primary/hover/secondary) |
| **Typography** | 4 font families | type_body_font, type_heading_font, type_subheading_font, type_accent_font |
| **Layout** | Page structure | page_width, section_spacing, card_hover_effect |
| **Cart** | Cart behavior | cart_type (drawer/page), quick_add, mobile_quick_add |
| **Social Media** | All platforms URLs | social_facebook_link, social_instagram_link, social_tiktok_link, etc. |
| **Animations** | Motion settings | page_transition_enabled, transition_to_main_product |
| **Search** | Search behavior | predictive_search_enabled, search_modal_settings |

## File 2: settings_data.json

### Role
**Saved choices** — jo bhi merchant ne Customizer mein set kiya, sab yahan stored. Real values.

### Structure

```json
{
  "current": {
    "logo": "shopify://shop_images/logo.png",
    "logo_height": 32,
    "color_schemes": {
      "scheme-1": {
        "background": "#FFFFFF",
        "background_gradient": "",
        "text": "#1A1A1A",
        "heading": "#000000",
        "primary_button_background": "#000000",
        "primary_button_text": "#FFFFFF"
      },
      "scheme-2": { ... },
      "scheme-3": { ... },
      "scheme-4": { ... },
      "scheme-5": { ... },
      "scheme-6": { ... }
    },
    "type_body_font": "helvetica_n4",
    "type_heading_font": "helvetica_n7",
    "page_width": 1400,
    "cart_type": "drawer",
    "quick_add": "standard",
    "social_facebook_link": "https://facebook.com/...",
    "page_transition_enabled": true
  },
  "presets": {
    "Default": { ... },
    "Editorial": { ... },
    "Minimal": { ... }
  }
}
```

### Key Properties

- **`current`**: Active settings (live on storefront)
- **`presets`**: Saved style presets (merchant can switch)
- Settings keys MUST match `settings_schema.json` IDs exactly

## How They Work Together

```
1. Merchant opens Customizer
   ↓
2. Customizer reads settings_schema.json
   ↓
3. Renders UI (color pickers, sliders, dropdowns)
   ↓
4. Loads CURRENT values from settings_data.json
   ↓
5. Merchant changes color from #FFFFFF to #F5F5F5
   ↓
6. Customizer saves to settings_data.json
   ↓
7. Storefront reloads
   ↓
8. theme.liquid → snippets/color-schemes.liquid → reads settings_data.json
   ↓
9. CSS custom properties generated with new color
   ↓
10. Site shows new background color
```

## Setting Types Reference

```json
{ "type": "text", "id": "heading", "default": "Welcome" }
{ "type": "textarea", "id": "description" }
{ "type": "richtext", "id": "content" }
{ "type": "html", "id": "code" }
{ "type": "image_picker", "id": "image" }
{ "type": "video", "id": "video" }
{ "type": "video_url", "id": "video_url", "accept": ["youtube", "vimeo"] }
{ "type": "url", "id": "button_url" }
{ "type": "color", "id": "text_color", "default": "#000000" }
{ "type": "color_scheme", "id": "color_scheme", "default": "scheme-1" }
{ "type": "color_background", "id": "bg" }
{ "type": "font_picker", "id": "font", "default": "helvetica_n4" }
{ "type": "checkbox", "id": "show_title", "default": true }
{ "type": "select", "id": "layout",
  "options": [
    { "value": "left", "label": "Left" },
    { "value": "right", "label": "Right" }
  ],
  "default": "left"
}
{ "type": "radio", "id": "align",
  "options": [
    { "value": "left", "label": "Left" },
    { "value": "center", "label": "Center" }
  ]
}
{ "type": "range", "id": "padding",
  "min": 0, "max": 100, "step": 4, "unit": "px", "default": 24
}
{ "type": "link_list", "id": "menu" }
{ "type": "collection", "id": "collection" }
{ "type": "collection_list", "id": "collections", "limit": 8 }
{ "type": "product", "id": "product" }
{ "type": "product_list", "id": "products", "limit": 12 }
{ "type": "blog", "id": "blog" }
{ "type": "article", "id": "article" }
{ "type": "page", "id": "page" }
{ "type": "header", "content": "Section Heading" }
```

## RANGE RULE (CRITICAL!)

```
FORMULA: (max - min) / step ≤ 100

✅ min: 0, max: 100, step: 4 → 25 steps ✓
✅ min: 0, max: 200, step: 4 → 50 steps ✓
❌ min: 0, max: 500, step: 1 → 500 steps ✗ CRASH

ALSO: default value MUST be valid step from min
✅ min: 30, max: 60, step: 5, default: 35 ✓ (30 + 1×5)
✅ min: 30, max: 60, step: 5, default: 45 ✓ (30 + 3×5)
❌ min: 30, max: 60, step: 5, default: 33 ✗ (33 not on step grid)
❌ min: 30, max: 60, step: 5, default: 32 ✗ INVALID
```

## COLOR PICKER RULE

Shopify color picker **NEVER returns blank** — always has a value (default `#000000` or whatever set).

```liquid
{# ❌ WRONG — always true #}
{% if section.settings.text_color != blank %}
  ...
{% endif %}

{# ✅ CORRECT — use checkbox toggle #}
{% if section.settings.use_custom_color %}
  color: {{ section.settings.text_color }};
{% endif %}

{# ✅ ALTERNATE — empty string check #}
{% if section.settings.text_color != "" %}
  ...
{% endif %}
```

## CRITICAL Connection Files

`settings_data.json` is read by:
- `snippets/theme-styles-variables.liquid` (CSS vars)
- `snippets/color-schemes.liquid` (color CSS)
- `snippets/fonts.liquid` (font loading)
- EVERY file that uses `settings.xyz`

## IF-THEN Logic

```
IF: settings_schema.json mein invalid JSON
THEN: Customizer crashes ENTIRELY → merchant can't customize anything
→ SEVERITY: 11/10

IF: settings_data.json delete
THEN: All merchant customizations lost → falls back to defaults
→ Logo, colors, fonts all reset

IF: Setting ID mismatch between schema and data
THEN: Setting value not found → uses default

IF: Range step rule violated
THEN: "Setting must be a step in the range" error in Customizer
→ Setting can't be saved

IF: Color picker check `!= blank`
THEN: Always TRUE → buggy logic
→ FIX: Use checkbox toggle pattern

IF: Naya setting add to schema but no default
THEN: Existing stores get null/undefined → potential errors
→ Always provide default

IF: Setting ID change kiya
THEN: Old saved value lost → merchant has to re-set
→ Versioning carefully

IF: settings_data.json corrupt JSON
THEN: Theme load FAILS → store BROKEN
```

## Best Practices

1. **NEVER directly edit `settings_data.json`** — let Customizer handle it
2. **Schema validation pehle test** — invalid JSON crashes everything
3. **Always provide defaults** for new settings
4. **Setting IDs are permanent** — don't rename, only add new
5. **Group settings** with `header` type for visual organization
6. **Range rule enforced**: `(max-min)/step ≤ 100` AND default on valid step
7. **Color picker pattern**: Always use checkbox toggle for "use custom color"
8. **Use translation keys**: `"label": "t:settings.logo.label"` (not hardcoded English)
9. **Limit lists**: collection_list/product_list have `"limit": N` for performance
10. **Test in Customizer before commit** — schema errors silently break editing
