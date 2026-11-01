# Hosting the Resource Pack

Installing ZIPs in `Packs/` makes the assets available to the plugin. Players also need an HTTP or HTTPS address from which they can download the prepared pack. Inspect the effective setup with `/beastminimap pack info`.

## Built-in HTTP hosting

The following is a partial `config.yml` example. Merge it into the existing `Pack` section and replace the example address:

```yaml
Pack:
  Host:
    Enabled: true
    Bind: 0.0.0.0
    Port: 8862
  PublicUrl: 'http://YOUR-SERVER-IP:8862/beastminimap/{sha1}.zip'
```

`Bind` is the server's local listening interface. `0.0.0.0` listens on its available IPv4 interfaces; it is not a download address for players. Put the reachable public hostname or IP in `PublicUrl`.

Allow inbound **TCP** access to the selected port in the firewall and any required NAT/router forwarding. On a managed Minecraft host, use an allocated additional TCP port in both `Pack.Host.Port` and the advertised URL. The game server's main port does not automatically expose this HTTP listener.

Leaving `PublicUrl` blank is suitable for local testing, where its localhost fallback is reachable. For remote players, `localhost` points to their computer and cannot reach your server's pack host.

The built-in listener serves HTTP. Use an appropriately configured reverse proxy if you want to advertise HTTPS.

## Keep downloads tied to their content

The `{sha1}` URL placeholder gives different pack contents different addresses. This avoids serving new bytes under an old cached URL. The shared template also supports `{path}` and `{version}`.

Each installed client version and prepared artwork combination must resolve to its correct file. Do not redirect every content-addressed request to a single ZIP regardless of its requested hash.

## External web hosting

With `Pack.Host.Enabled: false`, publish the appropriate files from `plugins/BeastMiniMap/Packs/Prepared/` on your web host. Use the effective URL and hash reported by `/beastminimap pack info`; the complete source download is not a substitute for a prepared pack containing your server's effective artwork.

If a single fixed `PublicUrl` cannot select the right file for each version, configure the corresponding overrides:

| Client family | Override |
| --- | --- |
| 1.21.9 / 1.21.10 | `Pack.PublicUrl1219` |
| 1.21.11 | `Pack.PublicUrl12111` |
| 26.1 family | `Pack.PublicUrl261` |
| 26.2 | `Pack.PublicUrl262` |
| 26.3 | `Pack.PublicUrl263` |

For example, one version could use:

```yaml
Pack:
  Host:
    Enabled: false
  PublicUrl263: 'https://packs.example.com/minimap/26.3/{sha1}.zip'
```

Upload the file for every URL you advertise, including prepared theme variants used by your setup. After asset changes, publish the new prepared files before expecting clients to download them.

## Apply and check

1. Reload with `/beastminimap reload` after editing the hosting configuration.
2. Run `/beastminimap pack info` and inspect the advertised address.
3. Test that URL from outside the server's local network. It should return the ZIP directly, not a web login page or file-sharing preview.
4. Join with a matching supported client and accept the offered pack.
5. If needed, enable delivery diagnostics with `/beastminimap pack debug on`, reproduce once, then turn them off with `/beastminimap pack debug off`.

Downloading and applying are separate stages. If transfer completes but Minecraft is still reloading resources, inspect the client's logs and resource-pack conflicts before changing server download settings.

See [common issues](../troubleshooting/common-issues.md) for missing packs, rejected offers and slow application.
