# Quick guide

**F8** opens Weaver. Players use **/travel** and **/kit** for destinations and rewards.

## Editor controls

Use the colored node shortcuts to place a node, then choose its type inside the card. **Graphs** opens a searchable list with draft and published labels. Right-click removes wires.

- Click an output, then an input to connect. Right-click a wire to remove it; Undo restores it.
- Drag titles to move nodes. Middle-drag to pan; scroll to zoom.
- **Fullscreen** expands the menu; **Restore** returns to a window. F8 hides it and keeps your edits.
- Write dialogue and replies inside their nodes. Click their text when zoomed out to open the node at editing size with the caret focused.
- Choose action and condition types inside nodes. Save drafts while working; **Publish & link** makes a graph active on its NPC or zone.

## Nodes

| Node | Use |
| --- | --- |
| Origin | Start here. |
| Dialogue | NPC speech. |
| Option | A player's reply and what follows it. |
| Condition | Choose a check, then connect True and False. |
| Action | Give rewards, change progress, or control NPCs, zones, spawners and chests. |
| Wait | Pause for seconds, including fractions. |
| Randomiser | Choose one connected path. |
| Bounce / Land | Jump to another part of the graph. |
| Comment | Leave a note. |

## Conversations and quests

Add one **Action** or **Condition** node, then use its **Type** dropdown. For number comparisons, choose **Numeric Variable Condition**, a scope and variable name, then select `<`, `<=`, `=`, `!=`, `>` or `>=`. Use **Text Variable Condition** for text and **True / False** for flags.

Place an NPC and choose **Create dialogue**. Write its speech in Dialogue. Connect the same output to an Option for each reply, then connect each Option to its next action. Dialogue and Randomiser support up to eight paths. Place a Wait between Dialogue and an Option to delay that reply.

Dialogue continues into its connected nodes automatically. Options wait for the player's choice. Put a condition before an Option to show it only when that check passes. Use **Dialogue → Wait → Close Dialogue** for an automatic farewell. Other outputs support up to 32 connections; each connected path runs. Randomiser chooses one.

Use an Option before actions that should wait for a player's reply. This also applies when updating older graphs.

**Text speed** controls speech reveal; 0 shows it immediately. **Append** keeps earlier speech. Players use 1–8 to reply, Space to reveal text and Esc to leave. Older replies keep working when moved into Option nodes.

Use the same **Quest key** in Give Quest, Has Quest, Complete Quest and Has Completed Quest. **Quest name** and **Instructions** appear in the journal. True / False checks a separate flag; it does not check quest progress.

For another NPC to continue a quest, use **Handoff Quest**, select that NPC and connect **At next NPC** to the next step.

In **Give Quest**, set a timer in seconds, minutes, hours or days. Zero means no timer. **Expire quest** sets a completion deadline. **Reset for repeat** clears progress when the timer ends, including completed quests. Timers start when accepted and continue offline and across restarts. Abandoning a repeatable quest keeps its cooldown.

Use **Has Quest Timer**, **Quest Time Remaining** or **Has Expired Quest** to branch on timing. Players can open **Quest journal** from Travel & Kits to see countdowns. Give Quest follows False if already accepted or cooling down; Complete Quest follows False unless active. Put rewards after successful completion.

## Events and rewards

Edit text and settings inside each node. Click a compact Dialogue or Option to enlarge it for editing. Enter or Tab finishes typing; Shift+Enter adds a line. Wait accepts decimal seconds such as **1.5**.

Import and export keep node positions and connections. **Arrange** tidies the layout; Undo restores it. Imported graphs are drafts: check references to NPCs, spawners, chests and other world content before publishing.

The graph starts at its selected Origin. If a graph skips its Origin, use **Start from Origin**, then publish. After replacing an NPC, select the new NPC under **Link to** and use **Publish & link**.

Place a zone, choose an Enter or Exit event, then publish and link its graph. Check **Enabled**, **Ignore admins** and the cooldown if it does not fire.

Choose **View zone** to walk around its boundary with Weaver closed. Press **Esc** to return without losing your edits. Boundaries also appear while placing a zone.

For a boss encounter, create a spawner and reward chest. Connect **Trigger NPC Spawner → Wait for Spawner Clear → Lock Chest**, with Locked turned off in the last node. Use False paths for busy or timeout messages. **Protect Chest** controls damage protection.

Spawners run only through a graph, zone or **Spawn now**. After a restart, surviving Weaver-spawned enemies are cleared without loot. That cleanup cancels pending encounter-clear waits; it does not award victory rewards. Normal kills still drop configured loot. Nearby players and restarts do not trigger them. Live status shows cooldown and alive count. Cooldown edits adjust an active countdown immediately; 0 means no delay. **Maximum alive** still limits each group. Changes affect future creatures.

Add cooldowns to repeatable rewards. Saving a refill time updates active countdowns. Switching from one-time starts a fresh refill countdown for previous claims. Chest locks are shared; use a Player-scope variable for personal chest requirements.

Spawner loot kits can contain up to **1,000 items per creature**. A rejected save shows the reason; correct it and save again before selecting the spawner in an Action node.

The eight Weaver keys appear first in the chest key list: Ember, Tide, Grove, Frost, Storm, Sun, Moon and Void. Ordinary items remain available below them. **Give Key** issues a personal inventory key for one chest or quest. **Has Key** checks it; **Use Key** consumes it. Chests consume their Weaver key when the reward is delivered. Used copies cannot unlock again. Use Give Key rather than spawning an unissued key item.

## Handy details

- **Ghost** enables collision-free flight. Turn it off to restore your previous flight mode. Turning Fly off also ends Ghost. Works with or without Server Devcommands.
- Actions with two outputs use **True** for success and **False** when the action cannot finish.
- **Delete node** removes only that node. Undo restores it and its wires.

- World has separate time/weather, spawning, inspection and cleanup tabs. Choose an object before pressing Spawn.
- Turn **Inspect mode** on to close Weaver and inspect what you aim at. Esc returns to the toggle. Turn it off when finished.
- Use **World markers** on Dashboard or World to show nearby zones and spawner eggs with Weaver closed. Esc returns to World; use the same toggle to hide them. Requires admin editing permission.

- During placement, keep moving and looking. A gold FRONT arrow shows the facing direction for NPCs and chests. Click to place, Q/E to rotate, Esc to cancel.
- Use **Delete NPC**, then confirm. Disabling an NPC keeps its settings.
- **Players → View inventory** opens a separate window. Refresh requests a new report from that player's client.
- CharVar is per player, LocVar is per NPC or zone, and GlobVar is shared.
- Keep both mod DLLs together. Everyone needs the content mods used in your graphs.
- Back up `BepInEx/config/VariantWeaver` when moving servers.
