---
name: Export PlanRadar project tickets to Excel or PDF
description: Kick off an asynchronous ticket export and retrieve the finished file via its direct URL.
api: openapi/planradar-openapi-original.json
operations:
  - "POST /api/v1/{customer_id}/projects/{project_id}/tickets/export/xls"
  - "GET /api/v1/{customer_id}/projects/{project_id}/tickets/export/pdf"
---

# Export PlanRadar project tickets to Excel or PDF

Use this skill to generate a report of a project's tickets as an Excel or PDF file.

## Auth
- Header `X-PlanRadar-API-Key`; `Accept: application/json`; 30 req/min/account limit.

## Steps
1. **Request the export** — `POST /api/v1/{customer_id}/projects/{project_id}/tickets/export/xls` (or `.../export/pdf`) with a JSON body of filters selecting the tickets. Pass `async: true` for large exports.
2. **Poll status** — for async exports, poll the export status endpoint until the job completes; request the `direct_url` parameter to receive a direct download link when ready (see `changelog/planradar-changelog.yml`, CW23 2026).
3. **Download** — fetch the returned `direct_url`.

## Errors
`404` unknown project, `422` invalid filter/body, `429` rate limit. See `errors/planradar-problem-types.yml`.
