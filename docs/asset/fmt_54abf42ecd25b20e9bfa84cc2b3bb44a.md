
## 7.22 数组、指针与字符串

### 7.5.15 strcmp 函数

**作用：**

`strcmp` 函数比较两个字符串的片段。

**输入：**

两个字符串 `str1` 和 `str2` 以及数值 `n` 的值，即要比较的字符数。

**输出：**

`strcmp` 函数对 `str1` 和 `str2` 进行比较，从每个字符串的第一个字符开始，继续比较随后的字符，直到对应的字符不同、到达字符串末尾或已比较了 `n` 个字符为止。它返回第一个不同字符的 ASCII 值；如果两个字符串中的 `n` 个字符均不相同，则返回 0。

程序 7-21 中的代码段说明了 `strcmp` 函数的使用以及自定义函数的开发。

**用法：**

| 行号 | Prog 7-21a.c 使用库函数 | Prog 7-21b.c 使用自定义函数 | 输出窗口 |
|---|---|---|---|
| 1 | //比较两个字符串的片段 | //比较两个字符串的片段 | 输入字符串 1: |
| 2 | `#include<stdio.h>` | `#include<stdio.h>` | Hello |
| 3 | `#include<string.h>` | `int strcmp(const char* s1, const char* s2, int n)` | 输入字符串 2: |
| 4 | `main()` | | Hello |
| 5 | `{` | `}` | I |
| 6 | `char str1[20],str2[20];` | `char str1[20],str2[20];` | 输入 n 的值: |
| 7 | `int n;` | `int n;` | I |
| 8 | `puts("Enter string 1:");` | `puts("Enter string 1:");` | 字符串片段相等 |
| 9 | `gets(str1);` | `puts("Enter string 2:");` | |
| 10 | `gets(str2);` | `gets(str2);` | (第二次执行) |
| 11 | `puts("Enter the value of n:");` | | 输入字符串 1: |
| 12 | `scanf("%d",&n);` | `res=strcmp(str1,str2);` | Hello |
| 13 | | `if(res==0) {` | 输入字符串 2: |
| 14 | `res=strcmp(str1,str2);` | `puts("String portions are equal");` | Hello |
| 15 | `if(res==0)` | `else` | 输入 n 的值: |
| 16 | `puts("String portions are equal");` | `puts("String portions are not equal");` | 4 |
| 17 | `else` | `}` | 字符串片段相等 |
| 18 | `puts("String portions are not equal");` | `}` | 输出窗口 |
| 19 | `}` | | (第三次执行) |
| 20 | | `return 0;` | `return 0;` | 输入字符串 1: |
| 21 | | `int i=0;` | Hello |
| 22 | | `while(str1[i] != str2[i] && i<66) {` | HELLO |
| 23 | | `if(str1[i]!=str2[i]) {` | 3 |
| 24 | | `return(str1[i]-str2[i]);` | 字符串片段不等 |
| 25 | | `i++;` | | |
| 26 | | `}` | | |
| 27 | | `}` | | |

**程序 7-21** 该程序用于比较两个字符串的片段：(a) 使用库函数和 (b) 使用自定义函数。

### 7.5.16 strncmp 函数

**作用：**

`strncmp` 函数在不区分大小写的情况下比较两个字符串的片段。

**输入：**

两个字符串 `str` 和 `str2` 以及数值 `n` 的值，即要比较的字符数。

**输出：**

`strncmp` 函数在不区分大小写的情况下对 `str` 和 `str2` 进行比较，从每个字符串的第一个字符开始，继续比较随后的字符，直到对应的字符不同、到达字符串末尾或已比较了 `n` 个字符为止。它返回第一个不同字符的 ASCII 差异；如果字符串相同，则返回 0。

**用法：**

程序 7-22 中的代码段说明了 `strncmp` 函数的使用以及 `strncmp` 功能的开发。

**程序 7-22** 该程序在不区分大小写的情况下比较两个字符串的片段：(a) 使用库函数和 (b) 使用自定义函数。

## 7.24 数组、指针与字符串

### 7.5.17 strnset 函数

**作用：**

`strnset` 函数将字符串中的前 `n` 个字符设置为特定字符。

**输入：**

一个字符串、一个字符和一个整数值 `n`。

`strnset` 函数将字符串中的前 `n` 个字符设置为指定的字符，并返回指向字符串的指针。

**用法：**

程序 7-23 中的代码段说明了 `strnset` 函数的使用以及 `strnset` 功能的开发。

| Prog 7-23a.c | Prog 7-23b.c | 输出窗口 |
|---|---|---|
| 使用库函数 | 使用自定义函数 | |
| //设置字符串的前 n 个字符 | //设置字符串的前 n 个字符 | 输入 n 的值: |
| // 为特定字符 | // 为特定字符 | Hello!! |
| `#include<stdio.h>` | `#include<stdio.h>` | 输入字符: |
| `#include<string.h>` | `char* strnset(char* s, int ch, int n);` | X |
| `main()` | `main()` | 输入 n 的值: |
| `{` | `{` | S |
| `char str[20];` | `char str[20];` | 使用 strnset 前，字符串为: |
| `int n;` | `int n;` | Hello!! |
| `puts("Enter the string:");` | `puts("Enter the string:");` | 使用 strnset 后，字符串为: |
| `gets(str);` | `gets(str);` | XXXXX!! |
| `puts("Enter the character:");` | `puts("Enter the character:");` | 备注: |
| `scanf("%d", &n);` | `scanf("%d", &n);` | 如果字符串的长度 |
| `puts("Enter the value of n:");` | `puts("Enter the value of n:");` | 小于 n 的值， |
| `scanf("%d", &n);` | `scanf("%d", &n);` | 则 `strnset` 函数 |
| `puts("After using strnset(), string is: ");` | `puts("After using strnset(), string is: ");` | 将字符串的前 |
| `puts(str);` | `puts(str);` | 所有字符设置为 |
| `strnset(str, ch, n);` | `strnset(str, ch, n);` | 字符串的 |
| `puts("After using strnset(), string is: ");` | `puts("After using strnset(), string is: ");` | 特定字符 |
| `puts(str);` | `puts(str);` | 字符 |
| `}` | `}` | |
| | `char* strnset(char* s, int ch, int n);` | |
| | `int i=0;` | |
| | `while(s[i] != '\0' && i<n)` | |
| | `{` | |
| | `s[i]=ch;` | |
| | `i++;` | |
| | `}` | |
| | `return s;` | |
| | `}` | |

**程序 7-23** 该程序用于将字符串的前 `n` 个字符设为特定字符：(a) 使用库函数和 (b) 使用自定义函数。

## 7.6 字符串列表

在之前的节中，我们学习了如何在字符数组中存储字符串以及用于处理字符串的函数。然而，实际应用需要存储和处理多个字符串（即字符串列表），而不仅仅是一个字符串。字符串列表可以通过两种方式存储：

1. 使用字符串数组
2. 使用字符指针数组

### 7.6.1 字符串数组

如果应用程序需要存储多个字符串，可以使用字符串数组来存储。由于字符串本身存储在一维字符数组中，可以通过创建一维字符数组数组（即二维字符数组）来存储字符串列表。图 7.3 展示了一个字符串数组。

| R | a | m | a | n | \0 | ←第1 个字符串 |
|---|---|---|---|---|---|---|
| S | a | m | \0 | | | ←第2 个字符串 |
| V | i | s | h | \0 | | ←第3 个字符串 |
| N | e | h | a | \0 | | ←第4 个字符串 |

**图 7.3** 字符串数组

#### 7.6.1.1 字符串数组的声明

字符串数组的通用形式为：

`<class_specifier><type_qualifier><type_modifier>{row_specifier][column_specifier]=initialization_list>;`

关于字符串数组声明的重要点如下：

1. 字符串数组声明由 `char` 类型说明符、标识符名称、行大小和列大小组成。以下声明是有效的：

```c
char array[2][30]; // 数组可以存储2个最多30个字符的字符串
char array[2][5];  // 数组可以存储5个最多5个字符的字符串
```

2. 第 6 章中讨论的所有声明二维数组的语法规则也适用于字符串数组的声明。

3. 字符串数组的初始化：字符串数组可以通过两种方式初始化：

   a. 使用字符串字面量：使用字符串字面量可以初始化字符串数组：

   ```c
   char str[4][20]={
       "Raman",
       "Sam",
       "Vishal",
       "Neha",
   };
   ```

   b. 使用字符初始化列表：使用字符初始化列表可以初始化字符串数组：

   ```c
   char str[][20]{
       {'R','a','m','a','\n','\0'},
       {'S','a','m','\0'},
       {'V','y','s','t','h','a','\n','\0'},
       {'N','e','h','a','\0'}
   };
   ```

#### 7.6.1.2 从终端读取字符串列表

可以通过迭代调用 `gets` 或 `scanf` 函数从终端读取字符串列表。程序 7-24 从终端读取字符串列表并将其存储在字符串数组中。

| 行号 | Program 7-24.c | 输出窗口 |
|---|---|---|
| 1 | //从终端读取字符串列表 | 输入学生姓名和分数: |
| 2 | `#include<stdio.h>` | Praveen 89 |
| 3 | `main()` | 你想继续输入吗(Y/N) Y |
| 4 | `{` | Ashok 80 |
| 5 | `int i=0` | |

**程序 7-24** 该程序演示了读取字符串列表的方法。

### 7.6.2 字符指针数组

字符串数组也可以使用字符指针数组来存储。字符串的起始地址存储在字符指针数组中，如图 7.4 所示。

**图 7.4** 使用字符指针数组存储字符串列表

#### 7.6.2.1 字符指针数组的使用

程序 7-25 演示了如何使用字符指针数组存储字符串列表。

| 行号 | Prog 7-25.c | 输出窗口 | 州府 |
|---|---|---|---|
| 1 | //使用字符指针数组 | 邦 | 1. Gandhinagar |
| 2 | `#include<stdio.h>` | 1. Punjab | 2. Chandragadh |
| 3 | `main()` | 2. Bihar | 3. Jaipur |
| 4 | | 3. Rajasthan | 4. Patna |
| 5 | `int i[4];` | 4. Gujarat | |
| 6 | `char* states[]={"Punjab", "Bihar", "Rajasthan", "Gujarat"};` | | 匹配列 1 中的字符串与列 2 中的州府 |
| 7 | `char* capitals[]={"Gandhinagar", "Chandragadh", "Jaipur", "Patna"};` | | (仅输入序号) |
| 8 | `printf("%s\n",states[i]);` | | 州 1 的州府在 2 |
| 9 | | | 州 2 的州府在 4 |
| 10 | `for(i=0;i<4;i++)` | | 州 3 的州府在 3 |
| 11 | `printf("%s:%s\n",states[i],i+1,capitals[i]);` | | 州 4 的州府在 1 |
| 12 | `printf("Match st in Col. 1 with capitals in Col. 2:\n");` | | |
| 13 | `printf("Enter only Sr. Nos.\n");` | | Chandragadh 是 Punjab 的州府 |
| 14 | | | Patna 是 Bihar 的州府 |
| 15 | `for(i=0;i<4;i++)` | | Jaipur 是 Rajasthan 的州府 |
| 16 | | | Gandhinagar 是 Gujarat 的州府 |
| 17 | `printf("Capital of state %d is at\t%s\n",i+1,capitals[i]);` | | 备注： |
| 18 | `scanf("%d",&i);` | | - 字符串列表使用字符指针数组 |
| 19 | `}` | | 存储在第 6 和 7 行 |
| 20 | `printf("--------------------------------------\n");` | | |
| 21 | `for(i=0;i<4;i++) {` | | | |
| 22 | `printf("--------------------------------------\n"); printf("-%s is capital of %s\n",capitals[i-1],states[i]);` | | | |
| 23 | `}` | | | |

**程序 7-25** 一个演示使用字符指针数组的程序

## 7.7 命令行参数

在第 8 章中，我们将看到通过参数向函数提供输入。`main` 也是一个函数。因此，我们也可以通过提供参数给函数 `main` 提供输入吗？问题的答案是肯定的！函数 `main` 的输入是通过使用称为命令行参数的特殊参数提供的。

如果你有 DOS，你一定用过 `copy source_file.txt dest_file`。`copy` 命令看起来如下：

```
copy source_file.txt dest_file
```

对于程序来说，源文件名（即 `source_file.txt`）和目标文件名（即 `dest_file.txt`）是作为输入的。这些输入是在命令行或命令提示符提供的，被称为命令行参数。

C 提供了一种非常简单的机制来获取用户在命令行输入的行参数。要获取命令行参数，应该这样定义函数 `main`：
