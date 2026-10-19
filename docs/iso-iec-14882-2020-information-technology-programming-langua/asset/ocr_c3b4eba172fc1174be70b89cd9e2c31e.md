# 27.4.2 duration_values [time.traits.duration.values]

```
template<class Rep>
struct duration_values {
public:
    static constexpr Rep zero() noexcept;
    static constexpr Rep min() noexcept;
    static constexpr Rep max() noexcept;
};
```

1 The duration template uses the duration_values trait to construct special values of the duration’s representation (Rep). This is done because the representation can be a class type with behavior that requires some other implementation to return these special values. In that case, the author of that class type should specialize duration_values to return the indicated values.

```
static constexpr Rep zero() noexcept;
```

2 Returns: Rep(0).

[Note 1: Rep(0) is specified instead of Rep() because Rep() can have some other meaning, such as an uninitialized value. — end note]

3 Remarks: The value returned shall be the additive identity.

```
static constexpr Rep min() noexcept;
```

4 Returns: numeric_limits<Rep>::lowest().

5 Remarks: The value returned shall compare less than or equal to zero().

```
static constexpr Rep max() noexcept;
```

6 Returns: numeric_limits<Rep>::max().

7 Remarks: The value returned shall compare greater than zero().

# 27.4.3 Specializations of common_type [time.traits.specializations]

```
template<class Rep1, class Period1, class Rep2, class Period2>
struct common_type<chrono::duration<Rep1, Period1>, chrono::duration<Rep2, Period2>> {
    using type = chrono::duration<common_type_t<Rep1, Rep2>, see below>;
};
```

1 The period of the duration indicated by this specialization of common_type is the greatest common divisor of Period1 and Period2.

[Note 1: This can be computed by forming a ratio of the greatest common divisor of Period1::num and Period2::num and the least common multiple of Period1::den and Period2::den. — end note]

2 [Note 2: The typedef name type is a synonym for the duration with the largest tick period possible where both duration arguments will convert to it without requiring a division operation. The representation of this type is intended to be able to hold any value resulting from this conversion with no truncation error, although floating-point durations can have round-off errors. — end note]

```
template<class Clock, class Duration1, class Duration2>
struct common_type<chrono::time_point<Clock, Duration1>, chrono::time_point<Clock, Duration2>> {
    using type = chrono::time_point<Clock, common_type_t<Duration1, Duration2>>;
};
```

3 The common type of two time_point types is a time_point with the same clock as the two types and the common type of their two durations.

# 27.4.4 Class template is_clock [time.traits.is.clock]

```
template<class T> struct is_clock;
```

1 is_clock is a Cpp17UnaryTypeTrait (20.15.2) with a base characteristic of true_type if T meets the Cpp17Clock requirements (27.3), otherwise false_type. For the purposes of the specification of this trait, the extent to which an implementation determines that a type cannot meet the Cpp17Clock requirements is unspecified, except that as a minimum a type T shall not qualify as a Cpp17Clock unless it meets all of the following conditions: