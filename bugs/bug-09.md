# BUG-09: Устгах үйлдлийн товч улаан бус ногоон байна

Орчин: Reading List v2.0; Node.js v24.13.0; Codex In-app Browser (ажигласан User-Agent Chrome/155.0.0.0); Windows x64, 25H2, build 26200.9711; 2026-10-21.
API хэрэгсэл: curl.exe 8.21.0.
Урьдчилсан нөхцөл: Өмнөх node app.js process-ийг Ctrl+C-ээр зогсоож node app.js-ийг дахин асаасан; браузераа reload хийсэн; GET /api/books нь id 1, 2, 3 бүхий Тунгалаг Тамир, Clean Code, The Pragmatic Programmer гэсэн яг гурван ном буцаана. Page reload дангаараа server reset биш.

## Дахин гаргах алхам

1. Анхны гурван номын мөр дэх Устгах товчнуудын өнгийг ажиглана.
2. Зурагтай харьцуулж, шаардлагатай бол харагдах DOM-ийн computed background color-ийг шалгана.

Хүлээгдэж байсан: Спецификацийн дагуу аюултай үйлдлийн Устгах товч улаан өнгөтэй байна.

Бодит үр дүн: Гурван товч бүгд ногоон; хэмжсэн background нь rgb(44, 122, 75) байсан.

Ноцтой байдал: Cosmetic — Устгал ажиллаж байгаа ч аюултай үйлдлийн өнгөний дохио зааварт нийцэхгүй.

Олдсон аялал: Supermodel.

## Хавсралт

![BUG-09](../screenshots/session-03/baseline.jpg)

[Дэлгэцийн CSS хэмжилт](../evidence/session-03/baseline-ui-metrics.json)
