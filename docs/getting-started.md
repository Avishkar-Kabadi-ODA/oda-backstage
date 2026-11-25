# Getting Started

Run Unity locally with Docker Compose.

## Before you begin

- Docker Desktop (Windows or macOS) or Docker Engine (Linux), with Compose v2
- At least 8 GB of RAM available to Docker
- About 10 GB of free disk space
- Ports 8080 and 3307 free on your machine

## Start the stack

1. Copy the example configuration:

   ```bash
   cp .env.example .env
   ```

2. Set the database and administrator passwords in `.env`.

3. Start everything:

   ```bash
   docker compose up -d
   ```

4. Follow the site creation. It installs every app and takes 10 to 20 minutes:

   ```bash
   docker compose logs -f create-site
   ```

   Wait until the `create-site` container exits with code 0.

5. Open `http://localhost:8080` and sign in as `Administrator` with the password from `.env`.

## Check that it works

```bash
docker compose ps -a
docker compose exec backend bench version
```

All services should be `Up`, except one-shot services such as `configurator`, `create-site` and `nltk-init`, which exit with code 0.

## Next steps

- [Install](guides/install.md) for the full installation guide
- [Configure](guides/configure.md) for settings you will want to change
