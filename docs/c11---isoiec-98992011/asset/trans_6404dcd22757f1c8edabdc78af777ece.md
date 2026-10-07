

© ISO/IEC 2011 – 版权所有 ISO/IEC 9899:2011 (E)

s 的最大宽字符数大小应通过 wcsnlen_s 访问。

## K.3.9.3 扩展多字节/宽字符转换实用程序

### K.3.9.3.1 可重入的多字节/宽字符转换函数

- 与 wctomb 不同，wctomb_s 不允许 ps 参数（转换状态的指针）为空指针。

### K.3.9.3.1.1 wctomb_s 函数

#### 概要

```
#include <wchar.h>
errno_t wctomb_s(size_t * restrict retrieval,
char * restrict s, size_t smax,
wchar_t wc, mbstate_t * restrict ps);
```

#### 运行时约束

- 检索或 s 和 ps 均不为空指针。如果 s 不是空指针，则 smax 不应为零且大于 RSIZE_MAX。如果 s 不是空指针，则 smax 不应大于 s 所指数组中要存储的字节数。如果 s 是空指针，则 smax 等于零。

- 如果发生运行时约束违反，wctomb_s 将执行以下操作：如果 s 不是空指针且 smax 大于零且不大于 RSIZE_MAX，则 wctomb_s 将 s[0] 设置为空字符。如果 retval 不是空指针，则 wctomb_s 将 *retrieval 设置为 (size_t) (-1)。

#### 描述

- 如果 s 是空指针，则 wctomb_s 函数等同于调用 wctomb_s(&retval, buf, sizeof buf, L'\0', ps)，其中 retval 和 buf 是相应类型的变量，且 buf 的大小大于 MB_CUR_MAX。

- 如果 s 不是空指针，wctomb_s 函数确定表示与宽字符 wc 对应的多字节字符（包含任何移位序列）所需的字节数，并将多字节字符表示存储在由 s 指指的第一个元素的数组中。如果 wc 是宽字符，则存储一个字节，并在前面带有任何用于恢复初始移位状态的移位序列；结果状态描述了初始转换状态。

- 注意，wcsnlen_s 没有运行时约束。这种缺乏运行时约束加上对于空指针或不确定宽字符串参数返回的返回值，使得 wcsnlen_s 在能够处理异常数据的算法中非常。

#### §K.3.9.3.1.1 边界检查接口

如果 wc 不对应有效的多字节字符，则发生编码错误：wctomb_s 函数将值 (size_t) (-1) 存储到 *retval，且转换状态未指定。否则，wctomb_s 函数将 s 所指数组中存储的字节数（包括任何移位序列）存储到 *retval。

#### 返回

如果没有发生运行时约束违反和编码错误，wctomb_s 函数返回零。否则，返回非零值。

## K.3.9.3.2 可重入的多字节/宽字符串函数

- 与 mbsrtowcs 和 wctombs 不同，mbsrtowcs_s 和 wctombs_s 不允许 ps 参数（转换状态的指针）为空指针。

### K.3.9.3.2.1 mbsrtowcs_s 函数

#### 概要

```
#include <wchar.h>
errno_t mbsrtowcs_s(size_t * restrict retval,
char * restrict dst, size_t dstmax,
const char ** restrict src, size_t len,
mbstate_t * restrict ps);
```

#### 运行时约束

- retval、*src、*dst 均不为空指针。如果 dst 不是空指针，则 dst 和 dstmax 都不应大于 RSIZE_MAX。如果 dst 是空指针，则 dstmax 等于零。如果 dst 不是空指针，则 dstmax 不应小于 len，且在 *src 所指数组的第一个多字节字符之后不出现任何字符。

- 如果发生运行时约束违反，则 mbsrtowcs_s 将 *retval 设置为 (size_t) (-1)。如果 dst 不是空指针且 dstmax 大于零且小于 RSIZE_MAX，则 mbsrtowcs_s 将 dst[0] 设置为宽字符。

#### 描述

mbsrtowcs_s 函数将由 src 索引的数组中从由 ps 指向的对象描述的转换状态开始的多字节字符序列转换。如果 dst 不是空指针，则转换后的字符存储在由 dst 指向的数组中。转换持续进行直到遇到终止空字符，该空字符也会被存储。在以下情况下转换会提前停止：遇到不是有效多字节字符的字节序列时；或者当 len 个字符已存储到 dst 指向的数组中且 dst 不是空指针时。

#### §K.3.9.3.2.1 边界检查接口

- 如果 dst 不是空指针且 dstmax 大于零且小于 RSIZE_MAX，则 mbsrtowcs_s 将 dst[0] 设置为宽字符。

- 如果 dst 不是空指针，转换后的字符存储在由 dst 指的数组中。

- 如果 dst 不是空指针，转换后的字符存储在由 dst 指向的数组中。

- 如果 dst 不是空指针，*retval 的值是成功转换的多字节字符数。

- 如果 dst 不是空指针，转换后的字符存储在由 dst 指向的数组中。

- 如果 dst 不是空指针，*retval 的值是成功转换的多字节字符数。

- 如果 dst 不是空指针，*retval 的值是成功转换的多字节字符数。

- 如果 dst 不是空指针，*retval 的值是成功转换的多字节字符数。

- 如果 dst 不是空指针，*retval 的值是成功转换的多字节字符数。

- 如果 dst 不是空指针，*retval 的值是成功转换的多字节字符数。

- 如果 dst 不是空指针，*retval 的值是成功转换的多字节字符数。

- 如果 dst 不是空指针，*retval 的值是成功转换的多字节字符数。

- 如果 dst 不是空指针，*retval 的值是成功转换的多字节字符数。

- 如果 dst 不是空指针，转换后的字符存储在由 dst 指向的数组中。

- 如果 dst 不是空指针，转换后的字符存储在由 dst 指向的数组中。

- 如果 dst 不是空指针，转换后的字符存储在由 dst 指向的数组中。

- 如果 dst 不是空指针，转换后的字符存储在由 dst 指向的数组中。

- 如果 dst 不是空指针，转换后的字符存储在由 dst 指向的数组中。

- 如果 dst 不是空指针，转换后的字符存储在由 dst 指向的数组中。

- 如果 dst 不是空指针，转换后的字符存储在由 dst 指向的数组中。

- 如果 dst 不是空指针，转换后的字符存储在由 dst 指向的数组中。

- 如果 dst 不是空指针，转换后的字符存储在由 dst 指向的数组中。

- 如果 dst 不是空指针，转换后的字符存储在由 dst 指向的数组中。

- 如果 dst 不是空指针，*retval 的值是成功转换的多字节字符数。

- 如果 dst 不是空指针，*retval 的值是成功转换的多字节字符数。

- 如果 dst 不是空指针，*retval 的值是成功转换的多字节字符数。

- 如果 dst 不是空指针，*retval 的值是成功转换的多字节字符数。

- 如果 dst 不是空指针，*retval 的值是成功转换的多字节字符数。

- 如果 dst 不是空指针，*retval 的值是成功转换的多字节字符数。

- 如果 dst 不是空指针，*retval 的值是成功转换的多字节字符数。

- 如果 dst 不是空指针，*retval 的值是成功转换的多字节字符数。

### K.3.9.3.2.2 wcsrtombs_s 函数

#### 概要

```
#include <wchar.h>
errno_t wcsrtombs_s(size_t * retrieval,
char * restrict dst, size_t dstmax,
const wchar_t ** restrict src, size_t len,
mbstate_t * restrict ps);
```

成功转换的多字节字符数。

- 如果 dst 不是空指针，*retval 的值是成功转换的多字节字符数。

- 如果 dst 不是空指针，*retval 的值是成功转换的多字节字符数。

- 如果 dst 不是空指针，*retval 的值是成功转换的多字节字符数。

- 如果 dst 不是空指针，*retval 的值是成功转换的多字节字符数。

- 如果 dst 不是空指针，*retval 的值是成功转换的多字节字符数。

- 如果 dst 不是空指针，*retval 的值是成功转换的多字节字符数。

- 如果 dst 不是空指针，*retval 的值是成功转换的多字节字符数。

- 如果 dst 不是空指针，*retval 的值是成功转换的多字节字符数。

