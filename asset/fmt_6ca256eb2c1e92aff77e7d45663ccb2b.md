
`retval` 和 `src` 都为空指针。如果 `dst` 不是空指针，则 `len` 和 `dtmax` 都不大于 `SIZE_MAX/sizeof(wchar_t)`。如果 `dst` 不是空指针，则 `dtmax` 等于 0。如果 `dst` 不是空指针且小于 `len`，则在 `src` 指向的数组的前多字节字符内会出现空字符。

如果发生运行时约束违反，`mbtowcs_s` 执行以下操作：如果 `retval` 不是空指针，`mbtowcs_s` 将 `retval` 设置为 `(size_t)(-1)`。如果 `dst` 不是空指针且 `dtmax` 大于且小于 `SIZE_MAX/sizeof(wchar_t)`，则 `mbtowcs_s` 将 `dst[0]` 设置为宽字符。

### 描述 (Description)

`mbtowcs_s` 函数将从 `src` 数组初始状态开始的多字节字符序列转换为相应的宽字符序列。如果 `dst` 不是空指针，转换后的字符存储在 `dst` 指向的数组中。转换持续直到遇到以下情况：遇到无法形成有效多字节字符的字节序列，或者（当 `dst` 不是空指针时）宽字符存储在 `dst` 指向的数组中⁴⁸⁰ 如果 `dst` 是空指针，`len` 的值被忽略。如果 `dst` 不是空指针且未在 `dst` 指向的数组中存储空字符，则 `dst[dtmax]` 被设置为宽字符。每次转换的发生都如同调用了 `mbtowc` 一样。

无论 `dst` 是否为空指针，如果输入转换了无法形成有效多字节字符的字节序列，则会发生错误代码：`mbtowcs_s` 函数在 `retval` 中存储值 `(size_t)(-1)`。否则，`mbtowcs_s` 返回成功转换的多字节字符数，不包括终止空字符（如果有）。

当 `mbtowcs_s` 在 `dst` 指向的长度为 `dtmax` 的宽字符数组中写入终止空字符之后的所有元素，其值是不确定的。

## 返回 (Returns)

`mbtowcs_s` 函数成功时返回 0，如果发生运行时约束违反或 `src` 不对应有效的多字节字符，则返回非零值。

# ISO/IEC 9899:2024(en)

返回<sup>467</sup>

如果在重叠的对象之间进行拷贝，这些对象将变为未指定的值。

返回值

如果没有发生运行时约束违反且没有发生编码错误，`mbstows_s` 函数返回零。否则，返回非零值。

# K.3.6.6.3 mbstows_s 函数

# 概要

```
#include <stdlib.h>
errno_t mbstows_s(size_t *restrict retrieval, char *restrict dst, size_t dmax,
                const char *restrict src, size_t len);
```

# 运行时约束

`retval` 和 `src` 均不能为空指针。如果 `dst` 不是空指针，则 `len` 必须大于 `RSIZE_MAX/sizeof(char_t)`，且 `dmax` 必须为非零且不大于 `RSIZE_MAX`。如果 `dst` 是空指针，则 `dmax` 必须为零。如果 `dst` 不是空指针且 `len` 小于 `dmax`，则转换已经停止（见下文），因为遇到了终止空空字符或发生了编码错误。

如果发生运行时约束违反，`mbstows_s` 返回零。如果 `retval` 不是空指针，则 `mbstows_s` 将 `*retval` 设置为 `(size_t)(-1)`。如果 `dst` 不是空指针且 `dmax` 大于零且不大于 `RSIZE_MAX`，则 `mbstows_s` 将 `dst[0]` 设置为空字符。

# 描述

`mbstows_s` 函数将由 `src` 指向的数组的多字节字符序列转换为从初始偏移状态开始的多字节字符序列。如果 `dst` 不是空指针，则转换后的字符被存储在 `dst` 指向的数组中。转换将持续到并包括终止空字符，该字符也会被存储。转换在以下两种情况下提前停止：

- 当遇到不对应有效多字节字符的字符时；
- （如果 `dst` 不是空指针）下一个多字节字符将超过 `dst` 指向的数组可存储的 `n` 总字节数限制。如果正在转换的宽字符是空字符，则 `n` 小于 `len` 或 `dmax`。

如果转换停止时没有写入空字符且 `dst` 不是空指针，则会在已存储的任何多字节字符之后立即在 `dst` 中存储一个空字符。每次转换的发生就像通过 `wcrtomb` 函数<sup>478</sup>一样。

无论 `dst` 是否为空指针，如果输入转换遇到一个不对应有效多字节字符的宽字符，则会发生编码错误：函数将值 `(-1)` 设置到 `*retval`。否则，`mbstows_s` 函数返回生成的多字节字符序列的字节数，包括终止空字符（任何的话）。

终止空字符之后的所有元素（任何的话）在 `mbstows_s` 的 `dst` 指向的具有 `dmax` 个元素的数组中被设置为未指定的值，当 `mbstows_s` 返回<sup>479</sup>。

如果在重叠的对象之间进行拷贝，这些对象将变为未指定的值。

<sup>477</sup>这允许实现在发现没有发生终止空字符之前尝试转换多字节字符串。

<sup>478</sup>如果因为遇到终止空字符而停止转换，则存储的字节包括在空字节之前为了到达初始偏移状态所需的字节。如果转换在遇到终止空宽字符之前停止，则结果将是的，但可能不在初始偏移状态。

<sup>479</sup>如果 `len` 小于 `dmax`，实现在可以在发现运行时约束违反之前限制数组。

ISO/IEC 2024 - 版权所有

657

# ISO/IEC 9899:2024(en)

返回值

如果没有运行时约束违反且没有发生编码错误，`wcstombs_s` 函数返回零。否则，返回非零值。

# K.3.7 字符串处理 <string.h>

## K.3.7.1 通用

头文件 `<string.h>` 定义了两种类型。

类型是

```
errno_t
```

类型 `int`；以及

```
size_t
```

类型 `size_t`。

# K.3.7.2 拷贝函数

## K.3.7.2.1 memcpy_s 函数

### 概要

```
#define _STDC_WANT_LIB_EXT 1
#include <string.h>
errno_t memcpy_s(void * restrict s1, size_t slmax, const void * restrict s2,
size_t n);
```

### 运行时约束

`n` 和 `s2` 均不能为空指针。`slmax` 和 `n` 均不能大于 `RSIZE_MAX`。`n` 不大于 `slmax`。不能在重叠的对象之间拷贝。

如果发生运行时约束违反，且 `s1` 不是空指针且 `slmax` 不大于 `RSIZE_MAX`，则 `memcpy_s` 在 `s1` 指向的对象的前 `slmax` 个字符中存储零。

### 描述

`memcpy_s` 函数将 `s2` 指向的 `n` 个字符拷贝到 `s1` 指向的对象中。

### 返回值

如果没有运行时约束违反，`memcpy_s` 函数返回零。否则，返回非零值。

## K.3.7.2.2 memmove_s 函数

### 概要

```
#define _STDC_WANT_LIB_EXT 1
#include <string.h>
errno_t memmove_s(void *s1, size_t slmax, const void *s2, size_t n);
```

### 运行时约束

`n` 和 `s2` 均不能为空指针。`slmax` 和 `n` 均不能大于 `RSIZE_MAX`。`n` 不大于 `slmax`。

如果发生运行时约束违反，且 `s1` 不是空指针且 `slmax` 不大于 `RSIZE_MAX`，则 `memmove_s` 在 `s1` 指向的对象的前 `slmax` 个字符中存储零。

### 描述

`memmove_s` 函数将 `s2` 指向的 `n` 个字符拷贝到 `s1` 指向的对象中。这种拷贝的发生就像首先将 `s2` 的 `n` 个字符拷贝到与 `s1` 指向的对象不重叠的临时数组，然后将临时数组的 `n` 个字符拷贝到 `s1` 指向的对象中。

### 返回值

如果没有运行时约束违反，`memmove_s` 函数返回零。否则，返回非零值。

## K.3.7.2.3 strcpy_s 函数

### 概要

```
#define _STDC_WANT_LIB_EXT 1
#include <string.h>
errno_t strcpy_s(char * restrict s1, size_t slmax, const char * restrict s2);
```

### 运行时约束

`s1` 和 `s2` 均不能为空指针。`slmax` 不大于 `RSIZE_MAX` 且不为。不能在重叠的对象之间拷贝。

如果发生运行时约束违反，且 `s1` 不是空指针且 `slmax` 大于零且不大于 `RSIZE_MAX`，则 `strcpy_s` 将 `s1[0]` 设置为空字符。

### 描述

`strcpy_s` 函数将 `s2` 指向的字符串（包括终止空字符）拷贝到 `s1` 指向的数组中。

终止空字符之后的所有元素（任何的话）在 `strcpy_s` 的 `s1` 指向的具有 `slmax` 个元素的数组中被设置为未指定的值，当 `strcpy_s` 返回<sup>490</sup>

### 返回值

如果没有运行时约束违反，`strcpy_s` 函数返回零<sup>491</sup>否则，返回非零值。

## K.3.7.2.4 strncpy_s 函数

### 概要

```
#define _STDC_WANT_LIB_EXT 1
#include <string.h>
errno_t strcpy_s(char * restrict s1, size_t slmax, const char * restrict s2,
size_t n);
```

### 运行时约束

`s1` 和 `s2` 均不能为空指针。`slmax` 不大于 `RSIZE_MAX` 且不为零。如果 `n` 不小于 `slmax`，则 `slmax` 必须大于 `strnlen(s2, s2)`，不能在重叠的对象之间拷贝。

如果发生运行时约束违反，且 `s1` 不是空指针且 `slmax` 大于零且不大于 `RSIZE_MAX`，则 `strcpy_s` 将 `s1[0]` 设置为空字符。

## ISO/IEC 9899:2024(en)

### 描述

`strncpy_s` 函数从 `s2` 指向的数组拷贝多于 `n` 个连续的字符（空字符之后的字符不被复制）到 `s1` 指向的数组。如果从 `s2` 中没有拷贝到空字符，则 `s1[n]` 被置为空字符。

当 `strncpy_s` 返回非零值时，在 `s1` 指向的长度为 `smax` 个字符的数组中，由 `strncpy_s` 写入的空字符（如果有）之后的所有元素其值都是未定义的。

### 返回

如果没有发生运行时约束违例，`strncpy_s` 函数返回零。否则，返回一个非零值。

示例：`strncpy_s` 函数可以拷贝字符串，而不会产生结果未终止或字符将位于数组末尾的危险。

```c
#define _STDC_WANT_LIB_EXT1 1
#include <string.h>
/* ... */
char src1[100] = "hello";
char src2[7] = {'g', 'o', 'o', 'd', 'b', 'y', '\0'};
char dst1[6], dst2[5];
int r1, r2, r3;
r1 = strncpy_s(dst1, 5, src1, 100);
r2 = strncpy_s(dst2, 5, src2, 7);
r3 = strncpy_s(dst3, 5, src2, 4);
```

第一次调用将 `dst0` 的值赋值给 `r1`，并将 `dst1` 赋值为序列 `hello\0`。

第二次调用将一个非零值赋值给 `r2`，并将 `dst2` 赋值为序列 `\0`。

第三次调用将 `dst2` 的值赋值给 `r3`，并将 `dst3` 赋值为序列 `good\0`。

## K.3.7 拼接函数

### K.3.7.1 strcat_s 函数

### 概要

```c
#define _STDC_WANT_LIB_EXT1 1
#include <string.h>
error_t strcat_s(char * restrict s1, size_t slmax, const char * restrict s2);
```

### 运行时约束

- 在进入 `strcat_s` 时，`n` 表示 `smax - strlen(s1)` 的值。
- `s1` 和 `s2` 均不为空指针；`slmax` 不大于 `RSIZE_MAX`；`slmax` 不为零。如果 `slmax` 不为零，则 `n` 大于 `strlen(s2)`。重叠的对象之间不进行拷贝。
- 如果发生运行时约束违例且 `s1` 不为空指针且 `slmax` 不大于 `RSIZE_MAX`，`strcat_s` 将 `s1[0]` 置为空字符。

### 描述

`strcat_s` 函数将 `s2` 指向的字符串（包括空字符）附加到 `s1` 指向的字符串的末尾。`s2` 的起始字符将覆盖 `s1` 末尾的空字符。

这允许实现在检查这些字符是否为空字符的同时，将 `s2` 拷贝到 `s1`。在发现第一个元素是空字符之前，向 `s1` 的每个元素写入字符。

零值表示 `s2` 指向的字符串中的所有请求字符都位于 `s1` 指向的数组内，且结果已终止。

在进入 `strcat_s` 时，`s1` 未终止。

当 `strcat_s` 返回时，在 `s1` 指向的 `smax` 个字符数组中，由 `strcat_s` 写入的终止空字符（如果有）之后的所有元素值都是未指定的。

### 返回

如果没有发生运行时约束违例，`strcat_s` 函数返回零。否则，返回一个非零值。

### K.3.7.2 strcat_s 函数

### 概要

```c
#define _STDC_WANT_LIB_EXT1 1
#include <string.h>
error_t strcat_s(char * restrict s1, size_t slmax, const char * restrict s2,
size_t n);
```

### 运行时约束

在进入 `strcat_s` 时，`m` 表示 `slmax - strlen(s1)` 的值。

- `s1` 和 `s2` 均不为空指针；`slmax` 和 `n` 均不大于 `RSIZE_MAX`；`slmax` 不为零。如果 `n` 小于 `m`，则 `m` 大于 `strlen(s2)`。重叠的对象之间不进行拷贝。

如果发生运行时约束违例且 `s1` 不为空指针且 `slmax` 不大于 `RSIZE_MAX`，`strcat_s` 将 `s1[0]` 置为空字符。

### 描述

`strcat_s` 函数从 `s2` 指向的数组附加最多 `n` 个字符（空字符之后的字符不拷贝）到 `s1` 指向的字符串的末尾。`s2` 的起始字符覆盖 `s1` 末尾的空字符。如果从 `s2` 中没有拷贝到空字符，则 `s1[slmax - m + n]` 被置为空字符。

当 `strcat_s` 返回时，在 `s1` 指向的 `smax` 个字符数组中，由 `strcat_s` 写入的终止空字符（如果有）之后的所有元素值未指定。

### 返回

如果没有发生运行时约束违例，`strcat_s` 函数返回零。否则，返回一个非零值。

示例：`strcat_s` 函数可以拷贝字符串，而不会产生结果未终止或字符将位于数组末尾的危险。

```c
#define _STDC_WANT_LIB_EXT1 1
#include <string.h>
/* ... */
char s1[100] = "good";
char s2[6] = "hello";
char s3[6] = "hello";
char s4[6] = "abc";
int r1, r2, r3;
size_t n;
strcat_s(s1, 100, s2, n);
strcat_s(s2, 6, s3, n);
strcat_s(s3, 6, s4, n);
```

第一次调用将 `dst0` 的值赋值给 `r1`，并将 `dst1` 赋值为序列 `hello\0`。

第二次调用将一个非零值赋值给 `r2`，并将 `dst2` 赋值为序列 `\0`。

第三次调用将 `dst2` 的值赋值给 `r3`，并将 `dst3` 赋值为序列 `good\0`。

## K.3.7.4 查找函数

### K.3.7.4.1 strtok_s 函数

### 概要

```c
#define _STDC_WANT_LIB_EXT1 1
#include <string.h>
char *strtok_s(char *restrict s1, size_t slmax, const char *restrict s2, char *restrict ptr);
```

### 运行时约束

`s1`、`s2` 或 `ptr` 均不能为空指针。如果 `s1` 为空指针，则 `*ptr` 不能为空指针。`slmax` 的值不大于 `SIZE_MAX`。对于第一次调用，标记的结束应出现在 `s1` 的前 `slmax` 个字符内；对于后续调用，应出现在前 `slmax` 个字符内。

如果发生运行时约束违例，`strtok_s` 函数不修改 `s1` 或 `s2` 指针，且不在 `ptr` 指向的对象中存储值。

### 描述

一系列 `strtok_s` 调用将 `s1` 指向的字符串拆分为一系列标记，每个标记都由 `s2` 指向的字符串中的字符分隔。第二个参数指向调用者提供的进入字符串的字符指针，`strtok` 函数在该处存储其继续扫描同一字符串所需的信息。

序列中的第一次调用第一个参数不为空指针，且 `slmax` 指向一个对象，其值为字符数组的元素个数。第一次调用在 `ptr` 指向的对象中存储一个初始值，并更新 `slmax` 为剩余元素个数。序列中的后续调用第一个参数为空指针，且要求 `slmax` 和 `ptr` 指向的对象具有由序列中上一次调用存储的值。`s2` 指向的隔符字符串在调用之间可以不同。

序列中的第一次调用在 `s1` 指向的字符串中查找第一个不包含在当前 `s2` 指向的隔符字符串中的字符。如果没有找到这样的字符，则 `strtok_s` 函数返回空指针。如果找到了这样的字符，它就是第一个标记的开始。
