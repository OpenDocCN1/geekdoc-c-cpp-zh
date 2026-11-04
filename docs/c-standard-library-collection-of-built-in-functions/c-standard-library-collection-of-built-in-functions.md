# C 标准库：内置函数集合

## 关于本教程

C 是一种通用、过程式、命令式计算机编程语言，由 Dennis M. Ritchie 于 1972 年在贝尔电话实验室开发，用于开发 Unix 操作系统。

C 是使用最广泛的计算机语言之一，与 Java 编程语言一起在流行度排名中不断波动于第一位，后者同样流行且被现代软件程序员广泛使用。

C 标准库是一组 C 内置函数、常量和头文件，如 <assert.h>、<ctype.h> 等。本库将作为 C 程序员的参考手册。

## 读者对象

C 标准库是 C 程序员的参考资料，可帮助他们进行系统编程相关项目。所有 C 函数都以用户友好的方式进行了解释，您可以将其复制并粘贴到您的 C 项目中。

## 先决条件

对 C 编程语言的基本理解将有助于您理解本库中涵盖的 C 内置函数。





## 引言

C 标准库的 **assert.h** 头文件提供了一个名为 **assert** 的宏，它可用于验证程序所做的假设，并在假设为假时打印诊断消息。

已定义的宏 **assert** 引用了另一个宏 **NDEBUG**，该宏不属于 `<assert.h>` 的一部分。如果在源文件中包含 `<assert.h>` 的位置将 NDEBUG 定义为宏名，则 **assert** 宏定义如下：

```c
#define assert(ignore) ((void)0)
```

## 库宏

以下是定义在头文件 assert.h 中的唯一函数：

| 序号 | 函数与描述 |
|---|---|
| 1 | `void assert(int expression)`<br>这实际上是一个宏而非函数，可用于在 C 程序中添加诊断。 |

## void assert(int expression)

### 描述

C 库宏 **void assert(int expression)** 允许将诊断信息写入标准错误文件。换句话说，它可用于在 C 程序中添加诊断。

### 声明

以下是 assert() 宏的声明。

```c
void assert(int expression);
```

### 参数

- **expression** -- 可以是变量或任何 C 表达式。如果 **expression** 的计算结果为真（TRUE），assert() 不执行任何操作。如果 **expression** 的计算结果为假（FALSE），assert() 会在

## 2. `<CTYPE.H>`

### 引言

C 标准库的 **ctype.h** 头文件声明了几个用于测试和映射字符的函数。

所有函数接受 **int** 作为参数，其值必须是 EOF 或可表示为 unsigned char。

如果参数 c 满足所描述的条件，所有函数返回非零值（真），如果不满足则返回零值（假）。

### 库函数

以下是定义在头文件 ctype.h 中的函数：

| 序号 | 函数与描述 |
|---|---|
| 1 | `int isalnum(int c)`<br>此函数检查传入的字符是否为字母数字字符。 |
| 2 | `int isalpha(int c)`<br>此函数检查传入的字符是否为字母。 |
| 3 | `int iscntrl(int c)`<br>此函数检查传入的字符是否为控制字符。 |
| 4 | `int isdigit(int c)`<br>此函数检查传入的字符是否为十进制数字。 |
| 5 | `int isgraph(int c)`<br>此函数使用区域设置检查传入的字符是否具有图形表示。 |
| 6 | `int islower(int c)`<br>此函数检查传入的字符是否为小写字母。 |
| 7 | `int isprint(int c)`<br>此函数检查传入的字符是否可打印。 |
| 8 | `int ispunct(int c)`<br>此函数检查传入的字符是否为标点字符。 |
| 9 | `int isspace(int c)`<br>此函数检查传入的字符是否为空白字符。 |
| 10 | `int isupper(int c)`<br>此函数检查传入的字符是否为大写字母。 |
| 11 | `int isxdigit(int c)`<br>此函数检查传入的字符是否为十六进制数字。 |

### int isalnum(int c)

**描述**

C 库函数 **int isalnum(int c)** 检查传入的字符是否为字母数字。

**声明**

以下是 isalnum() 函数的声明。

```c
int isalnum(int c);
```

**参数**

- **c** -- 这是要检查的字符。

**返回值**

如果 c 是一个数字或字母，此函数返回非零值，否则返回 0。

**示例**

以下示例演示了 isalnum() 函数的用法。

```c
#include <stdio.h>
#include <ctype.h>

int main()
{
    int var1 = 'd';
    int var2 = '2';
    int var3 = '\t';
    int var4 = ' ';

    if( isalnum(var1) )
    {
        printf("var1 = |%c| is alphanumeric\n", var1 );
    }
    else
    {
        printf("var1 = |%c| is not alphanumeric\n", var1 );
    }
    if( isalnum(var2) )
    {
        printf("var2 = |%c| is alphanumeric\n", var2 );
    }
    else
    {
        printf("var2 = |%c| is not alphanumeric\n", var2 );
    }
    if( isalnum(var3) )
    {
        printf("var3 = |%c| is alphanumeric\n", var3 );
    }
    else
    {
        printf("var3 = |%c| is not alphanumeric\n", var3 );
    }
    if( isalnum(var4) )
    {
        printf("var4 = |%c| is alphanumeric\n", var4 );
    }
    else
    {
        printf("var4 = |%c| is not alphanumeric\n", var4 );
    }

    return(0);
}
```

让我们编译并运行上述程序，以产生以下结果：

```text
var1 = |d| is alphanumeric
var2 = |2| is alphanumeric
var3 = | | is not alphanumeric
var4 = | | is not alphanumeric
```

### int isalpha(int c)

**描述**

C 库函数 **int isalpha(int c)** 检查传入的字符是否为字母。

**声明**

以下是 isalpha() 函数的声明。

```c
int isalpha(int c);
```

**参数**

- **c** -- 这是要检查的字符。

**返回值**

如果 c 是一个字母，此函数返回非零值，否则返回 0。

**示例**

以下示例演示了 isalpha() 函数的用法。

```c
#include <stdio.h>
#include <ctype.h>

int main()
{
    int var1 = 'd';
    int var2 = '2';
    int var3 = '\t';
    int var4 = ' ';

    if( isalpha(var1) )
    {
        printf("var1 = |%c| is an alphabet\n", var1 );
    }
    else
    {
        printf("var1 = |%c| is not an alphabet\n", var1 );
    }
    if( isalpha(var2) )
    {
        printf("var2 = |%c| is an alphabet\n", var2 );
    }
    else
    {
        printf("var2 = |%c| is not an alphabet\n", var2 );
    }
    if( isalpha(var3) )
    {
        printf("var3 = |%c| is an alphabet\n", var3 );
    }
    else
    {
        printf("var3 = |%c| is not an alphabet\n", var3 );
    }
    if( isalpha(var4) )
    {
        printf("var4 = |%c| is an alphabet\n", var4 );
    }
    else
    {
        printf("var4 = |%c| is not an alphabet\n", var4 );
    }

    return(0);
}
```

让我们编译并运行上述程序，以产生以下结果：

```text
var1 = |d| is an alphabet
var2 = |2| is not an alphabet
var3 = | | is not an alphabet
var4 = | | is not an alphabet
```

### int iscntrl(int c)

**描述**

C 库函数 **int iscntrl(int c)** 检查传入的字符是否为控制字符。

根据标准 ASCII 字符集，控制字符位于 ASCII 代码 0x00（NUL）、0x1f（US）和 0x7f（DEL）之间。某些平台的特定编译器实现可能会在扩展字符集（0x7f 以上）中定义额外的控制字符。

**声明**

以下是 iscntrl() 函数的声明。

```c
int iscntrl(int c);
```

**参数**

- **c** -- 这是要检查的字符。

**返回值**

如果 c 是控制字符，此函数返回非零值，否则返回 0。

**示例**

以下示例演示了 iscntrl() 函数的用法。

```c
#include <stdio.h>
#include <ctype.h>

int main ()
{
    int i = 0, j = 0;
    char str1[] = "all \a about \t programming";
    char str2[] = "tutorials \n point";

    /* Prints string till control character \a */
    while( !iscntrl(str1[i]) )
    {
        putchar(str1[i]);
        i++;
    }

    /* Prints string till control character \n */
    while( !iscntrl(str2[j]) )
    {
        putchar(str2[j]);
        j++;
    }

    return(0);
}
```

让我们编译并运行上述程序，以产生以下结果：

```text
all tutorials
```

### int isdigit(int c)

**描述**

C 库函数 **int isdigit(int c)** 检查传入的字符是否为十进制数字字符。

十进制数字是（数字）：0 1 2 3 4 5 6 7 8 9。

**声明**

以下是 isdigit() 函数的声明。

```c
int isdigit(int c);
```

**参数**

- **c** -- 这是要检查的字符。

```text
var2 = |2| is a digit
```

### int isgraph(int c)

**描述**

C 库函数 **int isgraph(int c)** 检查字符是否具有图形表示。

具有图形表示的字符是除空白字符（如 ' '）之外的所有可打印字符，空白字符不被视为 **isgraph** 字符。

**声明**

以下是 isgraph() 函数的声明。

```c
int isgraph(int c);
```

**参数**

- **c** -- 这是要检查的字符。

**返回值**

如果 c 具有作为字符的图形表示，此函数返回非零值，否则返回 0。

**示例**

以下示例演示了 isgraph() 函数的用法。

```c
#include <stdio.h>
#include <ctype.h>

int main()
{
   int var1 = '3';
   int var2 = 'm';
   int var3 = ' ';

   if( isgraph(var1) )
   {
      printf("var1 = |%c| can be printed\n", var1 );
   }
   else
   {
```




```c
printf("var1 = |%c| can't be printed\n", var1 );
}
if( isgraph(var2) )
{
    printf("var2 = |%c| can be printed\n", var2 );
}
else
{
    printf("var2 = |%c| can't be printed\n", var2 );
}
if( isgraph(var3) )
{
    printf("var3 = |%c| can be printed\n", var3 );
}
else
{
    printf("var3 = |%c| can't be printed\n", var3 );
}

return(0);
}
```

让我们编译并运行上述程序以产生以下结果：

```
var1 = |3| can be printed
var2 = |m| can be printed
var3 = | | can't be printed
```

## int islower(int c)

### 描述

C 库函数 int islower(int c) 检查传递的字符是否为小写字母。

### 声明

以下是 islower() 函数的声明。

```c
int islower(int c);
```

### 参数

- c -- 这是要检查的字符。

### 返回值

如果 c 是小写字母，则此函数返回非零值（true），否则返回零（false）。

### 示例

以下示例展示了 islower() 函数的用法。

```c
#include <stdio.h>
#include <ctype.h>


int main()
{
    int var1 = 'Q';
    int var2 = 'q';
    int var3 = '3';

    if( islower(var1) )
    {
        printf("var1 = |%c| is lowercase character\n", var1 );
    }
    else
    {
        printf("var1 = |%c| is not lowercase character\n", var1 );
    }
    if( islower(var2) )
    {
        printf("var2 = |%c| is lowercase character\n", var2 );
    }
    else
    {
        printf("var2 = |%c| is not lowercase character\n", var2 );
    }
    if( islower(var3) )
    {
        printf("var3 = |%c| is lowercase character\n", var3 );
    }
    else
    {
        printf("var3 = |%c| is not lowercase character\n", var3 );
    }

    return(0);
}
```

让我们编译并运行上述程序以产生以下结果：

```
var1 = |Q| is not lowercase character
var2 = |q| is lowercase character
var3 = |3| is not lowercase character
```

## int isprint(int c)

### 描述

C 库函数 int isprint(int c) 检查传递的字符是否可打印。可打印字符是指不是控制字符的字符。

### 声明

以下是 isprint() 函数的声明。

```c
int isprint(int c);
```

### 参数

- c -- 这是要检查的字符。

### 返回值

如果 c 是可打印字符，则此函数返回非零值（true），否则返回零（false）。

### 示例

以下示例展示了 isprint() 函数的用法。

```c
#include <stdio.h>
#include <ctype.h>

int main()
{
    printf("var4 = |%c| can't be printed\n", var4 );
    }

    return(0);
}
```

让我们编译并运行上述程序以产生以下结果：

```
var1 = |k| can be printed
var2 = |8| can be printed
var3 = |  | can't be printed
var4 = |  | can be printed
```

## int ispunct(int c)

### 描述

C 库函数 **int ispunct(int c)** 检查传递的字符是否为标点字符。标点字符是任何图形字符（如 isgraph 中所述）且不是字母数字（如 isalnum 中所述）的字符。

### 声明

以下是 ispunct() 函数的声明。

```c
int ispunct(int c);
```

### 参数

- **c** -- 这是要检查的字符。

### 返回值

如果 c 是标点字符，则此函数返回非零值（true），否则返回零（false）。

### 示例

以下示例展示了 ispunct() 函数的用法。

```c
#include <stdio.h>
#include <ctype.h>

int main()
{
    int var1 = 't';
    int var2 = '1';
    int var3 = '/';
    int var4 = ' ';

    if( ispunct(var1) )
    {
        printf("var1 = |%c| is a punctuation character\n", var1 );
    }
    else
    {
        printf("var1 = |%c| is not a punctuation character\n", var1 );
    }
    if( ispunct(var2) )
    {
        printf("var2 = |%c| is a punctuation character\n", var2 );
    }
    else
    {
        printf("var2 = |%c| is not a punctuation character\n", var2 );
    }
    if( ispunct(var3) )
    {
        printf("var3 = |%c| is a punctuation character\n", var3 );
    }
    else
    {
        printf("var3 = |%c| is not a punctuation character\n", var3 );
    }
    if( ispunct(var4) )
    {
        printf("var4 = |%c| is a punctuation character\n", var4 );
    }
    else
    {
        printf("var4 = |%c| is not a punctuation character\n", var4 );
    }

    return(0);
}
```

让我们编译并运行上述程序，它将产生以下结果：

```
var1 = |t| is not a punctuation character
var2 = |1| is not a punctuation character
var3 = |/| is a punctuation character
var4 = | | is not a punctuation character
```

## int isspace(int c)

### 描述

C 库函数 int isspace(int c) 检查传递的字符是否为空白字符。

标准空白字符如下：

```
' '      (0x20)    space (SPC)
'\t'    (0x09)    horizontal tab (TAB)
'\n'    (0x0a)    newline (LF)
'\v'    (0x0b)    vertical tab (VT)
'\f'    (0x0c)    feed (FF)
'\r'    (0x0d)    carriage return (CR)
```

### 声明

以下是 isspace() 函数的声明。

```c
int isspace(int c);
```

### 参数

- c -- 这是要检查的字符。

### 返回值

如果 c 是空白字符，则此函数返回非零值（true），否则返回零（false）。

### 示例

以下示例展示了 isspace() 函数的用法。

```c
#include <stdio.h>
#include <ctype.h>

int main()
{
    int var1 = 't';
    int var2 = '1';
    int var3 = ' ';

    if( isspace(var1) )
    {
        printf("var1 = |%c| is a white-space character\n", var1 );
    }
    else
    {
        printf("var1 = |%c| is not a white-space character\n", var1 );
    }
    if( isspace(var2) )
    {
        printf("var2 = |%c| is a white-space character\n", var2 );
    }
    else
    {
        printf("var2 = |%c| is not a white-space character\n", var2 );
    }
    if( isspace(var3) )
    {
        printf("var3 = |%c| is a white-space character\n", var3 );
    }
    else
    {
        printf("var3 = |%c| is not a white-space character\n", var3 );
    }

    return(0);
}
```

让我们编译并运行上述程序，它将产生以下结果：

```
var1 = |t| is not a white-space character
var2 = |1| is not a white-space character
var3 = | | is a white-space character
```

## int isupper(int c)

### 描述

C 库函数 int isupper(int c) 检查传递的字符是否为大写字母。

### 声明

以下是 isupper() 函数的声明。

```c
int isupper(int c);
```

### 参数

- c -- 这是要检查的字符。

### 返回值

如果 c 是大写字母，则此函数返回非零值（true），否则返回零（false）。

### 示例

以下示例展示了 isupper() 函数的用法。

```c
#include <stdio.h>
#include <ctype.h>

int main()
{
    int var1 = 'M';
    int var2 = 'm';
    int var3 = '3';

    if( isupper(var1) )
    {
        printf("var1 = |%c| is uppercase character\n", var1 );
    }

    return(0);
}
```

让我们编译并运行上述程序以产生以下结果：

```text
var1 = |tuts| is not hexadecimal character
var2 = |0xE| is hexadecimal character
```

该库还包含两个接受并返回一个 “int” 的转换函数。

| S.N. | 函数 & 描述 |
| --- | --- |
| 1 | **int tolower(int c)**<br>此函数将大写字母转换为小写。 |
| 2 | **int toupper(int c)**<br>此函数将小写字母转换为大写。 |

## int tolower(int c)

### 描述

C 库函数 **int tolower(int c)** 将给定字母转换为小写。

### 声明

以下是 tolower() 函数的声明。

```c
int tolower(int c);
```

### 参数

- **c** -- 这是要转换为小写的字母。

### 返回值

如果存在这样的值，则此函数返回 c 的小写等价物，否则 c 保持不变。该值作为 **int** 值返回，可以隐式转换为 **char**。

### 示例

以下示例展示了 tolower() 函数的用法。

```c
#include <stdio.h>
```



以下示例展示了 toupper() 函数的用法。

```c
#include <stdio.h>
#include <ctype.h>

int main()
{
   int i = 0;
   char c;
   char str[] = "Tutorials Point";

   while(str[i])
   {
      putchar (toupper(str[i]));
      i++;
   }

   return(0);
}
```

让我们编译并运行上述程序以产生以下结果：

```text
TUTORIALS POINT
```

## 字符类

| 序号 | 字符类 & 描述 |
| --- | --- |
| 1 | **数字**<br>这是一组整数 { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 }。 |
| 2 | **十六进制数字**<br>这是集合 { 0 1 2 3 4 5 6 7 8 9 A B C D E F a b c d e f }。 |
| 3 | **小写字母**<br>这是一组小写字母 { a b c d e f g h i j k l m n o p q r s t u v w x y z }。 |

| 编号 | 标题 | 描述 |
|---|---|---|
| 4 | 大写字母 | 这是一组大写字母 {A B C D E F G H I J K L M N O P Q R S T U V W X Y Z }。 |
| 5 | 字母 | 这是一组小写字母和大写字母。 |
| 6 | 字母数字字符 | 这是一组数字、小写字母和大写字母。 |
| 7 | 标点字符 | 这是一组 ! " # $ % & ' ( ) * + , - . / : ; < = > ? @ [ \ ] ^ _ ` { | } ~ |
| 8 | 图形字符 | 这是一组字母数字字符和标点字符。 |
| 9 | 空白字符 | 这是一组制表符、换行符、垂直制表符、换页符、回车符和空格。 |
| 10 | 可打印字符 | 这是一组字母数字字符、标点字符和空白字符。 |
| 11 | 控制字符 | 在 ASCII 中，这些字符的八进制代码为 000 到 037，以及 177 (DEL)。 |
| 12 | 空白字符 | 这些是空格和制表符。 |
| 13 | 字母字符 | 这是一组小写字母和大写字母。 |

## 介绍

C 标准库的 **errno.h** 头文件定义了整数变量 **errno**，它由系统调用和某些库函数在发生错误时设置，以指示出了什么问题。此宏扩展为类型为 int 的可修改左值，因此程序既可以读取也可以修改它。

**errno** 在程序启动时被设置为零。标准 C 库的某些函数会将其值修改为非零以表示某些类型的错误。您也可以根据需要修改其值或将其重置为零。

**errno.h** 头文件还定义了一系列宏，表示不同的错误代码，这些宏将扩展为类型为 **int** 的整数常量表达式。

## 库宏

以下是 errno.h 头文件中定义的宏：

| 序号 | 宏 & 描述 |
|------|---------------------|
| 1 | **extern int errno**<br>这是在发生错误时由系统调用和某些库函数设置的宏，以指示出了什么问题。 |
| 2 | **EDOM 域错误**<br>此宏表示域错误，如果输入参数超出数学函数定义的域，则会发生此错误，并且 errno 被设置为 EDOM。 |
| 3 | **ERANGE 范围错误**<br>此宏表示范围错误，如果输入参数超出数学函数定义的范围，则会发生此错误，并且 errno 被设置为 ERANGE。 |

### extern int errno

### 描述

C 库宏 **extern int errno** 在发生错误时由系统调用和某些库函数设置，以指示是否出现问题。

### 声明

以下是 errno 宏的声明。

```c
extern int errno
```

### 参数

- 不适用

### 返回值

- 不适用

### 示例

以下示例展示了 errno 宏的用法。

```c
#include <stdio.h>
#include <errno.h>
#include <string.h>

extern int errno ;

int main ()
{
   FILE *fp;

   fp = fopen("file.txt", "r");
   if( fp == NULL )
   {
      fprintf(stderr, "Value of errno: %d\n", errno);
      fprintf(stderr, "Error opening file: %s\n", strerror(errno));
   }
   else
   {
      fclose(fp);
   }
}
```

```
{
    printf("Invalid value \n");
}
else
{
    printf("Valid value\n");
}

errno = 0;
val = sqrt(10);
if(errno == EDOM)
{
    printf("Invalid value\n");
}
else
{
    printf("Valid value\n");
}

return(0);
}
```

让我们编译并运行上述程序以产生以下结果：

```
Invalid value
Valid value
```

## ERANGE 范围错误

### 描述

如上所述，C 库宏 ERANGE 表示范围错误，如果输入参数超出数学函数定义的范围，则会发生此错误，并且 errno 被设置为 ERANGE。

### 声明

以下是 ERANGE 宏的声明。

```c
#define ERANGE some_value
```

### 参数

- 不适用

### 返回值

- 不适用

### 示例

以下示例展示了 ERANGE 宏的用法。

```c
#include <stdio.h>
#include <errno.h>
#include <math.h>

int main()
{
   double x;
   double value;

   x = 1.000000;
   value = log(x);
   if( errno == ERANGE )
   {
      printf("Log(%f) is out of range\n", x);
   }
   else
   {
      printf("Log(%f) = %f\n", x, value);
   }

   x = 0.000000;
   value = log(x);
   if( errno == ERANGE )
   {
      printf("Log(%f) is out of range\n", x);
   }
   else
   {
```

## 介绍

**float.h** 头文件包含与浮点值相关的各种平台相关常量集合。这些常量由 ANSI C 提出。它们允许创建更可移植的程序。在检查所有常量之前，了解浮点数由以下四个元素组成是有益的：

| 组件 | 组件描述 |
|---|---|
| S | 符号 ( +/- ) |
| b | 基数或指数表示的半径，二进制为 2，十进制为 10，十六进制为 16，等等... |
| e | 指数，一个介于最小 **e<sub>min</sub>** 和最大 **e<sub>max</sub>** 之间的整数。 |
| p | 精度，尾数中基数 b 的位数 |

基于上述 4 个组件，浮点数的值如下：

```
floating-point = ( S ) p x b^e

or

floating-point = (+/-) precision x base^exponent
```

## 库宏

以下值是实现特定的，并使用 `#define` 指令定义，但这些值可能不会低于此处给出的值。请注意，在所有情况下，FLT 指类型 **float**，DBL 指 **double**，LDBL 指 **long double**。

| 宏 | 描述 |
|---|---|
|  |  |
|  |  |
| FLT_ROUNDS | 定义浮点加法的舍入模式，它可以具有以下任何值：<br><br>-1 - 不可确定<br>0 - 朝向零<br>1 - 四舍五入到最近<br>2 - 朝向正无穷大<br>3 - 朝向负无穷大 |
| FLT_RADIX 2 | 这定义了指数的基数基表示。基数 2 为二进制，基数 10 为正常的十进制表示，基数 16 为十六进制。 |
| FLT_MANT_DIG<br>DBL_MANT_DIG<br>LDBL_MANT_DIG | 这些宏定义数字中数字的位数（以 FLT_RADIX 为基数）。 |
| FLT_DIG 6<br>DBL_DIG 10<br>LDBL_DIG 10 | 这些宏定义在舍入后可以不改变表示的最大十进制数字位数（基数 10）。 |
| FLT_MIN_EXP<br>DBL_MIN_EXP<br>LDBL_MIN_EXP | 这些宏定义以 FLT_RADIX 为基数的指数的最小负整数值。 |
| FLT_MIN_10_EXP -37<br>DBL_MIN_10_EXP -37<br>LDBL_MIN_10_EXP -37 | 这些宏定义以 10 为基数的指数的最小负整数值。 |
| FLT_MAX_EXP<br>DBL_MAX_EXP<br>LDBL_MAX_EXP | 这些宏定义以 FLT_RADIX 为基数的指数的最大整数值。 |
| FLT_MAX_10_EXP +37<br>DBL_MAX_10_EXP +37 | 这些宏定义以 10 为基数的指数的最大整数值。 |

| 宏 | 描述 |
|---|---|
| LDBL_MAX_10_EXP +37 |  |
| FLT_MAX 1E+37<br>DBL_MAX 1E+37<br>LDBL_MAX 1E+37 | 这些宏定义最大有限浮点值。 |
| FLT_EPSILON 1E-5<br>DBL_EPSILON 1E-9<br>LDBL_EPSILON 1E-9 | 这些宏定义可表示的最低有效数字。 |
| FLT_MIN 1E-37<br>DBL_MIN 1E-37<br>LDBL_MIN 1E-37 | 这些宏定义最小浮点值。 |

## 示例

以下示例展示了 float.h 文件中定义的某些常量的用法。

```c
#include <stdio.h>
#include <float.h>

int main()
{
    printf("The maximum value of float = %.10e\n", FLT_MAX);
    printf("The minimum value of float = %.10e\n", FLT_MIN);

    printf("The number of digits in the number = %.10e\n", FLT_MANT_DIG);
}
```

让我们编译并运行上述程序以产生以下结果：

```
The maximum value of float = 3.4028234664e+38
The minimum value of float = 1.1754943508e-38
The number of digits in the number = 7.2996655210e-312
```


## 5. <limits.h>

### 简介

limits.h 头文件确定了各种变量类型的多种属性。此头文件中定义的宏限制了 char、int 和 long 等各种变量类型的值。

这些限制规定变量不能存储超出这些限制的任何值；例如，无符号字符最大可存储到 255。

### 库宏

以下值是实现特定的，并使用 #define 指令定义，但这些值不得低于此处给出的值。

| 宏 | 值 | 描述 |
| --- | --- | --- |
| CHAR_BIT | 8 | 定义一字节中的位数。 |
| SCHAR_MIN | -128 | 定义有符号 char 的最小值。 |
| SCHAR_MAX | 127 | 定义有符号 char 的最大值。 |
| UCHAR_MAX | 255 | 定义无符号 char 的最大值。 |
| CHAR_MIN | 0 | 定义 char 类型的最小值；如果 char 表示负值，则其值等于 SCHAR_MIN，否则为零。 |
| CHAR_MAX | 127 | 定义 char 类型的值；如果 char 表示负值，则其值等于 SCHAR_MAX，否则为 UCHAR_MAX。 |
| MB_LEN_MAX | 1 | 定义多字节字符中的最大字节数。 |
| SHRT_MIN | -32768 | 定义 short int 的最小值。 |
| SHRT_MAX | +32767 | 定义 short int 的最大值。 |
| USHRT_MAX | 65535 | 定义无符号 short int 的最大值。 |
| INT_MIN | -32768 | 定义 int 的最小值。 |
| INT_MAX | +32767 | 定义 int 的最大值。 |
| UINT_MAX | 65535 | 定义无符号 int 的最大值。 |
| LONG_MIN | -2147483648 | 定义 long int 的最小值。 |
| LONG_MAX | +2147483647 | 定义 long int 的最大值。 |
| ULONG_MAX | 4294967295 | 定义无符号 long int 的最大值。 |

### 示例

以下示例展示了 limits.h 文件中定义的少数常量的用法。

```
#include <stdio.h>
#include <limits.h>

int main()
{

    printf("The number of bits in a byte %d\n", CHAR_BIT);

    printf("The minimum value of SIGNED CHAR = %d\n", SCHAR_MIN);
```

### 简介

**locale.h** 头文件定义了与位置相关的设置，例如日期格式和货币符号。你将看到若干已定义的宏，以及一个重要结构体 **struct lconv** 和下面列出的两个重要函数。

### 库宏

以下是该头文件中定义的宏，这些宏将用于下面列出的两个函数：

| 序号 | 宏与描述 |
|------|---------------------|
| 1 | **LC_ALL**<br>设置所有内容。 |
| 2 | **LC_COLLATE**<br>影响 strcoll 和 strxfrm 函数。 |
| 3 | **LC_CTYPE**<br>影响所有字符函数。 |
| 4 | **LC_MONETARY**<br>影响 localeconv 函数提供的货币信息。 |
| 5 | **LC_NUMERIC**<br>影响小数点格式以及 localeconv 函数提供的信息。 |
| 6 | **LC_TIME**<br>影响 strftime 函数。 |

### 库函数

以下是 locale.h 头文件中定义的函数：

| 序号 | 函数与描述 |
|------|------------------------|
| 1 | `char *setlocale(int category, const char *locale)`<br>设置或读取与位置相关的信息。 |
| 2 | `struct lconv *localeconv(void)`<br>设置或读取与位置相关的信息。 |

### char \*setlocale(int category, const char \*locale)

### 描述

C 库函数 **char \*setlocale(int category, const char \*locale)** 设置或读取与位置相关的信息。

### 声明

以下是 setlocale() 函数的声明。

```
char *setlocale(int category, const char *locale)
```

### 参数

- **category** -- 这是一个命名常量，指定受区域设置影响的函数类别。
  - LC_ALL 表示以下所有类别。
  - LC_COLLATE 用于字符串比较。参见 strcoll()。
  - LC_CTYPE 用于字符分类和转换。例如：strtoupper()。
  - LC_MONETARY 用于 localeconv() 的货币格式。
  - LC_NUMERIC 用于 localeconv() 的小数分隔符。
  - LC_TIME 用于通过 strftime() 进行日期和时间格式。
  - LC_MESSAGES 用于系统响应。
- **locale** -- 如果 locale 为 NULL 或空字符串 ""，则区域名称将根据与上述类别同名的环境变量的值来设置。

### 返回值

成功调用 setlocale() 会返回一个对应于所设置区域的不透明字符串。如果无法满足请求，则返回值为 NULL。

### 示例

以下示例展示了 setlocale() 函数的用法。

```
#include <locale.h>
#include <stdio.h>
#include <time.h>

int main ()
{
    time_t currtime;
    struct tm *timer;
    char buffer[80];

    time( &currtime );
    timer = localtime( &currtime );

    printf("Locale is: %s\n", setlocale(LC_ALL, "en_GB"));
    strftime(buffer,80,"%c", timer );
    printf("Date is: %s\n", buffer);

    printf("Locale is: %s\n", setlocale(LC_ALL, "de_DE"));
    strftime(buffer,80,"%c", timer );
    printf("Date is: %s\n", buffer);

    return(0);
}
```

让我们编译并运行上述程序，它将产生以下结果：

```
Locale is: en_GB

Date is: Thu 23 Aug 2012 06:39:32 MST

Locale is: de_DE

Date is: Do 23 Aug 2012 06:39:32 MST
```

### struct lconv \*localeconv(void)

### 描述

C 库函数 struct lconv \*localeconv(void) 设置或读取与位置相关的信息。这些信息以 lconv 结构体类型的对象返回。

### 声明

以下是 localeconv() 函数的声明。

```
struct lconv *localeconv(void)
```

### 参数

- 无

### 返回值

该函数返回一个指向当前区域设置的 struct lconv 的指针，其结构如下：

```
typedef struct {
char *decimal_point;
char *thousands_sep;
char *grouping;
char *int_curr_symbol;
char *currency_symbol;
char *mon_decimal_point;
char *mon_thousands_sep;
char *mon_grouping;
char *positive_sign;
char *negative_sign;
char int_frac_digits;
char frac_digits;
char p_cs_precedes;
char p_sep_by_space;
char n_cs_precedes;
char n_sep_by_space;
char p_sign_posn;
char n_sign_posn;
} lconv
```

### 示例

以下示例展示了 localeconv() 函数的用法。

```
#include <locale.h>
#include <stdio.h>

int main ()
{
    struct lconv * lc;

    setlocale(LC_MONETARY, "it_IT");
    lc = localeconv();
    printf("Local Currency Symbol: %s\n",lc->currency_symbol);
    printf("International Currency Symbol: %s\n",lc->int_curr_symbol);

    setlocale(LC_MONETARY, "en_US");
    lc = localeconv();
    printf("Local Currency Symbol: %s\n",lc->currency_symbol);
    printf("International Currency Symbol: %s\n",lc->int_curr_symbol);

    setlocale(LC_MONETARY, "en_GB");
    lc = localeconv();
    printf ("Local Currency Symbol: %s\n",lc->currency_symbol);
    printf ("International Currency Symbol: %s\n",lc->int_curr_symbol);

    printf("Decimal Point = %s\n", lc->decimal_point);

    return 0;
}
```

让我们编译并运行上述程序，它将产生以下结果：

```
Local Currency Symbol: EUR
International Currency Symbol: EUR
Local Currency Symbol: $
International Currency Symbol: USD
Local Currency Symbol: £
International Currency Symbol: GBP
Decimal Point = .
```

### 库结构

```c
typedef struct {
    char *decimal_point;
    char *thousands_sep;
    char *grouping;
    char *int_curr_symbol;
    char *currency_symbol;
    char *mon_decimal_point;
    char *mon_thousands_sep;
    char *mon_grouping;
    char *positive_sign;
    char *negative_sign;
    char int_frac_digits;
    char frac_digits;
    char p_cs_precedes;
    char p_sep_by_space;
    char n_cs_precedes;
    char n_sep_by_space;
    char p_sign_posn;
    char n_sign_posn;
} lconv
```

以下是每个字段的说明：

| 序号 | 字段与说明 |
|------|---------------------|
| 1 | **decimal_point**<br>用于非货币值的小数点字符。 |
| 2 | **thousands_sep**<br>用于非货币值的千位分隔符字符。 |
| 3 | **grouping** |




| 索引 | 详细信息 |
|---|---|
| 3 | **分组（grouping）**<br>一个字符串，表示非货币数量中每组数字的位数。每个字符表示一个整数值，指定当前组的位数。值为 0 表示其余各组沿用前一个值。 |
| 4 | **国际货币符号（int_curr_symbol）**<br>它是所使用的国际货币符号字符串。前三个字符是 ISO 4217:1987 规定的字符，第四个字符用于分隔货币符号与货币数量。 |
| 5 | **货币符号（currency_symbol）**<br>用于货币的本地符号。 |
| 6 | **货币小数点（mon_decimal_point）**<br>用于货币值的小数点字符。 |
| 7 | **货币千位分隔符（mon_thousands_sep）**<br>用于货币值的千位分组字符。 |
| 8 | **货币分组（mon_grouping）**<br>一个字符串，其元素定义货币值中数字分组的位数。每个字符表示一个整数值，指定当前组的位数。值为 0 表示其余各组沿用前一个值。 |
| 9 | **正号（positive_sign）**<br>用于正货币值的字符。 |
| 10 | **负号（negative_sign）**<br>用于负货币值的字符。 |
| 11 | **国际小数位数（int_frac_digits）**<br>国际货币值中小数点后显示的位数。 |
| 12 | **小数位数（frac_digits）**<br>货币值中小数点后显示的位数。 |
| 13 | **正数货币符号前置（p_cs_precedes）**<br>如果等于 1，则 currency_symbol 出现在正货币值之前。如果等于 0，则 currency_symbol 出现在正货币值之后。 |
| 14 | **正数符号与空格分隔（p_sep_by_space）**<br>如果等于 1，则 currency_symbol 与正货币值之间用空格分隔。如果等于 0，则 currency_symbol 与正货币值之间没有空格。 |
| 15 | **负数货币符号前置（n_cs_precedes）**<br>如果等于 1，则 currency_symbol 出现在负货币值之前。如果等于 0，则 currency_symbol 出现在负货币值之后。 |
| 16 | **负数符号与空格分隔（n_sep_by_space）**<br>如果等于 1，则 currency_symbol 与负货币值之间用空格分隔。如果等于 0，则 currency_symbol 与负货币值之间没有空格。 |
| 17 | **正号位置（p_sign_posn）**<br>表示 positive_sign 在正货币值中的位置。 |
| 18 | **负号位置（n_sign_posn）**<br>表示 negative_sign 在负货币值中的位置。 |

以下值用于 **正号位置（p_sign_posn）** 和 **负号位置（n_sign_posn）**：

| 值 | 描述 |
|---|---|
| 0 | 圆括号将值和 currency_symbol 括起来。 |
| 1 | 符号位于值和 currency_symbol 之前。 |
| 2 | 符号位于值和 currency_symbol 之后。 |
| 3 | 符号紧接在值和 currency_symbol 之前。 |
| 4 | 符号紧接在值和 currency_symbol 之后。 |

## 简介

**math.h** 头文件定义了各种数学函数和一个宏。此库中所有可用函数均接受 **double** 作为参数，并返回 **double** 作为结果。

## 库宏

此库中仅定义了一个宏：

| 序号 | 宏与描述 |
|------|---------------------|
| 1 | **HUGE_VAL**<br>当函数结果可能无法表示为浮点数时，使用此宏。如果正确结果的量级过大而无法表示，函数会将 errno 设置为 ERANGE 以指示范围错误，并返回一个特定的极大值，该值由宏 HUGE_VAL 或其负值（- HUGE_VAL）命名。<br>如果结果的量级过小，则改为返回值零。在这种情况下，errno 可能会也可能不会设置为 ERANGE。 |

## 库函数

以下是头文件 math.h 中定义的函数：

| 序号 | 函数与描述 |
|------|------------------------|
| 1 | `double acos(double x)`<br>返回 x 的反余弦值，以弧度为单位。 |
| 2 | `double asin(double x)`<br>返回 x 的反正弦值，以弧度为单位。 |
| 3 | `double atan(double x)`<br>返回 x 的反正切值，以弧度为单位。 |
| 4 | `double atan2(double y, double x)`<br>返回 y/x 的反正切值（以弧度为单位），并根据两个值的符号确定正确的象限。 |
| 5 | `double cos(double x)`<br>返回弧度角 x 的余弦值。 |
| 6 | `double cosh(double x)`<br>返回 x 的双曲余弦值。 |
| 7 | `double sin(double x)`<br>返回弧度角 x 的正弦值。 |
| 8 | `double sinh(double x)`<br>返回 x 的双曲正弦值。 |
| 9 | `double tanh(double x)`<br>返回 x 的双曲正切值。 |
| 10 | `double exp(double x)`<br>返回 **e** 的 **x** 次幂的值。 |
| 11 | `double frexp(double x, int *exponent)`<br>返回值是尾数，而 exponent 指向的整数是指数。结果值为 **x = mantissa * 2 ^ exponent**。 |
| 12 | `double ldexp(double x, int exponent)`<br>返回 **x** 乘以 2 的 exponent 次幂。 |
| 13 | `double log(double x)`<br>返回 **x** 的自然对数（以 e 为底的对数）。 |
| 14 | `double log10(double x)`<br>返回 **x** 的常用对数（以 10 为底的对数）。 |
| 15 | `double modf(double x, double *integer)`<br>返回值是小数部分（小数点后的部分），并将 integer 设置为整数部分。 |
| 16 | `double pow(double x, double y)`<br>返回 **x** 的 **y** 次幂。 |
| 17 | `double sqrt(double x)`<br>返回 **x** 的平方根。 |
| 18 | `double ceil(double x)`<br>返回大于或等于 **x** 的最小整数值。 |
| 19 | `double fabs(double x)`<br>返回 **x** 的绝对值。 |
| 20 | `double floor(double x)`<br>返回小于或等于 **x** 的最大整数值。 |
| 21 | `double fmod(double x, double y)`<br>返回 **x** 除以 **y** 的余数。 |

### double acos(double x)

**描述**

C 库函数 **double acos(double x)** 返回 **x** 的反余弦值，以弧度为单位。

**声明**

以下是 acos() 函数的声明。

```c
double acos(double x)
```

**参数**

- **x** -- 这是区间 [-1, +1] 内的浮点值。

**返回值**

此函数返回 x 的反余弦主值，区间为 [0, pi] 弧度。

**示例**

以下示例展示了 acos() 函数的用法。

```c
#include <stdio.h>
#include <math.h>

#define PI 3.14159265

int main ()
{
    double x, ret, val;

    x = 0.9;
    val = 180.0 / PI;

    ret = acos(x) * val;
    printf("The arc cosine of %lf is %lf degrees", x, ret);

    return(0);
}
```

让我们编译并运行上述程序，将产生以下结果：

```
The arc cosine of 0.900000 is 25.855040 degrees
```

### double asin(double x)

**描述**

C 库函数 **double asin(double x)** 返回 **x** 的反正弦值，以弧度为单位。

**声明**

以下是 asin() 函数的声明。

```c
double asin(double x)
```

**参数**

- **x** -- 这是区间 [-1,+1] 内的浮点值。

**返回值**

此函数返回 x 的反正弦值，区间为 [-pi/2,+pi/2] 弧度。

**示例**

以下示例展示了 asin() 函数的用法。

```c
#include <stdio.h>
#include <math.h>

#define PI 3.14159265

int main ()
{
    double x, ret, val;
    x = 0.9;
    val = 180.0 / PI;
    ret = asin(x) * val;
    printf("The arc sine of %lf is %lf degrees", x, ret);
    return(0);
}
```

让我们编译并运行上述程序，将产生以下结果：

```
The arc sine of 0.900000 is 64.190609 degrees
```

### double atan(double x)

**描述**

C 库函数 double atan(double x) 返回 x 的反正切值，以弧度为单位。

**声明**

以下是 atan() 函数的声明。

```c
double atan(double x)
```

**参数**

- **x** -- 这是浮点值。

**返回值**

此函数返回 x 的反正切主值，区间为 [-pi/2,+pi/2] 弧度。




### 示例

以下示例展示了 atan() 函数的用法。

```
#include <stdio.h>
#include <math.h>

#define PI 3.14159265

int main ()
{
    double x, ret, val;
    x = 1.0;
    val = 180.0 / PI;

    ret = atan (x) * val;
    printf("The arc tangent of %lf is %lf degrees", x, ret);

    return(0);
}
```

让我们编译并运行上述程序，将产生以下结果：

```
The arc tangent of 1.000000 is 45.000000 degrees
```

## double atan2(double y, double x)

### 描述

C 库函数 double atan2(double y, double x) 返回 y/x 的反正切值（以弧度为单位），根据两个值的符号来确定正确的象限。

### 声明

以下是 atan2() 函数的声明。

```
double atan2(double y, double x)
```

### 参数

- x -- 这是表示 x 坐标的浮点值。
- y -- 这是表示 y 坐标的浮点值。

### 返回值

此函数返回 y/x 的主反正切值，范围在 [-pi,+pi] 弧度之间。

### 示例

以下示例展示了 atan2() 函数的用法。

```
#include <stdio.h>
#include <math.h>

#define PI 3.14159265

int main ()
{
    double x, y, ret, val;

    x = -7.0;
    y = 7.0;

    val = 180.0 / PI;

    ret = atan2 (y,x) * val;
    printf("The arc tangent of x = %lf, y = %lf ", x, y);
    printf("is %lf degrees\n", ret);

    return(0);
}
```

让我们编译并运行上述程序，将产生以下结果：

```
The arc tangent of x = -7.000000, y = 7.000000 is 135.000000 degrees
```

## double cos(double x)

### 描述

C 库函数 double cos(double x) 返回弧度角 x 的余弦值。

### 声明

以下是 cos() 函数的声明。

```
double cos(double x)
```

### 参数

- **x** -- 这是以弧度表示的角度的浮点值。

### 返回值

此函数返回 x 的余弦值。

### 示例

以下示例展示了 cos() 函数的用法。

```
#include <stdio.h>
#include <math.h>

#define PI 3.14159265

int main ()
{
    double x, ret, val;

    x = 60.0;

    val = PI / 180.0;
    ret = cos( x*val );
    printf("The cosine of %lf is %lf degrees\n", x, ret);

    x = 90.0;

    val = PI / 180.0;
    ret = cos( x*val );
    printf("The cosine of %lf is %lf degrees\n", x, ret);

    return(0);
}
```

让我们编译并运行上述程序，将产生以下结果：

```
The cosine of 60.000000 is 0.500000 degrees
The cosine of 90.000000 is 0.000000 degrees
```

## double cosh(double x)

### 描述

C 库函数 **double cosh(double x)** 返回 **x** 的双曲余弦。

### 声明

以下是 cosh() 函数的声明。

```
double cosh(double x)
```

### 参数

- **x** -- 这是浮点值。

### 返回值

此函数返回 x 的双曲余弦。

### 示例

以下示例展示了 cosh() 函数的用法。

```
#include <stdio.h>
#include <math.h>

int main ()
{
    double x;

    x = 0.5;
    printf("The hyperbolic cosine of %lf is %lf\n", x, cosh(x));

    x = 1.0;
    printf("The hyperbolic cosine of %lf is %lf\n", x, cosh(x));

    x = 1.5;
    printf("The hyperbolic cosine of %lf is %lf\n", x, cosh(x));

    return(0);
}
```

让我们编译并运行上述程序以产生以下结果：

The hyperbolic cosine of 0.500000 is 1.127626
The hyperbolic cosine of 1.000000 is 1.543081
The hyperbolic cosine of 1.500000 is 2.352410

## double sin(double x)

### 描述

C 库函数 **double sin(double x)** 返回弧度角 **x** 的正弦值。

### 声明

以下是 sin() 函数的声明。

```c
double sin(double x)
```

### 参数

- **x** -- 这是以弧度表示的角度的浮点值。

### 返回值

此函数返回 x 的正弦值。

### 示例

以下示例展示了 sin() 函数的用法。

```c
#include <stdio.h>
#include <math.h>

#define PI 3.14159265

int main ()
{
  double x, ret, val;

  x = 45.0;
  val = PI / 180;
  ret = sin(x*val);
  printf("The sine of %lf is %lf degrees", x, ret);

  return(0);
}
```

让我们编译并运行上述程序以产生以下结果：

```
The sine of 45.000000 is 0.707107 degrees
```

## double sinh(double x)

### 描述

C 库函数 **double sinh(double x)** 返回 **x** 的双曲正弦。

### 声明

以下是 sinh() 函数的声明。

```c
double sinh(double x)
```

### 参数

- **x** -- 这是浮点值。

### 返回值

此函数返回 x 的双曲正弦。

### 示例

以下示例展示了 sinh() 函数的用法。

```c
#include <stdio.h>
#include <math.h>

int main ()
{
    double x, ret;
    x = 0.5;

    ret = sinh(x);
    printf("The hyperbolic sine of %lf is %lf degrees", x, ret);

    return(0);
}
```

让我们编译并运行上述程序，这将产生以下结果：

```
The hyperbolic sine of 0.500000 is 0.521095 degrees
```

## double tanh(double x)

### 描述

C 库函数 double tanh(double x) 返回 x 的双曲正切。

### 声明

以下是 tanh() 函数的声明。

```
double tanh(double x)
```

### 参数

- x -- 这是浮点值。

### 返回值

此函数返回 x 的双曲正切。

### 示例

以下示例展示了 tanh() 函数的用法。

```
#include <stdio.h>
#include <math.h>

int main ()
{
    double x, ret;
    x = 0.5;

    ret = tanh(x);
    printf("The hyperbolic tangent of %lf is %lf degrees", x, ret);

    return(0);
}
```

让我们编译并运行上述程序，将产生以下结果：

```
The hyperbolic tangent of 0.500000 is 0.462117 degrees
```

## double exp(double x)

### 描述

C 库函数 **double exp(double x)** 返回 **e** 的 **xth** 次幂的值。

### 声明

以下是 exp() 函数的声明。

```c
double exp(double x)
```

### 参数

- **x** -- 这是浮点值。

### 返回值

此函数返回 x 的指数值。

### 示例

以下示例展示了 exp() 函数的用法。

```c
#include <stdio.h>
#include <math.h>

int main ()
{
    double x = 0;

    printf("The exponential value of %lf is %lf\n", x, exp(x));
    printf("The exponential value of %lf is %lf\n", x+1, exp(x+1));
    printf("The exponential value of %lf is %lf\n", x+2, exp(x+2));

    return(0);
}
```

让我们编译并运行上述程序，将产生以下结果：

```
The exponential value of 0.000000 is 1.000000
The exponential value of 1.000000 is 2.718282
The exponential value of 2.000000 is 7.389056
```

## double frexp(double x, int *exponent)

### 描述

C 库函数 **double frexp(double x, int *exponent)** 的返回值是尾数，而 **exponent** 指向的整数是指数。结果值为 **x = mantissa * 2 ^ exponent**。

### 声明

以下是 frexp() 函数的声明。

```
double frexp(double x, int *exponent)
```

### 参数

- **x** -- 这是要计算的浮点值。
- **exponent** -- 这是指向 int 对象的指针，用于存储指数值。

### 返回值

此函数返回规范化分数。如果参数 x 不为零，则规范化分数是 x 的 2 的幂次倍，其绝对值始终在 1/2（包含）到 1（不包含）之间。如果 x 为零，则规范化分数为零，且 exp 中存储零。

### 示例

以下示例展示了 frexp() 函数的用法。

```
#include <stdio.h>
#include <math.h>

int main ()
{
    double x = 1024, fraction;
    int e;

    fraction = frexp(x, &e);
    printf("x = %.2f = %.2f * 2^%d\n", x, fraction, e);

    return(0);
}
```

让我们编译并运行上述程序以产生以下结果：

```
x = 1024.00 = 0.50 * 2^11
```



## double ldexp(double x, int exponent)

### 描述

C 库函数 **double ldexp(double x, int exponent)** 返回 **x** 乘以 2 的 **exponent** 次方。

### 声明

以下是 ldexp() 函数的声明。

```c
double ldexp(double x, int exponent)
```

### 参数

- **x** -- 这是表示尾数的浮点值。
- **exponent** -- 这是指数的数值。

### 返回值

此函数返回 x * 2<sup>exp</sup>

### 示例

以下示例展示了 ldexp() 函数的用法。

```c
#include <stdio.h>
#include <math.h>

int main ()
{
   double x, ret;
   int n;

   x = 0.65;
   n = 3;
   ret = ldexp(x ,n);
   printf("%f * 2^%d = %f\n", x, n, ret);

   return(0);
}
```

让我们编译并运行上面的程序，将会产生以下结果：

```text
0.650000 * 2^3 = 5.200000
```

## double log(double x)

### 描述

C 库函数 double log(double x) 返回 x 的自然对数（以 e 为底的对数）。

### 声明

以下是 log() 函数的声明。

```c
double log(double x)
```

### 参数

- x -- 这是浮点值。

### 返回值

此函数返回 x 的自然对数。

### 示例

以下示例展示了 log() 函数的用法。

```c
#include <stdio.h>
#include <math.h>

int main ()
{
    double x, ret;
    x = 2.7;

    /* finding log(2.7) */
    ret = log(x);
    printf("log(%lf) = %lf", x, ret);

    return(0);
}
```

让我们编译并运行上面的程序，将会产生以下结果：

```text
log(2.700000) = 0.993252
```

## double log10(double x)

### 描述

C 库函数 double log10(double x) 返回 x 的常用对数（以 10 为底的对数）。

### 声明

以下是 log10() 函数的声明。

```c
double log10(double x)
```

### 参数

- x -- 这是浮点值。

### 返回值

此函数返回 x 的常用对数，x 的值大于零时。

### 示例

以下示例展示了 log10() 函数的用法。

```c
#include <stdio.h>
#include <math.h>

int main ()
{
    double x, ret;
    x = 10000;

    /* finding value of log10(10000) */
    ret = log10(x);
    printf("log10(%lf) = %lf\n", x, ret);

    return(0);
}
```

让我们编译并运行上面的程序，将会产生以下结果：

```text
log10(10000.000000) = 4.000000
```

## double modf(double x, double *integer)

### 描述

C 库函数 **double modf(double x, double *integer)** 返回小数部分（小数点后的部分），并将 integer 设置为整数部分。

### 声明

以下是 modf() 函数的声明。

```c
double modf(double x, double *integer)
```

### 参数

- **x** -- 这是浮点值。
- **integer** -- 这是指向存储整数部分的对象的指针。

### 返回值

此函数返回 x 的小数部分，保持相同的符号。

### 示例

以下示例展示了 modf() 函数的用法。

```c
#include<stdio.h>
#include<math.h>

int main ()
{
    double x, fractpart, intpart;

    x = 8.123456;
    fractpart = modf(x, &intpart);

    printf("Integral part = %lf\n", intpart);
    printf("Fraction Part = %lf \n", fractpart);

    return(0);
}
```

让我们编译并运行上面的程序，将会产生以下结果：

```text
Integral part = 8.000000
Fraction Part = 0.123456
```

## double pow(double x, double y)

### 描述

C 库函数 double pow(double x, double y) 返回 x 的 y 次幂，即 x^y。

### 声明

以下是 pow() 函数的声明。

```c
double pow(double x, double y)
```

### 参数

- x -- 这是浮点底数。
- y -- 这是指数浮点值。

### 返回值

此函数返回 x 的 y 次幂的结果。

### 示例

以下示例展示了 pow() 函数的用法。

```c
#include <stdio.h>
#include <math.h>

int main ()
{
    printf("Value 8.0 ^ 3 = %lf\n", pow(8.0, 3));
    printf("Value 3.05 ^ 1.98 = %lf", pow(3.05, 1.98));
    return(0);
}
```

让我们编译并运行上面的程序，将会产生以下结果：

```text
Value 8.0 ^ 3 = 512.000000
Value 3.05 ^ 1.98 = 9.097324
```

## double sqrt(double x)

### 描述

C 库函数 double sqrt(double x) 返回 x 的平方根。

### 声明

以下是 sqrt() 函数的声明。

```c
double sqrt(double x)
```

### 参数

- **x** -- 这是浮点值。

### 返回值

此函数返回 x 的平方根。

### 示例

以下示例展示了 sqrt() 函数的用法。

```c
#include <stdio.h>
#include <math.h>

int main ()
{

    printf("Square root of %lf is %lf\n", 4.0, sqrt(4.0) );
    printf("Square root of %lf is %lf\n", 5.0, sqrt(5.0) );

    return(0);
}
```

让我们编译并运行上面的程序，将会产生以下结果：

```text
Square root of 4.000000 is 2.000000
Square root of 5.000000 is 2.236068
```

## double ceil(double x)

### 描述

C 库函数 **double ceil(double x)** 返回大于或等于 **x** 的最小整数值。

### 声明

以下是 ceil() 函数的声明。

```c
double ceil(double x)
```

### 参数

- **x** -- 这是浮点值。

### 返回值

此函数返回不小于 **x** 的最小整数值。

### 示例

以下示例展示了 ceil() 函数的用法。

```c
#include <stdio.h>
#include <math.h>

int main ()
{
   float val1, val2, val3, val4;

   val1 = 1.6;
   val2 = 1.2;
   val3 = 2.8;
   val4 = 2.3;

   printf ("value1 = %.1lf\n", ceil(val1));
   printf ("value2 = %.1lf\n", ceil(val2));
   printf ("value3 = %.1lf\n", ceil(val3));
   printf ("value4 = %.1lf\n", ceil(val4));

   return(0);
}
```

让我们编译并运行上面的程序，将会产生以下结果：

```text
value1 = 2.0
value2 = 2.0
value3 = 3.0
value4 = 3.0
```

## double fabs(double x)

### 描述

C 库函数 double fabs(double x) 返回 x 的绝对值。

### 声明

以下是 fabs() 函数的声明。

```c
double fabs(double x)
```

### 参数

- x -- 这是浮点值。

### 返回值

此函数返回 x 的绝对值。

### 示例

以下示例展示了 fabs() 函数的用法。

```c
#include <stdio.h>
#include <math.h>

int main ()
{
    int a, b;
    a = 1234;
    b = -344;

    printf("The absolute value of %d is %lf\n", a, fabs(a));
    printf("The absolute value of %d is %lf\n", b, fabs(b));

    return(0);
}
```

让我们编译并运行上面的程序，将会产生以下结果：

```text
The absolute value of 1234 is 1234.000000
The absolute value of -344 is 344.000000
```

## double floor(double x)

### 描述

C 库函数 double floor(double x) 返回小于或等于 x 的最大整数值。

### 声明

以下是 floor() 函数的声明。

```c
double floor(double x)
```

### 参数

- x -- 这是浮点值。

### 返回值

此函数返回不大于 x 的最大整数值。

### 示例

以下示例展示了 floor() 函数的用法。

```c
#include <stdio.h>
#include <math.h>

int main ()
{
    float val1, val2, val3, val4;

    val1 = 1.6;
    val2 = 1.2;
    val3 = 2.8;
    val4 = 2.3;

    printf("Value1 = %.1f\n", floor(val1));
    printf("Value2 = %.1f\n", floor(val2));
    printf("Value3 = %.1f\n", floor(val3));
    printf("Value4 = %.1f\n", floor(val4));

    return(0);
}
```

让我们编译并运行上面的程序，将会产生以下结果：

```text
Value1 = 1.0
Value2 = 1.0
Value3 = 2.0
```




Value4 = 2.0

## double fmod(double x, double y)

### 描述

C 库函数 **double fmod(double x, double y)** 返回 **x** 除以 **y** 的余数。

### 声明

以下是 fmod() 函数的声明。

```
double fmod(double x, double y)
```

### 参数

- **x** -- 这是除法分子的浮点值，即 x。
- **y** -- 这是除法分母的浮点值，即 y。

### 返回值

该函数返回 x/y 的余数。

### 示例

以下示例展示了 fmod() 函数的用法。

```
#include <stdio.h>
#include <math.h>

int main ()
{
    float a, b;
    int c;
    a = 9.2;
    b = 3.7;
    c = 2;
    printf("Remainder of %f / %d is %lf\n", a, c, fmod(a,c));
    printf("Remainder of %f / %f is %lf\n", a, b, fmod(a,b));
    return(0);
}
```

让我们编译并运行上述程序，这将产生以下结果：

```
Remainder of 9.200000 / 2 is 1.200000
Remainder of 9.200000 / 3.700000 is 1.800000
```

## 简介

setjmp.h 头文件定义了宏 **setjmp()**、一个函数 **longjmp()** 以及一种变量类型 **jmp_buf**，用于绕过正常的函数调用和返回规则。

### 库变量

以下是 setjmp.h 头文件中定义的变量类型：

| 序号 | 变量与描述 |
|------|------------------------|
| 1    | **jmp_buf**<br>这是一种数组类型，用于保存宏 **setjmp()** 和函数 **longjmp()** 所需的信息。 |

### 库宏

该库中仅定义了一个宏：

| 序号 | 宏与描述 |
|------|---------------------|
| 1    | **int setjmp(jmp_buf environment)**<br>该宏将当前 *环境* 保存到变量 **environment** 中，供函数 **longjmp()** 后续使用。如果该宏直接从宏调用返回，则返回零；但如果它从 **longjmp()** 函数调用返回，则返回非零值。 |

## int setjmp(jmp_buf environment)

### 描述

C 库宏 **int setjmp(jmp_buf environment)** 将当前 **environment** 保存到变量 environment 中，供函数 **longjmp()** 后续使用。如果该宏直接从宏调用返回，则它

```
}

void jmpfunction(jmp_buf env_buf)
{
    longjmp(env_buf, "tutorialspoint.com");
}
```

让我们编译并运行上述程序，这将产生以下结果：

```
Jump function call
Returned from a longjmp() with value = tutorialspoint.com
```

### 库函数

以下是 setjmp.h 头文件中定义的唯一一个函数：

| 序号 | 函数与描述 |
|------|------------------------|
| 1 | **void longjmp(jmp_buf environment, int value)**<br>该函数使用相应的 **jmp_buf** 参数，恢复程序中同一调用内最近一次调用 **setjmp()** 宏所保存的环境。 |

## void longjmp(jmp_buf environment, int value)

### 描述

C 库函数 **void longjmp(jmp_buf environment, int value)** 使用相应的 **jmp_buf** 参数，恢复程序中同一调用内最近一次调用 **setjmp()** 宏所保存的环境。

### 声明

以下是 longjmp() 函数的声明。

```
void longjmp(jmp_buf environment, int value)
```

### 参数

- **environment** -- 这是 **jmp_buf** 类型的对象，包含用于在 setjmp 调用点恢复环境的信息。
- **value** -- 这是 **setjmp** 表达式求值得到的值。

### 返回值

该函数不返回任何值。

### 示例

以下示例展示了 longjmp() 函数的用法。

```
#include <stdio.h>
#include <stdlib.h>
#include <setjmp.h>

int main()
{
    int val;
    jmp_buf env_buffer;

    /* save calling environment for longjmp */
    val = setjmp( env_buffer );
    if( val != 0 )
    {
        printf("Returned from a longjmp() with value = %s\n", val);
        exit(0);
    }

    printf("Jump function call\n");
    jmpfunction( env_buffer );

    return(0);
}

void jmpfunction(jmp_buf env_buf)
{
    longjmp(env_buf, "tutorialspoint.com");
}
```

让我们编译并运行上述程序，这将产生以下结果：

```
Jump function call
Returned from a longjmp() with value = tutorialspoint.com
```

## 简介

**signal.h** 头文件定义了变量类型 **sig_atomic_t**、两个函数调用以及若干宏，用于处理程序执行期间报告的不同信号。

### 库变量

以下是 signal.h 头文件中定义的变量类型：

| 序号 | 变量与描述 |
|------|------------------------|
| 1 | **sig_atomic_t**<br>这是 **int** 类型，用作信号处理程序中的变量。这是一种对象的整数类型，即使存在异步信号，也可以作为原子实体访问。 |

### 库宏

以下是 signal.h 头文件中定义的宏，这些宏将用于下面列出的两个函数中。**SIG_** 宏与 signal 函数一起使用，以定义信号函数。

| 序号 | 宏与描述 |
|------|---------------------|
| 1 | **SIG_DFL**<br>默认信号处理程序。 |
| 2 | **SIG_ERR**<br>表示信号错误。 |
| 3 | **SIG_IGN**<br>忽略信号。 |

**SIG** 宏用于在以下情况下表示信号编号：

| 序号 | 宏与描述 |
|------|---------------------|
| 1 | **SIGABRT**<br>程序异常终止。 |
| 2 | **SIGFPE**<br>浮点错误，如除以零。 |
| 3 | **SIGILL**<br>非法操作。 |
| 4 | **SIGINT**<br>中断信号，如 Ctrl-C。 |
| 5 | **SIGSEGV**<br>无效的存储访问，如段违规。 |
| 6 | **SIGTERM**<br>终止请求。 |

### 库函数

以下是 signal.h 头文件中定义的函数：

| 序号 | 函数与描述 |
|------|------------------------|
| 1 | `void (*signal(int sig, void (*func)(int)))(int)`<br>该函数设置一个函数来处理信号，即信号处理程序。 |
| 2 | `int raise(int sig)`<br>该函数导致生成信号 sig。sig 参数与 SIG 宏兼容。 |

## void (*signal(int sig, void (*func)(int)))(int)

### 描述

C 库函数 void (*signal(int sig, void (*func)(int)))(int) 设置一个函数来处理信号，即具有信号编号 sig 的信号处理程序。

### 声明

以下是 signal() 函数的声明。

```
void (*signal(int sig, void (*func)(int)))(int)
```

### 参数

- sig -- 这是要设置处理函数的信号编号。以下是一些重要的标准信号编号：

| 宏 | 信号 |
|---|---|
| SIGABRT | （信号中止）异常终止，例如由函数引发。 |
| SIGFPE | （信号浮点异常）错误的算术操作，例如除以零或导致溢出的操作（不一定是浮点操作）。 |
| SIGILL | （信号非法指令）无效的函数映像，例如非法指令。这通常是由于代码损坏或试图执行数据造成的。 |
| SIGINT | （信号中断）交互式注意信号。通常由应用程序用户生成。 |
| SIGSEGV | （信号段违规）无效的存储访问：当程序试图读取或写入其分配的内存之外时。 |
| SIGTERM | （信号终止）发送给程序的终止请求。 |

- func -- 这是一个指向函数的指针。它可以是由程序员定义的函数，也可以是以下预定义函数之一：

|  |  |
|---|---|
| SIG_DFL | 默认处理：信号由该特定信号的默认操作处理。 |
| SIG_IGN | 忽略信号：信号被忽略。 |

### 返回值

该函数返回信号处理程序的前一个值，出错时返回 SIG_ERR。

### 示例

以下示例展示了 signal() 函数的用法。

```
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <signal.h>

void sighandler(int);

int main()
{
    signal(SIGINT, sighandler);

    while(1)
    {
        printf("Going to sleep for a second...\n");
        sleep(1);
    }

    return(0);
}

void sighandler(int signum)
{
    printf("Caught signal %d, coming out...\n", signum);
    exit(1);
}
```

让我们编译并运行上述程序，这将产生以下结果，并且程序将进入无限循环。要退出程序，我们使用了 CTRL + C 键。

```
Going to sleep for a second...
Going to sleep for a second...
```





```
Going to sleep for a second...
Going to sleep for a second...
Going to sleep for a second...
Caught signal 2, coming out...
```

## int raise(int sig)

### 描述
C 库函数 int raise(int sig) 会生成信号 sig。sig 参数与 SIG 宏兼容。

### 声明
以下是 raise() 函数的声明。

```c
int raise(int sig)
```

### 参数
- sig -- 这是要发送的信号编号。以下是一些重要的标准信号常量：

| 宏 | 信号 |
|---|---|
| SIGABRT | （信号中止）异常终止，例如由 abort 函数发起的终止。 |
| SIGFPE | （信号浮点异常）错误的算术运算，例如除零或导致溢出的运算（不一定是浮点运算）。 |
| SIGILL | （信号非法指令）无效的函数映像，例如非法指令。这通常是由于代码损坏或试图执行数据所致。 |
| SIGINT | （信号中断）交互式注意信号。通常由应用程序用户生成。 |
| SIGSEGV | （信号段违规）对存储器的无效访问：当程序试图读取或写入为其分配的内存之外时。 |
| SIGTERM | （信号终止）发送给程序的终止请求。 |

### 示例
```c
    printf("!! signal caught !!\n");
}
```

让我们编译并运行上面的程序，以产生以下结果：

```
Going to raise a signal
!! signal caught !!
Exiting...
```

## 简介
stdarg.h 头文件定义了一种变量类型 **va_list** 以及三个宏，当参数数量未知（即参数数量可变）时，可使用这些宏获取函数中的参数。

可变参数函数通过在参数列表末尾使用省略号（...）来定义。

## 库变量
以下是 stdarg.h 头文件中定义的变量类型：

| 序号 | 变量与描述 |
|------|------------------------|
| 1 | **va_list**<br>这是一种适合保存三个宏 **va_start()**、**va_arg()** 和 **va_end()** 所需信息的类型。 |

## 库宏
以下是 stdarg.h 头文件中定义的宏：

| 序号 | 宏与描述 |
|------|---------------------|
| 1 | `void va_start(va_list ap, last_arg)`<br>该宏初始化 **ap** 变量，以便与 **va_arg** 和 **va_end** 宏一起使用。**last_arg** 是传递给函数的最后一个已知固定参数，即省略号之前的参数。 |
| 2 | `type va_arg(va_list ap, type)`<br>该宏获取函数参数列表中类型为 **type** 的下一个参数。 |
| 3 | `void va_end(va_list ap)`<br>该宏允许使用 va_start 宏的可变参数函数返回。如果在从函数返回之前未调用 va_end，则结果未定义。 |

## void va_start(va_list ap, last_arg)

### 描述
C 库宏 **void va_start(va_list ap, last_arg)** 初始化 **ap** 变量，以便与 **va_arg** 和 **va_end** 宏一起使用。**last_arg** 是传递给函数的最后一个已知固定参数，即省略号之前的参数。

在使用 **va_arg** 和 **va_end** 之前必须先调用此宏。

### 声明
以下是 va_start() 宏的声明。

```c
    void va_start(va_list ap, last_arg);
```

### 参数
- **ap** -- 这是 **va_list** 的对象，它将保存使用 **va_arg** 获取额外参数所需的信息。
- **last_arg** -- 这是传递给函数的最后一个已知固定参数。

### 返回值
无

### 示例
以下示例展示了 va_start() 宏的用法。

```c
    #include<stdarg.h>
    #include<stdio.h>

    int sum(int, ...);

    int main(void)
    {
        printf("Sum of 10, 20 and 30 = %d\n", sum(3, 10, 20, 30) );
        printf("Sum of 4, 20, 25 and 30 = %d\n", sum(4, 4, 20, 25, 30) );

        return 0;
    }
```

## type va_arg(va_list ap, type)

### 参数
- **type** -- 这是一个类型名称。此类型名称用作该宏展开后表达式的类型。

### 返回值
该宏返回下一个额外参数，作为类型为 **type** 的表达式。

### 示例
以下示例展示了 va_arg() 宏的用法。

```c
#include <stdarg.h>
#include <stdio.h>

int sum(int, ...);

int main()
{
    printf("Sum of 15 and 56 = %d\n",  sum(2, 15, 56) );
    return 0;
}

int sum(int num_args, ...)
{
    int val = 0;
    va_list ap;
    int i;

    va_start(ap, num_args);
    for(i = 0; i < num_args; i++)
    {
        val += va_arg(ap, int);
    }
    va_end(ap);

    return val;
}
```

让我们编译并运行上面的程序，以产生以下结果：

```
Sum of 15 and 56 = 71
```

## void va_end(va_list ap)

### 描述
C 库宏 void va_end(va_list ap) 允许使用了 va_start 宏的可变参数函数返回。如果在从函数返回之前未调用 va_end，则结果未定义。

### 声明
以下是 va_end() 宏的声明。

```c
void va_end(va_list ap)
```

### 参数
- ap -- 这是之前由同一函数中的 va_start 初始化的 va_list 对象。

### 返回值
该宏不返回任何值。

### 示例
以下示例展示了 va_end() 宏的用法。

```c
#include <stdarg.h>
#include <stdio.h>

int mul(int, ...);

int main()
{
    printf("15 * 12 = %d\n",  mul(2, 15, 12) );

    return 0;
}

int mul(int num_args, ...)
{
    int val = 1;
    va_list ap;
    int i;

    va_start(ap, num_args);
    for(i = 0; i < num_args; i++)
    {
        val *= va_arg(ap, int);
    }
    va_end(ap);

    return val;
}
```

让我们编译并运行上面的程序，以产生以下结果：

```
15 * 12 =  180
```

## 简介
stddef.h 头文件定义了各种变量类型和宏。其中许多定义也出现在其他头文件中。

## 库变量
以下是 stddef.h 头文件中定义的变量类型：

| 序号 | 变量与描述 |
|------|------------------------|
| 1 | ptrdiff_t<br>这是一种有符号整型，是两个指针相减的结果。 |
| 2 | size_t<br>这是一种无符号整型，是 sizeof 关键字的结果。 |
| 3 | wchar_t<br>这是一种大小与宽字符常量相同的整型。 |

## 库宏
以下是 stddef.h 头文件中定义的宏：

| 序号 | 宏与描述 |
|------|---------------------|
| 1 | NULL<br>该宏是空指针常量的值。 |
| 2 | offsetof(type, member-designator)<br>这会生成一个类型为 size_t 的常量整数，它是结构体成员距结构体起始位置的字节偏移量。该成员由 member-designator 给出，结构体名称由 *type* 给出。 |

## NULL

### 描述
C 库宏 **NULL** 是空指针常量的值。根据编译器供应商的不同，它可能定义为 **((void*)0)**、**0** 或 **0L**。

### 声明
根据编译器的不同，NULL 宏的声明可能如下。

```c
#define NULL ((char *)0)

or

#define NULL 0L

or

#define NULL 0
```

### 参数
- 无

### 返回值
- 无

### 示例
以下示例展示了 NULL 宏的用法。

```c
#include <stddef.h>
#include <stdio.h>

int main ()
{
    FILE *fp;

    fp = fopen("file.txt", "r");
    if( fp != NULL )
    {
        printf("Opened file file.txt successfully\n");
        fclose(fp);
    }

    fp = fopen("nofile.txt", "r");
    if( fp == NULL )
    {
        printf("Could not open file nofile.txt\n");
    }

    return(0);
}
```

假设我们有一个已存在的文件 **file.txt**，但 **nofile.txt** 不存在。让我们编译并运行上面的程序，它将产生以下结果：

```
Opened file file.txt successfully
Could not open file nofile.txt
```

## offsetof(type, member-designator)

### 描述
C 库宏 **offsetof(type, member-designator)** 会生成一个类型为 **size_t** 的常量整数，它是结构体成员距结构体起始位置的字节偏移量。该成员由 member-designator 给出，结构体名称由 type 给出。

### 声明
以下是 offsetof() 宏的声明。

```c
offsetof(type, member-designator)
```

### 参数
- **type** -- 这是类类型，其中 member-designator 是有效的成员指示符。
- **member-designator** -- 这是类类型的成员指示符。

### 返回值
该宏返回类型为 **size_t** 的值，即成员在 type 中的偏移值。




## 示例

以下示例展示了 offsetof() 宏的使用。

```
#include <stddef.h>
#include <stdio.h>

struct address {
    char name[50];
    char street[50];
    int phone;
};

int main()
{
    printf("name offset = %d byte in address structure.\n", offsetof(struct address, name));

    printf("street offset = %d byte in address structure.\n", offsetof(struct address, street));

    printf("phone offset = %d byte in address structure.\n", offsetof(struct address, phone));

    return(0);
}
```

让我们编译并运行上述程序，这将产生以下结果：

```
name offset = 0 byte in address structure.
street offset = 50 byte in address structure.
phone offset = 100 byte in address structure.
```

## 介绍

**stdio.h** 头文件定义了三种变量类型、多个宏以及用于执行输入和输出的各种函数。

## 库变量

以下是 stdio.h 头文件中定义的变量类型：

| 序号 | 变量与描述 |
|------|------------------------|
| 1 | **size_t**<br>这是一种无符号整数类型，是 **sizeof** 关键字的结果。 |
| 2 | **FILE**<br>这是一种适合存储文件流信息的对象类型。 |
| 3 | **fpos_t**<br>这是一种适合存储文件中任意位置的对象类型。 |

## 库宏

以下是 stdio.h 头文件中定义的宏：

| 序号 | 宏与描述 |
|------|---------------------|
| 1 | **NULL**<br>该宏是空指针常量的值。 |
| 2 | **_IOFBF, _IOLBF and _IONBF**<br>这些宏展开为具有不同值的整数常量表达式，适用于作为 **setvbuf** 函数的第三个参数。 |
| 3 | **BUFSIZ**<br><br>该宏是一个整数，表示 **setbuf** 函数使用的缓冲区的大小。 |
| 4 | **EOF**<br><br>该宏是一个负整数，表示已到达文件末尾。 |
| 5 | **FOPEN_MAX**<br><br>该宏是一个整数，表示系统保证可以同时打开的最大文件数。 |
| 6 | **FILENAME_MAX**<br><br>该宏是一个整数，表示适合容纳最长可能文件名的 char 数组的最长长度。如果实现不设限制，则该值应为推荐的最大值。 |
| 7 | **L_tmpnam**<br><br>该宏是一个整数，表示适合容纳由 **tmpnam** 函数创建的最长可能临时文件名的 char 数组的最长长度。 |
| 8 | **SEEK_CUR, SEEK_END, and SEEK_SET**<br><br>这些宏在 **fseek** 函数中使用，用于定位文件中的不同位置。 |
| 9 | **TMP_MAX**<br><br>该宏是函数 **tmpnam** 可以生成的唯一文件名的最大数量。 |
| 10 | **stderr, stdin, and stdout**<br><br>这些宏是指向 FILE 类型的指针，对应标准错误、标准输入和标准输出流。 |

## 库函数

以下是 stdio.h 头文件中定义的函数：

为更好地理解并使用 **Try it**（在线编译器）选项，请遵循相同的函数顺序，因为在第一个函数中创建的文件将在后续函数中使用。

| 序号 | 函数与描述 |
| --- | --- |
| 1 | int fclose(FILE *stream)<br>关闭流。所有缓冲区都被刷新。 |
| 2 | void clearerr(FILE *stream)<br>清除给定流的末尾文件和错误指示符。 |
| 3 | int feof(FILE *stream)<br>测试给定流的末尾文件指示符。 |
| 4 | int ferror(FILE *stream)<br>测试给定流的错误指示符。 |
| 5 | int fflush(FILE *stream)<br>刷新流的输出缓冲区。 |
| 6 | int fgetpos(FILE *stream, fpos_t *pos)<br>获取流的当前文件位置并将其写入 pos。 |
| 7 | FILE *fopen(const char *filename, const char *mode)<br>使用给定模式打开 filename 指向的文件名。 |
| 8 | size_t fread(void *ptr, size_t size, size_t nmemb, FILE *stream)<br>从给定流读取数据到 ptr 指向的数组中。 |
| 9 | FILE *freopen(const char *filename, const char *mode, FILE *stream)<br>将新文件名与给定的打开流关联，同时关闭流中的旧文件。 |
| 10 | int fseek(FILE *stream, long int offset, int whence)<br>将流的文件位置设置为给定偏移量。参数 offset 表示从给定的 whence 位置开始查找的字节数。 |
| 11 | `int fsetpos(FILE *stream, const fpos_t *pos)`<br>设置给定流的文件位置到给定位置。参数 pos 是由函数 fgetpos 给出的位置。 |
| 12 | `long int ftell(FILE *stream)`<br>返回给定流的当前文件位置。 |
| 13 | `size_t fwrite(const void *ptr, size_t size, size_t nmemb, FILE *stream)`<br>将 ptr 指向的数组中的数据写入给定流。 |
| 14 | `int remove(const char *filename)`<br>删除给定文件名，使其不再可访问。 |
| 15 | `int rename(const char *old_filename, const char *new_filename)`<br>使 old_filename 引用的文件名更改为 new_filename。 |
| 16 | `void rewind(FILE *stream)`<br>将文件位置设置为给定流的文件开头。 |
| 17 | `void setbuf(FILE *stream, char *buffer)`<br>定义流应如何缓冲。 |
| 18 | `int setvbuf(FILE *stream, char *buffer, int mode, size_t size)`<br>另一个定义流应如何缓冲的函数。 |
| 19 | `FILE *tmpfile(void)`<br>在二进制更新模式 (wb+) 中创建临时文件。 |
| 20 | `char *tmpnam(char *str)`<br>生成并返回一个有效且不存在的临时文件名。 |
| 21 | `int fprintf(FILE *stream, const char *format, ...)` |  |

| # | 函数 | 描述 |
|---|----------|-------------|
| 32 | int fputc(int char, FILE *stream) | 写入由参数 char 指定的字符（无符号字符）到指定流并推进流的位置指示器。 |
| 33 | int fputs(const char *str, FILE *stream) | 将字符串写入指定流，直到但不包括空字符。 |
| 34 | int getc(FILE *stream) | 从指定流获取下一个字符（无符号字符）并推进流的位置指示器。 |
| 35 | int getchar(void) | 从 stdin 获取一个字符（无符号字符）。 |
| 36 | char *gets(char *str) | 从 stdin 读取一行并将其存储到 str 指向的字符串中。它在读取到换行符或到达文件末尾时停止，以先发生的为准。 |
| 37 | int putc(int char, FILE *stream) | 写入由参数 char 指定的字符（无符号字符）到指定流并推进流的位置指示器。 |
| 38 | int putchar(int char) | 将由参数 char 指定的字符（无符号字符）写入 stdout。 |
| 39 | int puts(const char *str) | 将字符串写入 stdout，直到但不包括空字符。输出末尾会附加一个换行符。 |
| 40 | int ungetc(int char, FILE *stream) | 将字符 char（无符号字符）推回指定流，以便下次读取该字符。 |
| 41 | void perror(const char *str) | 打印描述性错误消息到 stderr。首先打印字符串 str，然后是冒号和空格。 |

## int fclose(FILE *stream)

### 描述

C 库函数 int fclose(FILE *stream) 关闭流。所有缓冲区都被刷新。

### 声明

以下是 fclose() 函数的声明。

```c
int fclose(FILE *stream)
```

### 参数

- stream -- 这是指向 FILE 对象的指针，指定要关闭的流。

### 返回值

此方法在流成功关闭时返回零。失败时返回 EOF。

### 示例

以下示例展示了 fclose() 函数的使用。

```c
#include <stdio.h>

int main()
{
    FILE *fp;

    fp = fopen("file.txt", "w");

    fprintf(fp, "%s", "This is tutorialspoint.com");
    fclose(fp);

    return(0);
}
```



让我们编译并运行上面的程序，该程序将创建一个文件 **file.txt**，然后写入以下文本行，最后使用 **fclose()** 函数关闭文件。

```
This is tutorialspoint.com
```

## void clearerr(FILE *stream)

### 描述

C 库函数 **void clearerr(FILE *stream)** 清除给定流的末尾文件和错误指示符。

### 声明

以下是 clearerr() 函数的声明。

```c
void clearerr(FILE *stream)
```

### 参数

- **stream** -- 这是指向标识流的 FILE 对象的指针。

### 返回值

这不应失败并且不会设置外部变量 *errno*，但如果检测到其参数不是有效的流，则必须返回 -1 并将 *errno* 设置为 EBADF。

### 示例

以下示例展示了 clearerr() 函数的用法。

```c
#include <stdio.h>

int main()
{
   FILE *fp;
   char c;

   fp = fopen("file.txt", "w");

   c = fgetc(fp);
   if( ferror(fp) )
   {
      printf("Error in reading from file : file.txt\n");
   }

   clearerr(fp);
   if( ferror(fp) )
   {
      printf("Error in reading from file : file.txt\n");
   }
   fclose(fp);

   return(0);
}
```

假设我们有一个文本文件 file.txt，它是一个空文件，让我们编译并运行上面的程序，这将产生以下结果，因为我们尝试读取一个以只写模式打开的文件。

```
Error reading from file "file.txt"
```

## int feof(FILE *stream)

### Description

C 库函数 int feof(FILE *stream) 测试给定流的末尾文件指示符。

### Declaration

以下是 feof() 函数的声明。

```c
int feof(FILE *stream)
```

### Parameters

- stream -- 这是指向标识流的 FILE 对象的指针。

### Return Value

当与流关联的末尾文件指示符被设置时，此函数返回非零值，否则返回零。

### Example

以下示例展示了 feof() 函数的用法。

```c
#include <stdio.h>

int main ()
{
    FILE *fp;
    int c;

    fp = fopen("file.txt","r");
    if(fp == NULL)
    {
        perror("Error in opening file");
        return(-1);
    }
    while(1)
    {
        c = fgetc(fp);
        if( feof(fp) )
        {
            break ;
        }
        printf("%c", c);
    }
    fclose(fp);
    return(0);
}
```

假设我们有一个文本文件 **file.txt**，其内容如下。此文件将用作我们示例程序的输入：

```
This is tutorialspoint.com
```

让我们编译并运行上面的程序，这将产生以下结果：

```
This is tutorialspoint.com
```

## int ferror(FILE *stream)

### Description

C 库函数 **int ferror(FILE *stream)** 测试给定流的错误指示符。

### Declaration

以下是 ferror() 函数的声明。

```c
int ferror(FILE *stream)
```

### Parameters

- **stream** -- 这是指向标识流的 FILE 对象的指针。

### Return Value

如果与流关联的错误指示符被设置，函数返回非零值，否则返回零值。

### Example

以下示例展示了 ferror() 函数的用法。

```c
#include <stdio.h>

int main()
{
    FILE *fp;
    char c;

    fp = fopen("file.txt", "w");

    c = fgetc(fp);
    if( ferror(fp) )
    {
        printf("Error in reading from file : file.txt\n");
    }

    clearerr(fp);
    if( ferror(fp) )
    {
        printf("Error in reading from file : file.txt\n");
    }
    fclose(fp);

    return(0);
}
```

假设我们有一个文本文件 file.txt，它是一个空文件。让我们编译并运行上面的程序，这将产生以下结果，因为我们尝试读取一个以只写模式打开的文件。

```c
fprintf(stdout, "and this will appear when programm\n");
fprintf(stdout, "will come after sleeping 5 seconds\n");

sleep(5);

return(0);
}
```

让我们编译并运行上面的程序，这将产生以下结果。这里程序将输出缓冲到 buff 中，直到遇到第一次调用 fflush()，之后它再次开始缓冲输出，最后休眠 5 秒。它在程序退出前将剩余输出发送到 STDOUT。

```
Going to set full buffering on
This is tutorialspoint.com
This output will go into buff
and this will appear when programm
will come after sleeping 5 seconds
```

## int fgetpos(FILE *stream, fpos_t *pos)

### Description

C 库函数 int fgetpos(FILE *stream, fpos_t *pos) 获取流的当前文件位置并将其写入 pos。

### Declaration

以下是 fgetpos() 函数的声明。

```c
int fgetpos(FILE *stream, fpos_t *pos)
```

### Parameters

- stream -- 这是指向标识流的 FILE 对象的指针。
- pos -- 这是指向 fpos_t 对象的指针。

### Return Value

此函数在成功时返回零，否则在出错时返回非零值。

### Example

以下示例展示了 fgetpos() 函数的用法。

```c
#include <stdio.h>

int main ()
{
    FILE *fp;
    fpos_t position;

    fp = fopen("file.txt","w+");
    fgetpos(fp, &position);
    fputs("Hello, World!", fp);

    fsetpos(fp, &position);
    fputs("This is going to override previous content", fp);
    fclose(fp);

    return(0);
}
```

让我们编译并运行上面的程序以创建文件 **file.txt**，其内容如下。首先我们使用 **fgetpos()** 函数获取文件的初始位置，然后在文件中写入 *Hello, World!*，但后来我们使用 **fsetpos()** 函数将写指针重置到文件开头，然后用以下内容覆盖文件：

This is going to override previous content

现在让我们使用以下程序查看上述文件的内容：

```c
#include <stdio.h>

int main ()
{
    FILE *fp;
    int c;
    int n = 0;

    fp = fopen("file.txt","r");
    while(1)
    {
        c = fgetc(fp);
        if( feof(fp) )
        {
            break ;
        }
        printf("%c", c);
    }

    fclose(fp);

    return(0);
}
```

## FILE *fopen(const char *filename, const char *mode)

### Description

C 库函数 FILE *fopen(const char *filename, const char *mode) 使用给定的模式打开由 filename 指向的文件名。

### Declaration

以下是 fopen() 函数的声明。

```c
FILE *fopen(const char *filename, const char *mode)
```

### Parameters

- **filename** -- 这是包含要打开的文件名的 C 字符串。
- **mode** -- 这是包含文件访问模式的 C 字符串。它包括：

| mode | Description |
|------|-------------|
| "r" | 打开文件进行读取。文件必须存在。 |
| "w" | 创建一个空文件用于写入。如果已存在同名文件，其内容将被擦除并且文件被视为新的空文件。 |
| "a" | 追加到文件。写入操作将数据追加到文件末尾。如果文件不存在，则创建文件。 |
| "r+" | 打开文件以便同时进行读写。文件必须存在。 |
| "w+" | 创建一个空文件用于读写。 |
| "a+" | 打开文件以便读取和追加。 |

### Return Value

此函数返回一个 FILE 指针。否则，返回 NULL 并且全局变量 errno 被设置为指示错误。

### Example

以下示例展示了 fopen() 函数的用法。

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    FILE * fp;

    fp = fopen ("file.txt", "w+");
    fprintf(fp, "%s %s %s %d", "We", "are", "in", 2012);

    fclose(fp);

    return(0);
}
```

让我们编译并运行上面的程序，它将创建文件 file.txt，其内容如下：

We are in 2012

现在让我们使用以下程序查看上述文件的内容：

```c
#include <stdio.h>

int main ()
{
    FILE *fp;
```


int c;

fp = fopen("file.txt","r");
while(1)
{
    c = fgetc(fp);
    if( feof(fp) )
    {
        break ;
    }
    printf("%c", c);
}
fclose(fp);
return(0);
}

## size_t fread(void *ptr, size_t size, size_t nmemb, FILE *stream)

### Description
C 库函数 **size_t fread(void *ptr, size_t size, size_t nmemb, FILE *stream)** 从给定的 **stream** 读取数据到由 **ptr** 指向的数组中。

### Declaration
以下是 fread() 函数的声明。

```
size_t fread(void *ptr, size_t size, size_t nmemb, FILE *stream)
```

### Parameters
- **ptr** -- 这是指向一块内存的指针，其最小大小为 size * nmemb 字节。
- **size** -- 这是要读取的每个元素的字节大小。
- **nmemb** -- 这是元素的数量，每个元素的大小为 **size** 字节。
- **stream** -- 这是指向 FILE 对象的指针，指定输入流。

### Return Value
返回成功读取的元素总数，以 size_t 对象形式返回，这是一个整数数据类型。如果该数字与 nmemb 参数不同，则表示发生了错误或到达了文件末尾。

### Example
以下示例展示了 fread() 函数的用法。

```c
#include <stdio.h>
#include <string.h>

int main()
{
   FILE *fp;
   char c[] = "this is tutorialspoint";
   char buffer[20];

   /* Open file for both reading and writing */
   fp = fopen("file.txt", "w+");

   /* Write data to the file */
   fwrite(c, strlen(c) + 1, 1, fp);

   /* Seek to the beginning of the file */
   fseek(fp, SEEK_SET, 0);

   /* Read and display data */
   fread(buffer, strlen(c)+1, 1, fp);
   printf("%s\n", buffer);
   fclose(fp);

   return(0);
}
```

让我们编译并运行上面的程序，它将创建一个文件 **file.txt** 并写入内容 *this is tutorialspoint*。之后，我们使用 **fseek()** 函数将写入指针重置到文件的开头，文件内容如下：

```
this is tutorialspoint
```

## FILE *freopen(const char *filename, const char *mode, FILE *stream)

### Description
C 库函数 **FILE *freopen(const char *filename, const char *mode, FILE *stream)** 将新的 **filename** 与给定的打开流关联，同时关闭流中的旧文件。

### Declaration
以下是 freopen() 函数的声明。

```c
FILE *freopen(const char *filename, const char *mode, FILE *stream)
```

### Parameters
- **filename** -- 这是包含要打开的文件名的 C 字符串。
- **mode** -- 这是包含文件访问模式的 C 字符串。包括：

| 模式 | 描述 |
| --- | --- |
| "r" | 打开文件进行读取。文件必须存在。 |
| "w" | 创建空文件用于写入。如果已存在同名文件，则其内容将被擦除并被视为新的空文件。 |
| "a" | 向文件追加。写入操作将数据追加到文件末尾。如果文件不存在则创建文件。 |
| "r+" | 打开文件以同时进行读写更新。文件必须存在。 |
| "w+" | 创建空文件用于读写。 |
| "a+" | 打开文件以进行读取和追加。 |

- **stream** -- 这是指向 FILE 对象的指针，标识要重新打开的流。

### Return Value
如果文件成功重新打开，函数返回标识该流的对象的指针，否则返回空指针。

### Example
以下示例展示了 freopen() 函数的用法。

```c
#include <stdio.h>

int main ()
{
    FILE *fp;

    printf("This text is redirected to stdout\n");

    fp = freopen("file.txt", "w+", stdout);

    printf("This text is redirected to file.txt\n");

    fclose(fp);

    return(0);
}
```

让我们编译并运行上面的程序，它将向 STDOUT 发送以下行，因为最初我们没有打开 stdout：

```
This text is redirected to stdout
```

在调用 **freopen()** 之后，它将 STDOUT 关联到文件 **file.txt**，因此写入 STDOUT 的任何内容都会进入 **file.txt**。因此，文件 **file.txt** 将具有以下内容。

```
This text is redirected to file.txt
```

现在让我们使用以下程序查看上述文件的内容：

```c
#include <stdio.h>

int main ()
{
    FILE *fp;
    int c;

    fp = fopen("file.txt", "r");
    while(1)
    {
        c = fgetc(fp);
        if( feof(fp) )
        {
            break ;
        }
        printf("%c", c);
    }
    fclose(fp);
    return(0);
}
```

## int fseek(FILE *stream, long int offset, int whence)

### Description
C 库函数 int fseek(FILE *stream, long int offset, int whence) 将流的文件位置设置为给定偏移量。

### Declaration
以下是 fseek() 函数的声明。

```
int fseek(FILE *stream, long int offset, int whence)
```

### Parameters
- **stream** -- 这是指向 FILE 对象的指针，标识该流。
- **offset** -- 这是从 whence 偏移的字节数。
- **whence** -- 这是偏移量添加的位置。由以下常量之一指定：

| 常量 | 描述 |
|---|---|
| SEEK_SET | 文件开头 |
| SEEK_CUR | 文件指针的当前位置 |
| SEEK_END | 文件末尾 |

### Return Value
该函数在成功时返回零，否则返回非零值。

### Example
以下示例展示了 fseek() 函数的用法。

```c
#include <stdio.h>

int main ()
{
    FILE *fp;

    fp = fopen("file.txt","w+");
    fputs("This is tutorialspoint.com", fp);

    fseek( fp, 7, SEEK_SET );
    fputs(" C Programming Language", fp);
    fclose(fp);

    return(0);
}
```

让我们编译并运行上面的程序，它将创建文件 file.txt 并具有以下内容。最初程序创建文件并写入 This is tutorialspoint.com，但后来我们将写入指针重置到开头第 7 个位置并使用 puts() 语句覆盖文件，内容如下：

```
This is C Programming Language
```

现在让我们使用以下程序查看上述文件的内容：

```c
#include <stdio.h>

int main ()
{
    FILE *fp;
    int c;

    fp = fopen("file.txt","r");
    while(1)
    {
        c = fgetc(fp);
        if( feof(fp) )
        {
            break ;
        }
        printf("%c", c);
    }
    fclose(fp);
    return(0);
}
```

## int fsetpos(FILE *stream, const fpos_t *pos)

### Description
C 库函数 **int fsetpos(FILE *stream, const fpos_t *pos)** 将给定 **stream** 的文件位置设置为给定位置。参数 **pos** 是由函数 fgetpos 给出的位置。

### Declaration
以下是 fsetpos() 函数的声明。

```c
int fsetpos(FILE *stream, const fpos_t *pos)
```

### Parameters
- **stream** -- 这是指向 FILE 对象的指针，标识该流。
- **pos** -- 这是指向 fpos_t 对象的指针，包含先前通过 fgetpos 获得的位置。

### Return Value
该函数在成功时返回零值，否则返回非零值并将全局变量 **errno** 设置为正值，可通过 perror 进行解释。

### Example
以下示例展示了 fsetpos() 函数的用法。

```c
#include <stdio.h>

int main ()
{

   FILE *fp;
    printf("%c", c);
}
    fclose(fp);
    return(0);
}
```

## long int ftell(FILE *stream)

### Description
C 库函数 **long int ftell(FILE *stream)** 返回给定流的当前文件位置。

### Declaration
以下是 ftell() 函数的声明。

```
long int ftell(FILE *stream)
```

### Parameters
- **stream** -- 这是指向 FILE 对象的指针，标识该流。

### Return Value
该函数返回位置指示器的当前值。如果发生错误，则返回 -1L，并将全局变量 errno 设置为正值。

### Example
以下示例展示了 ftell() 函数的用法。

```c
#include <stdio.h>

int main ()
{
    FILE *fp;
    int len;

    fp = fopen("file.txt", "r");
    if( fp == NULL )
    {
        perror ("Error opening file");
        return(-1);
    }
}
```




```
fseek(fp, 0, SEEK_END);

len = ftell(fp);
fclose(fp);

printf("Total size of file.txt = %d bytes\n", len);

return(0);
}
```

假设我们有一个文本文件 file.txt，其内容如下：

```
This is tutorialspoint.com
```

现在让我们编译并运行上述程序，如果文件具有上述内容，它将产生以下结果；否则将根据文件内容给出不同的结果：

```
Total size of file.txt = 27 bytes
```

## size_t fwrite(const void *ptr, size_t size, size_t nmemb, FILE *stream)

### 描述

C 库函数 size_t fwrite(const void *ptr, size_t size, size_t nmemb, FILE *stream) 将 ptr 所指向的数组中的数据写入给定的流。

### 声明

以下是 fwrite() 函数的声明。

```
size_t fwrite(const void *ptr, size_t size, size_t nmemb, FILE *stream)
```

### 参数

- ptr -- 这是指向要写入的元素数组的指针。
- size -- 这是要写入的每个元素的字节大小。
- nmemb -- 这是元素的数量，每个元素的大小为 size 字节。
- stream -- 这是指向 FILE 对象的指针，该对象指定一个输出流。

### 返回值

该函数返回成功返回的元素总数，以 size_t 对象形式返回，size_t 是一种整数数据类型。如果此数字与 nmemb 参数不同，则会显示错误。

### 示例

以下示例展示了 fwrite() 函数的用法。

```
#include<stdio.h>

int main ()
{
    FILE *fp;
    char str[] = "This is tutorialspoint.com";

    fp = fopen( "file.txt" , "w" );
    fwrite(str , 1 , sizeof(str) , fp );

    fclose(fp);

    return(0);
}
```

让我们编译并运行上述程序，它将创建一个文件 file.txt，其内容如下：

```
This is tutorialspoint.com
```

现在让我们使用以下程序查看上述文件的内容：

```
#include <stdio.h>

int main ()
{
    FILE *fp;
    int c;

    fp = fopen("file.txt","r");
    while(1)
    {
        c = fgetc(fp);
        if( feof(fp) )
        {
           break ;
        }
        printf("%c", c);
    }
    fclose(fp);
    return(0);
}
```

## int remove(const char *filename)

### 描述

C 库函数 **int remove(const char *filename)** 删除给定的 **filename**，使其不再可访问。

### 声明

以下是 remove() 函数的声明。

```
int remove(const char *filename)
```

### 参数

- **filename** -- 这是包含要删除文件名的 C 字符串。

### 返回值

成功时返回零。出错时返回 -1，并适当设置 errno。

### 示例

以下示例展示了 remove() 函数的用法。

```
#include <stdio.h>
#include <string.h>

int main ()
{
   int ret;
   FILE *fp;
   char filename[] = "file.txt";
   fp = fopen(filename, "w");

   fprintf(fp, "%s", "This is tutorialspoint.com");
   fclose(fp);

   ret = remove(filename);

   if(ret == 0)
   {
       printf("File deleted successfully");
   }
   else
   {
       printf("Error: unable to delete the file");
   }

   return(0);
}
```

假设我们有一个包含一些内容的文本文件 file.txt。因此，我们将使用上述程序删除此文件。让我们编译并运行上述程序以产生以下消息，该文件将被永久删除。

```
File deleted successfully
```

## int rename(const char *old_filename, const char *new_filename)

### 描述

C 库函数 int rename(const char *old_filename, const char *new_filename) 将 old_filename 引用的文件名更改为 new_filename。

### 声明

以下是 rename() 函数的声明。

```
int rename(const char *old_filename, const char *new_filename)
```

### 参数

- **old_filename** -- 这是包含要重命名和/或移动的文件名的 C 字符串。
- **new_filename** -- 这是包含文件新名称的 C 字符串。

### 返回值

成功时返回零。出错时返回 -1，并适当设置 errno。

### 示例

以下示例展示了 rename() 函数的用法。

```
#include <stdio.h>

int main ()
{
   int ret;
   char oldname[] = "file.txt";
   char newname[] = "newfile.txt";

   ret = rename(oldname, newname);

   if(ret == 0)
   {
      printf("File renamed successfully");
   }
   else
   {
      printf("Error: unable to rename the file");
   }

   return(0);
}
```

假设我们有一个包含一些内容的文本文件 **file.txt**。因此，我们将使用上述程序重命名此文件。让我们编译并运行上述程序以产生以下消息，该文件将被重命名为 **newfile.txt** 文件。

```
File renamed successfully
```

## void rewind(FILE *stream)

### 描述

C 库函数 **void rewind(FILE *stream)** 将文件位置设置为给定 **stream** 的文件开头。

### 声明

以下是 rewind() 函数的声明。

```
void rewind(FILE *stream)
```

### 参数

- **stream** -- 这是指向 FILE 对象的指针，该对象标识流。

### 返回值

该函数不返回任何值。

### 示例

以下示例展示了 rewind() 函数的用法。

```
#include <stdio.h>

int main()
{
   char str[] = "This is tutorialspoint.com";
   FILE *fp;
   int ch;

   /* First let's write some content in the file */
   fp = fopen( "file.txt" , "w" );
   fwrite(str , 1 , sizeof(str) , fp );
   fclose(fp);

   fp = fopen( "file.txt" , "r" );
   while(1)
   {
      ch = fgetc(fp);
      if( feof(fp) )
      {
         break ;
      }
}
    printf("%c", ch);
}
rewind(fp);
printf("\n");
while(1)
{
    ch = fgetc(fp);
    if( feof(fp) )
    {
        break ;
    }
    printf("%c", ch);
}
fclose(fp);

    return(0);
}
```

假设我们有一个文本文件 file.txt，其内容如下：

```
This is tutorialspoint.com
```

现在让我们编译并运行上述程序以产生以下结果：

```
This is tutorialspoint.com
This is tutorialspoint.com
```

## void setbuf(FILE *stream, char *buffer)

### 描述

C 库函数 void setbuf(FILE *stream, char *buffer) 定义流应如何缓冲。应在与流关联的文件已经打开之后、但尚未进行任何输入或输出操作之前调用此函数。

### 声明

以下是 setbuf() 函数的声明。

```
void setbuf(FILE *stream, char *buffer)
```

### 参数

- **stream** -- 这是指向 FILE 对象的指针，该对象标识一个打开的流。
- **buffer** -- 这是用户分配的缓冲区。其长度至少应为 BUFSIZ 字节，BUFSIZ 是一个宏常量，用作此数组的长度。

### 返回值

该函数不返回任何值。

### 示例

以下示例展示了 setbuf() 函数的用法。

```
#include <stdio.h>

int main()
{
    char buf[BUFSIZ];

    setbuf(stdout, buf);
    puts("This is tutorialspoint");

    fflush(stdout);
    return(0);
}
```

让我们编译并运行上述程序以产生以下结果。此处程序在输出出现之前将其发送到 STDOUT，否则它会持续缓冲输出。你也可以使用 fflush() 函数来刷新输出。

```
This is tutorialspoint
```

## int setvbuf(FILE *stream, char *buffer, int mode, size_t size)

### 描述

C 库函数 int setvbuf(FILE *stream, char *buffer, int mode, size_t size) 定义流应如何缓冲。

### 声明

以下是 setvbuf() 函数的声明。

```
int setvbuf(FILE *stream, char *buffer, int mode, size_t size)
```

### 参数

- **stream** -- 这是指向 FILE 对象的指针，该对象标识一个打开的流。
- **buffer** -- 这是用户分配的缓冲区。如果设置为 NULL，函数会自动分配指定大小的缓冲区。
- **mode** -- 这指定文件缓冲模式：

| mode | 描述 |
|------|-------------|
| _IOFBF | **全缓冲：** 在输出时，数据在缓冲区满后写入。在输入时，当请求输入操作且缓冲区为空时，缓冲区被填满。 |
| _IOLBF | **行缓冲：** 在输出时，当向流中插入换行符或缓冲区已满时（以先发生者为准）写入数据。在输入时，当请求输入操作且缓冲区为空时，缓冲区会被填充直到下一个换行符。 |
| _IONBF | **无缓冲：** 不使用缓冲区。每个 I/O 操作都尽快写入。buffer 和 size 参数被忽略。 |

- **size** -- 这是缓冲区大小，以字节为单位

### 返回值

该函数成功时返回零，否则返回非零值。

### 示例

以下示例展示了 setvbuf() 函数的用法。

```
#include <stdio.h>

int main()
{
    char buff[1024];

    memset( buff, '\0', sizeof( buff ));
```



```
fprintf(stdout, "Going to set full buffering on\n");
setvbuf(stdout, buff, _IOFBF, 1024);

fprintf(stdout, "This is tutorialspoint.com\n");
fprintf(stdout, "This output will go into buff\n");
fflush( stdout );

fprintf(stdout, "and this will appear when programm\n");
fprintf(stdout, "will come after sleeping 5 seconds\n");

sleep(5);

return(0);
}
```

让我们编译并运行上面的程序以产生以下结果。这里程序将输出缓冲到 buff 中，直到遇到第一次 fflush() 调用，之后它再次开始缓冲输出，最后休眠 5 秒。它在程序退出前将剩余输出发送到 STDOUT。

```
Going to set full buffering on
This is tutorialspoint.com
This output will go into buff
and this will appear when programm
will come after sleeping 5 seconds
```

## FILE \*tmpfile(void)

### 描述

C 库函数 FILE \*tmpfile(void) 以二进制更新模式（wb+）创建一个临时文件。创建的临时文件在流被关闭（fclose）或程序终止时自动删除。

### 声明

以下是 tmpfile() 函数的声明。

```
FILE *tmpfile(void)
```

### 参数

- NA

### 返回值

如果成功，函数返回指向创建的临时文件的流指针。如果无法创建文件，则返回 NULL。

### 示例

以下示例展示了 tmpfile() 函数的使用。

```
#include <stdio.h>

int main ()
{
    FILE *fp;

    fp = tmpfile();
    printf("Temporary file created\n");

    /* you can use tmp file here */

    fclose(fp);

    return(0);
}
```

让我们编译并运行上面的程序以在 /tmp 文件夹中创建一个临时文件，但一旦你的程序退出，它将被自动删除，并且程序将产生以下结果：

```
Temporary file created
```

## char \*tmpnam(char \*str)

### 描述

C 库函数 char \*tmpnam(char \*str) 生成并返回一个有效且不存在的临时文件名。如果 str 为空，则它仅返回 tmp 文件名。

### 声明

以下是 tmpnam() 函数的声明。

```
char *tmpnam(char *str)
```

### 参数

- str -- 这是指向字符数组的指针，其中建议的临时名称将作为 C 字符串存储。

### 返回值

- 返回值是指向包含临时文件建议名称的 C 字符串的指针。如果 str 为空指针，则指向一个内部缓冲区，该缓冲区将在下一次调用此函数时被覆盖。
- 如果 str 不是空指针，则返回 str。如果函数无法创建合适的名称，则返回空指针。

### 示例

以下示例展示了 tmpnam() 函数的使用。

```
#include <stdio.h>

int main()
{
    char buffer[L_tmpnam];
    char *ptr;

    tmpnam(buffer);
    printf("Temporary name 1: %s\n", buffer);

    ptr = tmpnam(NULL);
    printf("Temporary name 2: %s\n", ptr);

    return(0);
}
```

让我们编译并运行上面的程序以产生以下结果：

```
Temporary name 1: /tmp/filebaalTb
Temporary name 2: /tmp/filedCIbb0
```

## int fprintf(FILE \*stream, const char \*format, ...)

### 描述

C 库函数 int fprintf(FILE \*stream, const char \*format, ...) 将格式化输出发送到 stdout。

|  |  |
|---|---|
| X | 无符号十六进制整数（大写字母） |
| p | 指针地址 |
| n | 不打印任何内容 |
| % | 字符 |

| **flags** | **描述** |
|---|---|
| - | 在给定字段宽度内左对齐；右对齐为默认值（参见 width 子说明符）。 |
| + | 强制在结果前加上正负号（+ 或 -），即使对于正数也是如此。默认情况下，只有负数前面加上 - 号。 |
| (space) | 如果未写入符号，则在值前插入一个空白字符。 |
| # | 与 o、x 或 X 说明符一起使用。值前面加上 0、0x 或 0X，分别对应非零值。用于 e、E 和 f 时，强制写入的输出包含小数点，即使后面没有数字。默认情况下，如果后面没有数字则不写入小数点。用于 g 或 G 时，结果与 e 或 E 相同，但尾随零不会被移除。 |
| 0 | 在指定填充的情况下，用零（0）而不是空格左填充数字（参见 width 子说明符）。 |

| **width** | **描述** |
|---|---|
| (number) | 最小打印字符数。如果要打印的值短于此数字，结果将用空白字符填充。即使结果更大，值也不会被截断。 |
| \* | 宽度未在格式字符串中指定，而是作为格式化前的前置额外整数值参数。 |

| .precision | 描述 |
|---|---|
| .number | 对于整数说明符（d、i、o、u、x、X）：precision 指定要写入的最小数字数。如果要写入的值短于此数字，结果将用前导零填充。即使结果更长，值也不会被截断。precision 为 0 表示对于值 0 不写入任何字符。对于 e、E 和 f 说明符：这是要在小数点后打印的位数。对于 g 和 G 说明符：这是要打印的最大有效位数。对于 s：这是要打印的最大字符数。默认情况下，直到遇到结束空字符，所有字符都会被打印。对于 c 类型：无效。当未指定精度时，默认值为 1。如果指定了小数点但未明确给出精度值，则假定为 0。 |
| .\* | 精度未在格式字符串中指定，而是作为格式化前的前置额外整数值参数。 |

| length | 描述 |
|---|---|
| h | 参数被解释为 short int 或 unsigned short int（仅适用于整数说明符：i、d、o、u、x 和 X）。 |
| l | 对于整数说明符（i、d、o、u、x 和 X），参数被解释为 long int 或 unsigned long int；对于说明符 c 和 s，则解释为宽字符或宽字符字符串。 |
| L | 参数被解释为 long double（仅适用于浮点说明符：e、E、f、g 和 G）。 |

- **additional arguments** -- 根据格式字符串，函数可能期望一系列额外参数，每个参数包含一个值，用来代替格式参数中指定的每个 %-标记，如果有的话。这些参数的数量应与期望值的 %-标记数量相同。

### 返回值

如果成功，返回写入的字符总数，否则返回负数。

### 示例

以下示例展示了 fprintf() 函数的使用。

```
#include <stdio.h>
#include <stdlib.h>

int main()
{
    FILE * fp;

    fp = fopen ("file.txt", "w+");
    fprintf(fp, "%s %s %s %d", "We", "are", "in", 2012);

    fclose(fp);

    return(0);
}
```

让我们编译并运行上面的程序，它将创建一个文件 **file.txt**，内容如下：

We are in 2012

现在让我们使用以下程序查看上述文件的内容：

```
#include <stdio.h>

int main ()
{
    FILE *fp;
    int c;

    fp = fopen("file.txt","r");
    while(1)
    {
        c = fgetc(fp);
        if( feof(fp) )
        {
            break ;
        }
        printf("%c", c);
    }

    fclose(fp);

    return(0);
}
```

## int printf(const char \*format, ...)

### 描述

C 库函数 int printf(const char \*format, ...) 将格式化输出发送到 stdout。

### 声明

以下是 printf() 函数的声明。

```
int printf(const char *format, ...)
```

### 参数

- **format** -- 这是包含要写入 stdout 的文本的字符串。它可以 optionally 包含嵌入的格式标记，这些标记将被后续额外参数中指定的值替换并按请求格式化。格式标记原型为 %[flags][width][.precision][length]specifier，其解释如下：

| specifier | 输出 |
|---|---|
| c | 字符 |
| d or i | 有符号十进制整数 |
| e | 使用 e 字符的科学计数法（尾数/指数） |
| E | 使用 E 字符的科学计数法（尾数/指数） |
| f | 十进制浮点数 |
| g | 使用 %e 或 %f 中较短的一个。 |
| G | 使用 %E 或 %f 中较短的一个。 |




| specifier | Output |
| --- | --- |
| o | 有符号八进制 |
| s | 字符字符串 |
| u | 无符号十进制整数 |
| x | 无符号十六进制整数 |
| X | 无符号十六进制整数（大写字母） |
| p | 指针地址 |
| n | 不打印任何内容 |
| % | 字符 |

| flags | Description |
| --- | --- |
| - | 在给定字段宽度内左对齐；右对齐为默认值（参见宽度子说明符）。 |
| + | 强制在结果前加上正负号（+ 或 -），即使对于正数也是如此。默认情况下，只有负数前面加上 - 号。 |
| (space) | 如果不写入符号，则在值前插入一个空白字符。 |
| # | 与 o、x 或 X 说明符一起使用时，若值不为零，则在值前加上 0、0x 或 0X。 与 e、E 和 f 一起使用时，强制输出包含小数点，即使其后没有数字。默认情况下，如果其后没有数字，则不写入小数点。 与 g 或 G 一起使用时，结果与 e 或 E 相同，但尾随零不会被移除。 |
| 0 | 在指定填充的情况下，用零（0）而不是空格左填充数字（参见宽度子说明符）。 |

| width | Description |
| --- | --- |
| (number) | 打印的最小字符数。如果要打印的值短于此数字，则结果用空白填充。即使结果更大，值也不会被截断。 |
| * | 宽度未在格式字符串中指定，而是作为格式化前的前一个附加整数值参数。 |

| .precision | Description |
| --- | --- |
| .number | 对于整数说明符（d、i、o、u、x、X）：精度指定要写入的最小位数。如果要写入的值短于此数字，则结果用前导零填充。即使结果更长，值也不会被截断。精度为 0 表示对于值 0 不写入任何字符。对于 e、E 和 f 说明符：这是小数点后要打印的位数。对于 g 和 G 说明符：这是要打印的最大有效位数。对于 s：这是要打印的最大字符数。默认情况下，直到遇到结束空字符为止，所有字符都会被打印。对于 c 类型：无效。当未指定精度时，默认为 1。如果指定了小数点但未明确给出精度值，则假定为 0。 |
| .* | 精度未在格式字符串中指定，而是作为格式化前的前一个附加整数值参数。 |

| length | Description |
| --- | --- |
| h | 参数被解释为 short int 或 unsigned short int（仅适用于整数说明符：i、d、o、u、x 和 X）。 |
| l | 参数被解释为 long int 或 unsigned long int（适用于整数说明符：i、d、o、u、x 和 X），以及宽字符或宽字符字符串（适用于说明符 c 和 s）。 |
| L | 参数被解释为 long double（仅适用于浮点说明符：e、E、f、g 和 G）。 |

- **additional arguments** -- 根据格式字符串，函数可能期望一系列附加参数，每个参数包含一个值，用以替换格式参数中指定的每个 %-标记（如果有）。这些参数的数量应与期望值的 %-标记数量相同。

### 返回值

如果成功，返回写入的总字符数。失败时，返回负数。

### 示例

以下示例展示了 printf() 函数的使用。

```c
#include <stdio.h>

int main ()
{
    int ch;

    for( ch = 75 ; ch <= 100; ch++ ) {
        printf("ASCII value = %d, Character = %c\n", ch , ch );
    }

    return(0);
}
```

编译并运行上述程序以产生以下结果：

```
ASCII value = 75, Character = K
ASCII value = 76, Character = L
ASCII value = 77, Character = M
ASCII value = 78, Character = N
ASCII value = 79, Character = O
ASCII value = 80, Character = P
ASCII value = 81, Character = Q
ASCII value = 82, Character = R
ASCII value = 83, Character = S
ASCII value = 84, Character = T
ASCII value = 85, Character = U
ASCII value = 86, Character = V
ASCII value = 87, Character = W
ASCII value = 88, Character = X
ASCII value = 89, Character = Y
ASCII value = 90, Character = Z
ASCII value = 91, Character = [
ASCII value = 92, Character = \
ASCII value = 93, Character = ]
ASCII value = 94, Character = ^
ASCII value = 95, Character = _
ASCII value = 96, Character = `
ASCII value = 97, Character = a
ASCII value = 98, Character = b
ASCII value = 99, Character = c
ASCII value = 100, Character = d
```

## int sprintf(char *str, const char *format, ...)

### 描述

C 库函数 int sprintf(char *str, const char *format, ...) 将格式化输出发送到由 str 指向的字符串。

### 声明

```c
int sprintf(char *str, const char *format, ...)
```

### 参数

- **str** -- 这是指向字符元素数组的指针，其中存储结果的 C 字符串。
- **format** -- 这是包含要写入缓冲区的文本的字符串。它可以 optionally 包含嵌入的格式标记，这些标记将被后续附加参数中指定的值替换并按请求格式化。格式标记原型：`%[flags][width][.precision][length]specifier`，如下所述：

| specifier | Output |
| --- | --- |
| c | 字符 |
| d or i | 有符号十进制整数 |
| e | 科学计数法（尾数/指数）使用 e 字符 |
| E | 科学计数法（尾数/指数）使用 E 字符 |
| f | 十进制浮点数 |
| g | 使用 %e 或 %f 中较短者。 |
| G | 使用 %E 或 %f 中较短者 |
| o | 有符号八进制 |
| s | 字符字符串 |
| u | 无符号十进制整数 |
| x | 无符号十六进制整数 |
| X | 无符号十六进制整数（大写字母） |
| p | 指针地址 |
| n | 不打印任何内容 |
| % | 字符 |

| flags | Description |
| --- | --- |
| - | 在给定字段宽度内左对齐；右对齐为默认值（参见宽度子说明符）。 |
| + | 强制在结果前加上正负号（+ 或 -），即使对于正数也是如此。默认情况下，只有负数前面加上 - 号。 |
| (space) | 如果不写入符号，则在值前插入一个空白字符。 |
| # | 与 o、x 或 X 说明符一起使用时，若值不为零，则在值前加上 0、0x 或 0X。 与 e、E 和 f 一起使用时，强制输出包含小数点，即使其后没有数字。默认情况下，如果其后没有数字，则不写入小数点。 与 g 或 G 一起使用时，结果与 e 或 E 相同，但尾随零不会被移除。 |
| 0 | 在指定填充的情况下，用零（0）而不是空格左填充数字（参见宽度子说明符）。 |

| width | Description |
| --- | --- |
| (number) | 打印的最小字符数。如果要打印的值短于此数字，则结果用空白填充。即使结果更大，值也不会被截断。 |
| * | 宽度未在格式字符串中指定，而是作为格式化前的前一个附加整数值参数。 |

| .precision | Description |
| --- | --- |
| .number | 对于整数说明符（d、i、o、u、x、X）：精度指定要写入的最小位数。如果要写入的值短于此数字，则结果用前导零填充。即使结果更长，值也不会被截断。精度为 0 表示对于值 0 不写入任何字符。对于 e、E 和 f 说明符：这是小数点后要打印的位数。对于 g 和 G 说明符：这是要打印的最大有效位数。对于 s：这是要打印的最大字符数。默认情况下，直到遇到结束空字符为止，所有字符都会被打印。对于 c 类型：无效。当未指定精度时，默认为 1。如果指定了小数点但未明确给出精度值，则假定为 0。 |
| .* | 精度未在格式字符串中指定，而是作为格式化前的前一个附加整数值参数。 |

| length | Description |
| --- | --- |
| h | 参数被解释为 short int 或 unsigned short int（仅适用于整数说明符：i、d、o、u、x 和 X）。 |
| l | 参数被解释为 long int 或 unsigned long int（适用于整数说明符：i、d、o、u、x 和 X），以及宽字符或宽字符字符串（适用于说明符 c 和 s）。 |
| L | 参数被解释为 long double（仅适用于浮点说明符：e、E、f、g 和 G）。 |




| 长度 | 描述 |
| --- | --- |
| h | 参数被解释为 short int 或 unsigned short int（仅适用于整数说明符：i, d, o, u, x 和 X）。 |
| l | 参数被解释为 long int 或 unsigned long int 用于整数说明符（i, d, o, u, x 和 X），并且对于说明符 c 和 s 被解释为宽字符或宽字符字符串。 |
| L | 参数被解释为 long double（仅适用于浮点说明符：e, E, f, g 和 G）。 |

- **附加参数** -- 根据格式字符串，函数可能期望一系列附加参数，每个参数包含一个值，用于替换格式参数中指定的每个 %-tag（如果有）。这些参数的数量应与期望值的 %-tag 数量相同。

### 返回值

如果成功，返回写入的字符总数，不包括字符串末尾附加的空字符；否则，在失败情况下返回负数。

### 示例

以下示例展示了 sprintf() 函数的使用。

```c
#include <stdio.h>
#include <math.h>

int main()
{
    char str[80];

    sprintf(str, "Value of Pi = %f", M_PI);
    puts(str);

    return(0);
}
```

让我们编译并运行上述程序，这将产生以下结果：

```
Value of Pi = 3.141593
```

## `int vfprintf(FILE *stream, const char *format, va_list arg)`

### 描述

C 库函数 int vfprintf(FILE *stream, const char *format, va_list arg) 使用传递给它的参数列表向流发送格式化输出。

### 声明

以下是 vfprintf() 函数的声明。

```c
int vfprintf(FILE *stream, const char *format, va_list arg)
```

### 参数

- **stream** -- 这是指向标识流的 FILE 对象的指针。
- **format** -- 这是要写入流的 C 字符串。它可以可选地包含嵌入的格式标签，这些标签将被后续附加参数指定的值替换并按请求格式化。格式标签原型：%[flags][width][.precision][length]specifier，如下所述：

| 说明符 | 输出 |
| --- | --- |
| c | 字符 |
| d or i | 有符号十进制整数 |
| e | 使用 e 字符的科学计数法（尾数/指数） |
| E | 使用 E 字符的科学计数法（尾数/指数） |
| f | 十进制浮点数 |
| g | 使用 %e 或 %f 中较短的一个 |
| G | 使用 %E 或 %f 中较短的一个 |
| o | 有符号八进制 |
| s | 字符字符串 |
| u | 无符号十进制整数 |
| x | 无符号十六进制整数 |
| X | 无符号十六进制整数（大写字母） |
| p | 指针地址 |
| n | 无输出 |
| % | 字符 |

| 标志 | 描述 |
| --- | --- |
| - | 在给定字段宽度内左对齐；右对齐为默认值（参见 width 子说明符）。 |
| + | 强制在结果前加上正负号（+ 或 -），即使对于正数也是如此。默认情况下，只有负数前面加上 - 号。 |
| (space) | 如果不写入符号，则在值前插入一个空白字符。 |
| # | 与 o、x 或 X 说明符一起使用时，对于非零值，值前面分别加上 0、0x 或 0X。与 e、E 和 f 一起使用时，它强制写入的输出包含小数点，即使后面没有数字。默认情况下，如果后面没有数字，则不写入小数点。与 g 或 G 一起使用时，结果与 e 或 E 相同，但尾随零不会被移除。 |
| 0 | 在指定填充的位置用零（0）而不是空格左填充数字（参见 width 子说明符）。 |

| 宽度 | 描述 |
| --- | --- |
| (number) | 打印的最小字符数。如果要打印的值短于此数字，结果将用空白字符填充。即使结果更大，值也不会被截断。 |
| * | 宽度未在格式字符串中指定，而是作为格式化前参数的前一个附加整数值参数。 |

| .精度 | 描述 |
| --- | --- |
| .number | 对于整数说明符（d、i、o、u、x、X）：精度指定要写入的最小位数。如果要写入的值短于此数字，结果将用前导零填充。即使结果更长，值也不会被截断。精度为 0 表示对于值 0 不写入任何字符。对于 e、E 和 f 说明符：这是小数点后要打印的位数。对于 g 和 G 说明符：这是要打印的最大有效位数。对于 s：这是要打印的最大字符数。默认情况下，直到遇到结束空字符，所有字符都会被打印。对于 c 类型：无效。当未指定精度时，默认值为 1。如果指定了小数点但未明确给出精度值，则假定为 0。 |
| .* | 精度未在格式字符串中指定，而是作为格式化前参数的前一个附加整数值参数。 |

| 长度 | 描述 |
| --- | --- |
| h | 参数被解释为 short int 或 unsigned short int（仅适用于整数说明符：i, d, o, u, x 和 X）。 |
| l | 参数被解释为 long int 或 unsigned long int 用于整数说明符（i, d, o, u, x 和 X），并且对于说明符 c 和 s 被解释为宽字符或宽字符字符串。 |
| L | 参数被解释为 long double（仅适用于浮点说明符：e, E, f, g 和 G）。 |

- **arg** -- 表示可变参数列表的对象。这应由 `<stdarg.h>` 中定义的 va_start 宏初始化。

### 返回值

如果成功，返回写入的字符总数；否则返回负数。

### 示例

以下示例展示了 vfprintf() 函数的使用。

```c
#include <stdio.h>
#include <stdarg.h>

void WriteFrmtd(FILE *stream, char *format, ...)
{
    va_list args;

    va_start(args, format);
    vfprintf(stream, format, args);
    va_end(args);
}

int main ()
{
    FILE *fp;

    fp = fopen("file.txt","w");

    WriteFrmtd(fp, "This is just one argument %d \n", 10);

    fclose(fp);

    return(0);
}
```

让我们编译并运行上述程序，该程序将在当前目录中以写入方式打开文件 **file.txt** 并写入以下内容：

```
This is just one argument 10
```

现在让我们使用以下程序查看上述文件的内容：

```c
#include <stdio.h>

int main ()
{
    FILE *fp;
    int c;

    fp = fopen("file.txt","r");
    while(1)
    {
        c = fgetc(fp);
        if( feof(fp) )
        {
            break ;
        }
        printf("%c", c);
    }
    fclose(fp);
    return(0);
}
```

## `int vprintf(const char *format, va_list arg)`

### 描述

C 库函数 int vprintf(const char *format, va_list arg) 使用传递给它的参数列表向 stdout 发送格式化输出。

### 声明

以下是 vprintf() 函数的声明。

```c
int vprintf(const char *format, va_list arg)
```

### 参数

- **format** -- 这是要写入 stdout 的 C 字符串。它可以可选地包含嵌入的格式标签，这些标签将被后续附加参数指定的值替换并按请求格式化。格式标签原型为：%[flags][width][.precision][length]specifier，如下所述：

| 说明符 | 输出 |
| --- | --- |
| c | 字符 |

| **标志** | **描述** |
| --- | --- |
| # | 与 o、x 或 X 说明符一起使用时，对于非零值，值前面分别加上 0、0x 或 0X。与 e、E 和 f 一起使用时，它强制写入的输出包含小数点，即使后面没有数字。默认情况下，如果后面没有数字，则不写入小数点。与 g 或 G 一起使用时，结果与 e 或 E 相同，但尾随零不会被移除。 |
| 0 | 在指定填充的位置用零（0）而不是空格左填充数字（参见 width 子说明符）。 |

| **宽度** | **描述** |
| --- | --- |
| (number) | 打印的最小字符数。如果要打印的值短于此数字，结果将用空白字符填充。即使结果更大，值也不会被截断。 |
| * | 宽度未在格式字符串中指定，而是作为格式化前参数的前一个附加整数值参数。 |

| **.精度** | **描述** |
| --- | --- |
| .number | 对于整数说明符（d、i、o、u、x、X）：精度指定要写入的最小位数。如果要写入的值短于此数字，结果将用前导零填充。即使结果更长，值也不会被截断。精度为 0 表示对于值 0 不写入任何字符。对于 e、E 和 f 说明符：这是小数点后要打印的位数。对于 g 和 G 说明符：这是要打印的最大有效位数。对于 s：这是要打印的最大字符数。默认情况下，直到遇到结束空字符，所有字符都会被打印。对于 c 类型：无效。当未指定精度时，默认值为 1。如果指定了小数点但未明确给出精度值，则假定为 0。 |
| .* | 精度未在格式字符串中指定，而是作为格式化前参数的前一个附加整数值参数。 |

| **长度** | **描述** |
| --- | --- |



| 修饰符 | 描述 |
|---|---|
| h | 参数被解释为 short int 或 unsigned short int（仅适用于整数说明符：i、d、o、u、x 和 X）。 |
| l | 对于整数说明符（i、d、o、u、x 和 X），参数被解释为 long int 或 unsigned long int；对于说明符 c 和 s，参数被解释为宽字符或宽字符串。 |
| L | 参数被解释为 long double（仅适用于浮点说明符：e、E、f、g 和 G）。 |

- **arg** -- 表示可变参数列表的对象。这应由 <stdarg> 中定义的 va_start 宏初始化。

### 返回值

如果成功，则返回写入的总字符数，否则返回负数。

### 示例

以下示例演示了 vprintf() 函数的用法。

```c
#include <stdio.h>
#include <stdarg.h>

void WriteFrmtd(char *format, ...)
{
    va_list args;

    va_start(args, format);
    vprintf(format, args);
    va_end(args);
}

int main ()
{
    WriteFrmtd("%d variable argument\n", 1);
    WriteFrmtd("%d variable %s\n", 2, "arguments");

    return(0);
}
```

让我们编译并运行上述程序，它将产生以下结果：

```
1 variable argument
2 variable arguments
```

## int vsprintf(char *str, const char *format, va_list arg)

### 描述

C 库函数 int vsprintf(char *str, const char *format, va_list arg) 使用传递给它的参数列表将格式化输出发送到字符串。

### 声明

以下是 vsprintf() 函数的声明。

```c
int vsprintf(char *str, const char *format, va_list arg)
```

### 参数

- str -- 这是 char 元素数组，结果字符串将存储在其中。
- format -- 这是 C 字符串，包含要写入 str 的文本。它可以选择包含内嵌格式标签，这些标签会被后续附加参数中指定的值替换，并按要求格式化。格式标签原型：%[flags][width][.precision][length]specifier，如下所述：

| 说明符 | 输出 |
|---|---|
| c | 字符 |
| d 或 i | 有符号十进制整数 |
| e | 使用 e 字符的科学计数法（尾数/指数） |
| E | 使用 E 字符的科学计数法（尾数/指数） |
| f | 十进制浮点数 |
| g | 使用 %e 或 %f 中较短者 |
| G | 使用 %E 或 %f 中较短者 |
| o | 有符号八进制 |
| s | 字符串 |
| u | 无符号十进制整数 |
| x | 无符号十六进制整数 |
| X | 无符号十六进制整数（大写字母） |
| p | 指针地址 |
| n | 不打印任何内容 |
| % | 字符 |

| 标志 | 描述 |
|---|---|
| - | 在给定字段宽度内左对齐；默认右对齐（参见 width 子说明符）。 |
| + | 强制在结果前加上正号或负号（+ 或 -），即使对于正数也是如此。默认情况下，只有负数前会加上负号。 |
| (空格) | 如果不会写入任何符号，则在值前插入一个空格。 |
| # | 与 o、x 或 X 说明符一起使用时，对于不等于零的值，值前会分别加上 0、0x 或 0X。与 e、E 和 f 一起使用时，它强制写入的输出包含小数点，即使后面没有数字。默认情况下，如果后面没有数字，则不写入小数点。与 g 或 G 一起使用时，结果与 e 或 E 相同，但不会删除末尾的零。 |
| 0 | 在指定填充时（参见 width 子说明符），用零（0）而不是空格左填充数字。 |
| width | 描述 |

### 返回值

如果成功，则返回写入的总字符数，否则返回负数。

### 示例

以下示例演示了 vsprintf() 函数的用法。

```c
#include <stdio.h>
#include <stdarg.h>

char buffer[80];
int vspfunc(char *format, ...)
{
   va_list aptr;
   int ret;

   va_start(aptr, format);
   ret = vsprintf(buffer, format, aptr);
   va_end(aptr);

   return(ret);
}

int main()
{
   int i = 5;
   float f = 27.0;
   char str[50] = "tutorialspoint.com";

   vspfunc("%d %f %s", i, f, str);
   printf("%s\n", buffer);

   return(0);
}
```

让我们编译并运行上述程序，这将产生以下结果：

## int fscanf(FILE *stream, const char *format, ...)

### 描述

C 库函数 int fscanf(FILE *stream, const char *format, ...) 从流中读取格式化输入。

### 声明

以下是 fscanf() 函数的声明。

```c
int fscanf(FILE *stream, const char *format, ...)
```

### 参数

- **stream** -- 这是指向 FILE 对象的指针，该对象标识流。
- **format** -- 这是 C 字符串，包含以下一项或多项：空白字符、非空白字符和格式说明符。格式说明符将如下所示：[= %[*][width][modifiers]type=]，其说明如下：

| 参数 | 描述 |
|---|---|
| * | 这是一个可选的起始星号，表示要从流中读取数据但忽略它，即不将其存储到对应参数中。 |
| width | 指定当前读取操作中要读取的最大字符数。 |
| modifiers | 为对应附加参数所指向的数据指定与 int（对于 d、i 和 n）、unsigned int（对于 o、u 和 x）或 float（对于 e、f 和 g）不同的大小：h：short int（对于 d、i 和 n），或 unsigned short int（对于 o、u 和 x）；l：long int（对于 d、i 和 n），或 unsigned long int（对于 o、u 和 x），或 double（对于 e、f 和 g）；L：long double（对于 e、f 和 g） |
| type | 指定要读取的数据类型以及期望如何读取的字符。参见下表。 |

### fscanf 类型说明符：

| 类型 | 限定输入 | 参数类型 |
|---|---|---|
| c | 单个字符：读取下一个字符。如果指定了不同于 1 的宽度，函数将读取 width 个字符并将它们存储在作为参数传递的数组的连续位置中。末尾不会追加空字符。 | char * |
| d | 十进制整数：可选地以 + 或 - 符号开头的数字 | int * |
| e、E、f、g、G | 浮点数：包含小数点的十进制数，可选地以 + 或 - 符号开头，并可选地后跟 e 或 E 字符和十进制数。有效条目的两个示例是 -732.103 和 7.12e4 | float * |
| o | 八进制整数： | int * |
| s | 字符串。这将读取后续字符，直到找到空白字符（空白字符被视为空格、换行和制表符）。 | char * |
| u | 无符号十进制整数。 | unsigned int * |
| x、X | 十六进制整数 | int * |

- **附加参数** -- 根据格式字符串，函数可能期望一系列附加参数，每个参数包含一个值，用于替换格式参数中指定的每个 % 标签（如果有）。这些参数的数量应与期望值的 % 标签数量相同。

### 返回值

该函数返回成功匹配并赋值的输入项数，该数量可能少于提供的数量，或者在早期匹配失败时甚至为零。

### 示例

以下示例演示了 fscanf() 函数的用法。

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
   char str1[10], str2[10], str3[10];
   int year;
   FILE * fp;

   fp = fopen ("file.txt", "w+");
   fputs("We are in 2012", fp);

   rewind(fp);
   fscanf(fp, "%s %s %s %d", str1, str2, str3, &year);

   printf("Read String1 |%s|\n", str1 );
   printf("Read String2 |%s|\n", str2 );
   printf("Read String3 |%s|\n", str3 );
   printf("Read Integer |%d|\n", year );

   fclose(fp);

   return(0);
}
```

让我们编译并运行上述程序，它将产生以下结果：

```text
Read String1 |We|
Read String2 |are|
Read String3 |in|
Read Integer |2012|
```

## int scanf(const char *format, ...)

### 描述

C 库函数 **int scanf(const char *format, ...)** 从 stdin 读取格式化输入。





### 声明

以下是 scanf() 函数的声明。

```c
int scanf(const char *format, ...)
```

### 参数

- **format** -- 这是 C 字符串，包含以下一项或多项：

*空白字符、非空白字符和格式说明符。格式说明符将类似于 [= % [*] [width] [modifiers] type=]，如下所述：*

| 参数 | 描述 |
|---|---|
| * | 这是一个可选的起始星号，表示数据将从流中读取但被忽略，即它不会存储在相应的参数中。 |
| width | 指定当前读取操作中要读取的最大字符数。 |
| modifiers | 指定与 int（对于 d、i 和 n 的情况）、unsigned int（对于 o、u 和 x 的情况）或 float（对于 e、f 和 g 的情况）不同的大小，用于相应附加参数所指向的数据：h：short int（对于 d、i 和 n），或 unsigned short int（对于 o、u 和 x）；l：long int（对于 d、i 和 n），或 unsigned long int（对于 o、u 和 x），或 double（对于 e、f 和 g）；L：long double（对于 e、f 和 g） |
| type | 指定要读取的数据类型以及预期如何读取的字符。参见下表。 |

### fscanf 类型说明符：

| 类型 | 限定输入 | 参数类型 |
|---|---|---|
| c | 单个字符：读取下一个字符。如果指定了不同于 1 的宽度，该函数会读取 width 个字符，并将它们存储在作为参数传入的数组的连续位置中。末尾不会追加空字符。 | char * |
| d | 十进制整数：可选带有 + 或 - 符号的数字 | int * |
| e, E, f, g, G | 浮点数：包含小数点的十进制数，可选带有 + 或 - 符号，并可选后跟 e 或 E 字符和一个十进制数。两个有效条目的示例是 -732.103 和 7.12e4 | float * |
| o | 八进制整数： | int * |
| s | 字符串。这将读取后续字符，直到遇到空白字符为止（空白字符被视为空白、换行和 | char * |
|  | 制表符）。 |  |
| u | 无符号十进制整数。 | unsigned int * |
| x, X | 十六进制整数 | int * |

- **附加参数** -- 根据格式字符串，该函数可能期望一系列附加参数，每个参数包含一个要插入的值，以替代 format 参数中指定的每个 % 标记（如果有）。这些参数的数量应与期望值的 % 标记数量相同。

### 返回值

如果成功，则返回写入的字符总数；否则返回负数。

### 示例

以下示例展示了 scanf() 函数的用法。

```c
#include <stdio.h>

int main()
{
    char str1[20], str2[30];

    printf("Enter name: ");
    scanf("%s", &str1);
printf("Enter your website name: ");
scanf("%s", &str2);

printf("Entered Name: %s\n", str1);
printf("Entered Website:%s", str2);

return(0);
}
```

让我们编译并运行上述程序，它将在交互模式下产生以下结果：

```text
Enter name: admin
Enter your website name: www.tutorialspoint.com

Entered Name: admin
Entered Website: www.tutorialspoint.com
```

## int sscanf(const char *str, const char *format, ...)

### 描述

C 库函数 **int sscanf(const char *str, const char *format, ...)** 从字符串中读取格式化输入。

### 声明

以下是 sscanf() 函数的声明。

```c
int sscanf(const char *str, const char *format, ...)
```

### 参数

- **str** -- 这是 C 字符串，函数将其作为源来处理以检索数据。
- **format** -- 这是 C 字符串，包含以下一项或多项：*空白字符、非空白字符和格式说明符*

格式说明符遵循以下原型：`[=%[*][width][modifiers]type=]`

| 参数 | 描述 |
| --- | --- |
| * | 这是一个可选的起始星号，表示数据将从流中读取但被忽略，即它不会存储在相应的参数中。 |
| width | 指定当前读取操作中要读取的最大字符数。 |
| modifiers | 指定与 int（对于 d、i 和 n 的情况）、unsigned int（对于 o、u 和 x 的情况）或 float（对于 e、f 和 g 的情况）不同的大小，用于相应附加参数所指向的数据：h：short int（对于 d、i 和 n），或 unsigned short int（对于 o、u 和 x）；l：long int（对于 d、i 和 n），或 unsigned long int（对于 o、u 和 x），或 double（对于 e、f 和 g）；L：long double（对于 e、f 和 g） |
| type | 指定要读取的数据类型以及预期如何读取的字符。参见下表。 |

### fscanf 类型说明符：

| 类型 | 限定输入 | 参数类型 |
|---|---|---|
| c | 单个字符：读取下一个字符。如果指定了不同于 1 的宽度，该函数会读取 width 个字符，并将它们存储在作为参数传入的数组的连续位置中。末尾不会追加空字符。 | char * |
| d | 十进制整数：可选带有 + 或 - 符号的数字 | int * |
| e, E, f, g, G | 浮点数：包含小数点的十进制数，可选带有 + 或 - 符号，并可选后跟 e 或 E 字符和一个十进制数。两个有效条目的示例是 -732.103 和 7.12e4 | float * |
| o | 八进制整数： | int * |
| s | 字符串。这将读取后续字符，直到遇到空白字符为止（空白字符被视为空白、换行和 | char * |
|  | 制表符）。 |  |
| u | 无符号十进制整数。 | unsigned int * |
| x, X | 十六进制整数 | int * |

- **其他参数** -- 此函数期望一系列指针作为附加参数，每个指针按相同顺序指向格式字符串中其对应 % 标记所指定类型的对象。

对于格式字符串中每个检索数据的格式说明符，都应指定一个附加参数。如果要将 sscanf 操作的结果存储到普通变量中，应在其标识符前加上引用运算符，即 & 符号，例如：int n; sscanf (str,"%6d",&n);

### 返回值

成功时，该函数返回已填充的变量数。如果在成功读取任何数据之前发生输入失败，则返回 EOF。

### 示例

以下示例展示了 sscanf() 函数的用法。

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int day, year;
    char weekday[20], month[20], dtm[100];

    strcpy( dtm, "Saturday March 25 1989" );
    sscanf( dtm, "%s %s %d %d", weekday, month, &day, &year );

    printf("%%s %%d, %%d = %%s\n", month, day, year, weekday );

    return(0);
}
```

让我们编译并运行上述程序，它将产生以下结果：

March 25, 1989 = Saturday

## int fgetc(FILE *stream)

### 描述

C 库函数 int fgetc(FILE *stream) 从指定流中获取下一个字符（一个无符号字符），并推进该流的位置指示符。

### 声明

以下是 fgetc() 函数的声明。

```c
int fgetc(FILE *stream)
```

### 参数

- **stream** -- 这是指向 FILE 对象的指针，该对象标识要在其上执行操作的流。

### 返回值

该函数返回读取的字符（作为 unsigned char 转换为 int），或者在文件结束或出错时返回 EOF。

### 示例

以下示例展示了 fgetc() 函数的用法。

```c
#include <stdio.h>

int main ()
{
    FILE *fp;
    int c;
    int n = 0;
    fp = fopen("file.txt","r");
    if(fp == NULL)
    {
        perror("Error in opening file");
        return(-1);
    }
    do
    {
```




```c
c = fgetc(fp);
if( feof(fp) )
{
    break ;
}
printf("%c", c);
}while(1);

fclose(fp);
return(0);
}
```

假设我们有一个文本文件 file.txt，其内容如下。该文件将用作示例程序的输入：

```
We are in 2012
```

现在，让我们编译并运行上述程序，它将产生以下结果：

```
We are in 2012
```

## `char *fgets(char *str, int n, FILE *stream)`

### 描述

C 库函数 `char *fgets(char *str, int n, FILE *stream)` 从指定流中读取一行，并将其存储到 str 指向的字符串中。当读取到 (n-1) 个字符、读取到换行符或到达文件末尾时（以先发生者为准），该函数将停止。

### 声明

以下是 fgets() 函数的声明。

```
char *fgets(char *str, int n, FILE *stream)
```

### 参数

- str -- 这是指向字符数组的指针，读取的字符串存储在该数组中。
- n -- 这是要读取的最大字符数（包括最后的空字符）。通常使用作为 str 传递的数组长度。
- stream -- 这是指向 FILE 对象的指针，该对象标识要从中读取字符的流。

### 返回值

成功时，该函数返回相同的 str 参数。如果遇到文件末尾且未读取任何字符，则 str 的内容保持不变，并返回空指针。

如果发生错误，则返回空指针。

### 示例

以下示例展示了 fgets() 函数的用法。

```
#include <stdio.h>

int main()
{
    FILE *fp;
    char str[60];

    /* opening file for reading */
    fp = fopen("file.txt" , "r");
    if(fp == NULL) {
        perror("Error opening file");
        return(-1);
    }
    if( fgets (str, 60, fp)!=NULL ) {
        /* writing content to stdout */
        puts(str);
    }

    fclose(fp);

    return(0);
}
```

假设我们有一个文本文件 file.txt，其内容如下。该文件将用作示例程序的输入：

```
We are in 2012
```

现在，让我们编译并运行上述程序，它将产生以下结果：

```
We are in 2012
```

## `int fputc(int char, FILE *stream)`

### 描述

C 库函数 `int fputc(int char, FILE *stream)` 将参数 **char** 指定的字符（一个无符号字符）写入指定流，并推进流的当前位置指示器。

### 声明

以下是 fputc() 函数的声明。

```
int fputc(int char, FILE *stream)
```

### 参数

- **char** -- 这是要写入的字符。以 int 提升形式传递。
- **stream** -- 这是指向 FILE 对象的指针，该对象标识要写入字符的流。

### 返回值

如果没有错误，则返回已写入的相同字符。如果发生错误，则返回 EOF，并设置错误指示器。

### 示例

以下示例展示了 fputc() 函数的用法。

```
#include <stdio.h>

int main ()
{
    FILE *fp;
    int ch;

    fp = fopen("file.txt", "w+");
    for( ch = 33 ; ch <= 100; ch++ )
    {
        fputc(ch, fp);
    }
    fclose(fp);
    return(0);
}
```

让我们编译并运行上述程序，它将在当前目录中创建一个文件 file.txt，其内容如下：

```
!"#$%&'()*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ[\]^_`abcd
```

现在让我们使用以下程序查看上述文件的内容：

```
#include <stdio.h>

int main ()
{
    FILE *fp;
    int c;

    fp = fopen("file.txt","r");
    while(1)
    {
        c = fgetc(fp);
        if( feof(fp) )
        {
            break ;
        }
        printf("%c", c);
    }
    fclose(fp);
    return(0);
}
```

## `int fputs(const char *str, FILE *stream)`

### 描述

C 库函数 `int fputs(const char *str, FILE *stream)` 将字符串写入指定流，直到但不包括空字符。

### 声明

以下是 fputs() 函数的声明。

```
int fputs(const char *str, FILE *stream)
```

### 参数

- str -- 这是包含要写入的以空字符结尾的字符序列的数组。
- stream -- 这是指向 FILE 对象的指针，该对象标识要写入字符串的流。

### 返回值

该函数返回非负值，否则在出错时返回 EOF。

### 示例

以下示例展示了 fputs() 函数的用法。

```
#include <stdio.h>

int main ()
{
    FILE *fp;

    fp = fopen("file.txt", "w+");

    fputs("This is c programming.", fp);
    fputs("This is a system programming language.", fp);

    fclose(fp);

    return(0);
}
```

让我们编译并运行上述程序，这将创建一个文件 file.txt，其内容如下：

```
This is c programming.This is a system programming language.
```

现在让我们使用以下程序查看上述文件的内容：

```
#include <stdio.h>

int main ()
{
    FILE *fp;
    int c;

    fp = fopen("file.txt","r");
    while(1)
    {
        c = fgetc(fp);
        if( feof(fp) )
        {
            break ;
        }
        printf("%c", c);
    }
    fclose(fp);
    return(0);
}
```

## `int getc(FILE *stream)`

### 描述

C 库函数 `int getc(FILE *stream)` 从指定流中获取下一个字符（一个无符号字符），并推进流的当前位置指示器。

### 声明

以下是 getc() 函数的声明。

```
int getc(FILE *stream)
```

### 参数

- stream -- 这是指向 FILE 对象的指针，该对象标识要在其上执行操作的流。

### 返回值

该函数返回读取的字符（以无符号字符转换为 int），或在文件末尾或出错时返回 EOF。

### 示例

以下示例展示了 getc() 函数的用法。

```
#include<stdio.h>

int main()
{
    char c;

    printf("Enter character: ");
    c = getc(stdin);
    printf("Character entered: ");
    putc(c, stdout);

    return(0);
}
```

让我们编译并运行上述程序，它将产生以下结果：

```
Enter character: a
Character entered: a
```

## `int getchar(void)`

### 描述

C 库函数 `int getchar(void)` 从 stdin 获取一个字符（一个无符号字符）。这等效于以 stdin 作为参数的 getc。

### 声明

以下是 getchar() 函数的声明。

```
int getchar(void)
```

### 参数

- 无

### 返回值

该函数返回读取的字符（以无符号字符转换为 int），或在文件末尾或出错时返回 EOF。

### 示例

以下示例展示了 getchar() 函数的用法。

```
#include <stdio.h>

int main ()
{
    char c;

    printf("Enter character: ");
    c = getchar();

    printf("Character entered: ");
    putchar(c);

    return(0);
}
```

让我们编译并运行上述程序，它将产生以下结果：

```
Enter character: a
Character entered: a
```

## `char *gets(char *str)`

### 描述

C 库函数 `char *gets(char *str)` 从 stdin 读取一行，并将其存储到 str 指向的字符串中。当读取到换行符或到达文件末尾时（以先发生者为准），该函数将停止。

### 声明

以下是 gets() 函数的声明。

```
char *gets(char *str)
```

### 参数

- str -- 这是指向字符数组的指针，C 字符串存储在该数组中。

### 返回值

成功时该函数返回 str；出错时或到达文件末尾且未读取任何字符时，返回 NULL。

### 示例

以下示例展示了 gets() 函数的用法。

```
#include <stdio.h>

int main()
{
    char str[50];

    printf("Enter a string : ");
    gets(str);

    printf("You entered: %s", str);

    return(0);
}
```

让我们编译并运行上述程序，它将产生以下结果：

```
Enter a string : tutorialspoint.com
You entered: tutorialspoint.com
```

## `int putc(int char, FILE *stream)`

### 描述

C 库函数 `int putc(int char, FILE *stream)` 将参数 char 指定的字符（一个无符号字符）写入指定流，并推进流的当前位置指示器。

### 声明

以下是 putc() 函数的声明。

```
int putc(int char, FILE *stream)
```

### 参数

- char -- 这是要写入的字符。该字符以 int 提升形式传递。
- stream -- 这是指向 FILE 对象的指针，该对象标识要写入字符的流。

### 返回值

该函数返回写入的字符（以无符号字符转换为 int），或在出错时返回 EOF。

### 示例

以下示例展示了 putc() 函数的用法。

```



```c
#include <stdio.h>

int main ()
{
    FILE *fp;
    int ch;

    fp = fopen("file.txt", "w");
    for( ch = 33 ; ch <= 100; ch++ )
    {
        putc(ch, fp);
    }
    fclose(fp);

    return(0);
}
```

让我们编译并运行上述程序，它将在当前目录中创建一个文件 **file.txt**，其内容如下：

```text
!"#$%&'()*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ[\]^_`abcd
```

现在让我们使用以下程序查看上述文件的内容：

```c
#include <stdio.h>

int main ()
{
    FILE *fp;
    int c;

    fp = fopen("file.txt","r");
    while(1)
    {
        c = fgetc(fp);
        if( feof(fp) )
        {
            break;
        }
        printf("%c", c);
    }
    fclose(fp);
    return(0);
}
```

## int putchar(int char)

### 描述

C 库函数 int putchar(int char) 将参数 char 指定的字符（一个无符号字符）写入 stdout。

### 声明

以下是 putchar() 函数的声明。

```c
int putchar(int char)
```

### 参数

- **char** -- 这是要写入的字符。它作为 int 提升传递。

### 返回值

该函数返回写入的字符（将 unsigned char 转换为 int），出错时返回 EOF。

### 示例

以下示例展示了 putchar() 函数的用法。

```c
#include <stdio.h>

int main ()
{
    char ch;

    for(ch = 'A' ; ch <= 'Z' ; ch++) {
        putchar(ch);
    }
    return(0);
}
```

让我们编译并运行上述程序，将产生以下结果：

```text
ABCDEFGHIJKLMNOPQRSTUVWXYZ
```

## int puts(const char *str)

### 描述

C 库函数 **int puts(const char *str)** 将字符串写入 stdout，直到但不包括空字符。输出中会追加一个换行符。

### 声明

以下是 puts() 函数的声明。

```c
int puts(const char *str)
```

### 参数

- **str** -- 这是要写入的 C 字符串。

### 返回值

如果成功，返回非负值。出错时，函数返回 EOF。

### 示例

以下示例展示了 puts() 函数的用法。

```c
#include <stdio.h>
#include <string.h>

int main()
{
    char str1[15];
    char str2[15];

    strcpy(str1, "tutorialspoint");
    strcpy(str2, "compileonline");

    puts(str1);
    puts(str2);
    return(0);
}
```

让我们编译并运行上述程序，以产生以下结果：

```text
tutorialspoint
compileonline
```

## int ungetc(int char, FILE *stream)

### 描述

C 库函数 int ungetc(int char, FILE *stream) 将字符 char（一个无符号字符）推回到指定的流中，以便下一次读取操作可以使用它。

### 声明

以下是 ungetc() 函数的声明。

```c
int ungetc(int char, FILE *stream)
```

### 参数

- **char** -- 这是要放回的字符。它作为 int 提升传递。
- **stream** -- 这是指向标识输入流的 FILE 对象的指针。

### 返回值

如果成功，它返回被推回的字符；否则返回 EOF，且流保持不变。

### 示例

以下示例展示了 ungetc() 函数的用法。

```c
#include <stdio.h>

int main ()
{
    FILE *fp;
    int c;
    char buffer [256];

    fp = fopen("file.txt", "r");
    if( fp == NULL )
    {
        perror("Error in opening file");
        return(-1);
    }
    while(!feof(fp))
    {
        c = getc (fp);
        /* replace ! with + */
        if( c == '!' )
        {
            ungetc ('+', fp);
        }
        else
        {
            ungetc(c, fp);
        }
        fgets(buffer, 255, fp);
        fputs(buffer, stdout);
    }
    return(0);
}
```

假设我们有一个文本文件 file.txt，其中包含以下数据。该文件将用作我们示例程序的输入：

```text
this is tutorials point
!c standard library
!library functions and macros
```

现在让我们编译并运行上述程序，将产生以下结果：

```text
this is tutorials point
+c standard library
+library functions and macros
```

## void perror(const char *str)

### 描述

C 库函数 void perror(const char *str) 向 stderr 打印描述性错误消息。首先打印字符串 str，随后是一个冒号，然后是一个空格。

### 声明

以下是 perror() 函数的声明。

```c
void perror(const char *str)
```

### 参数

- **str** -- 这是包含自定义消息的 C 字符串，该消息将在错误消息本身之前打印。

### 返回值

该函数不返回任何值。

### 示例

以下示例展示了 perror() 函数的用法。

```c
#include <stdio.h>

int main ()
{
    FILE *fp;

    /* first rename if there is any file */
    rename("file.txt", "newfile.txt");

    /* now let's try to open same file */
    fp = fopen("file.txt", "r");
    if( fp == NULL ) {
        perror("Error: ");
        return(-1);
    }
    fclose(fp);

    return(0);
}
```

让我们编译并运行上述程序，将产生以下结果，因为我们试图打开一个不存在的文件：

```text
Error: : No such file or directory
```

## 简介

**stdlib.h** 头文件定义了四种变量类型、若干宏以及用于执行通用功能的各种函数。

## 库变量

以下是头文件 stdlib.h 中定义的变量类型：

| 序号 | 变量与描述 |
|---|---|
| 1 | **size_t**<br>这是无符号整型，是 **sizeof** 关键字的结果。 |
| 2 | **wchar_t**<br>这是一种整数类型，其大小等于一个**宽**字符常量的大小。 |
| 3 | **div_t**<br>这是 **div** 函数返回的结构。 |
| 4 | **ldiv_t**<br>这是 **ldiv** 函数返回的结构。 |

## 库宏

以下是头文件 stdlib.h 中定义的宏：

| 序号 | 宏与描述 |
|---|---|
| 1 | **NULL**<br>该宏是空指针常量的值。 |
| 2 | **EXIT_FAILURE**<br>这是 exit 函数在失败时返回的值。 |
| 3 | **EXIT_SUCCESS**<br>这是 exit 函数在成功时返回的值。 |
| 4 | **RAND_MAX**<br>该宏是 **rand** 函数返回的最大值。 |
| 5 | **MB_CUR_MAX**<br>该宏是多字节字符集中的最大字节数，不能大于 MB_LEN_MAX。 |

## 库函数

以下是头文件 stdlib.h 中定义的函数：

| 序号 | 函数与描述 |
|---|---|
| 1 | `double atof(const char *str)`<br>将参数 *str* 所指向的字符串转换为浮点数（double 类型）。 |
| 2 | `int atoi(const char *str)`<br>将参数 *str* 所指向的字符串转换为整数（int 类型）。 |
| 3 | `long int atol(const char *str)`<br>将参数 *str* 所指向的字符串转换为长整数（long int 类型）。 |
| 4 | `double strtod(const char *str, char **endptr)`<br>将参数 *str* 所指向的字符串转换为浮点数（double 类型）。 |
| 5 | `long int strtol(const char *str, char **endptr, int base)`<br>将参数 *str* 所指向的字符串转换为长整数（long int 类型）。 |
| 6 | `unsigned long int strtoul(const char *str, char **endptr, int base)`<br>将参数 str 所指向的字符串转换为无符号长整数（unsigned long int 类型）。 |
| 7 | `void *calloc(size_t nitems, size_t size)`<br>分配请求的内存并返回指向它的指针。 |
| 8 | `void free(void *ptr)`<br>释放先前通过调用 calloc、malloc 或 realloc 分配的内存。 |
| 9 | `void *malloc(size_t size)`<br>分配请求的内存并返回指向它的指针。 |
| 10 | `void *realloc(void *ptr, size_t size)`<br>尝试调整 ptr 所指向的内存块的大小，该内存块先前通过调用 malloc 或 calloc 分配。 |
| 11 | `void abort(void)`<br>导致程序异常终止。 |
| 12 | `int atexit(void (*func)(void))`<br>使指定函数 func 在程序正常终止时被调用。 |
| 13 | `void exit(int status)`<br>使程序正常终止。 |
| 14 | `char *getenv(const char *name)`<br>搜索 name 所指向的环境字符串，并返回与该字符串关联的值。 |
| 15 | `int system(const char *string)`<br>由 string 指定的命令被传递给宿主环境，以由命令处理器执行。 |




| 序号 | 函数原型及说明 |
|---|---|
| 16 | `void *bsearch(const void *key, const void *base, size_t nitems, size_t size, int (*compar)(const void *, const void *))`<br><br>执行二分查找。 |
| 17 | `void qsort(void *base, size_t nitems, size_t size, int (*compar)(const void *, const void*))`<br><br>对数组进行排序。 |
| 18 | `int abs(int x)`<br><br>返回 x 的绝对值。 |
| 19 | `div_t div(int numer, int denom)`<br><br>将 numer（分子）除以 denom（分母）。 |
| 20 | `long int labs(long int x)`<br><br>返回 x 的绝对值。 |
| 21 | `ldiv_t ldiv(long int numer, long int denom)`<br><br>将 numer（分子）除以 denom（分母）。 |
| 22 | `int rand(void)`<br><br>返回 0 到 RAND_MAX 范围内的伪随机数。 |
| 23 | `void srand(unsigned int seed)`<br><br>此函数为 rand 函数使用的随机数生成器设置种子。 |
| 24 | `int mblen(const char *str, size_t n)`<br><br>返回参数 str 所指向的多字节字符的长度。 |
| 25 | `size_t mbstowcs(wchar_t *pwcs, const char *str, size_t n)`<br><br>将参数 str 所指向的多字节字符字符串转换为 pwcs 所指向的数组。 |
| 26 | `int mbtowc(wchar_t *pwc, const char *str, size_t n)`<br><br>检查参数 *str* 所指向的多字节字符。 |
| 27 | `size_t wcstombs(char *str, const wchar_t *pwcs, size_t n)`<br><br>将 *pwcs* 数组中存储的代码转换为多字节字符并存储在字符串 *str* 中。 |
| 28 | `int wctomb(char *str, wchar_t wchar)`<br><br>检查与参数 *wchar* 给出的多字节字符相对应的代码。 |

## double atof(const char *str)

### Description

C 库函数 **double atof(const char *str)** 将字符串参数 **str** 转换为浮点数（类型为 double）。

### Declaration

以下是 atof() 函数的声明。

```c
double atof(const char *str)
```

### Parameters

- **str** -- 这是具有浮点数表示的字符串。

### Return Value

此函数将转换后的浮点数作为 double 值返回。如果无法执行有效转换，则返回零（0.0）。

### Example

以下示例展示了 atof() 函数的用法。

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main()
{
    float val;
    char str[20];

    strcpy(str, "98993489");
    val = atof(str);
    printf("String value = %s, Float value = %f\n", str, val);

    strcpy(str, "tutorialspoint.com");
    val = atof(str);
    printf("String value = %s, Float value = %f\n", str, val);

    return(0);
}
```

编译并运行上述程序，将产生以下结果：

```
String value = 98993489, Float value = 98993488.000000
String value = tutorialspoint.com, Float value = 0.000000
```

## int atoi(const char *str)

### Description

C 库函数 int atoi(const char *str) 将字符串参数 str 转换为整数（类型为 int）。

### Declaration

以下是 atoi() 函数的声明。

```c
int atoi(const char *str)
```

### Parameters

- str -- 这是整数的字符表示。

### Return Value

此函数将转换后的整数作为 int 值返回。如果无法执行有效转换，则返回零。

### Example

以下示例展示了 atoi() 函数的用法。

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main()
{
    int val;
    char str[20];
    strcpy(str, "98993489");
    val = atoi(str);
    printf("String value = %s, Int value = %d\n", str, val);
    strcpy(str, "tutorialspoint.com");
    val = atoi(str);
    printf("String value = %s, Int value = %d\n", str, val);
    return(0);
}
```

编译并运行上述程序，将产生以下结果：

```
String value = 98993489, Int value = 98993489
String value = tutorialspoint.com, Int value = 0
```

## long int atol(const char *str)

### Description

C 库函数 long int atol(const char *str) 将字符串参数 str 转换为长整数（类型为 long int）。

### Declaration

以下是 atol() 函数的声明。

```c
long int atol(const char *str)
```

### Parameters

- **str** -- 这是包含整数表示的字符串。

### Return Value

此函数将转换后的整数作为 long int 返回。如果无法执行有效转换，则返回零。

### Example

以下示例展示了 atol() 函数的用法。

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main()
{
    long val;
    char str[20];

    strcpy(str, "98993489");
    val = atol(str);
    printf("String value = %s, Long value = %ld\n", str, val);

    strcpy(str, "tutorialspoint.com");
    val = atol(str);
    printf("String value = %s, Long value = %ld\n", str, val);

    return(0);
}
```

编译并运行上述程序，将产生以下结果：

```
String value = 98993489, Long value = 98993489
String value = tutorialspoint.com, Long value = 0
```

## double strtod(const char *str, char **endptr)

### Description

C 库函数 double strtod(const char *str, char **endptr) 将参数 str 所指向的字符串转换为浮点数（类型为 double）。如果 endptr 不为 NULL，则转换后最后一个字符之后的指针将存储在 endptr 引用的位置。

### Declaration

以下是 strtod() 函数的声明。

```c
double strtod(const char *str, char **endptr)
```

### Parameters

- **str** -- 这是包含浮点数表示的字符串。
- **endptr** -- 这是对已分配的 char* 类型对象的引用，其值由函数设置为 str 中数值之后下一个字符。

### Return Value

此函数将转换后的浮点数作为 double 值返回，否则返回零值（0.0）。

### Example

以下示例展示了 strtod() 函数的用法。

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    char str[30] = "20.30300 This is test";
    char *ptr;
    double ret;

    ret = strtod(str, &ptr);
    printf("The number(double) is %lf\n", ret);
    printf("String part is |%s|", ptr);

    return(0);
}
```

编译并运行上述程序，将产生以下结果：

```
The number(double) is 20.303000
String part is | This is test|
```

## long int strtol(const char *str, char **endptr, int base)

### Description

C 库函数 long int strtol(const char *str, char **endptr, int base) 根据给定的 base 将 str 中字符串的初始部分转换为 long int 值，base 必须在 2 到 36 之间，或为特殊值 0。

### Declaration

以下是 strtol() 函数的声明。

```c
long int strtol(const char *str, char **endptr, int base)
```

### Parameters

- **str** -- 这是包含整数表示的字符串。
- **endptr** -- 这是对 char* 类型对象的引用，其值由函数设置为 str 中数值之后下一个字符。
- **base** -- 这是基数，必须在 2 到 36 之间，或为特殊值 0。

### Return Value

此函数将转换后的整数作为 long int 值返回，否则返回零值。

### Example

以下示例展示了 strtol() 函数的用法。

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    char str[30] = "2030300 This is test";
    char *ptr;
    long ret;

    ret = strtol(str, &ptr, 10);
    printf("The number(unsigned long integer) is %ld\n", ret);
    printf("String part is |%s|", ptr);

    return(0);
}
```

编译并运行上述程序，将产生以下结果：

```
The number(unsigned long integer) is 2030300
String part is | This is test|
```




## unsigned long int strtoul(const char *str, char **endptr, int base)

### 描述

C 库函数 unsigned long int strtoul(const char *str, char **endptr, int base) 将 str 所指向的字符串的初始部分，根据给定的基数转换为一个 unsigned long int（无符号长整型）值。基数必须在 2 到 36（包含）之间，或者是特殊值 0。

### 声明

下面是 strtoul() 函数的声明。

```
unsigned long int strtoul(const char *str, char **endptr, int base)
```

### 参数

- **str** -- 这是包含无符号整数表示形式的字符串。
- **endptr** -- 这是对 char* 类型对象的引用，其值由函数设置为 str 中数值之后的下一个字符。
- **base** -- 这是基数，必须在 2 到 36（包含）之间，或者是特殊值 0。

### 返回值

该函数将转换后的整数作为 long int 值返回。如果无法执行有效的转换，则返回零值。

### 示例

下面的示例演示了 strtoul() 函数的使用。

```
#include <stdio.h>
#include <stdlib.h>

int main()
{
    char str[30] = "2030300 This is test";
    char *ptr;
    long ret;

    ret = strtoul(str, &ptr, 10);
    printf("The number(unsigned long integer) is %lu\n", ret);
    printf("String part is |%s|", ptr);

    return(0);
}
```

让我们编译并运行上述程序，将产生以下结果：

```
The number(unsigned long integer) is 2030300
String part is | This is test|
```

## void *calloc(size_t nitems, size_t size)

### 描述

C 库函数 void *calloc(size_t nitems, size_t size) 分配所需的内存并返回指向它的指针。malloc 和 calloc 之间的区别在于，malloc 不会将内存设置为零，而 calloc 会将分配的内存设置为零。

### 声明

下面是 calloc() 函数的声明。

```
void *calloc(size_t nitems, size_t size)
```

### 参数

- nitems -- 这是要分配的元素个数。
- size -- 这是元素的大小。

### 返回值

该函数返回指向已分配内存的指针，如果请求失败，则返回 NULL。

### 示例

下面的示例演示了 calloc() 函数的使用。

```
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int i, n;
    int *a;

    printf("Number of elements to be entered:");
    scanf("%d",&n);

    a = (int*)calloc(n, sizeof(int));
    printf("Enter %d numbers:\n",n);
    for( i=0 ; i < n ; i++ )
    {
        scanf("%d",&a[i]);
    }

    printf("The numbers entered are: ");
    for( i=0 ; i < n ; i++ ) {
        printf("%d ",a[i]);
    }

    return(0);
}
```

让我们编译并运行上述程序，将产生以下结果：

```
Number of elements to be entered:3

Enter 3 numbers:

22

55

14

The numbers entered are: 22 55 14
```

## void free(void *ptr)

### 描述

C 库函数 void free(void *ptr) 释放之前通过调用 calloc、malloc 或 realloc 分配的内存。

### 声明

下面是 free() 函数的声明。

```
void free(void *ptr)
```

### 参数

- ptr -- 这是指向先前由 malloc、calloc 或 realloc 分配的内存块的指针，该内存块将被释放。如果传入空指针作为参数，则不执行任何操作。

### 返回值

该函数不返回任何值。

### 示例

下面的示例演示了 free() 函数的使用。

```
#include <stdio.h>
#include <stdlib.h>

int main()
{
    char *str;

    /* Initial memory allocation */
    str = (char *) malloc(15);
    strcpy(str, "tutorialspoint");
    printf("String = %s,  Address = %u\n", str, str);

    /* Reallocating memory */
    str = (char *) realloc(str, 25);
    strcat(str, ".com");
    printf("String = %s,  Address = %u\n", str, str);

    /* Deallocate allocated memory */
    free(str);

    return(0);
}
```

让我们编译并运行上述程序，将产生以下结果：

```
String = tutorialspoint, Address = 355090448
String = tutorialspoint.com, Address = 355090448
```

## void *malloc(size_t size)

### 描述

C 库函数 void *malloc(size_t size) 分配所需的内存并返回指向它的指针。

### 声明

下面是 malloc() 函数的声明。

```c
void *malloc(size_t size)
```

### 参数

- **size** -- 这是内存块的大小，以字节为单位。

### 返回值

该函数返回指向已分配内存的指针，如果请求失败，则返回 NULL。

### 示例

下面的示例演示了 malloc() 函数的使用。

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    char *str;

    /* Initial memory allocation */
    str = (char *) malloc(15);
    strcpy(str, "tutorialspoint");
    printf("String = %s,  Address = %u\n", str, str);

    /* Reallocating memory */
    str = (char *) realloc(str, 25);
    strcat(str, ".com");
    printf("String = %s,  Address = %u\n", str, str);

    free(str);

    return(0);
}
```

让我们编译并运行上述程序，将产生以下结果：

```
String = tutorialspoint, Address = 355090448
String = tutorialspoint.com, Address = 355090448
```

## void *realloc(void *ptr, size_t size)

### 描述

C 库函数 void *realloc(void *ptr, size_t size) 尝试调整由 ptr 指向的内存块的大小，该内存块此前通过调用 malloc 或 calloc 分配。

### 声明

下面是 realloc() 函数的声明。

```
void *realloc(void *ptr, size_t size)
```

### 参数

- ptr -- 这是指向先前由 malloc、calloc 或 realloc 分配的内存块的指针，将被重新分配。如果它为 NULL，则分配一个新内存块，并由函数返回指向它的指针。
- size -- 这是内存块的新大小，以字节为单位。如果它为 0 且 ptr 指向一个现有的内存块，则 ptr 所指向的内存块将被释放，并返回一个 NULL 指针。

### 返回值

该函数返回指向新分配内存的指针，如果请求失败，则返回 NULL。

### 示例

下面的示例演示了 realloc() 函数的使用。

```
#include <stdio.h>
#include <stdlib.h>

int main()
{
    char *str;

    /* Initial memory allocation */
    str = (char *) malloc(15);
    strcpy(str, "tutorialspoint");

    printf("String = %s,  Address = %u\n", str, str);

    /* Reallocating memory */
    str = (char *) realloc(str, 25);
    strcat(str, ".com");
    printf("String = %s,  Address = %u\n", str, str);

    free(str);

    return(0);
}
```

让我们编译并运行上述程序，将产生以下结果：

```
String = tutorialspoint, Address = 355090448
String = tutorialspoint.com, Address = 355090448
```

## void abort(void)

### 描述

C 库函数 void abort(void) 中止程序的执行，并直接从调用处退出。

### 声明

下面是 abort() 函数的声明。

```
void abort(void)
```

### 参数

- 无

### 返回值

该函数不返回任何值。

### 示例

下面的示例演示了 abort() 函数的使用。

```
#include <stdio.h>
#include <stdlib.h>

int main ()
{
  FILE *fp;

  printf("Going to open nofile.txt\n");
  fp = fopen( "nofile.txt","r" );
  if(fp == NULL)
  {
    printf("Going to abort the program\n");
    abort();
  }
  printf("Going to close nofile.txt\n");
  fclose(fp);

  return(0);
}
```

让我们编译并运行上述程序，当它尝试打开不存在的 **nofile.txt** 文件时，将产生以下结果：

```
Going to open nofile.txt
Going to abort the program
Aborted (core dumped)
```

## int atexit(void (*func)(void))

### 描述

C 库函数 **int atexit(void (*func)(void))** 使指定的函数 **func** 在程序终止时被调用。你可以在任何地方注册终止函数，但它会在程序终止时被调用。

### 声明

下面是 atexit() 函数的声明。

```c
int atexit(void (*func)(void))
```

### 参数

- **func** -- 这是在程序终止时要调用的函数。

### 返回值




此函数在成功注册时返回零值，否则在失败时返回非零值。

### 示例
以下示例展示了 atexit() 函数的用法。

```c
#include <stdio.h>
#include <stdlib.h>

void functionA ()
{
    printf("This is functionA\n");
}

int main ()
{
    /* register the termination function */
    atexit(functionA );

    printf("Starting  main program...\n");

    printf("Exiting main program...\n");

    return(0);
}
```

让我们编译并运行上述程序，将会产生以下结果：

```
Starting main program...
Exiting main program...
This is functionA
```

## void exit(int status)
### 描述
C 库函数 **void exit(int status)** 会立即终止调用进程。进程拥有的任何打开文件描述符都会被关闭，进程的任何子进程都将被进程 1、init 继承，并且向进程父进程发送 SIGCHLD 信号。

### 声明
以下是 exit() 函数的声明。

```c
void exit(int status)
```

### 参数
- **status** -- 这是返回给父进程的状态值。

### 返回值
此函数不返回任何值。

### 示例
以下示例展示了 exit() 函数的用法。

```c
#include <stdio.h>
#include <stdlib.h>

int main ()
{
    printf("Start of the program....\n");
    printf("Exiting the program....\n");
    exit(0);
    printf("End of the program....\n");
    return(0);
}
```

让我们编译并运行上述程序，将会产生以下结果：

```
Start of the program....
Exiting the program....
```

## char *getenv(const char *name)
### 描述
C 库函数 char *getenv(const char *name) 按名称搜索指向的环境字符串并返回该字符串关联的值。

### 声明
以下是 getenv() 函数的声明。

```c
char *getenv(const char *name)
```

### 参数
- name -- 这是包含所请求变量名称的 C 字符串。

### 返回值
此函数返回一个以空字符结尾的字符串，其中包含所请求环境变量的值，如果该环境变量不存在则返回 NULL。

### 示例
以下示例展示了 getenv() 函数的用法。

```c
#include <stdio.h>
#include <stdlib.h>

int main ()
{
    printf("PATH : %s\n", getenv("PATH"));
    printf("HOME : %s\n", getenv("HOME"));
    printf("ROOT : %s\n", getenv("ROOT"));

    return(0);
}
```

让我们编译并运行上述程序，将会产生以下结果：

```
PATH : /sbin:/usr/sbin:/bin:/usr/bin:/usr/local/bin
HOME : /
ROOT : (null)
```

## int system(const char *string)
### 描述
C 库函数 int system(const char *command) 将 command 指定的命令名称或程序名称传递给主机环境，由命令处理器执行，并在命令完成后返回。

### 声明
以下是 system() 函数的声明。

```c
int system(const char *command)
```

### 参数
- **command** -- 这是包含所请求变量名称的 C 字符串。

### 返回值
返回值在出错时为 -1，否则为命令的返回状态。

### 示例
以下示例展示了 system() 函数的用法，用于在 unix 机器上列出当前目录下的所有文件和目录。

```c
#include <stdio.h>
#include <string.h>

int main ()
{
    char command[50];

    strcpy( command, "ls -l" );
    system(command);

    return(0);
}
```

让我们编译并运行上述程序，将会在我的 unix 机器上产生以下结果：

```
drwxr-xr-x 2 apache apache 4096 Aug 22 07:25 hsperfdata_apache
drwxr-xr-x 2 railo railo 4096 Aug 21 18:48 hsperfdata_railo
rw------- 1 apache apache   8 Aug 21 18:48 mod_mono_dashboard_XXGLOBAL_1
rw------- 1 apache apache   8 Aug 21 18:48 mod_mono_dashboard_asp_2
srwx----- 1 apache apache   0 Aug 22 05:28 mod_mono_server_asp
rw------- 1 apache apache   0 Aug 22 05:28 mod_mono_server_asp_1280495620
srwx----- 1 apache apache   0 Aug 21 18:48 mod_mono_server_global
```

以下示例展示了 system() 函数的用法，用于在 windows 机器上列出当前目录下的所有文件和目录。

```c
#include <stdio.h>
#include <string.h>

int main ()
{
    char command[50];

    strcpy( command, "dir" );
    system(command);

    return(0);
}
```

让我们编译并运行上述程序，将会在我的 windows 机器上产生以下结果：

```
a.txt
amit.doc
sachin
saurav
file.c
```

## void *bsearch(const void *key, const void *base, size_t nitems, size_t size, int (*compar)(const void *, const void *))
### 描述
C 库函数 void *bsearch(const void *key, const void *base, size_t nitems, size_t size, int (*compar)(const void *, const void *)) 在由 base 指向的 nitems 个对象的数组中搜索与 key 指向的对象匹配的成员。数组中每个成员的大小由 size 指定。

数组的内容应根据 compar 引用的比较函数按升序排序。

### 声明
以下是 bsearch() 函数的声明。

```c
void *bsearch(const void *key, const void *base, size_t nitems, size_t size, int (*compar)(const void *, const void *))
```

### 参数
- **key** -- 这是指向用作搜索键的对象的指针，类型强制转换为 void*。
- **base** -- 这是指向执行搜索的数组第一个对象的指针，类型强制转换为 void*。
- **nitems** -- 这是由 base 指向的数组中的元素数量。
- **size** -- 这是数组中每个元素的字节大小。
- **compar** -- 这是比较两个元素的函数。

### 返回值
此函数返回数组中与搜索键匹配的条目的指针。如果未找到 key，则返回 NULL 指针。

### 示例
以下示例展示了 bsearch() 函数的用法。

```c
#include <stdio.h>
#include <stdlib.h>

int cmpfunc(const void * a, const void * b)
{
    return ( *(int*)a - *(int*)b );
}

int values[] = { 5, 20, 29, 32, 63 };

int main ()
{
    int *item;
    int key = 32;

    /* using bsearch() to find value 32 in the array */
    item = (int*) bsearch (&key, values, 5, sizeof (int), cmpfunc);
    if( item != NULL )
{
    printf("Found item = %d\n", *item);
}
else
{
    printf("Item = %d could not be found\n", *item);
}

return(0);
}
```

让我们编译并运行上述程序，将会产生以下结果：

```
Found item = 32
```

## void qsort(void *base, size_t nitems, size_t size, int (*compar)(const void *, const void *))
### 描述
C 库函数 void qsort(void *base, size_t nitems, size_t size, int (*compar)(const void *, const void *)) 对数组进行排序。

### 声明
以下是 qsort() 函数的声明。

```c
void qsort(void *base, size_t nitems, size_t size, int (*compar)(const void *, const void *));
```

### 参数
- **base** -- 这是指向要排序的数组第一个元素的指针。
- **nitems** -- 这是由 base 指向的数组中的元素数量。
- **size** -- 这是数组中每个元素的字节大小。
- **compar** -- 这是比较两个元素的函数。

### 返回值
此函数不返回任何值。

### 示例
以下示例展示了 qsort() 函数的用法。

```c
#include <stdio.h>
#include <stdlib.h>

int values[] = { 88, 56, 100, 2, 25 };

int cmpfunc (const void * a, const void * b)
{
    return ( *(int*)a - *(int*)b );
}

int main()
{
    int n;

    printf("Before sorting the list is: \n");
    for( n = 0 ; n < 5; n++ ) {
        printf("%d ", values[n]);
    }

    qsort(values, 5, sizeof(int), cmpfunc);

    printf("\nAfter sorting the list is: \n");
    for( n = 0 ; n < 5; n++ ) {
        printf("%d ", values[n]);
    }

    return(0);
}
```

让我们编译并运行上述程序，将会产生以下结果：

```
Before sorting the list is:
88 56 100 2 25
After sorting the list is:
2 25 56 88 100
```




## int abs(int x)

### 描述

C 库函数 **int abs(int x)** 返回 **int x** 的绝对值。

### 声明

下面是 abs() 函数的声明。

```
int abs(int x)
```

### 参数

- **x** -- 这是整数值。

### 返回值

该函数返回 x 的绝对值。

### 示例

下面的实例演示了 abs() 函数的用法。

```
#include <stdio.h>
#include <stdlib.h>

int main ()
{
    int a, b;

    a = abs(5);
    printf("value of a = %d\n", a);

    b = abs(-10);
    printf("value of b = %d\n", b);

    return(0);
}
```

让我们编译并运行上面的程序，这将产生以下结果：

```
value of a = 5
value of b = 10
```

## div_t div(int numer, int denom)

### 描述

C 库函数 div_t div(int numer, int denom) 用 numer（分子）除以 denom（分母）。

### 声明

下面是 div() 函数的声明。

```
div_t div(int numer, int denom)
```

### 参数

- numer -- 这是分子。
- denom -- 这是分母。

### 返回值

该函数返回定义在 <cstdlib> 中的结构中的值，该结构有两个成员。对于 div_t：int quot; int rem;

### 示例

下面的实例演示了 div() 函数的用法。

```
#include <stdio.h>
#include <stdlib.h>

int main()
{
    div_t output;

    output = div(27, 4);
    printf("Quotient part of (27/ 4) = %d\n", output.quot);
    printf("Remainder part of (27/4) = %d\n", output.rem);

    output = div(27, 3);
    printf("Quotient part of (27/ 3) = %d\n", output.quot);
    printf("Remainder part of (27/3) = %d\n", output.rem);

    return(0);
}
```

让我们编译并运行上面的程序，将产生以下结果：

```
Quotient part of (27/ 4) = 6
Remainder part of (27/4) = 3
Quotient part of (27/ 3) = 9
Remainder part of (27/3) = 0
```

## long int labs(long int x)

### 描述

C 库函数 **long int labs(long int x)** 返回 **x** 的绝对值。

### 声明

下面是 labs() 函数的声明。

```c
long int labs(long int x)
```

### 参数

- **x** -- 这是整数值。

### 返回值

该函数返回 **x** 的绝对值。

### 示例

下面的实例演示了 labs() 函数的用法。

```c
#include <stdio.h>
#include <stdlib.h>

int main ()
{
    long int a,b;

    a = labs(65987L);
    printf("Value of a = %ld\n", a);

    b = labs(-1005090L);
    printf("Value of b = %ld\n", b);

    return(0);
}
```

让我们编译并运行上面的程序，将产生以下结果：

```
Value of a = 65987
Value of b = 1005090
```

## ldiv_t ldiv(long int numer, long int denom)

### 描述

C 库函数 ldiv_t ldiv(long int numer, long int denom) 用 numer（分子）除以 denom（分母）。

### 声明

下面是 ldiv() 函数的声明。

```
ldiv_t ldiv(long int numer, long int denom)
```

### 参数

- numer -- 这是分子。
- denom -- 这是分母。

### 返回值

该函数返回定义在 <cstdlib> 中的结构中的值，该结构有两个成员。对于 ldiv_t：long quot; long rem;

### 示例

下面的实例演示了 ldiv() 函数的用法。

```
#include <stdio.h>
#include <stdlib.h>

int main ()
{
    ldiv_t output;

    output = ldiv(100000L, 30000L);

    printf("Quotient = %ld\n", output.quot);

    printf("Remainder = %ld\n", output.rem);

    return(0);
}
```

让我们编译并运行上面的程序，将产生以下结果：

```
Quotient = 3
Remainder = 10000
```

## int rand(void)

### 描述

C 库函数 **int rand(void)** 返回一个范围在 0 到 RAND_MAX 之间的伪随机数。

RAND_MAX 是一个常量，其默认值可能因实现而异，但保证至少为 32767。

### 声明

下面是 rand() 函数的声明。

```c
int rand(void)
```

### 参数

- NA

### 返回值

该函数返回一个介于 0 和 RAND_MAX 之间的整数值。

### 示例

下面的实例演示了 rand() 函数的用法。

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int i, n;
    time_t t;

    n = 5;

    /* Initializes random number generator */
    srand((unsigned) time(&t));

    /* Print 5 random numbers from 0 to 49 */
    for( i = 0 ; i < n ; i++ ) {
        printf("%d\n", rand() % 50);
    }

    return(0);
}
```

让我们编译并运行上面的程序，将产生以下结果：

```
38
45
29
29
47
```

## void srand(unsigned int seed)

### 描述

C 库函数 void srand(unsigned int seed) 为函数 rand 所使用的随机数生成器设定种子。

### 声明

下面是 srand() 函数的声明。

```
void srand(unsigned int seed)
```

### 参数

- seed -- 这是伪随机数生成器算法用作种子的整数值。

### 返回值

该函数不返回任何值。

### 示例

下面的实例演示了 srand() 函数的用法。

```
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

int main()
{
    int i, n;
    time_t t;
    
    n = 5;
    
    /* Initializes random number generator */
    srand((unsigned) time(&t));
    
    /* Print 5 random numbers from 0 to 50 */
    for( i = 0 ; i < n ; i++ ) {
        printf("%d\n", rand() % 50);
    }
    
    return(0);
}
```

让我们编译并运行上面的程序，将产生以下结果：

```
38
45
29
29
47
```

## int mblen(const char *str, size_t n)

### 描述

C 库函数 int mblen(const char *str, size_t n) 返回参数 str 所指向的多字节字符的长度。

### 声明

下面是 mblen() 函数的声明。

```
int mblen(const char *str, size_t n)
```

### 参数

- **str** -- 这是指向多字节字符第一个字节的指针。
- **n** -- 这是要检查字符长度的最大字节数。

### 返回值

如果识别到非空宽字符，mblen() 函数返回从 str 开始的多字节序列传递的字节数。如果识别到空宽字符，则返回 0。如果遇到无效的多字节序列或无法解析完整的多字节字符，则返回 -1。

### 示例

下面的实例演示了 mblen() 函数的用法。

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main()
{
    int len;
    char *pmbnull = NULL;
    char *pmb = (char *)malloc( MB_CUR_MAX );
    wchar_t *pwc = L"Hi";
    wchar_t *pwcs = (wchar_t *)malloc( sizeof( wchar_t ));

    printf("Converting to multibyte string\n");
    len = wcstombs( pmb, pwc, MB_CUR_MAX);
    printf("Characters converted %d\n", len);
    printf("Hex value of first multibyte character: %#.4x\n", pmb);

    len = mblen( pmb, MB_CUR_MAX );
    printf( "Length in bytes of multibyte character %x: %u\n", pmb, len );

    pmb = NULL;

    len = mblen( pmb, MB_CUR_MAX );
    printf( "Length in bytes of multibyte character %x: %u\n", pmb, len );

    return(0);
}
```

让我们编译并运行上面的程序，将产生以下结果：

```
Converting to multibyte string
Characters converted 1
Hex value of first multibyte character: 0x168c6010
Length in bytes of multibyte character 168c6010: 1
Length in bytes of multibyte character 0: 0
```

## size_t mbstowcs(wchar_t *pwcs, const char *str, size_t n)

### 描述

C 库函数 size_t mbstowcs(wchar_t *pwcs, const char *str, size_t n) 将参数 str 指向的多字节字符串转换为 pwcs 指向的数组。

### 声明

下面是 mbstowcs() 函数的声明。

```
size_t mbstowcs(wchar_t *pwcs, const char *str, size_t n)
```

### 参数

- pwcs -- 这是一个指向 wchar_t 元素数组的指针，该数组足够长，可存储最长的宽字符串。
- str -- 这是要解释的 C 多字节字符串。
- n -- 这是要解释的 wchar_t 字符的最大数量。

### 返回值

该函数返回转换后的字符数，不包括结尾的空字符。如果遇到无效的多字节字符，则返回 -1。

### 示例

下面的实例演示了 mbstowcs() 函数的用法。

```
#include<stdio.h>
#include<stdlib.h>
#include<string.h>
```


```c
int main()
{
    int len;
    char *pmbnull = NULL;
    char *pmb = (char *)malloc( MB_CUR_MAX );
    wchar_t *pwc = L"Hi";
    wchar_t *pwcs = (wchar_t *)malloc( sizeof( wchar_t ) );

    printf("Converting to multibyte string\n");
    len = wcstombs( pmb, pwc, MB_CUR_MAX);
    printf("Characters converted %d\n", len);
    printf("Hex value of first multibyte character: %#.4x\n", pmb);

    printf("Converting back to Wide-Character string\n");
    len = mbstowcs( pwcs, pmb, MB_CUR_MAX);
    printf("Characters converted %d\n", len);
    printf("Hex value of first wide character %#.4x\n\n", pwcs);

    return(0);
}
```

让我们编译并运行上面的程序，它将产生以下结果：

```
Converting to multibyte string
Characters converted 1
Hex value of first multibyte character: 0x19a60010
Converting back to Wide-Character string
Characters converted 1
Hex value of first wide character 0x19a60030
```

## int mbtowc(wchar_t *pwc, const char *str, size_t n)

### 描述
C 库函数 int mbtowc(wchar_t *pwc, const char *str, size_t n) 将多字节序列转换为宽字符。

### 声明
以下是 mbtowc() 函数的声明。

```c
int mbtowc(wchar_t *pwc, const char *str, size_t n)
```

### 参数
- pwc -- 这是指向类型为 wchar_t 的对象的指针。
- str -- 这是指向多字节字符的第一个字节的指针。
- n -- 这是检查字符长度的最大字节数。

### 返回值
- 如果 str 不为 NULL，mbtowc() 函数返回从 str 开始消耗的字节数，如果 s 指向空字节则返回 0，失败时返回 -1。
- 如果 str 为 NULL，mbtowc() 函数如果编码具有非平凡的移位状态则返回非零值，如果编码是无状态的则返回零。

### 示例
以下示例展示了 mbtowc() 函数的使用。

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main()
{
    char *str = "This is tutorialspoint.com";
    wchar_t mb[100];
    int len;

    len = mblen(NULL, MB_CUR_MAX);

    mbtowc(mb, str, len*strlen(str) );

    wprintf(L"%ls \n", mb );

    return(0);
}
```

让我们编译并运行上面的程序，它将产生以下结果，该结果将为多字节，是一种二进制输出。

???

## size_t wcstombs(char *str, const wchar_t *pwcs, size_t n)

### 描述
C 库函数 size_t wcstombs(char *str, const wchar_t *pwcs, size_t n) 将宽字符字符串 pwcs 转换为从 str 开始的多字节字符串。最多写入 n 字节到 str。

### 声明
以下是 wcstombs() 函数的声明。

```c
size_t wcstombs(char *str, const wchar_t *pwcs, size_t n)
```

### 参数
- str -- 这是指向至少有 n 个字节长的 char 元素数组的指针。
- pwcs -- 这是要转换的宽字符字符串。
- n -- 这是要写入 str 的最大字节数。

### 返回值
此函数返回转换并写入 str 的字节数（不是字符数），不包括结束的空字符。如果遇到无效的多字节字符，则返回 -1 值。

### 示例
以下示例展示了 wcstombs() 函数的使用。

```c
#include <stdio.h>
#include <stdlib.h>

#define BUFFER_SIZE 50

int main()
{
    size_t ret;
    char *MB = (char *)malloc( BUFFER_SIZE );
    wchar_t *WC = L"http://www.tutorialspoint.com";

    /* converting wide-character string */
    ret = wcstombs(MB, WC, BUFFER_SIZE);
    printf("Characters converted = %u\n", ret);
    printf("Multibyte character = %s\n", MB);

    return(0);
}
```

让我们编译并运行上面的程序，它将产生以下结果：

```
Characters converted = 29
Multibyte character = http://www.tutorialspoint.com
```

## int wctomb(char *str, wchar_t wchar)

### 描述
C 库函数 int wctomb(char *str, wchar_t wchar) 函数将宽字符 wchar 转换为其多字节表示形式，并将其存储在 str 指向的字符数组的开头。

### 声明
以下是 wctomb() 函数的声明。

```c
int wctomb(char *str, wchar_t wchar)
```

### 参数
- str -- 这是指向足够大以容纳多字节字符的数组的指针，
- wchar -- 这是类型为 wchar_t 的宽字符。

### 返回值
- 如果 str 不为 NULL，wctomb() 函数返回已写入 str 处的字节数组的字节数。如果 wchar 不能表示为多字节序列，则返回 -1。
- 如果 str 为 NULL，wctomb() 函数如果编码具有非平凡的移位状态则返回非零值，如果编码是无状态的则返回零。

### 示例
以下示例展示了 wctomb() 函数的使用。

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int i;
    wchar_t wc = L'a';
    char *pmbnull = NULL;
    char *pmb = (char *)malloc(sizeof( char ));

    printf("Converting wide character:\n");
    i = wctomb( pmb, wc );
    printf("Characters converted: %u\n", i);
    printf("Multibyte character: %.1s\n", pmb);

    printf("Trying to convert when target is NULL:\n");
    i = wctomb( pmbnull, wc );
    printf("Characters converted: %u\n", i);
    /* this will not print any value */
    printf("Multibyte character: %.1s\n", pmbnull);

    return(0);
}
```

让我们编译并运行上面的程序，它将产生以下结果：

```
Converting wide character:
Characters converted: 1
Multibyte character: a
Trying to convert when target is NULL:
Characters converted: 0
Multibyte character:
```

## 介绍
**string.h** 头文件定义了一种变量类型、一个宏以及用于操作字符数组的各种函数。

### 库变量
以下是 string.h 头文件中定义的变量类型：

| S.N. | 变量 & 描述 |
|------|------------------------|
| 1 | **size_t**<br>这是一个无符号整数类型，是 **sizeof** 关键字的结果。 |

### 库宏
以下是 string.h 头文件中定义的宏：

| S.N. | 宏 & 描述 |
|------|---------------------|
| 1 | **NULL**<br>此宏是空指针常量的值。 |

### 库函数
以下是 string.h 头文件中定义的函数：

| S.N. | 函数 & 描述 |
|------|------------------------|
| 1 | `void *memchr(const void *str, int c, size_t n)`<br>在参数 str 指向的字符串的前 n 个字节中搜索字符 c（一个 unsigned char）的第一次出现。 |
| 2 | `int memcmp(const void *str1, const void *str2, size_t n)`<br>比较 *str1* 和 *str2* 的前 n 个字节。 |
| 3 | `void *memcpy(void *dest, const void *src, size_t n)`<br>从 src 复制 n 个字符到 *dest*。 |
| 4 | `void *memmove(void *dest, const void *src, size_t n)`<br>另一个函数用于从 *str2* 复制 n 个字符到 *str1*。 |
| 5 | `void *memset(void *str, int c, size_t n)`<br>将字符 c（一个 unsigned char）复制到参数 *str* 指向的字符串的前 n 个字符。 |
| 6 | `char *strcat(char *dest, const char *src)`<br>将 *src* 指向的字符串追加到 *dest* 指向的字符串末尾。 |
| 7 | `char *strncat(char *dest, const char *src, size_t n)`<br>将 *src* 指向的字符串追加到 *dest* 指向的字符串末尾，最多 n 个字符长。 |
| 8 | `char *strchr(const char *str, int c)`<br>在参数 *str* 指向的字符串中搜索字符 c（一个 unsigned char）的第一次出现。 |
| 9 | `int strcmp(const char *str1, const char *str2)`<br>比较 *str1* 指向的字符串与 *str2* 指向的字符串。 |
| 10 | `int strncmp(const char *str1, const char *str2, size_t n)`<br>比较 *str1* 和 *str2* 的前最多 n 个字节。 |
| 11 | `int strcoll(const char *str1, const char *str2)`<br>比较字符串 *str1* 与 *str2*。结果取决于位置的 LC_COLLATE 设置。 |
| 12 | `char *strcpy(char *dest, const char *src)`<br>将 *src* 指向的字符串复制到 *dest*。 |




| No | Function | Description |
|---|---|---|
| 13 | `char *strncpy(char *dest, const char *src, size_t n)` | 从 src 指向的字符串复制最多 n 个字符到 dest。 |
| 14 | `size_t strcspn(const char *str1, const char *str2)` | 计算 str1 的初始段长度，该段完全由不在 str2 中的字符组成。 |
| 15 | `char *strerror(int errnum)` | 在内部数组中搜索错误号 errnum，并返回指向错误消息字符串的指针。 |
| 16 | `size_t strlen(const char *str)` | 计算字符串 str 的长度，直到但不包括终止空字符。 |
| 17 | `char *strpbrk(const char *str1, const char *str2)` | 查找字符串 str1 中第一个与 str2 中指定任意字符匹配的字符。 |
| 18 | `char *strrchr(const char *str, int c)` | 在参数 str 指向的字符串中搜索字符 c（无符号字符）最后一次出现的位置。 |
| 19 | `size_t strspn(const char *str1, const char *str2)` | 计算 str1 的初始段长度，该段完全由 str2 中的字符组成。 |
| 20 | `char *strstr(const char *haystack, const char *needle)` | 查找整个字符串 needle（不包括终止空字符）在字符串 haystack 中第一次出现的位置。 |
| 21 | `char *strtok(char *str, const char *delim)` | 将字符串 str 分解为一系列由 delim 分隔的标记。 |
| 22 | `size_t strxfrm(char *dest, const char *src, size_t n)` | 将字符串 src 的前 n 个字符转换为当前区域设置，并将它们放入字符串 dest 中。 |

## void *memchr(const void *str, int c, size_t n)

### 描述

C 库函数 void *memchr(const void *str, int c, size_t n) 在参数 str 所指向字符串的前 n 个字节中搜索字符 c（无符号字符）第一次出现的位置。

### 声明

以下是 memchr() 函数的声明。

```
void *memchr(const void *str, int c, size_t n)
```

### 参数

- **str** -- 这是指向执行搜索的内存块的指针。
- **c** -- 这是作为 int 传递的值，但函数使用该值的无符号字符转换逐字节搜索。
- **n** -- 这是要分析的字节数。

### 返回值

该函数返回指向匹配字节的指针；如果给定内存区域中不存在该字符，则返回 NULL。

### 示例

以下示例演示了 memchr() 函数的用法。

```
#include <stdio.h>
#include <string.h>

int main ()
{
    const char str[] = "http://www.tutorialspoint.com";
    const char ch = '.';
    char *ret;

    ret = memchr(str, ch, strlen(str));

    printf("String after |%c| is - |%s|\n", ch, ret);

    return(0);
}
```

让我们编译并运行上述程序，它将产生以下结果：

```
String after |.| is - |.tutorialspoint.com|
```

## int memcmp(const void *str1, const void *str2, size_t n)

### 描述

C 库函数 int memcmp(const void *str1, const void *str2, size_t n) 比较内存区域 str1 和内存区域 str2 的前 n 个字节。

### 声明

以下是 memcmp() 函数的声明。

```
int memcmp(const void *str1, const void *str2, size_t n)
```

### 参数

- **str1** -- 这是指向内存块的指针。
- **str2** -- 这是指向内存块的指针。
- **n** -- 这是要比较的字节数。

### 返回值

- 如果返回值 < 0，则表示 str1 小于 str2。
- 如果返回值 > 0，则表示 str2 小于 str1。
- 如果返回值 = 0，则表示 str1 等于 str2。

### 示例

以下示例演示了 memcmp() 函数的用法。

```
#include <stdio.h>
#include <string.h>

int main ()
{
    char str1[15];
    char str2[15];
    int ret;

    memcpy(str1, "abcdef", 6);
    memcpy(str2, "ABCDEF", 6);

    ret = memcmp(str1, str2, 5);

    if(ret > 0)
    {
        printf("str2 is less than str1");
    }
    else if(ret < 0)
    {
        printf("str1 is less than str2");
    }
    else
    {
        printf("str1 is equal to str2");
    }

    return(0);
}
```

让我们编译并运行上述程序，它将产生以下结果：

```
str2 is less than str1
```

## void *memcpy(void *dest, const void *src, size_t n)

### 描述

C 库函数 void *memcpy(void *str1, const void *str2, size_t n) 从内存区域 str2 复制 n 个字符到内存区域 str1。

### 声明

以下是 memcpy() 函数的声明。

```
void *memcpy(void *str1, const void *str2, size_t n)
```

### 参数

- **str1** -- 这是指向目标数组的指针，内容将被复制到该数组，其被类型转换为 void* 类型的指针。
- **str2** -- 这是指向要复制的数据源的指针，其被类型转换为 void* 类型的指针。
- **n** -- 这是要复制的字节数。

### 返回值

该函数返回指向目标的指针，即 str1。

### 示例

以下示例演示了 memcpy() 函数的用法。

```
#include <stdio.h>
#include <string.h>

int main ()
{
    const char src[50] = "http://www.tutorialspoint.com";
    char dest[50];

    printf("Before memcpy dest = %s\n", dest);
    memcpy(dest, src, strlen(src)+1);
    printf("After memcpy dest = %s\n", dest);

    return(0);
}
```

让我们编译并运行上述程序，它将产生以下结果：

```
Before memcpy dest =
After memcpy dest = http://www.tutorialspoint.com
```

## void *memmove(void *dest, const void *src, size_t n)

### 描述

C 库函数 void *memmove(void *str1, const void *str2, size_t n) 从 str2 复制 n 个字符到 str1，但对于重叠的内存块，memmove() 是比 memcpy() 更安全的方法。

### 声明

以下是 memmove() 函数的声明。

```
void *memmove(void *str1, const void *str2, size_t n)
```

### 参数

- **str1** -- 这是指向目标数组的指针，内容将被复制到该数组，其被类型转换为 void* 类型的指针。
- **str2** -- 这是指向要复制的数据源的指针，其被类型转换为 void* 类型的指针。
- **n** -- 这是要复制的字节数。

### 返回值

该函数返回指向目标的指针，即 str1。

### 示例

以下示例演示了 memmove() 函数的用法。

```c
#include <stdio.h>
#include <string.h>

int main ()
{
    char dest[] = "oldstring";
    const char src[]  = "newstring";

    printf("Before memmove dest = %s, src = %s\n", dest, src);
    memmove(dest, src, 9);
    printf("After memmove dest = %s, src = %s\n", dest, src);

    return(0);
}
```

让我们编译并运行上述程序，它将产生以下结果：

```
Before memmove dest = oldstring, src = newstring
After memmove dest = newstring, src = newstring
```

## void *memset(void *str, int c, size_t n)

### 描述

C 库函数 **void *memset(void *str, int c, size_t n)** 将字符 **c**（无符号字符）复制到参数 **str** 所指向字符串的前 **n** 个字符。

### 声明

以下是 memset() 函数的声明。

```c
void *memset(void *str, int c, size_t n)
```

### 参数

- **str** -- 这是指向要填充的内存块的指针。
- **c** -- 这是要设置的值。该值作为 int 传递，但函数使用该值的无符号字符转换来填充内存块。
- **n** -- 这是要设置为该值的字节数。

### 返回值

该函数返回指向内存区域 str 的指针。

### 示例

以下示例演示了 memset() 函数的用法。

```c
#include <stdio.h>
#include <string.h>

int main ()
{
    char str[50];

    strcpy(str,"This is string.h library function");
    puts(str);

    memset(str,'$',7);
    puts(str);

    return(0);
}
```

让我们编译并运行上述程序，它将产生以下结果：

```
This is string.h library function
$$$$$$$ string.h library function
```

## char *strcat(char *dest, const char *src)

### 描述

C 库函数 char *strcat(char *dest, const char *src) 将 src 指向的字符串追加到 dest 指向的字符串末尾。





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





## char *strncpy(char *dest, const char *src, size_t n)

以下是 strncpy() 函数的声明。

```c
char *strncpy(char *dest, const char *src, size_t n)
```

### 参数

- **dest** -- 这是一个指向目标数组的指针，内容将被复制到该数组中。
- **src** -- 这是要复制的字符串。
- **n** -- 要从源字符串复制的字符数。

### 返回值

该函数返回复制后的最终字符串。

### 示例

以下示例演示了 strncpy() 函数的用法。这里我们使用 memset() 函数来清空内存位置。

```c
#include <stdio.h>
#include <string.h>

int main()
{
   char src[40];
   char dest[12];

   memset(dest, '\0', sizeof(dest));
   strcpy(src, "This is tutorialspoint.com");
   strncpy(dest, src, 10);

   printf("Final copied string : %s\n", dest);

   return(0);
}
```

让我们编译并运行上述程序，将产生以下结果：

```
Final copied string : This is tu
```

## size_t strcspn(const char *str1, const char *str2)

### 描述

C 库函数 size_t strcspn(const char *str1, const char *str2) 计算 str1 的初始段长度，该初始段完全由不在 str2 中的字符组成。

### 声明

以下是 strcspn() 函数的声明。

```c
size_t strcspn(const char *str1, const char *str2)
```

### 参数

- str1 -- 这是要扫描的主要 C 字符串。
- str2 -- 这是包含要在 str1 中匹配的字符列表的字符串。

### 返回值

该函数返回字符串 str1 的初始段中不在字符串 str2 中的字符数。

### 示例

以下示例演示了 strcspn() 函数的用法。

```c
#include <stdio.h>
#include <string.h>

int main ()
{
    int len;
    const char str1[] = "ABCDEF4960910";
    const char str2[] = "013";
    len = strcspn(str1, str2);
    printf("First matched character is at %d\n", len + 1);
    return(0);
}
```

让我们编译并运行上述程序，将产生以下结果：

```
First matched character is at 10
```

## char *strerror(int errnum)

### 描述

C 库函数 **char *strerror(int errnum)** 在内部数组中搜索错误编号 **errnum**，并返回指向错误消息字符串的指针。**strerror** 生成的错误字符串取决于开发平台和编译器。

### 声明

以下是 strerror() 函数的声明。

```c
char *strerror(int errnum)
```

### 参数

- **errnum** -- 这是错误编号，通常是 **errno**。

### 返回值

该函数返回一个指针，指向描述错误 errnum 的错误字符串。

### 示例

以下示例演示了 strerror() 函数的用法。

```c
#include <stdio.h>
#include <string.h>
#include <errno.h>

int main ()
{
    FILE *fp;

    fp = fopen("file.txt","r");
    if( fp == NULL )
    {
        printf("Error: %s\n", strerror(errno));
    }

    return(0);
}
```

由于我们尝试打开一个不存在的文件，让我们编译并运行上述程序，将产生以下结果：

```
Error: No such file or directory
```

## size_t strlen(const char *str)

### 描述

C 库函数 size_t strlen(const char *str) 计算字符串 str 的长度，直到终止空字符为止，但不包括该字符。

### 声明

以下是 strlen() 函数的声明。

```c
size_t strlen(const char *str)
```

### 参数

- str -- 这是要查找长度的字符串。

### 返回值

该函数返回字符串的长度。

### 示例

以下示例演示了 strlen() 函数的用法。

```c
#include <stdio.h>
#include <string.h>

int main ()
{
    char str[50];
    int len;

    strcpy(str, "This is tutorialspoint.com");

    len = strlen(str);
    printf("Length of |%s| is |%d|\n", str, len);

    return(0);
}
```

让我们编译并运行上述程序，将产生以下结果：

```
Length of |This is tutorialspoint.com| is |26|
```

## char *strpbrk(const char *str1, const char *str2)

### 描述

C 库函数 char *strpbrk(const char *str1, const char *str2) 查找字符串 str1 中与 str2 中任意指定字符匹配的第一个字符。这不包括终止的空字符。

### 声明

以下是 strpbrk() 函数的声明。

```c
char *strpbrk(const char *str1, const char *str2)
```

### 参数

- str1 -- 这是要扫描的 C 字符串。
- str2 -- 这是包含要匹配字符的 C 字符串。

### 返回值

该函数返回一个指针，指向 str1 中与 str2 中某个字符匹配的字符；如果未找到这样的字符，则返回 NULL。

### 示例

以下示例演示了 strpbrk() 函数的用法。

```c
#include <stdio.h>
#include <string.h>

int main ()
{
    const char str1[] = "abcde2fghi3jk41";
    const char str2[] = "34";
    char *ret;

    ret = strpbrk(str1, str2);
    if(ret)
    {
        printf("First matching character: %c\n", *ret);
    }
    else
    {
        printf("Character not found");
    }
    return(0);
}
```

让我们编译并运行上述程序，将产生以下结果：

```
First matching character: 3
```

## char *strrchr(const char *str, int c)

### 描述

C 库函数 char *strrchr(const char *str, int c) 在参数 str 指向的字符串中搜索字符 c（一个无符号字符）的最后一次出现位置。

### 声明

以下是 strrchr() 函数的声明。

```c
char *strrchr(const char *str, int c)
```

### 参数

- str -- 这是 C 字符串。
- c -- 这是要定位的字符。它以其 int 提升形式传递，但在内部会转换回 char。

### 返回值

该函数返回一个指针，指向 str 中字符最后一次出现的位置。如果未找到该值，函数返回空指针。

### 示例

以下示例演示了 strrchr() 函数的用法。

```c
#include <stdio.h>
#include <string.h>

int main ()
{
    int len;
    const char str[] = "http://www.tutorialspoint.com";
    const char ch = '.';
    char *ret;

    ret = strrchr(str, ch);

    printf("String after |%c| is - |%s|\n", ch, ret);

    return(0);
}
```

让我们编译并运行上述程序，将产生以下结果：

```
String after |.| is - |.com|
```

## size_t strspn(const char *str1, const char *str2)

### 描述

C 库函数 size_t strspn(const char *str1, const char *str2) 计算 str1 的初始段长度，该初始段完全由 str2 中的字符组成。

### 声明

以下是 strspn() 函数的声明。

```c
size_t strspn(const char *str1, const char *str2)
```

### 参数

- str1 -- 这是要扫描的主要 C 字符串。
- str2 -- 这是包含要在 str1 中匹配的字符列表的字符串。

### 返回值

该函数返回 str1 的初始段中仅由 str2 中字符组成的字符数。

### 示例

以下示例演示了 strspn() 函数的用法。

```c
#include <stdio.h>
#include <string.h>

int main ()
{
    int len;
    const char str1[] = "ABCDEF G019874";
    const char str2[] = "ABCD";

    len = strspn(str1, str2);

    printf("Length of initial segment matching %d\n", len );

    return(0);
}
```

让我们编译并运行上述程序，将产生以下结果：

```
Length of initial segment matching 4
```

## char *strstr(const char *haystack, const char *needle)

### 描述

C 库函数 char *strstr(const char *haystack, const char *needle) 查找子字符串 needle 在字符串 haystack 中的第一次出现位置。终止的 '\0' 字符不会被比较。

### 声明

以下是 strstr() 函数的声明。

```c
char *strstr(const char *haystack, const char *needle)
```

### 参数

- **haystack** -- 这是要扫描的主要 C 字符串。
- **needle** -- 这是要在 haystack 字符串中搜索的小字符串。

### 返回值

该函数返回一个指针，指向 haystack 中 needle 指定的整个字符序列首次出现的位置；如果该序列不在 haystack 中，则返回空指针。

### 示例

以下示例演示了 strstr() 函数的用法。

```c
#include <stdio.h>
#include <string.h>
```




```
int main()
{
    const char haystack[20] = "TutorialsPoint";
    const char needle[10] = "Point";
    char *ret;

    ret = strstr(haystack, needle);

    printf("The substring is: %s\n", ret);

    return(0);
}
```

让我们编译并运行上述程序，这将产生以下结果：

The substring is: Point

## char *strtok(char *str, const char *delim)

### 描述

C 库函数 **char *strtok(char *str, const char *delim)** 使用分隔符 **delim** 将字符串 **str** 分解为一系列标记。

### 声明

以下是 strtok() 函数的声明。

```
char *strtok(char *str, const char *delim)
```

### 参数

- **str** -- 此字符串的内容会被修改，并分解为更小的字符串（标记）。
- **delim** -- 这是包含分隔符的 C 字符串。这些分隔符可能因调用而异。

### 返回值

此函数返回指向字符串中找到的最后一个标记的指针。如果没有剩余标记可检索，则返回空指针。

### 示例

以下示例展示了 strtok() 函数的用法。

```c
#include <string.h>
#include <stdio.h>

int main()
{
    const char str[80] = "This is - www.tutorialspoint.com - website";
    const char s[2] = "-";
    char *token;

    /* get the first token */
    token = strtok(str, s);

    /* walk through other tokens */
    while( token != NULL )
    {
        printf( " %s\n", token );

        token = strtok(NULL, s);
    }

    return(0);
}
```

让我们编译并运行上述程序，这将产生以下结果：

```
This is
www.tutorialspoint.com
website
```

## size_t strxfrm(char *dest, const char *src, size_t n)

### 描述

C 库函数 size_t strxfrm(char *dest, const char *src, size_t n) 将字符串 src 的前 n 个字符转换为当前区域设置，并将它们放入字符串 dest。

### 声明

以下是 strxfrm() 函数的声明。

```
size_t strxfrm(char *dest, const char *src, size_t n)
```

### 参数

- **dest** -- 这是指向目标数组的指针，内容将被复制到其中。如果 n 参数为零，它可以是空指针。
- **src** -- 这是要转换为当前区域设置的 C 字符串。
- **n** -- 要复制到 str1 的最大字符数。

### 返回值

此函数返回转换后字符串的长度，不包括终止空字符。

### 示例

以下示例展示了 strxfrm() 函数的用法。

```c
#include <stdio.h>
#include <string.h>

int main()
{
    char dest[20];
    char src[20];
    int len;

    strcpy(src, "Tutorials Point");
    len = strxfrm(dest, src, 20);

    printf("Length of string |%s| is: |%d|", dest, len);

    return(0);
}
```

让我们编译并运行上述程序，这将产生以下结果：

```
Length of string |Tutorials Point| is: |15|
```

## 简介

time.h 头文件定义了四种变量类型、两个宏以及用于操作日期和时间的各种函数。

## 库变量

以下是 time.h 头文件中定义的变量类型：

| 序号 | 变量与描述 |
|------|------------------------|
| 1 | **size_t**<br>这是无符号整型，是 **sizeof** 关键字的结果。 |
| 2 | **clock_t**<br>这是一种适合存储处理器时间的类型。 |
| 3 | **time_t**<br>这是一种适合存储日历时间的类型。 |
| 4 | **struct tm**<br>这是一个用于保存时间和日期的结构体。 |

tm 结构体具有以下定义：

```c
struct tm {
    int tm_sec;     /* seconds, range 0 to 59     */
    int tm_min;     /* minutes, range 0 to 59     */
    int tm_hour;    /* hours, range 0 to 23       */
    int tm_mday;    /* day of the month, range 1 to 31 */
    int tm_mon;     /* month, range 0 to 11       */
    int tm_year;    /* The number of years since 1900 */
    int tm_wday;    /* day of the week, range 0 to 6  */
    int tm_yday;    /* day in the year, range 0 to 365 */
    int tm_isdst;          /* daylight saving time          */
};
```

## 库宏

以下是 time.h 头文件中定义的宏：

| 序号 | 宏与描述 |
|------|---------------------|
| 1 | **NULL**<br>此宏是空指针常量的值。 |
| 2 | **CLOCKS_PER_SEC**<br>此宏表示每秒的处理器时钟数。 |

## 库函数

以下是 time.h 头文件中定义的函数：

| 序号 | 函数与描述 |
|------|------------------------|
| 1 | `char *asctime(const struct tm *timeptr)`<br>返回一个指向字符串的指针，该字符串表示结构体 timeptr 的日期和时间。 |
| 2 | `clock_t clock(void)`<br>返回自实现定义的纪元开始（通常是程序开始）以来使用的处理器时钟时间。 |
| 3 | `char *ctime(const time_t *timer)`<br>返回一个表示基于参数 timer 的本地时间的字符串。 |
| 4 | `double difftime(time_t time1, time_t time2)`<br>返回 time1 和 time2 之间的秒数差（time1-time2）。 |
| 5 | `struct tm *gmtime(const time_t *timer)`<br>timer 的值被分解到 tm 结构中，并以协调世界时（UTC）表示，也称为格林尼治标准时间（GMT）。 |
| 6 | **struct tm *localtime(const time_t *timer)**<br>timer 的值被分解到 tm 结构中，并以本地时区表示。 |
| 7 | **time_t mktime(struct tm *timeptr)**<br>根据本地时区将 timeptr 指向的结构体转换为 time_t 值。 |
| 8 | **size_t strftime(char *str, size_t maxsize, const char *format, const struct tm *timeptr)**<br>根据 format 中定义的格式规则格式化结构体 timeptr 中表示的时间，并存储到 str 中。 |
| 9 | **time_t time(time_t *timer)**<br>计算当前日历时间并将其编码为 time_t 格式。 |

## char *asctime(const struct tm *timeptr)

### 描述

C 库函数 **char *asctime(const struct tm *timeptr)** 返回一个指向字符串的指针，该字符串表示结构体 **struct timeptr** 的日期和时间。

### 声明

以下是 asctime() 函数的声明。

```
char *asctime(const struct tm *timeptr)
```

### 参数

**timeptr** 是指向 tm 结构的指针，该结构包含分解为其组成部分的日历时间，如下所示：

```c
struct tm {
    int tm_sec;     /* seconds, range 0 to 59     */
    int tm_min;     /* minutes, range 0 to 59     */
    int tm_hour;    /* hours, range 0 to 23       */
    int tm_mday;    /* day of the month, range 1 to 31 */
    int tm_mon;     /* month, range 0 to 11       */
    int tm_year;    /* The number of years since 1900 */
};
```

## clock_t clock(void)

### 描述

C 库函数 **clock_t clock(void)** 返回自程序启动以来经过的时钟滴答数。要获取 CPU 使用的秒数，需要除以 CLOCKS_PER_SEC。

在 CLOCKS_PER_SEC 等于 1000000 的 32 位系统上，此函数大约每 72 分钟返回相同的值。

### 声明

以下是 clock() 函数的声明。

```c
clock_t clock(void)
```

### 参数

- 无

### 返回值

此函数返回自程序开始以来经过的时钟滴答数。失败时，函数返回 -1。

### 示例

以下示例展示了 clock() 函数的用法。

```c
#include <time.h>
#include <stdio.h>

int main()
{
    clock_t start_t, end_t, total_t;
    int i;

    start_t = clock();
    printf("Starting of the program, start_t = %ld\n", start_t);

    printf("Going to scan a big loop, start_t = %ld\n", start_t);
    for(i=0; i< 100000000; i++)
    {
    }
    end_t = clock();
    printf("End of the big loop, end_t = %ld\n", end_t);
```



```c
total_t = (double)(end_t - start_t) / CLOCKS_PER_SEC;
printf("Total time taken by CPU: %f\n", total_t );
printf("Exiting of the program...\n");

return(0);
}
```

让我们编译并运行上面的程序，它将产生以下结果：

```text
Starting of the program, start_t = 0
Going to scan a big loop, start_t = 0
End of the big loop, end_t = 20000
Total time taken by CPU: 0.000000
Exiting of the program...
```

## char \*ctime(const time_t \*timer)

### 描述

C 库函数 **char \*ctime(const time_t \*timer)** 返回一个表示基于参数 **timer** 的本地时间的字符串。

返回的字符串具有以下格式：**Www Mmm dd hh:mm:ss yyyy**，其中 *Www* 是星期几，*Mmm* 是月份的字母，*dd* 是月份的日期，*hh:mm:ss* 是时间，*yyyy* 是年份。

### 声明

```c
char *ctime(const time_t *timer)
```

### 参数

- **timer** -- 这是指向包含日历时间的 time_t 对象的指针。

### 返回值

此函数返回一个包含日期和时间信息的人类可读格式的 C 字符串。

### 示例

以下示例展示了 ctime() 函数的用法。

```c
#include <stdio.h>
#include <time.h>

int main ()
{
    time_t curtime;

    time(&curtime);

    printf("Current time = %s", ctime(&curtime));

    return(0);
}
```

让我们编译并运行上面的程序，它将产生以下结果：

```text
Current time = Mon Aug 13 08:23:14 2012
```

## double difftime(time_t time1, time_t time2)

### 描述

C 库函数 double difftime(time_t time1, time_t time2) 返回 time1 和 time2 之间的秒数差，即 (time1 - time2)。这两个时间以日历时间指定，表示自纪元（1970 年 1 月 1 日 00:00:00，协调世界时 (UTC)）以来经过的时间。

### 声明

```c
double difftime(time_t time1, time_t time2)
```

### 参数

- time1 -- 这是结束时间的 time_t 对象。
- time2 -- 这是开始时间的 time_t 对象。

### 返回值

此函数返回两个时间之差 (time2 - time1) 作为 double 值。

### 示例

以下示例展示了 difftime() 函数的用法。

```c
#include <stdio.h>
#include <time.h>

int main ()
{
   time_t start_t, end_t;
   double diff_t;

   printf("Starting of the program...\n");
   time(&start_t);

   printf("Sleeping for 5 seconds...\n");
   sleep(5);

   time(&end_t);
   diff_t = difftime(end_t, start_t);

   printf("Execution time = %f\n", diff_t);
   printf("Exiting of the program...\n");

   return(0);
}
```

让我们编译并运行上面的程序，它将产生以下结果：

```text
Starting of the program...
Sleeping for 5 seconds...
Execution time = 5.000000
Exiting of the program...
```

## struct tm \*gmtime(const time_t \*timer)

### 描述

C 库函数 **struct tm \*gmtime(const time_t \*timer)** 使用 timer 指向的值填充一个 **tm** 结构，其中的值表示相应的时间，以协调世界时 (UTC) 或 GMT 时区表示。

### 示例

```c
time(&rawtime);
/* Get GMT time */
info = gmtime(&rawtime );

printf("Current world clock:\n");
printf("London : %2d:%02d\n", (info->tm_hour+BST)%24, info->tm_min);
printf("China  : %2d:%02d\n", (info->tm_hour+CCT)%24, info->tm_min);

return(0);
}
```

让我们编译并运行上面的程序，它将产生以下结果：

```text
Current world clock:
London : 14:10
China  : 21:10
```

## struct tm \*localtime(const time_t \*timer)

### 描述

C 库函数 **struct tm \*localtime(const time_t \*timer)** 使用 **timer** 指向的时间填充一个 **tm** 结构，其中的值表示相应的本地时间。**timer** 的值被分解到结构 **tm** 中并以本地时区表示。

### 声明

```c
struct tm *localtime(const time_t *timer)
```

### 参数

- **timer** -- 这是指向表示日历时间的 time_t 值的指针。

### 返回值

此函数返回一个指向填充了时间信息的 **tm** 结构的指针。以下是 tm 结构信息：

```c
struct tm {
    int tm_sec;        /* seconds, range 0 to 59        */
```

```c
info.tm_year = 2001 - 1900;
info.tm_mon = 7 - 1;
info.tm_mday = 4;
info.tm_hour = 0;
info.tm_min = 0;
info.tm_sec = 1;
info.tm_isdst = -1;

ret = mktime(&info);
if( ret == -1 )
{
    printf("Error: unable to make time using mktime\n");
}
else
{
    strftime(buffer, sizeof(buffer), "%c", &info );
    printf(buffer);
}

return(0);
}
```

让我们编译并运行上面的程序，它将产生以下结果：

```text
Wed Jul 4 00:00:01 2001
```

## size_t strftime(char \*str, size_t maxsize, const char \*format, const struct tm \*timeptr)

### 描述

C 库函数 **size_t strftime(char \*str, size_t maxsize, const char \*format, const struct tm \*timeptr)** 根据 **format** 中定义的格式化规则对结构 **timeptr** 中表示的时间进行格式化并存储到 **str** 中。

### 声明

```c
size_t strftime(char *str, size_t maxsize, const char *format, const struct tm *timeptr)
```

### 参数

- **str** -- 这是指向目标数组的指针，其中复制结果的 C 字符串。
- **maxsize** -- 这是要复制到 str 的最大字符数。
- **format** -- 这是包含任意组合的常规字符和特殊格式说明符的 C 字符串。这些格式说明符由函数替换为对应值以表示 tm 中指定的时间。格式说明符为：

| Specifier | Replaced By | Example |
|---|---|---|
| %a | Abbreviated weekday name | Sun |
| %A | Full weekday name | Sunday |
| %b | Abbreviated month name | Mar |
| %B | Full month name | March |
| %c | Date and time representation | Sun Aug 19 02:56:02 2012 |
| %d | Day of the month (01-31) | 19 |
| %H | Hour in 24h format (00-23) | 14 |
| %I | Hour in 12h format (01-12) | 05 |
| %j | Day of the year (001-366) | 231 |
| %m | Month as a decimal number (01-12) | 08 |
| %M | Minute (00-59) | 55 |
| %p | AM or PM designation | PM |
| %S | Second (00-61) | 02 |
| %U | Week number with the first Sunday as the first day of week one (00-53) | 33 |
| %w | Weekday as a decimal number with Sunday as 0 (0-6) | 4 |
| %W | Week number with the first Monday as the first day of week one (00-53) | 34 |
| %x | Date representation | 08/19/12 |
| %X | Time representation | 02:50:06 |
| %y | Year, last two digits (00-99) | 01 |
| %Y | Year | 2012 |
| %Z | Timezone name or abbreviation | CDT |
| %% | A % sign | % |

- **timeptr** -- 这是指向包含日历时间分解为其组成部分的 tm 结构的指针，如下所示：

```c
struct tm {
    int tm_sec;         /* seconds,  range 0 to 59          */
    int tm_min;         /* minutes, range 0 to 59           */
    int tm_hour;        /* hours, range 0 to 23             */
    int tm_mday;        /* day of the month, range 1 to 31  */
    int tm_mon;         /* month, range 0 to 11             */
    int tm_year;        /* The number of years since 1900   */
    int tm_wday;        /* day of the week, range 0 to 6    */
    int tm_yday;        /* day in the year, range 0 to 365  */
    int tm_isdst;       /* daylight saving time             */
};
```

### 返回值

如果结果的 C 字符串小于 size 个字符（包括终止空字符），则返回复制到 str 的总字符数（不包括终止空字符），否则返回零。

### 示例

以下示例展示了 strftime() 函数的用法。

```c
#include <stdio.h>
#include <time.h>

int main ()
{
    time_t rawtime;
    struct tm *info;
    char buffer[80];

    time( &rawtime );

    info = localtime( &rawtime );

    strftime(buffer,80,"%x - %I:%M%p", info);
    printf("Formatted date & time : |%s|\n", buffer );

    return(0);
}
```

让我们编译并运行上面的程序，它将产生以下结果：

```text
Formatted date & time : |08/23/12 - 12:40AM|
```

## time_t time(time_t \*timer)

### 描述

C 库函数 `time_t time(time_t *seconds)` 返回自纪元（1970 年 1 月 1 日 00:00:00 UTC）以来经过的秒数。如果 seconds 不为 NULL，则返回值也会存储在变量 seconds 中。

### 声明

以下是 time() 函数的声明。





```
time_t time(time_t *)
```

### 参数

- **seconds** -- 指向 `time_t` 类型对象的指针，秒值将存储在该对象中。

### 返回值

以 `time_t` 对象表示的当前日历时间。

### 示例

以下示例演示了 `time()` 函数的用法。

```
#include <stdio.h>
#include <time.h>

int main ()
{
    time_t seconds;

    seconds = time(NULL);
    printf("Hours since January 1, 1970 = %ld\n", seconds/3600);

    return(0);
}
```

让我们编译并运行上述程序，将产生以下结果：

```
Hours since January 1, 1970 = 393923
```

