

## G.6.3 指数和对数函数

### G.6.3.1 cexp 函数

- cexp(conj(z)) = conj(cexp(z)).
- cexp(±0 +i0) 返回 1 + i0。
- cexp(x +∞) 对于有限的 x 返回 NaN+iNaN 并抛出“无效”（invalid）浮点异常。
- cexp(x +iNaN) 对于有限的 x 返回 NaN+iNaN 并可选地抛出“无效”（invalid）浮点异常。
- cexp(+∞ +i0) 返回 ∞ +i0。
- cexp(-∞ + iy) 对于有限的 y，返回 +0 cis(y)。
- cexp(+∞ + iy) 对于有限的 y，返回 -∞ cis(y)。
- cexp(-∞ +∞) 返回 ±0±i0（结果的实部和虚部的符号未指定）。
- cexp(+∞ + ∞) 返回 ±∞+iNaN 并抛出“无效”（invalid）浮点异常（结果的实部符号未指定）。
- cexp(-∞ +iNaN) 返回 ±0±i0（结果的实部和虚部的符号未指定）。
- cexp(+∞ +iNaN) 返回 ∞+iNaN（结果的实部符号未指定）。
- cexp(NaN +i0) 返回 NaN + i0。
- cexp(NaN + iy) 对于所有非零数字 y，返回 NaN+iNaN 并可选地抛出“无效”（invalid）浮点异常。
- cexp(NaN +iNaN) 返回 NaN +iNaN。

### G.6.3.2 clog 函数

- clog(conj(z)) = conj(clog(z)).
- clog(-0 +i0) 返回 -∞+iπ 并抛出“除以零”（divide-by-zero）浮点异常。
- clog(+0 +i0) 返回 -∞ +i0 并抛出“除以零”（divide-by-zero）浮点异常。
- clog(x +∞) 对于有限的 x 返回 +∞π/2。
- clog(x +iNaN) 对于有限的 x 返回 NaN +iNaN 并可选地抛出“无效”（invalid）浮点异常。
- clog(-∞ iy) 对于正符号的有限 y，返回 +∞π。
- clog(+∞ iy) 对于正符号的有限 y，返回 +∞0。
- clog(-∞ iy) 返回 +∞3π/4。
- clog(+∞ iy) 返回 +∞π/4。
- clog(±∞ iy) 返回 +∞ iNaN。
- clog(NaN+ iy) 对于有限的 y，返回 NaN iNaN 并可选地抛出“无效”（invalid）浮点异常。
- clog(NaN+∞) 返回 +∞NaN。
- clog(NaN+iNaN) 返回 NaN iNaN。

## G.6.4 幂和绝对值函数

### G.6.4.1 cpow 函数

cpow 函数在计算结果部分如果需要时会抛出浮点异常，也可能抛出虚假的浮点异常.³379)

### G.6.4.2 csqrt 函数

- csqrt(conj z) = conj(csqrt z).
- csqrt(±0+i0) 返回 +∞0。
- csqrt(x+ ix) 对于所有的 x（包括 NaN）返回 +∞∞。
- csqrt(x+iNaN) 对于有限的 x 返回 NaN iNaN 并可选地抛出“无效”（invalid）浮点异常。
- csqrt(-∞ iy) 对于正符号的有限 y，返回 +∞0。
- csqrt(+∞ iy) 对于正符号的有限 y，返回 +∞0。
- csqrt(-∞+iNaN) 返回 NaN±∞（结果的虚部符号未指定）。
- csqrt(+∞+iNaN) 返回 +∞NaN。
- csqrt(NaN+ iy) 对于有限的 y，返回 NaN iNaN 并可选地抛出“无效”（invalid）浮点异常。
- csqrt(NaN+iNaN) 返回 NaN iNaN。

> 379) 这允许 cpow(z, c) 被实现为 cexp(c clog(z))，而不会排除那些更仔细地处理特殊情况的实现。

## G.7 类型泛型数学 <tgmath.h>

接受复数参数的类型泛型宏也接受虚数参数。如果参数是虚数，则宏将展开为根据特定函数相应类型为实数、虚数或复数的表达式：如果参数是虚数，则 cos, cosh, fabs, carg, cimag, creal 的类型为实数；sin, tan, sinh, tanh, asin, atan, asinh, atanh 的类型为虚数；其他类型为复数。

给定一个虚数参数，每个类型泛型宏 cos, sin, tan, cosh, sinh, tanh, asin, atan, asinh, atanh 均由一个实函数的公式指定：

```
cos(iy)    = cosh(y)
sin(iy)    = i sinh(y)
tan(iy)    = i tanh(y)
cosh(iy)  = cos(y)
sinh(iy)  = i sin(y)
tanh(iy)  = i tan(y)
asin(iy)   = i asinh(y)
atan(iy)   = i atanh(y)
asinh(iy) = i asin(y)
atan(iy)= i atan(y)
```

## 录 H 与语言无关的运算

### H.1 引言

本文档记录了 C 语言支持 ISO/IEC 10967-1 语言无关运算的程度。LIA–1 比 IEC 60559 更通用，因为它涵盖了整数和浮点运算。

### H.2 类型

如果实现增加了异常运算的通知并满足最后一位精度（ULP）的精度要求，则相关的 算术类型满足 LIA–1 的要求。

### H.2.1 布尔

LIA–1 数据类型由 `<stdbool.h>` 中具有 **true** 和 **false** 值的 **bool** 类型实现。

### H.2.2 整数

有符号类型 **int, long int** 以及相应的无符号类型与 LIA–1 。如果实现增加了对 LIA–1 异常值“整数溢出”和“未定义”的支持，则这些类型符合。无符号类型在 LIA–1 意义下为“取模”或“越界”。定义有符号整数类型的实现必须检测整数溢出。

整数类型的参数可以通过以下值访问：

```
INT_MAX, LONG_MAX, LLONG_MAX, UINT_MAX, ULONG_MAX, ULLONG_MAX
INT_MIN, LONG_MIN, LLONG_MIN
```

“bounded”参数始终为 true，且不提供。“minint”参数对于无符号类型也不提供。

### H.2.2.1 整数运算

整数类型上的整数运算如下：

```
addl x + y
subl x - y
mull x * y
divl x / y
reml x % y
negl -x
absl (x), labs (x), llabs (x)
eqq x == y
eql x != y
lssl x < y
leql x <= y
mtrl x > y
geql x >= y
```

其中 x 和 y 是相同整数类型的表达式。

### H.2.3 浮点类型

浮点类型 float, double 和 long double 符合 LIA–1。如果实现增加了对 LIA–1 异常值“下溢”、“浮点溢出”和“未定义”的支持，则这些类型符合。使用 IEC 60559 浮点格式和运算（见录 F）带有状态标志和异常的实现符合 LIA–1 类型。

### H.2.3.1 浮点参数

浮点数据类型的参数可以通过以下值访问：

```
r FLT_RADIX
p FLT_MANT_DIG, DBL_MANT_DIG, LDB_MANT_DIG
amax FLT_MAX_EXP, DBL_MAX_EXP, LDB_MAX_EXP
emin FLT_MIN_EXP, DBL_MIN_EXP, LDB_MIN_EXP
```

浮点类型的派生常量通过以下值访问：

```
fmax FLT_MAX, DBL_MAX, LDB_MAX
fmin FLT_MIN, DBL_MIN, LDB_MIN
epsilon FLT_EPSON, DBL_EPSON, LDB_EPSON
rnd_style FLT_ROUNDS
```

### H.2.3.2 浮点运算

浮点类型上的浮点运算如下：

- addF x + y
- subF x - y
- mulF x * y
- divF x / y
- negF -x
- absF sf(x), fabs(x), fabsl(x)
- exponentF 1.f+logb(x), 1.0+logb(x), 1.L+logbl(x)
- scaleF scalnf(x, n), scalbn(x, n), scalnl(x, n), scalbnf(x, li), scalbnl(x, li)
- intpartF modff(x, &y), modf(x, &y), modfl(x, &y)
- fractpart modff(x, &y), modf(x, &y), modfl(x, &y)
- eqF x == y
- eqqF x != y
- lssF x < y
- leQF x <= y
- gtrF x > y
- geqF x >= y

其中 x 和 y 是相同浮点类型的表达式，n 是 int，li 是 long int。

### H.2.3.3 舍入方式

C 标准要求所有浮点类型使用相同的基和舍入方式，以便为每个标识符映射到 LIA–1。FLT_ROUNDS 参数可指示 LIA–1 舍入方式：

- truncate FLT_ROUNDS == 0
- nearest FLT_ROUNDS == 1
- other FLT_ROUNDS != 0 && FLT_ROUNDS != 1

只要实现扩展 FLT_ROUNDS 以涵盖所有相关的 LIA–1 操作中使用的舍入方式，而不仅仅是在 C 中。

### H.2.4 类型转换

LIA–1 类型转换是以下强制转换：

```
cvtI -> I (int) i, (long int) i, (long long int) i, (unsigned int) i, (unsigned long int) i, (unsigned long long int) i
ccvtF -> I (int) x, (long int) x, (long long int) x, (unsigned int) x, (unsigned long int) x, (unsigned long long int) x
ccvtI -> F (float) i, (double) i, (long double) i
ccvtF -> F (float) x, (double) x, (long double) x
```

在上述转换为浮点的（强制转换中，使用 (cast) x 可以替换为 (cast) round(x), (cast) rist(x), (cast) nearbyint(x), (cast) trunc(x), (cast) ceil(x) 或 (cast) floor(x)。此外，C 的浮点到整数转换函数 lrint(x), llrint(x), lround(x) 和 llround(x) 可以使用。它们都满足 LIA–1 对范围内值的浮点到整数舍入的要求。对于范围外值，转换对于取模类型应静默取回。

fmod(x) 函数适用于符号环到无符号整数类型，例如，fmod(fabs(x), 65536.0) 或 (0.0 <= (y = fmod(rint(x), 65536.0)) ? y : 65536.0 + y) 会计算 0 到 65535.0 之间的整数值，可以转换为 unsigned short int。但，remainder(x) 函数不适用于符号环到有符号整数类型，例如，remainder(rint(x), 65536.0) 会计算 -32767.0 到 +32768.0 之间的整数值，这通常不在有符号 short int 的范围内。

