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
