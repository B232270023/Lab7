# BUG-08: Хүчинтэй оныг энгийн тооны оронд мянгатын таслалтай харуулдаг

Орчин: Reading List v2.0; Node.js v24.13.0; Codex In-app Browser (ажигласан User-Agent Chrome/155.0.0.0); Windows x64, 25H2, build 26200.9711; 2026-10-21.
API хэрэгсэл: curl.exe 8.21.0.
Урьдчилсан нөхцөл: Өмнөх node app.js process-ийг Ctrl+C-ээр зогсоож node app.js-ийг дахин асаасан; браузераа reload хийсэн; GET /api/books нь id 1, 2, 3 бүхий Тунгалаг Тамир, Clean Code, The Pragmatic Programmer гэсэн яг гурван ном буцаана. Page reload дангаараа server reset биш.

## Дахин гаргах алхам

1. Шинээр асаасан аппын эхний хүснэгтийн Он баганыг уншина.
2. Clean Code-ийн 2008 болон The Pragmatic Programmer-ийн 1999 оны харагдах форматыг харьцуулна.

Хүлээгдэж байсан: Oracle-ийн “хүснэгтэд энгийн тоогоор, жишээ нь 1999” дүрмээр 2008, 1999 гэж харагдана.

Бодит үр дүн: 2,008 болон 1,999 гэж харагдсан; valid 1000/2100 control мөн 1,000/2,100 болсон.

Ноцтой байдал: Cosmetic — Утга уншигдаж байгаа боловч заасан жилийн формат зөрчигдөнө.

Олдсон аялал: Supermodel.

## Хавсралт

![BUG-08](../screenshots/session-03/baseline.jpg)

[Хүчинтэй 2100 оны хяналт](../screenshots/session-03/year-valid-2100.jpg)
