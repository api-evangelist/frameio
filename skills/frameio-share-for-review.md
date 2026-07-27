---
name: Share assets with external reviewers
description: Create a share in a project, add assets to it, and invite reviewers.
api: openapi/frameio-v4-openapi.json
operations: [shares.create, shares.add_asset, shares.add_reviewers, shares.show]
---

# Share assets with external reviewers

Base URL: `https://api.frame.io`. Adobe IMS OAuth2 bearer token required.

1. **Create the share** — `POST /v4/accounts/{account_id}/projects/{project_id}/shares`
   (`shares.create`) with a name and settings.
2. **Add assets** — `POST /v4/accounts/{account_id}/shares/{share_id}/assets`
   (`shares.add_asset`) for each file/folder to include.
3. **Invite reviewers** — `POST /v4/accounts/{account_id}/shares/{share_id}/reviewers`
   (`shares.add_reviewers`) with reviewer emails.
4. **Confirm** — `GET /v4/accounts/{account_id}/shares/{share_id}` (`shares.show`) to read the
   public review URL and reviewer list.

Conventions and error handling as in `conventions/frameio-conventions.yml`. To revoke access
later, use `shares.remove_reviewers` / `shares.remove_asset`.
