# WeaverEditor guide

Build conversations, quests and events in Valheim with WeaverEditor.

[Getting started](https://github.com/VariantCreator/WeaverEditor/blob/main/GUIDE.md#getting-started) · [Menus](https://github.com/VariantCreator/WeaverEditor/blob/main/GUIDE.md#menu-and-editor) · [Shared settings](https://github.com/VariantCreator/WeaverEditor/blob/main/GUIDE.md#shared-settings) · [First NPC](https://github.com/VariantCreator/WeaverEditor/blob/main/GUIDE.md#your-first-npc-conversation) · [Nodes](https://github.com/VariantCreator/WeaverEditor/blob/main/GUIDE.md#nodes-and-connections) · [Quests](https://github.com/VariantCreator/WeaverEditor/blob/main/GUIDE.md#quests-and-timers) · [Events](https://github.com/VariantCreator/WeaverEditor/blob/main/GUIDE.md#spawners-zones-and-chests) · [World tools](https://github.com/VariantCreator/WeaverEditor/blob/main/GUIDE.md#world-tools) · [Imports](https://github.com/VariantCreator/WeaverEditor/blob/main/GUIDE.md#sharing-graphs) · [Server settings](https://github.com/VariantCreator/WeaverEditor/blob/main/GUIDE.md#server-settings-and-backups) · [Troubleshooting](https://github.com/VariantCreator/WeaverEditor/blob/main/GUIDE.md#troubleshooting)

## Getting started

1. Install BepInExPack Valheim, then import the WeaverEditor ZIP into your mod manager.
2. Install the **same WeaverEditor build on the server or host and every client**. Keep `VariantWeaver.dll` and `VariantWeaver.Core.dll` together.
3. Join a world and press **F8**. Server admins and players with assigned permissions can edit content. Other players get Travel, Kits, Quests, Appearance and My Vendors.

For manual installation, copy the ZIP's `plugins/VariantWeaver` folder into `BepInEx/plugins`. Everyone also needs the content mods used by your graphs. WeaverEditor reads the items and creatures registered by installed mods; use **Mods → Rescan** if an entry is missing.

| Control | What it does |
| --- | --- |
| **F8** | Open WeaverEditor or the player menu |
| **/warp** | Open public warp destinations |
| **/kit** | Open public kits |
| **/return** | Return to the departure point of your last successful WeaverEditor teleport |
| **/tp <player name>** | Ask another player to allow your teleport; requires teleport permission |
| **Fullscreen / Restore** | Expand the editor or return to its window |
| **Esc** | Close WeaverEditor; during ordinary gameplay, open the pause menu and unlock quest-HUD dragging |

Create travel points under **Travel** and kits under **Community**. Mark them public if players should see them in their menu. They can still be used as graph actions without appearing there.

## Player-owned vendors

### Add a vendor to a kit

1. Create and save an NPC with the appearance you want players to receive.
2. Open **Community → Kits**, choose a kit, and add **Vendor Deed** (`VW_VendorDeed`).
3. Select that kit entry and choose its **NPC appearance**, then save the kit. Leave the appearance empty for a basic vendor.

The deed copies the NPC's appearance when placed. Its conversation, graph and admin actions do not carry over. Give the kit a claim limit or cooldown if you want to limit who receives deeds.

### Open your shop

Use the deed from your inventory, choose a nearby spot, and left-click to place it. **Q/E** turns it; **Esc** cancels. The deed is consumed only after placement succeeds. Press **E** at the vendor to open its shop.

Under **Stock**, choose an unequipped inventory item, enter the lot size, and choose the payment item and price. For example, deposit one chest piece and ask for **250 Stone**. Confirming removes those items from your inventory and lists that one lot. Buyers review the goods and payment before purchasing. Quality, condition and saved item details stay with the item.

Payments use the buyer's carried inventory. Equipped, protected and quest items are excluded. Vendor deeds and personal Weaver keys cannot be sold or used as payment. Everyone needs the content mods for the items being traded. Removing an item's mod leaves its vendor stock saved until the item is available again.

### Manage or move your vendor

Open **F8 → My Vendors** to manage your shops. **Earnings** holds payments from completed sales; collect one entry or all of them when you have room. **Listed stock** lets you withdraw an unsold lot.

**Appearance** changes the vendor's name, title, body, hair, beard, colours, outfit and pose. Choose clothing and held items under **Outfit & pose**. These are visual choices; they do not create inventory items or shop stock. Players can only list items they deposit and collect items already held by their own vendor.

**Pack vendor** removes it from the world and keeps its stock and earnings in My Vendors. Use **Place again** to move it without another deed. Only the owner or a server admin can change its appearance or pack it; stock and earnings can only be collected by the owner. Packed vendors still count towards the owner's limit.

### Vendor limits and backups

The host's `BepInEx/config/com.variantmods.weaver.cfg` has a **Player vendors** section. Defaults are enabled, **3 vendors per player**, **100 per world**, **32 listings per vendor**, and a **100,000-item maximum price**. These limits are enforced by the server. Disabling vendors stops new placements and sales while letting owners recover their items.

Vendors, listings, earnings and pending trades are saved in `BepInEx/config/VariantWeaver/vendors-world-<world ID>.json`. Back up that folder with your world. Keep client `BepInEx/config/WeaverEditor/vendor-receipts` files with character backups; they help recover interrupted trades. Install the same build on the server/host and every client.

## Themes, player journal and movable quest tracker

### Choosing a theme

Regular players open **F8 → Appearance**. Admins open **F8 → Settings → Appearance**. The themes are **Valheim**, **Black Forest**, **Frost**, **Ashlands** and **High Contrast**. Accent choices are Theme, Gold, Teal, Blue, Copper, Silver and Ember. Choose **Theme** to use each preset's own accent. Previously saved accent settings are retained.

Choose Valheim lettering or readable lettering, adjust text size, and enable or disable the subtle carved texture. High Contrast does not add grain. Fonts and item icons come from your game or system; no font installation is needed.

These settings affect WeaverEditor's player journal, all admin tabs, WeaverEditor, inventory and selection windows, dialogue, trader menus and quest tracker. Node-category and warning colours remain distinguishable. They do not recolour another mod's menus or the game's own pause/settings screens.

Theme and layout settings are local to each installation. Your choices do not change other players' interfaces.

### Item warning text

Enable **Hide summoned-item warning** under **Appearance** to hide Valheim's warning line in item tooltips. This only changes the text. Item flags, achievements and anti-cheat checks stay unchanged.

To hide the line for everyone, set this in the server's `BepInEx/config/com.variantmods.weaver.cfg`, then restart the server:

```ini
[Server presentation]
Hide summoned-item warning = true
```

Set it back to `false` to let players choose their own display setting. Everyone needs the updated WeaverEditor build.

### Travel, kits and quests

The player menu has **Travel**, **Kits**, **Quests**, **Appearance** and **My Vendors** pages. Travel cards show readiness, cooldown and optional distance/coordinates. The **Return to departure** button uses the same WeaverEditor-only return as **/return**.

Kit cards show availability and item previews. Expand a card to see quantities and the complete contents. Search kits and travel points by name. Claiming kits and using travel still use the existing server permissions, restrictions and cooldowns.

The quest journal has Active, Finished and All filters. Quest cards show instructions, item counts, destination distance and timers when those values are supplied by the quest. Use the tracked toggle to hide or restore a quest in the HUD. Full instructions remain available in the journal when a tracker row is too short. Abandoning or dismissing a quest still requires confirmation.

### Moving the tracker with Esc

1. Close WeaverEditor and any NPC dialogue, then press **Esc** during gameplay.
2. The tracker shows **MOVE MODE**. Hold the left mouse button on the tracker and drag it to your chosen position.
3. Release the mouse to save. Press **Esc** again to close the pause menu and lock the tracker.

A sample tracker appears in move mode when there are no active tracked quests, so you can arrange it before accepting a quest. When you finish a quest, a short themed completion/update notice may remain visible even when the active list is empty.

While playing normally, the tracker does not intercept mouse clicks or unlock your cursor. Dragging is disabled while WeaverEditor, dialogue, placement, inventory inspection or a native settings/player submenu is open. Closing the pause menu, losing focus or leaving the world ends the drag.

### Tracker settings and reset

Regular players use **F8 → Appearance → Quest tracker**. Admins use **F8 → Settings → Quest tracker**. Available controls:

- Show/hide the tracker, enable Esc dragging and enable quest destination map pins.
- Scale from **0.65× to 1.60×** and width from **280 to 520 pixels** before scaling.
- Background opacity from **35% to 100%** and compact quest rows.
- Maximum **1–6** tracked quests. Extra tracked quests remain in the journal.
- **Move tracker** opens the Esc menu for placement. **Reset position** restores the default placement.

The position is saved as a proportion of available screen space. Resolution, scale and width changes keep the complete panel on screen. Large trackers are automatically reduced to fit smaller screens. The default maximum is three quests.

Preferences are stored in the local `BepInEx/config/com.variantmods.weaver.cfg`, in **Menu appearance** and **Quest tracker**. Use the in-game controls rather than editing the file while the game is open. Reset position does not delete quests or server data.

### Updating from Variant Weaver

WeaverEditor is the new name for Variant Weaver. Update the existing mod to keep your saved content. The DLL names, package identifier and config folders keep their old names so existing installs update correctly. Replace both DLLs together.

Back up your config and world content. Stop the server/game before replacing the existing `VariantWeaver.dll` and `VariantWeaver.Core.dll` with the matching pair from this ZIP. Remove duplicate copies elsewhere in the profile. Update server/host and all clients together. Do not delete `BepInEx/config/VariantWeaver`.

## Optional travel restrictions

Edit the server or host's `BepInEx/config/com.variantmods.weaver.cfg`, under the existing `[Server rules]` section:

```ini
[Server rules]
Block travel while encumbered = true
Block travel with non-teleportable items = true
```

Both settings default to **false**, keeping existing travel behavior until enabled. Each can be turned on independently. Run the new build once to add the settings, stop the server or host, edit the file and restart it.

The rules cover **warps, /return, teleport to player, Bring player here and graph/NPC teleports**, including admins. The player actually being moved is checked, not a stationary request sender or destination player. Local client config cannot turn off the host's rules.

Weight is checked against the current carry limit. The item setting checks the no-teleport flag on carried items, including modded items, and special never-teleportable quest cargo. It is not a fixed ore/ingot list. A mod that changes an item's flag to teleportable changes what this setting sees. This separate WeaverEditor rule still applies when the world allows ore through normal portals.

The travelling player's inventory is checked again immediately before travel, including after another player accepts a pending request. Blocked travel explains why and keeps the previous return point. A rejected warp refunds its warp cooldown; the short anti-spam/retry timers still apply. Store restricted items or reduce weight, then try again. Normal portals and other mods' teleport commands are unchanged.

Install **1.2.3 on the server/host and every client**. Older client builds do not implement these checks. Custom storage supplied by another mod must expose its contents through the player's inventory to be inspected.

The admin **Settings → Server rules** panel shows whether each restriction is enabled. Change the settings in the host's config, not in personal Appearance options.

## Trader menus and player travel

### Item-icon traders

When a dialogue offers a direct Trade action or a straightforward exchange confirmation, WeaverEditor shows an item-icon trader menu. It displays the goods, bundle quantities, price, payment availability and the full exchange. Choose **Buy**, **Sell**, **Barter** or **All**, and use the search field to narrow the list.

Click an offer to select it. **Review exchange** opens an existing confirmation; **Confirm exchange** performs the selected direct exchange through the original graph. One click exchanges one authored bundle. The server still controls the graph and prices; the new menu does not create a separate shop inventory.

Existing straightforward trader graphs need no new import. Conditional offers, multiple-output options, hidden rewards and branching exchanges remain in their authored dialogue paths. An unavailable item uses a placeholder icon and cannot be confirmed through the icon panel. Item names and sprites are read from the installed game/mod items.

### Return from WeaverEditor travel

Use **/return** to go back to where your last successful WeaverEditor teleport started. This covers WeaverEditor travel points, WeaverEditor graph teleports and WeaverEditor player teleports. It does not use general teleport history.

Example: WeaverEditor takes you from your base to a town, then you use a normal portal. **/return** goes back to the base; the normal portal does not replace the WeaverEditor departure point.

A newer successful WeaverEditor teleport replaces the saved point. Failed travel keeps the old point. A successful return consumes it instead of creating a back-and-forth toggle. Return points are session-only and clear when you leave the world or disconnect. A short retry cooldown applies, along with existing WeaverEditor combat and travel restrictions.

### Teleport to an online player

Open **F8 → Players**, select an online player, and choose **Teleport to player**. The other player gets a themed **Accept / Deny** popup with your name. **Bring player here** instead asks the selected player to let WeaverEditor move them to you. Neither action moves anyone until they accept.

From chat, use:

```text
/tp PlayerName
/tp "Player Name"
```

Names are case-insensitive. A unique partial name works, but ambiguous matches are rejected. When names are duplicated, choose the player through the menu. The server resolves live positions when it receives the action, rather than trusting coordinates from the player's menu.

Player teleporting and bringing still require admin access or the **players.teleport** permission. This does not grant unrestricted player teleports to everyone. Admins must also get the recipient's approval.

**Accept** permits that one request. **Deny** or **Esc** dismisses it without moving anyone. Unanswered requests expire after **30 seconds**. Denial restores control immediately; accepting waits for the server to validate the request. The popup follows the recipient's selected theme and uses the portal icon. An initial click guard prevents an existing click from accepting a newly opened request.

Only one request can involve a player at a time. A sender must wait at least **10 seconds** between requests, and the recipient gets a brief **5-second** quiet period after one closes. Requests are cancelled when either player disconnects or changes character. They are not saved across worlds or server restarts.

On approval, the server checks the original player sessions, the sender's current permission and the travelling player's combat restriction again. The server includes its current travel rules with the approved effect; the travelling client checks its live inventory and weight before moving. It uses the destination player's **current position**, not where they stood when the request was sent. A stale, expired or replayed approval cannot cause another teleport.

Only a successful approved trip creates or replaces the travelling player's WeaverEditor return point. Denied and expired requests do not alter `/return`. This consent prompt applies to `/tp`, **Teleport to player** and **Bring player here**. Normal portals, named WeaverEditor warp destinations and quest-graph travel do not show this consent prompt. Enabled travel restrictions still apply to all WeaverEditor teleports.

Install **1.2.3** on the **server/host and every client**. Earlier builds without teleport approval do not implement this handshake: an old server can still have immediate-teleport behavior, while an old recipient client cannot display the request and it will expire.

### Updating

Install 1.2.3 on the server or host and every client. Keep **VariantWeaver.dll** and **VariantWeaver.Core.dll** together; remove old duplicate copies rather than leaving two versions installed. Back up and keep `BepInEx/config/VariantWeaver` and your existing WeaverEditor config. This package does not replace saved quests, NPCs or world configuration.

## Menu and editor

NPCs, zones, chests and spawners have a searchable browser with enabled and linked status. Select an object to open its settings; expand **Browse** to choose another. Your unsaved object edits stay available while switching within the session.

**Community → Kits** has a compact item list. Search, change quantities directly, or select an item to change it. **Merge duplicate items** combines matching entries. Save stays at the bottom of the panel. Kits allow 60 rows and 1,000 items per row by default; the server owner can change those limits.

WeaverEditor keeps the current graph name and save state visible. Use the arrows to go back and forward, or **Graphs** to search All, Recent, Linked or Draft graphs. Names such as `Tavern / Greeter` group related graphs.

- All nodes use the same size by default. Longer settings scroll inside the node.
- Shift-click or drag empty space to select nodes. Drag a title to move the selection.
- **Select branch** selects the connected path. Copy/paste keeps connections between copied nodes; reconnect any outside links.
- Align a selection into a row or column. Use the minimap to move around large graphs.
- **Fit graph** shows the whole graph. At a distance, nodes become coloured blocks. Select one and click **Focus**, or double-click it, to return to editing size.
- Click a validation result to find its node. Missing connections appear red.
- Collapse the inspector for more space. Edit node settings directly inside the cards.
- **Connections / Used by** opens related graphs and world objects.

Local draft recovery saves while you edit and does not publish anything. **Recovered drafts** also finds new graphs that were never saved to the server. Compare with the server copy before saving recovered work. Publishing and linking stay manual.

**Settings** controls text size, accent colour, visible rows, node dimensions, minimap, previews and recovery. Server draft autosave is optional and off by default. The server can disable it.

Players can expand a kit to see its items and icons. Travel and kit buttons show their own remaining cooldowns. NPC appearance previews let admins rotate the model before placing it.

## Shared settings

The config is created at `BepInEx/config/com.variantmods.weaver.cfg` after WeaverEditor starts.

| Section | Settings |
| --- | --- |
| Menu appearance | Text size, accent, collapsed sections, browser rows, previews and details |
| Editor preferences | Equal node sizes, dimensions, selection tools, minimap, inspector, local recovery and optional server autosave |
| Server rules | Encumbrance and non-teleportable-item travel restrictions, public travel/kits, NPC conversations, previews, inspection, admin powers, debug/devcommands, draft autosave and history cleanup |
| Storage | World content limit, saved revision limit and revisions retained per graph after cleanup |
| Server performance | Active creatures and spawns per second |

Change **Server rules**, **Storage** and **Server performance** on the server or host, then restart it. Clients cannot override server rules. WeaverEditor's debug/devcommands setting controls its own buttons; other mods keep their own controls. Normal portals are unchanged.

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
6. Click **Validate**, then **Publish & link**. Close WeaverEditor, face the NPC and press **E** to talk.

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

Spawners require a graph, zone or manual **Spawn now** trigger. WeaverEditor clears their surviving enemies after a server restart without loot or victory rewards.

### Start an event from a zone

Create a sphere or box under **Zones**, place it and save it. In the graph's **Link to** controls, select the zone and the event you want: Enter, Exit, Stay, First or Last. Use **Publish & link** to save that connection.

**View zone** shows the area with WeaverEditor out of the way; press **Esc** to return. **World markers** shows nearby zones and spawner eggs while moving around.

For a starting example, use **World → Encounters** to create a linked spawner, zone, reward chest and graph. The chest unlocks after the encounter is cleared and locks again on restart.

### Set up a reward chest

Choose its reward kit, name, access rules and protection. **Lock access** and **Protect chest** are separate settings: opening a chest and destroying it are controlled independently.

Choose a one-time reward or a refill cooldown. Claims can be per player or shared across the server. Saving a new refill duration updates active cooldowns.

Keys can be ordinary items or one of eight WeaverEditor key types. Issue a personal key with **Give Key**. It appears in the recipient's inventory and is bound to that player and the selected chest or quest. Personal keys are single-use; regular item keys have a separate consume setting.

## World tools

| Tool | How to use it |
| --- | --- |
| **Placement** | Move while aiming. Q/E rotates; Shift uses 15-degree steps. G toggles a 1 m grid. Page Up/Down changes height. Front arrows show facing. |
| **Placement handles** | Hold Left Alt to drag move/rotate handles. T returns to aiming. Click saves; Shift-click keeps placing a copy. Esc returns to WeaverEditor. |
| **Inspect** | Toggle it to inspect with WeaverEditor closed. Shows player identities and known building creators. Older creators become known when they join; other platforms show their platform ID. Esc returns to WeaverEditor. |
| **History** | Undo recent NPC, chest, zone and spawner edits, including deletions. Undo preserves player progress and refuses to overwrite newer edits. |
| **NPC routines** | Add poses, nearby greetings and patrol points. Set Pause to 0 for continuous walking or use seconds for a stop at each point. Patrols follow straight paths; keep them clear of walls. NPCs pause while talking and when nobody is nearby. |

WeaverEditor travel is blocked during combat and for **20 seconds afterward**, including NPC, graph and admin teleports. Blocked trips do not spend the warp cooldown; teleport actions follow False. Normal Valheim portals work as usual.

## Sharing graphs

Put graph JSON files in `BepInEx/config/WeaverEditor/exports`, then choose **Import** in WeaverEditor. **Export** writes files to the same folder. On first launch after updating, existing exports move here automatically. Files with matching names and different contents are kept under separate filenames.

New exports include link names. Imports match unique names and ask you to resolve missing or ambiguous references. Positions and wires are preserved; **Arrange** tidies the layout. Choose the destination NPC or zone on your own server, review item and spawner references, then **Publish & link**.

## Server settings and backups

When updating, replace the mod files on the server and every client, then restart them. **Keep and back up `BepInEx/config/VariantWeaver` alongside the Valheim world.** It holds graphs, NPC and zone links, kits, travel points and player progress.

The server allows **8 MB of saved WeaverEditor content per world** by default. This includes published graphs, drafts, earlier revisions and other saved state, rather than a separate allowance for each graph. Larger network transfers are compressed automatically.

To increase the limit, stop the server and edit `BepInEx/config/com.variantmods.weaver.cfg`:

```ini
[Storage]
World content limit (MB) = 16
```

The supported range is **1–16 MB**. Clients do not need matching config values, but they do need the same mod build.

Server performance defaults are **200 active WeaverEditor creatures** and **40 new creatures per second**. A blocked spawner follows False. Graphs share a work budget and continue on later ticks when busy.

## Troubleshooting

| Problem | Check |
| --- | --- |
| NPC has no conversation | Save and enable the NPC, publish the graph, then use Publish & link. Close WeaverEditor before interacting. |
| Preview works but Talk does nothing | Preview can run a draft. Check the published graph, its entry node and the NPC's saved On interaction field. |
| A spawner is missing from a dropdown | Save the spawner, refresh WeaverEditor, then select it by name. |
| An event will not start | Check the saved zone binding, cooldowns, enabled state and spawner's live status. |
| An imported graph has missing targets | Resolve its links and install the content mods its items or creatures need. |
| Travel or kits are missing for players | Mark them public and save. |
| Version mismatch or repeated old 1 MB warning | Update both server and clients to the same current build. The old hardcoded limit cannot be changed through config. |
| A server restart loses content | Check that the server retains its WeaverEditor config folder and world identity. Restore your backup if needed. |

If an older build already cleared a link, select its NPC or zone and use **Publish & link** after updating. For unresolved problems, include the mod version, what you clicked and the relevant client/server `BepInEx/LogOutput.log`.

## Inspiration and credit

WeaverEditor is inspired by [Pippi — User & Server Management](https://steamcommunity.com/sharedfiles/filedetails/?id=880454836) for Conan Exiles, created by **Joshtech (CoOkIeMoNsTeR)**. Credit to Joshtech for the NPC tools and visual quest editing that inspired this project. WeaverEditor is an independent Valheim mod, with its visual editor named **WeaverEditor**.

### Journal icons

Warps show a glowing portal, kits a supply chest, and quest headings a sealed scroll. The tracker uses the same scroll. Item objectives keep their native item icons. These icons are included in the mod and do not require an extra download.
