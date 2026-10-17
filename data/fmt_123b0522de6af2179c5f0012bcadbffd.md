
3 由 `s` 指向的数组中修改的字节不会超过 `n` 个。如果在重叠的对象之间发生拷贝，则其行为是未定义的。

返回值

4 如果遇到不对应于有效多字节字符的宽字符，`wcstombs` 函数返回 `(size_t)(-1)`。否则，函数返回修改的字节数，包括终止的空字符（如果有）。

## 7.23 noreturn <stdreturn.h>

头文件 `<stdreturn.h>` 定义了宏 `noreturn`，它展开为 `_noreturn`。

## 7.24 字符串处理 <string.h>

### 7.24.1 String <string.h> 约定

1 头文件 `<string.h>` 声明了一个和多个函数，并定义了一个用于字符类型数组和其他被视为字符类型数组的对象的宏。类型为 `size_t`，名称为 `NULL`（均在 7.19 中描述）。使用多种方法确定数组的长度，但在所有情况下，`char *` 或 `void *` 都指向数组的初始（地址最小的）字符。如果访问了任何数组的结尾，则其行为是未定义的。

2 当声明为 `size_t n` 的数组指定函数的长度时，在调用该函数时 `n` 的值可以为零。除非本子句中特定函数的描述有显式说明，否则此类调用中的指针参数仍应具有 7.14 中描述的有效值。在此类调用中，查找字符的函数未发现匹配，比较两个字符序列的函数返回零，拷贝字符的函数拷贝零字符。

3 对于本子句中的所有函数，每个字符的解释都应当类似于其类型为 `unsigned char`（因此所有可能的对象表示都是有效的且具有不同的值）。

## 7.24.2 拷贝函数

### 7.24.2.1 memcpy 函数

语法原型

```
#include <string.h>
void memcpy(void * restrict s1,
const void * restrict s2,
size_t n);
```

描述

1 `memcpy` 函数从 `s2` 指向的对象拷贝 `n` 个字符到 `s1` 指向的对象中。如果在重叠的对象之间发生拷贝，则其行为是未定义的。

返回值

3 `memcpy` 函数返回 `s1` 的值。

### 7.24.2.2 memmove 函数

语法原型

```
#include <string.h>
void *memmove(void *s1, const void *s2, size_t n);
```

描述

`memmove` 函数从 `s2` 指向的对象拷贝 `n` 个字符到 `s1` 指向的对象中。拷贝的发生方式类似于先将 `s2` 指向的对象的 `n` 个字符拷贝到一个不与 `s1` 指向的对象重叠的临时数组中，然后将这些字符拷贝到 `s1` 指向的对象中。

返回值

`memmove` 函数返回 `s1` 的值。

### 7.24.2.3 strcpy 函数

语法原型

```
#include <string.h>
char *strcpy(char * restrict s1,
const char * restrict s2);
```

描述

`strcpy` 函数将 `s2` 指向的字符串（包括空字符）拷贝到 `s1` 指向的数组中。如果在重叠的对象之间发生拷贝，则其行为是未定义的。

返回值

`strcpy` 函数返回 `s1` 的值。

### 7.24.2.4 strncpy 函数

语法原型

```
#include <string.h>
char *strncpy(char * restrict s1,
const char * restrict s2,
size_t n);
```

描述

`strncpy` 函数从 `s2` 指向的数组拷贝不超过 `n` 个字符（空字符之后的不被拷贝）到 `s1` 指向的数组中。如果在重叠的对象之间发生拷贝，则其行为是未定义的。如果 `s2` 指向的数组短于 `n` 个字符，则在 `s1` 指向的数组中追加空字符，直到总共写入 `n` 个字符。

返回值

`strncpy` 函数返回 `s1` 的值。

## 7.24.3 拼接函数

### 7.24.3.1 strcat 函数

语法原型

```
#include <string.h>
char *strcat(char * restrict s1,
const char * restrict s2);
```

描述

`strcat` 函数将 `s2` 指向的字符串拷贝（包括空字符）追加到 `s1` 指向的字符串末尾。`s2` 的起始字符覆盖 `s1` 结尾的空字符。如果在重叠的对象之间发生拷贝，则其行为是未定义的。

返回值

`strcat` 函数返回 `s1` 的值。

### 7.24.3.2 strncat 函数

语法原型

```
#include <string.h>
char *strncat(char * restrict s1,
const char * restrict s2,
size_t n);
```

描述

`strncat` 函数将 `s2` 指向的数组中超过 `n` 个字符（空字符及其之后的字符不被追加）追加到 `s1` 指向的字符串末尾。`s2` 的起始字符覆盖 `s1` 结尾的空字符。结果会被追加一个终止空字符。

返回值

`strncat` 函数返回 `s1` 的值。

© ISO/IEC 2011 – 保留所有 ISO/IEC 9899:2011 (E)

发生在重叠的对象之间时，其行为是未定义的。

返回值

- 3 `strcat` 函数返回 `s1` 的值。

前向引用：`strlen` 函数 (7.24.6.3)。

## 7.24.4 比较函数

- 1 比较函数 `memcmp`、`strcmp` 和 `strncmp` 返回的非零值的符号位，取决于所比较对象中第一对不同字符（均解释为无符号字符 `unsigned char`）的值差的符号位。

## 7.24.4.1 memcmp 函数

### 概要

- 1 `#include <string.h>`

`int memcmp(const void *s1, const void *s2, size_t n);`

### 描述

- 2 `memcmp` 函数比较 `s1` 指向的对象的前 `n` 个字符与 `s2` 指向的对象的前 `n` 个字符.³310)

返回值

- 3 `memcmp` 函数返回一个大于零、等于或小于零的整数，这取决于 `s1` 指向的对象是否大于、等于或小于 `s2` 指向的对象。

## 7.24.4.2 strcmp 函数

### 概要

- 1 `#include <string.h>`

`int strcmp(const char *s1, const char *s2);`

### 描述

- 2 `strcmp` 函数比较 `s1` 指向的字符串与 `s2` 指向的字符串。

返回值

- 3 `strcmp` 函数返回一个大于零、等于或小于零的整数，这取决于 `s1` 指向的字符串是否大于、等于或小于 `s2` 指向的字符串。

> 310 用于结构体对象内对齐目的填充的“空洞”内容是不确定的。短于其分配空间的字符串和联合体在比较时也可能导致问题。

## 7.24.4.3 strcat 函数

### 概要

```
#include <string.h>
int strcat(const char *s1, const char *s2);
```

### 描述

`strcat` 函数比较 `s1` 指向的字符串与 `s2` 指向的字符串，两者均根据当前区域设置（locale）的 LC_COLLATE 类别进行解释。

返回值

`strcat` 函数返回一个大于零、等于或小于零的整数，这取决于当两者都按照当前区域设置进行解释时，`s1` 指向的字符串是否大于、等于或小于 `s2` 指向的字符串。

## 7.24.4.4 strncmp 函数

### 概要

```
#include <string.h>
int strncmp(const char *s1, const char *s2, size_t n);
```

### 描述

`strncmp` 函数比较从 `s1` 指向的数组到 `s2` 指向的数组的最最多 `n` 个字符（空字符之后的字符不进行比较）。

返回值

`strncmp` 函数返回一个大于零、等于或小于零的整数，这取决于 `s1` 指向的可能以空终止的数组是否大于、等于或小于 `s2` 指向的可能以空终止的数组。

## 7.24.4.5 strxfrm 函数

### 概要

```
#include <string.h>
size_t strxfrm(const char *restrict s1, const char *restrict s2, size_t n);
```

### 描述

`strxfrm` 函数转换 `s2` 指向的字符串并将生成的字符串放入 `s1` 指向的数组中。该转换方式使得：如果将 `strxfrm` 函数应用于两个转换后的字符串，它返回一个大于零、等于或小于零的值，对应于将 `strcoll` 函数应用于相同的两个字符串的结果。最多有 `n` 个字符被放入 `s1` 指向的输出数组中，包括终止的空字符。如果 `n` 为零，则允许 `s1` 为空指针。如果在重叠的对象之间进行拷贝，其行为是未定义的。

返回值

- `strxfrm` 函数返回转换字符串的长度（不包括空字符）。如果返回的值为 `n` 或更多，则 `s1` 指向的数组的内容是不确定的。

- 示例：以下表达式的值是存放 `s` 指向的字符串转换结果所需的数组大小。

```
strxfrm(NULL, s, 0)
```

## 7.24.5 搜索函数

### 7.24.5.1 memchr 函数

### 概要

```
#include <string.h>
void memchr(const void *s, int c, size_t n);
```

### 描述

- `memchr` 函数定位 `s` 指向的对象中 `c`（转换为 `unsigned char`）的首次出现。该实现应当按顺序读取字符，并在找到匹配字符时立即停止。

返回值

- `memchr` 函数返回指向定位字符的指针，如果该字符未在对象中出现，则返回空指针。

## 7.24.5.2 strchr 函数

### 概要

```
#include <string.h>
char *strchr(const char *s, int c);
```

### 描述

- `strchr` 函数定位 `s1` 指向的字符串中 `c`（转换为 `char`）的首次出现。终止的空字符被视为字符串的一部分。

返回值

- `strchr` 函数返回指向定位字符的指针，如果该字符未在字符串中出现，则返回空指针。

## 7.24.5.3 strspn 函数

### 概要

```
#include <string.h>
size_t strspn(const char *s1, const char *s2);
```

### 描述

- `strspn` 函数计算 `s1` 指向的字符串的最大起始段的长度，该段完全由不在 `s2` 指向的字符串中的字符组成。

返回值

- `strspn` 函数返回该段的长度。

## 7.24.5.4 strbrk 函数

### 概要

```
#include <string.h>
char *strbrk(const char *s1, const char *s2);
```

### 描述

- `strbrk` 函数定位 `s1` 指向的字符串中 `s2` 字符串中任意字符的首次出现。

返回值

- `strbrk` 函数返回指向该字符的指针，如果 `s2` 中的字符没有出现在 `s1` 中，则返回空指针。

## 7.24.5.5 rchr 函数

### 概要

```
#include <string.h>
char *strchr(const char *s, int c);
```

### 描述

- `rchr` 函数定位 `s` 指向的字符串中 `c`（转换为 `char`）的最后一次。终止的空字符被视为字符串的一部分。

返回值

- `rchr` 函数返回指向定位字符的指针，如果 `c` 未在字符串中出现，则返回空指针。

## 7.24.5.6 strcspn 函数

### 概要

```
#include <string.h>
size_t strcspn(const char *s1, const char *s2);
```

### 描述

- `strcspn` 函数计算 `s1` 指向的字符串的最大起始段的长度，该段完全由 `s2` 指向的字符串中的字符组成。

返回值

- `strcspn` 函数返回该段的长度。

## 7.24.5.7 strstr 函数

### 概要

```
#include <string.h>
char *strstr(const char *s1, const char *s2);
```

### 描述

- `strstr` 函数定位 `s1` 指向的字符串中 `s2` 字符序列（不包括空字符）的首次出现。

返回值

- `strstr` 函数返回指向该字符串的指针，如果未找到则返回空指针。

## 7.24.5.8 strtok 函数

### 概要

```
#include <string.h>
char *strtok(char *s1, const char *s2);
```

### 描述

通过一系列调用 `strtok` 函数将 `s1` 指向的字符串分解为标记，每个标记由 `s2` 指向的字符串中的字符分隔。第一次调用具有非空第一个参数；后续调用具有空第一个参数。`s2` 指向的字符串字符串可能与所有调用不同。

序列中的第一次调用搜索 `s1` 指向的字符串中第一个不在 `s2` 指向的字符串中的字符。如果没有找到这样的字符，则 `s1` 指向的字符串中没有标记，`strtok` 函数返回空指针。如果找到了，则它是第一个标记的开始。

`strtok` 函数随后从那里开始搜索位于分隔符字符串中的字符。如果没有找到这样的字符，当前标记延伸到 `s1` 指向字符串的末尾，后续搜索标记将返回空指针。如果找到了这样的字符，它将被覆盖为空字符，从而终止当前标记。`strtok` 函数保存后续字符的指针，下一次搜索标记将从该处开始。

后续以空作为第一个参数调用的行为如上所述。

`strtok` 函数不要求避免与其他 `strtok` 函数调用之间的数据竞态.³11) 实现应当表现为没有库函数调用 `strtok` 函数。

返回值

`strtok` 函数返回指向标记第一个字符的指针，如果没有标记则返回空。

示例

```
#include <string.h>
static char str[] = "???b,,#c";char *t;

t = strtok(str, ","); // t 指向标记 "a"
t = strtok(NULL, "??"); // t 指向标记 "??b"
t = strtok(NULL, ",#"); // t 指向标记 "c"
t = strtok(NULL, "??"); // t 为空指针
```

## 72.4.6 杂函数

### 72.4.6.1 memset 函数

原型

```
#include <string.h>
void *memset(void *s, int c, size_t n);
```

描述

- `memset` 函数将 `c` 的值（转换为 `unsigned char`）复制到由 `s` 指向的对象的前 `n` 个字符的每一个中。

返回值

- `memset` 函数返回 `s` 的值。

### 72.4.6.2 strerror 函数

原型

```
#include <string.h>
char *strerror(int errnum);
```

描述

- `strerror` 函数将 `errnum` 中的数字映射到消息字符串。通常，`errnum` 的值来自 `errno`，但 `strerror` 应当将任何类型的值映射到消息。

- `strerror` 函数不要求避免与其他 `strerror` 函数调用产生的数据竞态。实现行为应当表现为没有库函数调用了 `strerror` 函数。

返回值

- `strerror` 函数返回一个指向字符串的指针，其内容取决于区域设置（locale-specific）。指向的数组不应被程序修改，但可能会被后续对 `strerror` 函数的调用覆盖。

前向引用：`strerror_s` 函数（K.3.7.4.2）。

> 可以使用 `strerror_s` 函数来避免数据竞态。

- `strlen` 函数返回终止空字符之前的字符数。

## 7.25 类型泛型数学 <tgmath.h>

- 头文件 `<tgmath.h>` 包含了 `<math.h>` 和 `<complex.h>` 头文件，并定义了几个类型泛型宏。

- 在 `<math.h>` 和 `<complex.h>` 的函数中，如果没有 `f` (float) 或 `l` (long double) 后缀，有几个函数具有一个或多个对应实类型为 `double` 的参数。对于每一个这样的函数（除 `modf` 外），都有一个对应的类型泛型宏。在函数原型中对应实类型为 `double` 的参数是泛型参数。使用该宏会调用一个函数，该函数对应的实类型和类型域由泛型参数的参数决定。

- 使用该宏会调用一个函数，其泛型参数对应的实类型按如下确定：

    - 首先，如果泛型参数的任何参数类型为 `long double`，则确定的类型为 `long double`。

    - 否则，如果泛型参数的任何参数类型为 `double` 或整数类型，则确定的类型为 `double`。

    - 确定的类型为 `float`。

- 对于 `<math.h>` 中的每个未指定的函数，如果在 `<complex.h>` 中存在一个除 `c` 前缀外同名的函数，则对应的类型泛型宏（针对这两个函数）具有与 `<math.h>` 中函数相同的名称。`fabs` 和 `cabs` 对应的类型泛型宏均同为 `fabs`。

> 像标准库中的其他函数类宏一样，每个类型泛型宏都可以被抑制以生成相应的普通函数。

> 如果参数与所选函数的参数类型不兼容，则行为是未定义的。

# ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – 保留所有权利

| <math.h> | <complex.h> | 类型泛型宏 |
