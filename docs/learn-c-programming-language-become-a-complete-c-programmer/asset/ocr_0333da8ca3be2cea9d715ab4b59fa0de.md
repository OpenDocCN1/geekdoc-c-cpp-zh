```
struct treat_as_floating_point : is_floating<Rep> { };
```

A few standard values are provided:

```
duration_values<Rep> (siso.20.11.4.2)
```

```
r=zero() r=Rep(0) ; static; constexpr
r=min() r=numeric_limits<Rep>::lowest(); static; constexpr
r=max() r=numeric_limits<Rep>::max(); static; constexpr
```

The common type of two durations is determined by computing their greatest common denominator (GCD):

```
template<typename Rep1, typename P1, typename Rep2, typename P2>
struct common_type<duration<Rep1,P1>, duration<Rep2, P2>> {
using type = duration<typename common_type<Rep1,Rep2>::type, GCD<P1,P2>> ;
};
```

# Section 35.2.4 Time Traits 1017

This makes type an alias for the duration with the largest possible tick period so that both duration arguments will convert to it without requiring a division operation. This implies that common_type<R1,P1,R2,P2>::type can hold any value from duration<R1,R2> and duration<R2,P2> without truncation error. However, floating-point durations may have round-off errors.

```
template<typename Clock, typename Duration1, typename Duration2>
struct common_type<time_point<Clock,Duration1>, time_point<Clock, Duration2>> { using type = time_point<Clock, typename common_type<Duration1, Duration2>::type>;
};
```

In words, to have a common_type, two time_points must have a common clock type. Their common_type is a time_point with the common_type of their durations.

# 35.3 Compile-Time Rational Arithmetic

In <ratio>, we find class ratio, which provides compile-time rational arithmetic. The standard library uses ratio to provide a compile-time representation of time duration and time points (§35.2):

```
template<intmax_t N, intmax_t D = 1>
struct ratio {
static constexpr intmax_t num;
static constexpr intmax_t den;

using type = ratio<num,den>;
};
```

The basic idea is to encode the numerator and denominator of a rational number as (value) template arguments. The denominator must always be nonzero.

# ratio Arithmetic Operations (siso.20.10.4)

```
z=ratio_add<x,y> z.num=x::num *y::den+y::num*x::den; z.den=x::den*y::den
```