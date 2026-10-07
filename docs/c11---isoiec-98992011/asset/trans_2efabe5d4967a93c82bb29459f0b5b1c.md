

## K.3.7.1.2 memove_s 函数

概要

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <string.h>
errno_t memove_s(void *s1, rsize_t slmax,
    const void *s2, rsize_t n);
```

运行时约束

- s1 和 s2 均不能为空指针。slmax 或 n 均不大于 RSIZE_MAX。n 不应大于 slmax。

- 如果发生运行时约束违反，若 s1 不是空指针且 slmax 不大于 RSIZE_MAX，则 memove_s 函数会在 s1 指向的对象的前 slmax 个字符中存储零。

描述

memove_s 函数将从 s1 指向的对象中拷贝 `n` 个字符到 s2（s2 指向的对象中）。其拷贝方式等于：先将从 s2 指向的对象中的 `n` 个字符复制到一个长度为 `n` 字符的临时数组中（该数组与 s1 或 s2 指向的对象不重叠），然后将该临时数组中的 `n` 个字符拷贝到 s1 指向的对象中。

返回值

如果没有发生运行时约束违反，memove_s 函数返回零。否则，返回非零值。

## K.3.7.1.3 strcpy_s 函数

概要

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <string.h>
errno_t strcpy_s(char * restrict s1,
    rsize_t slmax,
    const char * restrict s2);
```

运行时约束

- s1 和 s2 均不能为空指针。slmax 不应大于 RSIZE_MAX。slmax 不得为零。slmax 应当大于 strlen_s(s2, slmax)。不能在重叠的对象之间进行拷贝。

- 如果发生运行时约束违反，若 s1 不是空指针且 slmax 大于零且不大于 RSIZE_MAX，则 strcpy_s 将 s1[0] 设置为空字符。

描述

- 4 `strncpy_s` 函数将 `s2` 指向的字符串（包括终止的空字符）拷贝到 `s1` 指向的数组中。

- 5 当 `strncpy_s` 返回时，在 `s1` 指向的 `slmax` 字符数组中，终止空字符（如果有）之后的所有元素将取未指定的值。

返回值

- 6 如果没有发生运行时约束违反，`strncpy_s` 函数返回 `zero`¹⁴¹⁹。否则，返回非零值。

## K.3.7.1.4 strncpy_s 函数

概要

```
#define __STDC_WANT_LIB_EXT__ 1
#include <string.h>
errno_t strncpy_s(char * restrict s1,
               size_t slmax,
               const char * restrict s2,
               size_t n);
```

运行时约束

- 2 `s1` 和 `s2` 均不为空指针。`slmax` 或 `n` 均不大于 `RSIZE_MAX`。`slmax` 不得为零。如果 `n` 不小于 `slmax`，则 `slmax` 应当大于 `strlen(s2, slmax)`。不能在重叠的对象之间进行拷贝。

- 3 如果发生运行时约束违反，若 s1 不是空指针且 `n` 大于零且不大于 RSIZE_MAX，则 `strncpy_s` 将 `s1[0]` 设置为空字符。

描述

- 4 `strncpy_s` 函数从 `s2` 指向的数组中拷贝不多于 `n` 个连续字符（空字符之后的字符不被拷贝）到 `s1` 指向的数组中。如果从 `s2` 未拷贝空字符，则 `s1[n]` 将被设置为空字符。

> 418) 这允许实现在从 `s2` 拷贝字符到 `s1` 的同时，检查这些字符中是否有空字符。这种方法可能会在发现第一个元素应设置为空字符之前，向每个元素写入一个字符。

> 419) 返回零值意味着从 `s2` 指向的字符串中请求的所有字符都能放入 `s1` 指向的数组中，并且 `s1` 中的结果是终止的。

- 5 当 strncpy_s 返回时，在 s1 指向的 `slmax` 字符数组中，终止空字符（如果有）之后的所有元素将取未指定的值。^{420}

返回值

6 如果没有运行时约束违反，strncpy_s 函数返回零^{421}。否则，返回非零值。

7 示例 1 strncpy_s 函数可以用于拷贝字符串，而不会产生结果为空或字符写入到目标数组之外的危险。

```
#define _STDC_WANT_LIB_EXT1_ 1
#include <string.h>
/* */
char src1[100] = "hello";
char src2[7] = {'\0', 'o', 'o', 'b', 'b', 'y', 'e'};
char dst1[6], dst2[5], dst3[5];
int r1, r2, r3;
r1 = strncpy_s(dst1, 6, src1, 100);
r2 = strncpy_s(dst2, 5, src2, 7);
r3 = strncpy_s(dst3, 5, src2, 4);
```

第一次调用将零值赋值给 r1，并将 dst1 设置为 hello\0。
第二次调用将非零值赋值给 r2，并将 dst2 设置为 v\0。
第三次调用将该值赋值给 r3，并将 dst3 设置为 good\0。

## K.3.7.2 拼接函数

### K.3.7.1 strcat_s 函数

概要

```
#define _STDC_WANT_LIB_EXT1_ 1
#include <string.h>
errno_t strcat_s(char * restrict s1,
    rsize_t slmax,
    const char * restrict s2);
```

运行时约束

进入 strcat_s 时，令 m 为 `slmax - strlen_s(s1, slmax)`。

- s1 和 s2 均不能为空指针。slmax 不大于 RSIZE_MAX。slmax 不得为零。m 应当大于 strlen_s(s2, slmax)。不能在重叠的对象之间进行拷贝。

- 如果发生运行时约束违反，若 s1 不是空指针且 slmax 大于零且不大于 RSIZE_MAX，则 strcat_s 将 s1[0] 设置为空字符。

> 420) 这允许实现在从 `s2` 拷贝字符到 `s1` 的同时，检查这些字符中是否有空字符。这种方法可能会在发现第一个元素应设置为空字符之前，向每个元素写入一个字符。

> 421) 返回值表示从 `s2` 指向的字符串中请求的所有字符都位于 `s1` 指向的数组内，并且 s1 中的结果是终止的。

描述

strcat_s 函数将 s2 指向的字符串拷贝（包括终止空字符）追加到 s1 指向的字符串末尾。s2 的起始字符会覆盖 s1 末尾的空字符。

当 strcat_s 返回时，s1 指向的 `slmax` 字符数组中，终止空字符（如果有）之后的所有元素将取未指定的值。^{423}

返回值

如果没有运行时约束违反，strcat_s 函数返回零^{424}。否则，返回非零值。

### K.3.7.2.2 strncat_s 函数

概要

```
#define __STDC_NULL_LIB_EXT1__ 1
#include <string.h>
errno_t strncat_s(char * restrict s1,
    rsize_t slmax,
    const char * restrict s2,
    size_t n);
```

运行时约束

进入 strncat_s 时，令 m 为 `slmax - strlen_s(s1, slmax)`。

- s1 和 s2 均不能为空指针。slmax 不大于 RSIZE_MAX。slmax 不得为零。如果 n 不小于 slmax，则 m 应当大于 strlen_s(s2, m)。不能在重叠的对象之间进行拷贝。

- 如果发生运行时约束违反，若 s1 不是空指针且 slmax 大于零且不大于 RSIZE_MAX，则 strncat_s 将 s[1] 设置为空字符。

> 422) 零意味着进入 strncat_s 时 s1 未终止。

> 423) 这允许实现在从 s2 追加字符到 s1 的同时，检查这些字符中是否有空字符。这种方法可能会在发现第一个元素应设置为空字符之前，向每个元素写入一个字符。

> 424) 返回零值意味着从 s2 指向的字符串中请求的所有字符都追加到了 s1 指向的字符串上，并且结果是终止的。

描述

strncat_s 函数从 s2 指向的数组中追加不多于 n 个连续字符（空字符之后的字符不被拷贝）到 s1 指向的字符串末尾。s2 的起始字符会覆盖 s1 末尾的空字符。如果从 s2 未拷贝空字符，则 s1[slmax-n] 将设置为空字符。

当 strncat_s 返回时，s1 指向的 `slmax` 字符数组中，终止空字符（如果有）之后的所有元素返回未的值。

返回值

如果没有运行时约束违反，strncat_s 函数返回 0。否则，返回非零值。

示例 1 strncat_s 函数可以用于拷贝字符串，而不会产生结果未终止或字符拷贝到目标数组之外的危险。

```
#define __STDC_NULL_LIB_EXT1__ 1
#include <string.h>
/* ... */
char s1[10] = "good";
char s2[6] = "hello";
char s3[6] = "hello";
char s4[7] = "abc";
char s5[1000] = "bye";
int r1, r2, r3, r4
r1 = strncat_s(s1, s2, 1000);
r2 = strncat_s(s2, 6, ",", 1);
r3 = strncat_s(s3, 6, "X", 2);
r4 = strncat_s(s4, 7, "abcdefghijklmn");
```

第一次调用后 r1 的值为 0，s1 包含序列 goodbye\0。

