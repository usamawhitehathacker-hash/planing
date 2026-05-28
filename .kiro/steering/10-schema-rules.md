---
inclusion: always
---

# Schema Rules — Critical Validation Reference

## CRITICAL Rules (Customizer Crashes If Violated)

### Rule 1: Range Step Formula

```
(max - min) / step  MUST BE  ≤ 100
```

**Valid Examples**:
```json
{ "min": 0, "max": 100, "step": 4 }    → 25 steps  ✓
{ "min": 0, "max": 200, "step": 4 }    → 50 steps  ✓
{ "min": 0, "max": 500, "step": 5 }    → 100 steps ✓ (boundary)
{ "min": 0, "max": 1000, "step": 10 }  → 100 steps ✓
```

**Invalid Examples**:
```json
{ "min": 0, "max": 500, "step": 1 }    → 500 steps ✗ CRASH
{ "min": 0, "max": 1000, "step": 5 }   → 200 steps ✗ CRASH
{ "min": 0, "max": 100, "step": 0.5 }  → 200 steps ✗ CRASH
```

### Rule 2: Default Value Must Be on Valid Step

```
default = min + (n × step) where n is integer ≥ 0
default must be ≤ max
```

**Valid**:
```json
{ "min": 30, "max": 60, "step": 5, "default": 35 }  ✓ (30 + 1×5)
{ "min": 30, "max": 60, "step": 5, "default": 50 }  ✓ (30 + 4×5)
{ "min": 30, "max": 60, "step": 5, "default": 30 }  ✓ (30 + 0×5)
{ "min": 0, "max": 100, "step": 4, "default": 24 }  ✓ (0 + 6×4)
```

**Invalid**:
```json
{ "min": 30, "max": 60, "step": 5, "default": 33 }  ✗ (33 not on grid)
{ "min": 30, "max": 60, "step": 5, "default": 32 }  ✗
{ "min": 0, "max": 100, "step": 4, "default": 25 }  ✗ (25 not on grid)
{ "min": 0, "max": 60, "step": 5, "default": 65 }   ✗ (default > max)
```

### Rule 3: Block Nesting Limit

**Max 16 blocks per section** (Shopify-enforced)

### Rule 4: Block shopify_attributes

**EVERY block root element MUST have**:
```liquid
<div {{ block.shopify_attributes }}>
  <!-- block content -->
</div>
```

Without it: Customizer can't select/highlight block.

### Rule 5: Schema JSON Validity

- No trailing commas: `{ "a": 1, }` ✗
- Balanced brackets: `{ }` and `[ ]`
- Proper string escaping
- Valid JSON only

Invalid JSON = Customizer crashes entirely

### Rule 6: Color Picker Never Blank

Shopify color picker ALWAYS has a value (default `#000000`).

```liquid
{# ❌ WRONG — always true! #}
{% if section.settings.text_color != blank %}

{# ✅ CORRECT — checkbox toggle pattern #}
{% if section.settings.use_custom_color %}
  color: {{ section.settings.text_color }};
{% endif %}
```

## All Setting Types Reference

### Text Inputs
```json
{ "type": "text", "id": "heading", "label": "Heading", "default": "Welcome" }
{ "type": "textarea", "id": "description", "label": "Description" }
{ "type": "richtext", "id": "content", "label": "Content" }
{ "type": "html", "id": "code", "label": "Custom HTML" }
{ "type": "url", "id": "button_url", "label": "Button URL" }
```

### Media Inputs
```json
{ "type": "image_picker", "id": "image", "label": "Image" }
{ "type": "video", "id": "video", "label": "Video" }
{ "type": "video_url", "id": "video_url", "label": "Video URL", "accept": ["youtube", "vimeo"] }
```

### Color Inputs
```json
{ "type": "color", "id": "text_color", "label": "Text color", "default": "#000000" }
{ "type": "color_scheme", "id": "color_scheme", "label": "Color scheme", "default": "scheme-1" }
{ "type": "color_background", "id": "bg", "label": "Background gradient" }
{ "type": "color_scheme_group", "id": "color_schemes", "definition": [...], "role": {...} }
```

### Font Inputs
```json
{ "type": "font_picker", "id": "font", "label": "Font", "default": "helvetica_n4" }
```

### Choice Inputs
```json
{ "type": "checkbox", "id": "show_title", "label": "Show title", "default": true }

{ "type": "select", "id": "layout", "label": "Layout",
  "options": [
    { "value": "left", "label": "Left" },
    { "value": "right", "label": "Right" }
  ],
  "default": "left"
}

{ "type": "radio", "id": "align", "label": "Alignment",
  "options": [
    { "value": "left", "label": "Left" },
    { "value": "center", "label": "Center" }
  ]
}
```

### Range Slider
```json
{ "type": "range", "id": "padding", "label": "Padding",
  "min": 0, "max": 100, "step": 4, "unit": "px", "default": 24
}
```

### Resource Pickers
```json
{ "type": "link_list", "id": "menu", "label": "Menu" }
{ "type": "collection", "id": "collection", "label": "Collection" }
{ "type": "collection_list", "id": "collections", "label": "Collections", "limit": 8 }
{ "type": "product", "id": "product", "label": "Product" }
{ "type": "product_list", "id": "products", "label": "Products", "limit": 12 }
{ "type": "blog", "id": "blog", "label": "Blog" }
{ "type": "article", "id": "article", "label": "Article" }
{ "type": "page", "id": "page", "label": "Page" }
```

### Visual Divider (Header)
```json
{ "type": "header", "content": "Section Heading" }
{ "type": "paragraph", "content": "Help text for merchant" }
```

## Section Schema Complete Pattern

```liquid
{% schema %}
{
  "name": "t:names.section_name",
  "tag": "section",
  "class": "section-my-section",
  "max_blocks": 10,
  "limit": 1,
  "settings": [
    {
      "type": "header",
      "content": "Layout"
    },
    {
      "type": "select",
      "id": "layout",
      "label": "t:settings.layout",
      "options": [
        { "value": "grid", "label": "t:options.grid" },
        { "value": "list", "label": "t:options.list" }
      ],
      "default": "grid"
    },
    {
      "type": "range",
      "id": "padding_top",
      "min": 0,
      "max": 100,
      "step": 4,
      "unit": "px",
      "default": 24,
      "label": "t:settings.padding_top"
    },
    {
      "type": "color_scheme",
      "id": "color_scheme",
      "label": "t:settings.color_scheme",
      "default": "scheme-1"
    }
  ],
  "blocks": [
    { "type": "text" },
    { "type": "button" },
    { "type": "@app" }
  ],
  "presets": [
    {
      "name": "t:names.section_name",
      "blocks": [
        { "type": "text" }
      ]
    }
  ],
  "templates": ["index", "page", "collection"],
  "enabled_on": {
    "templates": ["index"]
  }
}
{% endschema %}
```

## Schema Properties Reference

| Property | Type | Purpose |
|----------|------|---------|
| `name` | string | Section name in Customizer |
| `tag` | string | HTML tag wrapper (`section`, `div`, `aside`) |
| `class` | string | CSS class on wrapper |
| `max_blocks` | number | Max blocks allowed |
| `limit` | number | Max instances on a page |
| `settings` | array | Section-level settings |
| `blocks` | array | Allowed block types |
| `presets` | array | Default configurations for "Add Section" |
| `templates` | array | DEPRECATED — use `enabled_on`/`disabled_on` |
| `enabled_on` | object | Where section can be added |
| `disabled_on` | object | Where section can't be added |

## Block Schema Pattern

```json
{
  "type": "text_block",
  "name": "t:blocks.text.name",
  "limit": 5,
  "settings": [
    {
      "type": "richtext",
      "id": "content",
      "label": "t:blocks.text.content_label",
      "default": "<p>Welcome</p>"
    },
    {
      "type": "select",
      "id": "alignment",
      "label": "t:settings.alignment",
      "options": [
        { "value": "left", "label": "Left" },
        { "value": "center", "label": "Center" }
      ],
      "default": "left"
    }
  ]
}
```

## App Block Support

```json
"blocks": [
  { "type": "@app" }
]
```

This enables Shopify Apps to add their blocks via App Block API.

## Schema Validation Pre-Flight Checklist

Before deployment, verify:

- [ ] All ranges: `(max-min)/step ≤ 100`
- [ ] All range defaults: `min + n×step` AND `≤ max`
- [ ] All blocks have `{{ block.shopify_attributes }}` on root
- [ ] No trailing commas in JSON
- [ ] All brackets balanced
- [ ] All setting IDs unique within section
- [ ] All block types match block files in `/blocks/`
- [ ] All translation keys exist in `locales/en.default.schema.json`
- [ ] Color settings use checkbox toggle (not `!= blank`)
- [ ] Default values for text settings (avoid blank Customizer states)
- [ ] `presets` array has at least one entry
- [ ] No setting IDs change between versions (saved data lost)

## Common Schema Mistakes

| Mistake | Result | Fix |
|---------|--------|-----|
| Range crash: `step: 1, max: 500` | Customizer error | `(max-min)/step ≤ 100` |
| Wrong default: `min:30 step:5 default:33` | Schema error | Default on step grid |
| Missing `block.shopify_attributes` | Block not selectable | Add to root div |
| Trailing comma in JSON | JSON parse error | Remove trailing commas |
| Block type doesn't match file | Block missing | Match filename |
| Hardcoded English label | Multilingual broken | Use `t:` prefix |
| Color != blank check | Always true | Use checkbox toggle |
| No default value for text | Empty Customizer state | Add `default` |
| Setting ID change | Saved data lost | Don't rename, add new |
| `templates` deprecated | Warning | Use `enabled_on`/`disabled_on` |

## Locale Schema Labels

```json
// en.default.schema.json
{
  "names": {
    "section_name": "My Section",
    "block_name": "My Block"
  },
  "settings": {
    "layout": "Layout",
    "padding_top": "Top padding",
    "color_scheme": "Color scheme"
  },
  "options": {
    "grid": "Grid",
    "list": "List"
  },
  "blocks": {
    "text": {
      "name": "Text",
      "content_label": "Content"
    }
  }
}
```

## Validation Tools

- **Shopify Theme Check**: `shopify theme check`
- **JSON validator**: validate schemas before commit
- **Customizer test**: actually open Customizer and verify settings appear correctly
- **Multi-template test**: test section in all `enabled_on` templates
