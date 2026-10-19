# 17.3.7 Header <cfloat> synopsis [cfloat.syn]

```
#define FLT_ROUNDS see below
#define FLT_EVAL_METHOD see below
#define FLT_HAS_SUBNORM see below
#define DBL_HAS_SUBNORM see below
#define LDDBL_HAS_SUBNORM see below
#define FLT_RADIX see below
#define FLT_MANT_DIG see below
#define DBL_MANT_DIG see below
#define LDDBL_MANT_DIG see below
#define FLT_DECIMAL_DIG see below
#define DBL_DECIMAL_DIG see below
#define LDDBL_DECIMAL_DIG see below
#define DECIMAL_DIG see below
#define FLT_DIG see below
#define DBL_DIG see below
#define LDDBL_DIG see below
#define FLT_MIN_EXP see below
#define DBL_MIN_EXP see below
#define LDDBL_MIN_EXP see below
#define FLT_MIN_10_EXP see below
#define DBL_MIN_10_EXP see below
#define LDDBL_MIN_10_EXP see below
#define FLT_MAX_EXP see below
#define DBL_MAX_EXP see below
#define LDDBL_MAX_EXP see below
#define FLT_MAX_10_EXP see below
#define DBL_MAX_10_EXP see below
#define LDDBL_MAX_10_EXP see below
#define FLT_MAX see below
#define DBL_MAX see below
#define LDDBL_MAX see below
#define FLT_EPSILON see below
#define DBL_EPSILON see below
#define LDDBL_EPSILON see below
#define FLT_MIN see below
#define DBL_MIN see below
#define LDDBL_MIN see below
#define FLT_TRUE_MIN see below
#define DBL_TRUE_MIN see below
#define LDDBL_TRUE_MIN see below
```

1 The header <cfloat> defines all macros the same as the C standard library header <float.h>.

SEE ALSO: ISO C 5.2.4.2.2

# 17.4 Integer types [cstdint]

# 17.4.1 General [cstdint.general]

1 The header <cstdint> (17.4.2) supplies integer types having specified widths, and macros that specify limits of integer types.

# 17.4.2 Header <cstdint> synopsis [cstdint.syn]

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