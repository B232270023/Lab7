Student name: О.Шинэбаяр  
Student code: B232270023  
Node.js: v24.14.1  
Browser: Codex In-app Browser; version unknown to the tester

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

The timed session is in progress; the final 8–10 sentence debrief will be added after the 60-minute session ends.
