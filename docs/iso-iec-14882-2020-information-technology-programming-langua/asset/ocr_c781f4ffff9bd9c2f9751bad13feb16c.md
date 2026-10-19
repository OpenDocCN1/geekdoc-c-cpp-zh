# 26.4.10 Additional overloads [cmplx.over]

1 The following function templates shall have additional overloads:

+   - arg
+   - norm
+   - conj
+   - proj
+   - imag
+   - real

where norm, conj, imag, and real are constexpr overloads.

2 The additional overloads shall be sufficient to ensure:

+   (2.1) — If the argument has type long double, then it is effectively cast to complex<long double>.
+   (2.2) — Otherwise, if the argument has type double or an integer type, then it is effectively cast to complex<double>.
+   (2.3) — Otherwise, if the argument has type float, then it is effectively cast to complex<float>.

3 Function template pow shall have additional overloads sufficient to ensure, for a call with at least one argument of type complex<T>:

+   (3.1) — If either argument has type complex<long double> or type long double, then both arguments are effectively cast to complex<long double>.
+   (3.2) — Otherwise, if either argument has type complex<double>, double, or an integer type, then both arguments are effectively cast to complex<double>.
+   (3.3) — Otherwise, if either argument has type complex<float> or float, then both arguments are effectively cast to complex<float>.

# 26.4.11 Suffixes for complex number literals [complex.literals]

1 This subclause describes literal suffixes for constructing complex number literals. The suffixes i, il, and if create complex numbers of the types complex<double>, complex<long double>, and complex<float> respectively, with their imaginary part denoted by the given literal number and the real part being zero.

```
constexpr complex<long double> operator""il(long double d);
constexpr complex<long double> operator""il(unsigned long long d);
```

2 Returns: complex<long double>{0.0L, static_cast<long double>(d)}.

```
constexpr complex<double> operator""i(long double d);
constexpr complex<double> operator""i(unsigned long long d);
```

3 Returns: complex<double>{0.0, static_cast<double>(d)}.

```
constexpr complex<float> operator""if(long double d);
constexpr complex<float> operator""if(unsigned long long d);
```

4 Returns: complex<float>{0.0f, static_cast<float>(d)}.

# 26.5 Bit manipulation [bit]

# 26.5.1 General [bit.general]

1 The header <bit> provides components to access, manipulate and process both individual bits and bit sequences.

# 26.5.2 Header <bit> synopsis [bit.syn]

```
namespace std {
// 26.5.3, bit_cast
template<class To, class From>
constexpr To bit_cast(const From& from) noexcept;

// 26.5.4, integral powers of 2
template<class T>
constexpr bool has_single_bit(T x) noexcept;
template<class T>
constexpr T bit_ceil(T x);
template<class T>
constexpr T bit_floor(T x) noexcept;
```