# Player Commands

`/beastminimap` is the permanent root. Default aliases are `/minimap`, `/bmm` and `/map`; they all run the same command tree. Another plugin may own an alias, so these examples use the permanent root.

An alias does not choose atlas mode: `/map zoom 5` changes minimap zoom. `/beastminimap map zoom 5` changes atlas zoom.

## General and Minimap

| Command | Action |
| --- | --- |
| `/beastminimap` | Open fullscreen; the server can configure help instead |
| `/beastminimap help` | Show command help |
| `/beastminimap on` / `off` / `toggle` | Set or toggle minimap visibility |
| `/beastminimap status` | Show your map/session status |
| `/beastminimap shape disc` | Set `disc`, `hexagon` or `box` |
| `/beastminimap corner upper_right` | Set one of the four screen corners |
| `/beastminimap size normal` | Set `small`, `normal`, `large`, `smaller`, `bigger` or 64–256 |
| `/beastminimap zoom 7` | Set minimap level 1–10; also accepts `in`, `out`, `reset` |
| `/beastminimap caves sky_light` | Choose `sky_light`, `open_air` or `deep_layers` in layered worlds |
| `/beastminimap pack` | Request the matching map resource pack again |

Corner IDs are `upper_left`, `upper_right`, `lower_left` and `lower_right`.

## Atlas

| Command | Action |
| --- | --- |
| `/beastminimap map` | Toggle your preferred atlas layout |
| `/beastminimap map close` | Close the atlas; recovery remains available after access changes |
| `/beastminimap map settings` | Open personal settings |
| `/beastminimap map faq` | Open map help |
| `/beastminimap map reset` | Center the map on the player |
| `/beastminimap map cursor` | Return the pointer to the middle of the map |
| `/beastminimap map zoom 5` | Set atlas level 1–16; also accepts `in`, `out`, `reset` |
| `/beastminimap map pan 32 0` | Pan east/south by the supplied block distances |
| `/beastminimap map layout framed` | Set `full` or `framed` |
| `/beastminimap map icons colorful` | Set `colorful` or `regular` destination icons |
| `/beastminimap map typing anvil` | Set `anvil`, `helper`, `auto` or `commands` search input |
| `/beastminimap map sensitivity 2` | Set pointer sensitivity 0.25–4; also accepts `reset` |
| `/beastminimap map search Market` | Open public-place search |
| `/beastminimap map waypoints` | Open the personal waypoint journal |

`atlas` can replace the `map` subcommand. Root opening forces fullscreen for that session without changing your saved layout; `map` opening uses the saved preference.

## Shortcuts and Destinations

```text
/beastminimap keybind
/beastminimap keybind set SNEAK+SWAP_HAND
/beastminimap keybind reset
/beastminimap waypoint new
/beastminimap waypoint add Home
/beastminimap waypoint list
/beastminimap waypoint select Home
/beastminimap waypoint remove Home
/beastminimap place list
/beastminimap place search Market
/beastminimap place select Market
```

`waypoint new` opens the map's creation form; `waypoint add <name>` saves the player's current position. Names may contain spaces. Selection sets a destination, not a teleport. See [waypoints and places](../maps/waypoints-and-places.md) and [shortcuts](../customization/keybinds.md).

## Permissions

Player commands require `beastminimap.use` and the relevant action/setting grant. The default explicit-grant policy applies equally to commands, shortcuts and menus. A command cannot bypass a locked setting or waypoint quota. See the [full permission list](../permissions.md).

Players wait for their saved data to load before changing it. If the plugin reports that data is still loading, retry shortly rather than resetting the database.
