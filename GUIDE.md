# Quick guide

**F8** opens Weaver. **Fullscreen / Restore** changes the window size. Players use **/kit**, **/travel**, and the Quest journal.

## WeaverEditor

Choose a colored node, then set its type inside the card. Connect an output to an input. Right-click removes a wire; Undo restores it. Drag titles to move nodes, middle-drag to pan, and scroll to zoom.

Dialogue is NPC speech; Options are player replies. A Dialogue output can connect to several Options. Conditions use True and False. Actions with two outputs use True for success and False for failure. Wait accepts seconds such as **1.5**. Enter or Tab finishes typing; Shift+Enter adds a line.

Use **Publish & link** to connect the graph to a saved NPC or zone. **Debug draft** steps through the graph and explains branch results. **Preview as player** shows the conversation without admin roles. Both use copied state and simulated world actions; live inventory and progress stay untouched. Debugger controls let you try full inventories, blocked travel and encounter outcomes. **Live test on me** runs the published graph in the real world.

Import JSON files from `BepInEx/config/VariantWeaver/exports`. New exports include link names. Imports match unique names and ask you to resolve missing or ambiguous links. Positions and wires are preserved; **Arrange** tidies the layout. Moving and arranging nodes in a saved graph keeps their positions automatically. Save a new graph as a draft first.

## World tools

- **Placement:** Q/E rotates; hold Shift for 15-degree steps. G toggles a 1m grid. Page Up/Down adjusts height. Hold Left Alt to drag move/rotate handles; T returns to aiming. Click saves; Shift-click keeps placing a copy. Esc returns to Weaver.
- **History:** undo recent NPC, chest, zone and spawner edits, including deletions. Undo preserves player progress and refuses to overwrite newer edits.
- **Inspect:** shows player identity and known building creators. Older creators become known when they join. Other platforms show their platform ID. Esc returns to Weaver.
- **World markers:** shows nearby zones and spawner eggs with the menu closed.
- **World → Encounters:** choose a creature and reward kit to create a linked spawner, zone, chest and graph. The chest unlocks after the encounter is cleared and locks again on restart.

## NPCs and quests

NPC routines can use sitting or working poses, nearby greetings and patrol points. Add points at your position or enter coordinates. Paths are straight: keep them clear of walls. NPCs pause while talking and when nobody is nearby.

**Give Quest** uses a quest key, name and instructions. Add an optional tracked item, target count, map destination and timer. **Handoff Quest** continues at another NPC. Use the same quest key for quest conditions and completion.

Players can track up to three active quests and turn map destinations on in the journal. Item counts show current inventory; the graph decides when the quest completes. Timers continue offline.

## Events and installation

Spawners fire through graphs, zones or manual triggers. Surviving Weaver enemies are cleared on restart without loot; restart cleanup does not award victory rewards. Chest keys can be regular items or personal, single-use Weaver keys.

Server settings default to 200 active Weaver creatures and 40 new creatures per second. A blocked spawner follows False. Graphs share a work budget and continue on later ticks when busy.

Install matching mod builds and content mods on the server and clients. When updating, replace the mod DLLs and keep `BepInEx/config/VariantWeaver` intact. Back up that folder along with the Valheim world; it holds graphs, links, kits, travel and player progress. If an older build already cleared a link, select its NPC or zone and use **Publish & link** once after updating.
