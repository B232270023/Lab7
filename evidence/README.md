# Evidence notes

The original CUA screenshot-export route was blocked. After the session, the tester supplied Opera screenshots; the original nine UI captures are in `../screenshots/`, and selected fresh-clone replay captures are in `../screenshots/replay/`.

- `bug-01-curl.txt` contains complete curl -i response headers and bodies for the original API count mismatch.
- `bug-02-curl.txt` contains the missing-fields POST response and follow-up book/stats responses.
- `bug-04-curl.txt` contains the original malformed-JSON response and follow-up unchanged book/stats responses.
- `fresh-clone-bug-01-counts.txt` records the fresh-clone stats/list counts before add, after add, and after delete; the screenshot is `../screenshots/replay/bug-01-api-counts.png`.
- `fresh-clone-bug-04-malformed-json.md` summarizes the fresh-clone malformed-JSON replay; its terminal capture is `../screenshots/replay/bug-04-malformed-json-api.png`.
