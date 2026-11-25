# Commands

Common commands, run from the folder that contains `compose.yaml`.

## Stack

| Task | Command |
|---|---|
| Start | `docker compose up -d` |
| Stop, keep data | `docker compose stop` |
| Remove containers, keep data | `docker compose down` |
| Remove containers and data | `docker compose down -v` |
| Status, including one-shot services | `docker compose ps -a` |
| Logs | `docker compose logs -f <service>` |
| Recreate after an image or `.env` change | `docker compose up -d --force-recreate` |

## Bench

Run inside the backend container with `docker compose exec backend ...`.

| Task | Command |
|---|---|
| Versions of all apps | `bench version` |
| Apps installed on a site | `bench --site <site> list-apps` |
| Install an app | `bench --site <site> install-app <app>` |
| Run migrations | `bench --site <site> migrate` |
| Clear cache | `bench --site <site> clear-cache` |
| Show site configuration | `bench --site <site> show-config` |
| Set a site option | `bench --site <site> set-config <key> <value>` |
| Backup with files | `bench --site <site> backup --with-files` |
| Console | `bench --site <site> console` |

## Image

| Task | Command |
|---|---|
| List apps in an image | `docker run --rm --entrypoint ls <image> apps` |
| Versions in an image | `docker run --rm --entrypoint bench <image> version` |
