# Peak Enchant — P3X3

Skript-based enchantment that adds a custom **PEAK** effect to pickaxes. When a player breaks a block, the surrounding 3x3x3 area is mined automatically.

Built with **Skript** and **SkBee** (used for reading/writing the persistent NBT tag that marks enchanted items) — no compiled plugin required.

## Requirements

- Skript
- SkBee

## Installation

1. Place the script file inside `plugins/Skript/scripts/`
2. Run `/sk reload <filename>.sk` or restart the server

## Commands

| Command | Description | Permission |
|---|---|---|
| `/pe enchant` | Applies PEAK to the pickaxe you're holding | `pe.mod` |
| `/pe book` | Gives a Peak enchantment book | `pe.mod` |
| `/pe wiki` | Opens the wiki link | `pe.mod` |

Tab completion is included for all subcommands (`enchant`, `book`, `wiki`).

> The permission node is configurable via `permission-need` (default `pe.mod`).

## How it works

- Apply the enchant with `/pe enchant`, give it via `/pe book`, or (if `bookEnchant` is enabled) combine a plain pickaxe with a Peak book in an anvil — the anvil repair cost is set to 0.
- The enchant is not a real Minecraft enchantment: it's tracked with a persistent NBT tag (`p3e_peak`, via SkBee) and shown cosmetically as lore text on the item, so it stays compatible with vanilla items.
- Breaking any block with an enchanted pickaxe also breaks the 26 surrounding blocks in a 3x3x3 cube, skipping air blocks, blacklisted blocks, and any block the player isn't allowed to build/break at.
- If `chanceDrill` is enabled, each block break rolls a random chance (`drillChance`) of triggering the 3x3 effect; otherwise it always triggers.
- If `particles` is enabled, orange dust particles appear at each broken block.
- If `durability` is enabled, the tool takes 1 extra durability point of damage for each additional block broken.
- If `Cooldown` is enabled, players must wait `peakCooldown` between activations.
- If `restrictWorlds` is enabled, the effect is disabled in the world(s) listed in `blackListWorlds`.
- A re-entry lock (`p3e::lock::<uuid>`) prevents recursive triggering while the 3x3 area is being broken.
- Only pickaxes are supported.

## Configuration

Located at the top of the script under `options:`.

| Option | Type | Default | Description |
|---|---|---|---|
| `prefix` | string | `&6&l[P3X3]&f>>` | Prefix used in plugin messages |
| `permission-need` | string | `pe.mod` | Permission required to use `/pe` subcommands |
| `blocksBlackList` | comma-separated list | `bedrock, barrier, end_portal_frame` | Block types immune to the 3x3 effect |
| `particles` | true/false | `false` | Orange dust particles at each broken block |
| `durability` | true/false | `false` | Extra durability loss per extra block broken |
| `enchantName` | string | `&6&lOP &7ᴘɪᴄᴋᴀxᴇ 3x3` | Cosmetic lore text added to enchanted pickaxes |
| `bookEnchant` | true/false | `true` | Enables giving/applying the enchant via book + anvil |
| `Cooldown` | true/false | `false` | Enables a cooldown between activations |
| `peakCooldown` | duration | `5 seconds` | Cooldown duration |
| `restrictWorlds` | true/false | `false` | Disables the effect in specific worlds |
| `blackListWorlds` | comma-separated list | `example_world` | World(s) where the effect is disabled |
| `chanceDrill` | true/false | `false` | Enables a random chance for the 3x3 to activate |
| `drillChance` | number | `25` | Percentage chance (0–100) of activating the 3x3 |
| `useCustomModelData` | true/false | `false` | Applies custom model data to the enchanted pickaxe |
| `customModelDataID` | number | `1001` | Custom model data ID |
| `craftingBook` | true/false | `true` | Registers a shaped crafting recipe for the Peak book |

## Crafting recipe

When `bookEnchant` and `craftingBook` are both enabled, a shaped recipe is registered for the enchanted book:

```
Emerald | Air     | Emerald
Air     | Book    | Air
Emerald | Air     | Emerald
```

## Notes

- The enchant is stored as an NBT tag plus cosmetic lore, not as a real Minecraft enchantment, so it's compatible with vanilla items.
- Only pickaxes are supported; other tools are rejected by validation.
- Blocks and worlds in the blacklists accept comma-separated lists (e.g. `bedrock, barrier, end_portal_frame`).
- The `chanceDrill` system rolls a random number for each triggering block break — if it's greater than `drillChance`, the 3x3 effect is skipped for that break.

## License

MIT License — see LICENSE for details.
