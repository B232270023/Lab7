# SBTM exploratory session report

- Tester name: pending confirmation
- Student code: B232270023 (repository account)
- Application: Reading List v2.0, http://localhost:3000/
- Runtime: Node.js v24.14.1
- Browser: pending tester-provided name/version; browser's internal version page was blocked by the browser safety boundary
- Charter: committed to the public repository before this session (`77fdb01`, 2026-10-15 14:55:41 +08:00)
- Session start: 2026-10-15 15:07:23 Asia/Ulaanbaatar (UTC+08:00)
- Planned session duration: 60 minutes, through 16:07:23 +08:00
- Session style: black-box, UI-first, with no inspection of `app.js`

## Chronological notes

- 15:07:23 +08:00 — Began the timed session after the charter commit. Opened the app in the Codex in-app browser. The page displayed three rows (Тунгалаг Тамир; Clean Code; The Pragmatic Programmer) while the summary read “Нийт ном: 4 · Хамгийн шинэ он: 2008”. This is a candidate count mismatch; verify through the “Бүгд” control and additional add/delete paths.
- 15:07:23 +08:00 — Removed the blank row left by pre-session reconnaissance, returning the UI to three visible rows. The page still displayed the prior “Ном нэмэгдлээ” status text immediately after removal; determine whether this is stale status or an issue by observing a new delete.
- 15:07:23 +08:00 — Attempted `curl -i http://127.0.0.1:3000/` from the workspace shell. It could not connect, although the same localhost app was reachable through the Codex in-app browser. Record as an environment obstacle; continue UI exploration and revisit API evidence via an available route.
- 15:07:23 +08:00 — Clicked “Бүгд”; the accessibility tree reported no change. The status remained 4 while three rows were visible. This strengthens the candidate but does not yet establish the intended count contract.

## Time accounting

Session end and per-tour time breakdown will be completed after the 60-minute session.
- 15:08 +08:00 — Added a valid test book (“SBTM Test - 2026”, “QA Session”, 2026). It appeared as a fourth table row, but the summary increased from 4 to 5; the year rendered as “2,026”. This confirmed the displayed total is one higher than the rendered row count and provided a candidate year-formatting issue.
- 15:08 +08:00 — Deleted the valid test book. The row disappeared and the summary returned to 4 / 2008. The visible success text still read “Ном нэмэгдлээ” after the delete, so deletion gave no fresh, accurate status feedback.
- 15:08 +08:00 — Submitted the add form with title, author, and year all empty. The app accepted the submission, showed “Ном нэмэгдлээ”, created a blank table row with year 0, and raised the summary to 5. Captured a browser screenshot for evidence; file export into the repository is still unresolved.
- 15:09 +08:00 — Searched for lowercase “clean”; no rows matched. Searching exact “Clean Code” returned one row, and partial author “Robert” returned Clean Code. “Бүгд” restored all four rendered rows, while the summary remained 5. Case sensitivity was observed but is not yet counted as a defect because the specification does not state case-insensitive search.

- 15:10:48 +08:00 — Ran curl -i against the app root to check shell connectivity. The response was 200 HTML and included inline client-script text; this was an unintended source exposure during environment setup. No app.js file was opened. Further findings were verified through rendered UI and JSON API responses, without continuing source-based investigation.
- 15:11:06 +08:00 — Compared JSON endpoints while the blank test record existed: /api/stats returned total: 5, while /api/books returned four objects. This matched four rendered rows and further established a one-item stats/list mismatch.
- 15:11:36 +08:00 — Removed the blank test record, returning the app to its original three visible books. The API then returned total: 4 versus three objects in /api/books; saved the complete curl -i response headers and bodies in evidence/bug-01-stats-curl.txt.
- 15:12 +08:00 — Added a record with year not-a-year; the app accepted it and displayed NaN. Reloading preserved the invalid record. Deleted the test record afterward; the default three visible books remain.
- 15:12 +08:00 — The visible “Хуучин хувилбар” link opened an about:blank tab. Direct navigation to the linked /old page was blocked by the browser; no alternate route was attempted.
- 15:13 +08:00 — Captured blank-row and NaN screenshots in the CUA browser output. The browser safety policy blocked the data-URL export needed to save image files to the repository. Requested the user's browser metadata; the user said the version is unknown. README now records “Codex In-app Browser; version unavailable.”

- 15:15:10 +08:00 — Saboteur tour: sent malformed JSON to POST /api/books with Content-Type application/json. The server returned HTTP 200 OK with {"result":"OK"}, but the book list remained unchanged on follow-up GET. Saved the full response in evidence/bug-04-malformed-json-curl.txt; filed the misleading success response as a separate API defect.
- 15:15 +08:00 — Session state remains the original three visible books; test-created valid, blank, and invalid-year records were removed. The “Ном нэмэгдлээ” status text remains after deletes.
