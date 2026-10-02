# Variant Weaver 1.2.1

Build quests and events in Valheim with WeaverEditor, NPCs, item-icon traders, spawners and reward chests. Includes admin tools, travel points and kits.

**Beta, provided as-is, with frequent updates to come.**

[Download 1.2.1](https://cdn.hexium.gg/upload/1630/1.2.1.zip) · [Hexium](https://valheim.hexium.gg/mods/VariantMods/VariantWeaver) · [Guide](GUIDE.md) · [Changelog](CHANGELOG.md) · [Earlier GitHub releases](https://github.com/VariantCreator/VariantWeaver/releases)

## What's new

- Separate server options to block Weaver travel while encumbered or carrying non-teleportable items. Both default off.
- Player teleports ask the other player to accept or deny. No response means no teleport.
- Valheim-themed player and admin menus, five personal themes, and a quest tracker you can move by pressing Esc and dragging.
- Portal, supply-chest and quest-scroll icons. Trader menus show supported exchanges with item icons, quantities, prices and confirmation.

## Quick controls

**F8** opens Weaver. Players get Travel, Kits, Quests and Appearance; admins get the full tools.

**/warp** opens warps, **/kit** opens kits, and **/return** returns to the departure point of your last successful Weaver teleport. Normal portals do not replace that point.

**/tp PlayerName**, **Teleport to player** and **Bring player here** require admin access or `players.teleport`, plus approval from the other player.

## Optional travel rules

In the server or host's `BepInEx/config/com.variantmods.weaver.cfg`, under the existing section:

```ini
[Server rules]
Block travel while encumbered = true
Block travel with non-teleportable items = true
```

Restart the server or host after editing. These independent options cover warps, returns, player teleports, bring requests and graph travel, including admins. The travelling player's inventory is checked just before moving, including after approval. Normal portals are unchanged.

## Installation

Install **1.2.1 on the server or host and every client**. Keep both DLLs together and remove duplicate older copies. Preserve `BepInEx/config/VariantWeaver` and `com.variantmods.weaver.cfg` when updating. Install BepInExPack Valheim first.

Personal appearance settings are available under **Appearance** for players and **Settings → Appearance** for admins. Shared rules belong in the host's config.

Inspired by [Pippi — User & Server Management](https://steamcommunity.com/sharedfiles/filedetails/?id=880454836) for Conan Exiles, created by **Joshtech (CoOkIeMoNsTeR)**.
