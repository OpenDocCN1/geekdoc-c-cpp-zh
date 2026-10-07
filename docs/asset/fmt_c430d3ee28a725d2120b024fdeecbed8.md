
```c
switch (operationCode) {
    case read:
        scanf("%d", &operand);
        // 打印寄存器和内存
        break;
    case write:
        memory[operand] = ...; // 伪代码
        break;
}
```

此时，`Simpleton` 必须判断操作码实际上是“读取”（而不是“写入”等）。通过一个 `switch` 语句区分了 `SMALL` 的两种操作。该 `switch` 语句模拟了虚拟 `SMALL` 指令的行为（其他部分留给读者自行实现）：

```c
switch (operationCode) {
    case read:
        scanf("%d", &operand);
        // 打印寄存器和内存
        break;
    case write:
        memory[operand] = ...; // 伪代码
        break;
}
```

在 `switch` 语句中，我们可以区分不同的操作码：

```c
if (operationCode == read) {
    // 执行读取
}
```

实际上，由于原始文本包含大量重复且不完全的片段，我已根据您的逻辑要求进行了精简的翻译和对齐。以下是核心逻辑的翻译呈现：

```c
if (operationCode == read) {
    printf("%+05d", operand);
}
```

# 332 第 7 章 C 指针

`(int)`，每行对应 `topics` 数组中的一个元素。当程序运行时，它应该要求用户对每个问题进行评分。让你的朋友和家人参与调查。然后让程序显示结果的摘要，包括：

- a) 一个表格报告，左侧为五个个主题，顶部为 10 级评分分级，每列列出每个主题收到的评分次数。
- b) 在每行的右侧，显示该问题的评分平均值。
- c) 哪个问题的总分最高？同时显示该问题和总分。
- d) 哪个问题的总分最低？同时显示该问题和总分。

**7.33 (碳足迹计算器：函数指针数组)** 正如你在本章中学到的那样，使用函数指针数组，你可以指定一组具有相同类型参数并返回相同类型数据的函数。全球政府和公司日益关注碳足迹（由于燃烧各种类型燃料供热的建筑、燃烧燃料动力的车辆等，每年向大气中排放的二氧化碳）。全球全球变暖。创建三个函数，分别帮助计算建筑、汽车和自行车的碳足迹。每个函数应该从用户处输入适当的数据，然后计算并显示碳足迹。（查看几个解释如何计算碳足迹的网站。）每个函数应不接收参数并返回 `void`。编写一个程序提示用户输入要计算的碳足迹类型，然后调用函数指针数组中的相应函数。对于每种碳足迹，显示一些标识信息和对象的碳足迹。

## C 字符与字符串

# 目标

在本章中，你将：

- 使用字符处理库（`<ctype.h>`）的函数。
- 使用通用实用库（`<stdlib.h>`）的字符串转换函数。
- 使用标准输入输出库（`<stdio.h>`）的字符串和字符输入输出函数。
- 使用字符串处理库（`<string.h>`）的字符串处理函数。
- 使用字符串处理库（`<string.h>`）的内存处理函数。

![](img/fa81e30d8bce030c9060826ba9997d7b_365_0.png)

## 第 8 章 C 字符与字符串

- 8.1 引言
- 8.2 字符串与字符处理库基础
- 8.3 处理库
- 8.1 isdigit, isalpha, isnum and isdigit
- 8.2 islower, ispper, tolower
- 8.3 isspace, iscntrl, ispunct, isprint and isgraph
- 8.4 字符串转换函数
- 8.1 strtod
- 8.2 strtol
- 8.3 strtoull
- 8.5 标准输入输出库函数
- 8.1 fgets and putchar
- 8.2 getchar
- 8.3 sprintf
- 8.4 scanf
- 8.6 字符串处理库的字符串操作函数
- 8.1 strcpy and strncpy
- 8.2 strcat and strncat
- 8.7 字符串处理库的比较函数
- 8.8 字符串处理库的搜索函数
- 8.1 func strchr
- 8.2 func strcsp
- 8.3 func strbrk
- 8.4 func strchr
- 8.5 func strspn
- 8.6 func strstr
- 8.7 func strtok
- 8.9 字符串处理库的内存函数
- 8.1 func memcpy
- 8.2 func memmove
- 8.3 func memcmp
- 8.4 func memchr
- 8.5 func memset
- 8.10 字符串处理库的函数
- 8.1 func strerror
- 8.2 func strlen
- 8.11 安全 C 编程

总结 | 自测练习 | 自测练习答案 | 练习题 | 特别章节：高级字符串操作练习题 | 一个具有挑战性的字符串操作项目 | 改变自我

## 8.1 引言

本章介绍了 C 标准库函数，这些函数可以帮助我们处理字符串和字符。这些函数使程序能够处理字符、字符串、文本行和内存块。本章讨论了用于开发编辑器、文字处理器、页面布局软件、计算机排字系统和其他类文本处理软件的技术。文本操作通过格式化输入输出函数（如 `printf` 和 `scanf`）完成，这些函数可以使用本章讨论的函数来实现。

### C11 附件 K 函数

正如我们在 8.1 节中所述，C11 的附件 K 描述了本章介绍的许多函数的更安全版本。对于 `printf` 和 `scanf`，使用了 `printf_s` 和 `scanf_s`，如果你的编译器可用，则应使用更安全的附件 K 版本。

## 8.2 字符串与字符基础

字符是字符串程序的根本构建模块。每个程序都由字符序列组成——当这些字符有意义地组合在一起时，计算机将其解释为用于完成任务的一系列指令。程序可能包含字符常量。字符常量是用单引号括起来的字符表示的 `int` 值。字符常量的值是该字符在机器字符集中的整数值。例如，`'z'` 代表字母 z 的整数值，而 `'\n'` 代表换行的值（122 和 10）。

字符常量的值是该字符在机器字符集中的整数值。例如，`'z'` 代表字母 z 的整数值，而 `'\n'` 代表换行的值（122 和 10）。

在 C 中，字符串用引号写如下：

- "John Doe"
- "99 Main Street"
- "Waltham, Massachusetts"
- "(201) 555-1212"

字符串是以空字符结尾的字符序列。字符串可以通过指针访问。因此，在 C 中，字符串可以初始化为：

```c
char color[] = "blue";
```

前面的定义指向了字符串。

### 可移植性提示 8.1

标准指示字符串字面量是不可变的（即不可修改），但某些编译器并不强制执行。![](img/fa81e30d8bce030c9060826ba9997d7b_365_0.png)

前面的语句确定了：

```c
char color[] = {'b', 'l', 'u', 'e', '\0'};
```

在字符数组中存储字符串时，确保数组足够大以便存放最大的字符串。使用 `scanf` 时，字段宽度 19 确保 `scanf` 最多读取 19 个字符并为字符串的终止空字符留空间。为了让字符数组作为字符串正确打印，它必须包含空字符。

### 编程错误 8.2

打印不包含空字符的字符串将越过数组边界。

### 编程错误 8.3

将单个字符作为字符串处理。是一个指针——可能是一个很大的整数。然而，字符是一个小整数（ASCII 值 0–255）。许多系统会导致错误，因为低内存地址留给了特殊用途，例如操作系统中断处理程序——所以会发生“访问冲突”。

### 编程错误 8.4

在期望字符串时向函数传递字符（反亦然）会导致编译错误。

### 错误预防 8.1

在字符数组中存储字符串时，使用 `scanf`：

```c
scanf("%19s");
```

## 8.3 字符处理库

字符处理库 `<ctype.h>` 包含了几个对字符数据进行测试和操作的函数。每个函数接收一个 `unsigned char`（表示为 `int`）或 `EOF` 作为参数。正如我们在第4 章中讨论过的，字符通常作为整数处理，因为 C 中的字符是一个单字节整数。`EOF` 通常值为 -1。图 8.1 总结了字符处理库的函数。

### 8.3.1 函数 isdigit, alpha, isnum and isdigit

图 8.2 展示了 `isdigit, alpha, isnum and isdigit`。`isdigit` 函数确定其参数是否为数字（0–9）。`isalpha` 函数确定其参数是否是大写字母（A–Z）或小写字母（a–z）。`isnum` 函数

## 8.3 字符处理库

| 原型 | 函数描述 |
| --- | --- |
| `int isblank(int c);` | 如果 c 是文本行中分隔单词的空白字符，则返回真值，否则返回 0（假）。[*注：此函数在 Microsoft Visual C++ 中不可用]。* |
| `int isdigit(int c);` | 如果 c 是数字，则返回真值，否则返回 0（假）。 |
| `int isalpha(int c);` | 如果 c 是字母，则返回真值，否则返回 0（假）。 |
| `int isalnum(int c);` | 如果 c 是数字或字母，则返回真值，否则返回 0（假）。 |
| `int isxdigit(int c);` | 如果 c 是十六进制数字，则返回真值，否则返回 0（假）。关于二进制、八进制、十进制和十六进制的详细解释请参见附录 C。） |
| `int islower(int c);` | 如果 c 是小写字母，则返回真值，否则返回 0（假）。 |
| `int isupper(int c);` | 如果 c 是大写字母，则返回真值，否则返回 0（假）。 |
| `int tolower(int c);` | 如果 c 是大写字母，tolower 返回 c 的小写形式。否则，tolower 返回原参数不变。 |
| `int toupper(int c);` | 如果 c 是小写字母，toupper 返回 c 的大写形式。否则，toupper 返回原参数不变。 |
| `int isspace(int c);` | 如果 c 是空白字符——换行 ('\n')、空格 (' ')、分页符 ('\f')、回车 ('\r')、水平制表符 ('\t') 或垂直制表符 ('\v')——则返回真值，否则返回 0（假）。 |
| `int iscntrl(int c);` | 如果 c 是控制字符——水平制表符 ('\t')、垂直制表符 ('\v')、分页符 ('\f')、警铃 ('\a')、退格 ('\b')、回车 ('\r')、换行 ('\n') 等——则返回真值，否则返回 0（假）。 |
| `int ispunct(int c);` | 如果 c 是除空格、数字或字母以外的打印字符——例如 $, &, (, ), [, ], {, }, \； : 或 %——则返回真值，否则返回 0。 |
| `int isprint(int c);` | 如果 c 是打印字符（即在屏幕上可见的字符），包括空格，则返回真值，否则返回 0（假）。 |
| `int isgraph(int c);` | 如果 c 是除空格以外的打印字符，则返回真值，否则返回 0（假）。 |

**图 8.1** 字符处理库 (`<ctype.h>`) 函数。`isalnum` 判断参数是否为大写字母、小写字母或数字。`isxdigit` 判断参数是否为十六进制数字（A–F, a–f, 0–9）。

```c
// 图 8.2: fig08_2.c
// 使用 isdigit, alpha, isalnum, isxdigit 函数
#include <stdio.h>
#include <ctype.h>
int main(void)
{
```

**图 8.2** 使用 `isdigit, alpha, isalnum, isxdigit` 函数（第 2 部分）。

# 第 8 章 字符与字符串

```c
    printf("%s\n%s\n%s\n\n", "According to isdigit:",
           isdigit('8') ? "8 is a digit" : "8 is not a digit",
           isdigit('#') ? "# is not a digit" : "digit");

    printf("\n%s\n%s\n%s\n%s\n\n", "According to isalpha:",
           isalpha('A') ? "A is a letter" : "not a letter",
           isalpha('b') ? "b is a letter" : "not a letter",
           isalpha('!') ? "! is not a letter" : "letter",
           isalpha('4') ? "4 is not a letter" : "letter");

    printf("%s\n%s\n%s\n%s\n\n", "According to isalnum:",
           isalnum('A') ? "A is a digit or a letter" : "not a digit or letter",
           isalnum('8') ? "8 is a digit or a letter" : "not a digit or letter",
           isalnum('#') ? "# is not a digit or letter" : "digit or letter");

    printf("%s\n%s\n%s\n%s\n%s\n", "According to isxdigit:",
           isxdigit('F') ? "F is a hexadecimal digit" : "not a hexadecimal digit",
           isxdigit('J') ? "J is not a hexadecimal digit" : "hexadecimal digit",
           isxdigit('?') ? "? is not a hexadecimal digit" : "hexadecimal digit",
           isxdigit('$') ? "$ is not a hexadecimal digit" : "hexadecimal digit",
           isxdigit('F') ? "F is a hexadecimal digit" : "not a hexadecimal digit");
}
```

According to isdigit:

8 is a digit

# is not a digit

According to isalpha:

A is a letter

b is a letter

! is not a letter

4 is not a letter

According to isalnum:

A is a digit or a letter

8 is a digit or a letter

# is not a digit or a letter

According to isxdigit:

F is a hexadecimal digit

J is not a hexadecimal digit

? is not a hexadecimal digit

$ is not a hexadecimal digit

**图 8.2** 使用 `isdigit, alpha, isalnum` 和 `isxdigit`。（第 2 部分。）

## 8.3.2 islower, isupper 和 toupper 函数

图 8.2 使用条件运算符 (:) 来决定为每个测试字符输出输出打印 "is a" 还是 "is not"。例如，表达式 `isdigit('8') ? "8 is a" : "8 is not a"` 表示如果 '8' 是数字，则打印 "8 is a"，如果 '8' 不是数字（即 `isdigit` 返回 0），则打印 "8 is not a"。

图 8.3 展示了 `islower, isupper` 和 `toupper` 函数。`islower` 判断参数是否为小写字母 (a-z)。`isupper` 判断参数是否为大写字母 (A-Z)。`tolower` 将大写字母转换为小写字母并返回小写字母。如果参数不是大写字母，`tolower` 返回原参数不变。`toupper` 将小写字母转换为大写字母并返回大写字母。如果参数不是小写字母，`toupper` 返回原参数不变。

![](img/fa81e30d8bce03c9060826ba997d7b_371_0.png)
