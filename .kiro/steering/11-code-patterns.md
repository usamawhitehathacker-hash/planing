---
inclusion: always
---

# Code Patterns — Liquid + CSS + JS Reference

## Standard Section Template

```liquid
{%- liquid
  assign section_id = section.id
  assign color_scheme = section.settings.color_scheme
  assign padding_top = section.settings.padding_top
-%}

<div
  id="section-{{ section_id }}"
  class="section section-[name] color-{{ color_scheme }}"
  style="--padding-top: {{ padding_top }}px;"
  {{ section.shopify_attributes }}
>
  <div class="container">
    {%- if section.settings.heading != blank -%}
      <h2 class="section-heading">{{ section.settings.heading }}</h2>
    {%- endif -%}

    <div class="section-blocks">
      {%- for block in section.blocks -%}
        {%- case block.type -%}
          {%- when 'text' -%}
            <div class="block block-text" {{ block.shopify_attributes }}>
              {{ block.settings.content }}
            </div>
          {%- when 'button' -%}
            <div class="block block-button" {{ block.shopify_attributes }}>
              {% render 'button',
                 label: block.settings.label,
                 url: block.settings.url,
                 style: block.settings.style %}
            </div>
          {%- when '@app' -%}
            {% render block %}
        {%- endcase -%}
      {%- endfor -%}
    </div>
  </div>
</div>

{% stylesheet %}
  /* Scoped CSS — section-specific styles */
{% endstylesheet %}

<script src="{{ 'my-section.js' | asset_url }}" type="module"></script>

{% schema %}
{
  "name": "t:names.section_name",
  "tag": "section",
  "class": "section-my-section",
  "settings": [],
  "blocks": [
    { "type": "text" },
    { "type": "button" },
    { "type": "@app" }
  ],
  "presets": [
    {
      "name": "t:names.section_name",
      "blocks": [{ "type": "text" }]
    }
  ]
}
{% endschema %}
```

## Liquid Patterns

### Snippet Render with Variables

```liquid
{%- render 'product-card',
    product: product,
    show_price: true,
    show_swatches: false,
    image_size: 'medium'
-%}
```

### Conditional Rendering

```liquid
{%- if image != blank -%}
  {% render 'image', image: image %}
{%- else -%}
  <div class="placeholder">No image</div>
{%- endif -%}
```

### Loop with Index

```liquid
{%- for product in collection.products -%}
  <div class="product-card" data-index="{{ forloop.index }}">
    {{ product.title }}
  </div>
{%- endfor -%}
```

### Case/When

```liquid
{%- case block.type -%}
  {%- when 'text' -%}
    <p>{{ block.settings.content }}</p>
  {%- when 'image' -%}
    {% render 'image', image: block.settings.image %}
  {%- else -%}
    <!-- fallback -->
{%- endcase -%}
```

### Variable Assignment

```liquid
{%- liquid
  assign heading = section.settings.heading | default: 'Default Heading'
  assign image_url = product.featured_image | image_url: width: 800
  if section.settings.layout == 'grid'
    assign grid_class = 'layout-grid'
  else
    assign grid_class = 'layout-list'
  endif
-%}
```

## Image Rendering Pattern (CRITICAL!)

### Safe Image Render

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
      widths: '300, 600, 900, 1200, 1500',
      class: 'img-responsive'
  }}
{%- endif -%}
```

### Hero Image (eager loading!)

```liquid
{{
  hero_image
  | image_url: width: 2000
  | image_tag:
    loading: 'eager',     {# CRITICAL — never lazy for hero! #}
    fetchpriority: 'high', {# Boost LCP #}
    alt: hero_image.alt | escape,
    width: hero_image.width,
    height: hero_image.height,
    sizes: '100vw',
    widths: '600, 900, 1200, 1500, 2000'
}}
```

### Via Image Snippet (Preferred)

```liquid
{% render 'image',
   image: product.featured_image,
   width: 800,
   height: 600,
   lazy: true,
   class: 'product-img' %}
```

## Video Pattern

```liquid
{%- if video != blank -%}
  <video
    autoplay
    muted          {# REQUIRED for autoplay! #}
    loop
    playsinline    {# Mobile inline play #}
    poster="{{ poster_image | image_url: width: 1200 }}"
  >
    <source src="{{ video.sources[0].url }}" type="{{ video.sources[0].mime_type }}">
  </video>
{%- endif -%}
```

## Translation Pattern

```liquid
{# Basic #}
{{ 'actions.add_to_cart' | t }}

{# With variable #}
{{ 'products.low_stock_html' | t: count: variant.inventory_quantity }}

{# Multiple variables #}
{{ 'cart.items_count' | t: count: cart.item_count, total: cart.total_price | money }}
```

## CSS Patterns

### Section Scoping (CRITICAL!)

```css
#shopify-section-{{ section.id }} {
  /* All section CSS scoped here */
}

#shopify-section-{{ section.id }} .my-class {
  /* Nested selectors */
}
```

### CSS Custom Properties from Settings

```liquid
<div
  class="section"
  style="
    --section-padding-top: {{ section.settings.padding_top }}px;
    --section-padding-bottom: {{ section.settings.padding_bottom }}px;
    --section-bg-color: {{ section.settings.background_color }};
  "
>
```

```css
.section {
  padding-top: var(--section-padding-top, 24px);
  padding-bottom: var(--section-padding-bottom, 24px);
  background-color: var(--section-bg-color, transparent);
}
```

### Color Scheme Application

```liquid
<div class="section color-{{ section.settings.color_scheme }}">
```

```css
.color-scheme-1 {
  background: var(--color-background-1);
  color: var(--color-text-1);
}
```

### Responsive Patterns

```css
/* Mobile-first */
.grid {
  display: grid;
  grid-template-columns: 1fr;  /* Mobile: 1 column */
  gap: 16px;
}

@media (min-width: 750px) {
  .grid {
    grid-template-columns: repeat(2, 1fr);  /* Tablet: 2 columns */
    gap: 24px;
  }
}

@media (min-width: 990px) {
  .grid {
    grid-template-columns: repeat(4, 1fr);  /* Desktop: 4 columns */
    gap: 32px;
  }
}
```

### Marquee Animation Pattern

```css
@keyframes marquee {
  from { transform: translateX(0); }
  to { transform: translateX(-50%); }
}

.marquee__content {
  animation: marquee 20s linear infinite;
}

@media (prefers-reduced-motion: reduce) {
  .marquee__content {
    animation: none;
  }
}
```

### Background Media Pattern

```css
.section-with-background {
  position: relative;
  overflow: hidden;
}

.section-with-background__media {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  z-index: -1;
}

.section-with-background__overlay {
  position: absolute;
  inset: 0;
  background: rgba(0, 0, 0, 0.4);
  z-index: 0;
}

.section-with-background__content {
  position: relative;
  z-index: 1;
}
```

## JavaScript Patterns

### Web Component Pattern (Horizon Style)

```javascript
import { Component } from '@theme/component';

class MyFeature extends Component {
  connectedCallback() {
    super.connectedCallback();
    this.init();
  }

  init() {
    this.button = this.querySelector('[data-button]');
    this.button?.addEventListener('click', this.handleClick.bind(this));
  }

  handleClick(event) {
    event.preventDefault();
    // Logic here
  }

  disconnectedCallback() {
    super.disconnectedCallback();
    // Cleanup
  }
}

customElements.define('my-feature', MyFeature);
```

### Use in Liquid

```liquid
<my-feature data-product-id="{{ product.id }}">
  <button data-button>Action</button>
</my-feature>
```

### Event Bus Pattern

```javascript
import { eventBus } from '@theme/events';

// Listen
eventBus.on('cart:updated', (data) => {
  console.log('Cart updated', data);
});

// Emit
eventBus.emit('cart:updated', { count: 3 });
```

### AJAX Cart Add

```javascript
async function addToCart(variantId, quantity = 1) {
  try {
    const response = await fetch('/cart/add.js', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify({
        items: [{
          id: variantId,
          quantity: quantity
        }]
      })
    });

    if (!response.ok) throw new Error('Cart add failed');

    const data = await response.json();
    eventBus.emit('cart:updated', data);
    return data;
  } catch (error) {
    console.error('Cart add error:', error);
  }
}
```

### AJAX Cart Update

```javascript
async function updateCartQuantity(lineKey, quantity) {
  const response = await fetch('/cart/change.js', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ id: lineKey, quantity })
  });
  return await response.json();
}
```

### Predictive Search Pattern

```javascript
class PredictiveSearch extends Component {
  constructor() {
    super();
    this.timeout = null;
    this.debounceMs = 300;
  }

  onInput(searchTerm) {
    clearTimeout(this.timeout);
    this.timeout = setTimeout(() => {
      this.fetchResults(searchTerm);
    }, this.debounceMs);
  }

  async fetchResults(query) {
    if (!query || query.length < 2) return;

    try {
      const response = await fetch(
        `/search/suggest.json?q=${encodeURIComponent(query)}` +
        `&resources[type]=product,collection,article` +
        `&resources[limit]=4`
      );
      const data = await response.json();
      this.renderResults(data);
    } catch (error) {
      console.error('Search error:', error);
    }
  }

  renderResults(data) {
    // DOM manipulation
  }
}
```

### Section Rendering API

```javascript
async function renderSection(sectionId, params = {}) {
  const url = new URL(window.location);
  url.searchParams.set('section_id', sectionId);
  Object.entries(params).forEach(([key, value]) => {
    url.searchParams.set(key, value);
  });

  const response = await fetch(url.toString());
  const html = await response.text();

  const tempDiv = document.createElement('div');
  tempDiv.innerHTML = html;

  return tempDiv.querySelector(`#shopify-section-${sectionId}`);
}
```

### Variant Change Handler Pattern

```javascript
class VariantPicker extends Component {
  connectedCallback() {
    super.connectedCallback();
    this.addEventListener('change', this.onVariantChange.bind(this));
  }

  onVariantChange(event) {
    const selectedVariant = this.getSelectedVariant();

    // 1. Update price
    eventBus.emit('variant:changed', {
      variant: selectedVariant,
      price: selectedVariant.price
    });

    // 2. Update gallery
    if (selectedVariant.featured_image) {
      this.updateGallery(selectedVariant.featured_image);
    }

    // 3. Update availability
    if (!selectedVariant.available) {
      this.disableAddToCart();
    } else {
      this.enableAddToCart();
    }

    // 4. Update URL (without reload)
    const url = new URL(window.location);
    url.searchParams.set('variant', selectedVariant.id);
    window.history.replaceState({}, '', url);
  }
}
```

### IntersectionObserver Lazy Loading

```javascript
const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      // Load content
      this.loadSection(entry.target);
      observer.unobserve(entry.target);
    }
  });
}, {
  rootMargin: '100px'
});

document.querySelectorAll('[data-lazy-section]').forEach(section => {
  observer.observe(section);
});
```

### Form Submission Pattern

```javascript
async function submitForm(form) {
  const formData = new FormData(form);

  try {
    const response = await fetch(form.action, {
      method: form.method,
      body: formData
    });

    if (!response.ok) throw new Error('Form submission failed');

    const data = await response.json();
    return data;
  } catch (error) {
    console.error('Form error:', error);
    throw error;
  }
}
```

## Schema Snippet Reuse Pattern

```liquid
{# In section #}
{% render 'snippet-with-multiple-params',
   product: product,
   show_price: true,
   show_swatches: false,
   image_size: 'medium',
   click_target: '_blank' %}
```

## Performance Patterns

### Conditional JS Loading

```liquid
{%- if section.settings.enable_carousel -%}
  <script src="{{ 'slideshow.js' | asset_url }}" type="module"></script>
{%- endif -%}
```

### Critical CSS Inline

```liquid
{# In section for above-fold content #}
<style>
  /* Critical styles only */
  .hero { /* ... */ }
</style>

{# Below-fold can use external CSS #}
<link rel="stylesheet" href="{{ 'below-fold.css' | asset_url }}">
```

### Preload Critical Assets

```liquid
{%- if template == 'product' -%}
  <link rel="modulepreload" href="{{ 'product-form.js' | asset_url }}">
  <link rel="modulepreload" href="{{ 'variant-picker.js' | asset_url }}">
{%- endif -%}
```

## Accessibility Patterns

### Skip to Content Link

```liquid
<a href="#main-content" class="skip-to-content-link">
  {{ 'general.accessibility.skip_to_content' | t }}
</a>

<main id="main-content" tabindex="-1">
  {{ content_for_layout }}
</main>
```

### ARIA for Dynamic Content

```liquid
<div
  aria-live="polite"
  aria-atomic="true"
  class="cart-notification"
>
  <!-- Content updated by JS -->
</div>
```

### Button vs Link

```liquid
{# Use button for actions #}
<button type="button" aria-label="{{ 'actions.close' | t }}">
  <svg>...</svg>
</button>

{# Use anchor for navigation #}
<a href="/collections/all">View all</a>
```
