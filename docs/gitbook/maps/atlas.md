# Fullscreen and Framed Atlas

The atlas is the large interactive map. Choose a fullscreen view for maximum terrain coverage or a framed view with the surrounding atlas artwork.

```text
/beastminimap
/beastminimap map
/beastminimap map settings
```

By default, `/beastminimap` opens fullscreen without changing your saved layout. `/beastminimap map` toggles your preferred full/framed layout. An administrator can make the root show command help instead with `Commands.ShowHelpOnNoArguments: true`.

If your minimap preference is disabled, enable it with `/beastminimap on` before opening the atlas. The opening action also requires its own permission and an accepted resource pack.

## Navigation

Move the mouse to position the custom map pointer. Hold left-click over terrain to drag the map, then release to stop. WASD also pans while left-click remains held over terrain. Left-clicking the toolbar uses its selected tool rather than starting a drag.

Dragging depends on a supported game mode and held item. If the map reports that dragging is unavailable, use the explicit pan command:

```text
/beastminimap map pan 32 0
```

This moves the view 32 blocks east. The second value moves the view south; negative values move west or north.

The wheel and toolbar zoom buttons change atlas zoom. There are sixteen levels, with larger numbers moving closer:

```text
/beastminimap map zoom in
/beastminimap map zoom 5
/beastminimap map reset
```

`map reset` returns the view to the player. It is a navigation command, separate from Reset in the settings draft.

## Toolbar Tools

| Tool | Purpose |
| --- | --- |
| Search | Find shared server places |
| Zoom + / − | Change atlas zoom |
| New waypoint | Create a personal marker |
| Settings | Edit personal map preferences |
| Center on Player | Return to your current position |
| Waypoint journal | Manage existing personal markers |
| Show/Hide Map Center | Toggle the center crosshair |
| Close | Leave the atlas |

Each action has its own [permission](../permissions.md). The administrator may allow a smaller selection of tools.

## Coordinates and Compass

With the center crosshair off, the coordinate panel shows your player X/Y/Z. With it on, the panel shows the map center's X/Z; it omits Y because the center has no single player height. Fullscreen uses one horizontal line, while the framed atlas stacks the coordinates.

The compass face stays north-up. Its needle follows the same direction as the atlas player symbol, from that symbol toward the displayed pointer. The last direction is retained over controls or while a menu is open. The corner minimap retains your actual world heading.

> **Screenshot placeholder — atlas navigation:** Show the fullscreen map and a framed view with stacked coordinates as `03-fullscreen-atlas.png` and `04-framed-atlas.png`. Use `05-center-point.png` for the center crosshair and its X/Z readout.

## Closing and Gliding

Use the swap-hands action, normally F, or `/beastminimap map close` to close the atlas. Recovery closing remains available after permissions change.

The atlas cannot open while actively gliding with elytra or another equipped glider item. Starting to glide closes an open atlas. Simply wearing or carrying a glider does not block opening while standing normally. The minimap remains available during gliding.
