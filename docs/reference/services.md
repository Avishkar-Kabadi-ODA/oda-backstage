# Services

The containers that make up the Unity stack.

| Service | Role |
|---|---|
| `backend` | Frappe application server |
| `frontend` | Nginx serving the UI and proxying to the backend |
| `websocket` | Real-time updates (Socket.IO) |
| `websocket-proxy` | Forwards websocket traffic |
| `queue-short` | Background worker for short jobs |
| `queue-long` | Background worker for long jobs |
| `scheduler` | Runs scheduled jobs |
| `db` | MariaDB database |
| `redis-cache` | Cache |
| `redis-queue` | Job queue |
| `configurator` | One-shot: writes the shared site configuration |
| `create-site` | One-shot: creates the site and installs the apps |
| `nltk-init` | One-shot: prepares language data |
| `backup` | Backup job |

One-shot services exit with code 0 when they finish.

## Volumes

| Volume | Holds |
|---|---|
| `sites` | Site files, configuration and uploads |
| `logs` | Application logs |
| `db-data` | Database files |
| `redis-queue-data` | Queue persistence |

Data survives `docker compose down` and is removed only by `docker compose down -v`.
