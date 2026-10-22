

| 宏 | 表示 |
|---|---|
| `DBL_DECIMAL_DIG` | double 从基数 b 转换为基数 10 再转换回基数 b 时数值不变的十进制位数（最小值为 10） |
| `LDBL_DECIMAL_DIG` | long double 从基数 b 转换为基数 10 再转换回基数 b 时数值不变的十进制位数（最小值为 10） |
| `DECIMAL_DIG` | 支持的最宽浮点类型从基数 b 转换为基数 10 再转换回基数 b 时数值不变的十进制位数（最小值为 10） |
| `FLT_DIG` | float 从基数 10 转换为基数 b 再转换回基数 10 时数值不变的十进制位数（最小值为 6） |
| `DBL_DIG` | double 从基数 10 转换为基数 b 再转换回基数 10 时数值不变的十进制位数（最小值为 10） |
| `LDBL_DIG` | long double 从基数 10 转换为基数 b 再转换回基数 10 时数值不变的十进制位数（最小值为 10） |
| `FLT_MIN_EXP` | float 的 e 的最小负整数值 |
| `DBL_MIN_EXP` | double 的 e 的最小负整数值 |
| `LDBL_MIN_EXP` | long double 的 e 的最小负整数值 |
| `FLT_MIN_10_EXP` | 满足 10 的该次幂仍是规范化 float 数的最小负整数（不大于 -37） |
| `DBL_MIN_10_EXP` | 满足 10 的该次幂仍是规范化 double 数的最小负整数（不大于 -37） |
| `LDBL_MIN_10_EXP` | 满足 10 的该次幂仍是规范化 long double 数的最小负整数（不大于 -37） |
| `FLT_MAX_EXP` | float 的 e 的最大正整数值 |
| `DBL_MAX_EXP` | double 的 e 的最大正整数值 |
| `LDBL_MAX_EXP` | long double 的 e 的最大正整数值 |
| `FLT_MAX_10_EXP` | 满足 10 的该次幂在可表示的有限 float 值范围内的最大正整数（至少 +37） |
| `DBL_MAX_10_EXP` | 满足 10 的该次幂在可表示的有限 double 值范围内的最大正整数（至少 +37） |
| `LDBL_MAX_10_EXP` | 满足 10 的该次幂在可表示的有限 long double 值范围内的最大正整数（至少 +37） |

| 宏 | 表示 |
|---|---|
| FLT_MAX | 最大可表示的有限 float 值（至少为 1E+37） |
| DBL_MAX | 最大可表示的有限 double 值（至少为 1E+37） |
| LDBL_MAX | 最大可表示的有限 long double 值（至少为 1E+37） |
| FLT_EPSILON | 1 与大于 1 的最小 float 值之间的差值（不超过 1E-5） |
| DBL_EPSILON | 1 与大于 1 的最小 double 值之间的差值（不超过 1E-9） |
| LDBL_EPSILON | 1 与大于 1 的最小 long double 值之间的差值（不超过 1E-9） |
| FLT_MIN | 最小正规范化 float 值（不超过 1E-37） |
| DBL_MIN | 最小正规范化 double 值（不超过 1E-37） |
| LDBL_MIN | 最小正规范化 long double 值（不超过 1E-37） |
| FLT_TRUE_MIN | 最小正 float 值（不超过 1E-37） |
| DBL_TRUE_MIN | 最小正 double 值（不超过 1E-37） |
| LDBL_TRUE_MIN | 最小正 long double 值（不超过 1E-37） |

## 整数类型的格式转换：inttypes.h（C99）

此头文件定义了若干宏，可用作扩展整数类型的格式说明符。第六节“扩展整数类型”对此做了进一步讨论。该头文件还声明了以下类型：

```
imaxdiv_t
```

这是一个结构类型，表示 idivmax() 函数的返回值。

该头文件还包含 stdint.h，并声明了几个使用最大宽度整数类型（在 stdint.h 中声明为 intmax）的函数。表 RS.V.10 列出了这些函数。

表 RS.V.10 最大宽度整数函数

| 原型 | 描述 |
|---|---|
| intmax_t imaxabs(intmax_t j); | 返回 j 的绝对值 |
| imaxdiv_t imaxdiv(intmax_t numer, intmax_t denom); | 在单次操作中计算 numer/denom 的商和余数，并将这两个值存入返回的结构体中 |

| 原型 | 描述 |
|---|---|
| `intmax_t strtoimax(const char * restrict nptr, char ** restrict endptr, int base);` | 与 `strtol()` 函数等效，不同之处在于它将字符串转换为 `intmax_t` 类型并返回该值 |
| `uintmax_t strtoumax(const char * restrict nptr, char ** restrict endptr, int base);` | 与 `strtoul()` 函数等效，不同之处在于它将字符串转换为 `uintmax_t` 类型并返回该值 |
| `intmax_t wcstoimax(const wchar_t * restrict nptr, wchar_t ** restrict endptr, int base);` | `strtoimax()` 的 `wchar_t` 版本 |
| `uintmax_t wcstoumax(const wchar_t * restrict nptr, wchar_t ** restrict endptr, int base);` | `strtoumax()` 的 `wchar_t` 版本 |

## 替代拼写：`iso646.h`

此头文件提供 11 个宏，它们展开为对应的运算符，如表 RS.V.11 所示。

# 表 RS.V.11 替代拼写

| 宏 | 运算符 | 宏 | 运算符 | 宏 | 运算符 |
|---|---|---|---|---|---|
| and | `&&` | and_eq | `&=` | bitand | `&` |
| bitor | `\|` | compl | `~` | not | `!` |
| not_eq | `!=` | or | `\|\|` | or_eq | `\|=` |
| xor | `^` | xor_eq | `^=` |  |  |

## 本地化：`locale.h`

*locale（区域设置）*是一组控制诸如小数点符号等项目的设置。区域设置值存储在以 `struct lconv` 类型定义的结构体中，该结构体在 `locale.h` 头文件中定义。区域设置可以由一个字符串指定，该字符串用于为结构体成员指定一组特定的值。默认区域设置由字符串 "c" 表示。表 RS.V.12 列出了本地化函数，随后是简要讨论。

表 RS.V.14 列出了 struct lconv 结构体的必需成员。

表 RS.V.14 必需的 struct lconv 成员

| 宏 | 描述 |
|---|---|
| char *decimal_point | 非货币值的小数点字符。 |
| char *thousands_sep | 用于分隔非货币量小数点前数字分组的字符。 |
| char *grouping | 一个字符串，其元素指示非货币量每组数字的大小。 |
| char *int_curr_symbol | 国际货币符号。 |
| char *currency_symbol | 本地货币符号。 |
| char *mon_decimal_point | 货币值的小数点字符。 |
| char *mon_thousands_sep | 用于分隔货币量小数点前数字分组的字符。 |
| char *mon_grouping | 一个字符串，其元素指示货币量每组数字的大小。 |
| char *positive_sign | 用于指示非负格式化货币值的字符串。 |
| char *negative_sign | 用于指示负格式化货币值的字符串。 |
| char int_frac_digits | 国际格式货币量在小数点后显示的位数。 |
| char frac_digits | 本地格式货币量在小数点后显示的位数。 |
| char p_cs_precedes | 设置为 1 或 0，取决于 currency_symbol 是位于非负格式化货币量值之前还是之后。 |
| char p_sep_by_space | 设置为 1 或 0，取决于 currency_symbol 是否与非负格式化货币量值用空格分隔。 |
| char n_cs_precedes | 设置为 1 或 0，取决于 currency_symbol 是位于负格式化货币量值之前还是之后。 |
| char n_sep_by_space | 设置为 1 或 0，取决于 currency_symbol 是否与负格式化货币量值用空格分隔。 |

| 宏 | 描述 |
|---|---|
| char p_sign_posn | 设置为指示 positive_sign 字符串位置的数值；0 表示括号包围数量和货币符号，1 表示字符串位于数量和货币符号之前，2 表示字符串位于数量和货币符号之后，3 表示字符串紧邻货币符号之前，4 表示字符串紧邻货币符号之后。 |
| char n_sign_posn | 设置为指示 negative_sign 字符串位置的数值；含义与 char p_sign_posn 相同。 |
| char int_p_cs_precedes | 设置为 1 或 0，取决于 int_currency_symbol 是位于非负格式化货币量值之前还是之后。 |
| char int_p_sep_by_space | 设置为 1 或 0，取决于 int_currency_symbol 是否与非负格式化货币量值用空格分隔。 |
| char int_n_cs_precedes | 设置为 1 或 0，取决于 int_currency_symbol 是位于负格式化货币量值之前还是之后。 |
| char int_n_sep_by_space | 设置为 1 或 0，取决于 int_currency_symbol 是否与负格式化货币量值用空格分隔。 |
| char int_p_sign_posn | 设置为指示非负国际格式化货币量 positive_sign 位置的数值。 |
| char int_n_sign_posn | 设置为指示负国际格式化货币量 negative_sign 位置的数值。 |

## 数学库：math.h

在 C99 中，math.h 头文件定义了两个类型：

```
float_t
double_t
```

这两个类型分别至少与 float 和 double 一样宽，且 double_t 至少与 float_t 一样宽。它们分别被设计为执行 float 和 double 计算时最高效的类型。

该头文件还定义了几个宏，如表 RS.V.15 所述；除 HUGE_VAL 外，其余宏都是 C99 新增的。其中一些宏在第八节“C99 数值计算增强”中有更详细的讨论。

