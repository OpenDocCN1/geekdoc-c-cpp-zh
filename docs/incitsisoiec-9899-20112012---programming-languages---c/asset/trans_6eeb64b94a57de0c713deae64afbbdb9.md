

[content]

## 7.8.2.2 imdiv 函数

### 概要

```
#include <inttypes.h>
imaxdiv_t imdiv(intmax_t numer, intmax_t denom);
```

### 描述

imdiv 函数在单次操作中计算 `numer / denom` 和 `numer % denom`。

### 返回

imdiv 函数返回一个 `imaxdiv_t` 类型的结构体，包含商和余数。该结构体应包含（顺序任意）成员 `quot`（商）和 `rem`（余数），每个成员的类型均为 `intmax_t`。如果结果的任何部分都无法表示，则行为是未定义的。

## 7.8.2.3 strtoumax 和 strtoullmax 函数

### 概要

```
#include <inttypes.h>
imax_t strtoumax(const char * restrict nptr,
char ** restrict endptr, int base);
uintmax_t strtoullmax(const char * restrict nptr,
char ** restrict endptr, int base);
```

### 描述

strtoumax 和 strtoullmax 函数与 strtol、strtoll、strtou 和 strtoull 函数等，不同在于字符串的起始部分分别转换为 `intmax_t` 和 `uintmax_t` 表示。

### 返回

strtoumax 和 strtoullmax 函数返回转换后的值（如果有）。如果无法进行转换，则返回零。如果正确的值在表示范围之外，则返回 `INTMAX_MAX`、`INTMAX_MIN` 或 `UINTMAX_MAX`（取决于返回类型和值的正负，如果有），并将宏 `ERANGE` 的值存储在 `errno` 中。

前向引用：strtol、strtoll、strtou 和 strtoull 函数（7.22.1.4）。

## 7.8.2.4 wcstoimax 和 wcstumax 函数

### 概要

```
#include <stdio.h> // 用于 wchar_t
#include <inttypes.h>
intmax_t wcstoimax(const wchar_t * restrict nptr,
wchar_t ** restrict endptr, int base);
uintmax_t wcstumax(const wchar_t * restrict nptr,
wchar_t ** restrict endptr, int base);
```

### 描述

- wcstoimax 和 wcstumax 函数与 wcstol、wcstoll、wcstoul 和 strtoull 函数等，不同在于宽字符串的起始部分分别转换为 `intmax_t` 和 `uintmax_t` 表示。

### 返回

- wcstoimax 函数返回转换后的值（如果有）。如果无法进行转换，则返回零。如果正确的值在表示范围之外，则返回 `INTMAX_MAX`、`INTMAX_MIN` 或 `UINTMAX_MAX`（取决于返回类型和值的正负，如果有），并将宏 `ERANGE` 的值存储在 `errno` 中。

前向引用：wcstol、wcstoll、wcstoul 和 strtoull 函数（7.29.4.1.2）。

## 7.9 替代拼法 <iso646.h>

头文件 `<iso646.h>` 定义了以下十一个宏（位于左侧），它们展开为对应的标记（右侧）：

```
and &&
and_eq &=
bitand &
bitor |
ncompl ~
not !
not_eq !=
or ||
or_eq |=
xor ^
xor_eq ^=
```

## 7.10 整数类型的大小 <limits.h>

头文件 `<limits.h>` 定义了若干宏，它们展开为标准整数类型的各种限制和参数。

这些宏的含义以及取值的约束（或限制）列在 5.2.4.2.1 中。

## 7.11 本地化 <locale.h>

头文件 `<locale.h>` 声明了两个函数、一个类型并定义了若干宏。

该类型是

```
struct lconv
```

它包含与数值格式化相关的成员。该结构体应至少包含以下成员，顺序任意。成员的语义和正常范围在 7.11.2.1 中进行了解释。在 "C" 区域中，成员应应具有注释中指定的值。

char *decimal_point;          // ""
char *thousands_sep;         // ""
char *grouping;               // ""
char *mon_decimal_point;     // ""
char *mon_thousands_sep;    // ""
char *mon_grouping;          // ""
char *positive_sign;         // ""
char *negative_sign;         // ""
char *currency_symbol;       // ""
char *fracac_digits;          // CHAR_MAX
char *p_cs_precedes;         // CHAR_MAX
char *n_cs_sep_by_space;     // CHAR_MAX
char *p_sep_by_space;        // CHAR_MAX
char *n_sep_by_space;        // CHAR_MAX
char *p_sign_posn;           // CHAR_MAX
char *n_sign_posn;           // CHAR_MAX
char *int_curr_symbol;       // ""
char *fracac_digits;      // CHAR_MAX
char *p_cs_precedes;     // CHAR_MAX
char *n_cs_precedes;     // CHAR_MAX
char *p_sep_by_space;    // CHAR_MAX
char *n_sep_by_space;    // CHAR_MAX
char *p_sign_posn;           // CHAR_MAX
char *n_sign_posn;           // CHAR_MAX
```
*(注：由于原文文本中部分成员存在重复和格式混乱，此处已按原文结构翻译)*

定义的宏如下（见 7.19）；以及

```
LC_ALL
LC_COLLATE
LC_CTYPE
LC_MONETARY
LC_NUMERIC
LC_TIME
```

这些宏展开为常量表达式，适用于作为 setlocale 函数的第一个参数。实现还可能指定以 LC_ 开头并跟大写字母的额外宏定义。

## 3.11 本地地控制

### 3.11.1 setlocale 函数

### 概要

```
#include <locale.h>
char *setlocale(int category, const char *locale);
```

### 描述

setlocale 函数选择合适的程序区域。setlocale 函数可以根据指定的类别和 locale 参数更改或查询程序的区域。类别值 LC_ALL 指代程序的整个区域；其他值仅程序区域的某部分。LC_COLLATE 影响 strcoll 和 strftime 函数；LC_CTYPE 影响字符处理函数；LC_MONETARY 影响 localconv 函数返回的货币信息；LC_NUMERIC 影响小数点和字符串转换函数；LC_TIME 影响 strftime 和 wstrftime 函数。

locale 值为 "C" 指明最小环境；locale 值为 "native" 指明特定区域的环境。可以传递实现定义的字符串作为第二个参数。

### 返回

如果 locale 给的是一个字符串指针且该选择可以满足，setlocale 返回与新区域对应类别关联的字符串指针。如果选择无法满足，setlocale 返回空指针且程序区域不改变。locale 为空指针将导致 setlocale 函数返回与当前程序区域的对应类别关联的字符串指针；程序区域不改变。setlocale 函数返回的指针使得后续使用该字符串值及其关联类别时可以恢复程序区域的该部分。指针指向的字符串不被程序修改，但可能会被后续的 setlocale 调用所覆盖。

在程序启动时，执行等同于
setlocale(LC_ALL, "C");



调用 setlocale 函数可能会与其他 setlocale 函数的调用或对受当前区域影响的函数的调用引入数据竞态。实现的行为应表现为没有库函数调用 setlocale 函数。

