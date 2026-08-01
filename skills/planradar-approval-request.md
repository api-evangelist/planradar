---
name: Raise a PlanRadar document approval request
description: Create and track an approval request for documents or plans in a PlanRadar project.
api: openapi/planradar-openapi-original.json
operations:
  - "POST /api/v2/{customer_id}/projects/{project_id}/approval_requests"
  - "GET /api/v2/{customer_id}/projects/{project_id}/approval_requests"
  - "GET /api/v2/{customer_id}/projects/{project_id}/approval_requests/{id}"
---

# Raise a PlanRadar document approval request

Use this skill to route a document/plan version through an approval workflow.

## Auth
- Header `X-PlanRadar-API-Key`; `Accept: application/json`; 30 req/min/account limit.

## Steps
1. **Create the request** — `POST /api/v2/{customer_id}/projects/{project_id}/approval_requests` with the target version(s) and reviewers/workflow. Capture the returned request `id`.
2. **List open requests** — `GET /api/v2/{customer_id}/projects/{project_id}/approval_requests` to see pending approvals.
3. **Track one** — `GET /api/v2/{customer_id}/projects/{project_id}/approval_requests/{id}` to poll status until approved/rejected.

## Errors
`403` missing permission, `404` unknown project/request, `422` invalid version. See `errors/planradar-problem-types.yml`.
