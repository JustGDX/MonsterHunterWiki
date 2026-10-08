
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
