# Player Map Settings

Open the atlas settings cog or run:

```text
/beastminimap map settings
```

The server can use the pixel menu or native Minecraft dialogs. `Atlas.MenuUi: pixel` is the bundled default; an administrator can select `native`. The menu style is a server policy, not a player preference.

## What Players Can Change

| Group | Options |
| --- | --- |
| Atlas | Pointer sensitivity, search input, full/framed layout, icon style and zoom |
| Minimap | Visibility, outline, corner, size and zoom |
| Icons | Minimap/atlas destination sizes, place edge icons and cave presentation |
| Player marker | Separate minimap and full-map symbols and their sizes |
| Shortcut | Opening modifiers and trigger |
| Appearance | Theme and minimap coordinate-panel visibility/width |

The settings previews use sample terrain. They show the proposed appearance without moving the player or exposing undiscovered world data.

> **Screenshot placeholder — settings previews:** Show the Player Marker page with different minimap and full-map symbols. Suggested image: `10-player-marker-settings.png`.

## Apply, Cancel and Reset

In the pixel settings menu, changes remain in a draft until **Apply**. **Cancel** discards the draft. **Reset** stages the server's defaults and still requires Apply; it does not erase the player's SQL record.

Native dialogs use their own action or Save/Apply controls. Top-level layout, icon-style and zoom actions apply immediately; closing a later dialog does not undo an action already saved.

Every option has its own [permission](../permissions.md). Draft Apply rechecks every changed field before saving any of them; direct native actions check their permission when used. Pixel Reset stages defaults only for fields the player may change. Back and Cancel remain available if access changes while a menu is open.

Saved player choices take precedence over later server defaults. Reloading `config.yml` is not a player-preference reset.

## Independent Player Symbols

The minimap and full/framed atlas can use different symbols:

Arrow, Chevron, Triangle, Diamond, Disc, Ring, Box, Cross, Target, Star and Flag.

Each map also has its own player-symbol size from 0.5x to 3x, adjusted in 0.25x menu steps. These settings do not change waypoint/place icon sizes, terrain quality or map zoom. In native dialogs, **Player marker** opens both symbol selectors and both size sliders.

```yaml
Hud:
  PlayerMarkerShape: arrow
  PlayerMarkerScale: 1.0
Atlas:
  PlayerMarkerShape: arrow
  PlayerMarkerScale: 1.0
```

These are initial server defaults. Each player's subsequent saved choices remain independent.

## Search Input

`anvil` is the default vanilla typing method and needs no client mod. Other available IDs are `helper`, `auto` and `commands`. The helper option needs the corresponding client typing support; `auto` uses the helper when available and falls back to anvil.

```text
/beastminimap map typing anvil
```

This changes only the current player's search preference. The server's initial default is `Atlas.SearchInput`.

See [opening shortcuts](keybinds.md), [themes](themes.md), and [languages](languages.md) for their configuration and limits.
