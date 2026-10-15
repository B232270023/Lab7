# BUG-04: Буруу JSON POST хүсэлт амжилттай мэт хариу буцаадаг

Орчин: Reading List v2.0 API, curl.exe, Windows 11 64-bit, 2026-10-15
Урьдчилсан нөхцөл: App ажиллаж, initial 3 book list өгөгдөлтэй байна.

## Дахин гаргах алхам
1. Content-Type: application/json толгойтой POST /api/books илгээнэ.
2. Body-г not-json болгоно.
3. HTTP статус ба body-г ажиглана.
4. GET /api/books-ээр өгөгдөл өөрчлөгдсөн эсэхийг шалгана.

Хүлээгдэж байсан: API буруу JSON биетэй POST хүсэлтэд HTTP 400 алдаа буцаана.
Бодит үр дүн: HTTP 200 OK болон {"result":"OK"} буцаасан; дараах GET-д өгөгдөл өөрчлөгдөөгүй.
Ноцтой байдал: Major — client амжилттай гэж итгэх боловч хүсэлт хэрэгжээгүй.
Хавсралт: evidence/bug-04-curl.txt (HTTP статусын мөр, толгой, body-той бүтэн гаралт).
Олдсон аялал: Saboteur.
