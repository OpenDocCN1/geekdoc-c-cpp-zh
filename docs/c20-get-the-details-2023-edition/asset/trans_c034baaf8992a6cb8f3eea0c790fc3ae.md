

```cpp
std::cout << "std::chrono::floor<std::chrono::minutes>(localTime)     "
          << std::chrono::floor<std::chrono::minutes>(localTime) << '\n';

std::cout << "std::chrono::floor<std::chrono::hours>(localTime)       "
          << std::chrono::floor<std::chrono::hours>(localTime) << '\n';

std::cout << "std::chrono::floor<std::chrono::days>(localTime)        "
          << std::chrono::floor<std::chrono::days>(localTime) << '\n';

std::cout << "std::chrono::floor<std::chrono::weeks>(localTime)       "
          << std::chrono::floor<std::chrono::weeks>(localTime) << '\n';

// std::cout << std::chrono::floor<std::chrono::months>(localTime) << '\n'; // ERROR
// std::cout << std::chrono::floor<std::chrono::years>(localTime) << '\n';  // ERROR

std::cout << '\n';

}
```

该程序以不同的精度显示 localTime，从时间长度 `std::chrono::microseconds`（第 18 行）开始，到 `std::chrono::weeks`（第 36 行）结束。奇怪的是，`std::chrono::months` 和 `std::chrono::years` 的时间长度无法显示，但这将在 C++23 中得到修复。

![](img/c60a87adb7f61e2e82071d081bbb389a_418_0.png)

以不同分辨率显示的本地时间

## 5.6.6.1.4 日历日期

下表展示了格式说明符，包括简短描述和示例。完整描述请参阅 cppreference.com/chrono/parse³⁶ 页面。

³⁶https://en.cppreference.com/w/cpp/chrono/parse

### 各种日历类型

| 日历类型 | 描述 | 输出示例 |
|---|---|---|
| `std::chrono::day` | 日 | `09` |
| `std::chrono::month` | 月 | `Aug` |
| `std::chrono::year` | 年 | `2021` |
| `std::chrono::weekday` | 星期几 | `Mon` |
| `std::chrono::weekday_indexed` | 第 n 个星期几 | `Mon[2]` |
| `std::chrono::weekday_last` | 最后一个星期几 | `Mon[last]` |
| `std::chrono::month_day` | 某月中的某日 | `Aug/09` |
| `std::chrono::month_day_last` | 某月最后一天 | `Aug/last` |
| `std::chrono::month_weekday` | 某月第 n 个星期几 | `Aug/Mon[2]` |
| `std::chrono::month_weekday_last` | 某月最后一个星期几 | `Aug/Mon[last]` |
| `std::chrono::year_month` | 某年中的某月 | `2021/Aug` |
| `std::chrono::year_month_day` | 某年某月某日 | `2021-08-09` |
| `std::chrono::year_month_day_last` | 某年某月最后一天 | `2021/Aug/last` |
| `std::chrono::year_month_weekday` | 某年某月第 n 个星期几 | `2021/Aug/Mon[2]` |
| `std::chrono::year_month_weekday_last` | 某年某月最后一个星期几 | `2021/Aug/Mon[last]` |

程序 `createCalendar.cpp` 输出各种日历日期。

## 5.6.6.1.5 格式化

下表展示了格式说明符，包括简短描述和示例。完整描述请参阅 cppreference.com/chrono/parse 页面。

### 日历日期的格式说明符

| 说明符 | 描述 | 示例 |
|---|---|---|
| **日历日期：** |  |  |
| `%c` | 区域设置的日期和时间表示 | `Mon Aug 9 22:58:04 2021` |
| `%x` | 区域设置的日期表示 | `09/08/21` |
| `%F` | 年-月-日 | `2021-08-08` |
| `%D` | 月/日/年 | `09/08/21` |
| **年** |  |  |
| `%Y` | 年 | `2021` |
| `%y` | 不带世纪的年份 | `21` |
| `%C` | 用两位数字表示的世纪 | `20` |
| **月：** |  |  |
| `%b`，或 `%h` | 缩写的月份名称 | `Aug` |
| `%B` | 月份名称 | `August` |
| `%m` | 月 | `08` |
| **周：** |  |  |
| `%W` | 一年中的第几周（01 到 53，周一开始） | `31` |
| `%U` | 一年中的第几周（01 到 53，周日开始） | `31` |
| **星期几：** |  |  |
| `%a` | 缩写的星期几名称 | `Mon` |
| `%A` | 星期几名称 | `Monday` |
| `%w` | 以数字表示的星期几（周日（0）到周六（6）） | `1` |
| `%u` | 以数字表示的星期几（周一（1）到周日（7）） | `1` |
| **日：** |  |  |
| `%e` | 日（必要时带前导空格） | `9` |
| `%d` | 用两位数字表示的日 | `09` |

### 时间的格式说明符

| 说明符 | 描述 | 示例 |
|---|---|---|
| `%c` | 日期和时间表示 | `Mon Aug 9 22:58:04 2021` |
| `%X` | 时间表示 | `22:58:04` |
| `%r` | 12 小时制时间 | `10:58:04 PM` |
| `%T` | 小时:分钟:秒 | `22:58:04` |
| `%R` | 小时:分钟 | `22:58` |
| `%H` | 24 小时制 | `22` |
| `%I` | 12 小时制 | `10` |
| `%p` | AM 或 PM（12 小时制） | `PM` |
| `%M` | 分钟 | `58` |
| `%S` | 秒.亚秒 | `04.453` |

### Chrono 的其他格式说明符

| 说明符 | 描述 | 示例 |
|---|---|---|
| `%Z` | 时区缩写 | `CEST` |
| `%z` | 相对于 UTC 的偏移（小时和分钟） | `+0200` |
| `%j` | 一年中的第几天（从 001 开始） | `221` |
| `%q` | 根据时间长度确定的单位后缀 | `ms` |
| `%n` | 换行符 | `\n` |
| `%t` | 制表符 | `\t` |
| `%%` | % 字符 | `%` |

以下程序使用了时间说明符和日历日期说明符。

### 时间说明符和日历日期说明符的使用

```cpp
// formattedOutputChrono.cpp

#include <chrono>
#include <iostream>
#include <thread>

int main() {

    std::cout << '\n';

    using namespace std::literals;

    auto start = std::chrono::steady_clock::now();
    std::this_thread::sleep_for(33ms);
    auto end = std::chrono::steady_clock::now();
    std::cout << std::format("The job took {} seconds\n", end - start);
    std::cout << std::format("The job took {:%S} seconds\n", end - start);

    std::cout << '\n';

    auto now = std::chrono::system_clock::now();
    std::cout << "now: " << now << '\n';
    std::cout << "Specifier {%c}: " << std::format("{:%c}\n", now);
    std::cout << "Specifier {%x}: " << std::format("{:%x}\n", now);
    std::cout << "Specifier {%X}: " << std::format("{:%X}\n", now);
    std::cout << "Specifier {%D}: " << std::format("{:%D}\n", now);
    std::cout << "Specifier {%d}: " << std::format("{:%d}\n", now);
    std::cout << "Specifier {%y}: " << std::format("{:%y}\n", now);
    std::cout << "Specifier {%Y}: " << std::format("{:%Y}\n", now);
    std::cout << "Specifier {%B}: " << std::format("{:%B}\n", now);
    std::cout << "Specifier {%m}: " << std::format("{:%m}\n", now);
    std::cout << "Specifier {%w}: " << std::format("{:%w}\n", now);
    std::cout << "Specifier {%d}: " << std::format("{:%d}\n", now);
    std::cout << "Specifier {%a}: " << std::format("{:%a}\n", now);
    std::cout << "Specifier {%A}: " << std::format("{:%A}\n", now);
    std::cout << "Specifier {%w}: " << std::format("{:%w}\n", now);
    std::cout << "Specifier {%U}: " << std::format("{:%U}\n", now);
    std::cout << "Specifier {%W}: " << std::format("{:%W}\n", now);
    std::cout << "Specifier {%z}: " << std::format("{:%z}\n", now);

    std::cout << '\n';

}
```

调用 `std::chrono::steady_clock::now()`（第 13 行和第 15 行）确定当前时间。进行测量时应使用 `std::chrono::steady_clock`，因为该时钟是单调的，不能像 `std::chrono::system_clock`（第 21 行）那样被调整。

![](img/c60a87adb7f61e2e82071d081bbb389a_422_0.png)

时间说明符和日历日期说明符的使用

你也可以将格式说明符用于格式化输入。

### 使用 `std::chrono::from_stream` 从输入流读取 chrono 对象

```cpp
// inputChrono.cpp

#include <chrono>
#include <iostream>
#include <string>
#include <sstream>

int main() {

    std::cout << '\n';

    std::chrono::sys_seconds timePoint;
    std::istringstream iStream1{"2021-08-11 21:49:35"};
    std::chrono::from_stream(iStream1, "%x %T", timePoint);
    if (iStream1) std::cout << "timePoint: " << timePoint << '\n';
    else std::cerr << "timePoint: Reading failed\n";

    std::chrono::year_month_day date1;
    std::istringstream iStream2{"11/08/21"};
    std::chrono::from_stream(iStream2, "%x", date1);
    if (iStream2) std::cout << "date1: " << date1 << '\n';
    else std::cerr << "date1: Reading failed\n";

    std::chrono::year_month_day date2;
    std::istringstream iStream3{"11/15/21"};
    std::chrono::from_stream(iStream3, "%x", date2);
    if (iStream3) std::cout << "date2: " << date2 << '\n';
    else std::cerr << "date2: Reading failed\n";

    std::cout << '\n';

}
```

在第 13 行和第 14 行，输入流（`iStream1`）中的数据与格式字符串 `"%x %T"` 匹配。输入流 `iStream2`（第 19 行）及相应格式字符串 `"%x"`（第 20 行）也是如此。相反，不存在第 15 个月，因此第 26 行的解析步骤失败。于是，`iStream3` 的 failbit 被设置。在布尔表达式中使用 `iStream3` 会求值为 false。

