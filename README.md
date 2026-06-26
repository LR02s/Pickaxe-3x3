# Peak Enchant — P3X3

Skript-based enchantment that adds a custom **PEAK** effect to pickaxes. When a player breaks a block, the surrounding 3x3x3 area is mined automatically.

Built with [Skript](https://github.com/SkriptLang/Skript), [SkBee](https://github.com/ShaneBeee/SkBee) and [PoaSK](https://www.spigotmc.org/resources/poask-skript-addon.104512/) — no compiled plugin required.

---

## Requirements

- Skript
- SkBee
- PoaSK

---

## Installation

1. Place `P3x3.sk` inside `plugins/Skript/scripts/`
2. Run `/sk reload P3x3.sk` or restart the server

---

## Commands

| Command | Description | Permission |
|---|---|---|
| `/p3e enchant` | Applies PEAK to the pickaxe you're holding | `p3e.mod` |
| `/p3e book` | Gives a Peak enchantment book | `p3e.mod` |
| `/p3e scene [player]` | Plays the enchantment animation on a player | `p3e.mod` |
| `/p3e wiki` | Opens the wiki link | `p3e.mod` |
| `/p3e version` | Shows the current version | `p3e.mod` |

Tab completion is included for all subcommands.

---

## How it works

1. Apply the enchant with `/p3e enchant` or combine a pickaxe with a Peak book in an anvil.
2. Breaking any block with the enchanted pickaxe also breaks the 26 surrounding blocks, skipping air and blacklisted blocks.
3. If `chanceDrill` is enabled, each break has a configurable chance of activating the 3x3 effect.
4. If `showParticles` is enabled, orange dust particles appear at each broken block.
5. If `realisticDurability` is enabled, each additional block costs 1 extra durability.
6. If `enableCooldown` is enabled, players must wait between activations.
7. If `restrictWorlds` is enabled, the effect is disabled in the specified world.
8. If `scene` or `anvilScene` is enabled, an enchantment animation plays when the enchant is applied.

---

## Configuration

Located at the top of the script under `options:`:

| Option | Type | Default | Description |
|---|---|---|---|
| `version` | string | `2.8` | Version shown by `/p3e version` |
| `prefix` | string | `[P3X3]>>` | Prefix used in messages |
| `nameEnchant` | string | `[OP] Peak` | Lore text added to enchanted pickaxes |
| `bookEnchant` | `true/false` | `true` | Enables the enchantment book system |
| `nameBook` | string | `Peak 3x3` | Display name of the enchantment book |
| `realisticDurability` | `true/false` | `false` | Extra durability loss per extra block broken |
| `blocksBlackList` | block | `bedrock` | Block immune to the 3x3 effect |
| `showParticles` | `true/false` | `true` | Orange particles at each broken block |
| `enableCooldown` | `true/false` | `false` | Enables a cooldown between uses |
| `peakCooldown` | duration | `5 seconds` | Cooldown duration |
| `restrictWorlds` | `true/false` | `false` | Disables the effect in a specific world |
| `BlackListWorlds` | string | `example_world` | World where the effect is disabled |
| `chanceDrill` | `true/false` | `false` | Enables a random chance for the 3x3 to activate |
| `drillChance` | number | `25` | Percentage chance (0–100) of activating the 3x3 |
| `useCustomModelData` | `true/false` | `false` | Applies custom model data to the enchanted pickaxe |
| `customModelDataID` | number | `1001` | Custom model data ID |
| `scene` | `true/false` | `false` | Enables the enchantment animation via command |
| `anvilScene` | `true/false` | `false` | Enables the animation when applied through an anvil |

---

## Notes

- The enchant is stored as lore text, not as a real Minecraft enchantment, so it's compatible with vanilla items.
- Only pickaxes are supported.
- A re-entry guard prevents recursive triggering when the 3x3 breaks blocks.
- The `chanceDrill` system rolls a random number each time a block is broken — if it exceeds `drillChance`, the 3x3 effect is skipped for that swing.

---

## License

MIT License — see [LICENSE](LICENSE) for details.
