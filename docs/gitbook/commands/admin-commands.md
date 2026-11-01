# Administrator Commands

Server controls require `beastminimap.admin`. Editing shared public places requires `beastminimap.places.admin`. Player controls continue to use their own [permissions](../permissions.md).

These examples use `/beastminimap`, the permanent root. In console, omit the slash. Console must supply a world for world operations.

## Configuration and Diagnostics

| Command | Action |
| --- | --- |
| `/beastminimap reload` | Reload settings/messages and prepare changed pack content |
| `/beastminimap pack info` | Show pack selection, hosting and advertised URLs |
| `/beastminimap pack debug on` / `off` | Toggle delivery diagnostics for the running service |
| `/beastminimap menuui pixel` / `native` | Save the server-wide settings/journal menu style |
| `/beastminimap debuggrid on` / `off` / `status` | Inspect your own live terrain grid; in-game only |
| `/beastminimap colors` | Show the current live renderer status |

`Pack.Debug` supplies startup logging policy. Changing `pack debug` is a temporary runtime diagnostic choice. Use [hosting guidance](../resource-packs/hosting.md) when a reported download URL is not reachable by players.

A settings reload is not a plugin JAR update or SQL migration. Restart normally for a new plugin JAR or deliberate storage-backend changes. Saved player choices take precedence over changed initial defaults.

## World Sources and Image Work

| Command | Action |
| --- | --- |
| `/beastminimap world list` | List world source settings |
| `/beastminimap world status world` | Show source/image preparation status |
| `/beastminimap world source live_terrain world` | Save a terrain source for a world |
| `/beastminimap world render world` | Render or rebuild the saved world image |
| `/beastminimap render world` | Short form of world image rendering |
| `/beastminimap world prerender world` | Prepare reusable live-terrain sources from saved regions |
| `/beastminimap world cancel world` | Cancel image/source preparation |

Source IDs are `live_terrain`, `live_strata` and `world_texture`. Rendering an image and selecting its use are separate operations.

An in-game render request uses the executing player's current X/Z as its center. Stand in the requested world. Console and automatic rendering use configured bounds. See [terrain sources](../terrain/overview.md) and [saved world images](../terrain/world-images.md) before scheduling a large job.

`prerender` prepares reusable terrain data; it does not reveal exploration to players or create a `world_texture` image.

## Themes

```text
/beastminimap theme list
/beastminimap theme status
/beastminimap theme set medieval
/beastminimap theme overrides on
/beastminimap reload
```

These set the server default and artwork policy. An ordinary player's theme dropdown controls only that player's preference. See [themes and custom artwork](../customization/themes.md).

## Public Places

Run these in-game at the destination:

```text
/beastminimap place add market Central Market
/beastminimap place describe Central Market Buy and sell supplies here
/beastminimap place icon house Central Market
/beastminimap place remove Central Market
```

The last command deletes the public record. These records do not count against player waypoint limits. For categories, names and personal display options, see [waypoints and places](../maps/waypoints-and-places.md).
