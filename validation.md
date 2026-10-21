# Илгээхийн өмнөх эцсийн шалгалт

2026-10-21-нд GitHub-аас шинэ work/Lab7-final-20261021 хавтаст clone хийж, b26e6baeab061b2f188a8ef8c731864a6ac34a57 commit-ийг шалгасан. Эх clone-ийн working tree цэвэр байсан; багшийн app.js-ийг .gitignore-д орсон байдлаар хуулсан. App-ийн SHA256 нь багшийн эх archive-тай ижил A2158DC202E62A18F11ADCC0FECA1D84FB6C6A9EC269B8EB63BC72F10EB27C6C.

Bug бүрийн үндсэн алхмыг тусдаа server restart, анхны гурван seeded record-ийн баталгаатай төлөвөөс давтсан; зөвхөн шинэ clone хийснээр server цэвэр болсон гэж үзээгүй. API ба UI давталтын нотолгоо нь [evidence/final-clone/](evidence/final-clone/) болон [screenshots/final-clone/](screenshots/final-clone/) дотор бий. Энэ нь SBTM цонхны дараах QA бөгөөд 60 минутын session-ийн цагт ороогүй.

| Тайлан | Давталтын арга | Тайлагнасан үр дүн |
| --- | --- | --- |
| [BUG-01](bugs/bug-01.md) | UI ба API | Дахин гарсан |
| [BUG-02](bugs/bug-02.md) | UI ба API | Дахин гарсан |
| [BUG-03](bugs/bug-03.md) | UI ба API | Дахин гарсан |
| [BUG-04](bugs/bug-04.md) | API / process | Дахин гарсан |
| [BUG-05](bugs/bug-05.md) | UI / харагдах DOM | Дахин гарсан |
| [BUG-06](bugs/bug-06.md) | UI ба API | Дахин гарсан |
| [BUG-07](bugs/bug-07.md) | UI / харагдах DOM | Дахин гарсан |
| [BUG-08](bugs/bug-08.md) | UI / харагдах DOM | Дахин гарсан |
| [BUG-09](bugs/bug-09.md) | UI / харагдах DOM | Дахин гарсан |
| [BUG-10](bugs/bug-10.md) | UI / харагдах DOM | Дахин гарсан |
| [BUG-11](bugs/bug-11.md) | UI ба API | Дахин гарсан |
| [BUG-12](bugs/bug-12.md) | UI / харагдах DOM | Дахин гарсан |
| [BUG-13](bugs/bug-13.md) | UI ба API | Дахин гарсан |
| [BUG-14](bugs/bug-14.md) | API / process | Дахин гарсан |

## Бүрдлийн шалгалт

| Шаардлага | Баримт |
| --- | --- |
| Public үндсэн репо | GitHub API: private=false, default_branch=main |
| README-ийн эхэнд нэр, код, node -v, браузерийн хувилбар | Шинэ тестийн бодит орчноор бичсэн; environment.txt хавсаргасан |
| Зааврын DOCX байхгүй, .gitignore | Tracked DOCX байхгүй; .DS_Store, .idea/, node_modules/ байна |
| Ажлын явцын commit | Шалгах үед 22 commit; доорх урьдчилсан charter → report → bug дараалалтай |
| Charter | 3 томьёоны хэсэг; үндэслэлтэй 4 аялал, өөр 4 district |
| Session report | Түүхий тэмдэглэлийн бүтэн хуулбар, issues, Setup / дизайн-гүйцэтгэл / согог судлах нийлбэр 100% |
| 60 минутын цонх | Урьдчилан тогтоосон 14:59:08–15:59:08; хожуу хаалтын бодит цаг ба дараах cleanup тусдаа ил тод бүртгэлтэй |
| 3+ ялгаатай согог | 14 report; required-field/year-ийн хувилбаруудыг тус тус нэгтгэсэн |
| UI screenshot | Одоогийн UI report бүр Session 03-ын зурагтай |
| UI бус нотолгоо | BUG-04 зэрэгт бүтэн curl -i HTTP статус/header/body; BUG-14-д хариугүй уналтын stdout/stderr/exit code |
| Debrief | 9 өгүүлбэр; tour mapping ба automation тайлбар report-уудтай нийцнэ |
| Шинэ clone-ийн replay | 14/14 үндсэн тайлан дахин гарсан; app.js byte-identical |
| Teams | Эзэмшигч өмнө нь Turn in хийсэн гэж баталсан; энэ QA-аар Teams эсвэл due date-ийг бие даан батлаагүй |

## Цагийн дараалал

- Charter: 9569ae40586c1aea179317c1ca388804d5c40b8a 2026-10-21T14:58:03+08:00.
- Session report: ecfa96380c8cdc7e9e93d326c7992446115cf365 2026-10-21T16:09:49+08:00.
- Bug report-ууд: b26e6baeab061b2f188a8ef8c731864a6ac34a57 2026-10-21T16:56:22+08:00.

Charter-ийн хамгийн сүүлийн өөрчлөлт нь session эхлэхээс өмнөх 9569ae4 хэвээр; дараа нь charter-ийн цаг, агуулгыг өөрчлөөгүй. Тасарсан Session 02 болон хуучин post-session screenshot-ууд нь архивын материал гэж ялгагдсан. Шинэ шалгалтыг Codex гүйцэтгэсэн AI-assisted ажил гэдгийг report/README-д ил тод бичсэн.

Машинаар унших үр дүн: [validation-summary.json](evidence/final-clone/validation-summary.json), [API summary](evidence/final-clone/api-summary.json), [UI summary](evidence/final-clone/ui-summary.json).

## GitHub дээрх зураг

UI report-уудын 10 ялгаатай үндсэн image URL бүгд HTTP 200 буцаасан; хуваалцсан baseline зурагтай нийлээд 12 UI report-ийг хамарна. BUG-05-ын GitHub Preview дэх image complete=true, naturalWidth=1280, naturalHeight=720 гэж бодитоор ачаалсан.

[Зураг бүрийн HTTP шалгалт](evidence/final-clone/github-image-http-check.json) · [GitHub Preview-ийн DOM баталгаа](evidence/final-clone/github-render-check.json) · [Баримтын холбоос ба бүтцийн шалгалт](evidence/final-clone/document-check.json).
