# Variant Weaver

[Download Variant Weaver 0.1.1 beta](https://github.com/VariantCreator/VariantWeaver/releases/download/v0.1.1/VariantMods-VariantWeaver-0.1.1.zip)

Build your own quests and events in Valheim. Place characters around your world, give them conversations, send players on adventures, and set up boss fights with rewards.

**This is a beta, provided as-is, with frequent updates to come.**

## What you can do

- **WeaverEditor:** connect nodes to build quests and events, with dialogue choices and True/False branches.
- **Custom NPCs:** choose names, appearance, clothing and size. Link conversations and pass quests from one NPC to another.
- **Event zones:** run your graphs when players enter, leave or stay inside an area.
- **Boss spawners:** place an egg marker, choose a creature, and set its size, health, damage, loot and cooldown.
- **Event chests:** name reward chests, require a key or quest progress, and protect them until your event is finished.
- **Admin tools:** manage players, items, travel points, kits, server messages and permissions.

Weaver picks up items and creatures registered by your installed mods. It also works without companion content mods. Mods with unusual custom systems may need extra support.

## Getting started

Install BepInExPack Valheim, then import the ZIP into your mod manager. For a manual install, copy the included `plugins/VariantWeaver` folder into `BepInEx/plugins`.

**Install the same Weaver version on the server or host and every player's client.** Keep both included DLL files together. When updating manually, replace the old files.

Join a world and press **F8**. The host and server admins have full access. Other players can use quests, conversations and public rewards; editing and admin actions require permission. Admins can grant specific permissions through Roles.

Start with a template in WeaverEditor, connect your nodes, publish the graph, then link it to an NPC or event zone. See `GUIDE.md` for a quest example and editor controls.
