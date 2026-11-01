# Saved world images

`world_texture` displays a saved RGB image of a chosen world area. Rendering
reads existing region files on workers without loading or generating Minecraft
chunks. It is useful for a known spawn, city or adventure-map area that does not
need continuous live repainting.

An image reflects saved world data. Save important world edits before rendering;
unsaved changes cannot appear in the output. After later terrain or colour
changes, explicitly render a replacement image.

> **Screenshot placement:** show a completed saved image in the atlas as `09-world-image.png`, with recognizable landmarks and the rendered area visible.

## Render around your position

1. Join the world you want to map and stand at the desired centre.
2. Confirm the side length in `worlds.yml`; the default is 4096 blocks.
3. Run the render command and inspect its reported bounds/status.
4. Select `world_texture` to use the completed image.

```text
/beastminimap world render world
/beastminimap world status world
/beastminimap world source world_texture world
```

All three commands require `beastminimap.admin`. A player in the target world
can omit its name. `/beastminimap render world` is a shortcut for the same image
render command.

The command captures your current block X/Z once. Movement afterward does not
move the job. You must stand in the target world; an in-game request cannot use
your position to centre another world's render.

With `RenderSizeBlocks: 4096`, standing at **X=1000, Z=2000** selects these
inclusive corners:

| Axis | Minimum | Maximum | Length |
| --- | --- | --- | --- |
| X | -1048 | 3047 | 4096 blocks |
| Z | -48 | 4047 | 4096 blocks |

The selected rectangle belongs to that job. It does not overwrite configured
`Bounds`, change the world's source, move the player or reveal their live-map
discovery. The completed image keeps its actual rectangle for reuse after a
restart.

## Configure size and resolution

These settings belong in `worlds.yml`. Edit the existing sections and replace
`world` with the exact world name:

```yaml
Defaults:
  TerrainSource: live_terrain
  BlocksPerPixel: 1
  RenderSizeBlocks: 4096
  RenderOnLoad: false
  Bounds: auto
  MaxImageSide: 8184
  MaxSourcePixels: 16777216
  Workers: 4
  Relief: 0.7
  WaterDepth: 1.0
  Contrast: 1.04
Worlds:
  world:
    TerrainSource: world_texture
    RenderSizeBlocks: 4096
```

Run `/beastminimap reload` after file edits, then explicitly render the area.

| Setting | Meaning |
| --- | --- |
| `RenderSizeBlocks` | Width and height of player-centred render commands; whole numbers 1–8192 |
| `BlocksPerPixel` | Output sampling scale; 1 preserves one-block detail, larger values reduce resolution |
| `MaxSourcePixels` | Source-area safety budget, checked before output downsampling |
| `MaxImageSide` | Maximum output side length |
| `Workers` | Worker count for the image job |
| `Relief` / `WaterDepth` / `Contrast` | Saved-image shading controls |

The default 4096-square area contains 16,777,216 source pixels. A larger
`RenderSizeBlocks` may exceed the default source budget. Increasing
`BlocksPerPixel` makes the output smaller but does not reduce the initial
source-area requirement. Reduce the selected area first if a job exceeds its
budget; only increase budgets when the server has suitable memory available.

## Console bounds and automatic rendering

Console commands and automatic jobs use `Bounds`, rather than a player's
position. `Bounds: auto` fits the existing saved chunks. To select an explicit
inclusive rectangle, set the world entry:

```yaml
Worlds:
  world:
    TerrainSource: world_texture
    Bounds:
      MinX: -2048
      MinZ: -2048
      MaxX: 2047
      MaxZ: 2047
```

From console, run `beastminimap world render world`. A player using the same
command still selects their current centre and `RenderSizeBlocks`, so use
console when you specifically want the configured rectangle.

`RenderOnLoad: true` can render a `world_texture` source when it loads without
an existing saved image manifest. It does not repaint an existing image every
restart. Explicit render commands rebuild even when a saved image exists.

## Delivery, replacement and cancellation

Players need the matching [base resource pack](../resource-packs/installation.md)
and the prepared image addon. Use a reachable content-addressed pack URL with
`{sha1}` or `{path}` so different images have different download addresses.

The previous committed image remains available until a replacement succeeds.
If a job fails or is cancelled, it does not erase that last good image. Use:

```text
/beastminimap world cancel world
/beastminimap world status world
```

Successful replacements are offered through the normal resource-pack flow.
Outside the saved rectangle the minimap can fall back to live terrain. Source
selection and image rendering are separate, so you can return to live mapping
with `/beastminimap world source live_terrain world` without resetting player
data.

See [terrain sources](overview.md) and
[administrator commands](../commands/admin-commands.md) for the other world
operations.
