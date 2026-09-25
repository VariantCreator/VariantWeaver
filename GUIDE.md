# Quick guide

**F8** opens Weaver. Players use **/travel** and **/kit** for destinations and rewards.

## Editor controls

- Click an output, then an input to connect. Click a wire to remove it.
- Drag titles to move nodes. Middle-drag to pan; scroll to zoom.
- **Fullscreen** expands the menu; **Restore** returns to a window. F8 hides it and keeps your edits.
- Edit settings inside nodes or in the side panel. Save drafts while working; **Publish & link** makes a graph active on its NPC or zone.

## Nodes

| Node | Use |
| --- | --- |
| Origin | Start here. |
| Dialogue | NPC speech. |
| Option | A player's reply and what follows it. |
| Condition | Choose a check, then connect True and False. |
| Action | Give rewards, change progress or run an action. |
| Event | Control NPCs, zones, spawners and chests. |
| Wait | Pause for seconds, including fractions. |
| Randomiser | Choose one connected path. |
| Bounce / Land | Jump to another part of the graph. |
| Comment | Leave a note. |

## Conversations and quests

Place an NPC and choose **Create dialogue**. Write its speech in Dialogue. Connect the same output to an Option for each reply, then connect each Option to its next action. Dialogue and Randomiser support up to eight paths.

**Text speed** controls speech reveal; 0 shows it immediately. **Append** keeps earlier speech. Players use 1–8 to reply, Space to reveal text and Esc to leave. Older replies keep working when moved into Option nodes.

Use the same **Quest key** in Give Quest, Has Quest, Complete Quest and Has Completed Quest. **Quest name** and **Instructions** appear in the journal. True / False checks a separate flag; it does not check quest progress.

For another NPC to continue a quest, use **Handoff Quest**, select that NPC and connect **At next NPC** to the next step.

## Events and rewards

Place a zone, choose an Enter or Exit event, then publish and link its graph. Check **Enabled**, **Ignore admins** and the cooldown if it does not fire.

For a boss encounter, create a spawner and reward chest. Connect **Trigger NPC Spawner → Wait for Spawner Clear → Lock Chest**, with Locked turned off in the last node. Use False paths for busy or timeout messages. **Protect Chest** controls damage protection.

Add cooldowns to repeatable rewards. Chest locks are shared; use a Player-scope variable for personal chest requirements.

## Handy details

- During placement, keep moving and looking. Click to place, Q/E to rotate, Esc to cancel.
- Use **Delete NPC**, then confirm. Disabling an NPC keeps its settings.
- CharVar is per player, LocVar is per NPC or zone, and GlobVar is shared.
- Keep both mod DLLs together. Everyone needs the content mods used in your graphs.
- Back up `BepInEx/config/VariantWeaver` when moving servers.
