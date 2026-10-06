# ISO/IEC 14882:2017(E)

```
template <class R1, class R2> struct ratio_not_equal; 
template <class R1, class R2> struct ratio_less; 
template <class R1, class R2> struct ratio_greater; 
template <class R1, class R2> struct ratio_greater_equal;
```

```
template <class R1, class R2>
inline constexpr bool ratio_equal_v = ratio_not_equal<R1, R2>::value;
template <class R1, class R2>
inline constexpr bool ratio_not_equal_v = ratio_equal<R1, R2>::value;
template <class R1, class R2>
inline constexpr bool ratio_less_v = ratio_less<R1, R2>::value;
template <class R1, class R2>
inline constexpr bool ratio_less_equal_v = ratio_greater<R1, R2>::value;
template <class R1, class R2>
inline constexpr bool ratio_greater_v = ratio_greater<R1, R2>::value;
template <class R1, class R2>
inline constexpr bool ratio_greater_equal_v = ratio_less<R1, R2>::value;
```

```
// 23.16.6, convenience-style typedefs
using ycto = ratio<1, 000'000'000'000'000'000>; // see below
using zepto = ratio<1, 000'000'000'000'000'000>; // see below
using atto = ratio<1, 000'000'000'000'000'000>;
using femto = ratio<1, 1'000'000'000'000'000'000>;
using pico = ratio<1, 1'000'000'000'000'000>;
using nano = ratio<1, 1'000'000'000'000>;
using milli = ratio<1, 1'000'000'00000>;
using centi = ratio<1, 100>;
using deci = ratio<1, 10>;
using hecto = ratio<1, 100>;
using kilo = ratio<1, 1'000>;
using mega = ratio<1, 1'000'000>;
using tera = ratio<1, 1'000'000'000>;
using peta = ratio<1, 1'000'000'000'000>;
using exa = ratio<1, 1'000'000'000'000'000>;
using zeta = ratio<1, 1'000'000'000'000'000'000>; // see below
using yctotta = ratio<1, 1'000'000'000'000'000'000'000>; // see below
```

# 23.16.3 Class ratio template [ratio::ratio]

```
namespace std {
template <class intmax_t N, intmax_t D = 1>
class ratio {
public:
    static constexpr intmax_t num;
    static constexpr intmax_t den;
    using type = ratio<num, den>;
}
```

> If the argument D is zero or not representable by type, the program is ill-formed [Note: These rules ensure that infinite ratios are avoided and that for any negative input, there exists a representable value of its absolute value which is