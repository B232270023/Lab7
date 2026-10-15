# Bug 04 — Malformed JSON receives a success response

- Severity: Medium (P2)
- Area: API error handling

## Expected

A malformed JSON body should be rejected with a client error (for example, HTTP 400) and an error response.

## Actual

POST /api/books with the body not-json returned HTTP 200 OK and {"result":"OK"}. Follow-up GET requests showed that the books list and stats had not changed, so the response reported success for a request the server did not apply.

## Reproduction

1. Send Content-Type: application/json to POST /api/books.
2. Use the malformed body not-json.
3. Observe the HTTP 200 response and check that GET /api/books remains unchanged.

## Evidence

The complete curl -i response is in [bug-04-malformed-json-curl.txt](../evidence/bug-04-malformed-json-curl.txt).
