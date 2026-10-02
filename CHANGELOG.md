# Changelog

## 1.2.1

- Separate server settings can block Weaver travel while encumbered or carrying non-teleportable items. Both default off.
- Covers warps, /return, player teleports, bring requests and graph travel, including admins.
- Rechecks the travelling player's inventory after approval and before moving.
- Shows blocked-travel reasons and preserves return points when blocked.
- Keeps normal portals, themes, trader menus and quest HUD behavior unchanged.

Update the server or host and every client together.

Beta, provided as-is, with frequent updates to come.

## 1.2.0

- Valheim-themed player and admin menus, five personal themes and updated portal, supply-chest and quest-scroll icons.
- Redesigned travel, kit and quest pages with clearer cards and item previews.
- Themed quest tracker with Esc-dragging, saved position, scale, width, opacity and display options.
- Item-icon traders with quantities, prices, search, filters and exchange confirmation.
- /warp replaces /travel. /return remembers only the last successful Weaver departure point.
- /tp, Teleport to player and Bring player here require the existing teleport permission and the other player's approval.
- Accept / Deny popup, Esc to deny, a 30-second expiry and repeat-request limits.

Update the server or host and every client together. Keep both DLLs and preserve existing configuration and world data.

## 1.1.9

- Cleaner menus with rounded frames, clearer selection and collapsible settings.
- Searchable world objects and compact kit editing with icons and quantities.
- Equal-sized nodes, graph navigation, group selection, minimap and clickable errors.
- Visible save status and local draft recovery. Optional server draft autosave.
- NPC appearance previews, smoother patrols and clearer player kits, travel and cooldowns.
- Configurable server rules, kit limits and storage cleanup with backups.

Update the server and every client together.

Beta, provided as-is, with frequent updates to come.

## 1.1.8

- Raised the world content limit to 8 MB, adjustable up to 16 MB on the server.
- Compressed larger transfers to fix the repeated 1 MB warning when saving, publishing or refreshing.
- Expanded the guide with setup steps, examples and Pippi creator credit.

Update the server and every client together.

## 1.1.7

- Weaver travel is blocked during combat and for 20 seconds afterward.
- Includes NPC, graph and admin teleports. Normal portals are unchanged.
- Blocked trips keep their cooldown ready. Teleport actions follow False.

## 1.1.6

- Fixed NPC conversations and quest actions failing for some players on servers.
- Moving nodes no longer causes a publishing conflict.
- Save conflicts refresh the server view while keeping your edits.

## 1.1.5

- Fixed NPC and zone links being overwritten by open editors.
- Saved graphs show their linked NPC or zone when reopened.
- Arrange and moving nodes now save their positions.
- Added Inspect identities, graph previews, world undo, quest tracking and NPC routines.
- Added encounter tools and server performance limits.

## 1.1.4

- Colored node shortcuts, a searchable graph list, inline editing and True/False outputs.
- Fixed overlapping inspector controls, node deletion and NPC dialogue links.
- Smoother dialogue, decimal waits, timed quests and improved graph connections.
- Eight personal keys for chests and quests. Fixed refill timers after changing one-time rewards.
- Spawners require a trigger. Restart cleanup drops no loot; normal kills support up to 1,000 loot items.
- World markers, zone previews and inspection with Weaver closed. Improved inventory viewing.
- Ghost mode passes through objects, with or without Server Devcommands. Front arrows help place NPCs and chests.

## 1.1.3

- Fixed buttons and nodes losing their backgrounds during play.

## 1.1.2

- Cleaner menus, fullscreen editing and rounded nodes.
- Edit settings inside nodes and connect multiple Options to Dialogue.
- Clearer quest fields, node hints and connection checks.
- Separate Travel & Kits menu, with /travel and /kit shortcuts.
- Improved NPC conversations and zone events for players.
- Fixed menu input; move freely while placing objects. NPC size now supports 10×.

## 0.1.2

- Fixed stuck NPCs after deletion and expanded inventory viewing.

## 0.1.1

- Fixed selection windows, dragging and input after switching away from the game.

## 0.1.0

- First beta: WeaverEditor, NPCs, quests, events, spawners, chests and admin tools.
