

# #define 指令

#define 指令指定一个标识符和一个字符序列（即一组字符）。每当在源文件中遇到该标识符时，字符序列就会被替换该标识符。#define 语句被称为宏。

该标识符被称为宏名（macro name），替换字符被称为宏替换内容（macro replacement）。该指令的一般形式为：

```
#define macro-name char-sequence
```

请注意，该语句末尾没有分号。宏名和字符序列之间可以有任意数量的空格，但一旦字符序列开始，它仅由换行符终止。

如果我们希望对单词 LEFT 使用值 0，对单词 RIGHT 使用值 1，我们可以声明这两个 #define 指令：

```
#define LEFT 0
#define RIGHT 1
```

这会导致预处理器在源文件中每次遇到 `LEFT` 宏名或遇到 `RIGHT` 宏名时，都将其替换为 0 或 1。

一旦定义了宏名，它就可以在其他宏名的定义中使用。例如：

```
#define ONE 1
#define TWO ONE + ONE
```

宏替换简单地将宏名替换为与其关联的字符序列。

**注意：** 如果宏名位于引号内，则不会发生宏名替换。

如果字符序列超过一行，我们可以在行末尾放置一个反斜杠来在下一行继续编写，如下所示：

```
#define LONG_STRING "this is a very long \
string that is used as an example"
```

按照惯例，使用大写字母表示宏名。将所有程序宏放在一个单独文件中也是一种惯例。

宏的常见用途之一是标识“魔术数字”（magic numbers）。

使用 #define 宏的一个问题是，编译器永远看不见宏，因为预处理器在将文件移交给编译器之前执行了宏替换。例如，如果我们指定了 `#define GREEN`，编译器将永远看不到 `GREEN` 标识符。此外，如果我们未能包含含有此宏定义的文件，那么编译器在每次看到 `GREEN` 时都会抛出未知声明的错误。

# 定义函数形式的宏

**define** 指令具有一个强大的特性：宏名可以带有参数。每当遇到宏名时，其定义中使用的参数就会被程序中找到的实际参数替换。这种形式的宏被称为函数形式（function-like）。

```
#include <stdio.h>

#define ABS(a) (a)<0 ? -(a) : (a)

int main(void) {
    printf("abs of -1 and 1: %d %d", -1, ABS(1));
    return 0;
}
```

当编译此程序时，宏定义中的 `a` 将被替换为值 -1 和 1。括号确保了在所有情况下都能正确替换。

强烈不建议使用函数宏，因为可能会产生奇怪的结果。
查看以下程序片段：

```
// 使用 a 和 b 的最大值调用 f
#define CALL_WITH_MAX(a, b) f((a) > (b) ? (a) : (b))

int a = 5, b = 0;
CALL_WITH_MAX(++a, b);      // a 被自增了两次
CALL_WITH_MAX(++a, b+10);   // a 被自增了一次
```

在调用 `f` 之前 `a` 自增的次数取决于它与什么进行比较。

在实际函数中使用函数形式的宏有一个主要优点：它增加了代码的执行速度，因为没有函数调用开销。然而，如果函数形式宏的大小非常大，那么由于代码重复，这种速度的提升可能以程序体积增大为代价。

# NULL 宏

在 C 语言中，NULL 定义如下：

```
#define NULL 0
```

# #error

#error 指令发出错误消息并强制编译器停止编译。它主要用于调试。#error 指令的一般形式为：

```
#error error-message
```

用法的示例为：

```
#if _STDC_ != 1
#error "Not a standard compliant compiler"
#endif
```

# #include 指令

#include 指令指示编译器读取另一个源文件，并将其放置在包含 #include 指令的源文件中。该文件将在 #include 指令出现的行处包含。附加源文件的名称必须封装在双引号或角括号之间。

```
#include "stdio.h"
```

或者

```
#include <stdio.h>
```

被包含的文件内部也可以有 #include 指令。这被称为嵌套包含（nested includes）。允许的嵌套层数在不同编译器之间有所不同。标准 C 规定必须至少支持 8 层嵌套包含。标准 C++ 建议至少支持 256 层嵌套。

文件名是封装在引号中还是角括号中决定了如何对指定的文件进行搜索。如果文件名封装在角括号中，则按照编译器创建者定义的方式搜索该文件。通常，这意味着搜索某些预留给包含文件的特殊目录。这是包含库文件的典型方式。

如果文件名封装在引号中，则按照实现者或程序创建者定义的方式搜索文件。这是包含用户文件的方式。对于许多编译器来说，这意味着搜索当前目录。

# 条件指令

有几种指令允许我们选择性地编译源代码的部分。最常用的条件指令是 #if、#elif、#else 和 #endif。这些条件指令允许我们根据常量表达式的值来选择性地编译。

#if 指令的形式为：

```
#if constant-expression
statements
#endif
```

如果 #if 的表达式为真，则 #if 和 #endif 之间的代码将被编译。否则，将跳过它。#if 后的表达式在编译时评估。因此它必须只包含已定义的标识符和常量。

```
/* Simple #if example */
#include <stdio.h>
#define MAX 10
int main(void) {
    #if MAX > 99
    printf("Compiled greater than 99");
    #endif
    return 0;
}
```

#else 指令在 #if 失败时建立一个替代方案。

```
/* Simple #if/#else example */
#include <stdio.h>
#define MAX 10
int main(void) {
    #if MAX > 99
    printf("Compiled greater than 99");
    #else
    printf("Compiled for a small array.");
    #endif
    return 0;
}
```

#elif 指令表示“else if”。它为多个编译选项建立 if-else 链。#elif 跟着一个常量表达式。如果表达式为真，则附加到 #elif 的块将被编译，且不再测试其他 #elif。否则，将测试 #if 链中的下一个块。

#elif 的一般形式为：

```
#if expression
statement sequence
#elif expression 1
statement sequence
#elif expression 2
.
#else
statement sequence
#endif
```

示例：

```
#define US 0
#define ENGLAND 1
#define FRANCE 2
```

```
#if ACTIVE_COUNTRY == US
char currency[] = "dollar";
#elif ACTIVE_COUNTRY == ENGLAND
char currency[] = "pound";
#else
char currency[] = "franc";
#endif
```

# #ifdef 和 #ifndef

另一种用于条件编译的预处理器使用了 #ifdef 和 #ifndef 指令。分别表示“如果定义”和“如果未定义”。

#ifdef 的一般形式为：

```
#ifdef macro-name
statement sequence
#endif
```

如果 macro-name 之前在 #define 语句中已定义，则代码块将被编译。

#ifndef 的一般形式为：

```
#ifndef macro-name
statement sequence
#endif
```

如果 macro-name 当前未被 #define 语句定义，则代码块将被编译。

#ifdef 和 #ifndef 指令都可以使用 #elif 或 #else 指令。例如：

```
#include <stdio.h>
#define __FREE 10
int main(void)
{
    #ifdef MONTHLY_SUBSCRIPTION
    printf("Monthly\n")
    #elif defined __YEARLY_SUBSCRIPTION
    printf("yearly\n")
    #elif defined __FREE
    printf("Free\n")
    #else
    printf("error\n")
    #endif

    #ifndef ALICE
    printf("ALICE not defined\n")
    #endif

    return 0;
}
```

