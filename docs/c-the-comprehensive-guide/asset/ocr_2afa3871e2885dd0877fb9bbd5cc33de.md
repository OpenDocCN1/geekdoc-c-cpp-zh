# Time Points: “time_point”

While duration represents some relative duration, `time_point` is absolute. For `<chrono>`, a `time_point` is a firmly connected pair of a duration and a reference point.

For example, the reference point could be January 1, 2000, and the duration 6,518 days; then the pair of these two values would name the time point as November 5, 2017.

Specifically in C++, for example, 10000s is 10,000 seconds, while

```
```cpp
time_point<system_clock, seconds> tp{10000s};
```
```

is 10,000 seconds after 1/1/1970, which is 1970-01-01 02:46:40 UTC (that January 1, 1970, is the start of `system_clock` is not a must, so be careful here).

Since C++20, there are aliases for `time_point<system_clock, seconds>` such as `sys_time<seconds>` and `sys_seconds`. The `sys_days` alias has also been added.

However, `time_point` and `duration` work well together. You can take the difference between two time points and get a duration—as in C++:

```
```cpp
// https://godbolt.org/z/q1znGWb85
#include <iostream>
#include <chrono>
int main() {
    using namespace std::chrono;
    time_point<system_clock, seconds> t1{10000s};
    time_point<system_clock, seconds> t2{50000s};
    auto dur = t2 - t1;
    std::cout << duration_cast<hours>(dur).count() << " h"; // Output: 11h
}
```
```

The compiler does not allow you to add two time points, as that would not make sense. However, you can add duration to a time_point and so on.

Every time_point is bound to a time unit—in this example, seconds. As with duration, the compiler allows implicit conversions to more precise time_point types but prevents those to less precise ones. With a time_point_cast, you can always force a conversion.

To convert a time_point to a duration, use the time_since_epoch() method.

# Clocks

A clock is a triplet of

+   - a duration in the form of a duration type,
+   - a point in time in the form of a time_point type, and
+   - a function to get the current time.