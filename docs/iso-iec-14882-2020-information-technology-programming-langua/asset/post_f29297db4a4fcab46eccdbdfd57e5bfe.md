
## ISO/IEC 14882:2020(E)

```
static constexpr T quiet_NaN() noexcept;
```

Representation of a quiet “Not a Number”, if available.207

Meaningful for all specializations for which has_quiet_NaN != false. Required in specializations for which is_iec559 != false.

```
static constexpr T signaling_NaN() noexcept;
```

Representation of a signaling “Not a Number”, if available.208

Meaningful for all specializations for which has_signaling_NaN != false. Required in specializations for which is_iec559 != false.

```
static constexpr T denorm_min() noexcept;
```

Minimum positive subnormal value.209

Meaningful for all floating-point types.

In specializations for which has_denorm == false, returns the minimum positive normalized value.

```
static constexpr bool is_iec559;
```

true if and only if the type adheres to ISO/IEC/IEEE 60559.210

Meaningful for all floating-point types.

```
static constexpr bool is_bounded;
```

true if the set of values representable by the type is finite.211

[Note 1: All fundamental types (6.8.2) are bounded. This member would be false for arbitrary precision types. — end note]

Meaningful for all specializations.

```
static constexpr bool is_modulo;
```

true if the type is modulo.212 A type is modulo if, for any operation involving +, -, or * on values of that type whose result would fall outside the range [min(), max()], the value returned differs from the true value by an integer multiple of max() - min() + 1.

[Example 1: is_modulo is false for signed integer types (6.8.2) unless an implementation, as an extension to this document, defines signed integer overflow to wrap. — end example]

Meaningful for all specializations.

```
static constexpr bool traps;
```

true if, at the start of the program, there exists a value of the type that would cause an arithmetic operation using that value to trap.213

Meaningful for all specializations.

```
static constexpr bool tinyness_before;
```

true if tinyness is detected before rounding.214

Meaningful for all floating-point types.

```
static constexpr float_round_style round_style;
```

The rounding style for the type.215

Meaningful for all floating-point types. Specializations for integer types shall return round_toward_zero.

207) Required by LIA-1.

208) Required by LIA-1.

209) Required by LIA-1.

210) ISO/IEC/IEEE 60559:2011 is the same as IEEE 754-2008.

211) Required by LIA-1.

212) Required by LIA-1.

213) Required by LIA-1.

214) Refer to ISO/IEC/IEEE 60559. Required by LIA-1.

215) Equivalent to FLT_ROUNDS. Required by LIA-1.

### 17.3.5.3 numeric_limits specializations [numeric.special]

1 All members shall be provided for all specializations. However, many values are only required to be meaningful under certain conditions (for example, epsilon() is only meaningful if is_integer is false). Any value that is not “meaningful” shall be set to 0 or false.

2 [Example 1:

```
namespace std {
  template<> class numeric_limits<float> {
  public:
    static constexpr bool is_specialized = true;

    static constexpr float min() noexcept { return 1.17549435E-38F; }
    static constexpr float max() noexcept { return 3.40282347E+38F; }
    static constexpr float lowest() noexcept { return -3.40282347E+38F; }

    static constexpr int digits   = 24;
    static constexpr int digits10 = 6;
    static constexpr int max_digits10 = 9;

    static constexpr bool is_signed = true;
    static constexpr bool is_integer = false;
    static constexpr bool is_exact   = false;

    static constexpr int radix = 2;
    static constexpr float epsilon() noexcept     { return 1.19209290E-07F; }
    static constexpr float round_error() noexcept { return 0.5F; }

    static constexpr int min_exponent   = -125;
    static constexpr int min_exponent10 = -37;
    static constexpr int max_exponent   = +128;
    static constexpr int max_exponent10 = +38;

    static constexpr bool has_infinity          = true;
    static constexpr bool has_quiet_NaN         = true;
    static constexpr bool has_signaling_NaN     = true;
    static constexpr float_denorm_style has_denorm = denorm_absent;
    static constexpr bool has_denorm_loss       = false;

    static constexpr float infinity()      noexcept { return value; }
    static constexpr float quiet_NaN()     noexcept { return value; }
    static constexpr float signaling_NaN() noexcept { return value; }
    static constexpr float denorm_min()    noexcept { return min(); }

    static constexpr bool is_iec559  = true;
    static constexpr bool is_bounded = true;
    static constexpr bool is_modulo  = false;
    static constexpr bool traps      = true;
    static constexpr bool tinyness_before = true;

    static constexpr float_round_style round_style = round_to_nearest;
  };
}
```

— end example]

3 The specialization for bool shall be provided as follows:

```
namespace std {
  template<> class numeric_limits<bool> {
  public:
    static constexpr bool is_specialized = true;
    static constexpr bool min() noexcept { return false; }
    static constexpr bool max() noexcept { return true; }
    static constexpr bool lowest() noexcept { return false; }

    static constexpr int digits = 1;
    static constexpr int digits10 = 0;
    static constexpr int max_digits10 = 0;

    static constexpr bool is_signed = false;
    static constexpr bool is_integer = true;
    static constexpr bool is_exact = true;
    static constexpr int radix = 2;
    static constexpr bool epsilon() noexcept { return 0; }
    static constexpr bool round_error() noexcept { return 0; }

    static constexpr int min_exponent = 0;
    static constexpr int min_exponent10 = 0;
    static constexpr int max_exponent = 0;
    static constexpr int max_exponent10 = 0;

    static constexpr bool has_infinity = false;
    static constexpr bool has_quiet_NaN = false;
    static constexpr bool has_signaling_NaN = false;
    static constexpr float_denorm_style has_denorm = denorm_absent;
    static constexpr bool has_denorm_loss = false;
    static constexpr bool infinity() noexcept { return 0; }
    static constexpr bool quiet_NaN() noexcept { return 0; }
    static constexpr bool signaling_NaN() noexcept { return 0; }
    static constexpr bool denorm_min() noexcept { return 0; }

    static constexpr bool is_iec559 = false;
    static constexpr bool is_bounded = true;
    static constexpr bool is_modulo = false;

    static constexpr bool traps = false;
    static constexpr bool tinyness_before = false;
    static constexpr float_round_style round_style = round_toward_zero;
  };
}
```

### 17.3.6 Header \<climits\> synopsis [climits.syn]

```
#define CHAR_BIT see below
#define SCHAR_MIN see below
#define SCHAR_MAX see below
#define UCHAR_MAX see below
#define CHAR_MIN see below
#define CHAR_MAX see below
#define MB_LEN_MAX see below
#define SHRT_MIN see below
#define SHRT_MAX see below
#define USHRT_MAX see below
#define INT_MIN see below
#define INT_MAX see below
#define UINT_MAX see below
#define LONG_MIN see below
#define LONG_MAX see below
#define ULONG_MAX see below
#define LLONG_MIN see below
#define LLONG_MAX see below
#define ULLONG_MAX see below
```

1 The header \<climits\> defines all macros the same as the C standard library header \<limits.h\>.

> [Note 1: The types of the constants defined by macros in \<climits\> are not required to match the types to which the macros refer. — end note]

SEE ALSO: ISO C 5.2.4.2.1

### 17.3.7 Header \<cfloat\> synopsis [cfloat.syn]

```
#define FLT_ROUNDS see below
#define FLT_EVAL_METHOD see below
#define FLT_HAS_SUBNORM see below
#define DBL_HAS_SUBNORM see below
#define LDBL_HAS_SUBNORM see below
#define FLT_RADIX see below
#define FLT_MANT_DIG see below
#define DBL_MANT_DIG see below
#define LDBL_MANT_DIG see below
#define FLT_DECIMAL_DIG see below
#define DBL_DECIMAL_DIG see below
#define LDBL_DECIMAL_DIG see below
#define DECIMAL_DIG see below
#define FLT_DIG see below
#define DBL_DIG see below
#define LDBL_DIG see below
#define FLT_MIN_EXP see below
#define DBL_MIN_EXP see below
#define LDBL_MIN_EXP see below
#define FLT_MIN_10_EXP see below
#define DBL_MIN_10_EXP see below
#define LDBL_MIN_10_EXP see below
#define FLT_MAX_EXP see below
#define DBL_MAX_EXP see below
#define LDBL_MAX_EXP see below
#define FLT_MAX_10_EXP see below
#define DBL_MAX_10_EXP see below
#define LDBL_MAX_10_EXP see below
#define FLT_MAX see below
#define DBL_MAX see below
#define LDBL_MAX see below
#define FLT_EPSILON see below
#define DBL_EPSILON see below
#define LDBL_EPSILON see below
#define FLT_MIN see below
#define DBL_MIN see below
#define LDBL_MIN see below
#define FLT_TRUE_MIN see below
#define DBL_TRUE_MIN see below
#define LDBL_TRUE_MIN see below
```

1 The header \<cfloat\> defines all macros the same as the C standard library header \<float.h\>.

SEE ALSO: ISO C 5.2.4.2.2

### 17.4 Integer types [cstdint]

### 17.4.1 General [cstdint.general]

1 The header \<cstdint\> (17.4.2) supplies integer types having specified widths, and macros that specify limits of integer types.

### 17.4.2 Header \<cstdint\> synopsis [cstdint.syn]

```
namespace std {
    using int8_t      = signed integer type;  // optional
    using int16_t     = signed integer type;  // optional
    using int32_t     = signed integer type;  // optional
    using int64_t     = signed integer type;  // optional

    using int_fast8_t  = signed integer type;
    using int_fast16_t = signed integer type;
    using int_fast32_t = signed integer type;
    using int_fast64_t = signed integer type;
```
