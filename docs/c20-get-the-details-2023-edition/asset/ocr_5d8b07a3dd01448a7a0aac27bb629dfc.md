```
```cpp
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
```

With the C++20 extension, you can directly display a time point, such as now (line 24). `std::chrono::floor` rounds the time point down to a day: `std::chrono::sys_days`. This value can be used to initialize the calendar type `std::chrono::year_month_day`. Finally, when I put the value into a `std::chrono::year_month_weekday` calendar type, I get the answer that this specific day is the 3rd Tuesday in October.

Of course, I can also ask a calendar date for its components, such as the current year, month, or day (line 34).

Line 44 is the most interesting one. When I subtract from the current date, using hour resolution, the first of January of the current year, I get the number of hours since the new year. Conversely, when I subtract from the first of January of the next year (line 48) the current date, I get the hours to the new year using hour resolution. Maybe you don’t like hour resolution. Lines 54 and 54 display the values using day resolution.