

### 声明

以下是 strcat() 函数的声明。

```c
char *strcat(char *dest, const char *src)
```

### 参数

- dest -- 这是指向目标数组的指针，该数组应包含一个 C 字符串，并且应足够大，以容纳拼接后的结果字符串。
- src -- 这是要追加的字符串。它不应与目标重叠。

### 返回值

该函数返回指向结果字符串 dest 的指针。

### 示例

以下示例展示了 strcat() 函数的用法。

```c
#include <stdio.h>
#include <string.h>

int main ()
{
    char src[50], dest[50];

    strcpy(src, "This is source");
    strcpy(dest, "This is destination");

    strcat(dest, src);

    printf("Final destination string : |%s|", dest);

    return(0);
}
```

让我们编译并运行上面的程序，这将产生以下结果：

```
Final destination string : |This is destinationThis is source|
```

## char *strncat(char *dest, const char *src, size_t n)

### 描述

C 库函数 char *strncat(char *dest, const char *src, size_t n) 将 src 指向的字符串追加到 dest 指向的字符串末尾，最多追加 n 个字符。

### 声明

以下是 strncat() 函数的声明。

```c
char *strncat(char *dest, const char *src, size_t n)
```

### 参数

- dest -- 这是指向目标数组的指针，该数组应包含一个 C 字符串，并且应足够大，以容纳拼接后的结果字符串，其中包括额外的空字符。
- src -- 这是要追加的字符串。
- n -- 这是要追加的最大字符数。

### 返回值

该函数返回指向结果字符串 dest 的指针。

### 示例

以下示例展示了 strncat() 函数的用法。

```c
#include <stdio.h>
#include <string.h>

int main ()
{
    char src[50], dest[50];

    strcpy(src, "This is source");
    strcpy(dest, "This is destination");

    strncat(dest, src, 15);

    printf("Final destination string : |%s|", dest);

    return(0);
}
```

让我们编译并运行上面的程序，这将产生以下结果：

```
Final destination string : |This is destinationThis is source|
```

## char *strchr(const char *str, int c)

### 描述

C 库函数 char *strchr(const char *str, int c) 在参数 str 指向的字符串中搜索字符 c（一个无符号字符）的首次出现。

### 声明

以下是 strchr() 函数的声明。

```c
char *strchr(const char *str, int c)
```

### 参数

- str -- 这是要扫描的 C 字符串。
- c -- 这是要在 str 中搜索的字符。

### 返回值

返回指向字符串 str 中字符 c 首次出现位置的指针；如果未找到该字符，则返回 NULL。

### 示例

以下示例展示了 strchr() 函数的用法。

```c
#include <stdio.h>
#include <string.h>

int main ()
{
    const char str[] = "http://www.tutorialspoint.com";
    const char ch = '.';
    char *ret;

    ret = strchr(str, ch);

    printf("String after |%c| is - |%s\n", ch, ret);

    return(0);
}
```

让我们编译并运行上面的程序，这将产生以下结果：

```
String after |.| is - |.tutorialspoint.com|
```

## int strcmp(const char *str1, const char *str2)

### 描述

C 库函数 **int strcmp(const char *str1, const char *str2)** 将 **str1** 指向的字符串与 **str2** 指向的字符串进行比较。

### 声明

以下是 strcmp() 函数的声明。

```c
int strcmp(const char *str1, const char *str2)
```

### 参数

- **str1** -- 这是要比较的第一个字符串。
- **str2** -- 这是要比较的第二个字符串。

### 返回值

该函数返回值如下：

- 如果返回值 < 0，则表示 str1 小于 str2。
- 如果返回值 > 0，则表示 str2 小于 str1。
- 如果返回值 = 0，则表示 str1 等于 str2。

### 示例

以下示例展示了 strcmp() 函数的用法。

```c
#include <stdio.h>
#include <string.h>

int main ()
{
   char str1[15];
   char str2[15];
   int ret;

   strcpy(str1, "abcdef");
   strcpy(str2, "ABCDEF");

   ret = strcmp(str1, str2);

   if(ret < 0)
   {
      printf("str1 is less than str2");
   }
   else if(ret > 0)
   {
      printf("str2 is less than str1");
   }
   else
   {
      printf("str1 is equal to str2");
   }

   return(0);
}
```

让我们编译并运行上面的程序，这将产生以下结果：

```
str2 is less than str1
```

## int strncmp(const char *str1, const char *str2, size_t n)

### 描述

C 库函数 **int strncmp(const char *str1, const char *str2, size_t n)** 最多比较 **str1** 和 **str2** 的前 **n** 个字节。

### 声明

以下是 strncmp() 函数的声明。

```c
int strncmp(const char *str1, const char *str2, size_t n)
```

### 参数

- **str1** -- 这是要比较的第一个字符串。
- **str2** -- 这是要比较的第二个字符串。
- **n** -- 要比较的最大字符数。

### 返回值

该函数返回值如下：

- 如果返回值 < 0，则表示 str1 小于 str2。
- 如果返回值 > 0，则表示 str2 小于 str1。
- 如果返回值 = 0，则表示 str1 等于 str2。

### 示例

以下示例展示了 strncmp() 函数的用法。

```c
#include <stdio.h>
#include <string.h>

int main ()
{
    char str1[15];
    char str2[15];
    int ret;

    strcpy(str1, "abcdef");
    strcpy(str2, "ABCDEF");

    ret = strncmp(str1, str2, 4);

    if(ret < 0)
    {
        printf("str1 is less than str2");
    }
    else if(ret > 0)
    {
        printf("str2 is less than str1");
    }
    else
    {
        printf("str1 is equal to str2");
    }

    return(0);
}
```

让我们编译并运行上面的程序，这将产生以下结果：

```
str2 is less than str1
```

## int strcoll(const char *str1, const char *str2)

### 描述

C 库函数 **int strcoll(const char *str1, const char *str2)** 将字符串 **str1** 与 **str2** 进行比较。结果取决于区域设置的 LC_COLLATE 设置。

### 声明

以下是 strcoll() 函数的声明。

```c
int strcoll(const char *str1, const char *str2)
```

### 参数

- **str1** -- 这是要比较的第一个字符串。
- **str2** -- 这是要比较的第二个字符串。

### 返回值

该函数返回值如下：

- 如果返回值 < 0，则表示 str1 小于 str2。
- 如果返回值 > 0，则表示 str2 小于 str1。
- 如果返回值 = 0，则表示 str1 等于 str2。

### 示例

以下示例展示了 strcoll() 函数的用法。

```c
#include <stdio.h>
#include <string.h>

int main ()
{
   char str1[15];
   char str2[15];
   int ret;

   strcpy(str1, "abc");
   strcpy(str2, "ABC");

   ret = strcoll(str1, str2);

   if(ret > 0)
   {
      printf("str1 is less than str2");
   }
   else if(ret < 0)
   {
      printf("str2 is less than str1");
   }
   else
   {
      printf("str1 is equal to str2");
   }

   return(0);
}
```

让我们编译并运行上面的程序，这将产生以下结果：

```
str1 is less than str2
```

## char *strcpy(char *dest, const char *src)

### 描述

C 库函数 char *strcpy(char *dest, const char *src) 将 src 指向的字符串复制到 dest。

### 声明

以下是 strcpy() 函数的声明。

```c
char *strcpy(char *dest, const char *src)
```

### 参数

- dest -- 这是指向目标数组的指针，内容将被复制到该数组中。
- src -- 这是要复制的字符串。

### 返回值

返回指向目标字符串 dest 的指针。

### 示例

以下示例展示了 strcpy() 函数的用法。

```c
#include <stdio.h>
#include <string.h>

int main()
{
    char src[40];
    char dest[100];

    memset(dest, '\0', sizeof(dest));
    strcpy(src, "This is tutorialspoint.com");
    strcpy(dest, src);

    printf("Final copied string : %s\n", dest);

    return(0);
}
```

让我们编译并运行上面的程序，这将产生以下结果：

```
Final copied string : This is tutorialspoint.com
```

## char *strncpy(char *dest, const char *src, size_t n)

### 描述

C 库函数 char *strncpy(char *dest, const char *src, size_t n) 将 src 指向的字符串中最多 n 个字符复制到 dest。如果 src 的长度小于 n，则 dest 的剩余部分将用空字节填充。

### 声明

