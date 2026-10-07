

## 72.29.4.2.2 wscncpy 函数

用法

```
#include <wchar.h>
wchar_t *wscncpy(wchar_t * restrict s1,
const wchar_t * restrict s2,
size_t n);
```

描述

wscncpy 函数从 s2 指向的数组拷贝至多 n 个宽字符（空宽宽字符之后的字符不被拷贝）到 s1 指向的数组。

如果 s2 指向的数组是一个短于 n 个宽字符的宽字符串，则会在 s1 指向的数组的拷贝内容后追加空宽宽字符，直到写了所有 n 个宽字符为止。

返回值

wscncpy 函数返回 s1 的值。

## 72.29.4.2.3 wmemcpy 函数

用法

```
#include <wchar.h>
wchar_t *wmemcpy(wchar_t * restrict s1,
const wchar_t * restrict s2,
size_t n);
```

描述

wmemcpy 函数从 s2 指向的对象拷贝 n 个宽字符到 s1 指向的对象。

返回值

wmemcpy 函数返回 s1 的值。

## 7.29.4.2.4 wmemmove 函数

用法

```
#include <wchar.h>
wchar_t *wmemmove(wchar_t *s1, const wchar_t *s2,
size_t n);
```

描述

wmemmove 函数从 s2 指向的对象拷贝 n 个宽字符到 s1 指向的对象。拷贝过程是首先将 s2 指向的对象中的 n 个宽字符拷贝到一个 n 个宽字符的临时数组中（该数组不与 s1 或 s2 指向的对象重叠），然后将临时数组中的 n 个宽字符拷贝到 s1 指向的对象中。

返回值

wmemmove 函数返回 s1 的值。

## 7.29.4.3 宽字符串连接函数

### 7.29.4.3.1 wscat 函数

用法

```
#include <wchar.h>
wchar_t *wscat(wchar_t * restrict s1,
wchar_t * restrict s2);
```

描述

wscat 函数将 s2 指向的宽字符串的拷贝（包括终止空字符）追加到 s1 指向的宽字符串的末尾。s2 的起始宽字符会覆盖 s1 末尾的空宽字符。

返回值

wscat 函数返回 s1 的值。

### 7.29.4.3.2 wscncat 函数

用法

```
#include <wchar.h>
wchar_t *wscncat(wchar_t * restrict s1,
wchar_t * restrict s2,
size_t n);
```

描述

wscncat 函数从 s2 指向的数组追加多于 n 个宽字符（空宽字符及其后的字符不追加）到 s1 指向的宽字符串的末尾。s2 的起始宽字符会覆盖 s1 末尾的空宽字符。结果中总是追加一个终止空字符。

返回值

- wscncat 返回 s1 的值。

## 7.29.4.4 宽字符串比较函数

- 除非另有明确说明，否则本子句描述的函数以与 wchar_t 指定底层整数类型相同的方式比较两个宽字符。

### 7.29.4.1 wscmp 函数

用法

```
#include <wchar.h>
int wscmp(const wchar_t *s1, const wchar_t *s2);
```

描述

- wscmp 函数比较 s1 指向的宽字符串与 s2 指向的宽字符串。

返回值

- wscmp 函数返回一个大于、等于或小于零的整数，取决于 s1 指向的宽字符串是否大于、等于或小于 s2 指向的宽字符串。

### 7.29.4.4.2 wscoll 函数

用法

```
#include <wchar.h>
int wscoll(const wchar_t *s1, const wchar_t *s2);
```

描述

- wscoll 函数比较 s1 指向的宽字符串与 s2 指向的宽字符串，两者均根据当前区域设置的 LC_COLLATE 类别进行相应的解释。

返回值

- wscoll 函数返回一个大于、等于或小于零的整数，取决于 s1 指向的宽字符串是否大于、等于或小于 s2 指向的宽字符串。因此，s1 指向的数组中可以使用的宽字符最大数量为 wcslen(s1)+n。

### 7.29.4.4.3 wcsncmp 函数

用法

```
#include <wchar.h>
int wcsncmp(const wchar_t *s1, const wchar_t *s2,
size_t n);
```

描述

wcsncmp 函数比较 s1 指向的数组中多于 n 个字符（空字符之后的字符不被比较）与 s2 指向的数组。

返回值

wcsncmp 返回一个大于、等于或小于零的整数，取决于 s1 指向的可能以空终止的数组是否大于、等于或小于 s2 指向的宽字符串。

### 7.29.4.4 wcsnrnc 函数

用法

```
#include <wchar.h>
int wcsnrnc(const wchar_t *s1, const wchar_t *s2,
size_t n);
```

描述

wcsnrnc 函数比较 s1 指向的数组中多于 n 个字符（空字符之后的字符不被比较）与 s2 指向的数组。

返回值

wcsnrnc 返回一个大于、等于或小于零的整数，取决于 s1 指向的可能以空终止的数组是否大于、等于或小于 s2 指向的宽字符串。

### 7.29.4.4.5 wcswcmp 函数

用法

```
#include <wchar.h>
int wcswcmp(const wchar_t *s1, const wchar_t *s2,
size_t n);
```

描述

wcswcmp 函数比较 s1 指向的数组中多于 n 个字符（空字符之后的字符不被比较）与 s2 指向的数组。

返回值

wcswcmp 函数返回一个大于、等于或小于零的整数，取决于 s1 指向的可能以空终止的数组是否大于、等于或小于 s2 指向的宽字符串。

### 7.29.4.4.6 wcsstrmp 函数

用法

```
#include <wchar.h>
int wcsstrmp(const wchar_t *s1, const wchar_t *s2,
size_t n);
```

描述

wcsstrmp 函数比较 s1 指向的数组中多于 n 个字符（空字符之后的字符不被比较）与 s2 指向的数组。

返回值

wcsstrmp 函数返回一个大于、等于或小于零的整数，取决于 s1 指向的可能以空终止的数组是否大于、等于或小于 s2 指向的宽字符串。

### 7.29.4.4.7 wcsspn 函数

用法

```
#include <wchar.h>
size_t wcsspn(const wchar_t *s1, const wchar_t *s2);
```

描述

wcsspn 函数计算 s1 指向的宽字符串中完全由 s2 指向的宽字符串中的字符组成的最大段的长度。

返回值

wcsspn 返回该段的长度。

### 7.29.4.4.8 wcspn 函数

用法

```
#include <wchar.h>
size_t wcspn(const wchar_t *s1, const wchar_t *s2,
size_t n);
```

描述

wcspn 函数转换 s2 指向的宽字符串并将多于 n 个字符放入 s1 指向的数组中。

返回值

wcspn 返回放入的字符长度。

### 7.29.4.4.9 wcsbrk 函数

用法

```
#include <wchar.h>
size_t wcsbrk(wchar_t *s1, const wchar_t *s2,
size_t n);
```

描述

wcsbrk 函数转换 s2 指向的宽字符串并将多于 n 个字符放入 s1 指向的数组中。

返回值

wcsbrk 返回放入的字符长度。

### 7.29.4.4.10 wcsspan 函数

用法

```
#include <wchar.h>
size_t wcsspan(wchar_t *s1, const wchar_t *s2,
size_t n);
```

描述

wcsspan 函数转换 s2 指向的宽字符串并将多于 n 个字符放入 s1 指向的数组中。

返回值

wcsspan 返回放入的字符长度。

