
### 描述

`remquo` 函数与 `remainder` 函数计算相同的余数。在 `quo` 指向的对象中存储模 2 等于 `x/y` 商值的整数 `n`，其中 `n` 是大于或等于 0 的实现定义的整数。

## 返回

`remquo` 函数返回 `x`。如果 `y` 为 0，`quo` 指向的对象的值未指定。

注意 没有十进制浮点的 `remquo` 版本。当 `y ≠ 0` 时，无论舍入模式如何，定义 `r = x - ny`，其中 `n` 是满足 `|n - x/y| ≤ |y|/2` 的整数。如果 `r = 0`，其符号为 `x`。此定义适用于所有实现。

## 7.12.12 符号函数

### 7.12.12.1 The copesign 函数

### 概要

```
#include <math.h>

double copysign(double x, double y);

float copysign(float x, float y);

long double copysign(long double x, long double y);

#ifdef _STDC_IEC_60559_DP

_Decimal32 copysign32(_Decimal32 x, _Decimal32 y);

_Decimal64 copysign64(_Decimal64 x, _Decimal64 y);

_Decimal128 copysign128(_Decimal128 x, _Decimal128 y);

#endif
```

### 描述

`copesign` 函数产生具有 `x` 的绝对值和 `y` 的符号的值。如果 `x` 或 `y` 是无符号值，结果的符号（如果有）取决于实现。在表示符号零但在算术操作中一致处理负零实现中，`copesign` 函数应将零视为正。

## 返回

`copesign` 函数返回具有 `x` 的绝对值和 `y` 的符号的值。

## 7.12.12.2 The nan 函数

### 概要

```
#include <math.h>

double nan(const char *tagp);

float nanf(const char *tagp);

long nanl(const char *tagp);

#ifdef _STDC_IEC_60559_DP

_Decimal32 nan32(const char *tagp);

_Decimal64 nan64(const char *tagp);

_Decimal128 nan128(const char *tagp);

#endif
```

### 描述

`nan`、`nanf` 和 `nanl` 函数按照以下规则将字符串转换为 `tagp`：`nan("n-char-sequence")` 等于 `strtod("NAN(n-char-sequence)", nullptr)`；`nan("")` 等于 `strtod("NAN", nullptr)`。如果 `tagp` 不指向空字符串或字符序列，则等于 `strtod("NAN", nullptr)`。对 `nan` 和 `nanl` 的调用等于 `strtof` 和 `strtol` 的对应调用。

## 返回

`nan` 函数返回静默 NAN，内容通过 `tagp` 指明。如果实现不支持静默 NaN，函数返回。

前向引用：`strtof`, `strtod` 和 `strtol` (7.24.2.6)。

## 7.12.12.3 The nextafter 函数

### 概要

```
#include <math.h>

double nextafter(double x, double y);

float nextafter(float x, float y);

long double nextafter(long double x, long double y);

#ifdef _STDC_IEC_60559_DP

_Decimal32 nextafter(_Decimal32 x, _Decimal32 y);

_Decimal64 nextafter(_Decimal64 x, _Decimal64 y);

_Decimal128 nextafter128(_Decimal128 x, _Decimal128 y);

#endif
```

### 描述

`nextafter` 函数在函数的返回类型中，确定向 `y` 方向 `x` 之后的下一个可表示值，其中 `x` 和 `y` 首先转换为函数的返回类型。如果 `x` 等于 `y`，`nextafter` 函数返回 `y`。

如果 `x` 的绝对值是类型中最大的有限值且结果不在类型内或在类型内可，则发生域错误。如果 `x != y`，每一个非规格化或零结果都会发生域错误。

## 返回

`nextafter` 函数返回指定格式下向 `y` 方向 `x` 之后的下一个可表示表示值。

## 7.12.12.4 The nextward 函数

### 概要

```
#include <math.h>

double nextward(double x, long double y);

float nextward(float x, float y);

long double nextward(long double x, long double y);

#ifdef _STDC_IEC_60559_DP

_Decimal32 nextward32(_Decimal32 x, _Decimal32 y);

_Decimal64 nextward64(_Decimal64 x, _Decimal64 y);

_Decimal128 nextward128(_Decimal128 x, _Decimal128 y);

#endif
```

### 描述

`nextward` 函数等于 `nextafter` 函数，但第二个参数类型为 `long double`、`_Decimal128`，且当 `x` 等于 `y` 时函数返回函数的返回类型。

## 返回

`nextward` 函数返回指定格式下向 `y` 方向 `x` 之后的下一个可表示值。

## 7.12.12.5 The nextup 函数

### 概要

```
#include <math.h>

double nextup(double x);

float nextup(float x);

long double nextup(long double x);

#ifdef _STDC_IEC_60559_DP

_Decimal32 nextup32(_Decimal32 x);

_Decimal64 nextup64(_Decimal64 x);

_Decimal128 nextup128(_Decimal128 x);

#endif
```

### 描述

`nextup` 函数在函数的返回类型中，确定大于 `x` 的下一个可表示值。如果 `x` 是类型中的负值，如果该类型有符号零则 `nextup(x)` 为 `-0`，否则为 `0`。如果 `x` 为零，`nextup(x)` 为正数。

# ISO/IEC 9899:2024(en)

`x` 类型中的幅值。如果 `x` 是该类型中最大幅值的（有限或无限）正数，则 `nextup(x)` 为 `x`。

# Returns

`nextup` 函数返回指定类型中大于 `x` 的下一个可表示值。

## 7.12.12.6 nextdown 函数

# 语法概要

```
#include <math.h>

double nextdown(double x);

float nextdownf(float x);

long nextdownl(long double x);

#ifdef _STDC_IEC_60559_DP

_Decimal32 nextdownd2(_Decimal32 *x);

_Decimal64 nextdownd4(_Decimal64 *x);

_Decimal128 nextdownl28(_Decimal128 *x);

#endif
```

# 描述

`nextdown` 函数确定返回类型中小于 `x` 的下一个可表示值。如果 `x` 是该类型中最小幅值的正数，且该类型具有符号零，则 `nextdown(x)` 为 `+0`，否则为 `0`。如果 `x` 为零，则 `nextdown(x)` 为该类型中最小幅值的负值。如果 `x` 是该类型中最大幅值的（有限或无限）负数，则 `nextdown(x)` 为 `x`。

# Returns

`nextdown` 函数返回指定类型中小于 `x` 的下一个可表示值。

## 7.12.12.7 canonicalize 函数

# 语法概要

```
#include <math.h>

int canonicalize(double *cx, const double x);

int canonicalizef(float *cx, const float x);

int canonicalizel(long double *cx, const long double x);

#ifdef _STDC_IEC_60559_DP

int canonicalized2(_Decimal32 *cx, const _Decimal32 *x);

int canonicalized4(_Decimal64 *cx, const _Decimal64 *x);

int canonicalizel28(_Decimal128 *cx, const _Decimal128 *x);

#endif
```

# 描述

`canonicalize` 函数尝试将参数 `x` 所指向的对象中的浮点表示转换为规范版本，并到指定类型的临时对象中，并将结果存储在参数 `cx` 所指向的对象中。如果输入 `*x` 是一个信号 NaN，则 `canonicalize` 函数旨在存储一个规范静默 NaN。

# Returns

如果在 `cx` 所指向的对象中存储了规范值，则 `canonicalize` 函数返回零。否则返回非零值。

## 7.12.13 最大、最小和正差函数

### 7.12.13.1 fdimmax 函数

> 参数 `x` 和 `cx` 可以指向同一个对象。

# 语法概要

```
#include <math.h>

double fdim(double x, double y);

float fdfmf(float x, float y);

long double dfdml(long double x, long double y);

#ifdef _STDC_IEC_60559_DP

_Decimal32 fdim32(_Decimal32 x, _Decimal32 y);

_Decimal64 fdim64(_Decimal64 x, _Decimal64 y);

_Decimal128 fdim128(_Decimal128 x, _Decimal128 y);

#endif
```

# 描述

`fdim` 函数确定其参数之间的正差：

```
x - y  if x > y

+0     if x ≤ y
```

对于某些有限参数会发生范围错误。

# Returns

`fdim` 函数返回正差值。

## 7.12.13.2 fmax 函数

# 语法概要

```
#include <math.h>

double fmax(double x, double y);

float fmax(float x, float y);

long double dfmax(long double x, long double y);

#ifdef _STDC_IEC_60559_DP

_Decimal32 fmax32(_Decimal32 x, _Decimal32 y);

_Decimal64 fmax64(_Decimal64 x, _Decimal64 y);

_Decimal128 fmax28(_Decimal128 x, _Decimal128 y);

#endif
```

# 描述

`fmax` 函数确定其参数的最大数值值。

# Returns

`fmax` 函数返回最大的数值值。

## 7.12.13.3 fmin 函数

# 语法概要

```
#include <math.h>

double fmin(double x, double y);

float fmin(float x, float y);

long double dfmin(long double x, long double y);

#ifdef _STDC_IEC_60559_DP

_Decimal32 fmin32(_Decimal32 x, _Decimal32 y);

_Decimal64 fmin64(_Decimal64 x, _Decimal64 y);

_Decimal128 fmin28(_Decimal128 x, _Decimal128 y);

#endif
```

> 静默 NaN 参数的处理方式为：如果一个参数是 NaN 而另一个不是，则 `fmax` 函数返回数值值。

# 描述

`fmin` 函数确定其参数的最小数值值。

# Returns

`fmin` 函数返回最小的数值值。

注意 `fmax` 和 `fmin` 函数与 `fmaximum_num` 和 `fminimum_num` ，后者在符号零的选择上可能不同。

## 7.12.13.4 fmaximum 函数

# 语法概要

```
#include <math.h>

double fmaximum(double x, double y);

float fmaximum(float x, float y);

long double fmaximum(long double x, long double y);

#ifdef _STDC_IEC_60559_DP

_Decimal32 fmaximum32(_Decimal32 x, _Decimal32 y);

_Decimal64 fmaximum64(_Decimal64 x, _Decimal64 y);

_Decimal128 fmaximum28(_Decimal128 x, _Decimal128 y);

#endif
```

# 描述

`fmaximum` 函数确定其参数的最大值。对于这些函数，`+0` 大于 `-0`。这些函数与 `fmaximum_num` 仅在对 NaN 参数的处理上不同（见 F10.10.4）。

# Returns

`fmaximum` 函数返回参数的最大值。

## 7.12.13.5 fminimum 函数

# 语法概要

```
#include <math.h>

double fminimum(double x, double y);

float fminimum(float x, float y);

long double fminimum(long double x, long double y);

#ifdef _STDC_IEC_60559_DP

_Decimal32 fminimum32(_Decimal32 x, _Decimal32 y);

_Decimal64 fminimum64(_Decimal64 x, _Decimal64 y);

_Decimal128 fminimum28(_Decimal128 x, _Decimal128 y);

#endif
```

# 描述

`fminimum` 函数确定其参数的最小值。对于这些函数，`-0` 小于 `+0`。这些函数与 `fminimum_num` 仅在对 NaN 参数的处理上不同（见 F10.10.4）。

# Returns

`fminimum` 函数返回参数的最小值。

## 7.12.13.6 fmaximum_mag 函数

# 语法概要

```
#include <math.h>

double fmaximum_mag(double x, double y);

float fmaximum_mag(float x, float y);

long double fmaximum_mag(long double x, long double y);

#ifdef _STDC_IEC_60559_DP

_Decimal32 fmaximum_magd32(_Decimal32 x, _Decimal32 y);

_Decimal64 fmaximum_magd64(_Decimal64 x, _Decimal64 y);

_Decimal128 fmaximum_magd28(_Decimal128 x, _Decimal128 y);

#endif
```

> `fmin` 函数在处理静默 NaN 时类似于 `fmax` 函数。

# 描述

`fmaximum_mag` 函数确定幅值最大的参数：如果 `|x| > |y|`，则返回 `x`；如果 `|y| > |x|`，则返回 `y`；否则返回 `x`。这些函数与 `fmaximum_mag_num` 仅在对 NaN 参数的处理上不同（见 F10.10.4, F10.10.5）。

# Returns

`fmaximum_mag` 函数返回幅值最大的参数。

## 7.12.13.7 fminimum_mag 函数

# 语法概要

```
#include <math.h>

double fminimum_mag(double x, double y);

float fminimum_mag(float x, float y);

long double fminimum_mag(long double x, long double y);

#ifdef _STDC_IEC_60559_DP

_Decimal32 fminimum_magd32(_Decimal32 x, _Decimal32 y);

_Decimal64 fminimum_magd64(_Decimal64 x, _Decimal64 y);

_Decimal128 fminimum_magd28(_Decimal128 x, _Decimal128 y);

#endif
```
