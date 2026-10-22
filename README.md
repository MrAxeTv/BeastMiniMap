# BeastMiniMap

A corner minimap and interactive fullscreen atlas for Minecraft servers. Explore terrain, find public places and save personal waypoints without installing a client mod.

This repository publishes **resource packs, editable theme examples and plugin information**. Obtain the BeastMiniMap plugin JAR separately from its official distribution. Plugin implementation and source code are not published here.

## Features

- Corner minimap and draggable fullscreen or framed atlas.
- Live surface terrain, optional cave layers and saved world-image maps.
- Personal exploration and waypoints, plus administrator-managed public places.
- Configurable zoom, minimap shapes/corners, markers and coordinate panels.
- Per-player settings, configurable opening shortcuts and seven coordinated themes.
- Editable language files; English and Croatian included.
- SQLite storage by default, with optional MySQL.

## Requirements

Paper or Spigot **1.21.9 through 26.3**, plus [BeastLib **1.7.3**](https://modrinth.com/plugin/beastlib). The plugin uses **Java 21 bytecode**; Minecraft **26.x servers require Java 25 or newer**. Players must accept the matching server resource pack.

## Base packs

Release [packs-1.0-r1](https://github.com/MrAxeTv/BeastMiniMap/releases/tag/packs-1.0-r1) accompanies the current **BeastMiniMap 1.0** build. Use matching plugin/pack release notes when updating; a shared version number alone does not guarantee compatibility. Verify downloads against [SHA256SUMS.txt](https://github.com/MrAxeTv/BeastMiniMap/releases/download/packs-1.0-r1/SHA256SUMS.txt).

| Minecraft client | Download | Use |
| --- | --- | --- |
| 1.21.9 and 1.21.10 | [BeastMiniMap-1.21.9.zip](https://github.com/MrAxeTv/BeastMiniMap/releases/download/packs-1.0-r1/BeastMiniMap-1.21.9.zip) | Optional server input |
| 1.21.11 | [BeastMiniMap-1.21.11.zip](https://github.com/MrAxeTv/BeastMiniMap/releases/download/packs-1.0-r1/BeastMiniMap-1.21.11.zip) | Optional server input |
| 26.1, 26.1.1 and 26.1.2 | [BeastMiniMap-26.1.zip](https://github.com/MrAxeTv/BeastMiniMap/releases/download/packs-1.0-r1/BeastMiniMap-26.1.zip) | Optional server input |
| 26.2 | [BeastMiniMap-26.2.zip](https://github.com/MrAxeTv/BeastMiniMap/releases/download/packs-1.0-r1/BeastMiniMap-26.2.zip) | Optional server input |
| 26.3 | [BeastMiniMap-26.3.zip](https://github.com/MrAxeTv/BeastMiniMap/releases/download/packs-1.0-r1/BeastMiniMap-26.3.zip) | Manual client editing, composition or reference |

**The current plugin JAR still includes the 26.3 base pack and all seven built-in themes.** Publishing separate downloads does not create a plugin JAR without embedded artwork. The plugin extracts its bundled 26.3 ZIP and replaces a different copy in its data folder; do not install an edited 26.3 ZIP there. Use the supported theme/artwork system for server customizations.

## Installation

1. Obtain BeastMiniMap separately. Install `BeastMiniMap.jar` and the normal `BeastLib.jar` runtime in the server's `plugins` folder, then restart normally.
2. For older supported clients, place the matching one of the first four ZIPs above in `plugins/BeastMiniMap/Packs/`. Keep its original filename. The 1.21.9 ZIP deliberately also serves 1.21.10.
3. Run `/beastminimap reload` after adding/updating optional packs. Configure pack hosting so the address reported by `/beastminimap pack info` is reachable by players.
4. Join, accept the offered resource pack and open `/beastminimap`.

The server builds effective shared packs under `plugins/BeastMiniMap/Packs/Prepared/`. External hosting must serve the **prepared** ZIP and corresponding URL/hash reported by the plugin, rather than an unprepared download. Missing older-version packs affect only their client versions. Other packs that replace the same Minecraft core shaders may require compatible composition.

## Editable theme examples

All seven presets are already included in the current plugin. These downloads are **optional starting points for custom artwork**, not extra files required to select a built-in preset.

| Theme | Artwork preview | Editable example |
| --- | --- | --- |
| Cartographer (default) | [View](previews/themes/cartographer.png) | [Download](https://github.com/MrAxeTv/BeastMiniMap/releases/download/packs-1.0-r1/BeastMiniMap-Theme-Cartographer-1.0.zip) |
| Futuristic | [View](previews/themes/futuristic.png) | [Download](https://github.com/MrAxeTv/BeastMiniMap/releases/download/packs-1.0-r1/BeastMiniMap-Theme-Futuristic-1.0.zip) |
| Vanilla | [View](previews/themes/vanilla.png) | [Download](https://github.com/MrAxeTv/BeastMiniMap/releases/download/packs-1.0-r1/BeastMiniMap-Theme-Vanilla-1.0.zip) |
| Medieval | [View](previews/themes/medieval.png) | [Download](https://github.com/MrAxeTv/BeastMiniMap/releases/download/packs-1.0-r1/BeastMiniMap-Theme-Medieval-1.0.zip) |
| Minimal Dark | [View](previews/themes/minimal_dark.png) | [Download](https://github.com/MrAxeTv/BeastMiniMap/releases/download/packs-1.0-r1/BeastMiniMap-Theme-MinimalDark-1.0.zip) |
| Cartoony | [View](previews/themes/cartoony.png) | [Download](https://github.com/MrAxeTv/BeastMiniMap/releases/download/packs-1.0-r1/BeastMiniMap-Theme-Cartoony-1.0.zip) |
| Oceanic | [View](previews/themes/oceanic.png) | [Download](https://github.com/MrAxeTv/BeastMiniMap/releases/download/packs-1.0-r1/BeastMiniMap-Theme-Oceanic-1.0.zip) |

Previews show artwork component sheets, not gameplay screenshots.

Extract an example into `plugins/BeastMiniMap/Themes/`. It creates `Themes/<Preset>Editable/Theme.yml` and `Artwork/` under the plugin's data folder, with a unique ID such as `medieval_editable`, the matching built-in `BasedOn` palette, and **`Enabled: false`**. Edit its PNGs and settings, then set `Enabled: true`, reload and accept the updated pack. Preserve image paths/dimensions and the theme's ID once players use it. Up to eight enabled custom themes can join the shared pack.

Players preview and Apply installed themes in Map Settings without another pack download. Adding or editing artwork changes the pack and requires renewed acceptance.

## Useful commands

| Command | Purpose |
| --- | --- |
| `/beastminimap` | Open fullscreen map; configurable to show help instead |
| `/beastminimap help` | Show commands |
| `/beastminimap on` / `/beastminimap off` | Show or hide the minimap |
| `/beastminimap map settings` | Open personal map settings |
| `/beastminimap keybind` | Inspect or customize the map shortcut |
| `/beastminimap pack` / `/beastminimap pack info` | Request a pack or inspect delivery |
| `/beastminimap theme list` / `/beastminimap theme set <id>` | Inspect themes or select the server default; administrator |
| `/beastminimap reload` | Reload settings; administrator |

`/beastminimap` is permanent. Default configurable aliases are `/minimap`, `/bmm` and `/map`; another plugin may own an alias. Permissions: `beastminimap.use` for players, `beastminimap.admin` for server controls, and `beastminimap.places.admin` for public-place editing.

## What is inside a base pack?

Map interface artwork, buttons, player/place icons, minimap instruments, bitmap fonts, shaders and pack metadata. Terrain and player data are supplied by the plugin while running; these downloads do not contain server world maps.

Machine-readable download and compatibility information: [packs.json](packs.json).
