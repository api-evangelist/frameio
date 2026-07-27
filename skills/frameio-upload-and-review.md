---
name: Upload media and collect review comments
description: Upload a file into a Frame.io folder, wait until it is ready, and read the review comments left on it.
api: openapi/frameio-v4-openapi.json
operations: [files.create_local_upload, files.show_file_upload_status, files.show, comments.index]
---

# Upload media and collect review comments

Base URL: `https://api.frame.io`. Authenticate with an Adobe IMS OAuth2 bearer token
(`Authorization: Bearer <token>`). See `authentication/frameio-authentication.yml`.

1. **Create the upload** — `POST /v4/accounts/{account_id}/folders/{folder_id}/files/local_upload`
   (`files.create_local_upload`) with the file name and size. The response returns the new
   file id and pre-signed upload URL(s).
2. **Upload the bytes** to the returned URL(s), then poll
   `GET /v4/accounts/{account_id}/files/{file_id}/status` (`files.show_file_upload_status`)
   until processing is complete.
3. **Confirm the asset** — `GET /v4/accounts/{account_id}/files/{file_id}` (`files.show`).
4. **Read review feedback** — `GET /v4/accounts/{account_id}/files/{file_id}/comments`
   (`comments.index`), paginating with `after` / `page_size`.

Conventions: cursor pagination (`after`, `page_size`), errors as `{errors:[{title,detail,source.pointer}]}`
(see `errors/frameio-problem-types.yml`). Honor `x-ratelimit-*` headers on 429. Writes are not
idempotent — do not blindly retry `create_local_upload`.
