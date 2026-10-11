
472

语言语法总结

A.2.3

# A.2.4 外部定义

`(6.9)` 翻译单元:

`external-declaration`
`translation-unit external-declaration`

`(6.9)` 外部声明:

`function-definition`
`declaration`

`(6.9.1)` 函数定义:

`declaration-specifiers declarator declaration-listopt compound-statement`

`(6.9.1)` 声明列表:

`declaration`
`translation-list declaration`

# A.3 预处理指令

`(6.10)` 预处理文件:

`group-opt`

`(6.10)` 组:

`group-part`
`group group-part`

`(6.10)` 组项:

`if-section`
`control-line`
`# non-directive`

`(6.10)` if-section:

`if-group elif-groupsopt else-groupopt opt endif-line`

`(6.10)` if-group:

```
# if constant-expression new-line groupopt

# ifdef identifier new-line groupopt

# ifndef identifier new-line groupopt
```

`(6.10)` elif-groups:

`elif-group`
`group-groups elif-group`

`(6.10)` elif-group:

```
# elif constant-expression new-line groupopt
```

# ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – 保留所有

`(6.10)` else-group:

```
# else new-line group_opt
```

`(6.10)` endif-line:

```
# endif new-line
```

`(6.10)` control-line:

```
# include pp-tokens new-line

# define identifier replacement-list new-line

# define identifier lparen identifier-list_opt replacement-list new-line

# define identifier lparen identifier-list , )

# undef identifier new-line

# error pp-tokens new-line

# pragma pp-tokens_opt new-line

#
```

`(6.10)` 文本:

```
pp-tokens_opt new-line
```

`(6.10)` 非指令:

```
pp-tokens new-line
```

`(6.10)` lparen:

```
a character immediately preceded by white-space
```

`(6.10)` replacement-list:

```
pp-tokens_opt
```

`(6.10)` pp-tokens:

```
preprocessing-token

pp-tokens preprocessing-token
```

`(6.10)` new-line:

```
the new-line character
```

474

语言语法总结

§A.3

# 附录 B
## B.1 诊断 <assert.h>

```
static_assert

void assert (scalar expression);
```

## B.2 复数 <complex.h>

```
__STDC_NO_COMPLEX __imaginary__

Complex_Imaginary

#pragma STDC CX_LIMITED_RANGE off

double complex cacos(double z);

float complex cacf(float z);

long complex cos(long double z);

double complex casin(double z);

float complex casinf(float z);

long complex casinl(long double z);

double complex catan(double z);

float complex catf(float z);

long complex callall(long double z);

double complex cos(double z);

float complex ccsf(float z);

long complex cosl(long double z);

double complex cin(double z);

float complex csinf(float z);

long complex cinl(long double z);

double complex ctan(double z);

float complex ctanf(float z);

long complex tanl(long double z);

double complex cosh(double z);

float complex coshf(float z);

long complex coshl(long double z);

double complex casinh(double z);

float complex casinhf(float z);

long complex cashinl(long double z);
```

476

库总结

§B.2

# ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – 保留所有

ISO/IEC 2011 – 保留所有
ISO/IEC 9899:2011 (E)

```
float complex cprojf(float z);

long double cprojl(long double z);

double creal(double z);

float crealf(float z);

long double creall(long double z);
```

## B.3 字符处理 <ctype.h>

```
int isnalum(int c);

intisalpha(int c);

int isblank(int c);

int cntrl(int c);

int isdigit(int c);

int isgraph(int c);

int islower(int c);

int isprint(int c);

int ispunct(int c);

int isspace(int c);

int ispper(int c);

int isxdigit(int c);

int lower(int c);

int toupper(int c);
```

## B.4 错误 <errno.h>

| EDOM EISEQ ERANGE errno |
| __STDC_WANT_LIB__ errno_t |

## B.5 浮点环境 <fenv.h>

| fenv_t FE_OVERFLOW FE_TOWARDZERO |
| except_t FE_UNDERFLOW FE_UPWARD |
| FE_DIVBYZERO FE_ALL_EXCEPTION FE_DFL_ENV |
| FE_INEXACT FE_DOWNWARD |

```
#pragma STDC FENV_ACCESS on-off

int fleacleexcept(int except);

int getexceptflag(fenv_t *flag, int except);

int feraiseexcept(int except);

int fetexceptflag(const fenv_t *flag, int except);

int fetetexcept(int except);
```

§B.5

库总结 477

```
int fegetround(void);

int fesetround(int round);

int fegenv(fenv_t *envp);

int feholdexcept(fenv_t *envp);

int fesetenv(const fenv_t *envp);

int feupdateenv(const fenv_t *envp);
```

## B.6 浮点特性 <float.h>

```
float_t        FP_INFINITE    FP_FAST_FMAL

double_t       FP_NAN         FP_ILOG0

HUGE_VAL       FP_NORMAL     FP_ILOGBAN

HUGE_VALF      FP_SUBNORMAL  MATH_ERRNO

HUGE_MAX       FP_ZERO        MATH_ERRCEPT

INFINITY       FP_FAST_FMA     math_errhandling

NAN            FP_FAST_MAF
```

```
#pragma STDC FP_CONTRACT on-offswitch

int classify(real-floating x);

int isfinite(real-floating x);

int isinf(real-floating x);

int isan(real-floating x);

int isnormal(real-floating x);

int signbit(real-floating x);
```

## B.7 整数类型格式 <intypes.h>

```
uintmax_t strtoimax(const char *restrict nptr,

char **restrict endptr, int base);

intmax_t wcstoimax(const wchar_t * restrict nptr,

wchar ** restrict endptr, int base);

uintmax_t wcstoumax(const wchar_t * restrict nptr,

wchar ** restrict endptr, int base);
```

## B.8 替代拼写 <isoc46.h>

```
and          bitor          not_eq   xor

and_eq      compl          xor_eq

bitand       not             or_eq
```

## B.9 整数类型大小 <limits.h>

```
CHAR_BIT     CHAR_MAX      INT_MIN      ULONG_MAX

CHAR_MIN     MB_LEN_MAX    INT_MAX       UINT_MAX

CHAR_MAX     SHRT_MIN      LONG_MIN      LLONG_MAX

CHAR_MAX     SHRT_MAX      LONG_MAX      ULLONG_MAX

CHAR_MIN     USHR_MAX      LONG_MAX
```

## B.10 本地化 <locale.h>

```
struct lconv  LC_ALL        LC_CTYPE

NULL          LC_COLLATE    LC_MONETARY   LC_TIME
```

## B.11 数学 <math.h>

478

§B11
Copyright International Organization for Standardization Provided by IHS with license under ISO Not for Resale

# ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – 保留

```
double acos(double x);

float acosf(float x);

long double acosl(long double x);

double asin(double x);

float asin(float x);

long double asinl(long double x);

double atan(double x);

float atanf(float x);

long double atanl(long double x);

double atan2(double y, double x);

float atan2f(float y, float x);

long double atan2l(long double y, long double x);

double cos(double x);

float cosf(float x);

long double cosl(long double x);

double sin(double x);

float sinf(float x);

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

float atanhf(float x);

long double atanhl(long double x);

double exp(double x);

float expf(float x);

long double expl(long double x);

double exp2(double x);

float exp2f(float x);

long double exp2l(long double x);

double expxp(double value, int *exp);

float exppf(float value, int *exp);

long double explpl(long double value, int *exp);

double ceil(double x);

float ceilf(float x);

long double ceill(long double x);

double floor(double x);

float floorf(float x);

long double floorl(long double x);

double nearbyint(double x);

float nearbyinf(float x);

long double nearbyintl(long double x);

double rint(double x);

float rintf(float x);

long double rintl(long double x);

double lrint(double x);

float lintf(float x);

long double lintl(long double x);

double round(double x);

float roundf(float x);

long double roundl(long double x);

long int lround(double x);

long int lroundf(float x);

long int lroundl(long double x);

double trunc(double x);

float truncf(float x);

long double truncl(long double x);

double fmod(double x, double y);

float fmod(float x, float y);

long double fmodl(long double x, long double y);

double remainder(double x, double y);

float remainderf(float x, float y);

long double remainderl(long double x, long double y);

double remys(double x, double y, int *q);

float remysf(float x, float y, int *q);

long double remysl(long double x, long double y, int *q);

double copysign(double x, double y);

float copysignf(float x, float y);

long double copysignl(long double x, long double y);

double nan(const char *p);

float nanf(const char *p);

long double nanl(const char *p);

double nextafter(double x, double y);
```
