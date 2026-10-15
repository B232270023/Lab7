# Bug 03 — Non-numeric year is accepted and displayed as NaN

- Severity: Medium (P2)
- Area: Input validation / display

## Expected

A book year should be validated as a numeric year; invalid text should be rejected without creating a record.

## Actual

Submitting a book with title SBTM invalid-year, author QA Session, and year not-a-year succeeded. The table displayed NaN, the success message remained, and the record was still present after reloading. The test record was removed during cleanup.

## Reproduction

1. Enter a title and author.
2. Enter not-a-year in the year field.
3. Click “Нэмэx”.
4. Observe the new row with year NaN.
5. Reload and confirm that the row remains.

## Evidence

A screenshot was captured in the browser during the session. The browser safety policy blocked exporting that screenshot to a local file using the available workflow, so an image file is not attached. The exact visual result is also recorded in session-report.md.
