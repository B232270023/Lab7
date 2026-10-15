# Bug 01 — Stats total does not match the books list

- Severity: Medium (P2)
- Area: Data/API consistency

## Expected

For the unfiltered list, stats.total should match the number of book objects returned by GET /api/books, and the UI total should agree with the displayed list.

## Actual

On the app's clean default state, the table and /api/books show three books, but GET /api/stats returns total: 4. The UI also says “Нийт ном: 4”. The same one-item discrepancy remained after adding and deleting a test record.

## Reproduction

1. Load the default Reading List v2.0 page.
2. Count the three visible book rows.
3. Request GET /api/stats and GET /api/books from the same local app.
4. Compare stats.total with the length of the returned array.

## Evidence

Full curl -i status lines, headers, and bodies are in [bug-01-stats-curl.txt](../evidence/bug-01-stats-curl.txt).
