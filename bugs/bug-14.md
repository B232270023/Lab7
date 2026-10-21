# BUG-14: JSON null POST нь Node server process-ийг унагаж бүх API-г зогсоодог

Орчин: Reading List v2.0; Node.js v24.13.0; Codex In-app Browser (ажигласан User-Agent Chrome/155.0.0.0); Windows x64, 25H2, build 26200.9711; 2026-10-21.
API хэрэгсэл: curl.exe 8.21.0.
Урьдчилсан нөхцөл: Өмнөх node app.js process-ийг Ctrl+C-ээр зогсоож node app.js-ийг дахин асаасан; браузераа reload хийсэн; GET /api/books нь id 1, 2, 3 бүхий Тунгалаг Тамир, Clean Code, The Pragmatic Programmer гэсэн яг гурван ном буцаана. Page reload дангаараа server reset биш.

## Дахин гаргах алхам

1. null гэсэн яг дөрвөн ASCII byte бүхий null.json файл үүсгэнэ.
2. Content-Type: application/json толгойтой POST /api/books-д файлыг curl -i-ээр илгээнэ.
3. Дараа нь GET /api/books илгээж холболтын төлөвийг шалгана.
4. node app.js ажиллаж байсан terminal-ийн runtime алдаа болон process дууссаныг шалгана.

Хүлээгдэж байсан: Номын шаардлагатай гурван талбаргүй JSON утгыг client error (400 төрлийн хариу)-аар татгалзаж, server ажиллаж үлдэх ёстой; дараагийн valid GET хэвийн хариулна. Үйлчилгээг бүхэлд нь унагахгүй байх нь эрүүл ухааны найдвартай ажиллагааны oracle.

Бодит үр дүн: POST-д HTTP хариу огт ирээгүй; энэ Windows орчинд curl exit=56 connection reset болсон. Дараах GET exit=7 could not connect; Node PID байхгүй болсон. Runtime stderr: TypeError: Cannot read properties of null (reading 'title').

Ноцтой байдал: Critical — Нэг хүсэлт нийт локал үйлчилгээг зогсоож, бүх хэрэглэгчийн UI/API ажиллагааг server-ийг гараар дахин асаах хүртэл хаана.

Олдсон аялал: Saboteur.

## Хавсралт

[Fresh baseline, POST-ийн stdout/stderr, дараах холболтын алдаа](../evidence/session-03/bug-14-curl.txt) · [Node runtime stderr](../evidence/session-03/bug-14-server-stderr.txt)

## Нэмэлт тодруулга

PowerShell-д curl.exe, Linux/macOS-д curl хэрэглэнэ. Доорх ASCII body файлыг UTF-8 BOM-гүй эсвэл ASCII байдлаар хадгална; JSON-ийг shell-ийн хашилтаар шууд дамжуулах шаардлагагүй.

```powershell
Set-Content -LiteralPath null.json -Value 'null' -Encoding ascii -NoNewline
curl.exe -i --max-time 5 -H "Content-Type: application/json" --data-binary "@null.json" http://localhost:3000/api/books
curl.exe -i --max-time 5 http://localhost:3000/api/books
```

Linux/macOS хувилбар:

```bash
printf '%s' 'null' > null.json
curl -i --max-time 5 -H "Content-Type: application/json" --data-binary "@null.json" http://localhost:3000/api/books
curl -i --max-time 5 http://localhost:3000/api/books
```

null нь синтаксийн хувьд хүчинтэй JSON боловч номын object биш. BUG-04-ийн not-json синтаксийн алдаатай хүсэлт амжилттай хариу аваад server ажиллаж үлддэг; энэ кейсийн availability үр дүн тусдаа. Байгаагүй HTTP 500 статусыг нотолгоонд зохиож нэмээгүй. Давталтын дараа node app.js-ийг дахин асааж анхны гурван ном руу сэргээнэ.
