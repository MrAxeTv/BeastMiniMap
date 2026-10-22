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

Release [packs-1.0-r2](https://github.com/MrAxeTv/BeastMiniMap/releases/tag/packs-1.0-r2) accompanies the current **BeastMiniMap 1.0** build. Use matching plugin/pack release notes when updating; a shared version number alone does not guarantee compatibility. Verify downloads against [SHA256SUMS.txt](https://github.com/MrAxeTv/BeastMiniMap/releases/download/packs-1.0-r2/SHA256SUMS.txt).

| Minecraft client | Download | Use |
| --- | --- | --- |
| 1.21.9 and 1.21.10 | [BeastMiniMap-1.21.9.zip](https://github.com/MrAxeTv/BeastMiniMap/releases/download/packs-1.0-r2/BeastMiniMap-1.21.9.zip) | Install for these clients |
| 1.21.11 | [BeastMiniMap-1.21.11.zip](https://github.com/MrAxeTv/BeastMiniMap/releases/download/packs-1.0-r2/BeastMiniMap-1.21.11.zip) | Install for these clients |
| 26.1, 26.1.1 and 26.1.2 | [BeastMiniMap-26.1.zip](https://github.com/MrAxeTv/BeastMiniMap/releases/download/packs-1.0-r2/BeastMiniMap-26.1.zip) | Install for these clients |
| 26.2 | [BeastMiniMap-26.2.zip](https://github.com/MrAxeTv/BeastMiniMap/releases/download/packs-1.0-r2/BeastMiniMap-26.2.zip) | Install for these clients |
| 26.3 | [BeastMiniMap-26.3.zip](https://github.com/MrAxeTv/BeastMiniMap/releases/download/packs-1.0-r2/BeastMiniMap-26.3.zip) | Install for these clients |

**The new plugin JAR contains no resource-pack ZIPs, theme ZIPs or artwork images.** Install the required [BeastMiniMap-Artwork.zip](https://github.com/MrAxeTv/BeastMiniMap/releases/download/packs-1.0-r2/BeastMiniMap-Artwork.zip) and each needed client base ZIP under `plugins/BeastMiniMap/Packs/`. The artwork bundle includes all seven built-in themes and is shared by all supported client versions. It is a server preparation input, not a separate Minecraft pack for players. The plugin retains small JSON layout/protocol contracts and does not download assets automatically.

This replaces the embedded-artwork distribution described in release `packs-1.0-r1`. The five client base packs retain their preceding runtime asset bytes; public installation/editing documentation is updated; `BeastMiniMap-Artwork.zip` is the additional required input for the new lean plugin. Use plugin and asset releases together; the unchanged plugin version `1.0` alone does not identify the matching distribution.

## Installation

1. Obtain the matching BeastMiniMap plugin build separately. Install `BeastMiniMap.jar` and the normal `BeastLib.jar` runtime in the server's `plugins` folder.
2. Create `plugins/BeastMiniMap/Packs/` if needed. Put `BeastMiniMap-Artwork.zip` and the matching client base ZIPs from the table above there. Keep the original filenames and leave these archives intact. Install `BeastMiniMap-26.3.zip` for 26.3 clients; it is no longer included in the plugin JAR. The 1.21.9 ZIP deliberately also serves 1.21.10.
3. Restart normally when installing a new plugin JAR. After changing only the base/artwork inputs, use `/beastminimap reload` or restart normally. Configure pack hosting so the address reported by `/beastminimap pack info` is reachable by players.
4. Join, accept the offered prepared resource pack and open `/beastminimap`.

The server builds effective shared packs under `plugins/BeastMiniMap/Packs/Prepared/`. External hosting must serve the **prepared** ZIP and corresponding URL/hash reported by the plugin, rather than an unprepared download. A missing or invalid client base ZIP affects only that version. The shared artwork bundle is required before packs can be prepared. Other packs that replace the same Minecraft core shaders may require compatible composition.

## Editable theme examples

All seven presets are included in the required `BeastMiniMap-Artwork.zip`. The seven editable downloads below are **optional starting points for custom artwork**, not additional files required to select a built-in preset.

| Theme | Artwork preview | Editable example |
| --- | --- | --- |
| Cartographer (default) | [View](previews/themes/cartographer.png) | [Download](https://github.com/MrAxeTv/BeastMiniMap/releases/download/packs-1.0-r2/BeastMiniMap-Theme-Cartographer-1.0.zip) |
| Futuristic | [View](previews/themes/futuristic.png) | [Download](https://github.com/MrAxeTv/BeastMiniMap/releases/download/packs-1.0-r2/BeastMiniMap-Theme-Futuristic-1.0.zip) |
| Vanilla | [View](previews/themes/vanilla.png) | [Download](https://github.com/MrAxeTv/BeastMiniMap/releases/download/packs-1.0-r2/BeastMiniMap-Theme-Vanilla-1.0.zip) |
| Medieval | [View](previews/themes/medieval.png) | [Download](https://github.com/MrAxeTv/BeastMiniMap/releases/download/packs-1.0-r2/BeastMiniMap-Theme-Medieval-1.0.zip) |
| Minimal Dark | [View](previews/themes/minimal_dark.png) | [Download](https://github.com/MrAxeTv/BeastMiniMap/releases/download/packs-1.0-r2/BeastMiniMap-Theme-MinimalDark-1.0.zip) |
| Cartoony | [View](previews/themes/cartoony.png) | [Download](https://github.com/MrAxeTv/BeastMiniMap/releases/download/packs-1.0-r2/BeastMiniMap-Theme-Cartoony-1.0.zip) |
| Oceanic | [View](previews/themes/oceanic.png) | [Download](https://github.com/MrAxeTv/BeastMiniMap/releases/download/packs-1.0-r2/BeastMiniMap-Theme-Oceanic-1.0.zip) |

Previews show artwork component sheets, not gameplay screenshots.

Extract an example into `plugins/BeastMiniMap/Themes/`. It creates `Themes/<Preset>Editable/Theme.yml` and `Artwork/` under the plugin's data folder, with a unique ID such as `medieval_editable`, the matching built-in `BasedOn` palette, and **`Enabled: false`**. Edit its PNGs and settings, then set `Enabled: true`, reload and accept the updated pack. Preserve image paths/dimensions and the theme's ID once players use it. Up to eight enabled custom themes can join the shared pack.

Players preview and Apply installed themes in Map Settings without another pack download. Adding or editing artwork changes the pack and requires renewed acceptance.

The separate legacy `/beastminimap theme set custom` artwork policy validates against the external 26.3 base ZIP. Older-client-only servers can use the registered `Themes/` examples described above without installing 26.3.

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

Each client base ZIP contains the default map interface artwork, buttons, player/place icons, minimap instruments, bitmap fonts, shaders and pack metadata for that Minecraft client version. The separate shared artwork bundle supplies theme overlays, HUD images and the built-in preview image used during server preparation. Terrain and player data are supplied by the plugin while running; these downloads do not contain server world maps.

Machine-readable download and compatibility information: [packs.json](packs.json).
