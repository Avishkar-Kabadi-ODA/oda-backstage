**Short answer:** Yes, partly. Frappe has no "create app" button, but you can build most of what `oda_marketing` does in the UI, and a feature called Packages lets you bundle it. A full app with its own Python code still needs the CLI.

**Layer:** UI configuration, with one `bench` command if you want a real app.

**What the docs say:**

- **Packages:** Packages are light apps built from the Framework UI, and since v14 you can make apps without the command line using DocTypes, Server Scripts and Web Pages. A Package is a set of Custom Module Defs, and a Package Release exports them as a `.tar.gz` that another site can import with Package Import. The page was last updated in February 2026, so it is still documented for v16.
- **Real apps:** A normal app is created with `bench new-app` and generates the Python package with `hooks.py` and `modules.txt`. That is the CLI route you were asking about.
- **Developer mode:** In developer mode, a DocType created in Desk gets its folder and files scaffolded in the app, and edits are written back to its `.json` file so you can commit them.

I didn't find a "New App" button for Desk in the v16 docs.

**What you can do in the UI, with no code:**

| `oda_marketing` piece | UI feature |
|---|---|
| Settings | Single DocType |
| Flow / approvals | Workflow |
| Master and transaction records | Custom DocTypes |
| Options and fields on existing doctypes | Custom Fields, Property Setters, Customize Form |
| Emails and alerts | Notification |
| Light logic | Client and Server Scripts |
| Navigation | Workspace |
| Public pages and forms | Web Form, Frappe Builder |

**What needs the CLI and code:** a custom Python controller, `hooks.py` entries (`doc_events` and `scheduler_events` are partly covered by Server Scripts), shared Python modules, and heavier custom pages. Server Scripts run in a restricted sandbox, so complex logic hits limits.

**Steps (Package route):**

1. `Home → Package`, create one.
2. `Home → Module Def`, create a module, tick **Custom**, and set its **Package**.
3. Build DocTypes (tick **Custom**), Workflows and Scripts under that module.
4. Create a **Package Release** to export the `.tar.gz`, then use **Package Import** with **Activate** ticked on the target site.

**Risks:**

- **Not everything may be exported.** The docs only list DocTypes, Server Scripts and Web Pages, so test whether Workflow, Notification and Workspace travel with the package.
- **Storage:** package files live in `sites/<site>/packages` inside the `sites` volume. They survive image rebuilds but are not in git or in the image, so a new site needs the import.
- **No upgrade path:** a Package has no version control or patches, unlike a git repo.
- **Developer mode in your Docker image:** with an app that is baked into the image, files written by developer mode are lost on `--force-recreate`. Develop in a bind-mounted bench, then commit.

**Recommendation:** Keep `oda_marketing` as a real app in git, since it is already your delivery unit. Create new apps once with `bench new-app` (it takes a minute), build the flows, settings and DocTypes in the UI with developer mode on, commit what Frappe writes out, and rebuild the image. That keeps it upgrade-safe, versioned and reproducible. Use Packages only for something small and portable that doesn't justify a repo.

**Upgrade Safe:** ✅ Yes for the UI features. Packages are ✅ with the caveats above.
