
- `std::chrono::tai_clock`

    International Atomic Time (abbreviated to TAI from its French name) is a very accurate time that does not account for leap seconds. It starts on January 1, 1958. When you format `tai_time`, it is always 19 seconds ahead of `gps_time`.

## Local Pseudo Clock

The `local_t` clock is a clock for intermediate calculations when you have a time point to which you want to add a time zone later. This clock does not have a `now()` method.

If you want the current time of a clock, such as `steady_clock`, you can get it as follows:

```cpp
steady_clock::time_point tp = steady_clock::now();
```

Or directly with auto:

```cpp
auto tp = steady_clock::now();
```

In general, when working with `<chrono>`, you can very often use auto and thus do not have to remember all return types.

You use this, for example, to measure the time of a function call.

```cpp
// https://godbolt.org/z/3MGbYh4d5
#include <iostream>
#include <chrono>
long fib(long n) { return n<2L ? 1L : fib(n-1L)+fib(n-2L); }
int main() {
    using namespace std::chrono;
    auto t0 = steady_clock::now();    // On your marks, get set ...
    auto res = fib(17);                // go!
    auto t1 = steady_clock::now();    // Stop!
    std::cout << "Result: " << res << "\n"; // Output: Result: 2584
    std::cout << "Time: " << nanoseconds(t1-t0).count() << " ns\n";
    // Output: Time: 50727ns (e.g.)
}
```

**Listing 28.32** Simple timing of a function call.

Simply measure the time before and after the call with `now()` and get a `time_point` each time. Between these two, you calculate the difference with `t1-t0` and get a `duration`. For the output, you then convert this duration into a time unit appropriate for the measurement—here, `nanoseconds{...}`. And you're done.

## Converting Times and Leap Seconds

Since C++20, you can use `clock_cast<>` to convert values between different `time_point<>` types. The starting points of the clocks and the leap seconds are taken into account.

For this, there is the `clock_time_conversion<>` trait. Clocks that support `to_utc`, `from_utc`, `sys`, and `from_sys` can then be converted using `clock_cast<>`.

```cpp
// https://godbolt.org/z/bsqP75Kr8
#include <iostream>
#include <chrono>
using namespace std::chrono;
int main() {
    auto tai_now = tai_clock::now();
    std::cout << tai_now << "\n";  // Output: 2023-10-19 01:13:06.2810034
    utc_time utc_now = clock_cast<utc_clock>(tai_now);
    std::cout << utc_now << "\n";  // Output: 2023-10-19 01:12:29.2810034
}
```

**Listing 28.33** Converting time points with “clock_cast”.

At the inception of these clocks, they were already 10 seconds apart. The additional 27 leap seconds since then lead to a discrepancy of 37 seconds, which will continue to change. The `clock_cast` function takes this into account.

The *leap seconds* are determined by an international committee and synchronize Earth’s rotation with atomic time. They are usually added or removed on June 30 or December 31. Since establishment in 1972, there have been a total of 27 inserted leap seconds, the last one on December 31, 2016. There has not been a skipped second so far, but it could happen.

If you want a coarser time unit that you cannot implicitly convert due to loss of precision, then you have two already explained options:

```cpp
// https://godbolt.org/z/rz38hc1cx
auto res = fib(45);
// ...
std::cout << "Time: " << duration_cast<seconds>(t1-t0).count() << " s\n";
// Output: Time: 7s (e.g.)
std::cout << "Time: " << duration<double>{t1-t0}.count() << " s\n";
// Output: Time: 7.35303s (e.g.)
}
```

With `duration_cast<>`, you can accept loss of precision in the output. If you convert to a floating-point duration, the compiler allows the loss of precision—which with floating-point numbers is not actually a loss.

If you don't need a stopwatch but a wall clock, then use `system_clock`. The point in time it describes results from the elapsed duration since the epoch. **Epoch** is the implicit start of this clock. You get the duration since the epoch with `time_since_epoch()`:

```cpp
// https://godbolt.org/z/1xbhhTdEv
#include <iostream>
#include <chrono>
int main() {
    using namespace std::chrono;
    auto tp = time_point_cast<seconds>(system_clock::now());
    auto d = tp.time_since_epoch();
    std::cout << d.count() << " s\n";
    std::cout << duration<double,std::ratio<86400>>(d).count() << " days\n";
}
```

On all systems known to me, the epoch corresponds to 1970-01-01 00:00:00.⁷ `time_since_epoch()` returns a duration here, usually based on seconds, which you can manipulate as usual.

The output is currently as follows for me:

```text
1488837296s
17231.9days
```

⁷ Microsoft plans to set this point to 1.11.1601, which aligns better with other Windows APIs. So be careful with this assumption.

### 28.4.2 Predefined Suffixes for User-Defined Literals

In the standard library, three types of user-defined literals are defined—**user-defined** in the sense that they are defined using operator"". This means that you can write literals of the respective type directly in the source code using the defined suffixes.

> **Custom User-Defined Literals**
> 
> Remember that you are only allowed to write custom user-defined literals that begin with an underscore. All others are reserved for the present and future of the standard library.

I have already mentioned the literals during the discussion of the respective types. However, I want to list them all together here and mention the commonalities.

The predefined user-defined literal suffixes are in **Table 28.10**. Each header defines its literals in its own inline namespace. Also, `std::literals` is an inline namespace:

- `<string>` defines inline namespace `std::literals::string_literals`
- `<complex>` defines inline namespace `std::literals::complex_literals`
- `<chrono>` defines inline namespace `std::literals::chrono_literals`

Because the literals are in their own namespaces, you can fetch them separately. But because they are inline namespaces, you can fetch them all with a single using:

- `using namespace std` makes the suffixes for `string` and `complex` available along with other identifiers of the standard library if you have included the respective headers. `chrono` is in its own namespace.
- `using namespace std::chrono` makes the suffixes from `<chrono>` available along with other identifiers when you have included `<chrono>`.
- `using namespace std::literals` also makes all suffixes available, but other identifiers must still be addressed with `std::`.
- `using namespace std::literals::chrono_literals` makes only the literals defined in `<chrono>` available.
- `using std::literals::string_literals::operator""s` makes only the suffix `"s"` available for `string`, but not the other suffixes, especially not `"s"` for second from `<chrono>`. This also works for all other `operator""s`.

| Suffix | Type | Header |
| --- | --- | --- |
| `""s` | `std::string` | `<string>` |
| `""sv` | `std::string_view` | `<string_view>` |
| `""i` | `std::complex<double>` | `<complex>` |
| `""if` | `std::complex<float>` |  |
| `""il` | `std::complex<long double>` |  |
| `""h` | `std::chrono::hours` | `<chrono>` |
| `""min` | `std::chrono::minutes` |  |
| `""s` | `std::chrono::seconds` |  |
| `""ms` | `std::chrono::milliseconds` |  |
| `""us` | `std::chrono::microseconds` |  |
| `""ns` | `std::chrono::nanoseconds` |  |
| `""d` | `std::chrono::day (since C++20)` |  |
| `""y` | `std::chrono::year (since C++20)` |  |

**Table 28.10** The predefined literals in the standard library for `operator""` suffixes.

What you depend on depends on the situation. In particular, `""s` for string from `<string>` and `""s` for seconds from `<chrono>` can be cleanly separated this way if needed.

You can find plenty of examples, such as in Chapter 4, Listing 4.17 for `<string>`, Chapter 4, Listing 4.39 for `<complex>`, and Listing 28.24 for `<chrono>`. Here is a summary with several different literals:

```cpp
// https://godbolt.org/z/o359TTHMj
#include <iostream>
#include <string>
#include <chrono>
#include <complex>

using std::cout;

int main() {
  {
    using namespace std;
    cout << "string"s << "\n";      // string
    cout << (1.7+3.4i) << "\n";    // complex
  }
  {
    using namespace std::chrono;
    cout << (35ms).count() << "ms\n";  // chrono
  }
  {
    using namespace std::literals;
    cout << (41s).count() << "s\n";   // chrono seconds
    cout << "text"s << "\n";           // string
  }
  {
    using namespace std::chrono;
    cout << (4h).count() << "h\n";     // chrono hours
  }
  {
    using namespace std::literals::chrono_literals;
    cout << (10min).count() << "min\n"; // chrono minutes
  }
  {
    using std::literals::string_literals::operator""s;
    cout << "letters"s << "\n";        // string
  }
}
```

Note that although `""s` exists for string and seconds, you can use both simultaneously because the overloads for `operator""` do not conflict. Text literals like `"text"s` become string, and numeric literals like `41s` become seconds.
