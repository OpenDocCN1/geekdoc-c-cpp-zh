
The combination year/day/month (line 19) is not allowed and causes a run-time message.

![](img/c60a87adb7f61e2e82071d081bbb389a_394_0.png)

### Use of cute syntax

I assume you want to display a calendar date (`year(2010)/March/last`) in a readable form, for example, 2020-03-31. This is a job for the `local_days` or `sys_days` operator.

### 5.6.4.4 Displaying Calendar Dates

Thanks to `std::chrono::local_days` or `std::chrono::sys_days`, you can convert calendar dates to a local or a system `std::chrono::time_point`. I use `std::chrono::sys_days` in my example. `std::chrono::sys_days` is based on `std::chrono::system_clock`^33. Let me convert the calendar dates (lines 18, 22, and 26) from the previous program `createCalendar.cpp`.

**Displaying calendar dates**

```cpp
// sysDays.cpp

#include <chrono>
#include <iostream>

int main() {

    std::cout << '\n';

    using std::chrono::last;

    using std::chrono::year;
    using std::chrono::sys_days;

    using std::chrono::March;
    using std::chrono::February;

    using std::chrono::Monday;
    using std::chrono::Thursday;

    constexpr auto yearMonthDayLast(year(2010)/March/last);
    std::cout << "sys_days(yearMonthDayLast): "
              << sys_days(yearMonthDayLast) << '\n';

    constexpr auto yearMonthWeekday(year(2020)/March/Thursday[2]);
    std::cout << "sys_days(yearMonthWeekday): "
              << sys_days(yearMonthWeekday) << '\n';

    constexpr auto yearMonthWeekdayLast(year(2010)/March/Monday[last]);
    std::cout << "sys_days(yearMonthWeekdayLast): "
              << sys_days(yearMonthWeekdayLast) << '\n';

    std::cout << '\n';

    constexpr auto leapDate(year(2012)/February/last);
    std::cout << "sys_days(leapDate): " << sys_days(leapDate) << '\n';

    constexpr auto noLeapDate(year(2013)/February/last);
    std::cout << "sys_days(noLeapDate): " << sys_days(noLeapDate) << '\n';

    std::cout << '\n';

}
```

The `std::chrono::last` constant (line 21) lets me quickly determine how many days a month has. The output shows that 2012 is a leap year (line 36), but not 2013 (line 39).

![](img/c60a87adb7f61e2e82071d081bbb389a_395_0.png)

Displaying calendar dates

Suppose you have a calendar date like year(2100)/2/29. Your first question may be: Is this date valid?

### 5.6.4.5 Check if a Date is Valid

The various calendar types in C++20 have the function ok. This function returns true if the date is valid.

**Checking if a date is valid**

```cpp
// leapYear.cpp

#include <chrono>
#include <iostream>

int main() {

    std::cout << std::boolalpha << '\n';

    std::cout << "Valid days" << '\n';
    std::chrono::day day31(31);
    std::chrono::day day32 = day31 + std::chrono::days(1);
    std::cout << " day31: " << day31 << '\n';
    std::cout << " day31.ok(): " << day31.ok() << '\n';
    std::cout << " day32: " << day32 << '\n';
    std::cout << " day32.ok(): " << day32.ok() << '\n';

    std::cout << '\n';

    std::cout << "Valid months" << '\n';
    std::chrono::month month1(1);
    std::chrono::month month0(0);
    std::cout << " month1: " << month1 << '\n';
    std::cout << " month1.ok(): " << month1.ok() << '\n';
    std::cout << " month0: " << month0 << '\n';
    std::cout << " month0.ok(): " << month0.ok() << '\n';

    std::cout << '\n';

    std::cout << "Valid years" << '\n';
    std::chrono::year year2020(2020);
    std::chrono::year year32768(-32768);
    std::cout << " year2020: " << year2020 << '\n';
    std::cout << "year2020.ok(): " << year2020.ok() << '\n';
    std::cout << " year32768: " << year32768 << '\n';
    std::cout << "year32768.ok(): " << year32768.ok() << '\n';

    std::cout << '\n';

    std::cout << "Leap Years" << '\n';

    constexpr auto leapYear2016{std::chrono::year(2016)/2/29};
    constexpr auto leapYear2020{std::chrono::year(2020)/2/29};
    constexpr auto leapYear2024{std::chrono::year(2024)/2/29};

    std::cout << " leapYear2016.ok(): " << leapYear2016.ok() << '\n';
    std::cout << " leapYear2020.ok(): " << leapYear2020.ok() << '\n';
    std::cout << " leapYear2024.ok(): " << leapYear2024.ok() << '\n';

    std::cout << '\n';

    std::cout << "No Leap Years" << '\n';

    constexpr auto leapYear2100{std::chrono::year(2100)/2/29};
    constexpr auto leapYear2200{std::chrono::year(2200)/2/29};
    constexpr auto leapYear2300{std::chrono::year(2300)/2/29};

    std::cout << " leapYear2100.ok(): " << leapYear2100.ok() << '\n';
    std::cout << " leapYear2200.ok(): " << leapYear2200.ok() << '\n';
    std::cout << " leapYear2300.ok(): " << leapYear2300.ok() << '\n';

    std::cout << '\n';

    std::cout << "Leap Years" << '\n';

    constexpr auto leapYear2000{std::chrono::year(2000)/2/29};
    constexpr auto leapYear2400{std::chrono::year(2400)/2/29};
    constexpr auto leapYear2800{std::chrono::year(2800)/2/29};

    std::cout << " leapYear2000.ok(): " << leapYear2000.ok() << '\n';
    std::cout << " leapYear2400.ok(): " << leapYear2400.ok() << '\n';
    std::cout << " leapYear2800.ok(): " << leapYear2800.ok() << '\n';

    std::cout << '\n';
}
```

I check in the program if a given day (line 10), a given month (line 21), or a given year (line 31) is valid. The range of a day is [1, 31], of a month [1, 12], and a year [−32767, 32767]. Consequently, the `ok()` calls on the corresponding values return false. Two facts are interesting when I display various values. First, if the value is not valid, the output shows: “is not a valid day”, “is not a valid month”, “is not a valid year”. Second, month values are displayed in string representation.

![](img/c60a87adb7f61e2e82071d081bbb389a_398_0.png)

Check if a date is valid

You can apply the `ok`-call on a calendar date. Now it's pretty easy to check if a specific calendar date is a leap day and, therefore, the corresponding year a leap year. In the worldwide used Gregorian calendar³, the following rules apply:

- Each year that is exactly divisible by 4 is a leap year.
- Except for years that are exactly divisible by 100. They are not leap years.
  - Except for years that are exactly divisible by 400. They are leap years.

Too complicated? The program `leapYears.cpp` exemplifies this rule.

The extended `chrono` library makes it relatively easy to ask for the time duration between calendar dates.

### 5.6.4.6 Query Calendar Dates

Without further ado, the following program `queryCalendarDates.cpp` queries a few calendar dates.

³https://en.wikipedia.org/wiki/Gregorian_calendar

**Query calendar dates**

```cpp
// queryCalendarDates.cpp

#include <chrono>
#include <iostream>

int main() {

    std::cout << '\n';

    using std::chrono::floor;

    using std::chrono::January;

    using std::chrono::years;
    using std::chrono::days;
    using std::chrono::hours;

    using std::chrono::year_month_day;
    using std::chrono::year_month_weekday;

    using std::chrono::sys_days;

    auto now = std::chrono::system_clock::now();
    std::cout << "The current time is: " << now << " UTC\n";
    std::cout << "The current date is: " << floor<days>(now) << '\n';
    std::cout << "The current date is: " << year_month_day(floor<days>(now))
              << '\n';
    std::cout << "The current date is: " << year_month_weekday(floor<days>(now))
              << '\n';

    std::cout << '\n';


    auto currentDate = year_month_day(floor<days>(now));
    auto currentYear = currentDate.year();
    std::cout << "The current year is " << currentYear << '\n';
    auto currentMonth = currentDate.month();
    std::cout << "The current month is " << currentMonth << '\n';
    auto currentDay = currentDate.day();
    std::cout << "The current day is " << currentDay << '\n';

    std::cout << '\n';

    auto hAfter = floor<hours>(now) - sys_days(January/1/currentYear);
    std::cout << "It has been " << hAfter << " since New Year!\n";
    auto nextYear = currentDate.year() + years(1);
    auto nextNewYear = sys_days(January/1/nextYear);
    auto hBefore = sys_days(January/1/nextYear) - floor<hours>(now);
    std::cout << "It is " << hBefore << " before New Year!\n";

    std::cout << '\n';

    std::cout << "It has been " << floor<days>(hAfter) << " since New Year!\n";
    std::cout << "It is " << floor<days>(hBefore) << " before New Year!\n";

    std::cout << '\n';

}
```

With the C++20 extension, you can directly display a time point, such as now (line 24). `std::chrono::floor` rounds the time point down to a day: `std::chrono::sys_days`. This value can be used to initialize the calendar type `std::chrono::year_month_day`. Finally, when I put the value into a `std::chrono::year_month_weekday` calendar type, I get the answer that this specific day is the 3rd Tuesday in October.

Of course, I can also ask a calendar date for its components, such as the current year, month, or day (line 34).

Line 44 is the most interesting one. When I subtract from the current date, using hour resolution, the first of January of the current year, I get the number of hours since the new year. Conversely, when I subtract from the first of January of the next year (line 48) the current date, I get the hours to the new year using hour resolution. Maybe you don’t like hour resolution. Lines 54 and 55 display the values using day resolution.
