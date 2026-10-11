
### 说明

`fswf` 函数从流中读取输入，格式指定了允许的输入以及如何将其转换。如果参数不足，则行为未定义。如果格式耗尽但仍有参数，多余的参数将（始终）被计算，但会被忽略。

- 一个可选的抑制小数宽字符。
- 一个大于零的可选整数，指定最大字段宽度（宽字符）。
- 一个可选的长度修饰符，指定接收对象的大小。
一个 指定应用转换类型的转换符宽字符。

4 `fswf` 函数执行格式的每个指令。当所有指令执行完毕，或某个指令失败时（见下文），函数返回。失败被描述为输入失败（由于编码错误或输入不可用）或匹配失败（由于输入不当）。

5 由空白宽字符组成的指令通过读取输入到第一个非空白宽字符（保持不变）或直到无法读取更多宽字符为止来执行。该指令不会失败。

6 普通宽字符指令通过读取流的下一个宽字符来执行。如果该字符与指令不符，则指令失败，该字符及后续宽字符保持不变。同样，如果文件结束、编码错误或读取错误阻止了宽字符的读取，则指令失败。

7 转换规范指令定义了一组匹配输入序列，如每个说明符所示。转换规范按以下步骤执行：

8 跳过空白宽字符（如 `isspace` 函数所示），除非规范包含 `l`、`c` 或 `n` 说明符。³³⁷

³³7 这些空白宽字符不计入指定的字段宽度。

9 从流中读取一个输入项，除非规范包含 `n` 说明符。输入项被定义为不超过任何指定字段宽度的输入宽字符序列，且是匹配序列的前缀

336 有效数字个数由说明符决定，在固定点情况下

结果应具有正确的符号。

# ISO/IEC 9899:2011 (E)

# © ISO/IEC 2011 – 版权所有

序列.³338 第一个宽字符（如果有的话），输入项保持未读状态。如果输入项的长度为 0，则指令的执行将失败；此情况为匹配失败，除非由于文件结束符、编码错误或读取错误阻止了从流中输入，在这种情况下，它为输入失败。

+   除 `%` 规格符的情况外，输入项（或在 `%n` 指令的情况下，输入字符的计数）被转换为适当的类型或转换说明符。如果输入项不符合匹配情况，则指令的执行将失败；此情况为匹配失败。除非通过 `*` 指明了赋值，否则转换的结果将放在格式参数之后、第一个尚未接收到转换结果的参数所指向的对象中。如果该对象没有适当的类型，或者转换结果无法在对象中表示，则行为是未定义的。

+   修饰符及其含义为：

+   `hh`
指定 `d`, `i`, `o`, `u`, `x` 或 `n` 转换说明符适用于类型为指向有符号 char 或无符号 char 指针的参数。

+   `h`
指定后续的 `d`, `i`, `o`, `u`, `x` 或 `n` 转换说明符适用于类型为指向 short int 或无符号 short int 指针的参数。

+   `l` (ell)
指定 `d`, `i`, `o`, `u`, `x`, `X` 或 `n` 转换说明符适用于类型为指向 long int 或无符号 long int 指针的参数；或者后续的 `A. e, E, f. g. 或 G` 转换说明符适用于类型为指向 double 指针的参数；或者后续的 `c, s` 或 `[` 转换说明符适用于类型为指向 wchar_t 指针的参数。

+   `ll` (ell-ell)
指定 `d`, `i`, `o`, `u`, `x`, `X` 或 `n` 转换说明符适用于类型为指向 long long int 或无符号 long int 指针的参数。

+   `j`
指定后续的 `d`, `i`, `o`, `u`, `x`, `X` 或 `n` 转换说明符适用于类型为指向 intmax_t 或 uintmax_t 指针的参数。

+   `z`
指定后续的 `d`, `i`, `o`, `u`, `x`, `X` 或 `n` 转换说明符适用于类型为指向 size_t 或相应有符号整数的指针的参数。

+   `t`
指定后续的 `d`, `i`, `o`, `u`, `x`, `X` 或 `n` 转换说明符适用于类型为指向 ptrdiff_t 或相应无符号整数类型的指针的参数。

> 338 `fswscanf` 向输入流中最多回退一个宽字符。因此，某些被 west, wcstl 等接受的序列在 `fswcanf` 中是不被接受的。

`L` 指定后续的 `a, A, e, E, f, g, 或 G` 转换说明符适用于类型为指向 long double 指针的参数。

如果长度修饰符出现在上述指定以外的任何转换说明符处，则行为是未定义的。

+   2 转换说明符及其含义为：

+   `d` 匹配一个可选的有符号十进制整数，其格式与 `wstol` 函数针对目标序列的预期格式相同，其中基数参数的取值为 10。相应的参数应为指向有符号整数的指针。

+   `i` 匹配一个可选的有符号整数，其格式与 `wstol` 函数针对目标序列的预期格式相同，其中基数参数的取值为 0。相应的参数应为指向有符号整数的指针。

+   `o` 匹配一个可选的有符号八进制整数，其格式与 `wstol` 函数针对目标序列的预期格式相同，其中基数参数的取值为 8。相应的参数应为指向无符号整数的指针。

+   `u` 匹配一个可选的有符号十进制整数，其格式与 `wstol` 函数针对目标序列的预期格式相同，其中基数参数的取值为 10。相应的参数应为指向无符号整数的指针。

+   `x` 匹配一个可选的有符号十六进制整数，其格式与 `wstol` 函数针对目标序列的预期格式相同，其中基数参数的取值为 16。相应的参数应为指向无符号整数的指针。

+   `a, e, E, f, g. 或 G` 匹配可选的有符号浮点数、无穷大或 NaN，其格式与 `wstol` 函数针对目标序列的预期格式相同，其中基数参数的取值为 10。相应的参数应为指向无符号整数的指针。

+   `c` 匹配单个的 `%` 宽字符；不发生转换或赋值。完整的转换说明符应为 `%`.

+   13 如果转换说明符无效，则行为是未定义的.³³³⁹

+   14 转换说明符 `A, E, F, G` 和 `X` 也是有效的，且行为分别与 `a. e. f. g.` 和 `x` 相同。

+   15 尾空白（包括换行符）在没有指令的情况下保持未匹配。字面量匹配和抑制赋值的成功无法通过 `%n` 指令直接确定。

# 返回

+   16 如果在第一个转换（如果有）完成之前发生输入失败，`fscanf` 返回宏 `EOF` 的值。否则，函数返回赋值的输入项数，在早期匹配失败的情况下，该值可能为零。

+   17 示例 I 调用：

```
#include <stdio.h>
#include <wchar.h>
/* ... */
int i; float x; char_t name[50];
n = fscanf(stdin, "%d%%%ls", &i, &x, name);
```

`P` 匹配一组实现定义的序列，应与 `fwprintf` 函数的 `%p` 转换可能产生的序列相同。相应的参数应为指向 void 指针。输入项以实现定义的方式转换为指针值。如果输入项是在同一个程序执行期间之前转换过的值，则指针结果等于该值；否则 `%p` 转换的行为是未定义的。

`n` 不消耗输入。结果参数应为有符号整数，用于写入到为止该调用从输入流中读取的宽字符数。`%n` 指令的执行不会增加返回的赋值计数，除非该参数被消耗。如果转换说明符包含抑制赋值的宽字符或字段宽度，则行为是未定义的。³³⁹

参见“未来库方向”（77.31.16）。

# ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – 保留所有权利

输入行：

25 54.32E-1 thompson

将给 `n` 赋值为 3，将 `i` 赋值为 25，将 `x` 赋值为 5.432，并将序列命名为 thom。

- 1 示例 2 调用如下：

```c
#include <stdio.h>
#include <wchar.h>
/* */
int i; float x; double y;
wcanf(stdin, "L%2d%f%d %lf", &i, &x, &y);
```

输入为：

56789 0123 56a72

将给 `i` 赋值为 56，将 `x` 赋值为 789.0，跳过 0123，并将 `y` 赋值为 56.0。从输入流中读取的下一个字符将是 `a`。

前向引用：`wcstod`、`wcstof` 和 `wcstold` 函数 (72.29.4.1.1)，`wcstol`、`wcstoll`、`wcstoul` 和 `wcstll` 函数 (72.29.4.1.2)，`wcrtomb` 函数 (72.29.6.3.3)。

## 79.29.3 sprintf 函数

概要

- 1 `#include <wchar.h>`
`int swprintf(wchar_t * restrict s, size_t n, const wchar_t * restrict format, ...);`

描述

- 2 `sprintf` 函数等同于 `fwprintf`，不同之处在于参数指定了一个用于写入生成输出宽字符数组，而不是写入到流。写入的宽字符不超过 `n` 个，其中包含一个总是添加的终止空字符（当 `n` 为零时）。

返回值

- 3 `sprintf` 函数返回写入数组的宽字符数，不计入终止空字符；如果发生编码错误，或者请求生成 `n` 或更多宽字符，则返回负值。

库

§ 79.29.2

### 7.29.2.4 swscancf 函数

概要

```c
#include <wchar.h>
int swscancf(const wchar_t * restrict s, const wchar_t * restrict format, ...);
```

描述

`swscancf` 函数等同于 `fwscancf`，不同之处在于参数 `s` 指定了一个从其中获取输入的宽字符串，而不是从流。到达宽字符串的末尾等同于 `fwscancf` 函数遇到文件结束符（`EOF`）。

返回值

如果在第一次转换（如果有）完成之前发生输入失败，`swscancf` 函数返回宏 `EOF` 的值。否则，`swscancf` 函数返回分配的输入数量，在提前匹配失败的情况下，该数量可以少于提供的数量甚至是零。

### 7.29.2.5 vfwprintf 函数

概要

```c
#include <stdarg.h>
#include <stdio.h>
#include <wchar.h>
int vfwprintf(FILE * restrict stream, wchar_t * restrict format, va_list arg);
```

描述

`vfwprintf` 函数等同于 `fwprintf`，将变长参数列表替换为 `arg`，`arg` 应由 `va_start` 宏（以及可能的后续 `va_arg` 调用）初始化。`vfwprintf` 函数不调用 `va_end` 宏。

返回值

`vfwprintf` 函数返回传输的宽字符数；如果发生输出或编码错误，则返回负值。

> 340) 由于函数 `vfwprintf`、`vswprintf`、`vfwscancf`、`vfwprintf`、`swscancf` 和 `vswancf` 调用了 `va_arg` 宏，返回值是不确定的。

# ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – 保留所有权利

- 4 示例显示了在通用错误例程中使用 `vfwprintf` 函数。

```c
#include <stdarg.h>
#include <stdio.h>
#include <wchar.h>
void error(char *function_name, wchar_t *format, ...)
{
    va_list args;
    va_start(args, format);
    // 打印函数名
    fwprintf(stderr, "ERROR in %s: ", function_name);
    // 打印消息剩余
    fwprintf(stderr, format, args);
    va_end(args);
}
```

### 7.29.2.6 vfwscanf 函数

概要

```c
#include <stdarg.h>
#include <stdio.h>
#include <wchar.h>
int vfwscanf(FILE * restrict stream, const wchar_t * restrict format, va_list arg);
```

描述

`vfwscanf` 函数等同于 `vfwscanf`，将变长参数列表替换为 `va_start` 宏（以及可能的 `va_arg` 调用）。

返回值

如果在第一次转换（如果有）完成之前发生输入失败，`vfwscanf` 函数返回宏 `EOF` 的值。否则，`vfwscanf` 函数返回分配的输入数量，在提前匹配失败的情况下，该数量可以少于提供的数量甚至是零。

### 7.29.2.7 vswprintf 函数

概要

```c
#include <stdarg.h>
#include <wchar.h>
int vswprintf(wchar_t * restrict s, size_t n, const wchar_t * restrict format, va_list arg);
```

描述

`vswprintf` 函数等同于 `swprintf`，将变长参数列表替换为 `arg`，`arg` 应由 `va_start` 宏（以及可能的 `va_arg` 调用）初始化。`vswprintf` 函数不调用 `va_end` 宏。

返回值

`vswprintf` 函数返回写入数组的宽字符数，不计终止空字符；如果发生编码错误或请求生成 `n` 或更多宽字符，则返回负值。

### 7.29.2.8 vswcanf 函数

概要

```c
#include <stdarg.h>
#include <wchar.h>
int vswcanf(const wchar_t * restrict s, const wchar_t * restrict format, va_list arg);
```

描述

`vswcanf` 函数等同于 `swscanf`，将变长参数列表替换为 `arg`，`arg` 应由 `va_start` 宏（以及可能的 `va_arg` 调用）初始化。`vswcanf` 函数不调用 `va_end` 宏。

返回值

如果在第一次转换（如果有）完成之前发生输入失败，`vswcanf` 函数返回宏 `EOF` 的值。否则，`vswcanf` 函数返回分配的输入数量，在提前匹配失败的情况下，该数量可以少于提供的数量甚至是零。

# ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – 保留所有权利

### 7.29.2.9 vwprintf 函数

概要

```c
#include <stdarg.h>
#include <wchar.h>
int vwprintf(const wchar_t * restrict format, va_list arg);
```

描述

`vwprintf` 函数等同于 `wprintf`，将变长参数列表替换为 `arg`，`arg` 应由 `va_start` 宏（以及可能的 `va_arg` 调用）初始化。`vwprintf` 函数不调用 `va_end` 宏。

返回值

`vwprintf` 函数返回传输的宽字符数；如果发生输出或编码错误，则返回负值。

### 7.29.2.10 vwscanaf 函数

概要

```c
#include <stdarg.h>
#include <wchar.h>
int vwscanaf(const wchar_t * restrict format, va_list arg);
```

描述

`vwscanaf` 函数等同于 `wscanf`，将变长参数列表替换为 `arg`，`arg` 应由 `va_start` 宏（以及可能的 `va_arg` 调用）初始化。`vwscanaf` 函数不调用 `va_end` 宏。

返回值

如果在第一次转换（如果有）完成之前发生输入失败，`vwscanaf` 函数返回宏 `EOF` 的值。否则，`vwscanaf` 函数返回分配的输入数量，在提前匹配失败的情况下，该数量可以少于提供的数量甚至是零。

### 7.29.2.11 wprintf 函数

概要

```c
#include <wchar.h>
int wprintf(const wchar_t * restrict format, ...);
```

描述

`wprintf` 函数等同于 `fwprintf`，在 `wprintf` 的参数之前插入了 `stdout`。

返回值

`wprintf` 函数返回传输的宽字符数；如果发生输入或编码错误，则返回负值。

### 7.29.2.12 wscanf 函数

概要

```c
#include <wchar.h>
int wscanf(const wchar_t * restrict format, ...);
```

描述

`wscanf` 函数等同于 `fwscanf`，在 `wscanf` 的参数之前插入了 `stdin`。

返回值

如果在第一次转换（如果有）完成之前发生输入失败，`wscanf` 函数返回宏 `EOF` 的值。否则，`wscanf` 函数返回分配的输入数量，在提前匹配失败的情况下，该数量可以少于提供的数量甚至是零。

## 7.29.3 宽字符输入输出函数

### 7.29.3.1 fgetwc 函数

概要

```c
#include <stdio.h>
#include <wchar.h>
wint_t fgetwc(FILE *stream);
```

描述

如果由 `stream` 指向的输入流结束指示未设置且存在下一个字符，`fgetwc` 函数获取该字符并作为 `wchar_t` 转换为 `wint_t`，并推进与流相关的的文件位置指示（定义）。

# ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – 版权所有

## 返回值

如果流的文件结束指示符被设置，或者该流已到达文件结束，则该流的文件结束指示符被设置，且 `fgetwc` 函数从由 `stream` 指向的输入流返回下一个宽字符。如果发生读取错误，则流的错误指示器被设置，`fgetwc` 函数返回 `WEOF`。如果发生编码错误（包括字节不足），宏 `ESEQ` 的值被设置在 `errno` 中，`fgetwc` 函数返回 `WEOF`。³34

> 341 可以通过 `feof` 和 `error` 函数区分文件结束和读取错误。此外，只有当发生编码错误时，输入/输出函数才会将 `errno` 设置为 `ESEQ`。

## 7.29.3.2 fgetwc 函数

字体 概要

```
#include <stdio.h>
```
