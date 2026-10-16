
- than casting to and from values of built-in types); §39.4.3.
- [17] The **time_put** facet can be used for both `<chrono>`- and `<ctime>`-style time; §39.4.4.
- [18] Prefer the character classification functions in which the **locale** is explicit; §39.4.5, §39.5.

This page intentionally left blank.

- Introduction
- Numerical Limits
  - Limit Macros
- Standard Mathematical Functions
- **complex** Numbers
- A Numerical Array: **valarray**
  - Constructors and Assignments; Subscripting; Operations; Slices; **slice_array**; Generalized Slices
- Generalized Numerical Algorithms
  - **accumulate()**; **inner_product()**; **partial_sum()** and **adjacent_difference()**; **iota()**
- Random Numbers
  - Engines; Random Device; Distributions; C-Style Random Numbers
- Advice

## Numerics

> The purpose of computing is insight, not numbers.
> — R. W. Hamming

> ... but for the student, numbers are often the best road to insight.
> — A. Ralston

### 40.1 Introduction

C++ was not designed primarily with numeric computation in mind. However, numeric computation typically occurs in the context of other work – such as database access, networking, instrument control, graphics, simulation, and financial analysis – so C++ becomes an attractive vehicle for computations that are part of a larger system. Furthermore, numeric methods have come a long way from being simple loops over vectors of floating-point numbers. Where more complex data structures are needed as part of a computation, C++’s strengths become relevant. The net effect is that C++ is widely used for scientific, engineering, financial, and other computation involving sophisticated numerics. Consequently, facilities and techniques supporting such computation have emerged. This chapter describes the parts of the standard library that support numerics. I make no attempt to teach numeric methods. Numeric computation is a fascinating topic in its own right. To understand it, you need a good course in numerical methods or at least a good textbook – not just a language manual and tutorial.

In addition to the standard-library facilities described here, Chapter 29 is an extended example of numerical programming: an N-dimensional matrix.

### 40.2 Numerical Limits

To do anything interesting with numbers, we typically need to know something about the general properties of built-in numeric types. To allow the programmer to best take advantage of hardware, these properties are implementation-defined rather than fixed by the rules of the language itself (§6.2.8). For example, what is the largest int? What is the smallest positive float? Is a double rounded or truncated when assigned to a float? How many bits are there in a char?

Answers to such questions are provided by the specializations of the `numeric_limits` template presented in `<limits>`. For example:

```cpp
void f(double d, int i)
{
    char classification[numeric_limits<unsigned char>::max()];
    if (numeric_limits<unsigned char>::digits == numeric_limits<char>::digits) {
        // chars are unsigned
    }
    if (i < numeric_limits<short>::min() || numeric_limits<short>::max() < i) { // i cannot be stored in a short without loss of digits
    }

    if (0 < d && d < numeric_limits<double>::epsilon()) d = 0;

    if (numeric_limits<Quad>::is_specialized) {
        // limits information is available for type Quad
    }
}
```

Each specialization provides the relevant information for its argument type. Thus, the general **numeric_limits** template is simply a notational handle for a set of constants and **constexpr** functions:

```cpp
template<typename T>
class numeric_limits {
public:

    static const bool is_specialized = false; // is information available for numeric_limits<T>?
    // ... uninteresting defaults ...
};
```

The real information is in the specializations. Each implementation of the standard library provides a specialization of **numeric_limits** for each fundamental numeric type (the character types, the integer types, the floating-point types, and **bool**) but not for any other plausible candidates such as **void**, enumerations, or library types (such as `complex<double>`).

For an integral type such as **char**, only a few pieces of information are of interest. Here is `numeric_limits<char>` for an implementation in which a **char** has 8 bits and is signed:

```cpp
template<>
class numeric_limits<char> {
public:

    static const bool is_specialized = true; // yes, we have information
    static const int digits = 7; // number of bits (“binary digits”) excluding sign
    static const bool is_signed = true; // this implementation has char signed
    static const bool is_integer = true; // char is an integral type
    static constexpr char min() noexcept { return -128; } // smallest value
    static constexpr char max() noexcept { return 127; } // largest value
    // lots of declarations not relevant to a char
};
```

Most members of **numeric_limits** are intended to describe floating-point numbers. For example, this describes one possible implementation of **float**:

```cpp
template<>
class numeric_limits<float> {
public:

    static const bool is_specialized = true;

    static const int radix = 2; // base of exponent (in this case, binary)
    static const int digits = 24; // number of radix digits in mantissa
    static const int digits10 = 9; // number of base 10 digits in mantissa
    static const bool is_signed = true;
    static const bool is_integer = false;
    static const bool is_exact = false;

    static constexpr float min() noexcept { return 1.17549435E-38F; } // smallest positive
    static constexpr float max() noexcept { return 3.40282347E+38F; } // largest positive
    static constexpr float lowest() noexcept { return -3.40282347E+38F; } // smallest value

    static constexpr float epsilon() noexcept { return 1.19209290E-07F; }
    static constexpr float round_error() noexcept { return 0.5F; } // maximum rounding error

    static constexpr float infinity() noexcept { return /* some value*/; }
    static constexpr float quiet_NaN() noexcept { return /* some value*/; }
    static constexpr float signaling_NaN() noexcept { return /* some value*/; }
    static constexpr float denorm_min() noexcept { return min(); }

    static const int min_exponent = -125;
    static const int min_exponent10 = -37;
    static const int max_exponent = +128;
    static const int max_exponent10 = +38;

    static const bool has_infinity = true;
    static const bool has_quiet_NaN = true;
    static const bool has_signaling_NaN = true;
    static const float_denorm_style has_denorm = denorm_absent;
    static const bool has_denorm_loss = false;

    static const bool is_iec559 = true; // conforms to IEC-559
    static const bool is_bounded = true;
    static const bool is_modulo = false;
    static const bool traps = true;
    static const bool tinyness_before = true;

    static const float_round_style round_style = round_to_nearest;
};
```

Note that **min()** is the smallest *positive* normalized number and that **epsilon** is the smallest positive floating-point number such that **1+epsilon−1** is larger than **0**.

When defining a scalar type along the lines of the built-in ones, it is a good idea also to provide a suitable specialization of **numeric_limits**. For example, if I write a quadruple-precision type Quad, a user could reasonably expect me to provide `numeric_limits<Quad>`. Conversely, if I use a nonnumeric type, Dumb_ptr, I would expect for `numeric_limits<Dumb_ptr<X>>` to be the primary template that has is_specialized set to false, indicating that no information is available.

We can imagine specializations of `numeric_limits` describing properties of user-defined types that have little to do with floating-point numbers. In such cases, it is usually better to use the general technique for describing properties of a type than to specialize `numeric_limits` with properties not considered in the standard.

### 40.2.1 Limit Macros

From C, C++ inherited macros that describe properties of integers. They are found in `<climits>`:

**Integer Limit Macros** (*iso.diff.library*, abbreviated)

| Macro | Meaning |
|---|---|
| CHAR_BIT | Number of bits in a char (usually 8) |
| CHAR_MIN | Smallest char value (possibly negative) |
| CHAR_MAX | Largest char value (usually 127 if char is signed and 255 if char is unsigned) |
| INT_MIN | Smallest int value |
| LONG_MAX | Largest long value |

Analogously named macros for signed chars, long long, etc., are also provided.

Similarly, `<cfloat>` and `<float.h>` define macros describing properties of floating-point numbers:

**Floating-Point Limit Macros** (*iso.diff.library*, abbreviated)

| Macro | Meaning |
|---|---|
| FLT_MIN | Smallest positive float value (e.g., 1.175494351e-38F) |
| FLT_MAX | Largest float value (e.g., 3.402823466e+38F) |
| FLT_DIG | Number of decimal digits of precision of a float (e.g., 6) |
| FLT_MAX_10_EXP | Largest decimal exponent of a float (e.g., 38) |
| DBL_MIN | Smallest double value |
| DBL_MAX | Largest double value (e.g., 1.7976931348623158e+308) |
| DBL_EPSILON | Smallest double such that 1.0 + DBL_EPSILON != 1.0 |

Analogously named macros for long double are also provided.

### 40.3 Standard Mathematical Functions

In `<cmath>` we find what are commonly called the standard mathematical functions:

**Standard Mathematical Functions**

| Function | Meaning |
|---|---|
| abs(x) | Absolute value |
| ceil(x) | Smallest integer ≥ x |
| floor(x) | Largest integer ≤ x |
