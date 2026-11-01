# Plugin Configuration

BeastMiniMap stores its editable settings under `plugins/BeastMiniMap/`. Configuration keys are case-sensitive: use the PascalCase spelling shown in the generated files.

## Which file should I edit?

| File or folder | Purpose |
| --- | --- |
| `config.yml` | Commands, permissions, minimap/atlas defaults, live-terrain budgets, menus, themes and pack hosting |
| `worlds.yml` | Per-world terrain source, saved-image render settings and plant filtering |
| `storage.yml` | SQLite or MySQL selection and connection settings |
| `discovery.yml` | Exploration persistence, retry and active-memory limits |
| `Lang/<locale>.yml` | Player/admin messages, menu labels and the framed atlas title |
| `Themes/<Name>/Theme.yml` | Optional custom theme definitions |

Player preferences, personal waypoints, public places and discoveries are SQL data. They are not a collection of new per-player YAML files. See [storage](../storage.md).

## Apply settings safely

Back up the file, edit the relevant existing section, then run:

```text
/beastminimap reload
```

Use the plugin's command rather than Bukkit's general `/reload`. A new plugin JAR needs a normal restart. Changes to the selected storage backend, database connection, path or table prefix need a deliberate data transfer and restart; the ordinary configuration reload does not switch databases.

The examples below are partial snippets. Merge them into the existing sections rather than replacing your entire file or adding the same top-level section twice. Use spaces for YAML indentation.

## Commands and aliases

```yaml
Commands:
  Aliases: [minimap, bmm, map]
  ShowHelpOnNoArguments: false
```

`/beastminimap` is the permanent command. Every configured alias has the same behavior as that root command. For example, `/map zoom 5` changes **minimap** zoom; `/beastminimap map zoom 5` changes **atlas** zoom.

With `ShowHelpOnNoArguments: false`, the root opens the fullscreen atlas. Set it to `true` to show help instead. `/beastminimap help` remains available in either case. An empty `Aliases: []` list disables optional aliases. Other plugins can keep aliases they already own.

## Initial player defaults

```yaml
Hud:
  EnabledByDefault: true
  DefaultZoom: x7
  Shape: disc
  Corner: upper_right
  Size: 96
  Coordinates: true
  AutoFitCoordinatePanel: true
Atlas:
  FullScreen: true
  SearchInput: anvil
  MenuUi: pixel
```

These values provide initial choices for players without saved preferences. Returning players keep their own saved choices. Reloading does not reset all players to the server defaults.

Minimap shapes are `disc`, `hexagon` and `box`. Corners are `upper_left`, `upper_right`, `lower_left` and `lower_right`. Configuration zoom identifiers use an `x` prefix, such as `x7`; commands use the plain number, such as `7`.

`Atlas.MenuUi` selects `pixel` or `native` for the server's settings, help and personal waypoint menus. `Atlas.SearchInput: anvil` is the default vanilla typing method. Use native menus when the compact map font cannot display the selected language's script.

## Action permissions

```yaml
Permissions:
  RequireExplicitGrants: true
  DeniedSound:
    Enabled: true
    Name: ENTITY_VILLAGER_NO
    Volume: 0.5
    Pitch: 1.0
    CooldownMs: 500
```

Grant the desired button and settings permissions to player roles. Set `RequireExplicitGrants: false` only when you want unassigned player controls to remain available; explicit denials still apply. The denial text is editable as `Permissions.Denied` in the selected language file. See [all permissions and waypoint limits](../permissions.md).

## World and quality settings

Terrain source selection belongs in `worlds.yml`. The available source IDs are `live_terrain`, `live_strata` and `world_texture`; see [terrain sources](../terrain/overview.md).

Live sampling and saved-image resolution are separate settings. `Terrain.SamplingDetail` in `config.yml` controls live source quality by map and zoom level. `BlocksPerPixel` in `worlds.yml` controls saved-image output resolution. Start with the defaults and change one setting at a time, measuring the result before changing budgets further.

## Pack and artwork changes

After changing installed pack inputs or custom artwork, reload and let players accept the changed prepared pack. Selecting an already installed theme in Map Settings does not require another pack download. See [resource-pack installation](../resource-packs/installation.md) and [hosting](../resource-packs/hosting.md).
