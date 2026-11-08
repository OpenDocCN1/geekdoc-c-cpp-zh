
## 日历类型上的操作

| 日历类型 | ++/-- | +/- | 差值 | ==/!= | <=> |
|---|---|---|---|---|---|
| `std::chrono::year_month` |  | 月、年 | 是 | 是 | 是 |
| `std::chrono::year_month_day` |  | 月、年 |  | 是 | 是 |
| `std::chrono::year_month_day_last` |  | 月、年 |  | 是 | 是 |
| `std::chrono::year_month_weekday` |  | 月、年 |  | 是 |  |
| `std::chrono::year_month_weekday_last` |  | 月、年 |  | 是 |  |

自增和自减运算<sup>52</sup>++/-- 支持前缀和后缀版本。加法和减法 +/- 需要 `std::chrono::duration` 类型的对象作为参数。你可以计算具有相同日历类型的两个对象的差值。结果是一个 `std::chrono::duration` 类型的对象。这意味着当你计算两个 `std::chrono::day` 日历类型对象的差值时，会得到一个 `std::chrono::days` 类型的对象。<=> 是新的三路比较运算符。

以下程序使用了日历类型上的操作。

### 日历类型上的操作

```cpp
// calendarOperations.cpp

#include <chrono>
#include <iostream>

int main() {

    std::cout << '\n';

    using std::chrono::Monday;
    using std::chrono::Saturday;

    using std::chrono::March;
    using std::chrono::June;
    using std::chrono::July;

    using std::chrono::days;
    using std::chrono::months;
    using std::chrono::years;

    using std::chrono::last;

    using namespace std::chrono_literals;

    std::cout << std::boolalpha;

    std::cout << "March: " << March << '\n';
    std::cout << "March + months(3): " << March + months(3) << '\n';
    std::cout << "March - months(25): " << March - months(25) << '\n';
    std::cout << "July - June: " << July - June << '\n';
    std::cout << "June < July: " << (June < July) << '\n';

    std::cout << '\n';

    std::cout << "Saturday: " << Saturday << '\n';
    std::cout << "Saturday + days(3): " << Saturday + days(3) << '\n';
    std::cout << "Saturday - days(22): " << Saturday - days(22) << '\n';
    std::cout << "Saturday - Monday: " << Saturday - Monday << '\n';

    std::cout << '\n';

    std::cout << "2021/March: " << 2021y/March << '\n';
    std::cout << "2021/March + years(3): " << 2021y/March + years(3) << '\n';
    std::cout << "2021/March + years(3) - months(35): " << 2021y/March + years(3) - months(35) << '\n';
    std::cout << "2021/July - 2021/June: " << (2021y/July - 2021y/June) << '\n';
    std::cout << "2021/June > 2021y/July: " << (2021y/June > 2021y/July) << '\n';

    std::cout << '\n';

    std::cout << "2021/March/Saturday[last]: " << 2021y/March/Saturday[last] << '\n';
    std::cout << "2021/March/Saturday[last] + months(13) + years(3): "
              << 2021y/March/Saturday[last] + months(13) + years(3) << '\n';
    std::cout << "2021/July/Saturday[last] - months(1) == 2021y/June/Saturday[last]: "
              << (2021y/July/Saturday[last] - months(1) == 2021y/June/Saturday[last])
              << '\n';

    std::cout << '\n';
}
```

<sup>52</sup> https://en.cppreference.com/w/cpp/language/operator_incdec

该程序对 `std::chrono::month`（第27行）、`std::chrono::weekday`（第35行）、`std::chrono::year_month`（第42行）和 `std::chrono::year_month_weekday_last`（第50行）执行操作。

| `std::chrono::weekday` |
|---|
| `std::chrono::Monday` |
| `std::chrono::Tuesday` |
| `std::chrono::Wednesday` |
| `std::chrono::Thursday` |
| `std::chrono::Friday` |
| `std::chrono::Saturday` |
| `std::chrono::Sunday` |

| `std::chrono::month` |
|---|
| `std::chrono::January` |
| `std::chrono::February` |
| `std::chrono::March` |
| `std::chrono::April` |
| `std::chrono::May` |
| `std::chrono::June` |
| `std::chrono::July` |
| `std::chrono::August` |
| `std::chrono::September` |
| `std::chrono::October` |
| `std::chrono::November` |
| `std::chrono::December` |

C++20 为日历类型 `std::chrono::day` 和 `std::chrono::year` 支持两个新字面量：`d` 和 `y`。你可以在**时间时长和字面量**一节中阅读更多细节。

让我开始创建几个日历日期。

### 5.6.4.2 创建日历日期

程序 createCalendar.cpp 展示了创建日历相关日期的各种方式。

```cpp
// createCalendar.cpp

#include <chrono>
#include <iostream>

int main() {

    std::cout << '\n';

    std::cout << yearMonthWeekdayLast << " ";
    std::cout << year_month_weekday_last(2019, month(March), weekday_last(Monday));

    std::cout << "\n\n";

    constexpr auto day_{19};
    std::cout << day_ << " ";
    std::cout << day(19) << '\n';

    constexpr auto month_{1};
    std::cout << month_ << " ";
    std::cout << month(1) << '\n';

    constexpr auto year_{1988};
    std::cout << year_ << " ";
    std::cout << year(1988) << '\n';

    constexpr auto weekday_{weekday(5)};
    std::cout << weekday_ << " ";
    std::cout << weekday(5) << '\n';

    constexpr auto yearMonth{year(1988)/1};
    std::cout << yearMonth << " ";
    std::cout << year_month(year(1988), January) << '\n';

    constexpr auto monthDay{October/22};
    std::cout << monthDay << " ";
    std::cout << month_day(October, day(22)) << '\n';

    constexpr auto monthDayLast{June/last};
    std::cout << monthDayLast << " ";
    std::cout << month_day_last(month(6)) << '\n';

    constexpr auto monthWeekday{February/Monday[3]};
    std::cout << monthWeekday << " ";
    std::cout << month_weekday(February, Monday[3]) << '\n';

    constexpr auto monthWeekdayLast{June/Sunday[last]};
    std::cout << monthWeekdayLast << " ";
    std::cout << month_weekday_last(June, weekday_last(Sunday)) << '\n';

    std::cout << '\n';
}
```

创建日历日期有两种方式。可以使用所谓的可爱语法 `yearMonthDay(year(1940)/month(6...`（第40行），或使用显式类型 `std::chrono::year_month_day(year(1940), June, 26d)`（第42行）。为了避免让你不堪重负，我将把可爱语法的解释推迟到下一节。显式类型很有意思，因为它使用了日期时间字面量 `1940y`、`26d` 和预定义常量 `June`。这是程序中显而易见的部分。

第46行、第50行和第54行提供了创建日历日期的其他方式。

- 第46行：2010年3月的最后一天：`year(2010)/March/last` 或 `year_month_day_last(2010y, month_day_last(month(3)))`
- 第50行：2020年3月的第二个星期四：`year(2020)/March/Thursday[2]` 或 `year_month_weekday(2020y, month(March), Thursday[2])`
- 第54行：2010年3月的最后一个星期一：`year(2010)/March/Monday[last]` 或 `year_month_weekday_last(2010y, month(March), weekday_last(Monday))`

其余日历类型分别表示一天（第60行）、一个月（第64行）或一年（第68行）。你可以将它们组合起来，作为完整指定日历日期的基础构建块，如第46、50或54行所示。

这是程序的输出：

![](img/c60a87adb7f61e2e82071d081bbb389a_392_0.png)

各种日历日期

如约，让我来写写可爱语法。

### 5.6.4.3 可爱语法

可爱语法由重载的除法运算符组成，用于指定日历日期。重载运算符支持日期字面量（例如 `2020y`、`3d`）以及 `std::chrono::month` 常量，如 `std::chrono::January`、`std::chrono::February`、…… `std::chrono::December`。

使用可爱语法可以有以下三种年、月、日的组合。

| 可爱语法 |
|---|
| 年/月/日 |
| 日/月/年 |
| 月/日/年 |

这些组合并非随意选择。它们是全世界使用的组合。不允许任何其他组合。

因此，当你为第一个参数选择年、月或日类型时，其余两个参数的类型不再必要，用数字即可。

```cpp
// cuteSyntax.cpp

#include <chrono>
#include <iostream>

int main() {

    std::cout << '\n';

    constexpr auto yearMonthDay{std::chrono::year(1966)/6/26};
    std::cout << yearMonthDay << '\n';

    constexpr auto dayMonthYear{std::chrono::day(26)/6/1966};
    std::cout << dayMonthYear << '\n';

    constexpr auto monthDayYear{std::chrono::month(6)/26/1966};
    std::cout << monthDayYear << '\n';

    constexpr auto yearDayMonth{std::chrono::year(1966)/std::chrono::day(26)/6};
    std::cout << yearDayMonth << '\n';

    std::cout << '\n';
}
```
