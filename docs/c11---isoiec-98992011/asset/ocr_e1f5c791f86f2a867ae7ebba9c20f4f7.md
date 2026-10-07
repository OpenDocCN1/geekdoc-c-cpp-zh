© ISO/IEC 2011 – All rights reserved ISO/IEC 9899:2011 (E)

```
uintmax_t strtoumax(const char * * restrict nptr,
char ** restrict endptr, int base);
intmax_t wcstoimax(const wchar_t * restrict nptr,
wchar ** restrict endptr, int base);
uintmax_t wcstoumax(const wchar_t * restrict nptr,
wchar ** restrict endptr, int base);
```

# B.8 Alternative spellings <isoc646.h>

```
and          bitor          not_eq   xor
and_eq      compl          xor_eq
bitand       not             or_eq
```

# B.9 Sizes of integer types <limits.h>

```
CHAR_BIT     CHAR_MAX      INT_MIN      ULONG_MAX
CHAR_MIN     MB_LEN_MAX    INT_MAX       LLONG_MIN
CHAR_MAX      SHRT_MIN      UINT_MAX      LLONG_MAX
CHAR_MAX      SHRT_MAX      LONG_MIN      ULLONG_MAX
CHAR_MIN     USHR_MAX      LONG_MAX
```

# B.10 Localization <locale.h>

```
struct lconv  LC_ALL        LC_CTYPE
NULL          LC_COLLATE    LC_MONETARY   LC_TIME
```

char *setlocale(int category, const char *locale);
struct lconv *localeconv(void);

# B.11 Mathematics <math.h>

```
float_t        FP_INFINITE    FP_FAST_FMAL
double_t       FP_NAN         FP_ILOG0
HUGE_VAL       FP_NORMAL     FP_ILOGBAN
HUGE_VALF      FP_SUBNORMAL  MATH_ERRNO
HUGE_MAX       FP_ZERO        MATH_ERRCEPT
INFINITY       FP_FAST_FMA     math_errhandling
NAN            FP_FAST_FMAF
```

```
#pragma STDC FP_CONTRACT on-off-switch
int classify(real-floating x);
int isfinite(real-floating x);
int isinf(real-floating x);
int isan(real-floating x);
int isnormal(real-floating x);
int signbit(real-floating x);
```

§B.11 Library summary 479
Copyright International Organization for Standardization Provided by IHS with license under ISO Not for Resale