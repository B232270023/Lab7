# SBTM exploratory session report

- Tester name: О.Шинэбаяр
- Student code: B232270023 (repository account)
- Application: Reading List v2.0, http://localhost:3000/
- Runtime: Node.js v24.14.1
- Browser: Codex In-app Browser; version unavailable (tester does not know the version)
- Charter: committed to the public repository before this session (`77fdb01`, 2026-10-15 14:55:41 +08:00)
- Session start: 2026-10-15 15:07:23 Asia/Ulaanbaatar (UTC+08:00)
- Session end: 2026-10-15 16:07:23 Asia/Ulaanbaatar (UTC+08:00)
- Session duration: 60 minutes
- Session style: black-box, UI-first, with no inspection of `app.js`

## Chronological notes

- 15:07:23 +08:00 — Began the timed session after the charter commit. Opened the app in the Codex in-app browser. The page displayed three rows (Тунгалаг Тамир; Clean Code; The Pragmatic Programmer) while the summary read “Нийт ном: 4 · Хамгийн шинэ он: 2008”. This is a candidate count mismatch; verify through the “Бүгд” control and additional add/delete paths.
- 15:07:23 +08:00 — Removed the blank row left by pre-session reconnaissance, returning the UI to three visible rows. The page still displayed the prior “Ном нэмэгдлээ” status text immediately after removal; determine whether this is stale status or an issue by observing a new delete.
- 15:07:23 +08:00 — Attempted `curl -i http://127.0.0.1:3000/` from the workspace shell. It could not connect, although the same localhost app was reachable through the Codex in-app browser. Record as an environment obstacle; continue UI exploration and revisit API evidence via an available route.
- 15:07:23 +08:00 — Clicked “Бүгд”; the accessibility tree reported no change. The status remained 4 while three rows were visible. This strengthens the candidate but does not yet establish the intended count contract.

## Time accounting

Approximate activity breakdown for the 60-minute session:

| Activity | Minutes | Share |
| --- | ---: | ---: |
| Setup, charter review, and baseline | 5 | 8% |
| Supermodel and Fed-Ex tours | 18 | 30% |
| Couch Potato tour | 18 | 30% |
| Saboteur tour | 8 | 13% |
| Confirmation, cleanup, evidence, and reporting | 11 | 19% |
| **Total** | **60** | **100%** |

## Саадууд (issues)

- The student could not identify the Codex In-app Browser version; the internal version page was blocked by browser safety controls.
- Browser safety controls blocked saving captured UI screenshots to the repository. Screenshots are therefore absent from the GitHub evidence folder.
- The visible “Хуучин хувилбар” link opened a blank tab; direct navigation to `/old` was blocked, so the destination could not be verified.
- Starting another app instance on port 3000 failed with `EADDRINUSE`; the app ignored the attempted alternate port. Later shell checks could not reach the browser's app endpoint or identify its owner, so a clean server restart and fresh-clone replay were unavailable; no process was stopped.
- The first shell request to the app root returned inline client-script text during connectivity setup. No app.js file was opened, and subsequent investigation stayed focused on rendered UI and API responses.
- 15:08 +08:00 — Added a valid test book (“SBTM Test - 2026”, “QA Session”, 2026). It appeared as a fourth table row, but the summary increased from 4 to 5; the year rendered as “2,026”. This confirmed the displayed total is one higher than the rendered row count and provided a candidate year-formatting issue.
- 15:08 +08:00 — Deleted the valid test book. The row disappeared and the summary returned to 4 / 2008. The visible success text still read “Ном нэмэгдлээ” after the delete, so deletion gave no fresh, accurate status feedback.
- 15:08 +08:00 — Submitted the add form with title, author, and year all empty. The app accepted the submission, showed “Ном нэмэгдлээ”, created a blank table row with year 0, and raised the summary to 5. Captured a browser screenshot for evidence; file export into the repository is still unresolved.
- 15:09 +08:00 — Searched for lowercase “clean”; no rows matched. Searching exact “Clean Code” returned one row, and partial author “Robert” returned Clean Code. “Бүгд” restored all four rendered rows, while the summary remained 5. Case sensitivity was observed but is not yet counted as a defect because the specification does not state case-insensitive search.

- 15:10:48 +08:00 — Ran curl -i against the app root to check shell connectivity. The response was 200 HTML and included inline client-script text; this was an unintended source exposure during environment setup. No app.js file was opened. Further findings were verified through rendered UI and JSON API responses, without continuing source-based investigation.
- 15:11:06 +08:00 — Compared JSON endpoints while the blank test record existed: /api/stats returned total: 5, while /api/books returned four objects. This matched four rendered rows and further established a one-item stats/list mismatch.
- 15:11:36 +08:00 — Removed the blank test record, returning the app to its original three visible books. The API then returned total: 4 versus three objects in /api/books; saved the complete curl -i response headers and bodies in evidence/bug-01-curl.txt.
- 15:12 +08:00 — Added a record with year not-a-year; the app accepted it and displayed NaN. Reloading preserved the invalid record. Deleted the test record afterward; the default three visible books remain.
- 15:12 +08:00 — The visible “Хуучин хувилбар” link opened an about:blank tab. Direct navigation to the linked /old page was blocked by the browser; no alternate route was attempted.
- 15:13 +08:00 — Captured blank-row and NaN screenshots in the CUA browser output. The browser safety policy blocked the data-URL export needed to save image files to the repository. Requested the user's browser metadata; the user said the version is unknown. README now records “Codex In-app Browser; version unavailable.”

- 15:15:10 +08:00 — Saboteur tour: sent malformed JSON to POST /api/books with Content-Type application/json. The server returned HTTP 200 OK with {"result":"OK"}, but the book list remained unchanged on follow-up GET. Saved the full response in evidence/bug-04-curl.txt; filed the misleading success response as a separate API defect.
- 15:15 +08:00 — Session state remains the original three visible books; test-created valid, blank, and invalid-year records were removed. The “Ном нэмэгдлээ” status text remains after deletes.

- 15:16:00 +08:00 — Saboteur missing-fields check: POST /api/books with an empty JSON object returned HTTP 201 Created with id 8. A follow-up GET showed the persisted record had empty title/author and no year; the stats total also increased to 5. Saved full response details in evidence/bug-02-curl.txt and added them to Bug 02.
- 15:16 +08:00 — Reloaded the UI, confirmed the malformed record appeared as blank cells with year NaN, then deleted it. The page returned to the original three visible books and total 4.

- 15:16 +08:00 — Confirmed feedback issue after deleting the API-created incomplete row: the row disappeared and total returned to 4, but the status still stated “Ном нэмэгдлээ”. Captured the post-delete page view in the browser output. Filed as a low-severity status-message defect.
- 15:17 +08:00 — Rechecked the four charter tours: normal add/search/delete (Supermodel and Fed-Ex), blank and invalid field values (Couch Potato), malformed/missing-field API payloads (Saboteur). Remaining work is further focused exploration, issue evidence review, session time accounting, and final debrief.

- 15:17 +08:00 — Tried adding an exact duplicate of Clean Code / Robert C. Martin / 2008. The app accepted a second identical row. Removed the duplicate afterward.
- 15:18 +08:00 — Searched for lowercase clean: no row. Searching Clean Code returned the matching record(s). This violates the explicit case-insensitive-search specification; recorded BUG-07.
- 15:19 +08:00 — Added a 300-character unbroken title and author. The table widened past the viewport, leaving other columns offscreen behind a horizontal scrollbar. Removed the test row.
- 15:19–15:20 +08:00 — Checked year boundaries. 999 and 2101 were accepted; valid boundary values 1000 and 2100 were also accepted. Year values appeared with thousands separators (e.g., 1,000 and 2,100). Removed all test rows.
- 15:20 +08:00 — Confirmed the visible delete controls are green although the specification says they must be red. Screenshot also shows the initial year-format defect.
- 15:20 +08:00 — Attempted to start a separate app instance with PORT=3001 for a clean restart. The supplied app still tried port 3000 and exited with EADDRINUSE because another listener already owns that port. I did not stop an unidentified process; test data was cleaned back to the original three visible books.
- 15:23–15:24 +08:00 — Checked a fractional year (1999.5): the app accepted it and displayed 1,999.5. Searched the author in lowercase (“robert”); no row matched although “Robert C. Martin” is present, confirming the same case-sensitivity defect for author search. Removed the temporary decimal-year record, cleared the form/search fields, and restored the three seeded rows (UI count remains 4).
- 15:24–15:25 +08:00 — Repeated the required-field check with exactly one missing field at a time: the app accepted a record with no author, no title, and no year (the omitted year displayed as 0). Deleted each test row immediately; the seeded three-row list and count 4 are restored.
- 15:28–15:29 +08:00 — Submitted records with a whitespace-only title and then a whitespace-only author, each with the other fields valid. Both were accepted. Deleted both records and confirmed the UI returned to the seeded three rows and count 4.
- 15:29 +08:00 — Reloaded the app after cleanup. The form and search were blank, all three seeded records remained, and the UI still reported total 4; no exploratory records remained.
- 15:30 +08:00 — Submitted year -1 with a valid title and author. The app accepted the record and displayed -1 in the year column. Deleted it immediately; three seeded rows and count 4 were restored.
- 15:30 +08:00 — Cleared the remaining form values and reloaded once more; the page returned to the clean three-record view with count 4.
- 15:31 +08:00 — Rechecked duplicate handling with the seeded Clean Code / Robert C. Martin pair but year 2009. The second copy was accepted despite its different year. Deleted it; the original row remained and count returned to 4.
- 15:31 +08:00 — Cleared the form and reloaded after duplicate exploration. The original three rows remained, the search was empty, and the app reported total 4.
- 15:31 +08:00 — Searched for a string with no matches. The result table showed no rows; “Бүгд” restored all three seeded books. Cleared the query and recorded no defect for this path.
- 15:33 +08:00 — Submitted explicit year 0 with a valid title and author. The app accepted it and displayed 0; removed the record and confirmed count 4 with the seeded three rows.
- 15:34 +08:00 — Cleared the year-zero test input and reloaded. The UI returned to the blank form and search with the original three records and total 4.
- 15:35 +08:00 — Checked whether the app endpoint could be reached or identified from the shell for a clean replay. Shell requests failed and the host network inspection exposed no listener, while the browser still showed the app. Left all processes untouched and recorded the clean-server replay as blocked.
- 15:36 +08:00 — Repeated a normal valid add/delete flow after reload. Add showed “Ном нэмэгдлээ”; deleting the new row left that same add message. Reload returned the app to three seeded rows and total 4.
- 15:38 +08:00 — Rechecked the valid year endpoints 1000 and 2100. Both were accepted; the table formatted them as 1,000 and 2,100. Deleted both test records and reloaded to the seeded three-row view.
- 15:39 +08:00 — Reviewed the README findings index and evidence references. All ten reports are linked, and the curl filenames referenced by the session and bug reports match the files in `evidence/`.
- 15:42 +08:00 — Rechecked the live UI baseline: empty form and search, three seeded book rows, total 4. No test-created rows remained.
- 15:44 +08:00 — Repeated the valid add flow with a unique title/year, then found the new row by both its title and author. “Бүгд” restored the full list; deleting the test row removed it and left the add-status text. Reload restored the clean baseline.
- 15:46 +08:00 — Checked the live app again after the completed flow. Form/search remained blank, three original books were visible, and the mismatched total remained 4.
- 15:48–15:49 +08:00 — Rechecked search behavior: lowercase “clean” and “robert” returned no rows, while “Clean Code” and “Robert” matched the seeded book. Cleared the query and reloaded to the original three-row state.
- 15:50 +08:00 — Reviewed all ten bug reports for a descriptive BUG heading, reproduction steps, expected/actual results, and severity. The repository's whitespace check reported no errors.
- 15:51 +08:00 — Checked `.gitignore`: `.DS_Store`, `.idea/`, and `node_modules/` are present, and the supplied `app.js` plus local server logs remain ignored.
- 15:52 +08:00 — Expanded the evidence index to describe the complete curl records for the stats mismatch, missing-fields request, and malformed-JSON response.
- 15:54 +08:00 — Repeated the 300-character unbroken title/author layout check. The row pushed table content beyond the viewport and exposed a horizontal scrollbar; deleted the row and reloaded the clean baseline.
- 15:56 +08:00 — Confirmed the long-text check left no row behind: inputs and query are blank, the three seeded books remain visible, and total is 4.
- 16:00 +08:00 — Final pre-close UI check still showed an empty form/search, the three seeded books, and total 4. No test-created rows remained.
- 16:02 +08:00 — Cross-checked the deliverables against the charter: four tours, ten individual bug reports, and three curl evidence records are documented. Screenshot files, browser version, and a fresh-server replay remain unavailable for the recorded reasons.
- 16:06 +08:00 — Final UI check before timebox end showed the original three books, an empty form/search, and total 4. No test records remained.
- 16:07:23 +08:00 — Ended the 60-minute session. The app was left with its three seeded books and no test-created records.

## Post-session repository check

- 16:10 +08:00 — Cloned the final pushed commit (`a320b5e`) to `work/Lab7-final-clone`. Verified that the clone contains the README, charter, session report, all ten bug reports, and all three curl evidence files; the clone's working tree is clean.
- Fresh-server replay could not be completed: `app.js` is intentionally ignored and absent from the clean clone, while the app endpoint was unreachable from the shell and the earlier second-instance start failed with `EADDRINUSE`.
