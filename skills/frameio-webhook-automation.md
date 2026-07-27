---
name: Automate workflows with webhooks
description: Register a webhook on a workspace to receive Frame.io events, and verify it.
api: openapi/frameio-v4-openapi.json
operations: [webhooks.create, webhooks.index, webhooks.show]
---

# Automate workflows with webhooks

Base URL: `https://api.frame.io`. Adobe IMS OAuth2 bearer token required.

1. **Register the webhook** — `POST /v4/accounts/{account_id}/workspaces/{workspace_id}/webhooks`
   (`webhooks.create`) with your subscriber `url` and the `events` to subscribe to (e.g.
   `file.ready`, `comment.created`, `share.viewed` — full list in `asyncapi/frameio-webhooks.yml`).
2. **List existing webhooks** — `GET /v4/accounts/{account_id}/workspaces/{workspace_id}/webhooks`
   (`webhooks.index`) to avoid duplicates.
3. **Inspect one** — `GET /v4/accounts/{account_id}/webhooks/{webhook_id}` (`webhooks.show`).
4. **Handle deliveries** at your subscriber endpoint; respond 2xx quickly and process
   asynchronously.

Errors follow the JSON:API-style envelope; honor `x-ratelimit-*` on 429. For synchronous
interactive automations consider Custom Actions (`actions.create`) instead of webhooks.
