# Live terrain and caves

Live maps collect terrain from chunks already loaded around players. As players
explore, the map can retain their discovered terrain for later visits. Multiple
players can reuse collected terrain without sharing their personal exploration
records.

Start with `live_terrain` for surface mapping. To add underground layers:

```text
/beastminimap world source live_strata world
```

This requires `beastminimap.admin`. It changes that world's source; other worlds
keep their configured choices.

## Player cave choices

In a `live_strata` world, players can select a cave preference in Map Settings or
run one of these commands:

| Command | Choice |
| --- | --- |
| `/beastminimap caves sky_light` | Automatic: follow sky exposure at the player's eyes |
| `/beastminimap caves open_air` | Keep the surface view |
| `/beastminimap caves deep_layers` | Follow cave layers at the player's current height |

The choice applies to the minimap and atlas and saves per player. It requires
`beastminimap.settings.caves` in addition to normal command access. It has no
cave effect in a `live_terrain` or `world_texture` world.

Automatic mode selects caves when sky light at the player's eyes is zero.
Torches do not change sky exposure. An enclosed building or tunnel can therefore
select a cave view too. Forced cave mode follows the player's height; it does not
let them browse arbitrary underground levels.

The default layer height is 16 blocks. The named ceiling guides a search for the
visible cave floor rather than showing every room above and below the player.
Surface and cave exploration remain separate: visiting the surface does not
uncover the caves underneath it.

> **Screenshot placement:** compare surface and cave views from the same region in `08-cave-layers.png`, with the selected mode labelled.

## Capture and refresh

Live captures stay within configured work limits and do not generate chunks.
Block changes invalidate nearby recorded terrain, while periodic refreshes
check loaded areas around players. Previously recorded distant terrain may
remain visible until its sources are refreshed.

These defaults are in `config.yml`:

```yaml
Terrain:
  SaveSources: true
  ObservationSharing: global
  CaptureRadiusChunks: -1
  NearbyRefreshTicks: 400
  CapturesPerTick: 12
  CaveLayers:
    SliceHeight: 16
    CaptureRadiusChunks: 6
    CapturesPerTick: 4
    SourceMemoryMib: 32
    SourceDiskMib: 256
    RoofSearchBlocks: 32
```

`CaptureRadiusChunks: -1` follows the player's effective server view distance.
Cave captures use a share of the ordinary capture budget; their setting does
not add four extra captures on top of the twelve.

`ObservationSharing` selects how retained live terrain is shared:

- `global` reuses the latest shared terrain within each player's discovered
  area.
- `nearby` retains that player's last-seen terrain until they revisit nearby.

Neither mode reveals a player's undiscovered live-map areas merely because
someone else has explored them. `SaveSources` controls terrain persistence;
player discovery itself is stored separately in SQL.

## Preparing existing terrain

An administrator can prepare reusable source data from saved chunks:

```text
/beastminimap world prerender world
/beastminimap world status world
/beastminimap world cancel world
```

This prepares the live-terrain cache. It does not generate new world chunks,
create a saved world-image PNG or reveal the world for players. Preparation has
worker, chunk-count and disk budgets under `Terrain.SourcePreparation` in
`config.yml`. Cancelling keeps completed source work.

If a cave view or newly explored area is blank, first check that the player has
visited it, the appropriate layer is selected, and the nearby chunks are loaded.
An unvisited or unavailable source is not filled by generating chunks in the
background.

See [terrain sources](overview.md), [storage and discovery](../storage.md),
and [permissions](../permissions.md) for the related settings.
