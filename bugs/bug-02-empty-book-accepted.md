# Bug 02 — Empty book form creates a blank record

- Severity: Medium (P2)
- Area: Input validation / data integrity

## Expected

The add flow should reject a book without a title, author, or year and should not create a record.

## Actual

Submitting the form with all three fields empty displayed “Ном нэмэгдлээ”, created a visible blank row with year 0, and incremented the total. The record remained after page reload. It was removed during cleanup.

## Reproduction

1. Open the Reading List v2.0 page.
2. Clear the title, author, and year fields.
3. Click “Нэмэx”.
4. Observe the success message, blank table row, year 0, and increased total.

## Evidence

A screenshot was captured in the browser during the session. The browser safety policy blocked exporting that screenshot to a local file using the available workflow, so an image file is not attached. The exact visual result is also recorded in session-report.md.
