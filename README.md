# Peak Enchant

Lightweight Skript-based plugin that adds a custom pickaxe enchantment called **PEAK**. When a player breaks a block with an enchanted pickaxe, the surrounding blocks in a 3x3x3 area are broken automatically as well, making mining faster without needing tools like WorldEdit.

Built entirely with [Skript](https://github.com/SkriptLang/Skript) and [SkBee](https://github.com/ShaneBeee/SkBee) — no compiled plugin, no extra dependencies.

## Requirements

- Skript
- SkBee (only needed if particle effects are enabled)

## Installation

1. Place the script file inside your `plugins/Skript/scripts/` folder
2. Run `/sk reload P3x3-0_5.sk` or restart the server
3. Make sure the script is enabled (not in the `-disabled` folder)

## Commands

| Command | Description | Permission |
|---|---|---|
| `/p3e enchant` | Applies the PEAK enchant to the pickaxe you're holding | `p3e.mod` |
| `/p3e version` | Shows the current plugin version | `p3e.mod` |

Tab completion is included for both subcommands.

## Permissions

- `p3e.mod` - grants access to the `/p3e` command. Without it, players will see the configured permission message and won't be able to use the command.

## How it works

1. Apply the enchant to a pickaxe using `/p3e enchant`. The pickaxe must not already have the enchant, and you must be holding it (can't be empty-handed or holding a non-pickaxe item).
2. Once enchanted, breaking any block with that pickaxe will also break the 26 blocks surrounding it (a 3x3x3 area centered on the block you mined), as long as those blocks aren't air.
3. If `showParticles` is enabled, orange dust particles will appear at each extra block broken (requires SkBee).
4. If `realisticDurability` is enabled, each additional block broken will consume 1 extra durability point from the pickaxe.

## Configuration

Located at the top of the script under `options:`

- `version` - the version number displayed by `/p3e version`
- `nameEnchant` - the text added to the pickaxe's lore to mark it as enchanted (also used to identify enchanted tools)
- `realisticDurability` - `true`/`false`, enables extra durability loss per block broken
- `showParticles` - `true`/`false`, enables particle effects per block broken (requires SkBee)

## Notes

- The enchant is stored as lore text on the item, not as a real Minecraft enchantment, so it's compatible with vanilla items and doesn't conflict with other enchant systems.
- Only pickaxes are supported; other tools won't trigger the area-mining effect.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
