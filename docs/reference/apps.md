# Apps

Applications baked into the Unity image.

| App | Source | Notes |
|---|---|---|
| frappe | frappe/frappe | The framework |
| erpnext | frappe/erpnext | Required by ODA Marketing |
| hrms | frappe/hrms | HR and payroll |
| helpdesk | frappe/helpdesk | Support tickets |
| insights | frappe/insights | Analytics |
| telephony | frappe/telephony | Call integration |
| payments | frappe/payments | Payment gateways |
| lms | frappe/lms | Learning |
| builder | frappe/builder | Pages |
| wiki | frappe/wiki | Documentation |
| oda_marketing | ODA repository | In-house app |

## Where the versions are fixed

Versions come from the branch or tag of each entry in `apps.json` at build time. Run `bench version` inside the image to see exactly what a build contains.

## Adding an app to the image

1. Add its entry to `apps.json`. Put apps that others depend on first.
2. Rebuild the image.
3. Install the app on each existing site with `bench --site <site> install-app <app>`.
