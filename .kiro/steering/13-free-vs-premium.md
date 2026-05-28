---
inclusion: always
---

# Free Horizon vs Premium Themes — Feature Gap Reference

## Big Picture

```
FREE Horizon Theme = Maruti Alto (basic — chalti hai, kaam chalata hai)
PREMIUM Theme     = Mercedes S-Class (luxury — har feature, har comfort)

Both take you Point A → Point B
BUT experience zameen-aasmaan ka farq hai!
```

## File Count Comparison

| Folder | Free Horizon | Premium | Difference |
|--------|--------------|---------|------------|
| Sections | 42 | 100-180+ | 2-4x more |
| Blocks | 91 | 80-150+ | Similar+ |
| Snippets | 98 | 60-120+ | Similar |
| JS | 75 | 40-80+ | More features |
| CSS | 3 | 30-60+ | More variants |
| **Total** | **419** | **350-600+** | **More feature density** |

## Premium Themes List (with Specialty)

| Theme | Price | Specialty | Best For |
|-------|-------|-----------|----------|
| **Prestige** | $380 | Luxury editorial, image-first | Fashion, jewelry, high-end |
| **Impulse** | $380 | Conversion features, cart upsells | General ecommerce, growing stores |
| **Turbo** | $400 | Speed + scale | Large catalogs (1000+ products) |
| **Broadcast** | $380 | Content + marketing, video | Brands with story |
| **Flex** | $380 | Flexibility, 50+ section types | Unique stores, custom layouts |
| **Symmetry** | $380 | Clean minimal, grid layouts | Home goods, lifestyle |
| **Impact** | $380 | Visual storytelling, scroll animations | Premium DTC brands |
| **Enterprise** | $380 | B2B features, wholesale | B2B stores, large businesses |
| **Taiga** | $350 | Modern animations, dark mode | Modern brands, tech products |
| **Palo Alto** | $350 | Editorial/magazine, recipes | Food, beverage, lifestyle |
| **Concept** | $350 | Artistic, gallery-first | Art, design, photography |
| **Release** | $350 | Product launches, drops | Limited editions, sneakers |
| **Canopy** | $350 | Visual richness | Home decor |
| **Stiletto** | $350 | Fashion lookbook | Fashion |

## CATEGORY 1: HEADER

### Free Horizon Has (3 sections)
- header-group.json
- header.liquid
- header-announcements.liquid

### Premium Adds (8-15 features)

| Feature | What It Does | Themes |
|---------|--------------|--------|
| Mega Menu (advanced) | Full-width dropdown with images, collections, featured products | Prestige, Impulse, Broadcast |
| Multi-Row Header | 3 rows: top bar + logo + navigation | Symmetry, Enterprise |
| Transparent Header | Hero overlay transparent header | Prestige, Taiga, Impact |
| Sticky Header Variants | Always/scroll-up only/shrink modes | Flex, Turbo, Impulse |
| Header Search Drawer | Full-screen search overlay | Prestige, Impact, Canopy |
| Top Bar Section | Phone, email, social ABOVE announcement | Enterprise, Stiletto |
| Multi-Announcement | Multiple rotating with countdown | Broadcast, Impulse, Flex |
| Currency/Language Selector | Standalone for international | Prestige, Turbo |
| Header Promo Banner | Image banner inside header | Canopy, Local |
| Side Navigation | Vertical sidebar instead of top | Concept, Release |

### Visual Comparison

**FREE Horizon Header**:
```
┌──────────────────────────────────────────────────┐
│ Free shipping on orders over $50                 │  ← basic
├──────────────────────────────────────────────────┤
│ [Logo] Home | Shop | About    🔍 👤 🛒          │  ← single row
└──────────────────────────────────────────────────┘
```

**Premium Header (Prestige/Impulse)**:
```
┌──────────────────────────────────────────────────┐
│ +1-800-XXX | hello@store.com | EN/$USD          │  ← top bar
├──────────────────────────────────────────────────┤
│ FLASH SALE ENDS IN 02:34:11 — 30% OFF           │  ← countdown
├──────────────────────────────────────────────────┤
│            [LUXURY LOGO]                         │  ← centered
├──────────────────────────────────────────────────┤
│ Women | Men | Collections | Blog | About         │  ← nav row
├──────────────────────────────────────────────────┤
│ ┌──── MEGA MENU with images ────────────────────┐│
│ │ Categories | Featured Products | Collections   ││
│ └────────────────────────────────────────────────┘│
└──────────────────────────────────────────────────┘
```

### Revenue Impact

- Mega menu with images = **+15-25% category clicks**
- Countdown timer = **+10-30% conversion during sales**
- Multi-row professional = **+5-10% trust**

## CATEGORY 2: HERO/BANNER

### Free Horizon Has (3)
- hero.liquid
- slideshow.liquid
- layered-slideshow.liquid

### Premium Adds (8-15)

| Feature | What It Does |
|---------|--------------|
| Split Hero | 50/50 left image, right content |
| Video Hero (Full) | Autoplay background video with sound |
| Parallax Hero | Background slower than foreground |
| Countdown Hero | Banner with live countdown overlay |
| Before/After Slider | Drag to compare |
| Shoppable Hero | Hotspots with products on hero |
| Mosaic/Grid Hero | Multiple images grid |
| Story Hero | Scroll-triggered storytelling |
| 3D/Interactive Hero | Mouse-based animations |
| Animated Text Hero | Typing animation, fade effects |
| Kenburns Slideshow | Slow zoom in/out |
| Lookbook Hero | Multiple CTAs to different pages |

## CATEGORY 3: PRODUCT (BIGGEST DIFFERENCE!)

### Free Horizon Has (8)
- product-information, product-list, product-recommendations
- product-hotspots, featured-product, featured-product-information
- quick-order-list, section-rendering-product-card

### Premium Adds (15-30 features)

| Feature | Revenue Impact |
|---------|----------------|
| **Product Tabs** | +Organized = -confusion = +sales |
| **Size Chart Popup** | -20-30% returns |
| **Color Swatches** (visual) | +10-15% variant selection |
| **Image Zoom** (advanced) | +Customer confidence |
| **360° Product View** | +Trust on high-value |
| **Product Video Gallery** | +85% likely to buy |
| **Sticky Add to Cart** | +5-10% ATC rate |
| **Recently Viewed** | +Re-engagement |
| **Product Bundles** | +25-40% AOV |
| **Frequently Bought Together** | +Cross-sell |
| **Product Reviews Built-in** | +15-25% conversion |
| **Inventory Counter** ("Only 3 left!") | +8-15% conversion |
| **Delivery Estimator** | -Uncertainty |
| **Product Compare** | Better choice |
| **Quick View Modal** | +5-15% explore |
| **Upsell Popup** | +Last-moment cross-sell |
| **Trust Badges** | -Anxiety |
| **Back In Stock Notify** | +Recover lost sales |
| **Gift Wrapping** | +Extra revenue |
| **Product Customizer** | +Personalization |
| **Complementary Products** | +Curated cross-sell |
| **Pickup Availability** | +Omnichannel |

### Free vs Premium Product Page

**FREE**:
```
[Images] [Title] [Price] [Variants] [ATC]
[Description]
[Recommendations]
Revenue Potential: 70-80%
```

**PREMIUM (e.g., Impulse)**:
```
[Advanced Gallery + Zoom + Video]
[Title] [Reviews ★★★★★ (124)]
[Price] [SAVE 20% badge]
[Color Swatches]
[Size Chart →] [Size dropdown]
[Quantity] [ADD TO CART — sticky]
[Secure] [Free Ship] [Returns]
[Only 3 left!] [Delivery: Thursday]
─── TABS ───
[Description | Reviews | Shipping | FAQ]
─── BUNDLES ───
[Buy Together: Shirt + Pants + Belt = $129]
─── RECENTLY VIEWED ───
Revenue Potential: 95-100%
```

## CATEGORY 4: COLLECTION

### Free Horizon Has (4)
- main-collection, main-collection-list, collection-list, collection-links

### Premium Adds (8-15)

| Feature |
|---------|
| Advanced Filters Sidebar (multi-select, visual color filters) |
| Collection Banner (Custom hero per collection) |
| Sub-Collections (nested navigation) |
| Grid/List Toggle |
| Infinite Scroll |
| Collection Tabs (multiple collections in one section) |
| Quick Add from Grid |
| Sort + Filter Drawer (mobile) |
| Product Count Badge |
| Empty Collection State |
| Promotional Banner in Grid |

## CATEGORY 5: CONTENT

### Free Horizon Has (8)
- media-with-content, carousel, marquee, custom-liquid
- custom, divider, logo, section

### Premium Adds (20-40)

**Top 5 Most Important**:

| Feature | Revenue Impact |
|---------|----------------|
| **Testimonials/Reviews Slider** | +15-25% conversion (social proof) |
| **FAQ Accordion** | -40% support tickets |
| **Countdown Timer** | +10-30% during sales |
| **Icon List (USPs)** | +10-15% trust |
| **Popup (Email Capture)** | +5-10% email signups |

**Other Premium Content Sections**:
- Timeline/History
- Team Members Grid
- Map Section
- Image Comparison
- Video Section (advanced)
- Logo List/Partners
- Tabs Section
- Image Gallery/Masonry
- Press/Media Section
- Stats/Numbers Counter
- Comparison Table
- Newsletter Popup
- Announcement Popup
- Custom Form
- Multi-Column Content
- Scrolling Text (advanced)
- Collage Section
- Story Section (scroll-triggered)
- Age Verification Popup

## CATEGORY 6: CART

### Free Horizon Has (1)
- main-cart.liquid only

### Premium Adds (4-8) — HUGE Revenue Impact

| Feature | Revenue Impact |
|---------|----------------|
| **Cart Drawer/Sidebar** | -20-30% abandonment (no page leave) |
| **Cart Upsells** | +15-25% AOV |
| **Cart Progress Bar** ("Spend $20 more for FREE SHIPPING!") | +20% AOV |
| **Gift Wrap Option** | +Extra revenue |
| **Cart Note (Advanced)** | Better UX |
| **Cross-Sell in Cart** | +Last-moment sales |
| **Cart Discount Code** | Smoother UX |
| **Express Checkout Buttons** | -Less abandonment |

**Total Cart Revenue Potential**: +40-60% MORE revenue per session

### Premium Cart Drawer Visual

```
SLIDE-OUT CART DRAWER:
┌────────────────────────────────────────┐
│ Your Cart (3)              [✕]        │
│ ████████████████░░░░ $75/$100         │
│ "Spend $25 more for FREE SHIPPING!"  │
│                                        │
│ [Img] Blue Shirt - M    $45          │
│ [-] 1 [+]    [Remove]                 │
│ [Img] Running Shoes     $89          │
│                                        │
│ ─── YOU MIGHT ALSO LIKE ───           │
│ [Sock+$15] [Belt+$25] [Hat+$20]      │
│                                        │
│ ☐ Add gift wrapping (+$5)            │
│ Order note: [____________]            │
│                                        │
│ Subtotal: $134                        │
│ Discount: [CODE] [Apply]              │
│ [Apple Pay] [Google Pay]              │
│ [═══ CHECKOUT $134 ═══]               │
└────────────────────────────────────────┘
```

## CATEGORY 7: SEARCH

### Free Horizon Has (4)
- search-header, search-results, predictive-search, predictive-search-empty

### Premium Adds (6-10)

| Feature |
|---------|
| Full-Screen Search Overlay |
| Search with Filters (large catalogs) |
| Visual Predictive Search (with images) |
| Popular Searches (trending) |
| Search Collections (grouped) |
| Voice Search |
| Search Analytics Display |
| Smart "Did you mean...?" |
| Recent Searches |
| Grid/List Toggle on Results |

## CATEGORY 8: PAGES & UTILITIES

### Premium Adds

| Feature |
|---------|
| Contact Page Section (styled) |
| About Page Template |
| FAQ Page Section |
| Coming Soon Page (with countdown) |
| Maintenance Mode |
| Customer Account Pages |
| Wishlist Page |
| Order Tracking Page |
| Store Locator Page |
| Lookbook Page |
| 404 (Advanced — with search + popular) |
| Landing Page Template |
| Cart Notification Toast |
| Cookie Banner (GDPR) |
| Quick View Section |
| Age Gate |
| Back to Top Button |
| Loading Indicator |

## TOTAL Feature Comparison

| Feature | Free Horizon | Premium |
|---------|--------------|---------|
| Mega Menu | ✗ | ✓ |
| Countdown Timer | ✗ | ✓ |
| Cart Drawer | ✗ | ✓ |
| Cart Upsells | ✗ | ✓ |
| Free Ship Bar | ✗ | ✓ |
| Color Swatches | ✗ | ✓ |
| Size Chart | ✗ | ✓ |
| Image Zoom | Basic | ✓ Advanced |
| Sticky ATC | ✗ | ✓ |
| Quick View | ✗ | ✓ |
| Product Tabs | ✗ | ✓ |
| Reviews Built-in | ✗ | ✓ |
| FAQ Accordion | ✗ | ✓ |
| Testimonials | ✗ | ✓ |
| Popup/Modal | ✗ | ✓ |
| Instagram Feed | ✗ | ✓ |
| Infinite Scroll | ✗ | ✓ |
| Advanced Filters | ✗ | ✓ |
| Back in Stock | ✗ | ✓ |
| Wishlist | ✗ | ✓ |
| Product Bundles | ✗ | ✓ |
| Recently Viewed | ✗ | ✓ |
| Trust Badges | ✗ | ✓ |
| Multi-Row Header | ✗ | ✓ |
| Cookie Banner | ✗ | ✓ |
| Landing Pages | ✗ | ✓ |
| Lookbook | ✗ | ✓ |
| Store Locator | ✗ | ✓ |

## Cost Analysis: Free + Apps vs Premium

### Free Theme + 15 Apps Approach

| Feature | App | Monthly | Yearly |
|---------|-----|---------|--------|
| Cart Drawer + Upsells | Slide Cart/CartCandy | $10-30 | $120-360 |
| Countdown Timer | Hextom/Essential | $7-15 | $84-180 |
| Reviews | Judge.me/Loox | $0-25 | $0-300 |
| Email Popup | Privy/Klaviyo | $0-20 | $0-240 |
| Wishlist | Wishlist Plus | $10-50 | $120-600 |
| FAQ Accordion | HelpCenter | $5-10 | $60-120 |
| Instagram Feed | Instafeed | $6-15 | $72-180 |
| Quick View | Quick View | $5-10 | $60-120 |
| Product Bundles | Bundler | $10-30 | $120-360 |
| Back in Stock | Back in Stock | $10-20 | $120-240 |
| Recently Viewed | Also Viewed | $5-10 | $60-120 |
| Trust Badges | Trust Badges | $5-10 | $60-120 |
| Color Swatches | Swatch King | $5-15 | $60-180 |
| Size Chart | Kiwi Size Chart | $7-15 | $84-180 |
| Cookie Banner | Pandectes/Avada | $5-10 | $60-120 |
| **TOTAL** | **15 apps** | **$100-305/mo** | **$1200-3660/yr** |

### Premium Theme Approach
- **One-time**: $320-400
- **Yearly**: $0 (after purchase)
- **3-year cost**: $320-400 ONE TIME

### Savings Math
- Apps route 3 years: **$3,600 - $10,980**
- Premium route 3 years: **$320 - $400**
- **SAVINGS: $3,000 - $10,000+ over 3 years**

## Performance Impact: Apps vs Premium

### Free Theme + 15 Apps
- **Each app adds**: 1-3 JS files (50-200KB) + 1-2 CSS files (20-50KB) + API calls (100-500ms)
- **15 apps total**: 2.25MB extra JS, 450KB extra CSS, 3 seconds extra wait
- **Result**: PageSpeed 30-50 (POOR), Load time 5-8s, LCP 4-6s, CLS 0.2-0.5
- **SEO**: Google ranks slower sites lower

### Premium Theme (built-in)
- **All JS**: 1 optimized bundle (150-300KB total)
- **All CSS**: 1 optimized file (80-150KB total)
- **No external API calls**: Server-side Liquid
- **Result**: PageSpeed 80-95 (EXCELLENT), Load 1.5-3s, LCP 1.5-2.5s, CLS 0.01-0.05
- **SEO**: Higher rankings = more organic traffic

### Speed → Revenue Correlation
- **Every 1 second slower = 7% LESS conversions** (Amazon research)
- Free + apps (~6s) vs Premium (~2s) = 4 seconds faster
- **4 seconds × 7% = 28% MORE conversions on premium theme**

## Top 5 Features to Add (Revenue-Boosting)

If user has Free Horizon and wants premium-like results, prioritize:

1. **⏰ Countdown Timer** — +10-30% conversion during sales
2. **⭐ Testimonials/Reviews** — +15-25% conversion
3. **❓ FAQ Accordion** — -40% support tickets
4. **🎯 Icon List (USPs)** — +10-15% trust ("Free Shipping | Secure | Returns")
5. **🎉 Email Capture Popup** — +5-10% email signups

## Combined Revenue Impact Potential

If ALL premium features are added/built into Free Horizon:

```
Cart Drawer:           -20-30% abandonment
Free Shipping Bar:     +15-25% AOV
Cart Upsells:          +10-20% AOV
Countdown Timer:       +10-30% conversion
Color Swatches:        +10-15% selection
Quick View:            +5-15% explore
Sticky Add to Cart:    +5-10% ATC
Predictive Search:     +20-40% search conversion
Testimonials:          +15-25% overall conversion
FAQ Accordion:         -30-50% support tickets
Recently Viewed:       +5-10% return conversion
Mega Menu:             +15-25% category clicks
Product Bundles:       +25-40% AOV
Inventory Counter:     +8-15% conversion

COMBINED: +50-150% MORE REVENUE
```

## Decision Framework

### Stay with Free Horizon If:
- New store, low traffic, learning phase
- Simple product catalog
- Budget constrained
- Willing to add features incrementally

### Consider Premium If:
- 100+ products
- $10K+ monthly revenue
- Need conversion optimization
- Apps becoming expensive
- Performance issues

### Build Premium Features into Free Horizon If:
- Developer skills available
- Specific features needed (1-3 at a time)
- Want full control
- Cost-conscious long-term

## Key Lessons

1. **Free Horizon is solid foundation** — not "broken", just "basic"
2. **Premium themes pack revenue features** built-in
3. **Apps add cost + slow site down**
4. **Premium themes faster than free + apps**
5. **3-year math heavily favors premium**
6. **OR: Build features yourself** (best of both worlds)
