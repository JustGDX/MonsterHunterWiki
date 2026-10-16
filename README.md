# MHW: Iceborne Wiki

**Live Website:** https://mhwiki.netlify.app/  
**Author:** GDX

A responsive, single-file HTML reference wiki for **Monster Hunter: World and Iceborne**. It brings weapon guides, combo inputs, monster information, armor details, weapon databases, and craftable-item references together in one browser-based tool.

## Overview

`mhw_wiki.html` runs entirely in the browser. Its data and rendering logic live inside the HTML file, so there is no build step, package installation, or backend server.

The interface uses a dark blue theme with icy-blue accents and adapts to desktop, tablet, and mobile screens.

## Features

### ⚔️ Weapons

- Browse all 14 weapon types.
- Open dedicated weapon detail views.
- Review weapon stats, including attack, affinity, element, sharpness, slots, and relevant weapon-specific properties.
- Read special-mechanic notes and matchup recommendations.
- Switch between **World** and **Iceborne** knowledge.
- View combo inputs for keyboard and mouse, PlayStation, and Xbox.
- Use visual key caps, mouse controls, controller labels, and tooltips to read inputs.
- Search weapon databases, filter by rarity, and browse paginated results.
- View recommended armor and craftable items where data is available.

### 🐉 Monsters

- Browse large and small monsters.
- Filter by expansion or monster group.
- Filter by recommended weapon type.
- Search monster names and available details.
- Open monster detail panels for additional information, including weaknesses and available hunt or reward data.
- Browse results with pagination.

### 🛡️ Armor

- Browse Low Rank, High Rank, and Master Rank armor sets.
- Filter by expansion, rank, rarity, or search text.
- Open armor set detail views.
- Review set bonuses, skills, materials, and individual armor-piece stats, including defense, slots, and resistances where available.

### 🧪 Items

- Browse craftable items and item references.
- Filter by expansion and item category.
- Review rarity, crafting recipes, acquisition notes, and usage information where available.
- Browse paginated results with adjustable page sizes.

## Getting Started

1. Save `mhw_wiki.html` to your computer.
2. Open the file in Chrome, Firefox, Edge, or Safari.
3. Use the tabs and filters to find the information you need.

No installation or local server is required. Most content works offline because the data and application logic are embedded in the HTML file.

**Offline note:** The page requests the Google Fonts `Cinzel` stylesheet for its display font. Without internet access, the browser falls back to the available serif fonts.

## Project Structure

The project is contained in one HTML file:

```text
mhw_wiki.html
├── HTML structure
│   ├── Header and branding
│   ├── Weapons tab
│   ├── Monsters tab
│   ├── Armor tab
│   └── Items tab
├── CSS styles
│   ├── Base layout and components
│   ├── MHW-inspired theme
│   └── Clean-theme overrides
└── JavaScript
    ├── Weapon definitions and combo data
    ├── Monster data
    ├── Armor data
    ├── Weapon database
    ├── Item data and fallbacks
    └── Rendering, filtering, pagination, and initialization
```

## Input Mapping Reference

The wiki uses the following general input labels as a reference. Specific combos and actions may differ by weapon, game version, and control configuration.

| Action | Keyboard & Mouse | PlayStation | Xbox |
|---|---|---|---|
| Light attack | Left Mouse Button (LMB) | Triangle | Y |
| Heavy attack | Right Mouse Button (RMB) | Circle | B |
| Both buttons | LMB + RMB | Triangle + Circle | Y + B |
| Special / guard | Mouse side button | R2 | RT |
| Aim | Depends on weapon and mapping | L2 | LT |
| Evade | Spacebar | Cross (×) | A |
| Movement | WASD | Left Stick | Left Stick |
| Item / ammo selection | Mouse Wheel | D-pad | D-pad |

Check the combo table for the selected weapon. The table's displayed controls serve as the main reference, and your in-game control settings might differ.

## Data and Accuracy Notes

The wiki combines weapon, monster, armor, and item information into an offline reference. Some recommendations and notes reflect compiled community guidance or testing, rather than official CAPCOM rankings.

- Weapon stats and crafting information aim to represent *Monster Hunter: World: Iceborne* data where available.
- Monster weaknesses and weapon matchups should be treated as reference guidance, not universal rankings for every build or player.
- Some database entries contain incomplete fields.
- Sharpness bars use a condensed representation and might not match the exact length of an in-game sharpness gauge.
- Some item `usedFor` fields might be blank.
- The weapon database uses compact positional tuples. Check `WDB_COLS` and `renderWdb()` in the HTML source to understand each weapon type's column layout.
- The monster weapon filter matches the text stored in each entry. Results depend on the weapon names used in the filter options and data.

If you find inaccurate or missing information, verify it against the game or a trusted community reference before relying on it.

## Customization

The data and UI are embedded in `mhw_wiki.html`. Edit the relevant JavaScript data structures to change entries, then test the file in a browser.

### Add a weapon definition

Add an entry to the `weapons` object using the same structure as an existing weapon. Fields used by the project include:

`name`, `icon`, `role`, `stats`, `specialMechanics`, `strongAgainst`, `weakAgainst`, `worldKnowledge`, `iceborneKnowledge`, `combos`, `fullComboList`, `mainCombo`, `armor`, and `craftables`.

Use an existing entry as the schema reference before adding fields.

### Add a monster

Add a monster object to `monsters[]`, following the structure of existing entries. For example:

```js
{
  name: "Frostfang Barioth",
  expansion: "iceborne",
  type: "Flying Wyvern",
  weakness: "Fire ⭐⭐⭐",
  secondary: "—",
  bestWeapon: "Long Sword · Dual Blades · Bow",
  notes: "Freezing breath"
}
```

Keep values consistent with the names and categories expected by the filters.

### Add an armor set

Add an entry to `ARMOR_DB` or `armorItems`, depending on which view you want to populate. Follow the fields used by nearby entries, such as `name`, `icon`, `expansion`, `rarity`, `rank`, `setBonus`, `skills`, `bestFor`, `materials`, `pieces`, `weapons`, and `items`.

### Add an item

Append an entry to `EMBEDDED_ITEMS` using the same format as the existing item records. Example:

```js
{
  id: 9999,
  name: "Mega Dash Juice",
  expansion: "world",
  category: "Potion",
  rarity: "Rare 4",
  craftable: "Yes",
  recipe: "Dash Juice + Catalyst → x1",
  obtain: "Craft (combine ingredients)",
  usedFor: "Reduces stamina depletion."
}
```

Treat these examples as format examples. Confirm game-specific recipe and item details before publishing them.

### Change the theme

The CSS variables in `:root` control the main colors, including `--gold`, `--gold2`, `--ember`, `--line`, and related variables. The `clean-theme` style block near the end of the document overrides parts of the earlier decorative theme. Edit or remove those overrides if you want to change the appearance.

## Browser Support

The wiki is designed for current versions of Chrome, Firefox, Edge, and Safari. It uses standard browser features, including:

- CSS Grid and Flexbox
- CSS custom properties
- JavaScript for filtering, pagination, and dynamic detail views
- The CSS `:has()` selector for certain table layout rules

Most wiki data does not require a network connection. The Google Fonts stylesheet is an optional external request.

## Disclaimer

This is an unofficial fan project. *Monster Hunter* is a trademark of CAPCOM. This project is not affiliated with, endorsed by, or sponsored by CAPCOM.

## License

For personal and community use. Check the applicable rights and source terms before redistributing the project or its compiled data. Do not present this wiki as an official CAPCOM product.

## Credits

- **CAPCOM**, for *Monster Hunter: World* and *Iceborne*.
- Community wiki editors and guide authors whose work informed the compiled reference data.
- **Google Fonts**, for the Cinzel typeface.

---

*Built by GDX for the Monster Hunter: World and Iceborne community.*
