Student name: О.Шинэбаяр  
Student code: B232270023  
Node.js: v24.14.1  
Browser used for UI reproductions and screenshots: Opera One 136.0.6008.80 (Chromium 152.0.7977.134), Windows 11 64-bit
Additional browser used during assisted exploration: Codex In-app Browser; version unavailable

# Lab 07 — Exploratory testing (SBTM)

Black-box exploratory testing of the Reading List v2.0 app. The session charter and chronological notes are in [charter.md](charter.md) and [session-report.md](session-report.md). Confirmed findings and evidence are listed in [bugs/](bugs/) and [evidence/](evidence/).

## Confirmed findings

| ID | Finding | Severity |
| --- | --- | --- |
| [BUG-01](bugs/bug-01.md) | Total count differs from the displayed book rows | Minor |
| [BUG-02](bugs/bug-02.md) | Empty/missing fields and whitespace-only title/author are accepted | Major |
| [BUG-03](bugs/bug-03.md) | Year range and integer rules are not enforced | Major |
| [BUG-04](bugs/bug-04.md) | Malformed JSON receives a success response | Major |
| [BUG-05](bugs/bug-05.md) | Delete leaves the “book added” status message | Minor |
| [BUG-06](bugs/bug-06.md) | Duplicate title and author pairs are accepted | Major |
| [BUG-07](bugs/bug-07.md) | Search is case-sensitive for title and author | Minor |
| [BUG-08](bugs/bug-08.md) | Years are displayed with thousands separators | Cosmetic |
| [BUG-09](bugs/bug-09.md) | Delete buttons are green instead of red | Cosmetic |
| [BUG-10](bugs/bug-10.md) | Long unbroken text expands the table beyond the viewport | Minor |

## Debrief

Supermodel and Fed-Ex were most effective for normal add, search, list, delete, and count flows; they exposed the count mismatch (BUG-01), stale delete feedback (BUG-05), duplicate records (BUG-06), and case-sensitive search (BUG-07). Couch Potato found missing or whitespace-only fields (BUG-02), invalid year values (BUG-03), year formatting (BUG-08), and long-text overflow (BUG-10). Saboteur confirmed malformed JSON receives HTTP 200 (BUG-04), and its missing-fields request also supports BUG-02; full `curl -i` transcripts are saved in `evidence/`. Supermodel's visual review also found the green delete buttons (BUG-09). No separate confirmed out-of-charter defect was filed; the old-version link opened a blank tab, but direct navigation was blocked, so its destination remains unverified. A follow-up charter should focus on page and link navigation, keyboard/accessibility behavior, and concurrent requests, which were not covered. The post-session fresh-clone replay is documented in [session-report.md](session-report.md). Lab 1 Playwright checks could automate the count, validation, duplicate, search, delete-feedback, and malformed-JSON findings. Playwright could also assert button color and table overflow through CSS and layout checks, although visual inspection made those presentation defects easy to notice. The original session app was restored to its three seeded records with the form and search cleared at session end; the separate post-session clone was used for replay. The nine original UI screenshots were captured in Opera One 136.0.6008.80 (Chromium 152.0.7977.134), Windows 11 64-bit; the assisted exploration also used Codex In-app Browser (version unavailable).
