

## F10.2 双曲函数

### F10.2.1 acosh 函数

- acosh (1) 返回 +0。
- acosh (x) 在 x < 1 时返回 NaN 并抛出“无效（invalid）”浮点异常。
- acosh (±∞) 返回 ±∞。

### F10.2.2 asinh 函数

- asinh (±0) 返回 ±0。
- asinh (±∞) 返回 ±∞。

### F10.2.3 atanh 函数

- atanh (±0) 返回 ±0。
- atanh (±1) 返回 ±∞ 并抛出“除零（divide-by-zero）”浮点异常。
- atanh (x) 在 |x| > 1 时返回 NaN 并抛出“无效（invalid）”浮点异常。

### F10.2.4 cosh 函数

- cosh (±0) 返回 1。
- cosh (±∞) 返回 +∞。

### F10.2.5 sinh 函数

- sinh (±0) 返回 ±0。
- sinh (±∞) 返回 ±∞。

### F10.2.6 tanh 函数

- tanh (±0) 返回 ±0。
- tanh (±∞) 返回 ±1。

## F10.3 指数和对数函数

### F10.3.1 exp 函数

- exp (±0) 返回 1。
- exp (-∞) 返回 +0。
- exp (±∞) 返回 +∞。

### F10.3.2 exp2 函数

- exp2(±0) 返回 1。
- exp2(-∞) 返回 +0。
- exp2(∞) 返回 ∞。

### F10.3.3 expm1 函数

- expm1(±0) 返回 ±0。
- expm1(-∞) 返回 -1。
- expm1(∞) 返回 +∞。

### F10.3.4 frexp 函数

- frexp(±0, exp) 返回 ±0，并在 exp 指向的对象内存中存储 0。
- frexp(∞, exp) 返回 ∞，并在 exp 指向的对象中存储一个未指定的值。
- frexp(NaN, exp) 在 exp 指向的对象中存储一个未指定的值（并返回 NaN）。

frexp 会抛出浮点异常。

当参数的基数为 2 的幂时，返回的值是精确的，且独立于当前的舍入方向模式。

在二进制系统中，frexp 函数的体可能是：

```
{
    *exp = (value == 0) ? 0 : (int) (1 + logb(value));
    return scalbn(value, -(exp));
}
```

### F10.3.5 ilogb 函数

当正确结果可以在返回类型的范围内表示时，返回的值是精确的，且独立于当前的舍入方向模式。

如果正确结果在返回类型的范围之外，数值结果未指定并抛出“无效（invalid）”浮点异常。

当 x 为零、无穷或 NaN 时，ilogb(x) 抛出“无效（invalid）”浮点异常并返回7.12.6 中指定的值。

### F10.3.6 1dexexp 函数

在二进制系统中，1dexp(x, exp) 等于 scalbn(x, exp)。

### F10.3.7 log 函数

- log(±0) 返回 -∞ 并抛出“除零（divide-by-zero）”浮点异常。
- log(1) 返回 +0。
- log(x) 在 x < 0 时返回 NaN 并抛出“无效（invalid）”浮点异常。
- log(+∞) 返回 +∞。

### F10.3.8 log10 函数

- log10(±0) 返回 -∞ 并抛出“除零（divide-by-zero）”浮点异常。
- log10(1) 返回 +0。
- log10(x) 在 x < 0 时返回 NaN 并抛出“无效（invalid）”浮点异常。
- log10(+∞) 返回 +∞。

### F10.3.9 logp 函数

- logp(±0) 返回 ±0。
- logp(-1) 返回 -∞ 并抛出“除零（divide-by-zero）”浮点异常。
- logp(x) 在 x ≤ -1 时返回 NaN 并抛出“无效（invalid）”浮点异常。
- logp(+∞) 返回 +∞。

### F10.3.10 log2 函数

- log2(±0) 返回 -∞ 并抛出“除零（divide-by-zero）”浮点异常。
- log2(1) 返回 +0。
- log2(x) 在 x < 0 时返回 NaN 并抛出“无效（invalid）”浮点异常。
- log2(+∞) 返回 +∞。

### F10.3.11 logb 函数

- logb(±0) 返回 -∞ 并抛出“除零（divide-by-zero）”浮点异常。
- logb(+∞) 返回 +∞。

返回的值是精确的，且独立于舍入方向模式。

### F10.3.12 modf 函数

- modf(±x, iptr) 返回与 x 符号相同的符号。
- modf(∞, iptr) 返回 ±0并在 iptr 指向的对象中存储 ∞。
- modf(NaN, iptr) 在 iptr 指向的对象中存储 NaN（返回 NaN）。

返回的值是精确的，且独立于舍入方向模式。

modf 的实现类似于：

```
#include <math.h>
#include <fenv.h>
#pragma STDC FENV_ACCESS
double modf(double value, double *iptr) {
    double result;
    int save_round = fegetround();
    fesetround(FE_TOWARDZERO);
    *iptr = rint(value);
    result = value - (*iptr);
    fesetround(save_round);
    return result;
}
```

### F10.3.13 scalbn 函数

- scalbn(±0, n) 返回 ±0。
- scalbn(x, 0) 返回 x。
- scalbn(∞, n) 返回 ∞。

如果计算没有溢出或下溢，返回的值是精确的，独立于舍入方向模式。

## F10.4 幂和绝对值函数

### F10.4.1 cbrt 函数

- cbrt(±0) 返回 ±0。
- cbrt(±∞) 返回 ±∞。

### F10.4.2 fabs 函数

- fabs(±0) 返回 ±0。
- fabs(±∞) 返回 ±∞。

返回的值是精确的，且独立于舍入方向模式。

### F10.4.3 hypot 函数

- hypot(x, y), hypot(y, x) 和 hypot(x, -y) 等价。
- hypot(x, ±0) 等于 fabs(x)。
- 如果 y 为 NaN，hypot(±∞, y) 返回 ±∞。

### F10.4.4 pow 函数

- pow(±0, y) 在 y 为负整数时返回 ±∞ 并抛出“除零（divide-by-zero）”浮点异常。
- pow(±0, y) 在 y < 0、有限且非整数时返回 +∞ 并抛出“除零（divide-by-zero）”浮点异常。
- pow(±0, -∞) 返回 +∞ 并可能抛出“除零（divide-by-zero）”浮点异常。
- pow(±0, y) 在 y 为负整数时返回 ±0。
- pow(±0, y) 在 y > 0 且非整数时返回 +0。
- pow(-1, ±∞) 返回 1。
- pow(+1, y) 对于任何 y（甚至是 NaN）都返回 1。
- pow(x, ±0) 对于任何 x（甚至是 NaN）都返回 1。
- pow(x, y) 在有限 x < 0 和有限非 y 时返回 NaN 并抛出“无效（invalid）”浮点异常。
- pow(x, -∞) 在 |x| < 1 时返回 +∞。
- pow(x, -∞) 在 |x| > 1 时返回 +0。
- pow(x, +∞) 在 |x| < 1 时返回 +0。
- pow(x, +∞) 在 |x| > 1 时返回 +∞。

pow(-∞, y) 在 y 为负整数时返回 -0。
pow(-∞, y) 在 y < 0 且非整数时返回 +0。
pow(-∞, y) 在 y 为正整数时返回 -∞。
pow(-∞, y) 在 y > 0 且非整数时返回 +∞。
pow(+∞, y) 在 y < 0 时返回 +0。
pow(+∞, y) 在 y > 0 时返回 +∞。

### F10.4.5 sqrt 函数

- sqrt 在 IEC 60559 中完整规定为基本算术运算。返回的值取决于舍入方向模式。

## F10.5 误差和伽函数

### F10.5.1 erf 函数

- erf(±0) 返回 ±0。
- erf(±∞) 返回 ±1。

### F10.5.2 erfc 函数

- erfc(-∞) 返回 2。
- erfc(+∞) 返回 +0。

### F10.5.3 lgamma 函数

- lgamma(1) 返回 +0。
- lgamma(2) 返回 +0。
- lgamma(x) 在 x 为负整数或零时返回 +∞ 并抛出“除零（divide-by-zero）”浮点异常。
- lgamma(-∞) 返回 +∞。
- lgamma(+∞) 返回 +∞。

### F10.5.4 tgamma 函数

- tgamma(±0) 在 x 为负整数时返回 ±∞ 并抛出“除零（divide-by-zero）”浮点异常。
- tgamma(x) 在 x 为负整数时返回 NaN 并抛出“无效（invalid）”浮点异常。
- tgamma(-∞) 返回 NaN 并抛出“无效（invalid）”浮点异常。
- tgamma(+∞) 返回 +∞。

## F10.6 接近整数函数

### F10.6.1 ceil 函数

- ceil(±0) 返回 ±0。
- ceil(±∞) 返回 ±∞。

返回的值独立于舍入方向模式。

double 版本的 ceil 实现类似于：

```
#include <math.h>
#include <fenv.h>
#pragma STDC FENV_ACCESS
double ceil(double x) {
    double result;
    int save_round = fegetround();
    fesetround(FE_UPWARD);
    result = rint(x); // 或者使用 nearbyint 代替 rint
    fesetround(save_round);
    return result;
}
```

### F10.6.2 floor 函数

- floor(±0) 返回 ±0。
- floor(±∞) 返回 ±∞。

返回的值独立于舍入方向模式。

### F10.6.3 nearbyint 函数

nearbyint 函数根据当前的舍入方向使用 IEC 60559 舍入。如果结果与参数的值不同，则不抛出“不精确（inexact）”浮点异常。

