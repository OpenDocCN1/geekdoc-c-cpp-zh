
### 7.12.9.2 floor 函数

Synopsis

```
#include <math.h>
double floor(double x);
float floorff(float x);
long double floorl(long double x);
```

Description

`floor` 函数计算大于 `x` 的最大整数。

Returns

`floor` 函数返回 `$[x]$`（浮点格式）。

### 7.12.9.3 nearbyint 函数

Synopsis

```
#include <math.h>
double nearbyint(double x);
float nearbyintf(float x);
long double nearbyintl(long double x);
```

Description

`nearbyint` 函数将参数舍入为浮点格式的整数值，使用当前的舍入方向且不引发“精确”异常。

Returns

`nearbyint` 函数返回整数值。

### 7.12.9.4 rint 函数

Synopsis

```
#include <math.h>
double rint(double x);
float rintf(float x);
long double rintl(long double x);
```

Description

`rint` 函数与 `nearbyint` 函数（7.12.9.3）的区别仅在于，如果结果与参数不同，`rint` 函数可能会引发“精确”异常。

Returns

`rint` 函数返回舍入的整数值。

### 7.12.9.5 rint 和 llrint 函数

Synopsis

```
#include <math.h>
long int lrint(double x);
long int rintf(float x);
long int rintl(long double x);
long long llrint(double x);
long long llrintf(float x);
long long llintl(long double x);
```

Description

`rint` 和 `llrint` 函数将参数舍入到最近的整数值，根据当前的舍入方向。如果舍入后的值超出返回类型的范围，则数值结果未定义且可能发生域错误或范围错误。

Returns

`lrint` 和 `llrint` 函数返回舍入的整数值。

## 7.12.9.6 舍入函数

Synopsis

```
#include <math.h>
double round(double x);
float roundf(float x);
long double roundl(long double x);
```

Description

`round` 函数将其参数舍入为浮点数格式的最近的整数值，无论当前的舍入方向如何，对于中间情况均向远离零的方向舍入。

Returns

`round` 函数返回舍入后的整数值。

## 7.12.9.7 round 和 lround 函数

Synopsis

```
#include <math.h>
long int round(double x);
int roundf(float x);
long int roundl(double x);
long int llround(double x);
long int llroundf(float x);
long int llroundl(double x);
```

Description

`round` 和 `lround` 函数将参数舍入为最近的整数值，无论当前的舍入方向如何，对于中间情况均向远离零的方向舍入。如果舍入后的值超出返回类型的范围，则数值结果未定义，并可能发生域错误或范围错误。

Returns

`round` 和 `lround` 函数返回舍入后的整数值。

## 7.12.9.8 trunc 函数

Synopsis

```
#include <math.h>
double trunc(double x);
float truncf(float x);
long double truncl(long double x);
```

Description

- `trunc` 函数将参数舍入为浮点格式的整数值，该值在绝对值上最接近参数但不大于参数的值。

Returns

- `trunc` 函数返回截断后的整数值。

## 7.12.10 余数函数

### 7.12.10.1 fmod 函数

### Synopsis

```
#include <math.h>
double fmod(double x, double y);
float fmod(float x, float y);
long double fmodl(long double x, long double y);
```

Description

- `fmod` 函数计算 `x/y` 的浮点余数。

Returns

- `fmod` 函数返回值 `x–ny`，其中存在某个整数 `n`，使得如果 `y` 不为零，则结果的符号与 `x` 相同且绝对值小于 `y` 的绝对值。如果 `y` 为零，则发生域错误或 `fmod` 函数返回零由实现定义。

### 7.12.10.2 remainder 函数

### Synopsis

```
#include <math.h>
double remainder(double x, double y);
float remainderf(float x, float y);
long double remainderl(long double x, long double y);
```

Description

- `remainder` 函数计算 IEC 60559:239 的余数 `x REM y`

> 239) 当 `x ≠ 0` 时，无论如何舍入，余数 `r=x REM y` 都通过数学关系 `r=x–ny` 定义，其中 `n` 是接近 `x/y` 确切值的整数；每当 `|n-ny| = 1/2` 时，则 `n` 为偶数。如果 `r=0`，其符号应为 `x` 的符号。此定义适用于所有实现。

Returns

- `remainder` 函数返回 `x REM y`。如果 `y` 为零，则发生域错误或函数返回零由实现定义。

### 7.12.10.3 remquo 函数

### Synopsis

```
#include <math.h>
double remquo (double x, double y, int *quo);
float remquof (float x, float y, int *quo);
long double remquoi (long double x, long double y, int *quo);
```

Description

- `remquo` 函数计算与 `remainder` 函数相同的余数。在 `quo` 指向的对象中，它们存储一个值，该值的符号为 `x/y`，且绝对值对模 `2*n` 等同于 `x/y` 整数商的绝对值，其中 `n` 是一个大于或等于 3 的实现定义的整数。

Returns

- `remquo` 函数返回 `x REM y`。如果 `y` 为零，则在 `quo` 指向的对象中存储的值未定义，并发生域错误或函数返回零由实现定义。

## 7.12.11 操函数

### 7.12.11.1 copysign 函数

### Synopsis

```
#include <math.h>
double copysign (double x, double y);
float copysignf (float x, float y);
long double copysign (long double x, long double y);
```

Description

- `copysign` 函数产生一个绝对值为 `x`、符号为 `y` 的值。如果 `x` 是 NaN，则产生一个 NaN（带有 `y` 的符号）。在表示符号零但在算术操作中不一致处理负零的实现上，`copysign` 函数将零符号视为正。

Returns

- `copysign` 函数返回一个绝对值为 `x`、符号为 `y` 的值。

### 7.12.11.2 nan 函数

Synopsis

```
#include <math.h>
double nan(const char *tagp);
float nanof(float x);
long double nanl(long double x);
```

Description

- `nan` 函数产生根据 `tagp` 生成的、符号为 `y` 的 NaN。如果 `x` 是 NaN，则产生带有 `y` 的符号。在表示符号零但在算术操作中不一致处理负零的实现上，`copysign` 函数将零符号视为正。

Returns

- `nan` 函数返回一个绝对值为 `x`、符号为 `y` 的值。

### 7.12.11.3 nextafter 函数

Synopsis

```
#include <math.h>
double nextafter (double x, double y);
float nextafter (float x, float y);
long double nextafter (long double x, long double y);
```

Description

- `nextafter` 函数产生 `x` 向 `y` 方向的下一个可表示浮点数。

Returns

- `nextafter` 函数返回 `x` 向 `y` 方向的下一个可表示浮点数。

### 7.12.11.4 nexttoward 函数

Synopsis

```
#include <math.h>
double nexttoward(double x);
float nexttoward(float x);
long double nexttoward(long double x);
```

Description

- `nexttoward` 函数产生 `x` 向正无穷方向的下一个可表示浮点数。

Returns

- `nexttoward` 函数返回 `x` 向正无穷方向的下一个可表示浮点数。

## 7.12.14 比较宏

关系运算符和相等运算符支持数值值之间常见的数学关系。对于任何一个有序的数值对，小于、大于和相等这些关系中恰好有一个为真。当参数值值为 NaN 时，关系运算符可能会抛出“无效（invalid）”浮点异常。对于一个 NaN 和一个数值，或者对于两个 NaN，无序关系（unordered relationship）为真。²⁴⁴ 以下子句提供了关系运算符的静默（quiet，即不抛出浮点异常）版本的宏，其他宏有助于编写高效代码，而不会遭受“无效（invalid）”浮点异常。该子句中的概要，`real-floating` 指明参数应为实数浮点类型的表达式²⁴⁵（两个参数不需要具有相同的类型）。²⁴⁶

### 7.12.14.1 isgreater 宏

#### 概要

```c
#include <math.h>
int isgreater(real-floating x, real-floating y);
```

### 描述

`isgreater` 宏确定其第一个参数是否大于其第二个参数。`isgreater(x, y)` 的值始终等于 `(x > y)`；然而，与 `(x) > (y)` 不同，当 `x` 和 `y` 无序时，`isgreater(x, y)` 不会抛出“无效（invalid）”浮点异常。

#### 返回

`isgreater` 宏返回 `(x) > (y)` 的值。

### 7.12.14.2 isgreaterqual 宏

#### 概要

```c
#include <math.h>
int isgreaterqual(real-floating x, real-floating y);
```

> 244) IEC 60559 要求内置关系运算符在操作数无序比较时抛出“无效（invalid）”浮点异常，作为未考虑 NaN 的编写程序的错误指示；在这些情况下，结果为假。

> 245) 如果任何参数为整数类型或任何非实数浮点类型的类型，行为是未定义的。

> 246) 用比其语义类型更宽的格式表示的参数如何转换为语义类型是不指定的。

# ISO/IEC 9899:2011 (E)

### 描述

`isgreaterequal` 宏确定其第一个参数是否大于或等于第二个参数。`isgreaterequal(x, y)` 的值始终等于 `(x) >= (y)`；然而，与 `(x) >= (y)` 不同，`isgreaterequal(x, y)` 在 `x` 和 `y` 无序时不会抛出“无效（invalid）”浮点异常。

#### 返回

`isgreaterequal` 宏返回 `(x) >= (y)` 的值。

### 7.12.14.3 isless 宏

#### 概要

```c
#include <math.h>
int isless(real-floating x, real-floating y);
```

### 描述

`isless` 宏确定其第一个参数是否小于其第二个参数。`isless(x, y)` 的值始终等于 `(x) < (y)`；然而，与 `(x) < (y)` 不同，当 `x` 和 `y` 无序时，`isless(x, y)` 不会抛出“无效（invalid）”浮点异常。

#### 返回

`isless` 宏返回 `(x) < (y)` 的值。

### 7.12.14.4 islesqual 宏

#### 概要

```c
#include <math.h>
int islesqual(real-floating x, real-floating y);
```

### 描述

`islesqual` 宏确定其第一个参数是否小于或等于第二个参数。`islesqual(x, y)` 的值始终等于 `(x) <= (y)`；然而，与 `(x) <= (y)` 不同，当 `x` 和 `y` 无序时，`islesqual(x, y)` 不会抛出“无效（invalid）”浮点异常。

#### 返回

`islesqual` 宏返回 `(x) <= (y)` 的值。

### 7.12.14.5 islessgreater 宏

#### 概要

```c
#include <math.h>
isslessgreater(real-floating x, real-floating y);
```

### 描述

`islessgreater` 宏确定其第一个参数是否小于或大于第二个参数。`islessgreater(x, y)` 宏类似于 `(x) < (y) || (x) > (y)`；然而，当 `x` 和 `y` 无序时，`islessgreater(x, y)` 不抛出“无效（invalid）”浮点异常。

#### 返回

`islessgreater` 宏返回表达式 `(x) < (y) || (x) > (y)` 的值。

### 7.12.14.6 unordered 宏

#### 概要

```c
#include <math.h>
int unordered(real-floating x, real-floating y);
```

### 描述

`unordered` 宏确定参数是否无序。

#### 返回

如果参数无序返回 1，否则返回 0。
