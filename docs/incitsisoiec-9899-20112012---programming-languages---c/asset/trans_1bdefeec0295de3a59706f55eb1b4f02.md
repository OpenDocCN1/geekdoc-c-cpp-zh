

对应于 %s 标识符的 snprintf_s 不得为空指针。不应发生编码错误。

如果发生运行时约束违反，且 s 不为空指针且 n 大于 0 且小于 RSIZE_MAX，则 snprintf_s 函数将 s[0] 设置为空字符。

## 描述

`snprintf_s` 函数与 `snprintf` 函数等效，但上述列出的显式运行时约束除外。

`snprintf_s` 函数与 `sprintf_s` 不同，它会将结果截断以适应由 s 指向的数组。

## 返回值

`snprintf_s` 函数返回如果 n 足够大时本应写入的字符数（不包括终止符 `\0`），或者在发生运行时约束违反时返回一个负值。因此，如果 n 为 0 或返回值非负且小于 n，则空终止符的输出已完全写入。

## K.3.5.3.6  sprintf_s 函数

### 概要

```
#define STDC_WANT_LIB_EXT1__ 1
#include <stdio.h>
int sprintf_s(char * restrict s, rsize_t n,
const char * restrict format, ...);
```

### 运行时约束

s 和 format 均不得为空指针。n 不等于 0 且不大于 RSIZE_MAX。结果写入 s 指向的数组所需的字符数（包括末尾空字符）不得大于 n。%n 标识符396（无论是否被标志、字段宽度或精度修改）不得出现在 format 指向的字符串中。`sprintf_s` 中对应于 %s 标识符的任何参数不得为空指针。不应发生编码错误。

395) 当 format 指向的字符串中顺序出现字符 %n 且这些字符不被解释为 %n 标识符时，这不属于运行时约束违反。例如，如果整个格式字符串为 %n。

396) 当 format 指向的字符串中顺序出现字符 %n 且这些字符不被解释为 %n 标识符时，这不属于运行时约束违反。例如，如果整个格式字符串为 %n。

如果发生运行时约束违反，且 s 不为空指针且 n 大于 0 且小于 RSIZE_MAX，则 `sprintf_s` 函数将 s[0] 设置为空字符。

## 描述

`sprintf_s` 函数与 `sprintf` 函数等效，但参数 n 以及上述列出的显式运行时约束除外。

`sprintf_s` 函数与 `snprintf_s` 不同，它将对于 s 指向数组过大的结果视为运行时约束违反。

## 返回值

如果没有发生运行时约束违反，`sprintf_s` 返回写入数组的字符数，不包括终止空字符。如果发生编码错误，`sprintf_s` 返回负值。如果发生任何其他运行时约束违反，`sprintf_s` 返回零。

## K.3.5.3.7 scanf_s 函数

### 概要

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <stdio.h>
int scanf_s(const char * restrict s,
const char * restrict format, ...);
```

### 运行时约束

s 和 format 均不得为空指针。用于存储转换后输入的任何间接参数不得为空指针。

如果发生运行时约束违反，`scanf_s` 函数将不再尝试执行输入，且在发现运行时约束违反之前 `scanf_s` 执行了多少输入是不确定的。

## 描述

`scanf_s` 函数与 `fscanf_s` 等效，但输入是从字符串（由参数 s 指定）而不是流获取。到达结尾等同于 `fscanf_s` 遇到文件结束（EOF）。如果在重叠的对象之间发生拷贝，则对象的行为是未定义的。

## 返回值

如果在任何转换之前发生失败或存在运行时约束违反，`scanf_s` 函数返回宏 `EOF` 的值。否则，`scanf_s` 返回分配的输入项数量，在提前匹配失败的情况下，该数量可能少于提供的数量，甚至为零。

## K.3.5.3.8 vfprintf_s 函数

### 概要

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <stdarg.h>
#include <stdio.h>
int vfprintf_s (FILE * restrict stream,
const char * restrict format,
va_list arg);
```

### 运行时约束

stream 和 format 均不得为空指针。%n 标识符397（无论是否被标志、字段宽度或精度修改）不得出现在 format 指向的字符串中。`vfprintf_s` 中对应于 %s 标识符的任何参数不得为空指针。

如果发生运行时约束违反，`vfprintf_s` 函数将不再尝试产生进一步输出，且在发现运行时约束违反之前 `vfprintf_s` 产生了输出是不确定的。

## 描述

`vfprintf_s` 函数与 `vfprintf` 函数等效，但上述列出的显式运行时约束除外。

## 返回值

`vfprintf_s` 函数返回传输的字符数，如果发生输出错误、编码错误或运行时约束违反，则返回负值。

## K.3.5.3.9 vscanff_s 函数

### 概要

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <stdarg.h>
#include <stdio.h>
int vfprintf_s (FILE * restrict stream,
const char * restrict format,
va_list arg);
```

397) 当 format 指向的字符串中顺序出现字符 %n 且这些字符不被解释为 %n 标识符时，这不属于运行时约束违反。例如，如果整个格式字符串为 %n。

stream 和 format 均不得为空指针。用于存储转换后输入的任何间接参数不得为空指针。

如果发生运行时约束违反，`vscanf_s` 函数将不再尝试执行输入，且在发现运行时约束违反之前 `vscanf_s` 执行了多少输入是不确定的。

## 描述

`vscanf_s` 函数与 `fscanf_s` 等效，变参数列表替换为 `arg`，该列表应由 `va_start` 宏初始化（以及可能的 `va_arg` 调用）。

## 返回值

如果在任何转换之前发生失败或存在运行时约束违反，`vscanf_s` 返回宏 `EOF` 的值。否则，`vscanf_s` 返回分配的输入项数量，在提前匹配失败的情况下，该数量可能少于提供的数量，甚至为零。

## K.3.5.3.10 vprintf_f 函数

### 概要

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <stdarg.h>
#include <stdio.h>
int vprintf_f(const char * restrict format,
va_list arg);
```

### 运行时约束

format 不得为空指针。%n 标识符399（无论是否被标志、字段宽度或精度修改）不得出现在 format 指向的字符串中。`vprintf_f` 中对应于 %s 标识符的任何参数不得为空指针。

如果发生运行时约束违反，`vprintf_f` 函数将不再尝试产生进一步输出，且在发现运行时约束违反之前 `vprintf_f` 产生了输出是不确定的。

398) 由于 `vprintf_f`、`vscanf_s`、`vprintf_s`、`vscanf_s`、`vsnprintf_f`、`vsprintf_s` 调用 `va_arg` 宏，`arg` 的值是不确定的。

399) 当 format 字符串中顺序出现字符 % 且这些字符不被解释为 %n 标识符时，这不属于运行时约束违反。例如，如果整个格式字符串为 %%。

## 描述

`vprintf_s` 函数与 `vprintf` 函数等效，但上述列出的显式运行时约束除外。

## 返回值

`vprintf_s` 函数返回传输的字符数，如果发生输出错误、编码错误或运行时约束违反，则返回负值。

## K.3.5.3.11 vscanf_s 函数

### 概要

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <stdarg.h>
#include <stdio.h>
int vscanf_s(const char * restrict format, va_list arg);
```

### 运行时约束

format 不得为空指针。用于存储转换后输入的任何间接参数不得为空指针。

如果发生运行时约束违反，`vscanf_s` 函数将不再尝试执行输入，且在发现运行时约束违反之前 `vscanf_s` 执行了多少输入是不确定的。

## 描述

`vscanf_s` 函数与 `fscanf_s` 等效，变参数列表替换为 `arg`，该列表应由 `va_start` 宏初始化（以及可能的 `va_arg` 调用）。`vscanf_s` 不调用 `va_end` 宏。

## 返回值

如果在任何转换之前发生输入失败或存在运行时约束违反，`vscanf_s` 返回宏 `EOF` 的值。

