# Personal Waypoints and Public Places

Personal waypoints belong to their player. Public places are shared destinations created by administrators. Both are restricted to their world; selecting a destination guides you on the map and does not teleport you.

## Create a Personal Waypoint

Use the atlas's New Waypoint tool or right-click a discovered map location to start a marker draft. Enter a name and review its coordinates and color, then save it. The location must have visible discovered terrain that the map can pick.

To save your current position instead:

```text
/beastminimap waypoint add Home
```

Names can contain spaces and must contain 1–40 characters. Names must be unique within your waypoints in the same world. Personal waypoints use the Pin category; the special destination categories belong to public places.

## Use the Journal

```text
/beastminimap waypoint list
/beastminimap waypoint select Home
/beastminimap waypoint remove Home
```

The atlas journal lets you locate a marker, edit it, hide or show it, change its edge-marker preference, or delete it. Hiding a marker preserves its saved location and edge preference. The journal's individual actions may have different permissions.

> **Screenshot placeholder — waypoint journal:** Show several personal markers and the edit/create form. Suggested image: `06-personal-waypoints.png`. Add `07-server-place-search.png` alongside the public-place instructions below.

## Waypoint Allowances

Administrators assign personal allowances through [permissions](../permissions.md):

```text
beastminimap.buttons.waypoints.create
beastminimap.waypoints.limit.16
```

The highest true numeric limit wins and counts all of that player's worlds. A zero limit blocks new markers. Without a numeric or unlimited grant, `Atlas.WaypointsPerPlayer` supplies the fallback, normally 64.

`beastminimap.waypoints.limit.unlimited` removes the quota. It does not grant the creation action. Lowering a quota never deletes or hides existing waypoints; the player must make room below the new allowance before creating another.

The number stored is separate from the bounded number of markers drawn at once.

## Find Public Places

Use Search in the atlas or:

```text
/beastminimap place list
/beastminimap place search Market
/beastminimap place select Market
```

Search supports the vanilla anvil input by default. Players with permission can choose another available typing method in [settings](../customization/player-settings.md). Escape leaves the text input and returns to map navigation.

Place visibility, minimap visibility and edge markers can be adjusted through the place controls when permitted. These are personal display choices, not edits to the shared destination.

## Create Public Places

An administrator with `beastminimap.places.admin` can stand at a destination and run:

```text
/beastminimap place add market Central Market
/beastminimap place describe Central Market Buy and sell supplies here
/beastminimap place icon house Central Market
```

Available categories are `pin`, `house`, `market`, `dungeon`, `tower`, `temple`, `quest` and `harbor`. Use tab completion to select a supported ID. `/beastminimap place remove Central Market` deletes the shared record.

`Atlas.PlacesLimit` sets the server-wide place allowance, normally 256. Public places do not consume personal waypoint quotas. Records are saved in the configured [SQL storage](../storage.md).
