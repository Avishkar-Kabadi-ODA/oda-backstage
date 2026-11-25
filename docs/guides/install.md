# Install

This guide installs Unity from the published Docker image.

## Requirements

| Item | Minimum |
|---|---|
| Docker Engine and Compose | Compose v2 |
| Memory | 8 GB for Docker |
| Disk | 10 GB free, more for production data |
| Network | Internet access on the first run to pull images |

## Files

Keep these two files in the same folder:

- `compose.yaml`
- `.env.example`, copied to `.env`

## Steps

1. Create your configuration file:

   ```bash
   cp .env.example .env
   ```

2. Edit `.env`. Set strong passwords before the first start. They are applied only when the database and site are first created.

3. Start the stack:

   ```bash
   docker compose up -d
   ```

4. Wait for site creation to finish:

   ```bash
   docker compose logs -f create-site
   docker compose ps -a create-site
   ```

   The status must be `Exited (0)`.

5. Check the installed apps:

   ```bash
   docker compose exec backend bench --site <site> list-apps
   ```

## Verify the image contents

Before starting a new image, check that every app is baked in:

```bash
docker run --rm --entrypoint ls <image> apps
docker run --rm --entrypoint cat <image> sites/apps.txt
docker run --rm --entrypoint bench <image> version
```

An app that is in the image but not on the site is installed with:

```bash
docker compose exec backend bench --site <site> install-app <app>
docker compose exec backend bench --site <site> migrate
```

## Troubleshooting

| Problem | What to check |
|---|---|
| `start.sh: cannot execute: required file not found` | The shell scripts have Windows (CRLF) line endings. Build the image from files with LF endings |
| `create-site` fails | `docker compose logs create-site`, then reset with `docker compose down -v` before retrying |
| Worker log shows a Redis connection error once at start | Normal startup timing. It is fine if the worker then reports `Listening on` its queues |
| An app is missing from the site | Install it with `install-app` as shown above |

## Reset

This deletes the database and all site data:

```bash
docker compose down -v
docker compose up -d
```
