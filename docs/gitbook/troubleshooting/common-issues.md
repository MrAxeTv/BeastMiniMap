# Common Issues

Start with `/beastminimap pack info` and the server log. Test changes with a matching supported client and an ordinary player account, since operators inherit more permissions.

## The plugin loads but the map does not open

Check these in order:

1. BeastLib is installed and no dependency or enable error appears in the server log.
2. The player uses a supported client, with its correctly named complete pack in `plugins/BeastMiniMap/Packs/`.
3. The advertised download address is reachable from the player's network and the current pack was accepted.
4. The player has `beastminimap.use` and `beastminimap.buttons.open`. With the default explicit-grant policy, basic command access alone does not unlock the atlas.
5. `Map.Enabled` is true, the player's minimap preference is enabled, and the player is not currently gliding. Use `/beastminimap on` if the saved preference is off.
6. Player data has finished loading successfully. SQL load failures must be resolved before maps and data editing become available.

Use `/beastminimap pack` for a manual pack retry. See [first install](../getting-started/first-install.md), [permissions](../permissions.md) and [pack hosting](../resource-packs/hosting.md).

## A missing-pack panel appears

Install the exact ZIP named in the panel, leaving it intact in `Packs/`, then run `/beastminimap reload`. All five client-version packs are external downloads; none is embedded in the plugin JAR. Do not rename another version's ZIP to satisfy the filename check.

## The pack downloads fail for remote players

`localhost` and `127.0.0.1` identify the player's computer when used as a client download URL. Advertise the server's reachable public address instead. Check the HTTP TCP port, firewall, host allocation and any router forwarding. `Pack.Host.Bind` and `Pack.PublicUrl` have different jobs; see [hosting](../resource-packs/hosting.md).

For external hosting, verify that the URL returns the matching prepared ZIP directly and that its current bytes match the reported hash. A browser page, login prompt or stale ZIP is not a usable pack download.

## The pack transfers quickly but applies slowly

Minecraft still has to load images and fonts and may compile shaders after the transfer finishes. First application of changed content can take longer than later applications. Transfer size and server timing do not establish where the client is spending time.

Check client reload logs, client graphics settings and conflicts with other packs that replace core shaders. Preserve a working configuration while comparing one change at a time. The plugin does not promise one apply time on every client or driver.

## A button refuses an action or makes a villager sound

The action is denied by permissions. Grant its individual node or the appropriate `beastminimap.buttons.*` / `beastminimap.settings.*` group. Explicit false child permissions override broader grants. The translated denial message and sound are configurable; see [permissions](../permissions.md).

Permissions are checked again on Apply. If an administrator removes a setting grant while a menu is open, the pending change cannot be saved. Back/cancel, the recovery key and `/beastminimap map close` remain available.

## Players cannot create more waypoints

The highest true `beastminimap.waypoints.limit.N` permission supplies the owner's allowance across all worlds. Without a numeric or unlimited grant, `Atlas.WaypointsPerPlayer` supplies the fallback, default 64. A limit of zero blocks creation.

The player also needs the creation action permission. Increasing a numeric quota does not unlock the action by itself. Lowering a quota keeps existing waypoints, so an owner can remain above the new limit until they remove enough markers.

## Reload did not change an existing player's layout or zoom

Server defaults initialize unsaved player choices. Returning players keep saved preferences. Change the desired option in `/beastminimap map settings` with the appropriate grant, or use its matching player command. Reset in settings stages server defaults only for fields the player may change; Apply saves the draft.

## `/map` behaves differently from the atlas command

The optional `/map` alias is a shortcut for the command root, not a separate atlas-only command. `/map zoom 5` changes minimap zoom. Use `/beastminimap map zoom 5` for atlas zoom and `/beastminimap map settings` for its menu.

Another plugin can own `/map`. In that case, use the permanent `/beastminimap` command or a namespaced route such as `/beastminimap:beastminimap`.

## Letters are missing in styled menus

The compact bitmap font cannot display every script. Set `Atlas.MenuUi: native` or use `/beastminimap menuui native` as an administrator. Chat and native dialogs support Unicode. Keep the atlas title and coordinate protocol labels in Latin text where required by the compact header presentation.

## Live terrain is empty or an image has not changed

Live sources capture already-loaded chunks. They do not generate or load distant world chunks, and the player's discovery still limits visibility. An administrator's prerender or saved-image render does not reveal exploration for other players.

Saved `world_texture` images are reused. Updating a plugin JAR does not automatically repaint an existing image. Run an explicit image render when the saved image needs rebuilding, then allow its successful publication to replace the previous result. See [terrain sources](../terrain/overview.md) and [world-image rendering](../terrain/world-images.md).

## A storage selection warning appears

Do not delete `Storage/backend-selection.txt`, the SQLite database or its WAL/SHM files to clear the message. It protects against accidentally selecting an empty database and losing access to existing progress. Back up and deliberately transfer existing data before changing the selected backend, connection, path or table prefix. See [storage](../storage.md).

## Reporting an issue

Provide the plugin, BeastLib, server and client versions; the exact command/action; the relevant server/client log; and whether another pack is active. Include the output of `/beastminimap pack info` for delivery problems. Redact database passwords, private addresses and other credentials before sharing files.
