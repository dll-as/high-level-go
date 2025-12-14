# تفاوت بین مقدار صفر (Zero Value) و Nil در Go

در Go، هر متغیر بدون مقدار اولیه یک **Zero Value** می‌گیرد. این مفهوم تضمین می‌کند که متغیرها همیشه مقدار معتبری دارند و ارورهایی مانند **uninitialized variable** رخ نمی‌دهد.

### Zero Value

* Zero value برای **typeهای اصلی (primitive types)** به شرح زیر است:

| Type      | Zero Value     |
| --------- | -------------- |
| int       | 0              |
| float     | 0.0            |
| string    | "" (رشته خالی) |
| bool      | false          |
| pointer   | nil            |
| slice     | nil            |
| map       | nil            |
| channel   | nil            |
| interface | nil            |
| func      | nil            |

> Zero value همیشه یک مقدار **معقول و معتبر** برای آن type است.

### Nil

* `nil` نمایانگر **عدم وجود مقدار** برای reference types است: pointer, slice, map, channel, func, interface.
* کاربرد اصلی nil:

  * بررسی اینکه متغیر هنوز مقداردهی نشده است.
  * جلوگیری از dereference یا panic در pointer, map یا slice.

### تفاوت اصلی

* همه nil values، zero value هستند برای reference types، اما **برای primitive types مانند int، zero value برابر با nil نیست**.
* مثال:

```go
var x int     // zero value = 0
var p *int    // zero value = nil
```

---

## نکات subtle و edge-case

1. **Zero value و nil همیشه یکسان نیستند**

   * Zero value برای int = 0، اما nil فقط برای reference types معتبر است.
   * برخی توسعه‌دهندگان تازه‌کار ممکن است انتظار داشته باشند که slice صفر مقدار با nil برابر باشد، اما رفتار subtle است.

2. **Struct**

   * Struct با zero value برای هر فیلد مقدار اولیه می‌گیرد، حتی اگر struct خودش pointer نباشد.
   * بنابراین یک struct zero value **هیچ‌گاه nil نیست** مگر اینکه خود pointer به struct nil باشد.

3. **Slice و Map**

   * Zero value یک slice یا map برابر nil است.
   * تفاوت عملی بین nil slice و empty slice مهم است و در append یا iteration کاربرد دارد.

---

## مثال عملی کوتاه

```go
package main

import "fmt"

type Person struct {
    Name string
    Age  int
}

func main() {
    // Zero value primitive types
    var n int
    var s string
    var b bool
    fmt.Println(n, s, b) // 0 "" false

    // Struct zero value
    var p Person
    fmt.Printf("%#v\n", p) // Person{Name:"", Age:0}

    // Slice zero value
    var sl []int
    fmt.Println(sl == nil, len(sl), cap(sl)) // true 0 0

    // Map zero value
    var mp map[string]int
    fmt.Println(mp == nil, len(mp)) // true 0

    // Pointer zero value
    var ptr *int
    fmt.Println(ptr == nil) // true
}
```


---

## ارتباط با دیگر مفاهیم

* **Pointer و reference types**: nil برای نشان دادن عدم وجود مقدار
* **Struct**: zero value برای هر فیلد، struct pointer می‌تواند nil باشد
* **Slice و Map**: nil slice/map تفاوت subtle با empty slice/map دارد
* **Memory allocation**: zero value تضمین می‌کند که متغیرها همیشه مقدار معتبر دارند و از undefined behavior جلوگیری می‌کند