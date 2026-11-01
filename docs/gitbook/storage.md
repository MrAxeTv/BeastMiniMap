# Storage and discovery

BeastMiniMap stores player preferences, native map IDs, personal waypoints,
shared places and exploration in one selected SQL database. SQLite is the
default; MySQL is optional. Configuration remains in the editable YAML files.
Terrain caches and saved world images remain separate files.

On join, a player's preferences and waypoints load asynchronously into memory.
Map use and data-editing commands wait until that load is ready. Ordinary play
reads cached data; changed records save asynchronously. This avoids creating a
separate YAML file for every player during normal operation.

## SQLite

SQLite needs no external database server. These defaults are in
`plugins/BeastMiniMap/storage.yml`:

```yaml
Backend: SQLite
TablePrefix: beastminimap_
SQLite:
  File: Discovery/discovery.sqlite
  BusyTimeoutMillis: 5000
QueueCapacity: 1024
ShutdownTimeoutMillis: 10000
```

`SQLite.File` is relative to the BeastMiniMap data folder and must stay inside
it. The default database is
`plugins/BeastMiniMap/Discovery/discovery.sqlite`. The folder name does not mean
it stores exploration only; the other player records use the same database.

Keep the database and its `-wal`/`-shm` companion files together. For a simple
consistent backup, stop the server normally, then back up the whole plugin data
folder. Back up world folders too if you need their terrain caches and world
data restored together.

## MySQL

Create a database and an account that can create and use its tables, then edit
the existing `storage.yml` sections:

```yaml
Backend: MySQL
TablePrefix: beastminimap_
MySQL:
  Host: database.example.com
  Port: 3306
  Database: beastminimap
  Username: minimap
  Password: ''
  UsernameEnvironment: ''
  PasswordEnvironment: BEASTMINIMAP_DB_PASSWORD
  UseSSL: true
  ConnectTimeoutMillis: 5000
  SocketTimeoutMillis: 10000
  PoolSize: 4
QueueCapacity: 1024
ShutdownTimeoutMillis: 10000
```

This example reads the password from `BEASTMINIMAP_DB_PASSWORD` in the server
process environment. Set that variable before starting the server. If you
prefer a YAML password, leave `PasswordEnvironment: ''` and fill `Password`.
Likewise, a nonempty `UsernameEnvironment` selects an environment variable for
the username. Configured environment variables must exist; they override the
corresponding YAML credential.

`UseSSL: true` enables TLS with server identity verification. Use the correct
database hostname and certificates for your host. MySQL is contacted only when
selected. An existing installation needs a data transfer before changing to it;
changing the backend alone does not migrate saved records.

## Discovery

Exploration belongs to the player, world and terrain layer. Surface exploration
does not uncover caves. Preparing terrain or rendering a world image does not
mark chunks as explored for all players.

`discovery.yml` controls discovery and its working limits:

```yaml
Enabled: true
FlushIntervalMillis: 2000
RetryDelayMillis: 5000
ShutdownTimeoutMillis: 10000
Limits:
  ActivePlayerWorlds: 128
  RegionsPerPlayerWorld: 4096
```

`Limits.ActivePlayerWorlds` and `Limits.RegionsPerPlayerWorld` bound active
exploration memory. They are not a maximum number of accounts that can have
records in the SQL database. `storage.yml` selects the shared backend; there is
no separate discovery database-backend selector in `discovery.yml`.

The default live-terrain sharing policy reuses current terrain inside each
player's discovered area. It does not reveal their unexplored areas just
because another player visited them. See [live terrain and caves](terrain/live-and-caves.md).

## Reloads, transfers and backups

`/beastminimap reload` refreshes map configuration while retaining saved player
preferences and the selected storage service. Database backend, path, table
prefix and connection changes require a normal server restart.

For an existing installation, back up and transfer its data before selecting a
different database. `Storage/backend-selection.txt` records the established
destination. A mismatch stops accidental use of another empty database; do not
delete this file to dismiss the warning. Restore the previous settings or
complete the transfer, then update the selection record to match the verified
destination.

Changing server defaults does not reset saved player choices. Lowering a
[waypoint permission limit](permissions.md) also keeps existing waypoints; it
restricts new creation until the player is below the current allowance.

Older `players.yml`, `waypoints.yml`, `places.yml` and exploration YAML can be
imported on first background use. Existing SQL records take precedence, and the
original files remain. Malformed import data is reported instead of silently
replacing a player's records with defaults. Normal operation saves to SQL.

For backup restores, restore a consistent plugin data snapshot and the matching
database. For MySQL, use the database host's consistent backup/dump procedure
as well as backing up the plugin's YAML settings and selection record. Keep
database passwords out of public support logs.
