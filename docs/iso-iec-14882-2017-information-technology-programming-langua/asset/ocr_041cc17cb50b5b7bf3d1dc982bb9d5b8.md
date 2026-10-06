# ISO/IEC 14882:2017(E)

```
ToDuration(static_cast<typename ToDuration::rep>
static_cast<CR>(d.count()) * static_cast<CR>(CF::num))
```

```
otherwise, if CF::num == 1 and den == 1, returns
static_cast<CR>(d.count()) * static_cast<CR>(CF::den))
```

```
ToDuration(static_cast<typename ToDuration::rep>
static_cast<CR>(d.count()) * static_cast<CR>(CF::den))
```

otherwise,

> Note: This function does not use any implicit conversions; all conversions are done with static_cast. It avoids multiplications and divisions when it is known at compile time that one or more arguments is unit. Intermediate calculations are carried out in the widest representation and only converted to the destination representation at the final step.

```
template<class ToDuration, class Rep, class Period>
constexpr Period floor(const durationRep, Period& d) = d;
```

Remarks: This function shall not participate in overload resolution unless ToDuration is a specialization

Returns: The greatest t representable in ToDuration for t <= d.

```
template<class ToDuration, class Rep, class Period>
constexpr Period ceil(const durationRep, Period& d) = d;
```

Remarks: This function shall not participate in overload resolution unless ToDuration is a specialization

Returns: The least t representable in ToDuration for t >= d.

```
template<class ToDuration, class Rep, class Period>
constexpr Period round(const durationRep, Period& d) = d;
```

Remarks: This function shall not participate in overload resolution unless ToDuration is a specialization
of duration, and treat_as_floating_point<typename ToDuration::rep> is false.

Returns: The value of ToDuration that is closest to d. if there are two closest values, return the one
of for which t % 2 == 0.

# 23.17.5-8 Suffixes for duration literals [time::duration::ms,]

+   1 This section describes literal suffixes for constructing duration literals. The suffixes h, min, s, us, ns
duration value of the constructing hours, minutes, seconds, milliseconds, microseconds,\and nanoseconds are preserved if they are applied to integral literals.

+   2 If any of these suffixes are applied to a floating-point literal the result is a chrono::literal with
unspecified floating-point representation.

+   3 If any of these suffixes are applied to an integer literal and the resulting chrono::duration value cannot be
represented in the result type because of overflow, the program is ill-formed.

+   4 The following example shows some duration literals.
using namespace std::chrono_literals;
auto constexpr aday=24h;
auto constexpr lesson=45min;
auto constexpr halfhour=0.5h;
-- end example --

©ISO/IEC 2017 - All rights reserved 713