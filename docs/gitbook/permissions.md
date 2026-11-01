# Permissions

BeastMiniMap checks the same action permission for atlas buttons, pixel and
native dialogs, shortcuts and commands. Permission nodes are lowercase and
case-insensitive. Use the lowercase spelling shown here when granting them.
`beastminimap.use` remains the basic player command permission; administrator
operations retain `beastminimap.admin`, and shared-place editing retains
`beastminimap.places.admin`.

## Access defaults and wildcard grants

The bundled configuration requires action grants:

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

With `RequireExplicitGrants: true`, an ordinary player needs the relevant
`beastminimap.buttons.*` or `beastminimap.settings.*` child permission. Each
individual button or setting permission defaults to false. The wildcard groups
have operator defaults. Grant the two groups to a role that should retain all
player controls, or grant individual nodes to provide fewer controls.

Set `Permissions.RequireExplicitGrants: false` to retain the previous open
player-control access while still honoring explicit denials. Reload after
editing this configuration. Existing `beastminimap.use`, administrator and
shared-place permission checks still apply.

| Grant | Scope |
| --- | --- |
| `beastminimap.buttons.*` | All player button actions |
| `beastminimap.settings.*` | All player settings |
| `beastminimap.waypoints.limit.*` | Unlimited personal waypoint creation |
| `beastminimap.waypoints.limit.unlimited` | Unlimited personal waypoint creation |
| `beastminimap.*` | All declared BeastMiniMap permissions, including unlimited waypoints |

An explicitly false child takes precedence over a broader wildcard. For
example, grant `beastminimap.settings.*` and set one settings node to false to
lock that row. An explicit false `beastminimap.waypoints.limit.unlimited` also
blocks unlimited access inherited from a broader wildcard. The button and
settings wildcards do not grant unlimited waypoints.

## Personal waypoint limits

Grant `beastminimap.waypoints.limit.N`, replacing `N` with a nonnegative whole
number. The highest true numeric grant is the player's limit. A limit of zero
blocks new personal waypoints. False numeric nodes do not contribute a limit.
When there is no numeric grant and no unlimited grant, the configured
`Atlas.WaypointsPerPlayer` supplies the limit; its bundled default is 64.

The limit counts all of the player's personal waypoints across worlds. It does
not include shared server places. Lowering a limit never deletes or hides
existing waypoints. A player at or above the limit can still access existing
waypoints through the actions they are permitted to use; creating another
requires room below the current limit. Creation from a map location and
creation from a command use the same limit check.

Numeric limits are independent of action grants. Granting a limit does not
grant access to the creation button or command. Unlimited access also requires
the action permission to create a waypoint.

## LuckPerms examples

Grant all player controls to the default group, then choose a numeric waypoint
limit:

```text
/lp group default permission set beastminimap.use true
/lp group default permission set beastminimap.buttons.* true
/lp group default permission set beastminimap.settings.* true
/lp group default permission set beastminimap.waypoints.limit.16 true
/lp group vip permission set beastminimap.waypoints.limit.128 true
```

A VIP who inherits the default group receives the higher true limit, 128.
Use `beastminimap.waypoints.limit.unlimited` for a role with unlimited personal
waypoints. Grant only `beastminimap.buttons.open` to a role that should open the
atlas without receiving every atlas action, then add the desired individual
button and setting nodes from the catalog below.

For example, allow the atlas and settings menu while granting only two setting
rows:

```text
/lp group explorer permission set beastminimap.use true
/lp group explorer permission set beastminimap.buttons.open true
/lp group explorer permission set beastminimap.buttons.settings true
/lp group explorer permission set beastminimap.settings.minimap.shape true
/lp group explorer permission set beastminimap.settings.atlas.playericon true
```

To grant all settings except theme changes and minimap resizing, use explicit
false leaves:

```text
/lp group default permission set beastminimap.settings.* true
/lp group default permission set beastminimap.settings.theme false
/lp group default permission set beastminimap.settings.minimap.size false
```

## Denial feedback and safe exit

Denied actions use the selected language's `Permissions.Denied` message.
This entry is editable under `plugins/BeastMiniMap/Lang/`, alongside the
existing waypoint-limit message.
The default sound is `ENTITY_VILLAGER_NO`. `Name`, `Volume`, `Pitch` and
`CooldownMs` configure the denial sound, and `Enabled: false` silences it.
The cooldown prevents repeated attempts from repeating denial feedback
continuously.

Permissions are checked again when an action executes. Applying a settings
draft rechecks each changed field, so a grant removed while the dialog is open
cannot save an unauthorized change; Apply saves the draft only when all of
its changed fields remain permitted. `beastminimap.buttons.close` controls the
atlas toolbar and native atlas Close buttons. Back/cancel controls for settings,
search and the journal, the recovery key, `/beastminimap map close`, and normal
input/session cleanup remain usable after access changes.

## Action catalog

The individual nodes below are checked in addition to the existing basic,
administrator or shared-place permission for the relevant operation.

| Button permission | Action |
| --- | --- |
| `beastminimap.buttons.open` | Open the atlas, including its configured opening shortcut |
| `beastminimap.buttons.search` | Open and use map search |
| `beastminimap.buttons.zoom.in` | Zoom the atlas in |
| `beastminimap.buttons.zoom.out` | Zoom the atlas out |
| `beastminimap.buttons.waypoints.create` | Create a personal waypoint, subject to the current limit |
| `beastminimap.buttons.waypoints.list` | Open the personal waypoint journal |
| `beastminimap.buttons.waypoints.edit` | Edit a personal waypoint |
| `beastminimap.buttons.waypoints.delete` | Delete a personal waypoint |
| `beastminimap.buttons.waypoints.track` | Select a personal waypoint as a destination |
| `beastminimap.buttons.waypoints.visibility` | Change personal waypoint visibility |
| `beastminimap.buttons.waypoints.edge` | Change personal waypoint edge markers |
| `beastminimap.buttons.settings` | Open player settings |
| `beastminimap.buttons.center` | Center the atlas on the player |
| `beastminimap.buttons.close` | Use the atlas close control |
| `beastminimap.buttons.centerpoint` | Toggle the map-center crosshair |
| `beastminimap.buttons.pan` | Pan the atlas |
| `beastminimap.buttons.help` | Open atlas help |
| `beastminimap.buttons.places.track` | Select a shared place as a destination |
| `beastminimap.buttons.places.visibility` | Change shared-place visibility |
| `beastminimap.buttons.places.minimap` | Change shared-place minimap visibility |
| `beastminimap.buttons.places.edge` | Change shared-place edge markers |

| Setting permission | Player setting |
| --- | --- |
| `beastminimap.settings.sensitivity` | Atlas pointer sensitivity |
| `beastminimap.settings.searchinput` | Search typing method |
| `beastminimap.settings.atlas.zoom` | Atlas zoom preference |
| `beastminimap.settings.atlas.layout` | Fullscreen or framed atlas layout |
| `beastminimap.settings.atlas.icons` | Atlas icon style |
| `beastminimap.settings.atlas.iconsize` | Atlas waypoint/place icon size |
| `beastminimap.settings.atlas.playericon` | Atlas player symbol |
| `beastminimap.settings.atlas.playersize` | Atlas player-symbol size |
| `beastminimap.settings.minimap.enabled` | Minimap visibility |
| `beastminimap.settings.minimap.shape` | Minimap outline shape |
| `beastminimap.settings.minimap.corner` | Minimap screen corner |
| `beastminimap.settings.minimap.size` | Minimap size |
| `beastminimap.settings.minimap.zoom` | Minimap zoom preference |
| `beastminimap.settings.minimap.iconsize` | Minimap waypoint/place icon size |
| `beastminimap.settings.minimap.playericon` | Minimap player symbol |
| `beastminimap.settings.minimap.playersize` | Minimap player-symbol size |
| `beastminimap.settings.coordinates` | Minimap coordinate-panel visibility |
| `beastminimap.settings.coordinatewidth` | Automatic or fixed coordinate-panel width |
| `beastminimap.settings.places.edgeicons` | Shared-place edge-icon presentation |
| `beastminimap.settings.caves` | Cave/surface presentation in layered worlds |
| `beastminimap.settings.keybind.modifiers` | Opening-shortcut modifiers |
| `beastminimap.settings.keybind.trigger` | Opening-shortcut trigger |
| `beastminimap.settings.theme` | Personal map theme |
| `beastminimap.settings.reset` | Stage server defaults for permitted fields in the settings draft |

Reset requires `beastminimap.settings.reset` and stages defaults only for fields
the player may change. Locked fields retain their draft values. The opening
shortcut's modifiers and trigger keep their separate permissions, including
during Reset. Apply rechecks all changed field permissions before saving.
Theme, marker and other previews do not grant permission to save a locked
choice; explicitly reapplying the current theme also requires theme permission.
