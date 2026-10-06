# ISO/IEC 14882:2017(E)

```
constexpr chrono::duration<unspecified,ratio<3600, 1>> operator"h(unsigned long long hours);
constexpr chrono::duration<unspecified,ratio<60>> operator"h(long double hours);
```

Returns: A duration literal representing hours hours.

```
constexpr chrono::minutes operator"min(unsigned long long minutes);
constexpr chrono::duration<unspecified,ratio<60>> operator"min(long double minutes);
```

Returns: A duration literal representing minutes minutes.

```
constexpr chrono::seconds operator"s(unsigned long sec);
constexpr chrono::duration<unspecified>operator"s(long double sec);
```

Returns: A duration literal representing seconds seconds.

> [Note: The same s is for basic_string when there is no conflict, duration suffixes apply to numbers and string literal suffixes apply to character arrays. — end note]

```
constexpr chrono::milliseconds operator"ms(unsigned long long msec);
constexpr chrono::duration<unspecified,milli>operator"ms(long double msec);
```

Returns: A duration literal representing milliseconds milliseconds.

```
constexpr chrono::microseconds operator"us(unsigned long long usec);
constexpr chrono::duration<unspecified,micro>operator"us(long double usec);
```

Returns: A duration literal representing microseconds microseconds.

```
constexpr chrono::nanoseconds operator"ns(unsigned long long nsec);
constexpr chrono::duration<unspecified,nano>operator"ns(long double nsec);
```

Returns: A duration literal representing nanoseconds nanoseconds.

# 23.17.5.9 duration algorithms [time.duration.alg]

```
template <class Rep, class Period>
constexpr duration<Rep, Period> abs(duration<Rep, Period> d);
```

+   1 Remarks: This function does not participate in overload resolution unless numeric_limits<Rep>::is_signed is true.
2 Returns: If d >= d.zero(), return d, otherwise return -d.

# 23.17.6 Class template_time_point [time.point]

```
template <class Clock, class Duration = typename Clock::duration>
class time_point {
public:
    using Clock = Clock;
    using duration = Duration;
    using rep = typename duration::rep;
    using period = typename duration::period;
private:
    duration d; // exposition only

public:
    // 23.17.6.1.
    constexpr time_point(); // has value epoch
    constexpr explicit time_point(const duration& d); // same as time_point() + d
template <class Duration2>
    constexpr time_point(const time_point<Clock, Duration2>& t);
```