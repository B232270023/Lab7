# Нотолгооны индекс

Үндсэн эх сурвалж: [Session 03](session-03/) — 2026-10-21. curl файл бүрт тухайн хүсэлтийн HTTP response header/body байна; server хариу өгөөгүй BUG-14-ийн хувьд baseline HTTP 200, POST-ийн бүтэн stderr/exit code, дараах холболтын алдаа хадгалагдсан.

| Файл | Утга |
| --- | --- |
| [bug-01-curl.txt](session-03/bug-01-curl.txt) | BUG-01-ийн шинэ server дээрх baseline ба үндсэн API нотолгоо |
| [bug-02-curl.txt](session-03/bug-02-curl.txt) | BUG-02-ийн шинэ server дээрх baseline ба үндсэн API нотолгоо |
| [bug-03-curl.txt](session-03/bug-03-curl.txt) | BUG-03-ийн шинэ server дээрх baseline ба үндсэн API нотолгоо |
| [bug-04-curl.txt](session-03/bug-04-curl.txt) | BUG-04-ийн шинэ server дээрх baseline ба үндсэн API нотолгоо |
| [bug-06-curl.txt](session-03/bug-06-curl.txt) | BUG-06-ийн шинэ server дээрх baseline ба үндсэн API нотолгоо |
| [bug-11-curl.txt](session-03/bug-11-curl.txt) | BUG-11-ийн шинэ server дээрх baseline ба үндсэн API нотолгоо |
| [bug-13-curl.txt](session-03/bug-13-curl.txt) | BUG-13-ийн шинэ server дээрх baseline ба үндсэн API нотолгоо |
| [bug-14-curl.txt](session-03/bug-14-curl.txt) | BUG-14-ийн шинэ server дээрх baseline ба үндсэн API нотолгоо |
| [bug-14-server-stderr.txt](session-03/bug-14-server-stderr.txt) | null JSON-ийн дараах Node runtime алдаа |
| [add-button-label.json](session-03/add-button-label.json) | BUG-12-ын UI text ба Unicode code point |
| [baseline-ui-metrics.json](session-03/baseline-ui-metrics.json) | Ногоон товчнууд, хэвийн 860 px хүснэгт |
| [long-text-ui-metrics.json](session-03/long-text-ui-metrics.json) | BUG-10-ын 6045 px өргөн |
| [source-integrity.txt](session-03/source-integrity.txt) | Багшийн archive ба тестэлсэн app.js SHA256 ижил |
| [environment.txt](session-03/environment.txt) | node -v, curl version, browser User-Agent, OS build |
| [session-timing.json](session-03/session-timing.json) | Урьдчилан тогтоосон цонх ба хожуу хаалтын бодит цаг |

Нэмэлт raw файлууд нь year, empty list, special characters, slow/incomplete client, schema төрөл, reload/reset зэрэг судалгааны ажиглалт. schema-null-body-curl.txt нь анхны collector хариугүй кейсийг бүрэн цуглуулж чадаагүй оролдлого; түүнийг үндсэн нотолгоо гэж ашиглаагүй, бүрэн давталт нь bug-14-curl.txt юм. schema-summary.json дахь таван кейсийг таван шинэ согог гэж тоолоогүй.

[Session 02](session-02/) тасарсан ажлын нэмэлт нотолгоо. Энэ хавтасны хуучин bug-01/02/04-curl.txt нь 2026-10-15-ны материал; fresh-clone-bug-01-counts.txt дахь 19 номтой төлөв нь шинэ server-ийн гурван seeded record-ийн баталгаа биш. Одоогийн report-ууд эдгээр хуучин файлыг үндсэн replay гэж ишлээгүй.

## Шинэ clone-ийн эцсийн давталт

[final-clone/](final-clone/) нь b26e6ba-г шинэ хавтаст clone хийж, bug бүрийг шинэ server дээр дагасан post-session QA-ийн үр дүн. API/UI summary болон validation-summary.json нь 14/14 тайлагнасан зан төлөв дахин гарсныг бүртгэсэн.
