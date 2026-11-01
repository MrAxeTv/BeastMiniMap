# BeastMiniMap

A corner minimap and interactive fullscreen atlas for Minecraft servers. Explore terrain, find public places and save personal waypoints without installing a client mod.

This repository publishes **resource packs, editable theme examples and plugin information**. Obtain the BeastMiniMap plugin JAR separately from its official distribution. Plugin implementation and source code are not published here.

Read the [BeastMiniMap wiki](docs/gitbook/README.md) for setup, pack hosting, map controls, permissions, themes, terrain rendering, and storage. The [GitBook sidebar](docs/gitbook/SUMMARY.md) lists every guide, with [instructions for connecting GitBook](docs/gitbook/troubleshooting/github-gitbook-workflow.md).

## Features

- Corner minimap and draggable fullscreen or framed atlas.
- Live surface terrain, optional cave layers and saved world-image maps.
- Personal exploration and waypoints, plus administrator-managed public places.
- Configurable zoom, minimap shapes/corners, markers and coordinate panels.
- Per-player settings, configurable opening shortcuts and seven coordinated themes.
- Individual button/settings permissions and personal waypoint limits per role.
- 33 bundled languages, with 17 optional language downloads.
- SQLite storage by default, with optional MySQL.

## Requirements

Paper or Spigot **1.21.9 through 26.3**, plus [BeastLib **1.7.3**](https://modrinth.com/plugin/beastlib). The plugin uses **Java 21 bytecode**; Minecraft **26.x servers require Java 25 or newer**. Players must accept the matching server resource pack.

## Complete packs

Release [packs-1.0-r3](https://github.com/MrAxeTv/BeastMiniMap/releases/tag/packs-1.0-r3) accompanies the current **BeastMiniMap 1.0** build. Use matching plugin/pack release notes when updating; a shared version number alone does not guarantee compatibility. Verify downloads against [SHA256SUMS.txt](https://github.com/MrAxeTv/BeastMiniMap/releases/download/packs-1.0-r3/SHA256SUMS.txt).

| Minecraft client | Download | Use |
| --- | --- | --- |
| 1.21.9 and 1.21.10 | [BeastMiniMap-1.21.9.zip](https://github.com/MrAxeTv/BeastMiniMap/releases/download/packs-1.0-r3/BeastMiniMap-1.21.9.zip) | Install for these clients |
| 1.21.11 | [BeastMiniMap-1.21.11.zip](https://github.com/MrAxeTv/BeastMiniMap/releases/download/packs-1.0-r3/BeastMiniMap-1.21.11.zip) | Install for these clients |
| 26.1, 26.1.1 and 26.1.2 | [BeastMiniMap-26.1.zip](https://github.com/MrAxeTv/BeastMiniMap/releases/download/packs-1.0-r3/BeastMiniMap-26.1.zip) | Install for these clients |
| 26.2 | [BeastMiniMap-26.2.zip](https://github.com/MrAxeTv/BeastMiniMap/releases/download/packs-1.0-r3/BeastMiniMap-26.2.zip) | Install for these clients |
| 26.3 | [BeastMiniMap-26.3.zip](https://github.com/MrAxeTv/BeastMiniMap/releases/download/packs-1.0-r3/BeastMiniMap-26.3.zip) | Install for these clients |

**One complete ZIP per client version; no separate artwork download.** Each `BeastMiniMap-<version>.zip` includes that client's base assets and all seven built-in themes. Install the matching ZIP unchanged under `plugins/BeastMiniMap/Packs/`. The plugin JAR contains no pack ZIPs or artwork images, retains small JSON layout/protocol contracts, and does not download asset files automatically.

This complete-pack layout replaces the separate-artwork installation used by the preceding release. The outer ZIPs and installation documents change; existing image, font and shader payload bytes retain their behavior. Use matching plugin/asset release notes when updating; plugin version `1.0` alone does not identify the matching distribution.

## Installation

1. Obtain the matching BeastMiniMap plugin build separately. Install `BeastMiniMap.jar` and the normal `BeastLib.jar` runtime in the server's `plugins` folder.
2. Create `plugins/BeastMiniMap/Packs/` if needed. Put the single complete ZIP matching each required client version from the table above there. Keep the original filename and leave the archive intact. For 26.3 clients, install only `BeastMiniMap-26.3.zip`; it already contains all seven themes. The 1.21.9 ZIP deliberately also serves 1.21.10.
3. Restart normally when installing a new plugin JAR. After adding or replacing only the complete pack inputs, use `/beastminimap reload` or restart normally. Configure pack hosting so the address reported by `/beastminimap pack info` is reachable by players.
4. Grant your player roles the desired [map permissions](#permissions), then join, accept the offered prepared resource pack and open `/beastminimap`.

Without a pack installed, administrative commands remain available and the plugin reports the missing file with the GitHub download link. Install the matching ZIP and reload to enable its maps. A missing or invalid version's pack leaves other installed versions available.

The server builds effective shared packs under `plugins/BeastMiniMap/Packs/Prepared/`. External hosting must serve the **prepared** ZIP and corresponding URL/hash reported by the plugin. The complete download contains server preparation artwork that is removed before the client pack is offered. Other packs that replace the same Minecraft core shaders may require compatible composition.

## Editable theme examples

All seven presets are included in each complete client-version ZIP. The seven editable downloads below are **optional starting points for custom artwork**, not additional files required to select a built-in preset.

| Theme | Artwork preview | Editable example |
| --- | --- | --- |
| Cartographer (default) | [View](previews/themes/cartographer.png) | [Download](https://github.com/MrAxeTv/BeastMiniMap/releases/download/packs-1.0-r3/BeastMiniMap-Theme-Cartographer-1.0.zip) |
| Futuristic | [View](previews/themes/futuristic.png) | [Download](https://github.com/MrAxeTv/BeastMiniMap/releases/download/packs-1.0-r3/BeastMiniMap-Theme-Futuristic-1.0.zip) |
| Vanilla | [View](previews/themes/vanilla.png) | [Download](https://github.com/MrAxeTv/BeastMiniMap/releases/download/packs-1.0-r3/BeastMiniMap-Theme-Vanilla-1.0.zip) |
| Medieval | [View](previews/themes/medieval.png) | [Download](https://github.com/MrAxeTv/BeastMiniMap/releases/download/packs-1.0-r3/BeastMiniMap-Theme-Medieval-1.0.zip) |
| Minimal Dark | [View](previews/themes/minimal_dark.png) | [Download](https://github.com/MrAxeTv/BeastMiniMap/releases/download/packs-1.0-r3/BeastMiniMap-Theme-MinimalDark-1.0.zip) |
| Cartoony | [View](previews/themes/cartoony.png) | [Download](https://github.com/MrAxeTv/BeastMiniMap/releases/download/packs-1.0-r3/BeastMiniMap-Theme-Cartoony-1.0.zip) |
| Oceanic | [View](previews/themes/oceanic.png) | [Download](https://github.com/MrAxeTv/BeastMiniMap/releases/download/packs-1.0-r3/BeastMiniMap-Theme-Oceanic-1.0.zip) |

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

`/beastminimap` is permanent. Default configurable aliases are `/minimap`, `/bmm` and `/map`; another plugin may own an alias.

## Permissions

Ordinary players require explicit action grants by default; operators inherit all declared permissions. Give roles the two control groups below, or grant individual actions. Commands, shortcuts, pixel menus and native dialogs use the same checks. Explicit false child permissions override broader wildcard grants.

| Permission | Access |
| --- | --- |
| `beastminimap.use` | Basic player commands; enabled by default |
| `beastminimap.buttons.*` | All map buttons, including opening the atlas |
| `beastminimap.buttons.zoom.in` | Atlas zoom-in action only |
| `beastminimap.settings.*` | All player settings |
| `beastminimap.settings.minimap.shape` | Minimap shape setting only |
| `beastminimap.waypoints.limit.N` | Personal waypoint allowance; highest true numeric grant wins |
| `beastminimap.waypoints.limit.unlimited` | Unlimited personal waypoints |
| `beastminimap.admin` | Server controls; operator default |
| `beastminimap.places.admin` | Shared-place editing; operator default |

Waypoint limits count all of a player's worlds. Zero blocks new waypoints; lowering a limit preserves existing records. Without a numeric or unlimited grant, `Atlas.WaypointsPerPlayer` applies (default 64). The button/settings groups do not grant unlimited waypoints, and quota grants do not unlock creation actions.

For example, with LuckPerms:

```text
/lp group default permission set beastminimap.buttons.* true
/lp group default permission set beastminimap.settings.* true
/lp group default permission set beastminimap.waypoints.limit.16 true
```

`Permissions.RequireExplicitGrants: false` permits unassigned controls while honoring explicit denials. Denied actions show the editable language message and play a configurable villager rejection sound, with a feedback cooldown. Back/cancel, the recovery key and `/beastminimap map close` remain available after access changes.

See the [complete permissions guide](docs/permissions.md) for every action, wildcard group, quota rule and configuration option.

## What is inside a complete pack?

Each complete ZIP contains the map interface artwork, buttons, player/place icons, minimap instruments, bitmap fonts, shaders and metadata for that Minecraft client version, plus the server artwork used to prepare all seven themes. It does not contain Java editor helpers, plugin implementation or server world maps. Edit optional theme PNGs through the supported runtime theme system; carrier cells are rebuilt automatically during preparation.

Machine-readable download and compatibility information: [packs.json](packs.json).

<!-- BEGIN BEASTMINIMAP LANGUAGES -->
## Languages

English (`en-US.yml`) is the default. The plugin bundles 33 European/US-English
language files, including Russian and Turkish. The remaining 17 files are
available in the [matching language snapshot](https://github.com/MrAxeTv/BeastMiniMap/tree/languages-502f0eddb9c0c115/languages).

Selecting an optional filename downloads its matching defaults in the background
when `Options.Language.Settings.AutoDownload: true` (the default). Set it to
`false` to use manual installation. English remains available offline.

For manual installation, download the YAML into `plugins/BeastMiniMap/Lang/`,
select its exact filename with `Options.Language.Settings.File` in `config.yml`,
then run `/beastminimap reload` or restart normally. Existing local edits are
preserved. See [language downloads and checksums](languages/README.md).

Translations are machine-assisted. Use `Atlas.MenuUi: native` for scripts the
compact bitmap font cannot display; retain Latin text for the atlas header.
<!-- END BEASTMINIMAP LANGUAGES -->
