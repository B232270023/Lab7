# Session 02 raw notes

Executor: Codex, AI-assisted exploration requested by О.Шинэбаяр (B232270023).
Start: 2026-10-20 15:18:27 +08:00
Planned end: 2026-10-20 16:18:27 +08:00
Charter: 2c7401bddee2eca59b228d5f5621d1985cb7fdd6, committed and pushed before this start.
Environment: Reading List v2.0; Windows x64; Node.js v24.13.0; Codex In-app Browser, observed User-Agent Chrome/155.0.0.0.
This file is appended during exploration. Bug reports and debrief will be edited after the timebox.

- 15:18:27 — Setup phase began. Restarted the supplied unmodified app.js; GET /api/books returned the three seeded records. No source-code inspection. Browser and screenshot-file export were verified during preparation before this timebox.

- 15:19:03 — Baseline UI after fresh restart: exactly three seeded rows; total is 4 (BUG-01), years show 1,971 / 2,008 / 1,999 (BUG-08), delete buttons are green (BUG-09). Saved screenshots/session-02/baseline.jpg immediately.

- 15:19:34 — Setup: captured full curl -i baseline headers and bodies. /api/books has three objects, /api/stats returns total=4 and newest=2008. Saved evidence/session-02/bug-01-curl.txt. UI screenshot and API share the same fresh process.

- 15:20:14 — Setup control: added S02 Valid Flow / Session Tester / 2026. Four rows, total=5, newest=2026; success message displayed. Saved valid-add.jpg. Setup complete; test design and execution phase begins now.

- 15:20:37 — Fed-Ex: searched the newly added book by exact title (one row), clicked Бүгд (four rows), then deleted only S02 Valid Flow. All three original books remain, total returns to 4, newest to 2008, but status still says Ном нэмэгдлээ (BUG-05). Saved bug-05.jpg immediately; this corrects the old two-row screenshot mismatch.

- 15:21:14 — Restarted the app for Couch Potato missing-field checks; verified exactly three seeded API objects before using the UI.

- 15:21:31 — Couch Potato: from a fresh three-book server, clicked Нэмэx with every add field empty. A fourth blank row appeared with year 0; total=5; status Ном нэмэгдлээ. BUG-02 confirmed and screenshot bug-02.jpg saved immediately.

- 15:21:52 — GUI blank row persisted after reload. Restarted separately for the Saboteur missing-fields variant: curl POST {} returned 201 and a fourth record with blank title/author, no year. Saved complete before/POST/after responses in evidence/session-02/bug-02-curl.txt. Same required-field defect, not a separate bug.

- 15:22:32 — Saboteur: fresh process baseline had three books. POST malformed body not-json received HTTP 200 with result=OK; complete follow-up GET shows unchanged three books and total=4. BUG-04 confirmed; all curl headers and bodies saved in evidence/session-02/bug-04-curl.txt.

- 15:23:38 — Restarted for year-boundary exploration. Additional Saboteur question: does a client that stops sending a JSON body block other users? Starting one bounded incomplete POST (at most 370 seconds) with low-rate GET controls, while exploring UI. This is observation of availability, with no assumed timeout requirement.

- 15:24:11 — Fed-Ex boundary input: fresh baseline plus S02 Year 2101 / Session Tester / 2101 was accepted; fourth row year 2,101, total=5, newest=2101. BUG-03 confirmed; bug-03.jpg saved. An incomplete HTTP client in parallel did not prevent this UI operation.

- 15:24:44 — Year 999 accepted in the GUI after removing the previous test row; newest stays 2008. Saved year-999.jpg. This is the lower-bound variant of BUG-03, not another defect.

- 15:25:00 — Year 1999.5 accepted, rendered as 1,999.5. Saved year-decimal.jpg. The integer rule is not enforced (BUG-03).

- 15:25:14 — not-a-year accepted and rendered NaN (BUG-03). Saved year-nonnumeric.jpg. Newest remains 2008; investigate persistence separately rather than assuming NaN was stored as a JSON number.

- 15:25:49 — Reload preserves the NaN display. curl GET shows the stored year is the string not-a-year, rather than a JSON NaN; saved year-nonnumeric-curl.txt. Incomplete-request control GETs remain HTTP 200 at 3–6 ms so far.

- 15:26:03 — Important refinement of BUG-05: reload had cleared the status; deleting the nonnumeric test row then displayed Ном нэмэгдлээ again. Thus the observed defect is an incorrect delete message, not merely an old message staying on screen. Saved delete-after-reload.jpg.

- 15:26:16 — Valid lower boundary 1000 was accepted and rendered 1,000. Validation outcome is correct at this endpoint; separator is BUG-08.

- 15:26:28 — Valid upper boundary 2100 accepted, newest becomes 2100, row rendered 2,100. Saved year-valid-2100.jpg as a positive control.

- 15:27:10 — Explicit year 0 accepted with nonempty title/author; saved year-zero.jpg. This distinguishes invalid numeric year (BUG-03) from a missing year (BUG-02).

- 15:27:21 — Year -1 accepted and displayed unchanged. Saved year-negative.jpg. Removed it after capture. Boundary exploration now covers valid 1000/2100 and invalid 0/-1/999/2101/1999.5/not-a-year.

- 15:27:41 — Followed the visible Хуучин хувилбар link. The browser navigated to /old and displayed Internal Server Error. New candidate BUG-11: a supplied page/link fails, contrary to the all-pages-and-links-work oracle. Screenshot bug-11.jpg saved immediately; verify HTTP status and a fresh-server replay before filing.

- 15:27:53 — curl -i GET /old confirms HTTP 500 Internal Server Error and body Internal Server Error. Saved evidence/session-02/bug-11-curl.txt. This resolves the original session's unverified-link question; still need a fresh-baseline UI replay.

- 15:28:22 — Test-design checkpoint: distinguish failures by observable contract. Required-field omissions remain one bug (02); invalid year acceptance is 03; a valid year still receives a separator, independently proving 08. Count mismatch 01 is established with an unfiltered three-row baseline, so it does not rely on ambiguous filtered-count semantics. /old failure is a separate route failure from malformed POST success (04). No source-based root-cause claims are made.

- 2026-10-21 14:58:03 +08:00 — Resume audit: session 02 was interrupted. Last interactive note is 2026-10-20 15:28:22; the bounded incomplete-request probe subsequently completed at 15:29:07 with HTTP 408 and responsive control GETs. The planned 16:18:27 ending did not constitute a completed 60-minute session. The overnight gap is excluded. Preserve these observations as supplemental evidence only.
