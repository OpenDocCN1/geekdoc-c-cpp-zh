# ISO/IEC 14882:2017(E)

# 23.17.6.5 time_point_nonmember [time.point.nonmember]

```
template <class Clock, common_type_t<Duration>, durationRep2, Period2>>>
constexpr time_point<Clock, common_type_t<Duration1>, durationRep2, Period2>>
operator+(const time_point<Clock, Duration1>&, const durationRep2, Period2>& rhs);
```

+   1. Returns: CT(lhs.time_since_epoch() + rhs), where CT is the type of the return value.

```
template <class Rep1, class Period, class Duration2>
constexpr time_point<Clock, common_type_t<Duration1>, lhs, const_time_point<Clock, Duration2>>
operator+(const time_point<Clock, Duration1>& lhs, const durationRep2>& rhs);
```

+   2. Returns: rhs + lhs;

```
template <class Clock, common_type_t<Duration>, Duration2>
constexpr time_point<Clock, common_type_t<Duration>, durationRep2>>
operator-(const time_point<Clock, Duration1>& lhs, const durationRep2, Period2>& rhs);
```

+   3. Returns: CT(lhs.time_since_epoch() - rhs), where CT is the type of the return value.

```
template <class Clock, common_type_t<Duration>, Duration2>
operator-(const time_point<Clock, common_type_t<Duration>& lhs, const_time_point<Clock, Duration2>& rhs);
```

+   4. Returns: lhs.time_since_epoch() - rhs.time_since_epoch().

# 23.17.6.6 time_point_comparisons [time.point.comparisons]

```
template <class Clock, class Duration2>
constexpr bool operator==(const time_point<Clock, Duration1>& lhs,
                               const_time_point<Clock, Duration2>& rhs);
```

+   1. Returns: lhs.time_since_epoch() == rhs.time_since_epoch().

```
template <class Clock, class Duration2>
constexpr bool operator!=(const time_point<Clock, Duration1>& lhs,
                               const_time_point<Clock, Duration2>& rhs);
```

+   2. Returns: !(lhs == rhs).

```
template <class Clock, class Duration2>
constexpr bool operator<(const time_point<Clock, Duration1>& lhs,
                               const_time_point<Clock, Duration2>& rhs);
```

+   3. Returns: lhs.time_since_epoch() < rhs.time_since_epoch().

```
template <class Clock, class Duration2>
constexpr bool operator<(const time_point<Clock, Duration1>& lhs,
                               const_time_point<Clock, Duration2>& rhs);
```

+   4. Returns: lhs < rhs.

```
template <class Clock, class Duration2>
constexpr bool operator>=(const time_point<Clock, Duration1>& lhs,
                               const_time_point<Clock, Duration2>& rhs);
```

+   5. Returns: lhs > rhs.

```
template <class Clock, class Duration2>
constexpr bool operator>=(const time_point<Clock, Duration1>& lhs,
                               const_time_point<Clock, Duration2>& rhs);
```

+   6. Returns: !(lhs < rhs).