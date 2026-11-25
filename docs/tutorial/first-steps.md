# First steps: build an app

Create a custom Frappe app, install it on a site, and add your first DocType.

## 1. Create the app

Run inside a bench, in a development environment:

```bash
bench new-app my_app
```

The command asks for a title, description, publisher, email and license, then creates `apps/my_app`.

## 2. Install it on a site

```bash
bench --site <site> install-app my_app
bench --site <site> list-apps
```

## 3. Turn on developer mode

```bash
bench --site <site> set-config developer_mode 1
bench --site <site> clear-cache
```

## 4. Add a DocType

1. Open **DocType List** and click **Add**.
2. Choose your app's module.
3. Add fields, then save.

Frappe creates the files in your app folder, next to the schema JSON. Commit them to git.

## 5. Add settings and a workflow

Most of an app can be built from the UI:

- **Settings**: a Single DocType
- **Approvals**: a Workflow
- **Alerts**: a Notification
- **Navigation**: a Workspace

## 6. Ship it

1. Commit and push the app.
2. Add its entry to `apps.json` after the apps it depends on.
3. Rebuild the image and install the app on the site.

Pin a tag or commit instead of a moving branch for release images.
