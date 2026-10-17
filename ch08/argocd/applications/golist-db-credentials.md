# Local MariaDB credentials

`golist-db.yaml` uses the separately provisioned Secret
`golist/golist-db-credentials`. Argo CD manages the Helm resources but does not
generate or rotate this Secret. Keep it when re-syncing or recreating pods.

Required Secret keys:

- `mariadb-root-password`: the root password stored in MariaDB.
- `mariadb-password`: the `golist` user's password (`golist` for this local lab,
  matching the API ConfigMap).
- `mariadb-replication-password`: retained for compatibility with the chart.

Provision the Secret before deploying this Application to a new cluster. Store
credentials outside Git and preserve them with database backups. Changing a
Secret does not change credentials in an initialized database on a PVC; update
the database accounts and Secret together.

The local API image remains `golist-api:local-arm64`. Password recovery does not
require rebuilding or downloading the API image.
