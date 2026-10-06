# ISO/IEC 14882:2017(E)

# 23.17.4.2 duration_values [time.traits.duration_values]

```
template <classRep>
struct duration_values {
public:
    static constexpr Rep zero();
    static constexpr Rep min();
    static constexpr Rep max();
}
```

The duration template uses duration_values to construct special values of the duration representation [Rep]. This is done because the representation might be a class with behavior which requires some other implementation to return these special values. In that case, the author of that class should specialize duration_values to return the indicated values.

static constexpr Rep zero();

+   Returns Rep(0). [Note: Rep(0) is specified instead of Rep() because Rep() may have some other meaning, such as an uninitialized value. — end note]

+   Remarks: The value returned should be the additive identity.

static constexpr Rep min();

+   Returns numeric_limits<Rep>::lowest().

+   Remarks: The value returned compare less than or equal to zero.

static constexpr Rep max();

+   Returns numeric_limits<Rep>::max().

+   Remarks: The value returned shall greater than zero.

# 23.17.4.3 Specializations of common_type [time.traits.specializations]

```
template <class Rep, class Period1, class Rep2, class Period2>
struct common_type<chrono::duration<Rep, Period1, Period2>> {
    using type = chrono::duration<common_type<Rep>, Period2>; see below>;
}
```

The duration indicated by this specialization of common_type shall be the greatest common divisor of Period1 and Period2. [Note: This can be computed by forming a ratio of the greatest divisor of Period1::den and the least common multiple of Period1::den and Period2::den — end note]

[Note: The typedefed name type is a synonym for the duration with the largest tick period where both argument values convert to it without performing a division operation. The representation of this is intended to be able to hold any value resulting from this conversion with no truncation, floating-point durations may have round-off errors. — end note]

```
template <class Clock, class Duration1, class Duration2>
struct common_type<chrono::time_point<Clock, Duration1>, chrono::time_point<Clock, Duration2>> {
    using type = chrono::time_point<Clock, common_type<Duration1, Duration2>>;
}
```

The common type of two time_points is a time_point with the same class as the two types and their common duration of them.