---
name: Create a PlanRadar ticket with a document
description: Authenticate, find the project, create a ticket, and attach a document in PlanRadar's Open API v2.
api: openapi/planradar-openapi-original.json
operations:
  - "GET /api/v2/{customer_id}/projects/my_projects"
  - "POST /api/v2/{customer_id}/projects/{project_id}/tickets"
  - "POST /api/v1/{customer_id}/projects/{project_id}/documents/"
---

# Create a PlanRadar ticket with a document

Use this skill to open a defect/task ticket in a PlanRadar project and attach supporting documentation.

## Auth
- Header: `X-PlanRadar-API-Key: <personal access token>` on every request (see `authentication/planradar-authentication.yml`).
- Requires a Pro/Enterprise account and a user with the **API Access** permission.
- Stay under **30 requests/minute/account** — breaching disables the token for 5 minutes (see `conventions/planradar-conventions.yml`).
- Send `Accept: application/json` (a missing/other Accept yields `406`).

## Steps
1. **List projects** — `GET /api/v2/{customer_id}/projects/my_projects`. Pick the target `project_id`.
2. **Create the ticket** — `POST /api/v2/{customer_id}/projects/{project_id}/tickets` with a JSON body carrying `ticket-type-id`, `subject`, `status-id`, `priority-id`, and optional `assigned-to-id` / `due-date`. Capture the returned ticket `uuid`.
3. **Attach a document** — `POST /api/v1/{customer_id}/projects/{project_id}/documents/` with `ticket-id`, `title`, `filename`, and the file (`document`, optionally base64 with `is-base64: true`); large uploads may run with `async: true`.

## Errors
Handle `401` (bad/rotated token), `403` (missing permission), `404` (wrong customer/project id), `422` (validation). See `errors/planradar-problem-types.yml`.
