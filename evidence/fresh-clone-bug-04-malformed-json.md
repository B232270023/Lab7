Fresh-clone replay on 2026-10-15 using the tester's Opera One session.

- GET /api/books before the malformed POST returned HTTP 200 and the current JSON array.
- POST /api/books with Content-Type: application/json and body `not-json` returned HTTP 200 with `{"result":"OK"}`.
- GET /api/books after the POST returned the unchanged array; no record was created.

See ../screenshots/replay/bug-04-malformed-json-api.png for the complete terminal capture.
