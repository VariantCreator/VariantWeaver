# Getting started with Weaver

Press **F8** after joining a world. Use the menu to create your NPCs, spawners, chests and event zones.

## WeaverEditor

- Click an output pin, then an input pin to connect two nodes. Right-click cancels a connection in progress.
- Drag nodes to move them. Middle-drag pans the graph; the mouse wheel zooms.
- Select a node to change its settings. Conditions have True and False paths; dialogue can have several choices.
- Save a draft while working. Publish when you're ready to use it in the world.
- Link the published graph to an NPC, zone or schedule.

## A quest from one NPC to another

1. Create and place two NPCs. Give them names and choose their appearance.
2. Open the **NPC quest handoff** template in WeaverEditor.
3. Select the destination NPC in **HandoffQuest**. Connect **At next NPC** to the next part of your quest.
4. Publish the graph, then choose it under the first NPC's **On interaction** field and save the NPC.

The quest waits until that player talks to the destination NPC. Renaming the NPC later won't break the link. Players can check their waiting quests in **Quests**.

## A boss fight with a reward chest

1. Create a loot kit in **Community**.
2. Create a spawner, choose the boss and its stats, and place the egg marker. Set **Maximum alive** to **1** for a single boss. Choose a loot kit if the boss should drop specific items.
3. Create and name an event chest. Choose its reward kit, lock access and enable damage protection. Add a required key if you want one.
4. Connect **TriggerSpawner → WaitSpawnerClear → SetChestLocked** in your graph. Turn the chest's lock off in the last node.
5. Use the False paths for cooldown, busy-encounter or timeout messages. Publish and link the graph to your NPC or event zone.

To make the chest destructible after the fight, add **ProtectChest** and turn protection off. Keep protection on if the chest should stay for other players.

For personal quest rewards, set a Player-scope variable when the quest finishes and use that variable as the chest's quest requirement. A chest's lock and damage protection are shared; its quest requirement and reward claims can be per player.

## Useful details

- Click a selection field to search items, creatures or appearances. Drag the popup by its title bar.
- Place objects by aiming at the ground and clicking. **Q/E** rotates; **Escape** cancels.
- Choose **Add** loot to keep normal drops, or **Replace** to use only your kit. Changes to a spawner affect future spawns.
- Set a cooldown or check a quest variable near the start of a graph to prevent repeat rewards.
- NPCs are stationary and invulnerable. Use spawners for combat creatures.
- The catalog refreshes as mods register content. You can also rescan from **Mods**. Everyone needs the content mods used by your quests.
- Change the menu key in `BepInEx/config/com.variantmods.weaver.cfg` after the first launch.
- Keep a backup of your world's Weaver data in `BepInEx/config/VariantWeaver` when moving servers.
