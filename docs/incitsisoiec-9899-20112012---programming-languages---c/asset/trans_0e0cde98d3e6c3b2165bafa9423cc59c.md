

返回值并不一定是写入或读取字符数量的有意义的测量。

## 返回

如果成功，`ftell` 函数返回流的文件位置指示器的当前值。如果失败，`ftell` 函数返回 -1 并在 `errno` 中存储一个由实现定义的正值。

## 7.21.9.5 rewind 函数

### 摘要

```
#include <stdio.h>
void rewind(FILE *stream);
```

### 描述

`rewind` 函数将指向文件开头的流的文件位置指示器设置为文件开头。它等同于

```
(void) fseek(stream, 0, SEEK_SET)
```

不同在于它还会清除流的错误指示器。

## 返回

`rewind` 函数不返回值。

## 7.21.10 错误处理函数

### 7.21.10.1 clearerr 函数

### 摘要

```
#include <stdio.h>
void clearerr(FILE *stream);
```

### 描述

`clearerr` 函数清除由 `stream` 指向的流的文件结束标志和错误指示器。

## 返回

`clearerr` 函数不返回值。

## 7.21.10.2 feof 函数

### 摘要

```
#include <stdio.h>
int feof(FILE *stream);
```

### 描述

`feof` 函数测试由 `stream` 指向的流的文件结束指示器。

## 返回

当且仅当流的文件结束指示器被设置时，`feof` 函数返回非零。

## 7.21.10.3 ferror 函数

### 摘要

```
#include <stdio.h>
int ferror(FILE *stream);
```

### 描述

`ferror` 函数测试由 `stream` 指向的流的错误指示器。

## 返回

当且仅当流的错误指示器被设置时，`ferror` 函数返回非零。

## 7.21.10.4 perror 函数

### 摘要

```c
#include <stdio.h>
void perror(const char *s);
```

### 描述

`perror` 函数将错误号（映射到整数表达式 `errno`）映射错误消息。它首先向标准错误流写入一系列字符：（如果 `s` 不是空指针且由 `s` 指向的字符不是空字符），则写入 `s` 指向的字符串，后跟一个冒号（:）和一个空格；随后是适当的错误消息以及一个换行符。错误消息字符串的内容与 `strerror` 函数带有参数 `errno` 返回的内容相同。

## 返回

`perror` 函数不返回值。

前向引用：`strerror` 函数 (7.24.6.2)。

## 7.22 通用工具 <stdlib.h>

头文件 `<stdlib.h>` 声明了五种类型和若干通用函数，并定义了若干宏。(291)

的类型有 `size_t` 和 `wchar_t`（均在 7.19 中描述过），

```
div_t
```

这是一个结构类型，是 `div` 函数返回值的类型，

```
ldiv_t
```

这是一个结构类型，是 `ldiv` 函数返回值的类型，

```
ll1div_t
```

这是一个结构类型，是 `ll1div` 函数返回值的类型。

定义的宏有 `NULL`（在 7.19 中描述过）；

```
EXIT_FAILURE
```

以及

```
EXIT_SUCCESS
```

它们展开为整数常量表达式，可以作为 `exit` 函数的参数，分别向宿主环境返回不成功或成功的终止状态；

```
RAND_MAX
```

它展开为整数常量表达式，是 `rand` 函数返回的最大值；以及

```
MB_CUR_MAX
```

它展开为类型为 `size_t` 的正整数表达式，表示当前区域设置（类别 `LC_CTYPE`）指定的扩展字符集中多字节字符的最大字节数，其值永远不会大于 `MB_LEN_MAX`。

## 7.22.1 数字转换函数

`atof`、`atoi` 和 `atoll` 函数在出错时不一定影响整数表达式 `errno` 的值。如果结果无法表示，则行为未定义。

### 7.22.1.1 atof 函数

### 摘要

```c
#include <stdlib.h>
double atof(const char *nptr);
```

### 描述

`atof` 函数将由 `nptr` 指向的字符串起始部分转换为 `double` 表示。除了出错的行为外，它等同于

```
strtod(nptr, (char **)NULL)
```

## 返回

`atof` 函数返回转换后的值。

前向引用：`strtod`、`strtof` 和 `strtol` 函数 (7.22.1.3)。

### 7.22.1.2 atoi, atoi 和 atoll 函数

### 摘要

```c
#include <stdlib.h>
int atoi(const char *nptr);
long atoi(const char *nptr);
long int atoll(const char *nptr);
```

### 描述

`atoi`、`atoi` 和 `atoll` 函数分别将由 `nptr` 指向的字符串起始部分转换为 `int`、`long int` 和 `long long int` 表示。除了出错的行为外，它们等同于

```
atoi: (int) strtol(nptr, (char **)NULL, 10)
atoi: strtol(nptr, (char **)NULL, 10)
atoll: strtol(nptr, (char **)NULL, 10)
```

## 返回

`atoi`、`atoi` 和 `atoll` 返回转换值。

前向引用：`strtol`、`strtoll` (7.22)。

## 7.22.1.3 stod, strtof 和 strtol 函数

### 摘要

```c
#include <stdlib.h>
double strtod(const char *nptr);
float strtof(const char *nptr);
long strtol(const char *nptr);
```

### 描述

`stod`、`strtof` 和 `strtol` 函数分别将由 `nptr` 指向的字符串转换为 `double`、`float` 和 `long` 表示。除了出错的行为外，它们将输入字符串分解为三部分：数字序列、可选的小数点以及可选的指数。然后尝试将其转换为相应的类型。

## 返回

`stod`、`strtof` 和 `strtol` 返回转换值。

## 7.22.1.4 strtod 函数

### 摘要

```c
#include <stdlib.h>
double strtod(const char *nptr, char **endptr);
```

### 描述 

`strtod` 函数将由 `nptr` 指向的字符串起始部分转换为 `double` 表示。除了出错的行为外，它等同于

```
strtod(nptr, (char **)NULL)
```

## 返回

`strtod` 函数返回转换值。

前向引用：`strtof`、`strtol` 函数 (7.22.1.3)。

## 7.22.1.5 strtof 函数

### 摘要

```c
#include <stdlib.h>
float strtof(const char *nptr, char **endptr);
```

### 描述 

`strtof` 函数将由 `nptr` 指向的字符串起始部分转换为 `float` 表示。除了出错的行为外，它等同于

```
strtof(nptr, (char **)NULL)
```

## 返回

`strtof` 函数返回转换值。

前向引用：`strtod`、`strtol` 函数 (7.22.1.3)。

## 7.22.1.6 strtol 函数

### 摘要

```c
#include <stdlib.h>
long strtol(const char *nptr, char **endptr, int base);
```

### 描述 

`strtol` 函数将由 `nptr` 指向的字符串起始部分转换为 `long` 表示。除了出错的行为外，它等同于

```
strtol(nptr, (char **)NULL, base)
```

## 7.22.1.7 strtoll 函数

### 摘要

```c
#include <stdlib.h>
long long strtoll(const char *nptr, char **endptr, int base);
```

### 描述 

`strtoll` 函数将由 `nptr` 指向的字符串起始部分转换为 `long long` 表示。除了出错的行为外，它等同于

```
strtoll(nptr, (char **)NULL, base)
```

## 7.22.1.8 strtou 函数

### 摘要

```c
#include <stdlib.h>
unsigned long strtou(const char *nptr, char **endptr, int base);
```

### 描述 

`strtou` 函数将由 `nptr` 指向的字符串起始部分转换为 `unsigned long` 表示。除了出错的行为外，它等同于

```
strtou(nptr, (char **)NULL, base)
```

## 7.22.1.9 strquad 函数

### 摘要

```c
#include <stdlib.h>
long double strquad(const char *nptr, char **endptr);
```

### 描述 

`strquad` 函数将由 `nptr` 指向的字符串起始部分转换为 `long double` 表示。除了出错的行为外，它等同于

```
strquad(nptr, (char **)NULL)
```

