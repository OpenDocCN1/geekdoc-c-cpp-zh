

| 原型 | 描述 |
|---|---|
| char *strcat(char * restrict s1, const char * restrict s2); | 将 s2 所指向的字符串的副本（包括空字符）附加到 s1 所指向的位置；s2 字符串的第一个字符覆盖 s1 字符串的空字符；返回 s1。 |
| char *strncat(char * restrict s1, const char * restrict s2, size_t n); | 将 s2 所指向的字符串中最多 n 个字符或直到空字符的副本附加到 s1 所指向的位置，s2 的第一个字符覆盖 s1 的空字符；始终附加空字符；函数返回 s1。 |
| char *strcpy(char * restrict s1, const char * restrict s2); | 将 s2 所指向的字符串（包括空字符）复制到 s1 所指向的位置；返回 s1。 |
| char *strncpy(char * restrict s1, const char * restrict s2, size_t n); | 将 s2 所指向的字符串中最多 n 个字符或直到空字符复制到 s1 所指向的位置；如果在复制 n 个字符之前在 s2 中遇到空字符，则追加空字符以使总数达到 n；如果在到达空字符之前复制了 n 个字符，则不追加空字符；函数返回 s1。 |
| int strcmp(const char *s1, const char *s2); | 比较 s1 和 s2 所指向的字符串；如果所有配对都匹配，则两个字符串相同；否则，字符串按第一个不匹配的配对比较。字符使用字符代码值比较；函数在字符串相同时返回零，小于零表示第一个字符串小于第二个，大于零表示字符串数组更大。 |
| int strcoll(const char *s1, const char *s2); | 工作方式与 strcmp() 相同，只是它使用 setlocale() 函数设置的当前区域设置的 LC_COLLATE 类别指定的排序序列。 |
| int strncmp(const char *s1, const char *s2, size_t n); | 比较 s1 和 s2 所指向的数组的前 n 个字符或直到第一个空字符；如果所有测试的配对都匹配，则两个数组相同；否则，数组按第一个不匹配的配对比较。字符使用字符代码值比较；函数在数组相同时返回零，小于零表示第一个数组小于第二个，大于零表示第一个数组更大。 |
| size_t strxfrm(char * restrict s1, const char * restrict s2, size_t n); | 转换 s2 中的字符串并将最多 n 个字符（包括终止空字符）复制到 s1 所指向的数组；转换的标准是，两个转换后的字符串按 strcmp() 放置的顺序与 strcoll() 将未转换的字符串放置的顺序相同；函数返回转换后字符串的长度（不包括终止空字符）。 |

| 原型 | 描述 |
|---|---|
| char *strchr(const char *s, int c); | 在 s 所指向的字符串中搜索 c（转换为 char）的第一次出现；空字符是字符串的一部分；返回指向第一次出现的指针，如果未找到则返回 NULL。 |
| size_t strcspn(const char *s1, const char *s2); | 返回 s1 的最大初始段的长度，该段不包含在 s2 中找到的任何字符。 |
| char *strpbrk(const char *s1, const char *s2); | 返回指向 s1 中第一个与 s2 中的任何字符匹配的字符位置的指针；如果未找到匹配项则返回 NULL。 |
| char *strrchr(const char *s, int c); | 在 s 所指向的字符串中搜索 c（转换为 char）的最后一次出现；空字符是字符串的一部分；返回指向第一次出现的指针，如果未找到则返回 NULL。 |
| size_t strspn(const char *s1, const char *s2); | 返回 s1 的最大初始段的长度，该段完全由 s2 中的字符组成。 |
| char *strstr(const char *s1, const char *s2); | 返回指向 s1 中 s2 字符序列（不包括终止空字符）的第一次出现位置的指针；如果未找到匹配项则返回 NULL。 |
| char *strtok(char * restrict s1, const char * restrict s2); | 此函数将字符串 s1 分解为单独的标记；字符串 s2 包含被识别为标记分隔符的字符。函数按顺序调用。对于初始调用，s1 应指向要分解为标记的字符串。函数定位在非分隔符字符之后出现的第一个标记分隔符并将其替换为空字符。它返回一个指向保存第一个标记的字符串的指针。如果未找到标记，则返回 NULL。要在字符串中找到进一步的标记，请再次调用 strtok()，但第一个参数为 NULL。每次后续调用返回指向下一个标记的指针，或如果未找到进一步的标记则返回 NULL。 （参见本表之后的示例。） |
| char * strerror(int errno); | 返回指向与 errno 中存储的错误号相对应的实现相关错误消息字符串的指针。 |
| int strlen(const char * s); | 返回字符串 s 中字符的数量（不包括终止空字符）。 |

strtok() 函数在使用方式上有点不寻常，因此这里有一个简短的示例：

```
#include <stdio.h>
#include <string.h>
```

```
fy = sin(fx);  // expands to fy = sinf(fx)
cly = sin(clx); // expands to cly = csinl(clyx)
```

头文件为三类函数定义了通用宏。第一类由 math.h 和 complex.h 函数组成，使用 l 和 f 后缀以及 c 前缀定义了六种变体，如之前的 sin() 示例所示。在这种情况下，通用宏的名称与该函数的 double 类型版本相同。

第二类由 math.h 函数组成，使用 l 和 f 后缀定义了三种变体，没有复数对应项，例如 erf()。在这种情况下，宏名称与不带后缀的函数相同，例如此示例中的 erf()。使用复数参数使用此类宏的效果未定义。

第三类由 complex.h 函数组成，使用 l 和 f 后缀定义了三种变体，没有实数对应项，例如 cimag()。在这种情况下，宏名称与不带后缀的函数相同，例如此示例中的 cimag()。使用实数参数使用此类宏的效果未定义。

## 表 RS.V.38 通用数学函数

| acos | asin | atanb | acosh | asinh | atanh |
| cos | sin | tan | cosh | sinh | tanh |
| exp | log | pow | sqrt | fabs | atan2 |
| cbrt | ceil | copysign | erf | erfc | exp2 |
| expm1 | fdim | floor | fma | fmax | fmin |
| fmod | frexp | hypot | ilogb | ldexp | lgamma |
| llrint | llround | log10 | log1p | log2 | logb |
| lrint | lround | nearbyint | nextafter | nexttoward | remainder |
| remquo | rint | round | scalbn | scalbln | tgamma |
| trunc | carg | cimag | conj | cproj | creal |

在 C11 之前，实现者不得不求助于标准的扩展来实现通用宏。但 _Generic 表达式的添加允许使用标准 C11 进行直接实现。

## 表 RS.V.41 struct tm 结构体的成员

| 成员 | 描述 |
|---|---|
| int tm_sec | 分钟后的秒数（0–61） |
| int tm_min | 小时后的分钟数（0–59） |
| int tm_hour | 午夜后的小时数（0–23） |
| int tm_mday | 月份中的天数（0–31） |
| int tm_mon | 自一月以来的月份数（0–11） |
| int tm_year | 自 1900 年以来的年数 |
| int tm_wday | 自星期日以来的天数（0–6） |
| int tm_yday | 自 1 月 1 日以来的天数（0–365） |
| int tm_isdst | 夏令时标志（大于零的值表示 DST 生效；零表示未生效；负值表示信息不可用） |

术语日历时间表示当前日期和时间；例如，它可以是自 1900 年第一秒以来经过的秒数。术语本地时间是针对本地时区表示的日历时间。表 RS.V.42 列出了时间函数。

## 表 RS.V.42 时间函数

| 原型 | 描述 |
|---|---|
| clock_t clock(void); | 返回程序被调用以来处理器时间的实现最佳近似值；除以 CLOCKS_PER_SEC 可得到以秒为单位的时间。如果时间不可用或无法表示，则返回 (clock_t)(-1)。 |
| double difftime(time_t t1, time_t t0); | 计算两个日历时间之间的差值（t1− t0）；以秒为单位表示结果并返回结果。 |
| time_t mktime(struct tm *tmptr); | 将 tmptr 所指向的结构中的分解时间转换为日历时间；使用与 time() 函数相同的编码，结构会被修改，即超出范围的值会被调整（例如，2 分钟 100 秒变为 3 分钟 40 秒），并且 tm_wday 和 tm_yday 会设置为其他成员所暗示的值。如果日历时间无法表示，则返回 (time_t)(-1)；否则，以 time_t 格式返回日历时间。 |
| time_t time(time_t *ptm) | 返回当前日历时间，并将其放置在 ptm 所指向的位置，前提是 ptm 不为 NULL。如果日历时间不可用，则返回 (time_t)(-1)。 |

