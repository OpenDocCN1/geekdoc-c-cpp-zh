

# ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – 保留所有权利

输入行：

25 54.32E-1 thompson

将给 n 赋值为 3，将 i 赋值为 25，将 x 赋值为 5.432，并将序列命名为 thom。

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

将给 i 赋值为 56，将 x 赋值为 789.0，跳过 0123，并将 y 赋值为 56.0。从输入流中读取的下一个字符将是 a。

前向引用：wcstod、wcstof 和 wcstold 函数 (72.29.4.1.1)，wcstol、wcstoll、wcstoul 和 wcstll 函数 (72.29.4.1.2)，wcrtomb 函数 (72.29.6.3.3)。

## 79.29.3 sprintf 函数

概要

- 1 #include <wchar.h>
int swprintf(wchar_t * restrict s, size_t n,
const wchar_t * restrict format, ...);

描述

- 2 sprintf 函数等同于 fwprintf，不同之处在于参数指定了一个用于写入生成输出宽字符数组，而不是写入到流。写入的宽字符不超过 n 个，其中包含一个总是添加的终止空字符（当 n 为零时）。

返回值

- 3 sprintf 函数返回写入数组的宽字符数，不计入终止空字符；如果发生编码错误，或者请求生成 n 或更多宽字符，则返回负值。

库

§ 79.29.2

### 7.29.2.4 swscancf 函数

概要

```c
#include <wchar.h>
int swscancf(const wchar_t * restrict s,
const wchar_t * restrict format, ...);
```

描述

swscancf 函数等同于 fwscancf，不同之处在于参数 s 指定了一个从其中获取输入的宽字符串，而不是从流。到达宽字符串的末尾等同于 fwscancf 函数遇到文件结束符（EOF）。

返回值

如果在第一次转换（如果有）完成之前发生输入失败，swscancf 函数返回宏 EOF 的值。否则，swscancf 函数返回分配的输入数量，在提前匹配失败的情况下，该数量可以少于提供的数量甚至是零。

### 7.29.2.5 vfwprintf 函数

概要

```c
#include <stdarg.h>
#include <stdio.h>
#include <wchar.h>
int vfwprintf(FILE * restrict stream,
 wchar_t * restrict format,
va_list arg);
```

描述

vfwprintf 函数等同于 fwprintf，将变长参数列表替换为 arg，arg 应由 va_start 宏（以及可能的后续 va_arg 调用）初始化。vfwprintf 函数不调用 va_end 宏。

返回值

vfwprintf 函数返回传输的宽字符数；如果发生输出或编码错误，则返回负值。

> 340) 由于函数 vfwprintf、vswprintf、vfwscancf、vfwprintf、swscancf 和 vswancf 调用了 va_arg 宏，返回值是不确定的。

# ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – 保留所有权利

- 4 示例显示了在通用错误例程中使用 vfwprintf 函数。

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

vfwscanf 函数等同于 vfwscanf，将变长参数列表替换为 va_start 宏（以及可能的 va_arg 调用）。

返回值

如果在第一次转换（如果有）完成之前发生输入失败，vfwscanf 函数返回宏 EOF 的值。否则，vfwscanf 函数返回分配的输入数量，在提前匹配失败的情况下，该数量可以少于提供的数量甚至是零。

### 7.29.2.7 vswprintf 函数

概要

```c
#include <stdarg.h>
#include <wchar.h>
int vswprintf(wchar_t * restrict s,
size_t n,
const wchar_t * restrict format,
va_list arg);
```

描述

vswprintf 函数等同于 swprintf，将变长参数列表替换为 arg，arg 应由 va_start 宏（以及可能的 va_arg 调用）初始化。vswprintf 函数不调用 va_end 宏。

返回值

vswprintf 函数返回写入数组的宽字符数，不计终止空字符；如果发生编码错误或请求生成 n 或更多宽字符，则返回负值。

### 7.29.2.8 vswcanf 函数

概要

```c
#include <stdarg.h>
#include <wchar.h>
int vswcanf(const wchar_t * restrict s,
const wchar_t * restrict format,
va_list arg);
```

描述

vswcanf 函数等同于 swscanf，将变长参数列表替换为 arg，arg 应由 va_start 宏（以及可能的 va_arg 调用）初始化。vswcanf 函数不调用 va_end 宏。

返回值

如果在第一次转换（如果有）完成之前发生输入失败，vswcanf 函数返回宏 EOF 的值。否则，vswcanf 函数返回分配的输入数量，在提前匹配失败的情况下，该数量可以少于提供的数量甚至是零。

# ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – 保留所有权利

### 7.29.2.9 vwprintf 函数

概要

```c
#include <stdarg.h>
#include <wchar.h>
int vwprintf(const wchar_t * restrict format,
va_list arg);
```

描述

vwprintf 函数等同于 wprintf，将变长参数列表替换为 arg，arg 应由 va_start 宏（以及可能的 va_arg 调用）初始化。vwprintf 函数不调用 va_end 宏。

返回值

vwprintf 函数返回传输的宽字符数；如果发生输出或编码错误，则返回负值。

### 7.29.2.10 vwscanaf 函数

概要

```c
#include <stdarg.h>
#include <wchar.h>
int vwscanaf(const wchar_t * restrict format,
va_list arg);
```

描述

vwscanaf 函数等同于 wscanf，将变长参数列表替换为 arg，arg 应由 va_start 宏（以及可能的 va_arg 调用）初始化。vwscanaf 函数不调用 va_end 宏。

返回值

如果在第一次转换（如果有）完成之前发生输入失败，vwscanaf 函数返回宏 EOF 的值。否则，vwscanaf 函数返回分配的输入数量，在提前匹配失败的情况下，该数量可以少于提供的数量甚至是零。

### 7.29.2.11 wprintf 函数

概要

```c
#include <wchar.h>
int wprintf(const wchar_t * restrict format, ...);
```

描述

wprintf 函数等同于 fwprintf，在 wprintf 的参数之前插入了 stdout。

返回值

wprintf 函数返回传输的宽字符数；如果发生输入或编码错误，则返回负值。

### 7.29.2.12 wscanf 函数

概要

```c
#include <wchar.h>
int wscanf(const wchar_t * restrict format, ...);
```

描述

wscanf 函数等同于 fwscanf，在 wscanf 的参数之前插入了 stdin。

返回值

如果在第一次转换（如果有）完成之前发生输入失败，wscanf 函数返回宏 EOF 的值。否则，wscanf 函数返回分配的输入数量，在提前匹配失败的情况下，该数量可以少于提供的数量甚至是零。

## 7.29.3 宽字符输入输出函数

### 7.29.3.1 fgetwc 函数

概要

```c
#include <stdio.h>
#include <wchar.h>
wint_t fgetwc(FILE *stream);
```

描述

如果由 stream 指向的输入流结束指示未设置且存在下一个字符，fgetwc 函数获取该字符并作为 wchar_t 转换为 wint_t，并推进与流相关的的文件位置指示（定义）。

