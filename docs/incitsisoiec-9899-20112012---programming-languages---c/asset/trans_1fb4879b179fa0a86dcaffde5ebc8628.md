
小于 m，m 应大于 `strlen_s(s2, m)`。拷贝操作不应发生在重叠的对象之间。

4 如果发生运行时约束违反，如果 s1 不是指针且 smax 大于 0 且不超过 RSIZE_MAX，则 `strcat_s` 将 s1[0] 设置为空字符。

# 描述

5 `strcat_s` 函数将数组 `s2` 中多于 `n` 个连续的字符（空字符之后的字符不被复制）从 `s2` 追加到 s1 所指向的字符串末尾。来自 `s2` 的起始字符将覆盖 s1 末尾的空字符。如果没有从 `s2` 拷贝空字符，则 `s1[slmax-m+n]` 将被设置为空字符。

6 当 `strcat_s` 在指向 s1 的 `slmax` 字符数组中写入终止空字符（如果有的话）之后的所有元素，这些元素在 `strcat_s` 返回时将具有未定义的值。426)

# 返回

7 如果没有发生运行时约束违反，`strcat_s` 函数返回零^{427}。否则，返回非零值。

8 示例 1 `strcat_s` 函数可以用于拷贝字符串，而不会产生结果未终止或超出目标数组边界的危险。

```
#define _STDC_WANT_LIB_EXT1__ 1
#include <string.h>
/* ... */
char s1[1000] = "good";
char s2[6] = "hello";
char s3[6] = "hello";
char s4[7] = "abc";
char s5[1000] = "bye";
int r1, r2, r3, r4;
r1 = strcat_s(s1, 100, s5, 1000);
r2 = strcat_s(s2, "", 1);
r3 = strcat_s(s3, "X", 2);
r4 = strcat_s(s4, 7, "defghijklmn", 3);
```

> 425) 零意味着在进入 `strcat_s` 时 s1 未终止。

> 426) 这允许实现在将来自 s2 的字符追加到 s1 的同时，检查这些字符中是否有空字符。这种方法可能会在发现第一个元素被设置为空字符之前，向 s1 的每个元素写入一个字符。

> 427) 返回值零意味着从 s2 所指向的字符串中请求的任何字符已追加到 s1 所指向的字符串中，且 s1 中的结果是空终止的。

在第二次调用后，`r2` 的值为零，s2 将包含序列 `hello\0`。在第三次调用后，`r3` 为非零值，s3 将包含序列 `abcdef\0`。在第四次调用后，`r4` 的值为零，s4 将包含序列 `abcdef\0`。

# K.3.7.3 搜索函数

### K.3.7.3.1 `strtok_s` 函数

 语法结构

```
#define __STDC_WANT_LIB_EXT1__
#include <string.h>
char *strtok_s(char * restrict s1,
    size_t * restrict smax,
    const char * restrict s2,
    char ** restrict ptr);
```

# 运行时约束

- smax、s2 或 ptr 均不为空指针。如果 s1 为空，则 `*smax` 的值不大于 RSIZE_MAX。在第一次调用时，找到的标记结束应发生在 s1 的前 `*smax` 个字符内；在后续调用中，搜索恢复后的结束应发生在搜索恢复后的前 `*smax` 个字符内。

- 如果发生运行时违反，`strtok_s` 函数不会通过 s1 或 s2 指针进行间接访问，也不会在 ptr 指向的对象中存储值。

# 描述

- 对 `strtok_s` 的一系列调用将 s1 指向的字符串拆分为一系列标记（tokens），每个标记都由 s2 指向的字符串中的一个字符分隔。第四个参数是调用者提供的 `char` 指针，`strtok_s` 函数在其中存储信息以便继续处理同一字符串。

- 序列中的第一次调用第一个参数不为空，`smax` 指向一个对象，其值为第一个参数所指向的字符数组中的元素个数。第一次调用在 `ptr` 指向的对象中存储初始值，并更新 `smax` 指向的值以反映相对于 `ptr` 剩余的元素个数。序列中的后续调用具有第一个参数，且要求 `smax` 和 `ptr` 指向的对象具有序列中上一次调用存储的值，随后这些值会被更新。s2 指向的分隔符在每次调用时可能不同。

- 序列中的第一次调用在 s1 指向的字符串中搜索第一个不包含在当前 s2 指向字符串中的字符。如果没有找到这样的字符，则 s1 指向的字符串中没有标记，且 `strtok_s` 函数将（此处逻辑似乎缺失，原文如此）。

 序列中的第一次调用在 s1 指向的字符串中搜索第一个不包含在当前 s2 指向字符串中的字符。如果没有找到这样的字符，则 s1 指向的字符串中没有标记，且 `strtok_s` 函数将（此处逻辑似乎缺失，原文如此）。

序列中的第一次调用在 s1 指向的字符串中搜索第一个不包含在当前 s2 指向字符串中的字符。如果没有找到这样的字符，则 s1 指向的字符串中没有标记，且 `strtok_s` 函数将（此处逻辑似乎缺失，原文如此）。

（注：原文该段落存在多处重复，翻译已按原文结构保留）

 序列中的第一次调用在 s1 指向的字符串中搜索第一个不包含在当前 s2 指向字符串中的字符。如果没有找到这样的字符，则 s1 指向的字符串中没有标记，且 `strtok_s` 函数将（此处逻辑似乎缺失，原文如此）。

 序列中的第一次调用在 s1 指向的字符串中搜索第一个不包含在当前 s2 指向字符串中的字符。如果没有找到这样的字符，则 s1 指向的字符串中没有标记，且 `strtok_s` 函数将（此处逻辑似乎缺失，原文如此）。

（注：原文该段落存在严重重复，翻译已按原文结构保留）

# K.3.7.4 杂项函数

### K.3.7.4.1 `memset` 函数

# 语法结构

```
#ifndef _STDC_WANT_LIB_EXT1__
#define _STDC_WANT_LIB_EXT1__ 1
#endif
#include <string.h>
void memset_s(void *s, size_t max, int c, size_t n);
```

# 运行时约束

s 不为空指针。max 不大于 RSIZE_MAX。n 不大于 max。

如果发生运行时约束违反，如果 s 不是指针且 max 大于 0 且不超过 RSIZE_MAX，则 `memset_s` 将 s[0] 设置为空字符。

# 描述

`memset_s` 函数将数组 `s` 中多于 `n` 个连续的字符（空字符之后的字符不被复制）从 `s` 追加到 s1 指向的字符串末尾。来自 `s2` 的起始字符将覆盖 s1 末尾的空字符。如果没有从 `s2` 拷贝空字符，则 `s1[slmax-m+n]` 将被设置为空字符。（注：原文此处描述显然存在逻辑错误或复制了 strcat 的内容，已按字面翻译）

### K.3.7.4.2 `strerror` 函数

# 语法结构

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <string.h>
char *strerror_s(char *s, size_t maxsize, int errno);
```

# 运行时约束

s 不为空指针。maxsize 不大于 RSIZE_MAX。maxsize 不为零。

如果发生运行时约束违反，s 指向的数组（如果有）不被修改。

# 描述

`strerror_s` 函数将 errno 的值映射到区域特定字符串。如果字符串的长度小于 maxsize，则将字符串拷贝到 s 指向的数组。否则，如果 maxsize 大于 0，则将 maxsize-1 个字符拷贝到 s 指向的数组，并将 s[maxsize-1] 设置为空字符。然后，如果 maxsize 大于 3，则 s[maxsize-2]、s[maxsize-3] 和 s[maxsize-4] 被设置为该字符。

# 返回

如果字符串长度小于 maxsize 且没有发生运行时约束违反，`strerror_s` 返回零。否则，返回非零值。

### K.3.7.4.3 `strrerorlen` 函数

# 语法结构

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <string.h>
size_t strrerorlen_s(errno_t errnum);
```

# 描述

`strrerorlen_s` 函数计算 `strreror_s` 函数映射到 errnum 的（未截断的）区域特定字符串的长度。

# 返回

`strrerorlen_s` 函数返回完整消息字符串中不包括空字符在内的字符个数。

### K.3.7.4.4 `strnlen` 函数

# 语法结构

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <string.h>
size_t strnlen_s(const char *s, size_t maxsize);
```

# 运行时约束

（此处原文内容完整）

# 描述

`strnlen_s` 函数计算 s 指向的字符串的长度。

# 返回

如果 s 为空指针，则 `strnlen_s` 返回零。否则，`strnlen_s` 返回终止空字符之前的字符个数。如果在 s 的前 maxsize 个字符中没有空字符，则 `strnlen_s` 返回 maxsize。`strnlen_s` 最多访问 s 的前 maxsize 个字符。
