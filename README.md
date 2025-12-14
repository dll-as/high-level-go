# 🧠 Fundamentals & Core Language (پایه اما مصاحبه‌ای)

---

## [1. تفاوت var x = y و x := y چیست؟](01_Fundamentals_Core/1-var-vs-short.md)
- چه تفاوت‌هایی در scope و type inference دارند؟
- چه زمانی ممکن است `:=` باعث shadowing شود؟
- آیا performance یا allocation runtime تفاوت دارد؟
- چند متغیر همزمان با `:=` تعریف کنیم، چگونه type inference اعمال می‌شود؟
- مثال عملی از shadowing در حلقه‌ها یا if block.

---

## [2. تفاوت بین مقدار صفر (zero value) و nil چیست؟](01_Fundamentals_Core/2-zero-vs-nil.md)
- zero value چیست و برای انواع اصلی مانند int, string, bool چه مقداری دارد؟
- nil برای reference types چه کاربردی دارد؟
- چرا nil و zero value همیشه یکسان نیستند؟
- مثال practical در struct، slice و map.

---

## [3. چه typeهایی zero value آن‌ها nil است؟](01_Fundamentals_Core/3-nil-types.md)
- reference types: pointer, slice, map, channel, func, interface
- چرا برای struct و array صفر value متفاوت است؟
- مثال practical از nil pointer و nil slice.

---

## [4. تفاوت nil slice و empty slice چیست؟](01_Fundamentals_Core/4-nil-vs-empty-slice.md)
- چگونه declaration یا make ایجاد می‌کند؟
- چه تفاوتی در len و cap دارند؟
- تاثیر بر append و reallocation.
- نکته subtle: اشتراک حافظه (underlying array) و garbage collection.

---

## [5. تفاوت nil slice و empty slice در JSON چیست؟](01_Fundamentals_Core/5-nil-vs-empty-json.md)
- خروجی marshal برای هرکدام چه تفاوتی دارد؟
- چه زمانی nil بهتر است و چه زمانی empty slice بهتر است؟
- مثال practical با encoding/json.

---

## [6. تفاوت len و cap در slice چیست؟](01_Fundamentals_Core/6-len-vs-cap-slice.md)
- len تعداد عناصر واقعی است.
- cap تعداد عناصر قابل ذخیره‌سازی در underlying array است.
- تاثیر بر append و reallocation.
- مثال از append که capacity رشد می‌کند.

---

## [7. تفاوت len و cap در array چیست؟](01_Fundamentals_Core/7-len-vs-cap-array.md)
- len و cap در array همیشه برابرند؟
- چرا slice این انعطاف را دارد ولی array نه؟
- مثال practical با slice گرفتن از array.

---

## [8. تفاوت make و new چیست؟](01_Fundamentals_Core/8-make-vs-new.md)
- new برای چه نوع‌ها استفاده می‌شود و heap/stack allocation؟
- make برای چه type هایی (slice, map, channel) لازم است؟
- مثال practical: slice با new و make.

---

## [9. تفاوت make و append برای ساخت slice چیست؟](01_Fundamentals_Core/9-make-vs-append.md)
- make capacity اولیه می‌سازد و append در صورت پر بودن capacity باعث reallocation می‌شود.
- append روی nil slice چگونه عمل می‌کند؟
- مثال practical با growth factor و copy.

---

## [10. تفاوت new و struct literal چیست؟](01_Fundamentals_Core/10-new-vs-literal.md)
- new(struct) و &struct{} چه تفاوتی دارند؟
- آیا new همیشه heap allocate می‌کند؟
- مثال practical با pointer receiver.

---

## [11. تفاوت string و []byte چیست؟](01_Fundamentals_Core/11-string-vs-byte.md)
- string immutable است ولی []byte mutable.
- تبدیل string به []byte و بالعکس معمولاً باعث copy می‌شود.
- string در Go نوعی slice از byte نیست، اما رفتار شبیه دارد.
- مثال practical با تغییر مقدار.

---

## [12. تفاوت rune و byte چیست؟](01_Fundamentals_Core/12-rune-vs-byte.md)
- byte = uint8
- rune = int32 (represent Unicode code point)
- مثال practical با string indexing و iteration.

---

## [13. چرا string در Go immutable است؟](01_Fundamentals_Core/13-string-immutable.md)
- مزیت برای concurrency و sharing.
- مثال practical از اشتباهات رایج در تغییر string.
- تبدیل به []byte برای ویرایش.

---

## [14. تفاوت constant و variable چیست؟](01_Fundamentals_Core/14-const-vs-var.md)
- compile-time vs runtime value
- memory allocation تفاوت دارد یا نه
- مثال practical با const و var

---

## [15. تفاوت untyped constant و typed constant چیست؟](01_Fundamentals_Core/15-untyped-vs-typed-const.md)
- untyped: flexible, می‌تواند در expression‌های مختلف استفاده شود
- typed: محدود به type مشخص
- مثال practical با عملیات ریاضی و type conversion

---

## [16. تفاوت constant expression و runtime value چیست؟](01_Fundamentals_Core/16-const-expr-vs-runtime.md)
- constant expression در compile-time محاسبه می‌شود
- runtime value فقط در زمان اجرای برنامه تعیین می‌شود
- تاثیر بر performance و compiler optimization

---

## [17. تفاوت fallthrough در switch چیست؟](01_Fundamentals_Core/17-fallthrough.md)
- fallthrough باعث می‌شود case بعدی اجرا شود حتی اگر شرط true نباشد
- مثال practical و ریسک‌های اشتباه

---

## [18. تفاوت break و continue چیست؟](01_Fundamentals_Core/18-break-vs-continue.md)
- break: خروج از loop
- continue: رد کردن iteration فعلی و رفتن به بعدی
- مثال practical با nested loops

---

## [19. تفاوت range روی array و slice چیست؟](01_Fundamentals_Core/19-range-array-vs-slice.md)
- range روی array copy می‌سازد؟
- range روی slice چه تفاوتی دارد؟
- تاثیر بر memory allocation

---

## [20. تفاوت range روی string چیست؟](01_Fundamentals_Core/20-range-string.md)
- range روی string توسط rune iteration انجام می‌شود
- مثال practical با کاراکترهای Unicode و multi-byte
- performance considerations
