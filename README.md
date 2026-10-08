# MHW: Iceborne Wiki

A self-contained, single-file HTML wiki for **Monster Hunter World: Iceborne**, covering weapons, combos, monsters, armor sets, and craftable items. No build step, no dependencies, no server required — just open the file in a browser.

---

## Overview

`mhw_wiki.html` is a standalone, offline-capable reference tool for MHW: Iceborne players. It bundles all data (weapon stats, combo inputs, monster weaknesses, armor skills, item recipes) directly into the HTML as JavaScript objects and embedded JSON, so it works entirely client-side.

The UI is styled with a dark, MHW-inspired theme (bronze/gold accents, Cinzel display font) and is fully responsive down to mobile widths.

---

## Features

### ⚔️ Weapons Tab
- 14 weapon types (Great Sword → Heavy Bowgun), each with a dedicated detail page
- Per-weapon **stats table** (attack, affinity, element, sharpness, slots, phial/shelling/coatings where applicable)
- **Special mechanics** list with auto-highlighted multipliers and percentages
- **Matchup cards** — strong vs. weak monsters
- **World vs. Iceborne knowledge** toggle (version tabs)
- **Combo table** with three input columns:
  - Keyboard & Mouse (SVG mouse glyphs, key caps)
  - PlayStation (PS5) face buttons and triggers
  - Xbox equivalent buttons
- **Full weapon database** per type with search + rarity filter and pagination (50 per page)
- Recommended armor and craftable items per weapon

### 🐉 Monsters Tab
- 94 monsters (71 large + 23 small)
- Filter by **expansion** (World / Iceborne / Small)
- Filter by **best weapon type**
- Full-text search across name, type, weakness, best weapon, and notes
- Paginated table (50 per page)

### 🛡️ Armor Tab
- Master Rank, High Rank, and Low Rank sets
- Filters: expansion, rank (LR/HR/MR), rarity (1–12), and search
- Detail pages with set bonuses, skills, materials, and per-piece breakdown (defense, skills, slots, resistances)

### 🧪 Items Tab
- Craftable items with category icons, rarity badges, recipes, and acquisition notes
- Filters: expansion, category (Potions, Seeds, Traps, Bombs, Ammo, Coatings, Materials, Mantles, Tools, Misc)
- Adjustable page size (25 / 50 / 100 / 200)

---

## Getting Started

1. Save `mhw_wiki.html` anywhere on your machine.
2. Double-click it, or drag it into any modern browser (Chrome, Firefox, Edge, Safari).
3. No installation, no internet connection required.

> **Note:** The only external request is the Google Fonts `Cinzel` stylesheet. If offline, the page gracefully falls back to `Trajan Pro`/`Georgia`/serif.

---

## File Structure

Everything lives in a single file:

```

svgsvg

mhw_wiki.html
├── \<style> ×3 — base theme, MHW bronze theme, clean-theme override
├── \<header> — crest logo, title, subtitle
├── .tabs — Weapons / Monsters / Armor / Items
├── #weaponsTab — weapon grid + dynamic detail pages
├── #monstersTab — filterable monster table
├── #armorTab — filterable armor grid + detail pages
├── #itemsTab — filterable item table
└── \<script> — all data + rendering logic
├── weapons{} — 14 weapon definitions
├── monsters[] — 94 monster entries
├── armorItems[] — base armor list
├── ARMOR_DB[] — full armor set database
├── WEAPON_DB{} — per-type weapon tables
├── EMBEDDED_ITEMS[] — item database
├── fallbackItems[] — offline fallback
└── render/init functions

text

````
---

## Input Mapping Reference

| Action | Keyboard | PlayStation | Xbox |
|---|---|---|---|
| Light attack | Left Mouse | Triangle | Y |
| Heavy attack | Right Mouse | Circle | B |
| Both buttons | LMB + RMB | Triangle + Circle | Y + B |
| Special / guard | Mouse side button | R2 | RT |
| Aim | — | L2 | LT |
| Evade | Spacebar | Cross (×) | A |
| Movement | WASD | Left Stick | Left Stick |
| Item/ammo select | Mouse Wheel | D-pad | D-pad |

Combo tables render these as clickable-looking glyphs with tooltips; non-keyboard players can use the PS/Xbox columns directly.

---

## Data Sources

- Monster weaknesses, hitzones, and best-weapon recommendations compiled from community guides and in-game testing.
- Weapon stats, sharpness, and crafting trees reflect Iceborne (Master Rank) values where available.
- Armor set bonuses and skills reflect the base game + Iceborne expansion.
- Item recipes and acquisition methods drawn from in-game crafting and gathering data.

> **Disclaimer:** This is an unofficial fan project. Monster Hunter is a trademark of CAPCOM. Not affiliated with or endorsed by CAPCOM.

---

## Customization

### Adding a weapon
Append an entry to the `weapons` object with the same shape as existing entries (`name`, `icon`, `role`, `stats`, `specialMechanics`, `strongAgainst`, `weakAgainst`, `worldKnowledge`, `iceborneKnowledge`, `combos`, `fullComboList`, `mainCombo`, `armor`, `craftables`).

### Adding a monster
Push an object into `monsters[]`:
```js
{ name:"Frostfang Barioth", expansion:"iceborne", type:"Flying Wyvern",
  weakness:"Fire ⭐⭐⭐", secondary:"—", bestWeapon:"Long Sword · Dual Blades · Bow",
  notes:"Freezing breath" }
````

svgsvg

### Adding an armor set

Push an object into `ARMOR_DB` (or `armorItems`) with `name`, `icon`, `expansion`, `rarity`, `rank`, `setBonus`, `skills`, `bestFor`, `materials`, `pieces[]`, `weapons[]`, `items[]`.

### Adding an item

Append to `EMBEDDED_ITEMS` using the display format:

js

```
{ id: 9999, name:"Mega Dash Juice", expansion:"world", category:"Potion",
  rarity:"Rare 4", craftable:"Yes", recipe:"Dash Juice + Catalyst → x1",
  obtain:"Craft (combine ingredients)", usedFor:"Greatly reduces stamina depletion." }
```

svgsvg

### Theming

Colors are CSS variables in `:root` (`--gold`, `--gold2`, `--ember`, `--line`, etc.). The `clean-theme` style block at the bottom overrides the decorative bronze theme with a minimal flat look — remove or comment it out to restore the full MHW aesthetic.

---

## Browser Support

Tested on current versions of Chrome, Firefox, Edge, and Safari. Uses:

- CSS Grid / Flexbox
- CSS custom properties
- `:has()` selector (used in `.table-wrap:has(...)` for min-width tuning — degrades gracefully)
- `Intl`-free, no `fetch` required at runtime

---

## Known Limitations

- Sharpness bars are rendered from condensed `"r,o,y,g,b,w,p"` values scaled to 4 units per color, so the total may not equal a real sharpness gauge length.
- Some `usedFor` fields in the late-game Iceborne material entries are empty (`—`); these were not documented at compile time.
- The weapon database uses a compact tuple format (positional columns) to keep the file size reasonable — read `WDB_COLS` and the `renderWdb()` function to understand column order per weapon type.
- Monster "Best Weapon" filter matches against the literal string, so it works best with the exact weapon names listed in the dropdown.

---

## License

Personal/community use. Data is compiled from publicly available community resources. Do not redistribute as an official CAPCOM product.

---

## Credits

- **CAPCOM** — Monster Hunter World: Iceborne
- Community wikis and guide authors whose data informed the monster matchups and weapon stats
- Google Fonts — Cinzel typeface

---

**Author: GDX**
