# Image Placement Guide

The wiki now embeds all twelve images from the owner's Spigot description. The PNGs live under `docs/gitbook/assets/images/` and retain the original downloaded bytes. Relative image links keep the pages and their images together when GitBook synchronizes the wiki.

## Images in use

| Local file | Source | Placement and visible content |
| --- | --- | --- |
| [00-beastminimap-logo.png](assets/images/00-beastminimap-logo.png) | [Imgur original](https://i.imgur.com/QzVBowH.png) | [Welcome](README.md): BeastMiniMap logo with map and compass. |
| [01-minimap-overview.png](assets/images/01-minimap-overview.png) | [Imgur original](https://i.imgur.com/4YgEbIA.png) | [Welcome](README.md) and [First Install](getting-started/first-install.md): minimap during normal gameplay. |
| [02-minimap-shapes.png](assets/images/02-minimap-shapes.png) | [Imgur original](https://i.imgur.com/AoAZUsw.png) | [Minimap](maps/minimap.md): disc, hexagon and box outlines at the same location. |
| [03-atlas-layouts.png](assets/images/03-atlas-layouts.png) | [Imgur original](https://i.imgur.com/UHhNUQp.png) | [Atlas](maps/atlas.md): fullscreen and framed layouts side by side. |
| [04-waypoint-journal.png](assets/images/04-waypoint-journal.png) | [Imgur original](https://i.imgur.com/XGAcYtk.png) | [Waypoints and Places](maps/waypoints-and-places.md): personal journal with saved destinations. |
| [05-server-place-search.png](assets/images/05-server-place-search.png) | [Imgur original](https://i.imgur.com/HqYb0zS.png) | [Waypoints and Places](maps/waypoints-and-places.md): public-place search panel. |
| [06-overworld-caves.png](assets/images/06-overworld-caves.png) | [Imgur original](https://i.imgur.com/9xKIYhY.png) | [Live Terrain and Caves](terrain/live-and-caves.md): underground passages, water and lava. |
| [07-nether-terrain.png](assets/images/07-nether-terrain.png) | [Imgur original](https://i.imgur.com/k2Eu2yo.png) | [Terrain Sources](terrain/overview.md): Nether terrain and lava. |
| [08-surface-terrain.png](assets/images/08-surface-terrain.png) | [Imgur original](https://i.imgur.com/obNIQCs.png) | [Terrain Sources](terrain/overview.md): surface rivers, trees and paths. |
| [09-theme-preview.png](assets/images/09-theme-preview.png) | [Imgur original](https://i.imgur.com/F3iIiKy.png) | [Themes](customization/themes.md): Oceanic preview before Apply. |
| [10-atlas-settings.png](assets/images/10-atlas-settings.png) | [Imgur original](https://i.imgur.com/lEYhL1e.png) | [Player Settings](customization/player-settings.md): atlas settings and previews. This example has Client Helper selected; the default is Vanilla Anvil. |
| [11-minimap-settings.png](assets/images/11-minimap-settings.png) | [Imgur original](https://i.imgur.com/DAXalMh.png) | [Player Settings](customization/player-settings.md) and [Setup Flow](getting-started/common-setup-flow.md): shape, corner, size, zoom and previews. |

## Add or replace an image

Use PNG for interface screenshots, keep text readable at the page's normal width, and remove private chat, addresses, or player information before publishing. Preserve an existing filename when replacing the same illustration, then update its caption and source record if needed.

For a page in a folder such as `maps/`, use:

```markdown
![Fullscreen and framed atlas layouts](../assets/images/03-atlas-layouts.png)
```

From the wiki home page, use:

```markdown
![BeastMiniMap during normal gameplay](assets/images/01-minimap-overview.png)
```

Only add an image link after its file exists. Use descriptive alt text and a short caption explaining what the image actually shows. An example's selected settings are not necessarily the current server defaults.

## Useful future screenshots

The current images cover the existing listing examples. Additional images could illustrate these specific instructions:

- Independent minimap and atlas player-icon selectors on the Player Marker page.
- Modifier and trigger selectors on the Shortcut page.
- Center crosshair enabled after panning, with its center X/Z readout.
- A confirmed saved `world_texture` render, showing its selected bounds.
- A denied action and translated feedback for the permission guide.
- The installed complete ZIP filenames inside `Packs/`.

The Nether image and underground Overworld image show different worlds and locations; do not label them as a before/after comparison of one area. A terrain screenshot alone does not identify its configured source mode.
