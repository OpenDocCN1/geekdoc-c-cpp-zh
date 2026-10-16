
tp-=d Move **tp** backward: **tp.d-=d**
tp2=tp+d tp2=time_point<Clock>{tp.time_since_epoch()+d} tp2=d+tp
tp2=time_point<Clock>{d+tp.time_since_epoch()} tp2=tp-d tp2=time_point<Clock>{tp.time_since_epoch()-d} d=tp-tp2 d=duration{tp.time_since_epoch()-tp2.time_since_epoch()} tp2=tp.min() tp2=time_point(duration::min()); static; constexpr tp2=tp.max() tp2=time_point(duration::max()); static; constexpr tp==tp2
tp.time_since_epoch()==tp2.time_since_epoch() tp!=tp2 !(tp==tp2)
tp<tp2 tp.time_since_epoch()<tp2.time_since_epoch() tp<=tp2 !(tp2<tp)
tp>tp2 tp2<tp
tp>=tp2 !(tp<tp2)

**tp2=time_point_cast<D>(tp)** Convert the **time_point** tp to **time_point<C,D>**:
**time_point<C,D>(duration_cast<D>(t.time_since_epoch()))** For example:

## Section 35.2.2 time_point 1015

```
void test20() {
  auto tp = steady_clock::now();
  auto d1 = time_point_cast<hours>(tp).time_since_epoch().count()/24; // days since startofepoch

  using days = duration<long,ratio<24*60*60,1>>; // days’ duration
  auto d2 = time_point_cast<days>(tp).time_since_epoch().count(); // days since startofepoch
  if (d1!=d2) cout << "Impossible\n";
}
```

The **time_point** operations that do not access a clock can be **constexpr**, but are not currently guaranteed to be so.

## 35.2.3 Clocks

The **time_point** and **duration** values are ultimately obtained from hardware clocks. In **<chrono>**, the standard library provides basic interfaces for clocks. Class **system_clock** represents “wall clock time” as obtained from a system’s real-time clock:

```
class system_clock {
public:
  using rep = /* implementation-defined signed type*/;
  using period = /* implementation-defined ratio<> */;
  using duration = chrono::duration<rep,period>;
  using time_point = chrono::time_point<system_clock>;
  // …
};
```

All data and function members are **static**. We don’t explicitly deal with clock objects. Instead, we use clock types:

is_steady

## Clock Members (§iso.20.11.7)

Is this clock type steady?
That is, is c.now()<=c.now() for all consecutive calls of now() and is the time between clock ticks constant? static

tp=now() tp is system_clock’s time_point for the time of call; noexcept t=to_time_t(tp) t is the time_t (§43.6) for the time_point tp; noexcept tp=from_time_t(t) tp is the time_point for the time_t t; noexcept

For example:

```
void test3()
{
auto t1 = system_clock::now();
f(x); // do something
auto t2 = system_clock::now();
cout << “f(x) took ” << duration_cast<milliseconds>(t2-t1).count() << ” ms”;
}
```

A system provides three named clocks:

system_clock
steady_clock
high_resolution_clock

## Clock Types (§iso.20.11.7)

The system’s real-time clock; the system’s clock may be reset (jump forward or backward) to match external clocks A clock where time moves steadily forward; that is, time does not go backward and the time between clock ticks is constant A clock with the shortest time increment on a system

These three clocks need not be different; a standard-library clock name may be an alias. We can determine the basic properties of the clocks like this:

```
cout << “min ” << system_clock::duration::min().count() << “, max ” << system_clock::duration::max().count() << “, ” << (treat_as_floating_point<system_clock::duration>::value ? “FP” : “integral”) << ‘\n’;
```

```
cout << (system_clock::is_steady?"steady\n": "not steady\n");
```

When I ran it on one of my systems, this produced:

min -9223372036854775808, max 9223372036854775807, integral not steady

Different systems and different clocks can give different results.

## 35.2.4 Time Traits

Implementations of the chrono facilities depend on a few standard facilities, collectively known as time traits.

The conversion rules for duration and time_point depend on whether their representation is floating-point (so that rounding is acceptable) or integral:

```
template<typename Rep>
```

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

## Section 35.2.4 Time Traits 1017

This makes type an alias for the duration with the largest possible tick period so that both duration arguments will convert to it without requiring a division operation. This implies that common_type<R1,P1,R2,P2>::type can hold any value from duration<R1,R2> and duration<R2,P2> without truncation error. However, floating-point durations may have round-off errors.

```
template<typename Clock, typename Duration1, typename Duration2>
struct common_type<time_point<Clock,Duration1>, time_point<Clock, Duration2>> { using type = time_point<Clock, typename common_type<Duration1, Duration2>::type>;
};
```

In words, to have a common_type, two time_points must have a common clock type. Their common_type is a time_point with the common_type of their durations.

## 35.3 Compile-Time Rational Arithmetic

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

## ratio Arithmetic Operations (siso.20.10.4)

```
z=ratio_add<x,y> z.num=x::num *y::den+y::num*x::den; z.den=x::den*y::den
```

```
z=ratio_subtract<x,y> z.num=x::num*y::den-y::num*x::den; z.den=x::den*y::den
z=ratio_multiply<x,y> z.num=x::num*y::num; z.den=x::den*y::den
z=ratio_divide<x,y> z.num=x::num*y::den; z.den=x::den*y::num
ratio_equal<x,y> x::num==y::num && x::den==y::den
ratio_not_equal<x,y> !ratio_equal<x,y>::value
ratio_less<x,y> x::num*y::den < y::num*x::den
ratio_less_equal<x,y> !ratio_less<y,x>::value
ratio_not_equal<x,y> !ratio_less<y,x>::value
ratio_greater<x,y> ratio_less<y,x>::value
ratio_greater_equal<x,y> !ratio_less<x,y>::value
```

For example:

```
static_assert(ratio_add<ratio<1,3>, ratio<1,6>>::num == 1, “problem: 1/3+1/6 != 1/2”); static_assert(ratio_add<ratio<1,3>, ratio<1,6>>::den == 2, “problem: 1/3+1/6 != 1/2”); static_assert(ratio_multiply<ratio<1,3>, ratio<3,2>>::num == 1, “problem: 1/3*3/2 != 1/2”); static_assert(ratio_multiply<ratio<1,3>, ratio<3,2>>::den == 2, “problem: 1/3*3/2 != 1/2”);
```

Obviously, this is not a convenient way of expressing numbers and arithmetic. In <chrono>, we find the conventional notation (e.g., + and *) for rational arithmetic for time (§35.2). Similarly, to help express unit values, the standard library provides common SI magnitude names:

```
using yocto using zepto using atto using femto using pico using nano using micro
using milli using centi using deci using deca using hecto using kilo
using mega using giga using tera using peta using exa using zetta using yotta =
ratio<1,1000000000000000000000000>; // conditionally supported =
ratio<1,1000000000000000000000>; // conditionally supported =
ratio<1,1000000000000000000>;
= ratio<1,1000000000000000>;
= ratio<1,1000000000000>;
= ratio<1,1000000000>;
= ratio<1,1000000>;
= ratio<1,1000>;
= ratio<1,100>;
= ratio<1,10>;
= ratio<10,1>;
= ratio<100,1>;
= ratio<1000,1>;
= ratio<1000000,1>;
= ratio<1000000000,1>;
= ratio<1000000000000,1>;
= ratio<1000000000000000,1>;
= ratio<1000000000000000000,1>;
= ratio<1000000000000000000000,1>;
= ratio<1000000000000000000000000,1>; // conditionally supported =
ratio<1000000000000000000000000000,1>; // conditionally supported
```

For an example of use, see §35.2.1.
