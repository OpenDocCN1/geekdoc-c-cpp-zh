
s1 指向的宽字符串。s2 的起始宽字符会覆盖 s1 末尾的空宽字符。结果中始终会追加一个终止空宽字符。 347

# 返回

wcscat 函数返回 s1 的值。

## 7.29.4.4 宽字符串比较函数

除非另有说明，否则本子句中描述的函数以与 `wchar_t` 指定的底层整数类型整数相同的方式比较两个宽字符。

### 7.29.4.4.1 wcsmp 函数

# 概要

```
#include <wchar.h>
int wcsmp(const wchar_t *s1, const wchar_t *s2);
```

# 描述

wcsmp 函数比较 s1 指向的宽字符串与 s2 指向的宽字符串。

# 返回

wcsmp 函数返回一个大于、等于或小于零的整数，相应取决于 s1 指向的宽字符串是否大于、等于或小于 s2 指向的宽字符串。

### 7.29.4.4.2 wscolcoll 函数

# 概要

```
#include <wchar.h>
int wscolcoll(const wchar_t *s1, const wchar_t *s2);
```

# 描述 

wscolcoll 函数比较 s1 指向的宽字符串与 s2 指向的宽字符串，两者均根据当前区域设置的 `LC_COLLATE` 类别进行解释。

# 返回

wscolcoll 函数返回一个大于、等于或小于零的整数，相应取决于当两者都按照当前区域设置解释时，s1 指向的宽字符串是否大于、等于或小于 s2 指向的宽字符串。

### 7.29.4.4.3 wscnmp 函数

# 概要

```
#include <wchar.h>
int wscnmp(const wchar_t *s1, const wchar_t *s2,
       size_t n);
```

# 描述 

wscnmp 函数从 s1 指向的数组中与 s2 指向的数组比较多于 n 个宽字符（空宽字符之后的字符不参与比较）。

# 返回

wscnmp 函数返回一个大于、等于或小于零的整数，相应取决于 s1 指向的可能空终止的数组是否大于、等于或小于 s2 指向的可能空终止的数组。

### 7.29.4.4.4 wscxfrm 函数

# 概要

```
#include <wchar.h>
size_t wscxfrm(wchar_t restrict s1,
       const wchar_t restrict s2,
       size_t n);
```

# 描述 

wscxfrm 函数转换 s2 指向的宽字符串，并将生成的宽字符串放入 s1 指向的数组中。该转换方式使得：如果对两个转换后的宽字符串应用 `wcsmp` 函数，其返回的大于、等于或小于零的值，取决于对两个原始宽字符串应用 `wscoll` 函数的结果。在 s1 指向的输出数组中最多最多放入 n 个宽字符，包括终止宽字符。如果 n 为零，则允许 s1 为空指针。

# 返回

wscxfrm 函数返回转换后的宽字符串的长度（不包括终止空宽字符）。如果返回的值等于 n 或更大，则 s1 指向的数组的内容是不确定的。

示例 如下表达式的值是存储 s 指向的宽字符串转换结果所需的数组长度：

### 7.29.4.4.5 wmemcmp 函数

# 概要

```
#include <wchar.h>
wmemcmp(const wchar_t *s1, const wchar_t *s2, size_t n);
```

# 描述 

wmemcmp 函数比较 s1 指向的对象的前 n 个宽字符与 s2 指向的对象的前 n 个宽字符。

# 返回

wmemcmp 函数返回一个大于、等于或小于零的整数，相应取决于 s1 指向的对象是否大于、等于或小于 s2 指向的对象。

## 7.29.4.4.5 宽字符串搜索函数

### 7.29.4.5.1 wcsnrchr 函数

# 概要

```
#include <wchar.h>
wchar_t *wcsnrchr(const wchar_t *s, wchar_t c);
```

# 描述 

wcsnrchr 函数在 s 指向的宽字符串中定位 c 第一次出现的位置。终止空宽字符被视为宽字符串的一部分。

# 返回

wcsnrchr 函数返回定位到的宽字符的指针；如果该宽字符未出现在宽字符串中，则返回空指针。

### 7.29.4.5.2 wcsspn 函数

# 概要

```
#include <wchar.h>
size_t wcsspn(const wchar_t *s1, const wchar_t *s2);
```

# 描述 

wcsspn 函数计算 s1 指向的宽字符串的最大起始段的长度，该段完全由并非 s2 指向的宽字符串的宽字符组成。

wcspn 函数返回该段的长度。

### 7.29.4.5.3 wcspbrk 函数

# 概要

```
#include <wchar.h>
wchar_t *wcspbrk(const wchar_t *s1, const wchar_t *s2);
```

# 描述 

wcspbrk 函数在 s1 指向的宽字符串中定位 s2 指向的宽字符串中任意字符第一次出现的位置。

# 返回

wcspbrk 函数返回 s1 中该宽字符的指针；如果 s2 中的宽字符未出现在 s1 中，则返回空指针。

### 7.29.4.5.4 wcscchr 函数

# 概要

```
#include <wchar.h>
wchar_t *wcscchr(const wchar_t *s, wchar_t c);
```

# 描述 

wcscchr 函数在 s 指向的宽字符串中定位 c 最后一次出现的位置。终止空宽字符被视为宽字符串的一部分。

# 返回

wcscchr 函数返回该字符的指针；如果 c 未出现在宽字符串中，则返回空指针。

### 7.29.4.5.5 wcspn 函数

# 概要

```
#include <wchar.h>
size_t wcspn(const wchar_t *s1, const wchar_t *s2);
```

# 描述 

wcspn 函数计算 s1 指向的宽字符串的最大起始段的长度，该段完全由并非 s2 指向的宽字符串的宽字符组成。

# 返回

wcspn 函数返回该段的长度。

### 7.29.4.5.6 wcsstr 函数

# 概要

```
#include <wchar.h>
wchar_t *wcsstr(const wchar_t *s1, const wchar_t *s2);
```

# 描述 

wcsstr 函数在 s1 指向的宽字符串中定位 s2 指向的宽字符串第一次出现的位置。

# 返回

wcsstr 函数返回 s1 中该宽字符串的指针；如果 s2 未出现在 s1 中，则返回空指针。

### 7.29.4.5.7 wcstok 函数

# 概要

```
#include <wchar.h>
wchar_t *wcstok(wchar_t *s1, const wchar_t *s2, wchar_t **ptr);
```

# 描述 

wcstok 函数将 s1 指向的宽字符串拆分为多个标记（tokens），每个标记由 s2 指向的字符分隔。第一次调用 wcstok 时 s1 使用空指针，后续调用使用 ptr 中存储的指针继续操作。

# 返回

wcstok 函数返回标记第一个字符的指针；如果没有标记，则返回空指针。
