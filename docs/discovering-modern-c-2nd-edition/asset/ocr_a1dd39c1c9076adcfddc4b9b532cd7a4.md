Therefore, steady_clock is the most convenient for a timer (when the resolution is sufficient).

+   - utc_clock is for Coordinated Universal Time (UTC), since C++20.
+   - tai_clock is for International Atomic Time (TAI), since C++20.
+   - gps_clock is for GPS time, since C++20.
+   - file_clock is for time properties of files, since C++20.
+   - local_t is to represent local time, pseudo-clock since C++20.

People knowing <ctime> might find <chrono> somewhat complicated at the beginning, but we don't need to deal with seconds, milliseconds, microseconds, and nanoseconds in different interfaces. The C++ library offers a uniform interface, and many errors can be detected at the type level —making the programs much safer.

```
C++14
```

User-defined literals were added in C++14 for duration types, e.g.:

Click here to view code image

```
auto dur1= 3h;    // 3 hours
auto dur2= 5.5 min; // 5.5 minutes
auto dur3= 9s;    // 9 seconds
auto dur4= 12.3 ms; // 12.3 milliseconds
auto dur5= 4us;   // 4 microseconds
auto dur6= 2.3 ns; // 2.3 nanoseconds
```

The values are stored either as long or long double depending on whether the number is an integer value. The units are not converted in seconds but represented by compile-time ratio. Thus, the type of dur2 is chrono::duration<long double, std::ratio<60l, 11 >. If we compute with different units, durations are converted to the smallest one, e.g.:

```
auto dur7= 2h + 12min;
```

is stored in minutes.

```
C++20
```

C++20 introduced the type chrono::hh_mm_ss to represent the time of day as a duration since midnight. In addition, an extensive type and function set is provided to deal with time zones. Likewise, many types are now available to provide calendar functionality.