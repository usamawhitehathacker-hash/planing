---
inclusion: fileMatch
fileMatchPattern: ['layout/**', '**/theme.liquid', '**/password.liquid']
---

# Folder 1: layout/ — Foundation (2 files)

## Role

Layout files **ghar ka dhanca** hain — har page ke around wrapper. Yeh `theme.liquid` har page ka starting point hai.

## Files

| # | File | Role | Use |
|---|------|------|-----|
| 1 | `theme.liquid` | Main wrapper — HAR page isse guzarta hai | Always (normal pages) |
| 2 | `password.liquid` | Store password page wrapper | Sirf store band hone pe |

## File 1: theme.liquid (MOST IMPORTANT FILE)

### Structure

```liquid
<!DOCTYPE html>
<html>
<head>
  ├── Favicon (settings.favicon)
  ├── {% render 'meta-tags' %}              → SEO tags
  ├── {% render 'stylesheets' %}            → CSS load
  ├── {% render 'fonts' %}                  → Google/Shopify fonts
  ├── {% render 'scripts' %}                → JS modules + import map
  ├── {% render 'theme-styles-variables' %} → CSS vars from settings
  ├── {% render 'color-schemes' %}          → 6 color schemes CSS
  └── {{ content_for_header }}              → Shopify system scripts
</head>

<body>
  ├── {% sections 'header-group' %}
  │     ├── sections/custom.liquid (custom announcement)
  │     ├── sections/header-announcements.liquid
  │     └── sections/header.liquid
  │
  ├── <main>
  │     {{ content_for_layout }}            → Template ka content
  │   </main>
  │
  ├── {% sections 'footer-group' %}
  │     ├── sections/footer.liquid
  │     └── sections/footer-utilities.liquid
  │
  ├── {% render 'search-modal' %}           → Hidden search overlay
  └── {% render 'quick-add-modal' %}        → Hidden quick add popup
</body>
</html>
```

### Connections (10-20+ files)

```
theme.liquid
├── LOADS:
│   ├── assets/base.css (via snippets/stylesheets)
│   ├── assets/overflow-list.css (preloaded)
│   ├── assets/component.js (modulepreload)
│   ├── assets/utilities.js (modulepreload)
│   ├── assets/events.js (modulepreload)
│   ├── assets/focus.js (modulepreload)
│   ├── assets/morph.js (modulepreload)
│   ├── assets/scrolling.js (modulepreload)
│   ├── assets/section-renderer.js (modulepreload)
│   └── assets/section-hydration.js (modulepreload)
│
├── RENDERS:
│   ├── snippets/meta-tags.liquid
│   ├── snippets/stylesheets.liquid
│   ├── snippets/fonts.liquid
│   ├── snippets/scripts.liquid
│   ├── snippets/theme-styles-variables.liquid
│   ├── snippets/color-schemes.liquid
│   ├── snippets/skip-to-content-link.liquid
│   ├── snippets/search-modal.liquid
│   └── snippets/quick-add-modal.liquid
│
├── SECTIONS:
│   ├── sections/header-group.json (3 sections inside)
│   └── sections/footer-group.json (2 sections inside)
│
└── READS:
    └── config/settings_data.json (logo, colors, fonts, layout)
```

### WHY This File Is Critical

1. **Every page passes through it** — so changes affect entire site
2. **CSS/JS loaded once here** — browser caches for all pages
3. **Shopify system injection** — `{{ content_for_header }}` for app scripts, currency, etc.
4. **Section groups orchestration** — header/footer consistency
5. **Performance foundation** — modulepreload, lazy load, view transitions

### IF-THEN Logic

```
IF: theme.liquid mein font load kiya
THEN: Poori website pe font change

IF: CSS load remove kiya from theme.liquid
THEN: Poori site ka style toot jayega — plain HTML

IF: Footer section group hatao
THEN: Koi page pe footer nahi dikhega

IF: {{ content_for_header }} remove kiya
THEN: Shopify apps + analytics + checkout DEAD
→ CRITICAL: NEVER REMOVE

IF: {{ content_for_layout }} remove kiya
THEN: Pages ka actual content nahi dikhega
→ CRITICAL: NEVER REMOVE

IF: Skip-to-content link hata diya
THEN: Accessibility violation (WCAG 2.1)

IF: Modulepreload remove kiya
THEN: JS modules slowly load → poor performance
```

## File 2: password.liquid

### Role

Store password-protected hone pe yeh wrapper use hota hai.

### When Activated

- Admin → Online Store → Preferences → Password page enabled
- Sirf jab tak store officially launch nahi kiya

### Structure (Simpler Than theme.liquid)

```liquid
<!DOCTYPE html>
<html>
<head>
  ├── Favicon
  ├── Stylesheets (minimal)
  ├── Fonts
  └── Meta tags
</head>
<body>
  ├── sections/password.liquid (password form)
  ├── {{ content_for_layout }}
  └── sections/password-footer.liquid (minimal footer)
</body>
</html>
```

### Connections

```
password.liquid
├── RENDERS:
│   ├── sections/password.liquid
│   └── sections/password-footer.liquid
├── USES:
│   └── snippets/password-layout-styles.liquid
└── READS:
    └── config/settings_data.json (logo)
```

### IF-THEN Logic

```
IF: password.liquid delete kiya
THEN: Password page break — store band hone pe error

IF: Password form action change kiya
THEN: Customers password enter nahi kar payenge → store unreachable
```

## Key Reminders

1. **`theme.liquid` is sacred** — bahut careful editing
2. **Modulepreload optimization** — core JS files preload hote hain
3. **Skip-to-content link** — accessibility ke liye mandatory
4. **Search/Quick-add modals** — hidden by default, JS opens them
5. **Section groups** (`header-group`, `footer-group`) — JSON files, not liquid
6. **`{{ content_for_header }}` and `{{ content_for_layout }}`** — Shopify system tokens, NEVER remove
