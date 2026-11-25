# Unity Platform

Unity is an enterprise platform built on the Frappe Framework. It runs as a set of Docker containers on an Azure Virtual Machine, behind Nginx, from one custom image that already contains all the applications.

## What is included

| App | Purpose |
|---|---|
| ERPNext | Accounting, sales, purchasing, inventory |
| HRMS | Employees, leave, attendance, payroll |
| Helpdesk | Tickets and support |
| Insights | Dashboards and analytics |
| Telephony | Call integration |
| Payments | Payment gateways |
| LMS | Learning and courses |
| Builder | Web pages with Frappe Builder |
| Wiki | Documentation spaces |
| ODA Marketing | In-house marketing app |

## How this documentation is organised

- **Getting Started**: run Unity on your machine in a few commands.
- **Guides**: install, then configure the platform.
- **Reference**: the services, commands and apps in the stack.
- **Tutorial**: build your first custom app.

## Design principle

Customer requirements are met with configuration first: Custom Fields, Workflows, Notifications, Scripts and Workspaces. Core framework and baked-in apps are never edited, so the platform stays easy to upgrade.
