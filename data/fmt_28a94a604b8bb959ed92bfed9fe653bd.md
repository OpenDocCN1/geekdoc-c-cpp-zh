
### 运行时约束

`s` 和 `format` 均不能为空指针。任何间接用于以存储转换后输入的参数均不能为空指针。

如果发生运行时约束违例，`vsscanf_s` 函数不会尝试执行后续输入，且 `vsscanf_s` 在发现运行时约束违例之前执行了多少输入是未确定的。

## 描述

`vsscanf_s` 函数与 `sscanf_s` 等效，将可变参数列表替换为 `arg`，`arg` 应当由 `va_start` 宏初始化（并可能使用了 `va_arg` 调用）。`vsscanf_s` 函数不调用 `va_end` 宏。

### 返回值

如果在任何转换之前发生输入失败或存在运行时约束违例，`vsscanf_s` 函数返回宏 `EOF` 值。否则，`vsscanf_s` 函数返回分配的输入项目数量，在匹配失败的情况下，该数量可能少于提供的数量甚至为零。

## K.3.5.4 字符输入/输出函数

## K.3.5.4.1 gets_s 函数

### 概要

```
#define __STDC_WANT_LIB_EXT1__ 1

#include <stdio.h>

char *gets_s(char *s, rsize_t n);
```

> 403) 与 `fgets` 函数一样，`vscanf_s`, `vprintf_s`, `vsprintf_s`, `vsscanf_s`, `vsnprintf_s` 调用 `va_arg` 宏，`gets` 的值未确定

### 运行时约束

`s` 应当是一个指针。`n` 既不等于零也不大于 `RSIZE_MAX`。

如果发生运行时约束违例，`s[0]` 被设置为空字符。

## 描述

`gets_s` 函数从标准输入读取少于 `n` 个字符到数组 `s` 中。如果遇到文件结束或发生读取错误，则写入空字符，`s` 的其他元素值未确定。

### 建议实践

`fgets` 函数允许安全地处理过长的输入行。考虑使用 `fgets` 代替 `gets`。

### 返回值

`gets_s` 函数成功时返回 `s`。如果发生运行时约束违例、遇到文件结束且未读取到字符或发生读取错误，则返回空指针。

> 404) 与历史 `gets` 函数不同，`gets_s` 将输入溢缓冲区视为运行时约束违例。与 `fgets` 函数不同，`gets_s` 维持了输入行与成功调用之间的一一对应关系。

该实现包含一个默认约束处理器，如果没有调用过 `set_constraint_handler_s` 函数，则将使用它。默认处理器的行为由实现定义，可能会导致程序退出或终止。

如果传递给 `set_constraint_handler_s` 的 `handler` 参数为空指针，则实现的默认处理处理器将成为当前的约束处理器。

# 返回

`set_constraint_handler_s` 函数返回指向上一个注册的处理器的指针。⁴405)

## K.3.6.1.2 abort_handler_s 函数

### 概要

```
#define __STDC_WANT_LIB_EXT1__ 1

#include <stdlib.h>

void abort_handler_s(

    const char * restrict msg,

    void * restrict ptr,

    errno_t error);
```

## 描述

指向 `abort_handler_s` 函数的指针应是 `set_constraint_handler_s` 函数的适当参数。

`abort_handler_s` 函数以实现的格式在标准错误流上写入消息。该消息应包含由 `msg` 指向的字符串。随后，`abort_handler_s` 函数调用 `abort` 函数。⁴406)

### 返回

`abort_handler_s` 函数不返回给调用者。

> 405) 如果上一个处理器是通过调用 `set_constraint_handler_s` 并传递空指针参数注册的，则返回指向实现默认处理器的指针（非 NULL）。

> 406) 许多实现在调用 `abort` 函数时会调用调试器。

## K.3.6.1.3 ignore_handler_s 函数

### 概要

```
#define __STDC_WANT_LIB_EXT1__ 1

#include <stdlib.h>

void ignore_handler_s(

    const char * restrict msg,

    void * restrict ptr,

    errno_t error);
```

## 描述

指向 `ignore_handler_s` 函数的指针应是 `set_constraint_handler_s` 函数的适当参数。

`ignore_handler_s` 函数简单地返回给调用者。⁴407)

### 返回

`ignore_handler_s` 函数不返回值。

## K.3.6.2 与环境交互

### K.3.6.2.1 getenv_s 函数

### 概要

```
#define __STDC_WANT_LIB_EXT1__ 1

#include <stdlib.h>

errno_t getenv_s(size_t * restrict len,

    char * restrict value, rsize_t maxsize,

    const char * restrict name);
```

### 运行时约束

`name` 不得为空。`maxsize` 不等于零也不大于 `RSIZE_MAX`。如果 `maxsize` 不等于零，则 `value` 不得为指针。

如果发生运行时约束违反，`len` 指向的整数被设置为 0（如果 `len` 不为空），且不搜索环境列表。

## 描述

`getenv_s` 函数在宿主环境提供的环境列表中查找与 `name` 指向的字符串匹配的字符串。

> 407) 如果运行时约束处理器被设置为 `ignore_handler_s` 函数，则发生运行时约束违反的任何库函数将返回给其调用者。调用者可以根据库函数的规范（通常，库函数返回非零 errno）来确定是否发生了运行时约束违反。

如果找到了该 `name`，`getenv_s` 执行以下操作：如果 `len` 不是空指针，则与匹配列表关联字符串存储在 `len` 指向的整数中。如果关联字符串的长度小于 `maxsize`，则将关联字符串拷贝到 `value` 指向的数组中。

如果未找到 `name`，则 `getenv_s` 执行以下操作：如果 `len` 不是空指针，则在 `len` 指向的整数中存储零。如果 `maxsize` 大于零，则 `value[0]` 被设置为空字符。

环境名称的集合以及更改环境列表的方法由实现定义。`getenv_s` 函数不需要避免与修改环境列表的其他执行线程发生数据竞态。⁴408

### 返回

如果找到指定的名称且关联字符串成功存储在 `value` 中，`getenv_s` 返回零。否则，返回非零值。

## K.3.6.3 搜索和排序工具

这些工具利用比较函数来搜索或排序未指定类型的数组。当声明为 `size_t nmemb` 的参数指定函数的数组长度时，如果在调用该函数时 `nmemb` 的值为零，则比较函数不会被调用，搜索将找不到匹配元素，不进行任何重排，且数组指针可能为空。

实现应确保比较函数的第二个参数（当从 `bsearch_s` 调用时）或两个参数（当从 `qsort_s` 调用时）都是指向数组元素的指针。⁴409 当从 `bsearch_s` 调用时，第一个参数应等于 `key`。

比较函数不应修改数组或搜索键的内容。实现可以在多次调用比较函数之间重新排列数组的元素，但不应更改任何单个元素的内容。

当多次将相同的对象（由 `size` 字节组成，且与它们在数组中的当前位置无关）传递给比较函数时，其结果应当是一致的。也就是说，对于 `qsort_s`，它们定义了数组的全序；而对于 `bsearch_s`，同一个对象与 `key` 比较的结果方式应始终保持一致。

> 408 许多实现提供了修改环境列表的非标准函数。
> 409 也就是说，如果值为 `p`，则以下表达式始终有效且非零：
> ```
> ((char*)p - (char*)base) == 0
> ((char*)p >= (char*)base)
> ((char*)p < (char*)base + nmemb * size)
> ```
> 在每次调用比较函数之前和之后都会发生序列点，且在传递给该调用的对象之间。

## K.3.6.3.1 bsearch_s 函数

### 概要

```
#define __STDC_WANT_LIB_EXT1__ 1

#include <stdlib.h>

void bsearch_s(const void *key, const void *base,

               size_t nmemb, size_t size,

               int (*compar)(const void *k, const void *y,

                             void *context),

               void *context);
```

### 运行时约束

`nmemb size` 不大于 `RSIZE_MAX`。如果 `nmemb` 不等于零，则 `key`、`base` 或 `compare` 不得为空指针。

## 描述

`bsearch_s` 函数在 `base` 指向的包含 `nmemb` 个元素的数组中查找与 `key` 指向的对象匹配的元素。元素的大小由 `size` 指定。

指向 `compare` 的比较函数带有三个参数。前两个参数指向 `key` 对象和数组元素。如果 `key` 对象被认为分别小于、等于或大于数组元素，函数应返回小于、等于或大于零的整数。¹⁰比较函数的第三参数是传递给 `bsearch_s` 的 `context` 参数。⁴¹¹

> 410 在实践中，这意味着整个数组已排序。

`bsearch_s` 函数返回匹配元素的指针，如果未找到或发生运行时约束违反，则返回空指针。如果两个元素相等，则返回哪一个是不指定的。

## K.3.6.3.2 qsort_s 函数

### 概要

```
#define __STDC_WANT_LIB_EXT1__ 1

#include <stdlib.h>

errno_t qsort_s(void *base, rsize_t nmemb, rsize_t size,

               int (*compar) (const void *x, const void *y,

                             void *context),

               void *context);
```

### 运行时约束

`nmemb size` 不大于 `RSIZE_MAX`。如果 `nmemb` 不等于零，则 `base` 和 `compar` 不得为空指针。

如果发生运行时约束违反，`qsort_s` 函数不对数组排序。

## 描述

`qsort_s` 函数对 `base` 指向的包含 `nmemb` 个元素的数组进行排序。每个对象的大小由 `size` 指定。数组的内容根据指向 `compar` 的比较函数按升序排列，比较函数带有三个参数。前两个参数指向待比较的对象。如果第一个参数被认为小于、等于或大于第二个参数，函数应返回小于、等于或大于零的整数。比较函数的第三参数是传递给 `qsort_s` 的 `context` 参数。⁴²

如果两个元素相等，它们在结果排序数组中的相对顺序是不指定的。

### 返回

如果没有发生运行时约束违反，`qsort_s` 函数返回零。否则，返回非零值。

> 4²) `context` 参数供比较函数执行其职责时使用。例如，它可能指定比较函数使用的排序规则。

## 3.6.4 多字节/宽字符转换函数

多字节字符函数的行为受当前区域中 `LC_CTYPE` 类别的影响。对于依赖状态的编码，每个函数通过一次其字符指针参数 `s` 为空指针的调用被置于其初始状态。后续使用 `s` 不为空指针的调用将根据需要更改函数的内部转换状态。当 `s` 为空指针时进行调用，如果编码具有状态依赖性，这些函数将把其 `status` 参数所指向的 `int` 设置为非零值，否则设置为零。413) 更改 `LC_CTYPE` 类别会导致这些函数的转换结果变得不确定。

## 3.6.4.1 wctomomb_s 函数

### 签概要

```
#define _STDC_WANT_LIB_EXT1__ 

#include <stdlib.h>

errno_t wctomomb_s(int * restrict status,

char * restrict s,

size_t smax,

wchar_t wc);
```

### 运行约束

如果 `n` 是表示由宽字符 `wc` 对应的多字节字符所需的字节数（包括任何移位序列）。

如果 `s` 不为空指针，则 `s` 不应小于 `n`，且 `smax` 不应大于 `RSIZE_MAX`。如果 `s` 为空指针，则 `smax` 应等于零。

如果违反运行约束，`wctomomb_s` 不修改 `status` 所指向的 `int`，且如果 `s` 不为空指针，则对 `s` 指向的数组中访问的元素不超过 `smax` 个。

## 描述

`wctomomb_s` 函数确定 `n` 并将 `wc` 的多字节表示存储在由 `s` 指向的第一个元素的数组中（如果 `s` 不为空指针）。存储的字符数永远不会超过 `MB_CUR_MAX` 或 `smax`。如果 `wc` 是空字符，则存储一个空字节，其前面带有任何恢复初始状态所需的移位序列，且该函数处于初始转换状态。

实现的行为应当表现得没有库函数调用 `wctomomb_s` 函数一样。

> 413) 如果区域使用特殊字节来改变移位状态，这些字节不产生宽字符代码，而是与相邻的多字节字符分组。

如果 `s` 为空指针，`wctomomb_s` 函数分别向 `status` 指向的 `int` 存储非零值或值，取决于多字节字符编码是否具有状态依赖性。

如果 `s` 不为空指针，`wctomomb_s` 函数分别向 `status` 指向的 `int` 存储 `n` 或 `-1`，取决于 `wc` 是否对应或不对应于有效的多字节字符。

在任何情况下，`status` 指向的 `int` 都不会被设置为大于 `MB_CUR_MAX` 宏的值。

### 返回值

`wctomomb_s` 函数在成功时返回零，如果发生运行约束违反或 `wc` 不对应有效的多字节字符，则返回非零值。

## K.3.6.5 多字节/宽字符串函数

多字节字符串函数的行为受当前区域中 `LC_CTYPE` 类别的影响。

## 3.6.5.1 mbstowcs_s 函数

### 签概要

```
#include <stdlib.h>

errno_t mbstowcs_s(size_t * restrict retval,

char * restrict dst, rsize_t dstmax,

const char * restrict src, rsize_t len);
```

### 运行约束

`retval` 和 `src` 均不为空指针。如果 `dst` 不为空指针，`len` 和 `dstmax` 均不应大于 `RSIZE_MAX`。如果 `dst` 为空指针，`dstmax` 应等于零。如果 `dst` 不为空指针，`dstmax` 不等于零。如果 `dst` 不为空指针且 `len` 小于 `dstmax`，则在 `src` 指向的数组的前 `dstmax` 个多字节字符内会出现空字符。

如果违反运行约束，`mbstowcs_s` 执行以下操作：如果 `retval` 不为空指针，`mbstowcs_s` 将 `*retval` 设置为 `(size_t) (-1)`。如果 `dst` 不为空指针且 `dstmax` 大于零且小于 `RSIZE_MAX`，`mbstowcs_s` 将 `dst[0]` 设置为空宽字符。

## 描述

`mbstowcs_s` 函数将从 `src` 指向的数组从初始状态开始的多字节字符序列转换为相应的宽字符序列。如果 `dst` 不为空指针，转换后的字符将存储在 `dst` 指向的数组中。转换持续到包括终止空字符，该字符也会被存储。转换在两种情况下会提前停止：当计数的字节序列不构成有效的多字节字符时，或者当在 `dst` 指向的数组中已存储了 `len` 个字符且 `dst` 不为空指针时。44)) 如果 `dst` 不为空指针且在 `dst` 指向的数组中没有存储空宽字符，则 `dst[len]` 被设置为空宽字符。每次转换的发生都如同调用了 `mbstowcs` 函数一样。

无论 `dst` 是否为空指针，如果输入转换遇到一个不构成有效多字节字符的字节序列，则发生编码错误：`mbstowcs_s` 函数将值 `(size_t) (-1)` 存储到 `*retval`。否则，`mbstowcs_s` 函数向 `*retval` 存储成功转换的多字节字符数，不包括终止空字符（如果有）。

由 `mbstowcs_s` 在 `dst` 指向的 `dstmax` 字符数组中写入终止空宽字符（如果有）的所有元素，在 `mbstowcs_s` 返回时都具有未指定的值。415)

如果在重叠对象之间发生拷贝，这些对象将获得未指定的值。

### 返回值

如果没有发生运行约束违反且没有发生编码错误，`mbstowcs_s` 函数返回零。否则返回非零值。

## K.3.6.5.2 wcstows_s 函数

### 签概要

```
#include <stdlib.h>

errno_t wcstows_s(size_t * restrict retval,

char * restrict dst, rsize_t dstmax,

const wchar_t * restrict src, rsize_t len);
```
