# Peak Enchant

Lightweight Skript-based plugin that adds a custom pickaxe enchantment called **PEAK**. When a player breaks a block with an enchanted pickaxe, the surrounding blocks in a 3x3x3 area are broken automatically as well, making mining faster without needing tools like WorldEdit.

Built entirely with [Skript](https://github.com/SkriptLang/Skript), [SkBee](https://github.com/ShaneBeee/SkBee) and [PoaSK](https://www.spigotmc.org/resources/poask-skript-addon.104512/)— no compiled plugin, no extra dependencies.

## Requirements

- Skript
- SkBee (only needed if particle effects are enabled)

## Installation

1. Place the script file inside your `plugins/Skript/scripts/` folder
2. Run `/sk reload P3x3.sk` or restart the server
3. Make sure the script is enabled (not in the `-disabled` folder)

## Commands

| Command | Description | Permission |
|---|---|---|
| `/p3e enchant` | Applies the PEAK enchant to the pickaxe you're holding | `p3e.mod` |
| `/p3e book` | Gives you a Peak enchantment book (if enabled) | `p3e.mod` |
| `/p3e version` | Shows the current plugin version | `p3e.mod` |
| `/p3e wiki` | To see the complete wiki for the full script | `p3e.mod` |
| `/p3escene` | Play enchantment animation and enchant | `p3e.mod` |

Tab completion is included for all subcommands.

## Permissions

- `p3e.mod` — grants access to the `/p3e` command. Without it, players will see the configured permission message and won't be able to use the command.

## How it works

1. Apply the enchant to a pickaxe using `/p3e enchant`, or combine a pickaxe with a Peak book in an anvil (if `bookEnchant` is enabled). The pickaxe must not already have the enchant, and you must be holding it.
2. Once enchanted, breaking any block with that pickaxe will also break the 26 surrounding blocks (a 3x3x3 area centered on the mined block), skipping air and any blacklisted blocks.
3. If `showParticles` is enabled, orange dust particles appear at each extra block broken (requires SkBee).
4. If `realisticDurability` is enabled, each additional block broken consumes 1 extra durability point from the pickaxe.
5. If `enableCooldown` is enabled, players must wait the configured time between activations.
6. If `restrictSpawnWorld` is enabled, the 3x3x3 effect is disabled in the specified world.

## Configuration

Located at the top of the script under `options:`:

| Option | Type | Description |
|---|---|---|
| `version` | string | Version number shown by `/p3e version` |
| `nameEnchant` | string | Lore text added to enchanted pickaxes (also used to detect them) |
| `bookEnchant` | `true`/`false` | Enables the enchantment book system |
| `nameBook` | string | Display name of the enchantment book |
| `realisticDurability` | `true`/`false` | Extra durability loss per additional block broken |
| `showParticles` | `true`/`false` | Orange dust particles per broken block (requires SkBee) |
| `enableCooldown` | `true`/`false` | Enables a cooldown between uses |
| `peakCooldown` | duration | Cooldown duration (e.g. `5 seconds`) |
| `blocksBlackList` | block list | Blocks immune to the 3x3x3 effect (e.g. `bedrock and spawner`) |
| `restrictSpawnWorld` | `true`/`false` | Disables the effect in a specific world |
| `spawnWorldName` | string | Name of the world where the effect is restricted |

## Notes

- The enchant is stored as lore text on the item, not as a real Minecraft enchantment, so it's compatible with vanilla items and doesn't conflict with other enchant systems.
- Only pickaxes are supported; other tools won't trigger the area-mining effect.
- The book system allows players to apply the enchant via an anvil, combining a pickaxe with a Peak book obtained through `/p3e book`.
- A re-entry guard (`{__p3e::%uuid%}`) prevents recursive triggering when the 3x3 breaks blocks.

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.
