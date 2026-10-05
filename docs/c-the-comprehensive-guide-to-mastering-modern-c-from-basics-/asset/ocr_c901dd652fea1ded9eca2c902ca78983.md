```
std::cout << noleap << "\t" << noleap.day() << "\n"; // Output: 2021-02-28
)
```

You can create a date using the year_month day constructor. To prevent dangerous mix-up errors, not simply pass three integers to the constructor. For example, year_month_day(10, 11, 12) should not work: What is the day, what is the month, and what is the year? Instead, you create instances of the types year, month, and day, which you then pass to the constructor:

```
year_month_day ymd(year(2024), month{11}, day{14});
```

It looks nicer with the predefined suffixes like "y", constants like November, and the / operator , which combines the individual elements into a date:

```
// https://godbolt.org/z/4s697od3
auto a = 2024y/11/14;
auto b = 2024y/11/14;
auto c = 14d/11/2024;
auto d = November/2024;
```

The following orders are possible: month/day/year, day/month/year, and year/month/day. One of the first two elements must be a calendar type—so, for example, not 14/10/2024y, because 14/18 would be recognized as integer division. The / operator cleverly creates "incomplete" types as intermediate values until you reach the complete date.

You can also generate the last day of a month:

```
auto ymd = last/February/2024; // last day in February 2024: 2024-02-29
```

Isn't that useful? This also makes the somewhat-looking "last" and "unspecified" types from Table 28.7 make sense. These are generated as intermediate results when you create a date with the / operator. However, they are also useful in further operations, as you will see, because you can even perform calculations with these intermediate results.

```
// https://godbolt.org/z/Md38bzvf
#include <chrono>
#include <iostream>
```