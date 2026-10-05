calendar, for example. In the C++ standard, the Gregorian calendar is referred to as the civil calendar as it is the most widely used calendar.

You will find some type aliases, suffixes, and constants that refer to the civil calendar. The constant November is part of the civil calendar, although of course there is also a November in other calendars.

The class for the civil calendar is year month, and day. Note that year does not denote a duration, but rather the "name" of a year in the calendar sense. However, you can subtract two years from instances of each other to a day.

It is important that an int is not implicitly converted to a year. This prevents careless mistakes. A year is literal with y, so 2024:

```
// codegbolt.org/z/zMojoMeav
#include <chrono>
#include <iostream>
using namespace std::chrono;
int main() {
    year y{2023};
    std::cout << y << "\n";
    month m(October);
    auto result = m + months(3); // 'months', not 'month': 3 months later
    std::cout << result << "\n"; // overflowed to January
    weekday wd = wd + days(4);   // 'days', not 'day': 4 days later
    std::cout << wd << "\n"; // overflowed to Monday
    weekday sun(0); // 0 is Sunday
    weekday sunday(7); // 7 is also Sunday
    std::cout << sun << "\t" << sunday;
    weekday indexed(wd, 4); // unspecified 4th Thursday
    std::cout << indexed << "\n"; // as given by chrono
    // unspecified values
}
```

And when you put the pieces together, you get:

```
// codegbolt.org/z/6z48xvvM
#include <chrono>
#include <iostream>
using namespace std::chrono;
int main() {
    year year{2023};
    year last{2020};
    year month day ymd{year, October, 28};
    std::cout << ymd << "\n"; // in an unspecified year
    month_weekday m_ymwd{ymd, Thursday[4]}; // Output: Nov/Thu[4]
    std::cout << m_ymwd << "\n";
    month day last mdlast(February); // last day of an unspecified February
    year month day last leap(year, mdlast); // Add year
    year_month_day last_nleap(this, year, mdlast); // Add year
    std::cout << leap << "\t" << leap.day() << "\n"; // Output: 2020-02-29
```