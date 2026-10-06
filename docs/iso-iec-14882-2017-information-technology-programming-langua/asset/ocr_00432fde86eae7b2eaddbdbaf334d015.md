# ISO/IEC 14882:2017(E)

positive. In a two's complement representation, this excludes the negative value. — end note

+   2 The static data members num and den shall have the following values, where gcd represents the greatest common divisor of the values of N and D:

```
(2.1) -- shall have the value sign(N) * sign(D) * abs(N) / gcd.
(2.2) -- shall have the value abs(D) / gcd.
```

# 23.16.4 Arithmetic on ratios [ratio.arithmetic]

+   1 Each of the aliases ratio_add, ratio_subtract, ratio_multiply, and ratio_divide denotes the result of an arithmetic computation on two X and Y (in the absence of arithmetic overflow) as specified by Table 5, each alias denotes a ratio<U, V> such that U is the same as ratio<X, Y> and V is the same as ratio<X, Y>::den.
2 If it is not possible to represent U or Y with intmax_t, the program is ill-formed. Otherwise, an implementation should yield correct values of U and V. If it is not possible to represent X or Y with intmax_t, the program is ill-formed unless the implementation yields correct values of D and V.

Table 51 — Expressions to perform arithmetic ratio

| Type | Value of X | Value of Y |
|---|---|--|
| ratio_add(R1, R2) | R1::num * R2::den + R1::den * R2::den |
| | | R1::num * R2::num |
| ratio_subtract(R1, R2) | R1::num * R2::den - R1::den * R2::den |
| | | R1::den * R2::num |
| ratio_multiply(R1, R2) | R1::num * R2::num | R1::den * R2::den |
| ratio_divide(R1, R2) | R1::num * R2::den | R1::den * R2::num |

+   3 Example:

```
static_assert(ratio_add<ratio1, 3, c6>:::num == 1, "1/3/6 == 1/2");
static_assert(ratio_add<ratio1, 3, c6>:::den == 2, "1/3/6 == 1/2");
static_assert(ratio_multiply<ratio1, 3, c3>:::num == 2, "1/3*3/2 == 1/2");

// The following cases may cause the program to be ill-formed under some implementations
static_assert(ratio_add<ratio1, int_MAX, int_MAX>:::num == 2, "1/MAX/MAX == 2");
static_assert(ratio_add<ratio1, int_MAX, int_MAX>:::den == 1, "1/MAX/MAX == 2");
static_assert(ratio_multiply<ratio1, int_MAX, int_MAX>:::num == 1, "1/MAX*MAX == 1/2");
static_assert(ratio_multiply<ratio1, int_MAX, int_MAX>:::den == 2, "1/MAX*MAX == 1/2");
```

— example

# 23.16.5 Comparison of ratios [ratio.comparison]

```
template <class R1, class R2>
struct ratio_equal : bool_constant<R1::num == R2::num && R1::den == R2::den> {};

template <class R1, class R2>
struct ratio_not_equal : bool_constant<!ratio_equal<R1, R2>::value> {};
```

§ ISO/IEC 2017 — All rights reserved 701