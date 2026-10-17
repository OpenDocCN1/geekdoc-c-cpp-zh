
### B.3 字符处理 `<ctype.h>`

```
int isnalnum(int c);
int isalpha(int c);
int isblank(int c);
int iscntrl(int c);
int isdigit(int c);
int isgraph(int c);
int islower(int c);
int isprint(int c);
int ispunct(int c);
int isspace(int c);
int isupper(int c);
int isxdigit(int c);
int tolower(int c);
int toupper(int c);
```

### B.4 错误 `<errno.h>`

| `EDOM` | `EISEQ` | `ERANGE` | `errno` |
| :--- | :--- | :--- | :--- |
| `__STDC_WANT_LIB_EXT1__` | `errno_t` | | |

### B.5 浮点数环境 `<fenv.h>`

| `fenv_t` | `FE_OVERFLOW` | `FE_TOWARDZERO` |
| :--- | :--- | :--- |
| `fexcept_t` | `FE_UNDERFLOW` | `FE_UPWARD` |
| `FE_DIVZERO` | `FE_ALL_EXCEPT` | `FE_DFL_ENV` |
| `FE_INEXACT` | `FE_DOWNWARD` | |
| `FE_INVALID` | `FE_TONAREST` | |

```
#pragma STDC FENV_ACCESS on-switch
int fecleexcept(int excepts);
int fegetexceptflag(int fecept *flagp, int excepts);
int feraiseexcept(int excepts);
int fesetexceptflag(const fecept *flagp, int excepts);
int fetexcept(int excepts);
```

```
int fegetround(void);
int fesetround(int round);
int fesetenv(fenv_t);
int feholdexcept(fenv_t *envp);
int fesetenv(const fenv_t *envp);
int feupdateenv(fenv_t *envp);
```

### B.6 浮点类型特性 `<float.h>`

| `FLT_ROUNDS` | `DBL_DIG` |
| :--- | :--- |
| `FLT_EVAL_METHOD` | `DBL_MAX` |
| `FLT_HAS_BNORM` | `DBL_MIN` |
| `LDBL_HAS_BNORM` | `DBL_EXP` |
| `FLT_RADIX` | `DBL_EPSON` |
| `FLT_MANT_DIG` | `DBL_MAX` |
| `LDBL_MANT_DIG` | `FLT_MAX` |
| `FLT_DECIMAL_DIG` | `FLT_MIN` |
| `LDBL_DECIMAL_DIG` | `FLT_EXP` |
| `FLT_DIG` | `LDBL_EPSILON` |
| `FLT_MAX` | `LDBL_TRUE_MIN` |

### B.7 整数类型格式转换 `<inttypes.h>`

```
intmax_t
```

| `PRIDN` | `PRIDFAST` | `PRIDMAX` |
| :--- | :--- | :--- |
| `PRII` | `PRIIFAST` | `PRIIMAX` |
| `PRION` | `PRIOLEFAST` | `PRIOMAX` |
| `PRIUN` | `PRIULEFAST` | `PRIUMAX` |
| `PRIXN` | `PRIXFAST` | `PRIXMAX` |
| `SCND` | `SCNDFAST` | `SCNDMAX` |
| `SCN` | `SCONFAST` | `SCNIMAX` |
| `SCNUN` | `SCNULEFAST` | `SCNUMAX` |

```
intmax_t imaxabs(intmax_t j);
intmax_t imaxdiv(intmax_t numer, intmax_t denom);
intmax_t strtomax(const char * restrict nptr, char ** restrict endptr, int base);
intmax_t strtoumax(const char * restrict nptr, char ** restrict endptr, int base);
intmax_t wcstomax(const wchar_t * restrict nptr, wchar_t ** restrict endptr, int base);
intmax_t wcstoumax(const wchar_t * restrict nptr, wchar_t ** restrict endptr, int base);
```

### B.8 备用写法 `<iso64.h>`

```
int64_t
uint64_t
int_fast_t
```

### B.9 整数范围 `<limits.h>`

```
CHAR_BIT
CHAR_MIN
CHAR_MAX
SHRT_MIN
SHRT_MAX
INT_MIN
INT_MAX
LONG_MIN
LONG_MAX
UINT_MIN
UINT_MAX
ULLONG_MIN
ULLONG_MAX
```

### B.10 本地化 `<locale.h>`

```
struct lconv
LC_ALL
LC_CTYPE
LC_NUMERIC
LC_COLLATE
LC_MONETARY
LC_TIME
```

```
char *setlocale(int category, const char *locale);
struct lconv *localeconv(void);
```

### B.11 数学 `<math.h>`

```
float_t FP_INFINITE FP_FAST_FMA
double_t FP_NAN FP_ILOG0
HUGE_VAL FP_NORMAL FP_ILOGBAN
HUGE_VALF FP_SUBNORMAL MATH_ERRNO
HUGE_VALL FP_ZERO MATH_EXCEPT
INFINITY FP_FAST_FMA math_errhandling
NAN FP_FAST_MAF
```

```
#pragma FP_CONTRACT on-switch
int classify(real_float x);
int isfinite(real_float x);
int isinf(real_float x);
int isnan(real_float x);
int isnormal(real_float x);
int signbit(real_float x);
```

```
double acos(double x);
float acos(float x);
long double acos(long double x);
double asin(double x);
float asinf(float x);
long double asin(long double x);
double atan(double x);
float atan(float x);
long double atan1(long double x);
double atan2(double y, double x);
float atan2f(float y, float x);
long double atan2l(long double y, long double x);
double cos(double x);
float cosf(float x);
long double cosl(long double x);
double sin(double x);
float sinh(float x);
long double sinl(long double x);
double tan(double x);
float tanf(float x);
long double tanl(long double x);
double acosh(double x);
float acoshf(float x);
long double acoshl(long double x);
double asinh(double x);
float asinhf(float x);
long double asinhl(long double x);
double atanh(double x);
float atanh(float x);
long double atangl(long double x);
double cos(double x);
float coshf(float x);
long double coshl(long double x);
double sinh(double x);
float sinhf(float x);
long double sinhl(long double x);
double tanh(double x);
float tanhf(float x);
long double tanhl(long double x);
double exp(double x);
float expf(float x);
float exppf(float x);
```

```c
long double expl1(long double x);
double exp2(double x);
float exp2f(float x);
long double exp21(long double x);
double expm1(double x);
float expm1(float x);
long double expm1(long double x);
double frexp(double value, int *exp);
float frexpf(float value, int *exp);
long double frexpl(long double value, int *exp);
int intogb(double x);
int intogbf(float x);
int intogbl(long double x);
double ldexp(double x, int exp);
float ldexpf(float x, int exp);
long double ldexp1(long double x, int exp);
double log(double x);
float logf(float x);
long double log1(long double x);
double log10(double x);
float log10f(float x);
long double log101(long double x);
double log1p(double x);
float log1pf(float x);
long double log1p1(long double x);
double log2(double x);
float log2f(float x);
long double log21(long double x);
double logb(double x);
float logbf(float x);
long double logb1(long double x);
double modf(double value, double *iptr);
float modff(float value, float *iptr);
long double modfl1(long double value, long double *iptr);
double scalbn(double x, int n);
float scalbnf(float x, int n);
long double scalbn1(long double x, int n);
double scalbln(double x, long int n);
float scalblnf(float x, long int n);
long double scalblnl(long double x, long int n);
double cbrt(double x);
float cbtrf(float x);
long double cbrtl(long double x);
double fabs(double x);
float fabsf(float x);
long double fabsl(long double x);
double hypot(double x, double y);
float hypotf(float x, float y);
long double hypotl(long double x, long double y);
double pow(double x, double y);
float powf(float x, float y);
long double powl(long double x, long double y);
double sqrt(double x);
float sqrtf(float x);
long double sqrtl(long double x);
double erf(double x);
float erff(float x);
long double erfl(long double x);
double erfc(double x);
float ercef(float x);
long double ercl(long double x);
double lgamma(double x);
float lgammaf(float x);
long double lgammal(long double x);
double tgamma(double x);
float tgammf(float x);
long double tgammal(long double x);
double ceil(double x);
float ceilf(float x);
long double ceill(long double x);
double floor(double x);
float floorf(float x);
long double floorl(long double x);
double nearbyint(double x);
float nearintf(float x);
long double nearbyintl(long double x);
double rint(double x);
float rintf(float x);
long double rintl(long double x);
long int lrint(double x);
long int lrintf(float x);
long int lrintl(long double x);
long long int llrint(double x);
long long int llrintf(float x);
long long int llrintl(long double x);
double round(double x);
float roundf(float x);
long double round(long double x);
long int round(double x);
long int roundf(float x);
long int llround(long double x);
long long int llround(double x);
long long int llroundf(float x);
long long int llroundl(long double x);
double trunc(double x);
float trunc(float x);
long double trunc(long double x);
```
