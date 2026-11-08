
| Type | Seconds | Suffix |
|---|---|---|
| hours | `ratio<3600,1>` | h |
| minutes | `ratio<60,1>` | min |
| seconds | `ratio<1,1>` | s |
| milliseconds | `ratio<1,1000>` | ms |
| microseconds | `ratio<1,1000000>` | us |
| nanoseconds | `ratio<1,1000000000>` | ns |

**Table 28.6** Various “duration” types of the standard library. (Cont.)

By using `ratio` as the basis of these time units, `<chrono>` allows the automatic conversion of all these time units into each other.

```cpp
// https://godbolt.org/z/qrs63vdzl
#include <chrono>
#include <iostream>
int main() {
    using namespace std::chrono;              // Allow suffixes
    seconds mySecs = 121s;                    // seconds{121}
    std::cout << mySecs.count() << " s\n";    // Output: 121 s
    milliseconds myMillis = mySecs;           // automatically converted
    std::cout << myMillis.count() << " ms\n"; // Output: 121000 ms
    nanoseconds myNanos = mySecs;
    std::cout << myNanos.count() << " ns\n";  // Output: 121000000000 ns
    minutes myMinutesErr = mySecs;             // Error: Conversion with loss
    minutes myMinutes = duration_cast<minutes>(mySecs); // explicit works
    std::cout << myMinutes.count() << "min\n";     // Output: 2min
}
```

**Listing 28.24** Automatic conversion between time units.

As you can see, you then get the converted size in `count()`. So long as the conversion can take place without loss, the transformation works automatically. It would also work implicitly for parameters and returns, as you have already seen in the introductory example with `sleep(_)`.

It is different when information would be lost during the conversion. This would be the case, for example, if you converted `mySecs` to minutes. Then, 121 seconds would become 2 minutes, and the remaining 1 second would be lost. Here, the compiler complains if you want to do it implicitly.

If you know what you're doing, you can force exactly this conversion with `duration_cast<...>`. The result is a rounding toward zero (decimal places are simply truncated). You get other rounding approaches with the `floor`, `round`, and `ceil` functions.

To be clear, `duration_cast<>` is not built-in like `static_cast<>` and its kin, but is a function template that is fully named `std::chrono::duration_cast<>` and is part of `<chrono>`.

All this works because `<chrono>` knows the relationships between different time units and knows whether and how to convert them into each other.

## Do Not Convert Yourself

When you start working with `<chrono>`, let the library handle the conversions. Do not convert yourself, like in the following listing.

```cpp
// https://godbolt.org/z/Y3dnsMYcs
#include <chrono>
#include <iostream>
int main() {
    using namespace std::chrono;
    milliseconds myMs = 4'000ms;
    std::cout << myMs.count()/1000 << "s\n"; // here loses precision
    std::cout << myMs.count()*1000 << "us\n"; // here loses type safety
    std::cout << duration_cast<seconds>(myMs).count() << "s\n"; // explicit
    std::cout << microseconds(myMs).count() << "us\n"; // like implicit
}
```

**Listing 28.25** Do not make your own calculations using `count()`.

It is much less error-prone to let `<chrono>` do the work in one place. The performance is also not worse than if you programmed it yourself by hand.

If the compiler tells you somewhere that it cannot convert something, believe it. Do not bypass its warning by using `count()` and your own calculation. The probability is high that you have made a logical error somewhere.

You can also mix conversions and arithmetic. An expression can contain different units. So long as no information is lost during the conversions, it works seamlessly.

```cpp
// https://godbolt.org/z/VTx4cdzq
#include <chrono>
#include <iostream>
void showDuration(std::chrono::milliseconds dur) {
    std::cout << dur.count() << "ms\n";
}
int main() {
    using namespace std::chrono;
```

would not work with the integer-based seconds because the compiler would protect against loss of precision. If you use a float type, the compiler allows the conversion. An explicit conversion with `duration_cast<>` then is not necessary.

## Calendars, Clocks, and Time Zones

For C++20, the `<chrono>` header has been extensively expanded. While the C++11 version only included durations, time points, and a few clocks, it now includes calendars, leap seconds, time zones, and additional clocks as well as formatting and parsing.

To work with calendars in a type-safe manner, you now have access to the calendar types shown in Table 28.7.

| Type | Meaning |
|---|---|
| `day` | Day of a month |
| `month` | Month of a year |
| `year` | Year of the Gregorian calendar |
| `weekday` | Weekday in the Gregorian calendar |
| `weekday_indexed` | The *n*-th weekday of a month |
| `weekday_last` | Last weekday of a month |
| `month_day` | Specific day in a specific month |
| `month_day_last` | Last day in a month |
| `month_weekday` | The *n*-th weekday in a month |
| `month_weekday_last` | Last weekday in a month |
| `year_month` | Specific month in a year |
| `year_month_day` | Specific day, month, and year |
| `year_month_day_last` | Last day in a specific month and year |
| `year_month_weekday` | The *n*-th weekday in a month and year |
| `year_month_weekday_last` | Last weekday in a month and year |

**Table 28.7** The complete list of calendar types in `chrono::` from C++20.

> **But What Is a Calendar?**
>
> A *calendar* is a collection of dates, each of which has a specific name. In the `<chrono>` sense, `sys_date` is the canonical calendar. A calendar that can be converted to and from `sys_date` can be converted to any other calendar.

## 1. Introduction

程序员是从事程序开发、程序维护的专业人员。他们通常需要具备扎实的编程基础、逻辑思维能力以及解决问题的能力。程序员的工作领域非常广泛，包括软件开发、系统维护、人工智能应用等。总之，程序员在现代社会中扮演着至关重要的角色，推动着技术进步与创新。

随着信息技术的飞速发展，程序员的工作内容不断丰富和拓展，涉及的领域也更加多样。为了更好地理解程序员的职业发展方向，下面将介绍一些主要的研究领域。

| 研究领域 | 主要研究内容 |
| --- | --- |
| 计算机科学与技术 | 研究计算机系统结构、操作系统、编译系统、程序设计语言及计算机应用等核心理论和技术。 |
| 软件工程 | 研究软件开发、维护和管理的方法学，包括需求分析、设计、测试和维护等。 |
| 人工智能 | 研究模拟、延伸和扩展人的智能的理论、方法、技术及应用系统，涵盖机器学习、深度学习、自然语言处理、计算机视觉等。 |
| 数据科学与大数据技术 | 研究数据的采集、存储、处理、分析和可视化等技术。 |

```cpp
year_month_day ymd{this_year, October, day{28}};
std::cout << ymd << "\n";
month_weekday mwd{November, Thursday[4]};    // in an unspecified year
std::cout << mwd << "\n";                    // Output: Nov/Thu[4]
month_day_last mlast{February};               // last day of an unspecified February
year_month_day_last leap{last_year, mlast};   // Add year
year_month_day_last noleap{this_year, mlast}; // Add year
std::cout << leap << "\t" << leap.day() << "\n";    // Output: 2020-02-29 29
std::cout << noleap << "\t" << noleap.day() << "\n"; // Output: 2021-02-28 28
}
```

You can create a date using the `year_month_day` constructor. To prevent dangerous mix-up errors, do not simply pass three integers to the constructor. For example, `year_month_day{10, 11, 12}` should not work: What is the day, what is the month, and what is the year? Instead, you create instances of the types year, month, and day, which you then pass to the constructor:

```cpp
year_month_day ymd{year{2024}, month{11}, day{14}};
```

It looks nicer with the predefined suffixes like `y`, constants like November, and the `/` operator, which combines the individual elements into a date:

```cpp
// https://godbolt.org/z/4s69W7qd3
auto a_date = 2024y/11/14d;
auto b_date = 2024y/11/14;
auto c_date = 14d/11/2024;
auto d_date = November/14/2024;
```

The following orders are possible: month/day/year, day/month/year, and year/month/day. One of the first two elements must be a calendar type—so, for example, not 14/10/2024, because 14/10 would be recognized as integer division. The `/` operator cleverly creates “incomplete” types as intermediate values until you reach the complete date.

You can also generate the last day of a month:

```cpp
auto ymd = last/February/2024; // last day in February 2024: 2024-02-29
```

Isn't that useful? This also makes the somewhat strange-looking “last” and “unspecified” types from Table 28.7 make sense. These are generated as intermediate results when you create a date with the `/` operator. However, they are also useful in further operations, as you will see, because you can even perform calculations with these intermediate results.

```cpp
// https://godbolt.org/z/Md38b9zvf
#include <chrono>
#include <iostream>
#include <format>
```
