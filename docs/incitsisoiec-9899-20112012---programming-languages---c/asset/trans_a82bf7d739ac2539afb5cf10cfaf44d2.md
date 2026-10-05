

## 7.12.11.4 nexttoward 函数

概要

描述：nexttoward 函数与 nextafter 函数等价，不同在于第二个参数的类型为 `long double`，且当 `x` 等于 `y` 时，函数返回转换为该函数类型的 `y`。241)

241) nexttoward 函数的结果由函数的类型决定，而不会在浮点数第二个参数中丢失丢失范围或精度。

## 7.12.12 最大值、最小值和正差函数

### 7.12.12.1 fdim 函数

概要

描述

fdim 函数确定其参数之间的正差。

> x-y，如果 x > y
> +0，如果 x ≤ y

 可能会发生范围错误。

返回

fdim 函数返回正差值。

### 7.12.12.2 fmax 函数

概要

描述

fmax 函数确定其参数中的最大数值。242

返回

fmax 函数返回其参数中的最大数值。

242 NaN 参数被视为未定义的数据：如果一个参数是 NaN 而另一个是数值，则 fmax 函数选择该数值值。参见 F.10.9.2。

## 7.12.13 fmin 函数

概要

```c
#include <math.h>
double fmin(double x, double y);
float fminf(float x, float y);
long double fminl(long double x, long double y);
```

描述

fmin 函数确定其参数中的最小数值。243

返回

fmin 函数返回其参数中的最小数值。

243 fmin 函数在处理 NaN 方面与 fmax 函数类似。

## 7.12.13 浮点乘加运算

### 7.12.13.1 fma 函数

概要

```c
#include <math.h>
double fma(double x, double y, double z);
float fmaf(float x, float y, float z);
long double fmal(long double x, long double y, long double z);
```

描述

fma 函数计算 (x × y) + z，并作为一次三元运算进行舍入：它们计算（仿佛）无限精度的值，并根据当前的舍入模式舍入到结果。可能会发生范围错误。

返回

fma 函数返回 (x × y) + z，作为一次三元运算进行舍入。

## 7.12.14 比较宏

关系运算符和相等运算符支持数值之间的通常关系。对于任何有序数值对，小于、大于和相等中恰好有一个为真。当参数为 NaN 时，关系运算符可能会抛出“无效”浮点异常。对于 NaN 和数值或两个 NaN，只有无序关系为真。244 以下宏提供了静默的（不抛出浮点异常）关系运算符版本，以及其他在不考虑 NaN 的情况下编写高效代码的比较宏。在这些宏的概要中，参数应当是浮点类型245（两个参数必须具有相同的类型）。244 如果操作数无序，结果为假。如果任何参数是整数类型或任何其他非浮点类型，行为是未定义的。246 在格式中表示的参数被转换为指定的类型。

### 7.12.14.1 isgreater 宏

概要

```c
#include <math.h>
int isgreater(real-floating x, real-floating y);
```

描述

isgreater 确定第一个参数是否大于第二个参数。isgreater(x, y) 的值始终等于 (x > y)；但与 (x > y) 不同，当 x 和 y 无序时，isgreater(x, y) 不抛出“无效”浮点异常。

返回

isgreater 宏返回 (x > y) 的值。

### 7.12.14.2 isgreaterequal 宏

概要

```c
#include <math.h>
int isgreaterequal(real-floating x, real-floating y);
```

描述

isgreaterequal 宏确定第一个参数是否大于等于第二个参数。isgreaterequal(x, y) 的值始终等于 (x >= y)；但与 (x >= y) 不同，当 x 和 y 无序时，isgreaterequal(x, y) 不抛出“无效”浮点异常。

返回

isgreaterequal 宏返回 (x >= y) 的值。

### 7.12.14.3 issless 宏

```c
#include <math.h>
int issless (real-floating x, real-floating y);
```

描述

issless 宏确定第一个参数是否小于第二个参数。issless(x, y) 的值始终等于 (x < y)；但与 (x < y) 不同，当 x 和 y 无序时，issless(x, y) 不抛出“无效”浮点异常。

返回

issless 宏返回 (x < y) 的值。

### 7.12.14.4 isslesqual 宏

概要

```c
#include <math.h>
int isslesqual (real-floating x, real-floating y);
```

描述

isslesqual 宏确定第一个参数是否小于等于第二个参数。isslesqual(x, y) 的值始终等于 (x <= y)；但与 (x <= y) 不同，当 x 和 y 无序时，isslesqual(x, y) 不抛出“无效”浮点异常。

返回

isslesqual 宏返回 (x <= y) 的值。

### 7.12.14.5 issgreater 宏

概要

```c
#include <math.h>
int issgreater(real-floating x, real-floating y);
```

描述

issgreater 宏确定第一个参数是小于还是大于第二个参数。issgreater(x, y) 宏类似于 (x < y) || (x > y)；但当 x 和 y 无序时，issgreater(x, y) 不抛出“无效”浮点异常。

返回

issgreater 宏返回 (x < y) || (x > y) 的值。

### 7.12.14.6 unordered 宏

概要

```c
#include <math.h>
int unordered(real-floating x, real-floating y);
```

描述

unordered 宏确定其参数是否无序。

返回

如果参数无序，unordered 宏返回 1，否则返回 0。

## 7.13 非局部跳转 <setjmp.h>

头文件 setjmp.h 通过绕过正常的函数调用和返回机制定义了 setjmp 宏，并声明了一个函数和一个类型。247)

声明的类型是

```
jmp_buf
```

这是一种适用于存储调用环境所需信息的数组类型。调用 setjmp 宏的环境由足够的信息组成，允许调用 longjmp 函数返回到正确的块以及该块的调用点（在这些块被递归调用的情况下）。它不包括浮点状态标志、已打开的文件或抽象机器的任何其他组件的状态。

未指定 setjmp 是宏还是具有外部链接的标识符。为了访问实际函数而抑制宏定义，或者程序定义了名为 setjmp 的外部标识符，行为是未定义的。

### 7.13.1 保存调用环境

概要

```c
#include <setjmp.h>
int setjmp(jmp_buf env);
```

描述

setjmp 宏将其调用环境保存在 jmp_buf 参数中，供 longjmp 函数以后使用。

返回

如果是直接调用，setjmp 宏返回零。如果是从调用 longjmp 函数返回，setjmp 宏返回非零值。

环境限制

setjmp 宏的调用应仅出现在以下上下文中：

- — 选择或迭代语句的整个控制表达式；
- 关系或相等运算符的一个操作数，另一个操作数为整数常量表达式，且结果表达式为整个控制

