# Configure

Settings you are most likely to change after installation.

## Passwords and site name

Set in `.env` before the first start. Changing them later does not update an existing database or administrator account.

## Developer mode

Developer mode is off by default and should stay off in production.

```bash
docker compose exec backend bench --site <site> set-config developer_mode 1
docker compose exec backend bench --site <site> clear-cache
docker compose restart backend websocket queue-short queue-long scheduler
```

Files written by developer mode go into the app folder inside the image. They are lost when the container is recreated, so develop in a bind-mounted bench and commit the result.

## Landing page after login

If users land in the wrong app after login, check these in order:

1. User: **Default App**
2. System Settings: **Default App**
3. Role: **Home Page**

Then clear the cache, restart the backend, and sign in again.

## Real client IP in logs

Behind a reverse proxy, logs show the proxy address unless the frontend trusts it. Set these on the `frontend` service, using your Docker network subnet:

```yaml
UPSTREAM_REAL_IP_ADDRESS: 172.18.0.0/16
UPSTREAM_REAL_IP_HEADER: X-Forwarded-For
UPSTREAM_REAL_IP_RECURSIVE: "on"
```

The host Nginx must also forward the header:

```nginx
proxy_set_header X-Real-IP $remote_addr;
proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
```

Never trust `0.0.0.0/0`, because clients could then forge their address.

## Security checklist

- Use a named user for each person instead of sharing the Administrator account
- Enable two-factor authentication in System Settings
- Do not publish the database port to the internet
- Keep secrets in `.env`, and keep `.env` out of git
- Back up before every upgrade: `bench --site <site> backup --with-files`
