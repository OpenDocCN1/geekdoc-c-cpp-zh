
# 字符串与字符数组

## 7.4 数组、指针与字符串

| 5 | `main()` | • 函数原型存在于头文件 `string.h` 中 |
|---|---|---|
| 6 | `{` | |
| 7 | `printf("Length of string literal \"xyz\" is %d characters"` | |

**Program 7-2** | 一个查找字符串长度的程序

**8. 长度为零的字符串常量被称为空字符串。** 空字符串写作 `""`，即双引号内没有包含字符。虽然空字符串的长度为零，但它在内存中占用 1 个字节来存储空字符。

**9. 在C语言中，没有字符串类型，使用字符指针来表示字符串。** 因此，字符串字面量的类型（例如 `"xyz"`）是 `const char*`。常量指针指向字符串第一个元素的地址。以这种方式表示和解释的字符串被称为C风格字符字符串。程序 7-3中的代码片段说明了字符串字面量会分解为指针。

**Prog 7-3.c**

| Line | 输出窗口 |
|---|---|
| 1 | `//C-style strings are represented by char*` | 字符串的第一个字符是 x |
| 2 | `#include<stdio.h>` | 字符串的第二个字符是 y |
| 3 | `main()` | 备注: |
| 4 | `{` | |
| 5 | `printf("The first character of string \"xyz\" is %c",*("xyz"));` | • 字符串字面量的类型是 `const char*` |
| 6 | `printf("The second character of string \"xyz\" is %c",*("xyz"));` | • 因此，解引用 `"xyz"` 输出 x |
| 7 | `}` | |

**Program 7-3** | 一个说明字符串字面量指向的程序

### 7.4 数组、指针与字符串

10. 由于字符串字面量是指常量指针且没有可修改的左值，只有适用于常量指针的操作才能应用于C风格字符串。对字符串字面量应用任何其他运算符都会导致 `'L-value'` 错误。程序 7-4说明了这一事实。

**Prog 7-4.c**

| Line | 输出窗口 |
|---|---|
| 1 | `//String literal refers to constant pointer` | 编译错误 "L-value" |
| 2 | `#include<stdio.h>` | |
| 3 | `main()` | 备注: |
| 4 | `{` | |
| 5 | `printf("The first character of string literal \"xyz\" is %c",*xyz++);` | • `"*xyz++"` 将解释为 `*(xyz++)` |
| 6 | `}` | |

**Program 7-4** | 一个说明字符串指向常量指针且没有可修改的左值的程序

11. 由于C风格字符串类型为 `char*`，可以赋值或初始化字符指针变量。以下语句是有效的：

```
char *string = "Strings!!!";
string = "Strings!!!";
```

12. 相邻的字符串常量会被连接。这种连接是在预处理阶段进行的。程序 7-5说明了这一事实。

**Prog 7-5.c**

| Line | 输出窗口 |
|---|---|
| 1 | `//Adjacent string literal constants get concatenated` | GOD Bless us!!! |
| 2 | `#include<stdio.h>` | 备注: |
| 3 | `main()` | |
| 4 | `{` | |
| 5 | `printf("God Bless %s", "!!!");` | • 第5行的相邻字符串字面量会被连接并打印 |
| 6 | `}` | |

**Program 7-5** | 一个说明相邻字符串字面量常量会被连接的程序

## 7.3 字符数组

整数变量可以存储整数常量的值。例如，语句 `int a=10;` 创建了一个存储整数 10 的变量。同样，`float` 变量可以存储浮点常量，现在字符变量可以用来存储字符了。这里出现的问题是：“我们能创建一个可以存储字符串字面量的变量吗？”对这个问题的答案是肯定的！我们可以创建 `char[]` 类型（即字符数组）的变量来存储字符串常量。

## 7.5 字符串与字符数组

字符串变量或字符数组定义的通用形式：

`<s_class_specif><type_qualifier><type_modifier>char identifier[size_specifier]=initialization_OR string literal;`

关于字符串变量声明的重要点如下：

1. 尖括号（即 `<>`）内的术语是可选的，在声明语句中可能不存在。**粗体**显示的术语是字符串变量声明的强制部分。
2. 由于字符串变量是一个字符数组，因此第 6 章讨论的所有用于数组的语法规则也适用于字符串变量的声明。
3. 如果显式初始化字符串变量，则大小规格是可选的。
4. 字符串变量或字符数组可以通过两种方式进行初始化：
   - a. 使用字符串字面量：在声明语句 `str[6]="Hello";` 中，字符数组或字符串变量 `str` 使用字符串字面量 `"Hello"` 初始化。它将如图 7.2 所示存储在内存中。
   - b. 使用初始化列表：初始化字符数组的另一种方法是使用字符初始化列表。声明语句 `str[6]={'H','e','l','l','o','\0'};` 使用字符初始化器初始化字符数组 `str` 的位置。字符数组 `str` 将以图 7.2 所示的方式存储在内存中。

```
char str[6]="Hello"; or str[6]={'H','e','l','l','o','\0'};
str
| H | e | l | l | o | \0 |
|---|---|---|---|---|---|
| 2000 | 2001 | 2002 | 2003 | 2004 | 2005 |
```

**图 7.2** | 初始化字符串变量或字符数组的两种不同方式

> 当使用字符列表初始化字符数组时，必须显式放置终止字符；当使用字符串字面量初始化时，会自动放置终止空字符（如果字符数组的大小比字符串字面量的长度大一）。

## 7.4 终止空字符的重要性

字符串中的终止空字符非常重要。每个字符串操作都会检查空字符是否存在，以确定字符串的结束。考虑程序 7-6 中的代码片段，它说明了字符串中终止空字符的重要性。

## 7.6 数组、指针与字符串

| 行 | Prog 7-6 | 输出窗口 |
|---|---|---|
| 1 | `//终止空字符的重要性` | The string is Hello$ |
| 2 | `#include<stdio.h>` | Its length is 10 |
| 3 | `#include<string.h>` | 备注： |
| 4 | `main()` | * `printf` 函数和 `puts` 函数从其参数指向的内存位置开始打印字符，直到遇到终止空字符 |
| 5 | `{` | * 在第 6 行中，数组使用字符列表初始化，且没有在末尾显式放置空字符 |
| 6 | `char str[5]={'H','e','l','l','o'};` | * 如果数组没有以空字符终止，则字符串的输出将是不确定的，并取决于空字符出现的位置 |
| 7 | `printf("The string is %s\n",str);` | * 因此，第 8 行中的 `puts` 函数而 `printf` 会产生垃圾值（任何任意值），因为它从其参数指向的内存位置（即 4000）开始并持续打印直到遇到终止空字符 |
| 8 | `puts(str);` | * 输出中垃圾字符的数量取决于遇到第一个空字符的位置 |
| 9 | `printf("Its length is %d\n",strlen(str));` | * 在不同时间或不同机器上执行相同的代码可能会产生不同的输出（即 Hello 后面跟着和/或不同数量的垃圾字符） |
| 10 | `}` | * `strlen` 通过计算从其参数指向的内存位置开始直到遇到空字符的字符数来确定字符串长度。在确定字符串长度时不计算终止空字符。 |

| 内存内容 |
|---|
| str |
| H | e | l | l | o | G | G | G | G | \0 |
| 4000 | | | | | | | | | 4010 |

| 行 | Prog 7-6.c | 输出窗口 |
|---|---|---|
| | | * 当使用字符初始化器初始化字符数组，或使用 `scanf` 和 `gets` 函数从用户处读取字符串时，空字符会自动放置在字符数组末尾 |

**Program 7-6** | 用于说明字符串中终止空字符重要性的程序

## 7.5 字符串库函数

C 字符串库提供了许多可用于字符串处理的函数。常用的 C 字符串库函数见表 7.1。

**表 7.1** | C 字符串库函数

| 序号 | 函数名 | 原型 | 作用 |
|---|---|---|---|
| 1 | `strlen` | `int strlen(char* s);` | 计算字符串 s 的长度 |
| 2 | `strcpy` | `char* strcpy(char* dest, const char* src);` | 将源字符串拷贝到目标字符串 dest |
| 3 | `strcat` | `char* strcat(char* dest, const char* src);` | 将字符串 src 附加到字符串 dest 的末尾 |
| 4 | `strcmp` | `int strcmp(char* s, const char* s2);` | 比较两个字符串 |
| 5 | `strncmp` | `int strncmp(char* s, const char* s2);` | 不区分大小写地比较两个字符串 |
| 6 | `strrev` | `char* strrev(char* s);` | 反转字符串的内容 |
| 7 | `strlower` | `char* strlower(char* s);` | 将字符串转换为小写 |
| 8 | `strupr` | `char* strupr(char* s);` | 将字符串转换为大写 |
| 9 | `strset` | `char* strset(char* s, int ch);` | 将字符串 s 中的所有字符设置为 ch |
| 10 | `strchr` | `char* strchr(char* s, int c);` | 扫描字符串 s 中字符 c 第一次出现的位置 |
| 11 | `strrchr` | `char* strrchr(char* s, int c);` | 找到字符最后一次出现的位置 |
| 12 | `strstr` | `char* strstr(char* s, const char* s2);` | 在另一个字符串（即 s）中找到子串（即 s2）的第一次出现的位置 |
| 13 | `strncpy` | `char* strncpy(char* dest, const char* src, int n);` | 将字符串 src 的前 n 个字符拷贝到字符串 dest |
| 14 | `strncat` | `char* strncat(char* dest, const char* src, int n);` | 将字符串 src 的前 n 个字符附加到字符串 dest |
| 15 | `strncmp` | `int strncmp(char* s, const char* s2, int n);` | 比较两个字符串 s 和 s2 的前 n 个字符 |

以下小节说明了上述字符串库函数与自定义函数的使用。

## 7.8 数组、指针与字符串

### 7.5.1 `strlen` 函数

**作用**：`strlen` 函数用于找到字符串的长度。

**输入**：`strlen` 函数的输入可以是字符串字面量、字符数组或指向它的字符指针。

**输出**：`strlen` 函数返回终止空字符之前的字符数。在确定字符串长度时不计算终止空字符。

**用法**：程序 7-7 中的代码片段说明了 `strlen` 函数的使用和字符串的功能。

| Prog 7-a.c 使用库函数 | Prog 7-b.c 使用自定义函数 | 输出窗口 |
|---|---|---|
| 1 | `//字符串的长度` | `//字符串的长度` | 字符串长度： |
| 2 | `#include<stdio.h>` | `#include<stdio.h>` | Hello is 5 |
| 3 | `#include<string.h>` | `int mystrlen(char* s);` | Dear is 4 |
| 4 | `main()` | `main()` | Reader is 6 |
| 5 | `{` | `{` | 备注： |
| 6 | `char *ptr="Dear";` | `char *ptr="Dear";` | • `strlen` 函数返回 |
| 7 | `char name[50]="Reader";` | `char name[50]="Reader";` | 终止空字符之前的字符数。 |
| 8 | `printf("length of strings:\n");` | `int i=0;` | • 如果字符串末尾没有终止字符 |
| 9 | `printf("Hello is %d\n",strlen(ptr));` | `while(*s+i)!='\0')` | 则 `strlen` 函数给出一个二元结果 |
| 10 | `printf("Reader is %d\n",strlen(name));` | `i++;` | |
| 11 | `}` | `return i;` | |
| 12 | | `}` | |

**程序 7-7** | 一个使用库函数 (a) 和 (b) 自定义函数查找字符串长度的程序

### 7.5.2 `strcpy` 函数

**作用**：`strcpy` 函数将源字符串拷贝到目标字符串。

**输入**：源字符串和目标字符串。源字符串可以是字符串字面量、字符数组或指向它的字符指针。目标应该是字符数组或指向要拷贝源字符串的内存位置的字符指针。

**输出**：`strcpy` 函数将源字符串拷贝到目标字符串并返回指向目标字符串的指针。

| | Prog 7-8a.c | Prog 7-8b.c | 输出窗口 |
|---|---|---|---|
| | 使用库函数 | 使用用户定义函数 | |
| 1 | `//Copying one string to another` | `//Copying one string to another` | 源字符串是 |
| 2 | `#include<stdio.h>` | `#include<stdio.h>` | Hello |
| 3 | `#include<string.h>` | `char* strcpy(char* dest, const char* src);` | 目标字符串是 |
| 4 | `main()` | `main();` | Hello |
| 5 | `{` | `{` | 备注: |
| 6 | `char src[50]="Hello";` | `char src[50]="Hello";` | * 如果源字符串中的字符 |
| 7 | `char dest[50];` | `char dest[50];` | 字符数量大于 |
| 8 | `puts("Source string is");` | `puts("Source string is");` | 目标字符串能够容纳的 |
| 9 | `puts(src);` | `puts(src);` | 字符数量，则内存 |
| 10 | `strcpy(dest,src);` | `strcpy(dest,src);` | |
| 11 | `puts("Destination string is");` | `puts("Destination string is");` | |
| 12 | `puts(dest);` | `puts(dest);` | |
| 13 | `}` | `char* strcpy(char* dest, const char* src)` | |
| 14 | | `{` | |
| 15 | | `int i=0;` | |
| 16 | | `while(src[i]!='\0')` | |
| 17 | | `{` | |
| 18 | | `dest[i]=src[i];` | |
| 19 | | `i++;` | |
| 20 | | `}` | |
| 21 | | `//Null character should be explicitly placed at` | |
| 22 | | `//the end of the string.` | |
| 23 | | `dest[i]='\0';` | |
| 24 | | `return dest;` | |
| 25 | | `}` | |
| 26 | | | |

**程序 7-8** 一个复制字符串的程序，(a) 使用库函数，(b) 使用用户定义函数。字符指针指向应该足够大以容纳源字符串。如果空间不足，可能会发生运行时异常。更多信息请参见问题 12 及其答案。

## 7.5.3 `strcpy` 函数
