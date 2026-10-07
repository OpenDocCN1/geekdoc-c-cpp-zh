

# ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – 版权所有

关于 D 的错误规定应对于当前的舍入方向具有正确的符号。294

# 返回值

+ 10 函数返回转换后的值（如果有）。如果未进行任何转换，则返回 0。如果正确值溢出且生效了默认舍入（7.12.1），则返回正或负 HUGE_VAL、HUGE_VALF 或 HUGE_VALL（取决于返回类型和值的符号），并将宏 **ERANGE** 的值存储在 **errno** 中。如果结果下溢（7.12.1），函数返回的值的幅度不大于该返回类型中最小的归一化正数；**errno** 是否获取值 **ERANGE** 由实现定义。

## 7.22.1.4 strtol, strtoll, strtoul, 和 strtoull 函数

## 概要

```
#include <stdlib.h>
long int strtol(
const char * restrict nptr,
char ** restrict endptr,
int base);
long long strtoll(
const char * restrict nptr,
char ** restrict endptr,
int base);
unsigned long int strtoul(
const char * restrict nptr,
char ** restrict endptr,
int base);
unsigned long int strtoull(
const char * restrict nptr,
char ** restrict endptr,
int base);
```

## 描述

+ 2 strtol, strtoll, strtoul, 和 strtoull 函数将 nptr 指向的字符串的初始部分转换为 `long int`、`long long int`、`unsigned long int` 和 `unsigned long long int` 表示。首先，它们将输入分解为三部分：一个初始的、可能为空的空白序列（由 `isspace` 函数分隔），一个主体序列

> 294 DECIMAL_DIG 定义在 <float.h> 中，其值应当大，使得 L 和 U 通常会舍入到相同的内部浮点值，但至少不会舍入到相邻的值。

类似于用由 **base** 值决定的某些进制表示的整数，以及一个由一个或多个无法识别字符组成的最终字符串，包括输入字符串的终止字符。然后，它们尝试将该序列转换为整数并返回结果。

+ 如果 **base** 的值为 0，主体序列的预期形式为如 6.4.4.1 所述的整数常量，可选的前跟带有加号或减号，但不包括整数后缀。如果 **base** 的值在 2 到 36 之间（包含），主体序列的预期形式是代表该整数的字母和数字序列，其进制由 **base** 指定，可选的前跟带有加号或减号，但不包括整数后缀。从 **a**（或 **A**）到 **z**（或 **Z**）的字母被赋予值 10 到 35；仅允许值小于 **base** 值的字母和数字。如果 **base** 的值为 36，则返回字符 **0x** 或 **0OX**。它们可以可选在符号（如果存在）之后提供字母和数字的序列。

+ 该序列定义为输入字符串中从第一个非空白字符开始的符合预期形式的最长初始子序列。如果输入字符串为空或完全由空白组成，或者第一个非空白字符不是符号、允许的字符或数字，则主体序列不包含任何字符。

+ 如果序列具有预期形式且 **base** 的值为 0，则从第一个数字开始的字符序列被根据 6.4.4.1 的规则解释为整数常量。如果序列具有预期形式且 **base** 的值在 2 到 36 之间，它被用作转换的基数，并将每个字母转换为上述值。如果主体以减号开头，则转换产生的值将取反（在返回类型中）。只要 **endptr** 不是空指针，则将最终字符串的指针存储在 **endptr** 指向的对象。

+ 在“C”区域之外，可能接受额外的特定区域的主体序列形式。

+ 如果序列为空或不具有预期形式，则不进行转换；只要 **endptr** 不是空指针，则将 **nptr** 的值存储在 **endptr** 指向的对象。

## 返回值

+ **strtol**, **strtoll**, **strtoul**, 和** 函数返回转换后的值（如果有）。如果无法执行转换，则返回 0。如果正确值在可表示范围之外，则返回 **LONG_MIN**、**LONG_MAX**、**LLONG_MIN**、**LLONG_MAX**、**ULONG_MAX** 或 **ULLONG_MAX**（取决于返回类型和值的符号，如果有），并将宏 **ERANGE** 的值存储在 **errno** 中。

§7.2.2.1 库

## 7.22.2 伪随机序列生成函数

## 7.22.2.1 rand 函数

## 概要

```
#include <stdlib.h>
int rand(void);
```

## 描述

rand 函数计算一个伪随机整数序列。rand 函数不需要避免与其他序列生成函数的调用产生数据竞态。实现的行为应当像一个库函数。

## 返回值

rand 函数返回一个伪随机整数。

## 环境限制

RAND_MAX 的值应至少为 32767。

## 7.22.2.2 srand 函数

## 概要

```
#include <stdlib.h>
void srand(unsigned int seed);
```

## 描述

srand 函数使用参数作为新伪随机数序列种子。如果使用相同的种子调用 srand，则序列将重复。如果在调用任何 srand 之前调用 rand，生成的序列应与首次调用种子值为 1 的 srand 时相同。

## 返回值

srand 函数不返回值。

```
static int next = 1;
int rand(void)      // 假设 RAND_MAX 为 32767
{
    next = next * 110351245 + 12345;
    return (unsigned int)(next/65536) % 32768;
}
void srand(unsigned int seed)
{
    next = seed;
}
```
