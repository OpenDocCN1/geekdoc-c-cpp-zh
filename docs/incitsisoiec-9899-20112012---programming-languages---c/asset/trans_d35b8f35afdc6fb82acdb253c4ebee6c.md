

精度不应出现在 format 指向的宽字符串中。`snprintf_f` 中对应于 %s 格式说明的任何参数都不应为空指针。不应发生编码错误。

如果发生运行时约束违反，且 `s` 不是空指针且 `n` 大于0 且小于 `RSIZE_MAX`，则 `snprintf_f` 函数将 `s[0]` 设置为空字符。

# 描述

`snprintf_f` 函数与 `swprintf` 函数等，上述列出的明确运行时约束除外。

`snprintf_s` 与 `swprintf_f` 不同，会将结果截断以适应 `s` 指向的数组。

# 返回

`snprintf_f` 函数返回如果 `n` 足够大时将写入的宽字符数（不包括终止空字符），或者在发生运行时约束违反时返回一个负值。因此，当且仅当返回值非负且小于 `n` 时，空终止的输出才被完全写入。

## K.3.9.1.4 The swprintf_f function

# 概要

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <wchar.h>
int swprintf_f(wchar_t * restrict s, rsize_t n,
const wchar_t * restrict format, ...);
```

# 运行时约束

`s` 和 `format` 均不能为空指针。`n` 既不等于0也不大于 `RSIZE_MAX`。将结果写入 `s` 指向的数组所需的宽字符数（包括末尾空字符）不应大于 `n`。`%n` 格式说明(433)（无论是否被标志、字段宽度或精度修改）不应出现在 `format` 指向的宽字符串中。`swprintf_f` 中对应于 %s 格式说明的任何参数都不应为空指针。不应发生编码错误。

432) 当宽字符 `%n` 连续出现在 `format` 指向的宽字符串中，且这些字符不被解释为 `%n` 格式说明时，不属于运行时约束违反。例如，如果整个字符串为 `L"%nn"`。

433) 当宽字符 `%n` 连续出现在 `format` 指向的宽字符串中，且这些字符不被解释为 `%n` 格式说明时，不属于运行时约束违反。例如，如果整个字符串为 `L"%nn"`。

如果发生运行时约束违反，且 `s` 不是空指针且 `n` 大于0 且小于 `RSIZE_MAX`，则 `swprintf_f` 函数将 `s[0]` 设置为空字符。

# 描述

`swprintf_f` 函数与 `swprintf` 函数等，上述列出的明确运行时约束除外。

`swprintf_s` 与 `swprintf_f` 不同，将对于 `s` 指向的数组过大的结果视为运行时约束违反。

# 返回

如果没有发生运行时约束违反，`swprintf_s` 函数返回写入数组的宽字符数，不包括空字符。如果发生编码错误或请求写入 `n` 或更多宽字符，`swprintf_s` 返回一个负值。如果发生任何其他运行时约束违反，`swprintf_s` 返回零。

## K.3.9.1.5 The scanf_s function

# 概要

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <wchar.h>
int swscanf_s(const wchar_t * restrict s,
              wchar_t * restrict format, ...);
```

# 运行时约束

`s` 和 `format` 均不能为空指针。任何用于存储转换后输入的参数都不应为空指针。

如果发生运行时约束违反，`swscanf_s` 函数不尝试执行输入，且 `swscanf_s` 在发现运行时约束违反之前执行了多少输入未定义。

# 描述

`swscanf_s` 函数与 `fwscanf_s` 等，不同之处参数指定的是用于获取输入的宽字符串，而不是流。到达宽字符串的末尾等于 `swscanf_s` 函数遇到文件结束（EOF）。

# 返回

如果发生输入失败或存在运行时约束违反，`swscanf_s` 函数返回宏 `EOF` 的值。否则，`swscanf_s` 返回分配的项目数，在提前匹配失败的情况下，该数量可能少于提供的数量，甚至为零。

## K.3.9.1.6 The vfwprintf_s function

# 概要

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <stdarg.h>
#include <stdio.h>
#include <wchar.h>
int vfwprintf_s(FILE * restrict stream,
const wchar_t * restrict format,
va_list arg);
```

# 运行时约束

`stream` 和 `format` 均不能为空指针。`%n` 格式说明(434)（无论是否被标志、字段宽度或精度修改）不应出现在指向 `format` 的宽字符串中。`vfwprintf_s` 中对应于 %s 格式说明的任何参数都不应为空指针。

如果发生运行时约束违反，`vfwprintf_s` 函数不尝试产生进一步输出，且 `vfwprintf_s` 在发现运行时约束违反之前产生了多少输出未定义。

# 描述

`vfwprintf_s` 函数与 `vprintf` 函数等，上述列出的明确运行时约束除外。

# 返回

`vfwprintf_s` 函数返回宽字符数，如果发生输出错误、编码错误或运行时约束违反，则返回负值。

## K.3.9.1.7 The vfwscanf_s function

# 概要

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <stdarg.h>
#include <stdio.h>
#include <wchar.h>
int vfwscanf_s(FILE * restrict stream,
const wchar_t * restrict format, va_list arg);
```

434) 当宽字符 `%n` 连续出现在 `format` 指向的宽字符串中，且这些字符不被解释为 `%n` 格式说明时，不属于运行时约束违反。例如，如果整个格式字符串为 `L"%nn"`。

# 运行时约束

`stream` 和 `format` 均不能为空指针。任何用于存储转换后输入的参数都不应为空指针。

如果发生运行时约束违反，`vfwscanf_s` 函数不尝试执行进一步输入，且 `vfwscanf_s` 在发现运行时约束违反之前执行了多少输入未定义。

# 描述

`vfwscanf_s` 函数与 `vscanf_s` 等，变变参数列表替换为 `arg`，该 `arg` 应当已由 `va_start` 宏初始化（并可能通过 `va_arg` 调用）。`vfwscanf_s` 函数不调用 `va_end` 宏。

# 返回

如果在转换前发生输入失败或存在运行时约束违反，`vfwscanf_s` 返回宏 `EOF` 的值。否则，`vfwscanf_s` 返回分配的项目数，在匹配失败的情况下可能少于提供的数量，甚至为零。

## K.3.9.1.8 The vswprintf_s function

# 概要

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <stdarg.h>
#include <wchar.h>
int vswprintf_s(wchar_t * restrict s,
size_t n,
               const wchar_t * restrict format,
               va_list arg);
```

# 运行时约束

`s` 和 `format` 不能为空指针。`n` 不应大于 `RSIZE_MAX`。`%n` 格式说明(435)（无论是否被标志、字段宽度或精度修改）不应出现在指向 `format` 的宽字符串中。`vswprintf_s` 中对应于 %s 格式说明的任何参数都不应为空指针。不应发生编码错误。

435) 由于函数 `vfwscanf_s`、`vfwscanf_s` 和 `vswscanf_s` 调用了 `va_arg` 宏，返回后 `arg` 的值是不定的。

436) 当宽字符 `%n` 连续出现在指向 `format` 的宽字符串中，且这些字符不被解释为 `%n` 格式说明时，不属于运行时约束违反。例如，如果整个字符串为 `L"%nn"`。

如果发生运行时约束违反，且 `s` 不是空指针且 `n` 大于0 且小于 `RSIZE_MAX`，则 `vsprintf_f` 函数将 `s[0]` 设置为空宽字符。

# 描述

`vsprintf_f` 函数与 `vprintf` 函数等，上述运行时约束除外。

`vsprintf_f` 函数与 `vsprintf_f` 不同，会将结果截断以适应 `s` 指向的数组。（注：原文此处可能误笔，应为 vswprintf_s 对比 vsprintf_f）

# 返回

`vsprintf_f` 函数返回如果 `n` 足够大时将写入的宽字符数（不包括终止空字符），或者在发生运行时约束违反时返回一个负值。因此，当且仅当返回值非负且小于 `n` 时，空终止的输出才被完全写入。

## K.3.9.1.9 The vsprintf_f function

# 概要

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <stdio.h>
#include <wchar.h>
int vsprintf_f(wchar_t * restrict s,
rsize_t n,
const wchar_t * restrict format,
va_list arg);
```

# 运行时约束

`s` 和 `format` 都不能为空指针。`n` 既不等于0也不大于 `RSIZE_MAX`。将结果写入 `s` 指向的数组所需的宽字符数（包括末尾空字符）不应大于 `n`。`%n` 格式说明(437)（无论是否被标志、字段宽度或精度修改）不应出现在 `format` 指向的宽字符串中。`vsprintf_f` 中对应于 %s 格式说明的任何参数都不应为空指针。不应发生编码错误。

