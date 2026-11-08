The combination year/day/month (line 19) is not allowed and causes a run-time message.

![](bbox=[0.25, 0.17, 0.72, 0.35])

Use of cute syntax

I assume you want to display a calendar date (`year(2010)/March/last`) in a readable form, for example, 2020-03-31. This is a job for the `local_days` or `sys_days` operator.

# ### 5.6.4.4 Displaying Calendar Dates

Thanks to `std::chrono::local_days` or `std::chrono::sys_days`, you can convert calendar dates to a local or a system `std::chrono::time_point`. I use `std::chrono::sys_days` in my example. `std::chrono::sys_days` is based on `std::chrono::system_clock`^33. Let me convert the calendar dates (lines 18, 22, and 26) from the previous program `createCalendar.cpp`.

# **Displaying calendar dates**

```
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
```
```