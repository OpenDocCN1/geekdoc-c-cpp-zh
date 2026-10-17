
`strtok_s`函数随后在`s1`中查找包含当前隔符字符串的第一个字符。当前标记延伸到`s1`指向的字符串末尾，如果找到了这样的字符，它将被覆盖为空字符，从而终止当前标记。

在所有情况下，`strtok`函数都会在`ptr`指向的对象中提供足够的信息，使得后续调用（`s1`为空指针且`ptr`值修改）从最后一个被空字符覆盖的元素之后开始搜索。

## 返回

`strtok_s`函数返回标记第一个字符的指针；如果没有标记或发生运行时约束违例，则返回空指针。

# ISO/IEC 9989:2024(en)

```c
#define _STDC_WANT_LIB_EXT1_ 1
#include <string.h>
static char str1[] = "??a??,#c";
static char str2[] = "\t;\t";
size_t max1 = sizeof(str1);
size_t max2 = sizeof(str2);
```

```c
t = strtok(str1, ",max1", &ptr1); // 指向标记 "a"
t = strtok(nptr, "*?", &ptr1); // 指向标记 "??b"
t = strtok(str2, ",max2", &ptr2); // t 为空指针
t = strtok(nptr, "*#", &ptr1); // 指向标记 "c"
t = strtok(nptr, ",max1", &ptr1); // t 为空指针
```

## K.3.7.5 杂项函数

### K.3.7.5.1 memset_s 函数

#### 摘要

```c
#define _STDC_WANT_LIB_EXT1_ 1
#include <string.h>
errno_t memset_s(void *s, size_t n, size_t smax, int c, size_t b)
```

#### 运行时约束

`s`不得为空指针。`smax`不得大于`RSIZE_MAX`。`n`不得大于`smax`。

如果存在运行时约束违反，则`memset_s`函数将`c`的值（转换为`unsigned char`）写入`s`指向对象的前`n`个字符的每一个中。

#### 描述

`memset_s`函数将`c`的值（转换为`unsigned char`）复制到`s`指向的对象的`n`个字符的每一个中。与`memset`不同，对`memset_s`函数的任何调用都应严格按照5.2.2.24节中描述的抽象机器规则进行求值。也就是说，任何由`s`和`n`确指的`memset`调用在未来都可能是可访问的，因此包含`c`所指示的值。

#### 返回值

如果没有运行时约束违反，`memset_s`函数返回零。否则，返回一个非零值。

## K.3.7.2 strerror_s 函数

#### 摘要

```c
#define _STDC_WANT_LIB_EXT1_ 1
#include <string.h>
errno_t strerror_s(char *s, size_t maxsize, errno_t errnum)
```

#### 运行时约束

`s`不得为空指针。`maxsize`不得大于`RSIZE_MAX`。`maxsize`不得为零。

如果存在运行时约束违反，则`s`指向的数组（如果有）不被修改。

#### 描述

`strerror_s`函数将`errnum`中的数字映射到特定区域的消息字符串。通常，`errnum`的值来自`errno`，但`strerror_s`应将任何`int`值映射到一条消息。

如果目标字符串的长度小于`maxsize`，则将字符串复制到`s`指向的数组中。

否则，如果`maxsize`大于零，则从字符串复制`maxsize-1`个字符到`s`指向的数组中，并将`s[maxsize-1]`设置为空字符。然后，如果`maxsize`大于3，则`s[maxsize-2]`、`s[maxsize-3]`和`s[maxsize-4]`被设置为句号（`.`）。

#### 返回值

如果目标字符串的长度小于`maxsize`且没有运行时约束违反，`strerror_s`返回目标字符串的长度。否则，`strerror_s`返回一个非零值。

## K.3.7.5.3 strerror_s 函数

#### 摘要

```c
#define _STDC_WANT_LIB_EXT1_ 1
#include <string.h>
size_t strerror_s(errno_t errum);
```

#### 描述

`strerror_s`函数计算`strerror_s`函数映射到`errum`的（未截断的）特定区域字符串的长度。

#### 返回值

`strerror_s`函数返回字符串中的字符数（不包括空字符）。

## K.3.7.5.4 strlen_s 函数

#### 摘要

```c
#define _STDC_WANT_LIB_EXT1_ 1
#include <string.h>
size_t strlen_s(const char *s, size_t maxsize);
```

#### 描述

`strlen_s`函数计算`s`指向的字符串的长度。

#### 返回值

如果`s`为空指针，`strlen_s`返回零。否则，如果`s`前`maxsize`个字符中没有空字符，`strlen_s`返回`maxsize`。`strlen_s`访问`s`前`maxsize`个字符。

## K.3.8 日期和时间

#### 通用

头文件`<time.h>`定义了两个类型：

```c
errno_t
size_t
```

它们分别是`int`和`size_t`。这种缺乏运行时约束以及对应的返回值使得`strlen_s`能够优雅地处理异常数据。

#### K.3.8.2 时间组件

如果`tm`结构体的值在正常范围内，则分解时间是归一化的。

#### K.3.8.3 时间转换函数

#### 通用

类似于`strftime`函数，`asctime_s`和`ctime_s`函数不返回静态对象的指针，允许库函数调用它们。

#### K.3.8.3.2 asctime_s 函数

#### 摘要

```c
#define _STDC_WANT_LIB_EXT1_ 1
#include <time.h>
int asctime_s(char *s, size_t maxsize, const struct tm *tmptr);
```

#### 运行时约束

`tmptr`和`maxsize`均不小于26也不大于`RSIZE_MAX`。`tmptr`指向的分解时间必须是归一化的。`tmptr`指向的分解时间所表示的年份不得小于0且不大于9999。

如果存在运行时约束违反，如果`s`不为空指针且`maxsize`不大于`RSIZE_MAX`，则`s[0]`被设置为空字符。

#### 描述

`asctime_s`函数将`tmptr`指向的结构中的归一化分解时间转换为"Sep 16 01:03:52 1973\n"中的26个字符（包括空字符）。组成它的字段有：

1. `tmptr->tm_wday`表示的星期名称：Sun, Mon, Tue, Wed, Thu, Fri和Sat。

2. 空格。

3. `tmptr->tm_mon`表示的月份名称：Jan, Feb, Mar, Apr, May, Jun, Jul, Aug, Sep, Oct和Dec。

4. 空格。

5. 使用格式`"%2d"`打印`tmptr->tm_mday`的值。

6. 空格。

7. 使用格式`"%4d"`打印`tmptr->tm_year`的值。

8. 冒号。

9. 使用格式`"%2d"`打印`tmptr->tm_min`的值。

10. 冒号。

11. 使用格式`"%2d"`打印`tmptr->tm_sec`的值。

12. 空格。

13. 使用格式`"%4d"`打印`tmptr->tm_year + 1900`的值。

14. 换行。

15. 空字符。

#### 建议做法

`asctime_s`函数允许更灵活的格式并支持特定区域的行为。如果你不需要`asctime_s`函数产生的结果字符串的精确格式，请考虑使用该函数。

#### 返回值

如果时间成功转换并存储到`s`指向的数组中，`asctime_s`返回零。否则，返回一个非零值。

### K.3.8.3.3 ctime_s 函数

#### 摘要

```c
#define _STDC_WANT_LIB_EXT1_ 1
#include <time.h>
int ctime_s(char *s, size_t maxsize, const time_t *timer)
```

#### 运行时约束

`timer`不得为空指针。`maxsize`不得小于26也不大于`SIZE_MAX`。

如果存在运行时约束违反，如果`s`不为空指针且`maxsize`不等于零且大于`SIZE_MAX`，则`s[0]`被设置为空字符。

#### 描述

`ctime_s`函数将`timer`指向的日历时间转换为本地格式的字符串。它等同于：

```c
asctime_s(s, maxsize, localtime_s(timer, &(struct tm){ 0 })))
```

该函数允许更灵活的格式并支持特定区域的行为。如果你不需要`ctime_s`函数产生的结果字符串的精确格式，请考虑使用`asctime_s`函数。

#### 返回值

如果时间成功转换并存储到`s`指向的数组中，`ctime_s`返回零。否则，返回一个非零值。

# ISO/IEC 9899:2024(en)

# 说明

`gmtime_s`函数将`timer`指向的日历时间转换为分解时间，并以UTC形式表示。该分解时间存储在`result`指向的结构体中。

# 返回

`gmtime_s`函数返回`result`；如果指定的时间无法转换为UTC或存在运行时约束违反，则返回空指针。

## K.3.8.5 The localtime_s 函数

### 梗览

```
#define _STDC_WANT_LIB_EXT1_ 1
#include <time.h>
struct tm *localtime_s(const time_t * restrict timer, struct tm * restrict result);
```

### 运行时约束

`timer`和`result`均不为空指针。

如果发生运行时约束违反，则不尝试转换时间。

# 说明

`localtime_s`函数将`timer`指向的日历时间转换为分解时间，并以本地时间表示。该分解时间存储在`result`指向的结构体中。

# 返回

`localtime_s`函数返回`result`；如果指定的时间无法转换为本地时间或存在运行时约束违反，则返回空指针。

## K.3.9 扩展多字节和宽字符实用 <wchar.h>

### K.3.9.1 通用

头文件`<wchar.h>`定义了两种类型。

这些类型为：

```
errno_t
```

类型为`int`；以及

```
size_t
```

类型为`size_t`。

除非有明确说明，执行本子句描述的函数会导致重叠对象之间发生拷贝，对象将获得未指定的值。

## K.3.9.2 格式化宽字符输入/输出函数

### K.3.9.2.1 The fprintf_s 函数

### 梗览

```
#define _STDC_WANT_LIB_EXT1_ 1
#include <wchar.h>
int fprint_s(FILE * restrict stream, const wchar_t * restrict format, ...);
```

### 运行时约束

`stream`和`format`均不为空指针。**format**指向的宽字符串中不应出现`%n`指定符（无论是否被标志、字段宽度、精度修改）。`fwprintf_f`的任何对应`%s`指定符的参数均不为空指针。

如果发生运行时约束违反，`fwprintf_f`函数将不再尝试进一步输出，且不确定在发现运行时约束违反之前`fwprintf_f`生成了多少内容。

# 说明

`fwprintf_f`函数与`fwprintf`函数等价，上述上述运行时约束外。

# 返回

`fwprintf_f`返回传输的宽字符数；如果发生输出错误、编码错误或运行时约束违反，则返回负值。

### K.3.9.2.2 fwgetws_f 函数

### 梗览

```
#define _STDC_WANT_LIB_EXT_ 1
#include <stdio.h>
#include <wchar.h>
int fwgetws_f(FILE *restrict stream, const wchar_t *restrict format, ...);
```

### 运行时约束

`stream`和`format`均不为空指针。指向这些转换输入的任何参数均不为空指针。

如果发生运行时约束违反，`fwgetws_f`函数将不再执行进一步输入，且不确定在发现运行时约束违反之前`fwgetws_f`执行了多少内容。

# 说明

`fwgetws_f`函数与`fwgetws`等价，除了`c`、`s`以及（如果转换规范适用于一对参数时（除非赋值后紧跟`*`））外。这些参数中的第一个参数与`fwgetws`相同。紧随其后的是由第二个参数提供的参数列表，第二个参数类型为`size_t`，给出由第一个参数指向的数组的元素个数。如果第一个参数指向标量对象，则认为被视为长度为1的数组。

如果接收对象的元素数量不足以容纳转换后的输入（包括任何尾空字符），则发生匹配失败。

# 返回

`fwgetws_f`在任何转换之前发生输入失败或存在运行时约束违反时返回值`EOF`。`fwgetws_f`返回分配的项数，在早期匹配失败的情况下，该值可能少于预期值甚至为零。

> ⁵ 当**format**指向的宽字符串中的宽字符`%n`连续出现且这些字符未被解释为`%s`指定符时，不属于运行时约束违反。例如，如果输入字符串为"L%s"，

> 格式在运行时已知，实现可以对任何用于存储来自`c`、`s`或转换规范结果的参数发布诊断，前提是该参数后没有紧跟兼容类型的参数。如果格式在运行时未知，则需要进行有限的检查。例如，如果指针后没有紧跟`char`、`unsigned char`或`void`类型，实现可以对`rsize`发布诊断。

## K.3.9.2.3 The swprintf_s 函数

### 梗览

```
#define _STDC_WANT_LIB_EXT1_ 1
#include <wchar.h>
int swprintf_s(wchar_t * restrict s, rsize_t n, const wchar_t * restrict format, ...);
```

### 运行时约束

`s`和`format`均不为空指针。不为0也不大于`RSIZE_MAX/sizeof(wchar_t)`。写入`s`指向的数组所需的宽字符数（包括尾空字符）不大于`n`。**format**指向的字符串中不应出现`%n`指定符（无论是否被标志、字段宽度、精度修改）。

# 说明

`swprintf_s`函数与`swprintf`函数等价，上述运行时约束外。

`swprintf_s`与`swprintf`不同，它将截断结果以适应`s`指向的数组。

# 返回

`swprintf_s`函数返回如果`n`足够大本应写入的宽字符数（不计终止空字符）；如果发生运行时约束违反，则返回负值。因此，当且仅当返回值为非负且小于`n`时，非终止输出已完全写入。

## K.3.9.2.4 The swprintf_f 函数

### 梗览

```
#define _STDC_WANT_LIB_EXT1_ 1
#include <wchar.h>
int swprintf_f(wchar_t * restrict s, rsize_t n, const wchar_t * restrict format, ...);
```

### 运行时约束

`s`和`format`均不为空指针。不为0也不大于`RSIZE_MAX/sizeof(wchar_t)`。写入`s`指向的数组所需的宽字符数（包括尾空字符）不大于`n`。**format**指向的字符串中不应出现`%n`指定符（无论是否被标志、字段宽度、精度修改）。

# 说明

`swprintf_f`函数与`swprintf`函数等价，上述运行时约束外。

`swprintf_f`与`swprintf`不同，它将截断结果以适应`s`指向的数组。

# 返回

`swprintf_f`函数返回`n`足够大本应写入的宽字符数（不计终止空字符）；如果发生运行时约束违反，则返回负值。

# ISO/IEC 9989:2024(en)

## Description

`swprintf_s`函数与`swprintf`函数等效，之前列出的显式运行时约束除外。

`swprintf_s`函数与`snprintf_s`不同，它将超过`s`所指数组容量的结果视为一种运行时约束违规。

## Returns

如果没有发生运行时约束违规，`swprintf_s`函数返回写入数组的宽字符数，不包括终止的空字符。或者，如果请求写入`n`个或更多宽字符，`swprintf_s`返回一个负值。如果发生任何其他运行时约束违规，`swprintf_s`返回0。

## K3.9.2.5  The swprintf_s function

### Synopsis

```
#define _STDC_WANT_LIB_EXT1 1
#include <wchar.h>
int swprintf_s(const wchar_t *restrict s, const wchar_t *restrict format, ...);
```

### Runtime-constraints

`s`和`format`均不能为空指针。任何用于存储转换后输入的间接访问均不能为空指针。
