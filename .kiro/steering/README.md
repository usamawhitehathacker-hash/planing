# Kiro Steering — Shopify Horizon Theme v3.5.1 Memory Set

Yeh folder Kiro ki **persistent memory** hai. Har conversation mein automatically load hoti hai. Total **14 detailed steering files** organized by topic.

## File Index

### Core Identity & Architecture (always loaded)

| File | Role | Inclusion |
|------|------|-----------|
| `00-identity-and-rules.md` | Senior dev identity, operating rules, response format | always |
| `01-architecture-overview.md` | 419 files breakdown, render sequence, 8-layer architecture | always |
| `10-schema-rules.md` | All schema validation rules + setting types reference | always |
| `11-code-patterns.md` | Liquid/CSS/JS code patterns and recipes | always |
| `12-if-then-cascade.md` | Dependency impact reference, severity tiers | always |
| `13-free-vs-premium.md` | Free Horizon vs 14 premium themes feature gap | always |
| `14-godfather-mega-prompt.md` | **9,222-word God-Father Mega Prompt** — Premium theme architect agent with full anatomy of 14 premium themes, 140+ feature inventory, 8 code patterns, decision matrix | always |

### Folder-Specific (load when working in that folder)

| File | Folder | Inclusion Pattern |
|------|--------|-------------------|
| `02-layout-folder.md` | `layout/` (2 files) | `layout/**`, `**/theme.liquid` |
| `03-templates-folder.md` | `templates/` (13 files) | `templates/**` |
| `04-sections-folder.md` | `sections/` (42 files) | `sections/**` |
| `05-blocks-folder.md` | `blocks/` (91 files) | `blocks/**` |
| `06-snippets-folder.md` | `snippets/` (98 files) | `snippets/**` |
| `07-assets-folder.md` | `assets/` (113 files) | `assets/**` |
| `08-config-folder.md` | `config/` (2 files) | `config/**` |
| `09-locales-folder.md` | `locales/` (51 files) | `locales/**` |

## How It Works

- **Always-loaded files** (6): Foundational knowledge present in every conversation
- **File-matched files** (8): Auto-loaded when working on files in that folder

Total memory size: ~95KB structured Markdown.

## Quick Reference

### When to Use Which File

- **Starting a new task** → `00-identity-and-rules.md` (4-Phase protocol)
- **Understanding theme structure** → `01-architecture-overview.md`
- **Writing schema** → `10-schema-rules.md`
- **Writing Liquid/CSS/JS** → `11-code-patterns.md`
- **Assessing change impact** → `12-if-then-cascade.md`
- **Discussing theme upgrade** → `13-free-vs-premium.md`
- **Modifying specific folder** → Folder-specific file (02-09)

## Source Knowledge (in `/skill/skill/` folder of repo)

- `SHOPIFY_DEVELOPER_MEGA_PROMPT.md` (761 lines)
- `horizon theme Content overview.txt` (1,682 lines)
- `content 2.txt` (2,926 lines)
- `content 3.txt` (7,356 lines)
- `Data Shopify -0.txt` (foundation)

These steering files are the **distilled, structured form** of all that knowledge.

## File Statistics

```
16 files (15 steering + 1 README)
~245 KB total
~7,000 lines of organized expert knowledge
~29,000 words total
Covers all 419 files of Horizon theme
100+ IF-THEN scenarios
50+ code patterns
14 premium themes deeply analyzed (anatomy + signature features)
8 folder deep-dives
1 Godfather Mega Prompt (9,222 words)
140+ premium feature inventory
```

## The Godfather Mega Prompt (File 14)

The crown jewel — a 9,222-word self-contained mega prompt that turns me into **The Godfather Shopify Theme Architect**. When user invokes (e.g., "Mega prompt activate", "Premium plan banao", "[Theme] jaisa [feature]"), I produce structured plans with:

- Premium theme equivalence (which premium theme does this best)
- Free Horizon current state analysis
- File structure plan (CREATE/MODIFY/READ/AFFECTED)
- Cascade risk assessment
- Build sequence (step-by-step)
- Schema design
- Code blueprint
- Performance budget
- Acceptance criteria

Covers anatomy of: **Prestige, Impulse, Turbo, Flex, Broadcast, Symmetry, Enterprise, Canopy, Taiga, Palo Alto, Concept, Impact, Release, Stiletto, Local** + their signature philosophies.

## Maintenance

When new Shopify Horizon learning happens:
- Add to relevant folder file
- Update IF-THEN cascade if dependency discovered
- Add to code patterns if new pattern proven
- Don't bloat 00 (identity) — keep it core principles only

## Auto-Load Verification

In any conversation, Kiro automatically loads:
1. All `inclusion: always` files (6 files)
2. Files matching current working file (1-2 files based on path)

Result: Full Horizon expert knowledge ready for every task.
