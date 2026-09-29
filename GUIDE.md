# Variant Weaver guide

Build conversations, quests and events in Valheim with WeaverEditor.

**Beta, provided as-is, with frequent updates to come.**

[Getting started](https://github.com/VariantCreator/VariantWeaver/blob/main/GUIDE.md#getting-started) · [Menus](https://github.com/VariantCreator/VariantWeaver/blob/main/GUIDE.md#menu-and-editor) · [Shared settings](https://github.com/VariantCreator/VariantWeaver/blob/main/GUIDE.md#shared-settings) · [First NPC](https://github.com/VariantCreator/VariantWeaver/blob/main/GUIDE.md#your-first-npc-conversation) · [Nodes](https://github.com/VariantCreator/VariantWeaver/blob/main/GUIDE.md#nodes-and-connections) · [Quests](https://github.com/VariantCreator/VariantWeaver/blob/main/GUIDE.md#quests-and-timers) · [Events](https://github.com/VariantCreator/VariantWeaver/blob/main/GUIDE.md#spawners-zones-and-chests) · [World tools](https://github.com/VariantCreator/VariantWeaver/blob/main/GUIDE.md#world-tools) · [Imports](https://github.com/VariantCreator/VariantWeaver/blob/main/GUIDE.md#sharing-graphs) · [Server settings](https://github.com/VariantCreator/VariantWeaver/blob/main/GUIDE.md#server-settings-and-backups) · [Troubleshooting](https://github.com/VariantCreator/VariantWeaver/blob/main/GUIDE.md#troubleshooting)

## Getting started

1. Install BepInExPack Valheim, then import the Weaver ZIP into your mod manager.
2. Install the **same Weaver build on the server or host and every client**. Keep `VariantWeaver.dll` and `VariantWeaver.Core.dll` together.
3. Join a world and press **F8**. Server admins and players with assigned permissions can edit content. Other players get Travel & Kits and their quest journal.

For manual installation, copy the ZIP's `plugins/VariantWeaver` folder into `BepInEx/plugins`. Everyone also needs the content mods used by your graphs. Weaver reads the items and creatures registered by installed mods; use **Mods → Rescan** if an entry is missing.

| Control | What it does |
| --- | --- |
| **F8** | Open Weaver or the player menu |
| **/travel** | Open public travel points |
| **/kit** | Open public kits |
| **Fullscreen / Restore** | Expand the editor or return to its window |
| **Esc** | Close a player window, or leave placement, inspection or a zone preview |

Create travel points under **Travel** and kits under **Community**. Mark them public if players should see them in their menu. They can still be used as graph actions without appearing there.

## Menu and editor

NPCs, zones, chests and spawners have a searchable browser with enabled and linked status. Select an object to open its settings; expand **Browse** to choose another. Your unsaved object edits stay available while switching within the session.

**Community → Kits** has a compact item list. Search, change quantities directly, or select an item to change it. **Merge duplicate items** combines matching entries. Save stays at the bottom of the panel. Kits allow 60 rows and 1,000 items per row by default; the server owner can change those limits.

WeaverEditor keeps the current graph name and save state visible. Use the arrows to go back and forward, or **Graphs** to search All, Recent, Linked or Draft graphs. Names such as `Tavern / Greeter` group related graphs.

- All nodes use the same size by default. Longer settings scroll inside the node.
- Shift-click or drag empty space to select nodes. Drag a title to move the selection.
- **Select branch** selects the connected path. Copy/paste keeps connections between copied nodes; reconnect any outside links.
- Align a selection into a row or column. Use the minimap to move around large graphs.
- Click a validation result to find its node. Missing connections appear red.
- Collapse the inspector for more space. Edit node settings directly inside the cards.
- **Connections / Used by** opens related graphs and world objects.

Local draft recovery saves while you edit and does not publish anything. **Recovered drafts** also finds new graphs that were never saved to the server. Compare with the server copy before saving recovered work. Publishing and linking stay manual.

**Settings** controls text size, accent colour, visible rows, node dimensions, minimap, previews and recovery. Server draft autosave is optional and off by default. The server can disable it.

Players can expand a kit to see its items and icons. Travel and kit buttons show their own remaining cooldowns. NPC appearance previews let admins rotate the model before placing it.

## Shared settings

The config is created at `BepInEx/config/com.variantmods.weaver.cfg` after Weaver starts.

| Section | Settings |
| --- | --- |
| Menu appearance | Text size, accent, collapsed sections, browser rows, previews and details |
| Editor preferences | Equal node sizes, dimensions, selection tools, minimap, inspector, local recovery and optional server autosave |
| Server rules | Public travel/kits, NPC conversations, previews, inspection, admin powers, debug/devcommands, draft autosave and history cleanup |
| Storage | World content limit, saved revision limit and revisions retained per graph after cleanup |
| Server performance | Active creatures and spawns per second |

Change **Server rules**, **Storage** and **Server performance** on the server or host, then restart it. Clients cannot override server rules. Weaver's debug/devcommands setting controls its own buttons; other mods keep their own controls. Normal portals are unchanged.

**History → World storage** shows the space used by published graphs, drafts, revisions and player state. Only the server owner can clean earlier revisions. Cleanup first saves the full world file under `BepInEx/config/VariantWeaver/backups`; current graphs, drafts and links are kept.

## Your first NPC conversation

1. Open **NPCs → New NPC**. Give it a name, choose its appearance, then place and save it.
2. Open **WeaverEditor** and create a graph. Add an **Origin**, **Dialogue**, **Option** and **Action** node.
3. Type the NPC's speech inside Dialogue and the player's reply inside Option. Set the Action's type to **Close Dialogue**.
4. Connect the nodes in this order:

   ```text
   Origin → Dialogue → Option → Action: Close Dialogue
   ```

5. Set **Starts from** to **Linked NPC**. Under **Link to**, choose **NPC conversation** and select your saved NPC.
6. Click **Validate**, then **Publish & link**. Close Weaver, face the NPC and press **E** to talk.

**Save draft** keeps your work without replacing the live conversation. **Publish** updates the live graph; **Publish & link** also assigns it to the chosen NPC or zone. The NPC's **On interaction** field shows its saved graph.

To add choices, connect one Dialogue output to several Option nodes. Each Option continues along its own connection after the player selects it.

## Nodes and connections

Choose a colored node shortcut, then edit its settings inside the card. **Action** and **Condition** have a type dropdown for their different jobs.

| Node | Use it for |
| --- | --- |
| **Origin** | The graph's starting point |
| **Dialogue** | What the NPC says |
| **Option** | A reply the player can select |
| **Condition** | Check items, funds, quests, flags, roles, timers or values |
| **Action** | Give rewards, trade, warp, change quest progress or trigger world objects |
| **Wait** | Pause for seconds, including decimals such as `1.5` |
| **Randomiser** | Choose one connected path at random |
| **Bounce** | Jump to a matching Land elsewhere in the graph |
| **Comment** | Leave a note; it does not run |
| **Repeat / Call Graph** | Run a bounded loop or call another published graph |

Click an **output pin**, then an **input pin** to connect them. Conditions use **True** when the check passes and **False** when it fails. Actions with True/False outputs use them for success and failure. Add a failure message where players need to know why something could not happen.

Dialogue continues through its output automatically; an Option waits for a player response. A Wait after Dialogue delays the next step. Several connections on a normal output can run several branches; use Options for player choices and Randomiser for a random choice.

| Editing | Control |
| --- | --- |
| Move a node | Drag its title |
| Pan / zoom | Middle-drag / mouse wheel |
| Remove a connection | Right-click its wire |
| Finish typing | Enter or Tab; Shift+Enter adds a line |
| Tidy the graph | Arrange, then Fit graph |
| Reverse an edit | Undo / Redo |

Node positions save automatically for saved graphs. Save a new graph as a draft first.

### Try a graph before publishing

- **Debug draft** lets you step through the graph and inspect branch results.
- **Preview as player** runs without admin roles. Preview controls can simulate inventory, travel and encounter outcomes.
- **Live test on me** runs the **published revision** with real effects on your character and world.

Draft previews use copied state and simulated actions. Finish by publishing and trying the actual NPC or zone interaction.

## Quests and timers

Use **Action → Give Quest** to set a quest key, display name and instructions. The **quest key** identifies the quest; use that same key in **Has Quest**, **Complete Quest**, **Has Completed Quest** and timer checks. A True/False flag is separate from quest progress.

For a timed quest, enter a duration and choose its unit:

- **Expire:** the quest expires when time runs out.
- **Reset:** clears the quest when the timer ends so it can be offered again.
- **Zero duration:** no time limit.

Timers continue while the player is offline. **Has Quest Timer** checks for a running timer; **Quest Time Remaining** compares its remaining seconds. Numeric conditions offer equals, not equals, less than, greater than and inclusive comparisons.

Use **Handoff Quest** to send a player to another saved NPC. Its continuation runs when that player talks to the destination NPC. Keep quest keys consistent across both conversations.

An optional item target and map destination help players follow a quest. Players can track up to three active quests. The displayed item count comes from their inventory; your graph still needs to check the requirement and complete the quest.

## Spawners, zones and chests

### Trigger a named spawner

Create and save a spawner under **Spawners**. Choose its creature, count, maximum alive, cooldown, size, health and loot settings. Health `0` uses the creature's normal health. Settings apply to future spawns; save changes before trying them.

In WeaverEditor, choose **Action → Trigger NPC Spawner**, then select the saved spawner by name. It spawns at its placed position. **False** means the spawner could not activate, for example because it is disabled, cooling down or at its living-creature limit.

Spawners require a graph, zone or manual **Spawn now** trigger. Weaver clears their surviving enemies after a server restart without loot or victory rewards.

### Start an event from a zone

Create a sphere or box under **Zones**, place it and save it. In the graph's **Link to** controls, select the zone and the event you want: Enter, Exit, Stay, First or Last. Use **Publish & link** to save that connection.

**View zone** shows the area with Weaver out of the way; press **Esc** to return. **World markers** shows nearby zones and spawner eggs while moving around.

For a starting example, use **World → Encounters** to create a linked spawner, zone, reward chest and graph. The chest unlocks after the encounter is cleared and locks again on restart.

### Set up a reward chest

Choose its reward kit, name, access rules and protection. **Lock access** and **Protect chest** are separate settings: opening a chest and destroying it are controlled independently.

Choose a one-time reward or a refill cooldown. Claims can be per player or shared across the server. Saving a new refill duration updates active cooldowns.

Keys can be ordinary items or one of eight Weaver key types. Issue a personal key with **Give Key**. It appears in the recipient's inventory and is bound to that player and the selected chest or quest. Personal keys are single-use; regular item keys have a separate consume setting.

## World tools

| Tool | How to use it |
| --- | --- |
| **Placement** | Move while aiming. Q/E rotates; Shift uses 15-degree steps. G toggles a 1 m grid. Page Up/Down changes height. Front arrows show facing. |
| **Placement handles** | Hold Left Alt to drag move/rotate handles. T returns to aiming. Click saves; Shift-click keeps placing a copy. Esc returns to Weaver. |
| **Inspect** | Toggle it to inspect with Weaver closed. Shows player identities and known building creators. Older creators become known when they join; other platforms show their platform ID. Esc returns to Weaver. |
| **History** | Undo recent NPC, chest, zone and spawner edits, including deletions. Undo preserves player progress and refuses to overwrite newer edits. |
| **NPC routines** | Add poses, nearby greetings and patrol points. Set Pause to 0 for continuous walking or use seconds for a stop at each point. Patrols follow straight paths; keep them clear of walls. NPCs pause while talking and when nobody is nearby. |

Weaver travel is blocked during combat and for **20 seconds afterward**, including NPC, graph and admin teleports. Blocked trips do not spend the warp cooldown; teleport actions follow False. Normal Valheim portals work as usual.

## Sharing graphs

Put graph JSON files in `BepInEx/config/VariantWeaver/exports`, then choose **Import** in WeaverEditor. **Export** writes files to the same folder.

New exports include link names. Imports match unique names and ask you to resolve missing or ambiguous references. Positions and wires are preserved; **Arrange** tidies the layout. Choose the destination NPC or zone on your own server, review item and spawner references, then **Publish & link**.

## Server settings and backups

When updating, replace the mod files on the server and every client, then restart them. **Keep and back up `BepInEx/config/VariantWeaver` alongside the Valheim world.** It holds graphs, NPC and zone links, kits, travel points and player progress.

The server allows **8 MB of saved Weaver content per world** by default. This includes published graphs, drafts, earlier revisions and other saved state, rather than a separate allowance for each graph. Larger network transfers are compressed automatically.

To increase the limit, stop the server and edit `BepInEx/config/com.variantmods.weaver.cfg`:

```ini
[Storage]
World content limit (MB) = 16
```

The supported range is **1–16 MB**. Clients do not need matching config values, but they do need the same mod build.

Server performance defaults are **200 active Weaver creatures** and **40 new creatures per second**. A blocked spawner follows False. Graphs share a work budget and continue on later ticks when busy.

## Troubleshooting

| Problem | Check |
| --- | --- |
| NPC has no conversation | Save and enable the NPC, publish the graph, then use Publish & link. Close Weaver before interacting. |
| Preview works but Talk does nothing | Preview can run a draft. Check the published graph, its entry node and the NPC's saved On interaction field. |
| A spawner is missing from a dropdown | Save the spawner, refresh Weaver, then select it by name. |
| An event will not start | Check the saved zone binding, cooldowns, enabled state and spawner's live status. |
| An imported graph has missing targets | Resolve its links and install the content mods its items or creatures need. |
| Travel or kits are missing for players | Mark them public and save. |
| Version mismatch or repeated old 1 MB warning | Update both server and clients to the same current build. The old hardcoded limit cannot be changed through config. |
| A server restart loses content | Check that the server retains its Weaver config folder and world identity. Restore your backup if needed. |

If an older build already cleared a link, select its NPC or zone and use **Publish & link** after updating. For unresolved problems, include the mod version, what you clicked and the relevant client/server `BepInEx/LogOutput.log`.

## Inspiration and credit

Variant Weaver is inspired by [Pippi — User & Server Management](https://steamcommunity.com/sharedfiles/filedetails/?id=880454836) for Conan Exiles, created by **Joshtech (CoOkIeMoNsTeR)**. Credit to Joshtech for the NPC tools and visual quest editing that inspired this project. Weaver is an independent Valheim mod, with its visual editor named **WeaverEditor**.
