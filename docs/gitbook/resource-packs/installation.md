# Resource-Pack Installation

BeastMiniMap needs a complete pack matching the player's Minecraft client. Download packs from the [official GitHub releases](https://github.com/MrAxeTv/BeastMiniMap/releases), using the asset release intended for your plugin build.

## Choose the correct filename

| Minecraft client | Complete pack |
| --- | --- |
| 1.21.9 or 1.21.10 | `BeastMiniMap-1.21.9.zip` |
| 1.21.11 | `BeastMiniMap-1.21.11.zip` |
| 26.1, 26.1.1 or 26.1.2 | `BeastMiniMap-26.1.zip` |
| 26.2 | `BeastMiniMap-26.2.zip` |
| 26.3 | `BeastMiniMap-26.3.zip` |

Install only the versions you need. A server accepting several client versions may need several ZIPs. When ViaVersion is installed, pack selection uses the original client protocol; changing the server version does not make one client's pack suitable for every other client.

## Put the complete ZIPs in Packs

```text
plugins/BeastMiniMap/Packs/
  BeastMiniMap-1.21.9.zip
  BeastMiniMap-26.3.zip
```

Keep each original filename and leave the archive intact. Do not extract it, rename another version's ZIP to match a missing filename, or install its nested preparation artwork separately.

Every complete ZIP contains the base assets and all seven built-in themes. There is no separate required artwork download. The plugin JAR includes no pack ZIPs or artwork PNGs, and the plugin does not automatically download these assets.

## Load the inputs

After adding or replacing only pack assets, run:

```text
/beastminimap reload
```

Installing a new plugin JAR requires a normal server restart. A missing or invalid pack for one client version leaves other valid installed versions available. Administrative commands remain available even when no usable pack is installed.

The plugin prepares effective client downloads under:

```text
plugins/BeastMiniMap/Packs/Prepared/
```

The installed complete ZIP is an input. Prepared ZIPs are the resulting files offered to clients after artwork and any supported composition have been applied. See [hosting](hosting.md) before using an external website to distribute them.

## Join and accept the offer

Players must accept the current BeastMiniMap pack for their connection. After applying it, open `/beastminimap`. A manual retry is available through:

```text
/beastminimap pack
```

Use `/beastminimap pack info` to inspect delivery details. The plugin's missing-pack panel provides the expected filename, folder and official download link; its reload action suggests a command rather than executing it automatically.

## Themes and updates

Selecting an installed theme in Map Settings switches its artwork without another pack download. Adding a custom theme or editing artwork changes the prepared pack; reload and allow players to accept the updated result.

An unchanged pack can reuse client downloads and caches. A changed pack can take longer to apply, particularly when new shaders must compile. Download size alone does not measure the entire apply time.

## Other resource packs

Other plugins or player packs that replace the same Minecraft core shaders can conflict. Use supported composition where available and test the resulting combined pack. The presence of an unrelated pack does not count as acceptance of BeastMiniMap's own offer.
