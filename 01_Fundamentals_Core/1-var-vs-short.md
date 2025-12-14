
# تفاوت `var x = y` و `x := y` در Go


در Go، دو روش اصلی برای تعریف متغیر وجود دارد:

1. **`var` declaration**

```go
var x = 10
```

* صریح و قابل استفاده در سطح package و function.
* می‌توان نوع متغیر را مشخص کرد یا به compiler اجازه داد که type inference انجام دهد:

```go
var x int = 10 // صریح
var y = 20     // type inferred: int
```

* می‌تواند بدون مقدار اولیه نیز استفاده شود و مقدار **zero value** می‌گیرد:

```go
var s string  // ""
var n int     // 0
```

2. **Short variable declaration (`:=`)**

```go
x := 10
```

* فقط در داخل **function scope** قابل استفاده است.
* همزمان declaration و initialization انجام می‌دهد.
* **type inference** اجباری است؛ type باید توسط مقدار سمت راست تعیین شود.

> به عبارت ساده:
> `var` انعطاف بیشتری دارد و می‌تواند در package level باشد، `:=` کوتاه و راحت است و فقط داخل توابع کاربرد دارد.

---

## نکات subtle و edge-case

### 1. Shadowing با `:=`

`:=` اگر متغیری با همان اسم در **outer scope** وجود داشته باشد، یک متغیر **جدید در inner scope** می‌سازد و outer variable را shadow می‌کند.

```go
x := 10
if true {
    x := 20        // shadowing
    fmt.Println(x) // 20
}
fmt.Println(x) // 10 (همان متغیر outer)
```

* این موضوع باعث باگ‌های subtle در حلقه‌ها و شرط‌ها می‌شود.
* در مصاحبه‌ها ممکن است از شما بخواهند که رفتار shadowing را تشریح کنید.

### 2. Multi-variable declaration و type inference

```go
a, b := 5, 3.14
```

* `a` inferred به `int`، `b` inferred به `float64`.
* اگر یکی از متغیرها قبلاً تعریف شده باشد، فقط متغیر جدید ایجاد می‌شود و ممکن است shadowing رخ دهد.

### 3. Performance و allocation

* در اکثر موارد، تفاوت `var` و `:=` **تأثیر عملی روی performance ندارد**.
* تفاوت عمده در **scope و visibility** است، نه runtime efficiency.

---

## مثال عملی کوتاه

### Shadowing در حلقه و if block

```go
package main

import "fmt"

func main() {
    x := 1
    fmt.Println("Outer x:", x)

    for i := 0; i < 1; i++ {
        x := 2  // Shadowing outer x
        fmt.Println("Inner x in loop:", x)
    }

    if true {
        x := 3  // Shadowing again
        fmt.Println("Inner x in if:", x)
    }

    fmt.Println("Outer x after blocks:", x)
}
```

**خروجی:**

```
Outer x: 1
Inner x in loop: 2
Inner x in if: 3
Outer x after blocks: 1
```

> توجه داشته باشید که shadowing می‌تواند باعث confusion یا bug شود اگر بدون دقت استفاده شود.


---

## ارتباط با دیگر مفاهیم

* **Scope:** outer vs inner block distinction
* **Type inference:** compiler type deduction
* **Memory allocation:** stack vs heap تصمیم compiler، ولی معمولا تفاوت عملکرد ندارد
* **Shadowing:** می‌تواند روی pointer و reference types تأثیر بگذارد

