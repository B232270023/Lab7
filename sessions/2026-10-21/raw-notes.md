# Session 03 raw notes

Executor: Codex, AI-assisted testing requested by О.Шинэбаяр (B232270023).
Start: 2026-10-21 14:59:08 +08:00
Planned end: 2026-10-21 15:59:08 +08:00
Charter: 9569ae40586c1aea179317c1ca388804d5c40b8a, committed and pushed before this start.
Environment: Reading List v2.0; Node.js v24.13.0; Windows x64; Codex In-app Browser observed User-Agent Chrome/155.0.0.0.
Method: black-box UI and curl; no app.js source inspection. This file is appended during the timebox. Reports are written afterward. Timestamps use UTC+08:00.

- 14:59:08 — Setup phase begins. The app was restarted during preparation and GET /api/books verified the original three seeded objects. Browser User-Agent was rendered by a separate localhost diagnostic endpoint. The interrupted session 02 is not included in this timebox.

- 14:59:32 — Setup baseline screenshot saved. Three seeded UI rows, total 4, years with thousands separators, green delete buttons. BUG-01/08/09 are visible independently of test-created data. Browser-version screenshot also saved.

- 15:00:01 — Setup: full curl -i baseline is saved in evidence/session-03/bug-01-curl.txt; three objects versus total=4. Compared screenshot with the API to distinguish a render issue from a count-response issue. Test design and execution phase begins now.

- 15:00:35 — Fed-Ex: S03 Valid Flow / Session Tester / 2026 accepted from the fresh baseline. Four rows, total 5, newest 2026; saved valid-add.jpg. The off-by-one count survives an add (BUG-01).

- 15:00:56 — BUG-05: reloaded after add (status became empty), then deleted only S03 Valid Flow. Three original books remain; status newly shows Ном нэмэгдлээ. Saved bug-05.jpg. This proves incorrect delete feedback independently of an old add message. Leaving this tab untouched temporarily to observe whether delayed feedback corrects it; further tests use another tab.

- 15:01:13 — Fresh server reset before missing-field tests; original three records confirmed. The previous tab's status observation is a client-side observation only and will not be used as proof of server persistence.

- 15:08:27 — Couch Potato: on a fresh three-book server, all-empty submission created a fourth row with empty title/author and year 0; total 5; success message. Saved bug-02.jpg immediately. Check reload and server record to exclude a transient client-only row.

- 15:08:50 — GUI empty submission persisted after reload; API recorded title/author empty and year 0. Separately restarted, confirmed three records, then POST {} via curl.exe: HTTP 201, id 4, empty title/author with year absent. Saved complete request responses and both variants. Same missing-required-fields bug, not separate findings.

- 15:09:03 — Clarification of the preceding persistence note: the GUI-created record stores year as the empty string "", while the UI converts it to display 0. The {} API variant omits year entirely. Do not claim that the GUI stored numeric zero.

- 15:09:20 — Restarted to isolate a single missing-author input. The API-created absent year had rendered NaN after reload, a display difference from the all-empty GUI submission's 0.

- 15:09:37 — Missing-author variant from a new server: S03 Missing Author / empty author / 2026 was accepted. Fourth row has a blank author. Saved missing-author.jpg (BUG-02).

- 15:10:05 — Fresh-server missing-title variant accepted: empty title / S03 Missing Title Author / 2026. Saved missing-title.jpg. The empty title and empty author observations belong in the same required-fields report.

- 15:10:38 — Missing-year variant from a fresh process accepted S03 Missing Year / Session Tester / empty year; UI displays 0 and newest stays 2008. Saved missing-year.jpg.

- 15:11:07 — Fresh-server whitespace-title variant accepted exactly one U+0020 character as title with S03 Space Title Author / 2026. Saved whitespace-title.jpg. Treat whitespace-only mandatory names as empty under the usable-name expectation; this is grouped with BUG-02.

- 15:11:36 — Fresh-server whitespace-author variant accepted S03 Space Author / one U+0020 / 2026. Saved whitespace-author.jpg. Required-field exploration covers all empty, title-only omission, author-only omission, year-only omission, and whitespace-only title/author.

- 15:11:54 — Fresh reset before year-boundary exploration. Starting one bounded incomplete POST with low-rate GET controls to investigate the Saboteur availability question; UI exploration continues on the same server, without assuming a timeout requirement from the oracle.

- 15:12:24 — BUG-03 primary replay: new server with three seeds, added S03 Year 2101 / Session Tester / 2101; accepted as fourth row, year 2,101, newest 2101, total 5. Saved bug-03.jpg. The incomplete HTTP client did not block the operation.

- 15:12:54 — Year variation "999": matching added rows=1; visible row="S03 Year 999\tSession Tester\t999\tУстгах". Saved year-999.jpg. This series starts with three seeds and removes each test row before the next variation; no server restart between variations.

- 15:12:55 — Year variation "0": matching added rows=1; visible row="S03 Year 0\tSession Tester\t0\tУстгах". Saved year-zero.jpg. This series starts with three seeds and removes each test row before the next variation; no server restart between variations.

- 15:12:55 — Year variation "-1": matching added rows=1; visible row="S03 Year -1\tSession Tester\t-1\tУстгах". Saved year-negative.jpg. This series starts with three seeds and removes each test row before the next variation; no server restart between variations.

- 15:12:56 — Year variation "1999.5": matching added rows=1; visible row="S03 Year 1999.5\tSession Tester\t1,999.5\tУстгах". Saved year-decimal.jpg. This series starts with three seeds and removes each test row before the next variation; no server restart between variations.

- 15:12:57 — Year variation "1000": matching added rows=1; visible row="S03 Year 1000\tSession Tester\t1,000\tУстгах". Saved year-valid-1000.jpg. This series starts with three seeds and removes each test row before the next variation; no server restart between variations.

- 15:12:58 — Year variation "2100": matching added rows=1; visible row="S03 Year 2100\tSession Tester\t2,100\tУстгах". Saved year-valid-2100.jpg. This series starts with three seeds and removes each test row before the next variation; no server restart between variations.

- 15:13:14 — Delayed feedback observation in the untouched first tab: incorrect delete message still visible (exact matches=1). Saved delete-message-later.jpg. This is only a client-message observation; intervening server restarts mean it is not evidence of unchanged server records.

- 15:13:40 — not-a-year accepted; row shows NaN; saved year-nonnumeric.jpg. Checking API persistence rather than inferring the stored type from the displayed NaN.

- 15:14:14 — Confirmed persisted year is the string not-a-year (full GET saved). Starting a bounded 64-byte incomplete-JSON upload at 1 byte/s to see whether delayed completion changes the malformed-JSON response; other UI work continues. No source inspection.

- 15:14:52 — Additional keyboard/Unicode question: entered S03 Монгол Өгүүллэг / Тест Зохиолч / 2026, pressed Return in the year field; no row was added. The lab does not specify Enter-to-submit, so this observation is not filed as a confirmed defect. Next use the explicit add button as a control.

- 15:15:09 — Explicit add accepted the Mongolian title/author without corrupted glyphs. Search Өгүүллэг returns the new book by a title substring. Saved unicode-valid-add.jpg; now compare the lowercase Cyrillic form.

- 15:15:47 — Cyrillic case comparison: Өгүүллэг matched the added book, өгүүллэг returned no data rows. Saved search-cyrillic-lowercase.jpg; grouped with BUG-07. Slow malformed upload actually measured 65 bytes / 65.00 seconds and still returned HTTP 200 result=OK; the earlier provisional note said 64 bytes, corrected by the measured transcript.

- 15:16:00 — Author comparison gives the same result: Тест Зохиолч matches, тест зохиолч returns no rows. Saved search-cyrillic-author.jpg. Search examines both fields but preserves case sensitivity; this narrows BUG-07 to the comparison behavior rather than a missing author search.

- 15:16:25 — Supermodel baseline metrics from visible DOM: {"deleteButtons":[{"background":"rgb(44, 122, 75)","text":"Устгах"},{"background":"rgb(44, 122, 75)","text":"Устгах"},{"background":"rgb(44, 122, 75)","text":"Устгах"}],"layout":{"documentWidth":1280,"tableWidth":860.0000610351562,"viewportWidth":1280}}. Read-only computed-style/layout checks support the visual green-delete finding and establish a normal-width control before long-text testing. Saved baseline-ui-metrics.json.

- 15:17:04 — Supermodel text review: add button visible label is "Нэмэx"; code points [{"character":"Н","codePoint":"U+041D"},{"character":"э","codePoint":"U+044D"},{"character":"м","codePoint":"U+043C"},{"character":"э","codePoint":"U+044D"},{"character":"x","codePoint":"U+0078"}]. Last letter is Latin x (U+0078), whereas Mongolian Нэмэх ends with Cyrillic х (U+0445). Candidate BUG-12 under the typo-free-text oracle; DOM text evidence saved in add-button-label.json.

- 15:18:05 — Saboteur investigation finished: incomplete POST timed out with 408 at 329.8s while control GETs remained responsive (1–8ms in this run). Not filed as a bug because the oracle gives no timeout duration. Restarted for BUG-04 primary replay: not-json POST returned HTTP 200 and result=OK, followed by unchanged three-book GET and total 4. All headers/bodies saved in bug-04-curl.txt.

- 15:18:27 — Restarted for duplicate-pair tests; three seeded books confirmed. Keep title/author identical to the seeded Clean Code pair; vary year only after the primary exact-duplicate observation.

- 15:18:45 — BUG-06 primary fresh replay: Clean Code / Robert C. Martin / 2008 accepted despite the identical seeded pair. Two identical rows now visible; total 5. Saved bug-06.jpg immediately.

- 15:19:11 — Same title/author with year 2009 also accepted: three Clean Code / Robert C. Martin rows (2008 seeded, 2008 duplicate, 2009 duplicate), newest 2009. Saved duplicate-different-year.jpg. The duplicate key in the oracle is the title/author pair, not a three-field key.

- 15:19:25 — Fresh reset for the primary case-insensitive search replay, removing duplicate-related ambiguity. Original Clean Code / Robert C. Martin is the sole matching record.

- 15:19:44 — BUG-07 primary fresh replay: query clean returned zero data rows although seeded Clean Code is present. Saved bug-07.jpg. Next compare the exact-case control.

- 15:19:57 — Exact-case query Clean Code returns one seeded row. Saved search-exact-title.jpg. The positive control confirms that the missing lowercase result is not due to an absent record or failed endpoint.

- 15:19:58 — Search variation "robert": visible rows including header=["ГарчигЗохиолчОн"]. Saved search-lowercase-author.jpg.

- 15:19:58 — Search variation "Robert": visible rows including header=["ГарчигЗохиолчОн","Clean CodeRobert C. Martin2,008Устгах"]. Saved search-exact-author.jpg.

- 15:19:59 — Search variation "S03 No Such Book": visible rows including header=["ГарчигЗохиолчОн"]. Saved search-no-match.jpg.

- 15:19:59 — Search variation "": visible rows including header=["ГарчигЗохиолчОн","Тунгалаг ТамирЧ.Лодойдамба1,971Устгах","Clean CodeRobert C. Martin2,008Устгах","The Pragmatic ProgrammerD.Thomas & A.Hunt1,999Устгах"]. Saved search-empty.jpg.

- 15:20:22 — Restarted for long-input layout replay. Positive search controls are complete: exact title/author match, no-match query empty, empty query returns all three. Lowercase author and title failed as BUG-07. Long-text comparison will use the normal 1280-pixel viewport already measured.

- 15:20:46 — BUG-10 fresh replay: title L×300, author A×300, year 2026 accepted. Visible DOM metrics {"documentWidth":6255,"tableWidth":6045.00048828125,"viewportWidth":1280}. Baseline table width was 860 at the same 1280 viewport. Saved bug-10.jpg and long-text-ui-metrics.json immediately; neighboring columns leave the visible area.

- 15:21:00 — Removed the long-text row, reloaded, and measured {"documentWidth":1280,"tableWidth":860.0000610351562,"viewportWidth":1280}. Width returns to the normal baseline, supporting an input-dependent layout defect rather than a permanently mis-sized browser.

- 15:21:37 — Fresh-server route investigation: /old returns HTTP 500 Internal Server Error; subsequent /api/books remains HTTP 200 with three seeds. Saved full curl responses in bug-11-curl.txt. Next follow the actual UI link in this same fresh process.

- 15:21:55 — BUG-11 primary fresh replay: clicked the actual Хуучин хувилбар link on the root page; it navigated to /old and displayed Internal Server Error. Saved bug-11.jpg immediately. Paired curl evidence proves HTTP 500, while the main API remains healthy.

- 15:24:02 — BUG-12 text confirmation on the freshly restarted root page: visible add-button text remains "Нэмэx", ending in Latin x U+0078, not Cyrillic х U+0445. This violates the typo-free Mongolian text requirement; saved bug-12.jpg alongside the earlier DOM code-point JSON. No implementation code was inspected.

- 15:24:33 — Limited keyboard observation: Tab from title moves to author, year, add button, then search input in the expected visual order. No keyboard-trap defect observed in this short path; this is not a complete accessibility audit. No add/delete was activated during this focus test.

- 15:25:24 — Fed-Ex special-character probe: input title S03 <b>Literal</b> & "quotes", author O'Connor & Co., year 2000. UI row instead shows literal entities &lt;b&gt; / &amp; in the title and &amp; in the author. Saved special-characters-candidate.jpg. Candidate BUG-13: valid user text changes along the data path; verify API and fresh replay before filing. This UI-created record explains any rise in book count during the concurrent interrupted-write probe; its unique marker is different.

- 15:26:10 — Interrupted-write probe completed: unique marker stayed absent during the partial upload and after client abort; completing the same JSON payload then returned 201 and created the marker. No partial-write defect observed. API confirmed the special-character record contained literal HTML entities, so next reset isolates a simple ampersand-only primary replay for candidate BUG-13.

- 15:26:29 — BUG-13 primary fresh replay: S03 Salt & Pepper / O'Connor & Co. / 2000 accepted, but row shows S03 Salt &amp; Pepper and O'Connor &amp; Co. Saved bug-13.jpg. All fields are nonempty and year is valid; this is independent of missing-field/year validation.

- 15:26:36 — Exact original title S03 Salt & Pepper returns no row, despite identical letter case. Saved encoded-title-search.jpg. This separates the encoding/data-change failure from BUG-07 case sensitivity.

- 15:26:52 — Positive search control S03 Salt returns the encoded record. Saved encoded-title-control.jpg. Therefore the original ampersand-containing exact query fails because the stored/searchable text differs, not because no book was created.

- 15:28:30 — BUG-13 separate fresh API replay: sent a JSON file containing literal ampersands; POST returned 201 and follow-up GET contains literal &amp; sequences in title and author. Full baseline/body/POST/GET transcript saved in bug-13-curl.txt. This demonstrates data alteration beyond the visual rendering step.

- 15:29:06 — New test-design question for BUG-10: does every 300-character value overflow, or specifically text without break opportunities? Restarted to compare equally long strings containing spaces against the unbroken-string result.

- 15:29:53 — Equal-length spaced-text control: title and author are each 300 characters with spaces; metrics {"documentWidth":1280,"tableWidth":860.0000610351562,"viewportWidth":1280}. Saved long-spaced-control.jpg and spaced-text-ui-metrics.json. This supports describing BUG-10 specifically as unbroken-text overflow.

- 15:31:03 — API schema exploration: six bounded cases, each on a restarted three-book server. Tested null, empty array, string, number, null author, and null year. Full curl transcripts and schema-summary.json saved. Inspect results before deciding whether any are independent of BUG-02/03/04; do not inflate the bug count for validation variants.

- 15:32:15 — Defect-investigation phase begins. Schema matrix produced a new availability candidate: null body reset the connection and subsequent GET could not connect. The batch collector failed to summarize that case after receiving no response, so schema-summary.json intentionally has only five successful collections. Array/string/number/null-author/null-year cases are validation variants of existing findings; do not count them as five new bugs. Isolate null crash and retain stderr before any restart.

- 15:32:18 — BUG-14 isolated fresh replay: POST JSON null returns no HTTP response (curl connection-reset failure), following GET cannot connect, and recorded server PID is gone. Preserved complete curl stdout/stderr and server stderr before restarting. The server error is a TypeError accessing title on null. A crash is an availability failure, not another accepted-empty-row variant.

- 15:33:36 — Recovery after null crash: restarted; original three records returned. Runtime stderr included an automatic source-line excerpt with the TypeError; app.js itself was not opened or inspected to search for defects. Next investigate count/max-year behavior at 3, 2, 1, and 0 valid records, without assuming a display contract for newest year when empty.

- 15:33:57 — Count/max-year boundary: deleted seeded Clean Code; remaining table rows=["ГарчигЗохиолчОн","Тунгалаг ТамирЧ.Лодойдамба1,971Устгах","The Pragmatic ProgrammerD.Thomas & A.Hunt1,999Устгах"]; Нийт ном: 3 · Хамгийн шинэ он: 1999. The fixture is disposable and the server restart restores it.

- 15:33:57 — Count/max-year boundary: deleted seeded The Pragmatic Programmer; remaining table rows=["ГарчигЗохиолчОн","Тунгалаг ТамирЧ.Лодойдамба1,971Устгах"]; Нийт ном: 2 · Хамгийн шинэ он: 1971. The fixture is disposable and the server restart restores it.

- 15:33:57 — Count/max-year boundary: deleted seeded Тунгалаг Тамир; remaining table rows=["ГарчигЗохиолчОн"]; Нийт ном: 1 · Хамгийн шинэ он: 0. The fixture is disposable and the server restart restores it.

- 15:34:11 — Empty-list API control confirms books=[] but stats.total=1 and newest=0. Saved empty-list-curl.txt and empty-list-count.jpg. This is another boundary manifestation of BUG-01, not a new count bug; no defect is asserted for the unspecified empty newest-year display.

- 15:34:48 — Added S03 Empty List Recovery / Session Tester / 1000 from an empty list; one row, total 2, newest 1000. Saved empty-list-recovery.jpg. Reload retained the one record. This tests an empty-to-populated transition and distinguishes reload from restarting the in-memory server.

- 15:35:44 — Reload-versus-restart control completed: reload retained the sole test book; restarting node app.js restored precisely ids 1/2/3 and removed the test record. Full API before/after saved. This supports the common reproduction precondition and avoids treating a page reload or a new clone alone as a fresh app state.

- 15:47:35 — Investigation analysis checkpoint: classify array/string/number/null-field acceptance as variants of required-field/year validation; distinguish valid-JSON-null process termination (availability) from malformed-syntax success (error status). Reviewed the measured HTTP/UI evidence and the exact fresh-state reproduction sequence. No new bug reports or debrief were written during this analysis. Next visually review primary screenshots against the observed states.

- 15:48:07 — Visual investigation review completed for primary screenshots: baseline, empty fields, year 2101, delete feedback, exact duplicate, lowercase search, long-text overflow, failed old link, add-label typo, and ampersand data change. Images show the recorded states; BUG-05 includes all three original books. API-only findings retain textual evidence. This review concerns observed application behavior, not post-session report authoring.

- 15:50:01 — Environment trace saved: node -v, curl.exe --version, observed browser User-Agent and OS build. This preserves the actual assisted-test environment separately from the original Opera reproductions. Primary screenshots were visually compared to observed states; no report files have been rewritten yet.

- 15:50:33 — Source-integrity control: re-extracted app.js from the user's teacher-provided app.rar to a separate reference folder and compared SHA256. Tested file is byte-identical; neither source was opened for defect hunting. Saved source-integrity.txt. Thus observed bugs belong to the supplied app rather than a modified fixture.

- 15:52:06 — Late-session UI health check after the earlier restart: form/search empty; exactly three original rows; total 4; no test-created records. Saved late-clean-baseline.jpg. Source-integrity check passed against the original archive, so the observed count/format/color defects persist on the unmodified teacher fixture.

- 15:53:43 — Investigation closure: unresolved coverage includes full accessibility/assistive technology, cross-browser comparison, sustained bulk concurrency, and broader security cases. Only the short Tab path and one slow/incomplete client were tested; do not generalize these into full accessibility/load/security claims. Prepared a scoped reset helper outside the repository for the later fresh-clone replay; teacher app.js remains unchanged.

- 15:54:27 — Additional server-side confirmations on separate fresh processes: POST year 2101 returned 201 and stored that out-of-range year (BUG-03); POST exact seeded Clean Code pair returned 201 and stored a duplicate (BUG-06). Full curl baseline/body/POST/GET files saved. These corroborate existing UI findings rather than adding new bug IDs.

- 16:07:30 — Final cleanup restart removed the duplicate created by the late API confirmation. Exactly the three original records remain. Closing observations will use a fresh browser reload and final GET; no test-created records will be left at timebox end.

- 16:09:44 — Closing record: the predeclared observation window was 14:59:08–15:59:08 (60 minutes). This closing entry and the cleanup at 16:07:30 were recorded after that cutoff and are excluded from the 60-minute accounting. The previous cleanup note's future-tense reference to timebox end was late; retain this correction rather than changing its timestamp. No report/debrief files were authored inside the 60-minute window. Post-window cleanup confirmed the original three records. Formal report authoring begins now.
