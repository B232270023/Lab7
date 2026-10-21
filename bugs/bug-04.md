# BUG-04: Синтакс буруу JSON-д HTTP 400 өгөхийн оронд HTTP 200 OK буцаадаг

Орчин: Reading List v2.0; Node.js v24.13.0; Codex In-app Browser (ажигласан User-Agent Chrome/155.0.0.0); Windows x64, 25H2, build 26200.9711; 2026-10-21.
API хэрэгсэл: curl.exe 8.21.0.
Урьдчилсан нөхцөл: Өмнөх node app.js process-ийг Ctrl+C-ээр зогсоож node app.js-ийг дахин асаасан; браузераа reload хийсэн; GET /api/books нь id 1, 2, 3 бүхий Тунгалаг Тамир, Clean Code, The Pragmatic Programmer гэсэн яг гурван ном буцаана. Page reload дангаараа server reset биш.

## Дахин гаргах алхам

1. not-json гэсэн яг найман ASCII byte бүхий body.json файл үүсгэнэ.
2. Content-Type: application/json толгойтой POST /api/books хүсэлтийг доорх curl -i командаар илгээнэ.
3. HTTP статус, response body-г уншаад дараа нь GET /api/books-ээр өөрчлөлтгүйг шалгана.

Хүлээгдэж байсан: API-ийн oracle: буруу JSON биетэй POST-д HTTP 400 алдаа буцаана.

Бодит үр дүн: HTTP/1.1 200 OK болон {"result":"OK"} ирсэн. Дараах GET нь өмнөх гурван номыг буцаасан; хүсэлт хэрэгжээгүй боловч амжилттай гэж мэдээлсэн.

Ноцтой байдал: Major — Клиент зөвшөөрөгдөөгүй хүсэлтээ амжилттай гэж ойлгоно.

Олдсон аялал: Saboteur.

## Хавсралт

[Baseline, POST, follow-up GET, stats-ийн бүтэн curl](../evidence/session-03/bug-04-curl.txt) · [Удаан upload-ийн нэмэлт баталгаа](../evidence/session-03/slow-malformed-curl.txt)

## Нэмэлт тодруулга

PowerShell-д curl.exe, Linux/macOS-д curl хэрэглэнэ. Доорх ASCII body файлыг UTF-8 BOM-гүй эсвэл ASCII байдлаар хадгална; JSON-ийг shell-ийн хашилтаар шууд дамжуулах шаардлагагүй.

```powershell
Set-Content -LiteralPath body.json -Value 'not-json' -Encoding ascii -NoNewline
curl.exe -i --max-time 5 -H "Content-Type: application/json" --data-binary "@body.json" http://localhost:3000/api/books
curl.exe -i --max-time 5 http://localhost:3000/api/books
```

Linux/macOS хувилбар:

```bash
printf '%s' 'not-json' > body.json
curl -i --max-time 5 -H "Content-Type: application/json" --data-binary "@body.json" http://localhost:3000/api/books
curl -i --max-time 5 http://localhost:3000/api/books
```
