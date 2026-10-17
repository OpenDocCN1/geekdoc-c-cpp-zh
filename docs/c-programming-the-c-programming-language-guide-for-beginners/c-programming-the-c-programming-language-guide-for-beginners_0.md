
# C语言编程：初学者 C 语言编程指南 (软件工程师编写) (编程珍珠) (计算机编程书籍第 1 册)

![](img/cover.jpeg)

## 目录

- [C 语言概述](#c-语言概述)

[点击此处免费获取电子书！](https://globalizedhealing1.leadpages.com/)

# C 语言概述

C 语言是一种强大的语言，最初由 Dennis Ritchie 于 1972 年在贝尔实验室创建。C 广泛用于开发操作系统、嵌入式系统和各种应用程序。它是一种结构化的过程化编程语言，提供了对内存的底层访问。C 是 C++、Java 和 Python 等许多其他语言的基础。

C 是一种为系统编程开发设计的通用编程语言。它以高效和可移植性而闻名，是许多类型项目的热门选择。C 广泛用于开发操作系统、嵌入式系统和各种应用程序。它是一种结构化的过程化编程语言，提供了对内存的底层访问。

C 是 C++、Java 和 Python 等许多其他语言的基础。

C 是一种为系统编程开发设计的通用编程语言。它以高效和可移植性而闻名，是许多类型项目的热门选择。C 广泛用于开发操作系统、嵌入式系统和各种应用程序。

## 关于 C 语言的事实

在继续之前，让我们来看一些关于 C 的事实。C 最初由 Dennis Ritchie 于 1972 年创建。它是一种结构化的过程化编程语言，提供了对内存的底层访问。C 是 C++、Java 和 Python 等许多其他语言的基础。

C 是一种为系统编程开发设计的通用编程语言。它以高效和可移植性而闻名，是许多类型项目的热门选择。C 广泛用于开发操作系统、嵌入式系统和各种应用程序。

## 为什么要使用 C？

C 是一种强大的语言，最初由 Dennis Ritchie 于 1972 年在贝尔实验室创建。C 广泛用于开发操作系统、嵌入式系统和各种应用程序。它是一种结构化的过程化编程语言，提供了对内存的底层访问。C 是 C++、Java 和 Python 等许多其他语言的基础。

C 是一种为系统编程开发设计的通用编程语言。它以高效和可移植性而闻名，是许多类型项目的热门选择。C 广泛用于开发操作系统、嵌入式系统和各种应用程序。

## C 程序

C 程序是计算机执行以完成特定任务的指令集。C 程序写在`.c`文件中，并必须编译成可执行文件。C 程序从`main()`函数开始，该函数是程序的入口点。

C 程序可以使用函数、变量、循环和其他控制结构。它们被用于创建从操作系统到嵌入式系统的各种应用程序。

## 环境搭建

在开始学习 C 语言之前，你需要在系统中准备好以下两个应用程序：

(a) 编译器：它将你的源代码翻译成可执行文件。

(b) 文本编辑器：这是你编写 C 代码的地方。

文本编辑器的名称可能根据你使用的操作系统而异。例如，Windows 上将使用记事本，而在 Linux 上也可以使用 VI 或 `vim`。

# 你的第一个 C 程序

和任何其他编程语言一样，除非你亲自编写代码，否则你无法学会一门编程语言。按照字面和传统，我们向你介绍第一个 C 程序，这是一个简单的“Hello World!”程序。选择这个程序作为你与 C 的首次面对面，是因为这段程序代码代表了最基础的 C 项目结构。

示例代码：`sample.c`

```c
#include <stdio.h>

int main() {
    /* 用于打印 Hello World! 的示例代码 */
    printf("Hello World!");
    return 0;
}
```

现在你已经了解了标准 C 程序的不同方面，让我们仔细观察一下我们刚刚编写的“Hello World!”。

● 第 1 行：

项目的第一行`#include <stdio.h>`是一个预处理器指令，它建议 C 编译器在编译之前包含头文件`stdio.h`的内容。

● 第 2 行：

下一行`int main()`是主函数，C 编程中的程序执行从这里开始。

● 第 3 行：

下一行`/*...*/`将被编译器忽略，它被用作注释，或者是项目中不是 C 代码中活动部分的行。换句话说，它们仅仅是供开发者参考以理解代码的备注信息。

● 第 4 行：

下一行`printf(...)`是 C 中可以使用的另一种函数，它负责打印文本：

"Hello World!"

● 第 5 行：

下一行`return 0`是`main()`函数完成后返回给系统的值。

## 编译和执行 C 程序

现在，你已经准备好了代码。接下来显而易见的步骤包括在机器上编译和执行代码。接下来的几步将说明代码是如何保存、编译和运行的。

● 将代码复制并粘贴到你用于项目的文本编辑器中。如果你使用集成框架如`Bloodshed C++`或`Xcode`进行开发，可以直接在这些环境的文本编辑器中编写代码。

● 将源文件保存为`sample.c`或任何你认为方便的名称，并存在系统内存中的指定位置。

● 使用基于控制的命令或编程环境中的集成快捷键编译代码。

● 如果文件编译成功，你会发现源文件相同的位置将创建`sample.o`和`a.out`文件。

● `a.out`文件可用于执行该文件。

运行可执行文件后，你将看到以下预期输出。

### 预期输出：

Hi, World!

验证你正在使用`GCC`编译器并从正确的目录位置运行文件。

## 语法

本章将提供关于 C 编程语言所有基础语言结构的见解。这些结构包括关键字、标记（tokens）、标识符等。你已经看到了 C 程序的本质结构。因此，你已经对 C 程序包含的内容有了基本的概念。在接下来的章节中，我们将仔细观察这些结构以及如何在现实世界的编程中使用它们。

### C 中的标记

为了说明 C 中标记的概念，让我们以下语句作为示例：

```c
printf("Print this text!");
```

该语句的各个标记为：

● `printf`

● `(`

● `"Hi, World! \n"`

● `)`

● `;`

一个 C 系统由不同的标记组成，标记可以是一个标识符、关键字、字面量或函数调用。

### 分号 (;)

注意每个语句末尾使用的分号。分号是 C 的终止序列，在每个 C 语句末尾必须使用分号。但是，请注意，在`#include`语句的预处理器指令末尾不应使用分号。

### 注释

C 编程语言允许使用以下格式的多行注释：

```c
/* This is a comment */
```

注释本质上是你的 C 项目中的帮助文本。它们会被编译器忽略，不被视为项目的活动部分。通常，它们必须以`/*`开头并以`*/`结束，如上例所示。你不能嵌套注释或在侧注释中使用注释。换句话说，`/*`必须有一个匹配的`*/`，并且在第一个注释开始序列被匹配序列终止之前，后面不能跟另一个`/*`。

## 标识符

C 标识符是用于区分函数、变量或开发者创建的任何其他结构的名称。标识符以字母或下划线`_`开头。然而，后续序列可以包含字母（大写或小写）和数字（0-9）。C 不允许重音字符，例如`@`、`$`和`%`作为标识符的组成字符。

请注意 C 语言是大写敏感的。因此，对于编译器来说，`Character`和`character`是不同的序列。标识符的一些示例有：

● `A_xyz`

● `a_xyz`

● `_inty`

● `a12b`

### 关键字

某些单词限制开发者使用，因为语言使用它们来指示编译器提供作为 C 编程语言一部分的基本功能。以下是保留关键字列表。你必须仔细观察这些关键字，并确保不要使用与这些关键字同名的标识符，否则会导致不可避免的编译错误。

● `else`

● `auto`

● `switch`

● `long`

● `enum`

● `break`

● `typedef`

● `register`

● `extern`

● `case`

● `union`

● `return`

● `float`

● `char`

● `unsigned`

● `short`

● `const`

● `signed`

● `for`

● `continue`

● `void`

● `sizeof`

● `goto`

● `default`

● `volatile`

● `static`

● `if`

● `while`

● `struct`

● `double`

● `int`

### 数据类型



在 C 语言中，数据类型指的是用于变量或函数的框架。变量的类型决定了它占据的空间以及其中保存的位模式。数据类型的基本分类如下：

- **基本类型**：它们是数字处理类型，包括两种类型：(a) 整数类型和 (b) 浮点类型。
- **枚举类型**：它们也是数字类型，用于描述必须通过系统分配的变量。
- **空类型**：关键字 `void` 表示无法赋值。
- **派生类型**：它们包括 (a) 数组、(b) 指针、(c) 联合体、(d) 结构和 (e) 函数。数组和结构数据类型也被称为聚合类型。函数的类型定义了函数将返回值的种类。我们将在后续章节中讨论基本数据类型。

## 整数类型

以下是该类别下的数据类型列表。此外，还指定了它们占据存储空间及其范围。

- `char`
  - 分配内存：1 字节
  - 范围：-128 到 127 或 0 到 255
- `signed char`
  - 分配内存：1 字节
  - 范围：-128 到 127
- `unsigned char`
  - 分配内存：1 字节
  - 范围：0 到 255
- `int`
  - 分配内存：2 或 4 字节
  - 范围：-32,768 到 32,767 或 -2,147,483,648 到 2,147,483,647
- `short`
  - 分配内存：2 字节
  - 范围：-32,768 到 32,767
- `unsigned short`
  - 分配内存：2 字节
  - 范围：0 到 65,535
- `unsigned int`
  - 分配内存：2 或 4 字节
  - 范围：0 到 65,535 或 0 到 4,294,967,295
- `long`
  - 分配内存：4 字节
  - 范围：-2,147,483,648 到 2,147,483,647
- `unsigned long`
  - 分配内存：4 字节
  - 范围：0 到 4,294,967,295

要获取变量或数据类型的精确大小，你可以利用 `sizeof` 运算符。`sizeof(<data type>)` 声明会产生该数据类型或变量以字节（bytes）为单位的大小。下面是一个示例，说明了下文讨论的概念：

```c
#include <limits.h>
#include <stdio.h>

int main() {
    printf("Data type char (size in bytes): %d \n", sizeof(char));
    return 0;
}
```

编译并执行此代码后，你将得到以下输出：

```
Data type char (size in bytes): 1
```

## 浮点数据类型

以下是属于此类别的的数据类型列表。此外，为了供参考，还规定了它们占用的存储空间、范围和精度值。

- `float`
  - 分配内存：4 字节
  - 范围：1.2e-38 到 3.4e+38
  - 精度：6 位小数
- `double`
  - 分配内存：8 字节
  - 范围：2.3e-308 到 1.7e+308
  - 精度：15 位小数
- `long double`
  - 分配内存：10 字节
  - 范围：3.4e-4932 到 1.1e+4932
  - 精度：19 位小数

名为 `float.h` 的头文件定义了允许你使用这些数据类型值的宏。以下代码将允许你找到你的系统中相关数据类型以字节为单位的精确分配内存量。

```c
#include <float.h>
#include <stdio.h>

int main(){
    printf("Allocated Memory for float : %d \n", sizeof(float));
    printf("Precision: %d\n", FLT_DIG );
    printf("Max Range Value: %E\n", FLT_MAX );
    printf("Min Range Value: %E\n", FLT_MIN );
    return 0;
}
```

编译并执行此代码后，你将得到以下输出：

```
Allocated Memory for float : 4
Precision: 6
Max Range Value: 3.402823E+38
Min Range Value: 1.175494E-38
```

## void 类型

`void` 数据类型表示没有可访问的值。它被用作三种情况之一：

- **函数返回 void**：你可能已经经常注意到 `void` 数据类型作为函数返回类型的使用。如果没有，随着你对 C 语言经验的增加，你会看到它被广泛使用。`void` 数据类型表示函数将不返回任何内容。这种实现的示例为：`void print(int);`
- **作为 void 的函数参数**：C 语言中有不同的函数不接受任何参数。没有参数的函数可以被声明为 `void`。这种实现的示例为：`int print(void);`
- **指向 void 的指针**：`void *` 类型的指针表示变量的位置。例如，考虑以下声明：`void *malloc( size_t size );` 此函数返回一个指向 `void` 的指针。换句话说，此函数可以返回指向任何类型位置的指针。

你现在可能无法完全理解 `void` 数据类型的用法和意义。然而，随着你经验的增长，你会发现更容易在你的代码中关联和使用这种数据类型。

# C 语言中的变量

变量只是提供给我们的 C 项目可以控制的内存区域的名称。C 语言中的每个变量都有特定的数据类型，它决定了变量内存的大小和格式、可以放入该内存中的值的范围，以及可以对变量执行的操作 set。

变量名由数字、字母和下划线字符组成。但是，它必须以字母或下划线开头。由于 C 是区分大小写的，大写字母和小字母是不同的。以下是 C 编程语言包含的数据类型列表。

- `Char`：`Char` 数据类型是单字节（8 字节）。
- `Int`：`Int` 是机器最常见的数字尺寸。
- `Float`：`float` 表示单精度浮点数值。
- `Double`：`double` 数据类型具有双倍精度。
- `Void`：表示任何数据类型的缺失。

C 编程语言同样允许描述不同类型的变量，我们将在书的后续部分介绍，如指针、枚举、结构体、数组和联合体等。对于这部分，让我们只考虑基本的变量类型。

## C 语言中的变量定义

变量定义旨在告诉编译器为变量制作内存的位置和数量。变量定义定义了变量的数据类型，并根据变量将包含的单个变量数量定义了变量类型。典型的变量声明如下：

`<data-type> <names of the variables>;`

在这里，`data-type` 必须是一个合法的 C 数据类型。因此，它可以是 `char`、`int`、`float` 或 `double`。然而，变量名可以是任何合法的标识符，如 `i`、`I`、`_intx` 或 `_i12`。这些变量必须用逗号隔开并分号结尾。此类语句的示例包括：

```c
char ch, name;
int i, j;
float i, j;
double i, j;
```

*(注：原文末尾部分存在大量重复的无效文本，已根据要求过滤掉重复内容)*

请注意数字中 `8` 的使用。八进制不能包含 `8`，因为它们的范围仅从 0 到 7。

- `011uu`：请注意后缀的重新哈希（更改）。这在 `C` 中是不允许的。

## 浮点数字面量

通常，浮点数包含一个数字部分、一个小数点、小数部分和一个指数部分。然而，浮点数也可以以指数结构或小数结构存在。下面给出了这些字面量的几个示例，供你理解和参考。

- `3.14159` /* 合法 */
- `314159e-5l` /* 合法 */

以下示例不是合法的声明。

- `510e`
- `.e55`

请注意声明中指数部分缺少了小数点。

## 字符常量

字符字面量被单引号包裹。例如，`'a'` 是一个字符常量。然而，这种类型的字面量可以包含字母数字、特殊字符或普通字符。在 `C` 中，当字符出现在斜杠标点符号之前时，它们是特殊的字符。它们具有独特的重要性，并用于引用特殊标点，如制表符 (`\t`) 或换行符 (`\n`)。列表说明了不同的转义序列及其含义。

- 字符
  - `\"` "
  - `\'` '
  - `\\` \
  - `\?` ?
- 退格 - `\b`
- 警报或铃声 - `\a`
- 换行 - `\n`
- 换页 - `\f`
- 水平制表符 - `\t`
- 回车 - `\r`
- 十进制数（1 位或更多数字） - `\xhh ...`
- 八进制数（1-3 位） - `\ooo`
- 垂直制表符 - `\v`

下面是一个说明这些字符及其意义的示例代码。

```c
#include <stdio.h>

int main () {
    printf("Hey \t Everyone \n\n");
    return 0;
}
```

在编译和执行此代码后，可以预期输出如下：

```
Hey Everyone
```

## 字符串字面量

字符串字面量或常量被双引号 `" "` 包裹。字符串包含与字符字面量类似的字符：普通字符、转义字符和其他字符。你可以利用字符串字面量将长行拆分为多行，并利用空白将它们划分。这里是字符串字面量的几种情况。这三种结构都是等效的字符串。

- `"hi, \`
- `"hi, dear"`
- `dear"`

## 如何声明常量

在 `C` 中声明常量有两种直接的方法：

1. 使用 `const` 关键字
2. 使用 `#define` 预处理器

### #define 预处理器

这种结构可以使用 `#define` 预处理器来实现。下面的实现说明了这种方法的用法。

```c
#include <stdio.h>

#define TAB "\t"
#define LEN 10

int main () {
    int x;
    x = LEN * 100;
    printf("x = %d", x);
    printf("%c", TAB);
    printf("x = %d", x);
    return 0;
}
```

在编译和执行上述代码后，可以预期如下结果：

```
10001000
```

### const 关键字

你可以利用 `const` 前缀为具有特定数据类型的常量进行声明：

`const <data type> <variable name> = <value>;`

这里有一段说明该概念的用法：

```c
#include <stdio.h>

int main ()
{
    const int LEN = 10;
    const char TAB = '\n';
    printf("LEN = %d", LEN);
    printf("%c", TAB);
    printf("LEN = %d", LEN);
    return 0;
}
```

在编译和执行上述代码后，可以预期如下结果：

```
10001000
```

注意在命名常量变量时使用大写字母。虽然这不是强制性的做法，但它无疑是一个良好的编程习惯。

# 存储类

存储类定义了 `C` 程序内部变量和/或函数的作用范围和生命周期。这些关键字通常放在变量或函数的数据类型之前。`C` 中有几种可选存储类，如下：

- `register`
- `auto`
- `static`
- `extern`

### auto 存储类

`auto` 类是 `C` 编程中所有变量的默认存储类。它在程序中的用方法如下：

`auto int x;`

上面的示例声明了一个变量 `x`，其声明为 `auto`。该存储类用于函数的局部变量。

### register 存储类

`register` 类用于声明应该放在寄存器而不是 RAM 中的局部变量。这意味着该变量具有等于寄存器大小的最大尺寸（通常为单字），并且不能与其连接一元操作符 `&`，因为它没有内存区域。该类变量的典型实现如下：

`register int x;`

`register` 应该仅用于计数器。同样需要注意的是，定义 `"register"` 并不意味着变量会被放入寄存器中。它意味着如果环境和系统允许，变量可能会被放入寄存器中。

### static 存储类

`static` 类允许变量在函数执行期间保持有效。`static` 修饰符允许变量在定义它的文件中保持可见。下面给出了一个使用了该存储类的示例代码：

```c
#include <stdio.h>

void samplefunc ();

static int tally = 10;

int main () {
    while(tally--) {
        samplefunc ();
    }
    return 0;
}

void samplefunc (void) {
    static int lvar = 10;
    printf("lvar is %d and tally is %d\n", lvar, tally);
}
```

编译并执行上述代码后，可以预期如下输出：

```
lvar is 10 and tally is 9
lvar is 10 and tally is 8
lvar is 10 and tally is 7
lvar is 10 and tally is 6
lvar is 10 and tally is 5
lvar is 10 and tally is 4
lvar is 10 and tally is 3
lvar is 10 and tally is 2
lvar is 10 and tally is 1
lvar is 10 and tally is 0
lvar is 11 and tally is 9
lvar is 12 and tally is 8
lvar is 13 and tally is 7
lvar is 14 and tally is 6
```

这里 `extern` 类用于声明在其他文件中定义的变量或函数。当你有多个文件并声明一个函数或全局变量时，使用 `extern` 来指示编译器引用的是另一个文件中存在的变量。下面的代码说明了这种类的用法：

文件名：`main.c`

```c
#include <stdio.h>

int count ;

extern void ext_write ();

int main () {
    ext_write ();
}
```

第二个文件：`write_e.c`

```c
#include <stdio.h>

extern int count;

void ext_write (void) {
    count = 5;
    printf("count = %d\n", count);
}
```

编译并执行包含上述两个文件的项目，可以预期发生如下结果：

```
count = 5
```

| 取模 | % | 结果值是除法的余数 |
| :--- | :--- | :--- |
| 递增 | ++ | 将值增加 1 |
| 递减 | -- | 将值减少 1 |

### 关系运算符

C 语言还支持几种关系运算符。C 支持的关系运算符列表下所示。

| 操作 | 运算符 | 描述 |
| :--- | :--- | :--- |
| 等于 | == | 比较两个变量的值是否相等 |
| 不等于 | != | 比较两个变量的值是否不相等 |
| 大于 | > | 检查一个值是否大于另一个值 |
| 小于 | < | 检查一个值是否小于另一个值 |
| 大于等于 | >= | 检查一个值是否大于或等于另一个值 |
| 小于等于 | <= | 检查一个值是否小于或等于另一个值 |

### 位运算符

C 中可用的位运算符可以轻松地应用于多种数据类型。这些数据类型包括字节 (byte)、短型 (short)、长型 (long)、整型 (int) 和字符 (char)。通常，任何位运算符都会按位执行相关操作。例如，考虑一个整数 `x`，其值为 `60`。因此，`x` 的二进制等效值是 `00111100`。考虑另一个变量 `y`，其值为 13 或 `00001101`。如果我们对这两个数字执行位运算 `&`，那么你将得到以下结果：

```
x&y = 0000 1100
```

下表显示了 C 中可用的位运算符列表。

| 操作 | 运算符 | 描述 |
| :--- | :--- | :--- |
| 二进制与 | & | 执行与操作 |
| 二进制或 | \| | 执行或操作 |
| 二进制异或 | ^ | 执行异或操作 |
| 补码取反 | ~ | 对一元变量执行取反操作 |
| 二进制左移 | << | 执行位的左移 |
| 二进制右移 | >> | 执行位的右移 |

除了上述运算符外，C 还支持右移零填充运算符 (`>>>`)，它会将移后的右侧位用零填充。

# 逻辑运算符

逻辑运算符是任何运算符集中不可或缺的一部分。C 支持的逻辑运算符如表所示。

| 操作 | 运算符 | 描述 |
| :--- | :--- | :--- |
| 逻辑与 | && | 如果提到的两个条件都为真，则返回 True |
| 逻辑或 | \|\| | 如果提到的一个或两个条件为真，则返回 True |
| 逻辑非 | ! | 如果提到的条件为假，则返回 True |

# 赋值运算符

C 语言支持以下赋值运算符：

| 操作 | 运算符 | 描述 |
| :--- | :--- | :--- |
| 简单赋值运算符 | = | 将右侧的值赋值给左侧变量 |
| 加赋值运算符 | += | 将右侧的值加到左侧变量的值，并将结果赋值给左侧变量 |
| 减赋值运算符 | -= | 从左侧变量的值减去右侧的值，并将结果赋值给左侧变量 |
| 乘赋值运算符 | *= | 将右侧的值乘以左侧变量的值，并将结果赋值给左侧变量 |
| 除赋值运算符 | /= | 将右侧的值除以左侧变量的值，并将结果赋值给左侧变量 |



| 取模赋值运算符 | `%=` | 取左侧和右侧的模数，并将结果赋值给左侧变量 |
| 左移赋值运算符 | `<<=` | 取左侧和右侧的左移，并将结果赋值给左侧变量 |
| 右移赋值运算符 | `>>=` | 取左侧和右侧的右移，并将结果赋值给左侧变量 |
| 位赋值运算符 | `&=` | 取左侧和右侧的位与结果，并将结果赋值给左侧变量 |
| 位异或赋值运算符 | `^=` | 取左侧和右侧的位异或结果，并将结果赋值给左侧变量 |
| 位或赋值运算符 | `|=` | 取左侧和右侧的位或结果，并将结果赋值给左侧变量 |

## 其他运算符

除了上述外，`C` 还支持其他几种运算符。

## 条件运算符 ( `? :` )

条件运算符是一个包含三个操作数的三元运算符。本质上，该运算符用于求值布尔表达式。该运算符测试第一个操作数或条件，如果条件为真，则将第二个值赋值给变量。然而，如果条件为假，则将第三个操作数赋值给变量。该运算符的语法如下：

```
variable a = (<condition>) ? valueiftrue : valueiffalse
```

示例实现：

```c
#include<stdio.h>

int main(){
int x, y;
x = 5;
y = (x == 5) ? 15: 40;
printf( "y = " + y );
y = (x == 34) ? 60: 95;
printf( "x = " + y );
}
```

此代码的编译和执行将产生如下结果：

```
y = 15
y = 95
```

### `sizeof()` 运算符

`sizeof()` 运算符返回变量的大小。该运算符可以使用如下方式：

```c
int x;
sizeof(x);
```

### 变量指针 (`*`)

星号 `*` 用于变量前表示变量指针。该运算符可以使用如下方式：

```c
int *ptr;
```

### 变量地址 (`&`)

取地址符号 `&` 用于变量前表示变量的地址。该运算符可以使用如下方式：

```c
int ptr = &x;
```

## C 运算符的优先级

通常情况下，运算符组合在表达式中使用。然而，你必须意识到预测执行时的操作顺序是困难的。`C` 运算符优先级表将帮助你预测操作。例如，如果你在同一个表达式中执行加法和乘法，那么乘法先于加法。下表说明了运算符的顺序和层次。所有运算符的结合性从左到右。然而，一元运算符、赋值和条件运算符从右到左。

| 运算符 | 类别 |
| :--- | :--- |
| `() [] .` (点运算符) | 后置 |
| `++ - ! ~` | 一元 |
| `* / %` | 乘除 |
| `+ -` | 加减 |
| `>> >>> <<` | 移位 |
| `> >= < <=` | 关系 |
| `== !=` | 相等 |
| `&` | 位与 |
| `\|` | 位或 |
| `^` | 位异或 |
| `&&` | 逻辑与 |
| `\|\|` | 逻辑或 |
| `?:` | 条件 |
| `= += -= %= >>= <<= &= ^= \|=` | 赋值 |
| `,` | 逗号 |

# C 中的循环

循环是编程中常见的情况，你可能会经常遇到。循环可以简单地描述为需要重复执行同一代码块的情况。C 支持三种循环结构，如下：

- `for` 循环
- `do...while` 循环
- `while` 循环

此外，还有 `foreach` 循环结构。然而，该结构将在数组章节解释。

## while 循环

`while` 循环允许你按指定的次数重复执行任务。该结构的语法如下：

```c
while(布尔表达式) {
// 语句
}
```

在执行时，如果布尔表达式的结果为真，则循环体内的活动将被执行。这将一直持续，直到条件结果为假。`while` 循环的关键点在于它可能永远不会运行。当尝试条件且结果为假时，循环体将被跳过，整个循环后的第一个语句将被执行。

示例实现：

```c
#include<stdio.h>

int main(){

int i=5;

while(i<10) {

printf(" i = " + i );

i++;

printf("\n");

}

}
```

这将会产生相应的结果：

```
i = 5
i = 6
i = 7
i = 8
i = 9
```

## do...while 循环

`do...while` 循环与 `while` 循环结构相似，不同之处 `do...while` 循环被确保至少执行一次。该循环构造的语法如下：

```c
do {
// 语句
} while(<布尔表达式>);
```

请注意，布尔声明出现在循环的末尾，因此代码在尝试布尔表达式之前会先执行一次。如果布尔声明为真，控制流将跳回 `do`，代码将再次执行一次。这种方法会重复执行，直到布尔表达式为假为止。

示例实现：

```c
#include<stdio.h>

int main(){

int i = 1;

do{
printf("i = " + i );
i++;
printf("\n");
}while( i< 1 );

}
```

这将产生相应的结果：

```
i = 1
```

## for 循环

`for` 循环是一种迭代控制结构，允许你有效地组合一个需要执行特定次数的循环。当你知道一个任务需要重复多少次时，`for` 循环构造非常有帮助。该循环构造的语法如下：

```c
for(初始化; 布尔表达式; 变量更新)
{
// 语句
}
```

以下是 `for` 循环中的控制流：

- 初始化步骤首先执行，且仅执行一次。此步骤允许你声明并引入任何循环控制变量。你不需要在这里进行声明，只需一个分号即可。
- 接下来，评估布尔输出。如果为真，则执行循环体内容。如果为假，则不执行循环体，控制流跳转到 `for` 循环之后的后续语句。
- 在 `for` 循环体执行完毕后，控制流跳回重构部分语句。此语句允许你更新任何循环控制变量。此语句可以留空，在布尔声明后会出现一个分号。
- 再次评估布尔输出。如果为真，循环执行并循环自身。当布尔声明为假后，`for` 循环结束。

示例实现：

```c
#include<stdio.h>

int main(){

for(int i = 0; i < 5; i = i+1) {

printf("i = " + i );
printf("\n");

}

}
```

这将产生相应的结果：

```
i = 0
i = 1
i = 2
i = 3
i = 4
```

## break 关键字

`break` 关键字用于停止整个循环的执行。`break` 词必须在任何循环或 `switch` 结构内部。`break` 关键字将停止最深层循环的执行，并在大括号结束后开始执行下一行代码。使用该关键字的语法如下：

```c
break;
```

## continue 关键字

`continue` 关键字可以作为任何循环控制结构的一部分。它导致循环快速跳转到循环的下一个语句。

- 在 `for` 循环中，`continue` 关键字使控制流快速跳回重构部分语句。
- 在 `while` 或 `do/while` 循环中，控制流立即跳转到布尔解释。

使用该关键字的语法如下：

```c
continue;
```

## 无限循环

如果循环条件始终为真，循环将无限持续。通常，`for` 循环构造用于此目的。为了实现 `for` 循环，你不需要提到 `for` 循环内部编写的三个表达式中的任何一个。无限循环的示例如下：

```c
#include<stdio.h>

int main(){

for(;;)
{
// 无限循环内部的语句
}
```

由于 `for` 循环不存在条件语句，编译器假设条件始终为真。因此，循环变为无限。可以使用外部中断（`Ctrl + C`）终止此循环。

## C 中的决策

C 语言中有两种决策结构。它们是：

- `if` 结构
- `switch` 结构

### if 语句

`if` 结构由一个或多个声明模拟的布尔输出组成。使用该构造的语法如下：

```c
if(<条件>) {
// 如果条件为真则执行语句
}
```

如果布尔结构评估为真，则执行 `if` 语句内部的代码块。如果不是，则执行 `if` 结构结束处（大括号结束后）后的第一组代码。

示例实现：

```c
#include<stdio.h>

int main(){

int i = 0;

if( i < 1 ){

printf("The if construct is executing!");

}

}
```

这将产生相应的结果：

```
The if construct is executing!
```

### if...else 语句

`if` 语句可以有一个可选的 `else` 语句，当布尔结构为假时执行 `else` 语句。

```c
if(<条件>){

// 如果条件为真则执行

}

else

// 如果条件为假则执行
```

示例实现：

```c
#include<stdio.h>

int main(){

int i = 0;

if( i < 1 ){

printf("The if construct is executing!");

}

else{

printf("The else construct is executing!");

}
```

### if...else if 语句

`if` 语句可以后跟一个 `else` 语句，也可以后跟多个 `else if` 语句，这有助于测试不同的条件。

- `if` 可以有一个 `else`，且它必须在任何 `else if` 之后。
- `if` 可以有零或多个 `else if`，它们必须在 `else` 之前。
- 如果其中一个 `if` 条件产生真值，其他的 `else if` 和 `else` 将被忽略。

使用此决策构造的语法如下：

```c
if(条件 1){

// 如果条件 1 为真则执行

}

else if(条件 2){

// 如果条件 2 为真则执行

}

else if(条件 3){

// 如果条件 3 为真则执行

}

else

{

// 如果所有条件为假则执行

}
```

示例实现：

```c
#include<stdio.h>

int main(){

int i = 0;

if( i > 1 ){

printf("The first if construct is executing!");

}

else if(i == 0){

printf("The second if construct is executing!");

}

else{

printf("The else construct is executing!");

}

}
```

这将产生相应的结果：

```
The second if construct is executing!
```

### 嵌套 if...else 语句

嵌套 `if-else` 结构是允许的，这意味着你可以在 `if` 或 `else` 语句内部使用 `if` 或 `else if` 声明。使用该构造的语法如下：

```c
if(条件 1){

// 如果条件 1 为真则执行

if(条件 2){

// 如果条件 2 为真则执行

}

}

else if(条件 3){

// 如果条件 3 为真则执行

}

else

{

// 如果所有条件为假则执行

}
```

示例实现：

```c
#include<stdio.h>

int main(){

int i = 1;

if( i >= 1 ){

printf("The if construct is executing!");

if(i == 1){

printf("The nested if construct is executing!");

}

}

else{

printf("The else construct is executing!");

}

}
```

这将产生相应的结果：

```
The if construct is executing!
The nested if construct is executing!
```

# switch 语句

`switch` 结构允许变量与一组值进行等值比对。每个值被称为一个 `case`，被用于交换的变量会在每个 `case` 中进行检查。使用此决策构造的语法如下：

```c
switch(<条件>){

case value1:

//语句

break;

case value2 :

//语句

break;

default:

// 可选
}
```

以下规则适用于 `switch` 结构：

- 作为 `switch` 解释一部分使用的变量必须是 `short`、`byte`、`char` 或 `int`。
- `switch` 内部可以有任意数量的 `case` 解释。每个 `case` 后面都跟着要与进行对比的值和一个冒号。
- `case` 的值必须与 `switch` 中变量的类型相同，并且必须是一个常量或精确的值。
- 当被交换的变量与某个 `case` 匹配时，该 `case` 之后的声明将一直执行，直到遇到 `break`。
- 当遇到 `break` 时，`switch` 结束，控制流跳转到 `switch` 之后的下一行。
- 并不是每个 `case` 都需要包含 `break`。在没有出现 `break` 的情况下，控制流将贯穿到随后的 `case`，直到遇到 `break` 为止。
- `switch` 语句可以有一个可选的 `default` case，它必须出现在 `switch` 的末尾。`default` case 可用于在没有任何 `case` 成立真时执行某些操作。`default` case 中不需要 `break`。但是，根据惯例，建议使用。

### 示例实现

```c
#include<stdio.h>

int main(){

char mygrade = 'A';

switch(mygrade)

{

case "A" :

printf("Excellent Performance!");

break;

case "B" :

printf("Good Performance!");

break;
default :
printf("Failed");

}
```

使用不同的等级输入汇总并运行上述代码。这将为 `mygrade` 的当前值产生相应的结果：

```
Excellent Performance!
```

C 语言中也允许在 `switch case` 结构中进行嵌套。因此，你可以在一个 `case` 结构内部包含一个 `switch` 结构。

## 函数

函数是一组语句的集合，这些语句共同执行指定的任务。每个 `C` 项目都至少有一个名为 `main()` 的函数。你可以对代码进行划分，并将它们排列成独立的函数。你如何将代码划分为不同的函数取决于你，但从逻辑上讲，划分通常是让每个函数执行一个特定的任务。

函数的声明告知编译器关于函数的名称、返回类型以及函数期望获取的参数。然而，函数的定义才包含了语句的集合。`C` 标准库提供了系统可以调用的各种内置函数。除了其他名称外，函数还被称为子程序（`subroutine`）或技术（`technique`）。

## 函数定义

在 `C` 编程中，函数定义的通用表现如下结构所示：

```c
return_type name_of_fn (list of parameters)
{
// 函数内部的语句
}
```

`C` 编程语言中的函数定义由函数头和函数体组成。以下是函数的所有部分：

- **返回类型 (Return Type)**：函数可能返回一个值，也可能不。`return_type` 是函数返回的值的数据类型。某些函数执行所需的操作而不返回值。在这种情况下，`return_type` 为 `void`。
- **函数名 (Function Name)**：这是函数的实际名称。名称和参数列表共同构成了函数的签名。
- **参数 (Parameters)**：参数类似于占位符。在函数被调用时，你将一个值传递给参数。这个值被称为参数。参数列表指的是函数参数的类型和数量。参数不是强制性的。因此，函数可以完全不包含任何参数。
- **函数体 (Function Body)**：函数体包含一组描述函数功能特征的语句。

### 示例实现

以下示例说明了如何声明和定义函数。涉及的函数是 `max()`，它接受两个参数 `number_1` 和 `number_2`。

```c
int max_num (int number_1, int number_2)

{

int f_result;

if (number_1 > number_2)
f_result = number_1;

else
f_result = number_2;

return f_result;

}
```

### 函数声明

声明语句告知编译器关于函数名称以及如何调用该函数。通常，函数的声明如下方式所示：

```c
return_type name_of_func ( list of parameters );
```

对于我们在上一节中定义的函数，声明可以是以下之一：

`int max_num (int number_1, int number_2);`

`int max_num (int, int);`

### 调用函数

在函数的声明语句中，参数名称并不是必需的。然而，它们的数据类型必须显式提到。在定义或使用函数之前，必须声明该函数。在编写 `C` 函数时，你必须清楚函数需要做什么。要使用一个函数，你需要调用该函数来执行特征的任务。

当项目调用一个函数时，系统控制权会切换到被调用的函数。被调用的函数执行特征赋值，并在执行其 `return` 语句或遇到闭括号时结束。要调用函数，你本质上需要连同名称传递所需的参数。此外，如果函数预期返回一个值，你必须将该值赋值给匹配的变量。



```c
#include <stdio.h>

int max_num (int number_1, int number_2);

int main () {

int num_a = 100; int num_b = 200; int ret_val;

ret_val = max_num (num_a, num_b);

printf( "Max val = %d\n", ret_val );

return 0;

}
```

`max_num()` 函数的定义与之前相同。

此程序的预期输出将为：

```
Max val = 200
```

# 函数参数

如果函数需要使用参数，必须声明变量以及这些变量将包含的值。这些变量被称为形式参数。形式参数在函数内部的作用类似于局部变量。

在调用函数时，有两种方式从调用函数传递参数到被调用函数：

### 值传递 (Call by Value)

值传递策略是将参数的实际值复制到函数的形式参数中。在这种情况下，对函数内部参数的修改不会对参数本身产生影响。自然地，C 语言使用值传递传递参数。上面的示例是简单的值传递。

### 引用传递 (Call by Reference)

引用传递策略是将参数的位置复制到函数的形式参数中。在函数内部，利用该位置来访问实际参数。这意味着对参数的修改会影响传递的参数。

要通过引用传递参数，你需要像传递其他值一样将指针传递给函数。因此，你必须将函数参数声明为指针类型，正如随后的函数 `swap()` 所示，交换参数指示的两个变量的值。下面的函数实现了引用传递。

```c
#include <stdio.h>

void swap_num (int *ptr_x, int *ptr_y);

int main () {

int num_a = 5; int num_b = 15;

printf("Original Value of num_a = %d\n", num_a );

printf("Original Value of num_b = %d\n", num_b );

swap_num (&num_a, &num_b);

printf("Post-swapping value of num_a = %d\n", num_a );

printf("Post-swapping value of num_b = %d\n", num_b );

return 0;

}
```

编译并执行此代码，将产生以下输出：

```
Original Value of num_a = 5
Original Value of num_b = 15
Post-swapping value of num_a = 15
Post-swapping value of num_b = 5
```

从这一讨论可以明显看出，原始参数值在交换后发生了变化。另一方面，如果使用值传递（pass by value）来实现相同的功能，则该程序的输出将是：

`num_a` 的原始值 = 5

`num_b` 的原始值 = 15

交换后 `num_a` 的值 = 5

交换后 `num_a` 的值 = 15（注：此处原文可能存在笔误）

## 作用域规则

作用域定义为变量或函数活跃的区域。因此，变量或函数在该区域之外无法被访问。任何变量或函数的作用域可以分为三大类，并据此变量被称为：

- **局部变量**：在块或函数内部定义和声明的变量称为局部变量。
- **全局变量**：在任何块或函数外部定义和声明的变量称为全局变量。
- **形式参数**：形式参数是函数参数的另一种呼。

## 数组

C 语言允许使用一种名为数组的数据结构。这种数组可以存储相同数据类型的长度变化的连续组件。虽然使用名为数组的结构来存储一组数据，但通常将这种结构视为同类变量的积累会更有帮助。

与声明单个变量（例如 `num_0`、`num_1`……到 `num_99`）相比，你只需要一个数组变量。你可以将变量命名为 `num[100]`，在这种情况下，可以通过 `num[0]`、`num[1]`……到 `num[99]` 来访问数组的各个元素或变量。所有数组由连续或线性的内存区域组成。0 元素对应第一个组件，最后一个位置对应最后一个组件。

### 定义数组

声明数组的语法如下：

`<data type> name_array [ size_array ];`

`double acc_bal [10];`

上述语句中声明的数组具有容纳最多 10 个 `double` 变量的能力。这被称为 1 维数组。`size_array` 必须大于零的数字，数据类型可以是任何合法的 C 数据类型。

### 如何声明数组

你可以通过以下方式逐一引入数组或使用单一语句在 C 中引入数组：

`double bal [5] = {670.0, 267.5, 30.4, 137.0, 560.0};`

### 访问数组元素

可以使用索引值访问数组元素。例如，如果你想访问数组的第一个元素，可以按以下方式访问：

`double x;`

`x = bal [0];`

通过数组名的索引来访问组件。这是通过在数组名后的方括号内放入组件列表来实现的。示例实现

```c
#include <stdio.h>

int main () {

int num [5];

/* num 是一个带有 10 个 int 类型元素的数组 */
int x, y;

/* 将 show n 的组件设置为 0 */
for ( x = 0; x < 5; x++ )
{
num[ x ] = x + 50; // 这条语句将值放入数组元素中
}
for (y = 0; y < 5; j++ )
{
printf("num[%d] = %d\n", y, num[y] );
}

return 0;
}
```

当上述代码编译并执行时，它会产生相应的结果：

```
num[0] = 50
num [1] = 51
num [2] = 52
num [3] = 53
num [4] = 54
num [5] = 55
```

## 多维数组

可以使用以下通用语法声明多维数组。

`<data type> name_array [arr_size_1][arr_size_2]...[arr_size_n];`

C 语言允许多维数组。这里是多维数组声明的示例：

`int arr_3d[2][3][2];`

### 将数组作为函数参数

可以通过三种方式将数组作为参数传递给函数。方法一种是传递数组的指针。如果你需要将数组作为参数传递，你需要在三种模拟方式之一中声明函数形式参数，并且这三条语句都会产生相当的结果，因为每条都会告诉编译器预期一个数字指针。此外，你也可以以相同的方式传递多维数组。

```c
void s_func(int *s_param)
{
.
.
.
}
```

另一种传递数组的方法是将整个数组发送到函数。这种方法的示例实现如下所示：

```c
void s_func (int s_param[5])
{
.
.
.
}
```

将数组传递到函数的最后一种方法在下面的示例代码中描述：

```c
void s_func (int s_param[])
{
.
.
.
}
```

### 从函数获取数组

显易见，由于 C 对形式参数不进行边界检查，数组的长度并没有区别。C 语言不允许返回整个数组。因此，你能做的就是返回数组的指针。换句话说，如果你需要从函数返回一个数组，你需要声明一个返回指针的函数，如下示例所示：

```c
int * s_func()
{
.
.
.
}
```

### 数组指针

如所易见，由于 C 对形式参数不进行边界检查，数组的长度并没有区别。C 语言不允许返回整个数组。因此，你所做的就是返回数组的指针。换句话说，如果你需要从函数返回一个数组，你需要声明一个返回指针的函数，如下示例所示：

```c
int * s_func()
{
.
.
.
}
```

# 指针

C 指针通常是 C 编程中最令人畏惧的话题。然而，让我们先说，指针可能是 C 编程中最容易理解的概念，并且能够满足项目的若干项编程需求。这些任务之一就是动态内存管理。

如之前所述，每个变量都保存在内存位置。变量的内容不仅可以通过变量名访问，还可以通过变量地址访问。指针持有变量的地址。简单来说，指针是一个包含地址的变量。

请注意，可以通过以下方式使用取地址运算符访问变量的地址：

```c
int i;

int *ptr;

ptr = &I;
```

下面给出一个示例实现以更清晰地阐明这一概念。

```c
#include <stdio.h>

int main () {

int  variable_1;

char variable_2 [5];

printf("Variable_1 variable’s address: %x\n", &variable_1 );

printf("Variable_2 variable’s address: %x\n", &variable_2 );

return 0;

}
```

现在，你已经对变量的存储以及如何使用地址来访问变量的值有了了解。

## 什么是指针？

如前所述，指针是任何存储另一个变量地址的变量。指针通常按以下方式声明：

`<data type> * <variable name>;`

在上述声明中，`data type` 是 C 语言允许的任何合法数据类型，变量名是分配给指针的标识符。注意在声明指针时使用了星号运算符。然而，值得注意的是，该运算符也用于乘法。以下是用于不同类型指针的示例声明：

```c
int *ptr; // 指 int 的指针
char *ptr; // 指 char 的指针
float *ptr; // 指 float 的指针
double *ptr; // 指 double 的指针
```

## 使用指针

指针用于若干任务，或者在某些情况下简化执行某些任务的方法。用于此目的的典型步骤包括：

● 定义指针

● 给指针变量分配一个合法的地址

● 使用指针变量访问地址及其内容

请看下面的实现以更好地理解该概念：

```c
#include <stdio.h>

int main () {
  int my_var = 405; 
  int *my_ptr;
  my_ptr = &my_var;
  printf("Variable’s address: %x\n", &my_var );
  printf("Value of address stored in the pointer: %x\n", my_ptr );
  printf("Content of pointer: %d\n", *my_ptr );
  return 0;
}
```

在编译并执行上述代码后，预期会出现以下输出：

```
Variable’s address: bff5a400
Value of address stored in the pointer: bff5a400
Content of pointer: 405
```

## C 语言中的 NULL 指针

你一定已经注意到上面的代码中指针声明没有包含赋值。为了确保不会因为指针声明和赋值产生错误范围，将指针赋值为 `NULL` 被认为是一种良好的编程实践。任何被赋值为 `NULL` 的指针被称为 `NULL` 指针。在大多数工作环境中，`NULL` 的值在标准库中定义为 `0`。该概念的示例实现如下：

```c
#include <stdio.h>

int main () {
  int *my_ptr = NULL;
  printf("my_ptr’s NULL value = : %x\n", &ptr );
  return 0;
}
```

编译并执行代码后，应当出现输出：

```
my_ptr’s NULL value = 0
```

在大多数操作系统上，项目不允许访问地址为 0 的内存，因为操作系统为了自身使用保留了该部分内存。尽管如此，内存地址 0 具有异常的中心性；它标志着指针未计划指向一个开放的内存区域。但根据传统，如果指针包含无效（零）值，则被接受表示“无”。

要检查无效指针，你可以利用如下方代码段所示的 `if` 结构：

```c
if(!ptr) // 表示指针无效
if(ptr) // 表示指针有效
```

## 指针操作

如已阐明，C 指针是一个位置，包含一个数值。因此，你可以像操作其他数值变量一样对指针进行操作。有四种数学运算符可以用于指针：`++`、`-`、`+` 和 `-`。为了理解指针操作，让我们假设 `ptr` 是一个 `int` 指针，指向位置 5000。假设数字是 32 位的，让我们对指针执行相应的数学操作：

### 指针递增

如果我们使用以下语句对指针执行递增操作，你可以预期指针的最终值将变为 `5004`。

```c
ptr++ ;
```

此操作将指针移动到下一个内存位置，而不影响内存区域的值。如果 `ptr` 是指向位置为 5000 的字符的指针，那么由于下一个字符可以在 5001 访问，上述操作将使 `ptr` 指向位置 5001。

考虑到数组具有固定容量，且对数据进行的任何运行时更改都无法调整到系统中，通常首于使用指针而不是数组。以下代码描述了该概念的使用：

```c
#include <stdio.h>

const int MAXVAL = 3;

int main () {
  int my_var[] = {1, 10, 20};
  int x = 0;
  int *my_ptr = NULL;
  ptr = my_var;
  for ( x = 0; x < MAXVAL; x++)
  {
    printf("my_var[%d] address = %x\n", x, my_ptr );
    printf("my_var[%d] value = %d\n", x, *my_ptr );
    my_ptr++;
  }
  return 0;
}
```

当上述代码编译并执行时，它会产生如下结果：

```
my_var [0] address = bf882b30
my_var [0] value = 1
my_var [1] address = bf882b34
my_var [1] value = 10
my_var [2] address = bf882b38
my_var [2] value = 20
```

指向指针的指针是各种重定向的体现，或者说是指针链。通常，指针包含变量的位置。当我们描述一个指向指针的指针时，第一个指针包含第二个指针的位置，而第二个指针指向包含实际值的区域。指向指针的指针的变量必须通过在其名称前添加一个额外的星号 `*` 来声明。示例实现：

```c
int **my_double_ptr;
```

当通过指向指针的指针指示目标值时，获取该值需要连接两次引用运算符，如下方的插所示：

```c
#include <stdio.h>

int main () {
    int my_var;
    int *my_ptr;
    int **my_pptr;

    my_var = 2435;
    my_ptr = &my_var;
    my_pptr = &my_ptr;

    printf("my_var = %d\n", my_var );
    printf("*my_ptr = %d\n", *my_ptr );
    printf("**my_pptr = %d\n", **my_pptr);
    return 0;
}
```

当上述代码编译并执行时，它会产生相应的结果：

```
my_var = 2435
*my_ptr = 2435
**my_pptr = 2435
```

## 将指针传递给函数

C 语言允许你将指针传递给函数。该概念通过以下代码进行了说明：

```c
#include <time.h>
#include <stdio.h>

void get_secs(unsigned long *my_par);

int main () {
    unsigned long my_sec;
    get_secs( &my_sec );
    printf("my_sec = %ld\n", sec );
    return 0;
}

void get_secs(unsigned long *my_par) {
    *my_par = time( NULL );
    return;
}
```

当上述代码编译并执行时，它会产生相应的结果：

```
my_sec = 12456668
```

请注意，任何可以接受指针的函数也可以接受指针数组。

```c
#include <stdio.h>

double get_avg (int *my_arr, int my_arr_size);

int main () {
    int bal[3] = {50, 4, 345};
    double my_avg;
    my_avg = get_avg ( bal, 3 ) ;
    printf("Average = %f\n", my_avg );
    return 0;
}

double get_avg(int *my_arr, int my_arr_size) {
    int x, my_sum=0;
    double my_avg;
    for (x = 0; x < my_arr_size; ++x) {
        my_sum += my_arr[x];
    }
    my_avg = (double)my_sum/my_arr_size;
    return my_avg;
}
```

当上述代码编译并执行时，它会交付相应的结果：

```
Average = 133.000000
```

## 从函数返回指针

正如指针可以作为参数发送到函数一样，它也可以由函数返回。此类结构的声明可以通过如下方式：

```c
int * sample_func () {
    . . .
}
```

## 字符串

C 语言中的字符串是字符的一维展示，以一个称为空字符的 `\0` 的无效字符结束。通过这种方式，字符串包含了属于字符串部分的字符，随后紧跟一个空字符。下面显示的字符串声明创建了一个包含字符‘name’的字符串。请注意声明中使用的额外字符。例如，“name”这个词有 4 个字符。使用长度为 5 的数组包含了空字符串结束字符。



```c
char str_name[5] = {'n', 'a', 'm', 'e', '\0'};
char str_name[] = "name";
```

在第二种声明中，你不需要将无效字符放在字符串的末尾。C 编译器在引入数组时，自然会在字符串末尾放置 `"\0"`。这里有一个使用该概念的代码示例：

```c
#include <stdio.h>

int main () {
    char str_name[5] = {'n', 'a', 'm', 'e', '\0'};
    printf("Message: %s\n", str_name );
    return 0;
}
```

当上述代码编译并执行时，它会产生以下结果：

```
Message: name
```

## 字符串函数

- `strcat(str_1, str_2);`: 此函数将字符串 `str_2` 接到字符串 `str_1` 的末尾。

- `strcpy(str_1, str_2);`: 此函数将字符串 `str_2` 复制到字符串 `str_1` 中。

- `strcmp(str_1, str_2);`: 如果两个比较的字符串相等，此函数返回值 `0`。如果返回任何非 `0` 值，则表示字符串不等。

- `strlen(str_1);`: 此函数返回相关字符串的长度。

- `strstr(str_1, str_2);`: 此函数匹配两个字符串，并返回 `str_2` 在 `str_1` 中首次出现的位置索引。

- `strchr(str_1, ch);`: 此函数返回字符串 `str_1` 中字符 `ch` 首次出现处的指针。

当上述代码被编译并执行时，它产生相应的结果：

```
ID of Book: 10002976
Title of Book: Humpty Dumpty
Author of Book: Humpty
Subject of Book: Nursery Rhyme
```

## 结构体指针

你可以以声明其他变量指针非常相似的方式来声明结构体指针。可以使用以下构造来执行此任务：

```c
struct BookRecord *s_ptr;
```

为了给结构体附加指针，必须使用以下语句：

```c
S_ptr = &mybook_1;
```

可以使用以下方式通过重定向运算符 (`->`) 访问结构体的成员：

```c
s_ptr->title;
```

上述代码可以重构为以下安排，以调整结构体指针的使用：

```c
#include <string.h>
#include <stdio.h>

struct BookRecord
{
char  title[50];
char  author[50];
char  subject[100];
int  bookID;
};

void printBookRecord ( struct BookRecord *mybook );

int main ( )
{
struct BookRecord myBook_1;
struct BookRecord myBook_2;
//Adding elements to the structure
strcpy( myBook_1.author, "Humpty");
strcpy( myBook_1.title, "Humpty Dumpty");
myBook_1.bookID = 10002976;
strcpy( myBook_1.subject, "Nursery Rhyme");
//Printing the structure elements
printBookRecord ( &myBook_1 );
return 0;
}

void printBookRecord ( struct BookRecord *myBook )
{
printf( " ID of Book: %d\n", myBook->bookID);
printf( " Title of Book: %s\n", myBook->title);
printf( " Author of Book: %s\n", myBook->author);
printf( " Subject of Book: %s\n", myBook->subject);
}
```

当上述代码被编译并执行时，它产生相应的结果：

```
ID of Book: 10002976
Title of Book: Humpty Dumpty
Author of Book: Humpty
Subject of Book: Nursery Rhyme
```

## 联合体

联合体（union）是 C 语言中一种独特的数据类型，它允许你在同一内存区域存储不同的数据类型。你可以声明一个包含多个元素的联合体，但同一时间联合体只能有一个元素包含值。联合体为出于多种目的使用同一内存区域提供了一种高效的方法。这里必须提到，分配给联合体的内存等于联合体中最大元素的大小。

### 如何声明联合体

要声明联合体，必须使用联合体声明，其构造与结构体声明相似。联合体构造创建一个新的数据类型，该类型由其他几个数据类型组成。声明联合体的标准语法如下：

```c
union [union tagname]
{
//Declaration of elements to be included in the union
} [union variablenames];
```

联合体的 `tagname` 是可选的，且联合体构造中的每个声明都是典型的变量声明。因此，你可以使用任何变量、数组或指针声明。在联合体声明的最后、分号之前，你可以指定一个或多个联合体变量。然而，这不是强制的。下面的代码段说明了如何声明和定义联合体。

```c
union myData {
char name[20];
int count;
float averageval;
} g_data;
```

目前，通过该声明创建了一个类型为 `myData` 的变量。该数据类型可以存储数字、浮点数或一系列字符。联合体拥有的内存将足够容纳联合体中最大的组件。例如，在上面的示例中，`myData` 将拥有 20 字节的内存空间，因为这是字符字符串使用的最大空间。下面的代码显示了如何计算联合体占据的内存大小。

```c
#include <string.h>
#include <stdio.h>

union myData {
char name[20];
int count;
float averageval;
} ;

int main( ) {
union myData data_1;
printf( "Memory of data_1 = %d\n", sizeof(data_1));
return 0;
}
```

当上述代码被编译并执行时，它产生相应的结果：

```
Memory of data_1 = 20
```

### 访问联合体成员

要访问联合体的任何组件，我们使用点运算符 (`.`)。该运算符被编码为联合体变量名与你想访问的联合体组件之间的句号。你会使用 `union` 关键字来声明联合体类型的变量。该概念的示例实现如下：

```c
#include <string.h>
#include <stdio.h>

union myData {
char name[20];
int count;
float averageval;
} ;

int main( ) {
union myData data_1;
strcpy( data_1.name, "Coding");
data_1.count = 100;
data_1.averageval = 22.45;
printf( "data_1.name = %s\n", data_1.name);
printf( "data_1.count = %d\n", data_1.count);
printf( "data_1.averageval = %f\n", data_1.averageval);
return 0;
}
```

当上述代码被编译并执行时，它产生相应的结果：

```
data_1.name = Coding
data_1.count = 100
data_1.averageval = 22.45
```

## 头文件

头文件是一个 C 文件，以 `.h` 扩展名保存，包含宏定义和 C 函数声明。此外，多个 C 文件也可以包含在头文件中。头文件有两种类型：开发者编写的文件和属于 C 包的文件。

你通过包含头文件（使用 C 预处理指令 `#include`）来请求在项目中使用头文件，就像我们在书中编写的大部分代码中看到的包含 `stdio.h` 头文件一样。

### 包含操作

为了包含头文件，你必须使用以下语句之一：

```c
#include <filename>

#include " filename "
```

这种结构用于框架头文件。它在标准框架索引列表中查找名为 `document` 的记录。在编译源代码时，可以通过 `-I` 选项向此列表添加额外的索引。

这种结构用于你项目的头文件。它在包含当前文件的索引或目录位置查找名为 `filename` 的文件。

```c
char *s_test (void);
```

`#include` 操作符合预期，它通过协调 C 预处理器在处理当前源文件剩余内容之前，输出详细文件内容作为信息。预处理器的输出包含了官方创建的输出，紧接着是来自被包含文档的输出，而这部分是由 `#include` 指令之后的内容所模拟的输出。

## 单次包含头文件 (Once-Only Headers)

在极少数情况下，如果头文件被意外包含了两次，编译器将处理两次其内容。结果是相同的变量和函数声明可能会重复。这将不可避免地导致编译错误。为了避免这种情况，最好使用以下构造结构：

```c
#ifndef H_file
#define H_file

// 需要被包含的头文件

#endif
```

这种构造通常被称为包装器 `#ifndef`。当头文件再次被包含时，`#ifndef` 指令返回假值，`#include` 语句将不会被处理。预处理器将跳过相关文件的全部内容，编译器将不会再次看到它。

## 计算型包含 (Computed Includes)

有时，从几个不同的头文件中选择一个包含到你的项目项目中是重要的。它们可能声明用于各种工作框架的设置参数。你可以通过类似于下方的条件组合来实现：

```c
#if Sys_1
#include "sys_1.h"
#elif Sys_2
#include "sys_2.h"
#elif Sys_3
...
#endif
```

同时，你必须注意到声明会变得重复。因此，预处理器提议使用宏作为头文件名。这被称为计算型包含。与直接将头文件名组合作为 `#include` 的直接参数不同，你基本上是在该处放置了一个宏名：

```c
#define Sys_h "sys_1.h"
...
#include Sys_h
```

`Sys_h` 将被计算，预处理器将搜索 `sys_1.h`，就像 `#include` 是按照最初的方式组合的一样。`Sys_h` 可以在 makefile 中使用 `-D` 编译器选项进行声明。

## 类型转换 (Typecasting)

类型转换是一种将一种数据类型的变量转换为另一种数据类型的方法。通常，类型转换是使用构造结构完成的：

```c
(<data_type>) declaration
```

例如，如果你需要将一个长整型（`long`）值存储到简单的整数（`int`）中，那么你可以将 `long` 转换为 `int`。你可以利用给定的工具明确地将值从一种类型转换为下一种类型。考虑以下示例，其中转换运算符导致一个整数变量除以另一个变量的操作被作为浮点数执行。

```c
#include <stdio.h>

int main ()
{
    int x = 21, y = 4;
    double div;
    div = (double) x/y;
    printf("Value of div = %f\n", div );
}
```

在编译和执行后，预期会有以下输出。

```
Value of div = 5.250000
```

在这里必须注意，转换运算符的优先级高于除法，因此 `div` 的估值首先转换为数据类型 `double`。结果是除法后获得的值是 `double`，并可以赋值给 `div`，`div` 也是一个 `double` 类型的变量。

类型转换也可以是隐含的。编译器执行这种形式的类型转换，或者可以通过使用转换运算符强制进行。在任何需要类型转换的地方使用转换运算符被视为良好的编程习惯。

## 整数提升 (Integer Promotion)

整数提升是将类型比 `int` 或 `unsigned int` “小”的数值类型转换为 `int` 或 `unsigned int` 的过程。考虑在 `int` 中包含一个字符的情况：

```c
#include <stdio.h>

int main () {
    int k = 5;
    char ch = 'c';
    int s_total;
    s_total = k + ch;
    printf("s_total = %d\n", s_total );
}
```

当上述代码被编译并执行时，它产生了如下结果：

```
Value of s_total : 104
```

结果的结果是因为 `'c'` 的 ASCII 等效值是 99。当 99 加上 5 时，最终值变为 104。

## 常规算术转换 (Normal Arithmetic Conversion)

常规数学转换无疑会被执行以将它们的值转换为典型数据类型。编译器首先执行整数提升。如果操作数仍然具有不同的类型，它们将被转换为后续顺序中似乎最重要的类型：

常见的数值处理转换不会为任务运算符执行，也不会为逻辑运算符 `&&` 和 `||` 执行。给我们一个机会通过模拟示例来理解这个概念：

```c
#include <stdio.h>

int main () {
    int k = 5;
    char ch = 'c';
    float final;
    final = ch + k;
    printf("final = %f\n", final );
}
```

当上述代码被编译并执行时，它输出了如下结果：

```
final = 104.000000
```

在这里，很容易理解 `c` 首先被转换为整数。然而，由于最后一个值是双，所以应用了常规数学转换，编译器将 `k` 和 `ch` 转换为 `float` 数据类型。最后，这个值被赋值给 `final`。

## 输入输出 (Input & Output)

当我们使用输入时，我们的意图是发送到系统的信息。另一方面，当我们谈论输出时，我们的目标是在屏幕上显示某些信息。

### 标准文件 (Standard Files)

C 语言将所有输入视为文件。例如，键盘是以相同的方式处理的。这里是对应的文件：

- 标准文件 - `stdin`

- 标准输入 - `stdin`

- 标准输出 - `stdout`

- 标准错误 - `stderr`

### 函数 - `getchar()` 和 `putchar()`

`getchar()` 函数从屏幕上读取字符并将其返回为整数。该函数一次只读取一个字符。在需要从屏幕上读取多个字符时，你可以使用这种策略。

`putchar()` 函数将给定的字符放在屏幕上。该函数一次只显示一个字符。在需要从屏幕上显示多个字符时，你可以使用这种策略。

以下代码说明了这些函数：

```c
#include <stdio.h>

int main ()
{
    int x;
    printf("Enter a number:");
    x = getchar( );
    printf("\nNumber entered: ");
    putchar( x ); // 注意：此处原文为 c，根据语境应为变量 x
return 0;
}
```

当上述代码被编译并执行时，你会发现系统在等待你输入一个字符。当你输入一个字符并按回车时，程序读取字符，然后将字符显示在屏幕上。

### 函数 - `gets()` 和 `puts()`

`gets()` 函数从 `stdin` 读取一行到 `str` 指向的数组，直到遇到换行符或 EOF。另一方面，`puts()` 函数将字符串 `str` 和一个随后的换行符写入 `stdout`。这些内置函数的用法在以下代码中说明：

```c
#include <stdio.h>

int main()
{
    char my_str[50];
    printf("Enter text:");
    my_str = gets( my_str );
    printf("\nText received: ");
    puts( my_str );
return 0;
}
```

当上述代码被编译并执行时，系统在等待你输入一些文本并按回车。当你输入一些文本并按回车时，程序读取它并将其内容输出到屏幕上。

## 函数 - `scanf()` 和 `printf()`

函数 `int scanf(const char *formatstr, ...)` 从标准数据流 `stdin` 中读取信息。另一方面，函数 `int printf(const char *formatstr, ...)` 将文本写入标准输出流 `stdout`。在给定的函数声明中指定的 `formatstr` 提供了 `%d`、`%s`、`%f`、`%c` 等。这些字符串用于打印或读取字符串、字符、整数或浮点数。以下代码演示了这些函数的使用：

```c
#include <stdio.h>

int main ( )
{
    char my_str[50];
    int x;
    printf( "Enter value:");
    scanf("%d", &x);
    printf( "\nEntered number = %d ", x);
    return 0;
}
```

当上述代码编译并执行时，它会停等待你输入内容。当你输入一个整数并按回车时，程序将返回并读取数据。因此，相同的文本将打印在屏幕上。



在这里，应该注意`scanf()`期望与格式字符串中提到的相同类型的数据。如果你给出“字符串”而不是整数，它将被视为错误输入。其次，当`scanf()`在读取一个字符串时，系统一旦遇到空格就会退出。因此，当你写`a b c`时，`a`、`b`和`c`对于`scanf()`来说是三个不同的字符串。

# 文件输入与输出

上一节澄清了 C 语言提供的标准输入和输出函数。这一部分我们将了解 C 软件开发者如何创建、打开、关闭和编辑文件。

文件是字节的组。但是，请记住，对于 C 来说，每个输入或输出设备都是文件，且文件之间没有区别。C 编程语言提供了访问低级（操作系统级）调用来处理文件。这部分将带你了解处理文件所需的本质函数和编程结构。

## 打开文件

你可以利用`fopen()`函数创建一个新文件，或者按指定的名称和模式打开一个当前文件。此调用将实例化`FILE`类型的对象，该对象包含控制文件流所需的所有数据。函数调用可以以以下方式进行：

`File *fopen( const char * samplefile, const char * filemode );`

在这里，`samplefile`是包含文件名的字符串，你用它来命名你的文件。函数调用的第二个参数是访问模式，它可以取以下值之一：

- `r`: 仅用于读取目的打开当前文件。

- `w`: 打开文件进行写入。然而，如果文件不存在，则会创建一个指定名称的文件。在这里，你的系统将从记录的最开始开始编写内容。

- `a`: 以追加模式打开文件进行写入。然而，如果文件不存在，则创建另一个记录。在这里，你的系统将从已写内容结束的地方追加文件。

- `r+`: 同时以读写模式打开文件。

- `w+`: 同时以读写模式打开文件。如果文件存在，它首先将其截断为零长度。然而，如果没有文件，则创建一个新文件。

- `a+`: 同时以读写模式打开文件。如果文档不存在，则创建该文档。读取将从最早点开始，但写入必须是追加。

如果你将处理二进制文件，将使用下面指定的访问模式而不是上述模式：

`"wb", "rb", "rb+", "ab", "wb+", "r+b","ab+", "w+b" and "a+b"`

## 关闭文件

要关闭记录，请利用`fclose()`函数。此函数调用的语法如下：

`int fclose( FILE *fptr );`

## 如何写入文件

为了向文件写入，使用了以下函数：

`int fputs( const char *str, FILE *fptr );`

`int fputc( int ch, FILE *fptr );`

函数`fclose()`在成功时返回 0，如果发生某些错误则返回`EOF`。

此函数会刷新当前在文件数组中等待的所有信息，关闭文件，并释放用于文档的任何内存。`EOF`在头文件`stdio.h`中声明并定义。

C 标准库提供了不同的函数来逐字符或逐行地读取和编写文件。随后的章节讨论了其中一些函数：

- `fputc()`函数将参数`ch`的字符值写入由`fptr`指向的输出流。成功时提供一个相应的已写入字符，如果发生故障则返回`EOF`。

- `fputs()`函数将字符串`s`写入由`fptr`指向的输出流。成功时返回非负值，如果发生任何故障则返回`EOF`。你也可以利用`int fprintf(file *fptr, const char *formatptr, ...)`来将字符串写入文件。尝试以下代码：

```c
#include <stdio.h>

int main () {
    File *fptr;
    fptr = fopen("sample.txt", "w+");
    fprintf(fptr, "fprintf executing..\n");
    fputs("fputs executing..\n", fptr);
    fclose(fptr);
}
```

当上述代码编译并执行时，它会创建一个`sample.txt`。

## 如何读取文件

为了读取文件，常用以下两个函数：

`int fgetc( FILE *fptr );`

`char *fgets( char *buffer, int count, FILE *fptr );`

`fgetc()`从`fptr`指向的文件读取一个字符。如果发生故障，返回的值将为`EOF`。`fgets()`从`fptr`指向的数据流读取最多`(count – 1)`个字符。如果遇到空格则会停止。

```c
#include <stdio.h>

int main() {
    File *fptr;
    fptr = fopen("sample.txt", "r");
    fscanf(fptr, "%s", buffer);
    printf("1 : %s\n", buffer);
    fgets(buffer, 255, fptr);
    printf("2: %s\n", buffer);
    fgets(buffer, 255, fptr);
    printf("3: %s\n", buffer);
    fclose(fptr);
}
```

## 二进制 I/O 函数

C 标准库提供了两个函数，可以用于二进制输入输出：

`size_t fread(void *s_ptr, size_t element_size, size_t elements_num, FILE * file_ptr);`

`size_t fwrite(const void *s_ptr, size_t elements_size, size_t elements_num, FILE * file_ptr);`

该指令是一个条件指令，跟在`if`指令之后。

- ● `#elif`

该指令是一个条件指令，是`#if`和`#else`的组合。

- ● `#endif`

该指令是一个条件指令，用于结束`#if`。

- ● `#error`

该指令用于错误报告。

- ● `#pragma`

该指令向编译器发出特殊的传唤，并利用了一项制度化的策略。

## 预处理器示例

以下是几个预处理器指令的示例，供你参考和理解。

- ● `#define MAXVAL 5`

该指令建议 C 预处理器将宏`MAXVAL`的所有出现处替换为整数值`5`。这种类型的宏定义常用于定义常量。

- ● `#include <stdio.h>`

这些指令建议 C 预处理器从系统库中获取`stdio.h`并将其内容添加到当前源文件中。这是包含标准 C 库中任何头文件的标准方法。

- ● `#include "myheader.h"`

该行建议 C 预处理器从本地注册表中获取`myheader.h`并将其内容添加到当前源文件中。这种文件包含方法通常用于包含与源文件处于相同位置的用户自定义创建的头文件。

## 预定义宏

C 库中预定义了一些宏。其中一些宏是`MESSAGE`和`DEBUG`。它们的用法和语法如下：

### 示例 1:

此示例告诉预处理器，如果`MESSAGE`尚未被定义，则必须将其定义为“Here I am!”。

```c
#ifndef MESSAGE
#define MESSAGE "Here I am!"
#endif
```

### 示例 2:

这些语句告诉预处理器，如果定义了`DEBUG`宏，则必须执行`#ifdef`之后发生的后续语句。

```c
#ifdef DEBUG
//Debugging statements
#endif
```

除了这些之外，C 编程环境还提供了其他宏，如下文所述所示：

- ● `__time__`

该宏按以下格式定义当前时间 - "HH:MM:SS"。

- ● `__date__`

该宏按以下格式定义当前日期 - "MMM DD YYYY"。

- ● `__line__`

该宏定义当前行号。

- ● `__file__`

该宏定义当前文件名。

- ● `__stdc__`

如果编译器遵循标准 ANSI，则此宏的值被设置为`1`。

## 预处理器运算符

- **宏延续 (`\`)**

  宏定义理想情况下必须结束在与其开始的同一行上。然而，对于参数化宏（将在下一节中讨论），你可能需要多行来定义该宏。如果你的宏延续到下一行，则前一行必须以宏延续运算符`\`结尾。

- **字符串化 (`#`)**

  每当在宏定义中使用该运算符时，它都被用于将宏的任何参数转换为字符串类型的常量。

- **标记粘接 (`##`)**

  该运算符执行组合功能。因此，如果该运算符在宏定义中与两个运算符一起使用，这些参数将被转换为单个参数。

- **`defined()` 运算符**

  提供此运算符是为了帮助开发者确保并检查标识符是否有匹配的宏定义。如果存在相关标识符的宏定义，该函数返回真。

## 参数化宏

C 预处理器的影响能力之一是利用参数化宏来模拟函数的能力。以下是此类构造的示例：

```c
int square_num(int i) { return i * i;}
```

带有参数的宏必须在使用它们之前通过`#define`进行定义。参数列表被封装在括号中，并且必须紧跟在宏后面。宏名和左括号之间不允许有空格。

## 错误处理

C 语言没有直接提供异常处理的支持。然而，作为一种编程语言，它通过返回值的形式为你提供了较低层级的访问。绝大多数 C 甚至 Unix 函数调用在发生任何错误时都会返回`-1`或`NULL`，并设置代码`errno`。这是一个全局变量，显示了错误发生的原因。你可以发现不同的错误代码。这些代码在头文件`<error.h>`中声明。

因此，C 开发者可以检查返回值并根据返回值采取适当行动。作为良好的实践，设计者在引入系统时应当将`errno`设置为`0`。值`0`表示系统中没有错误。

### `errno`、`perror()` 和 `strerror()`

C 编程语言提供了`strerror()`和`perror()`函数，它们可用于显示与`errno`相关的即时消息。

- `perror()`函数显示字符串，随后是冒号、空格以及当前`errno`值的字面表示。

- `strerror()`函数返回一个指向当前`errno`值的文本表示的指针。

下面的代码说明了异常是如何发生的以及如何在 C 中进行处理的。

```c
#include <errno.h>
#include <string.h>
#include <stdio.h>
extern int errno ;

int main () {
    File * s_f;
    int err_num;
    s_f = fopen ("file_sample.txt", "wb");
    if (s_f == NULL)
    {
        err_num = errno;
        fprintf(stderr, " errno = %d", err_num);
    }
```

需要注意的是，函数`s_func()`的最后一个参数是省略号`(...)`，而省略号之前的参数一定是一个`int`类型，它表示传递的参数总数。要使用此功能，你必须利用`stdarg.h`头文件，该头文件提供了实现变长参数功能的宏和函数，并遵循以下步骤：

● 定义一个函数，其最后一个参数为省略号，倒数第二个参数为`int`类型，用以定义参数的个数。

● 在函数定义中创建一个`va_list`类型的变量。该类型在`stdarg.h`头文件中定义。

● 使用`int`参数和`va_start`宏将`va_list`变量初始化为参数列表。`va_start`宏在`stdarg.h`头文件中定义。

● 使用`va_list`变量和`va_arg`宏获取参数列表中的所有内容。

● 使用`va_end`宏来清理为`va_list`变量分配的内存。

下面的代码详细地说明了变长参数的概念。

```c
#include <stdarg.h>
#include <stdio.h>

double s_average(int s_num,...)

{
va_list valist;
double aggregate = 0.0;
int i;
va_start(valist, s_num);
for (k = 0; k < s_num; k++)
{
aggregate += va_arg(valist, int);
}
va_end(valist);
return aggregate/s_num;
}

int main()
{
printf("Average of 2, 3 = %f\n", s_average(2, 2, 3));
printf("Average of 4, 7, 1 = %f\n", s_average(3, 4, 7, 1));
}
```

当上述代码编译并执行时，它会输出如下结果。需要注意的是，函数`s_average()`被调用了两次，每次第一个参数都表示传递的变长参数总数。

预期输出：

Average of 2, 3 = 1.500000

Average of 4, 7, 1 = 4.000000

# 命令行参数

在执行 C 项目时，可以从命令行传递几个值。当你需要从外部控制系统，而不是将这些值硬编码在代码内部时，这些参数对你的项目至关重要的。命令行参数由`main()`函数处理，其中`argc`指代传递的参数个数，而`argv[]`是一个指针数组，指示提供给系统的每一个参数。下面的示例代码详细地说明了这一概念。

```c
#include <stdio.h>

int main( int argc, singe *argv[] )
{
if( argc == 2 )
{
printf("Total number of arguments = %d\n", argc);
}
else if( argc > 2 )
{
printf("Too many arguments\n");
}
else
{
printf("Too few arguments\n");
}
}
```

当上述代码使用单个参数编译并执行时，会产生如下结果：

Too few arguments

当上述代码使用两个参数编译并执行时，会产生如下结果：

Total number of arguments = 2

当上述代码使用两个参数编译并执行时（注：原文此处可能有误，通常指三个及以上），会产生如下结果：

Too many arguments

需要注意的是，`argv[0]`保存的是项目本身的名称，`argv[1]`是指向第一个参数的指针，而`argv[n]`是最后一个参数。在没有提供参数的情况下，`argc`的值通常等于 1；如果你此时传递了一个参数，`argc`则为 2。你通过空格分隔传递所有命令行参数，但如果参数本身包含空格，你可以通过将其放在引号`""`或单引号`''`中来传递此类参数。

# 内存管理

关于内存管理的章节将澄清 C 中动态内存的使用和实现。C 语言提供了几个用于内存分配和管理的函数。这些函数可以在`<stdlib.h>`头文件中找到。

### 函数与描述

● `void free(void *address);`

此函数释放从给定地址开始的内存块。

● `void *calloc(int num, int size);`

此函数分配一组包含`num`个组件的内存，每个组件的大小（字节）为参数`size`。

● `void *realloc(void *address, int newsize);`

此函数重新分配内存，将其扩展到`newsize`参数指定的大小。

● `void *malloc(int num);`

此函数释放与请求字节数相同的内存块，并返回所分配内存块的地址。

### 动态分配内存

在编程时，如果你对数据的大小了然，那么就很简单，你可以将其声明为数组。例如存储任何人的名字，最多可以是 250 个字符。因此，这个名字可以声明为：

`char name[250];`

尽管如此，考虑一种你完全不知道要存储的`char`字符串长度的情况。例如，你需要存储关于某个主题的描述。在这里，我们需要声明一个指向字符的指针，而不声明所需的内存数量。稍后我们可以如下例所示分配内存：

```c
#include <string.h>
#include <stdlib.h>
#include <stdio.h>

int main () {
char s_name[250];
char *s_desc;
strcpy(s_name, "Alice");
s_desc = malloc(50 * sizeof(char));
if (s_desc == NULL ) {
fprintf(stderr, "Required memory not available");
}
else {
strcpy(s_desc, "Alice in wonderland");
}
printf("Name: %s\n", s_name);
printf("Desc: %s\n", s_desc);
}
```

编译并执行后，预期输出如下：

Name: Alice

Desc: Alice in wonderland

上述任务可以使用`calloc()`函数完成。使用`calloc()`代替`malloc()`函数可以使用：

`calloc(50, sizeof(char))`

这样你就有了完全的控制权，并在分配内存时传递任何大小。这与一旦声明就无法更改的数组不同。

### 调整大小与释放内存

当项目结束时，系统会释放所有内存，但当你不再需要它时，应该调用`free()`函数来释放内存。同样，你可以通过调用`realloc()`来增加或减少内存。下面的代码说明了这一点：



```c
#include <string.h>
#include <stdlib.h>
#include <stdio.h>

int main () {
    char s_name[50];
    char *s_desc;
    strcpy(s_name, "Alice");
    s_desc = malloc(6 * sizeof(char));
    if (s_desc == NULL ) {
        fprintf(stderr, "Memory cannot be allocated");
    }
    else {
        strcpy(s_desc, "Alice in wonderland.");
    }
    s_desc = realloc(s_desc, 23 * sizeof(char));
    if (s_desc == NULL ) {
        fprintf(stderr, " Error: Memory cannot be allocated");
    }
    else {
        strcat(s_desc, "She is a wonderful girl.");
    }
    printf("Name: %s\n", s_name);
    printf("Desc: %s\n", s_desc);
    free(s_desc);
}
```

当上述代码编译并执行时，它会输出如下结果：

```
Name: Alice
Desc: Alice in wonderland.She is a wonderful girl.
```

# 面向对象编程简介：类

- 运算符重载
- 类之间的继承
- 实现多态性
- 函数模板与类模板
- 命名空间
- 异常处理
- 类型转换
- 预处理器指令
- C++ 标准库 – 文件输入/输出
- 附录

# C++ 基础

C++ 是一种面向对象的语言，其大部分特性和基础构造都源于 C。这也许就是 C++ 被称为 C 的“超集”的原因。任何用 C 语言编写的程序在法律和语法上都是 ANSI C++ 程序。然而，这一陈述的反面并非如此。在不纠结于理论的情况下，让我们直接进入编程，这无疑是学习任何编程语言的最佳方式。

## 一个基础的 C++ 程序

最简单的入门程序是在屏幕上打印“Hello World”的程序。该程序的代码如下：

代码：

```cpp
// Simple C++ Program
#include <iostream>

using namespace std;

int main ()
{
    cout << "Hello World!";
    return 0;
}
```

输出：

```
Hello World!
```

在继续之前，让我们逐行分析这个程序。第一行是注释行。这一行不包含在机器运行的实际代码中。它仅供开发者日后参考，并更容易理解代码。在 C++ 中编写注释有两种方法。其中一种方法在文本前使用 `//`，另一种方法在文本前使用 `/*` 并在结束处使用 `*/`。

第二行使用 `#include` 并将 `iostream` 库引入代码中。该库促进了输入/输出操作，并允许用户使用控制台进行输入和获取输出。第三条语句指定了代码正在使用`std`命名空间。`std`命名空间包含了 C++ 包中所有的内置库。因此，如果你希望使用这些库中的任何一个，那么包含该语句对你来说是至关重要的。

打印“Hello World!”的程序从第四条语句开始。`main()`函数是 C++ 编程语言中执行开始的函数。`main()`必须返回一个整数值。函数的范围使用大括号`{`和`}`来描述。

函数体包含两条语句。第一条语句使用标准 I/O 操作`cout`，用于在屏幕上打印指定的输出。类似的函数`cin`用于从控制台获取输入。而`cout`操作使用`<<`运算符，`cin`操作则使用`>>`运算符。下一条语句返回一个整数值，如前所述。

这两条语句都以分号（`;`）结束，这是 C++ 的标准。然而，此规则不适用于像`include`这样的指令。需要注意的是，C++ 并不是特定的格式。因此，你可以将所有语句连续写，用分号隔开写在同一行。为程序提供适当的结构使其更具可读性并易理解。

请注意，编写、编辑、编译和运行程序的指令取决于编译器。如果你在 Windows 上，可以使用 Dev-C++ 或 Turbo C；在 Unix/Linux 或 Mac 上，可以使用任何 GCC 编译器。

# 数据类型、变量和常量

虽然上一章所示的程序相当简单且用途存疑，但它应该为开始 C++ 编程奠定必要的基础。显而易见，编程不仅仅局限于在控制台上打印文本。事实上，它比这复杂得多。当我们深入研究这种编程语言的复杂性时，首先要看的是变量。

当你还是个孩子学习加减法时，你的老师或父母一定要求你在记忆中保留一个数字，然后记住第二个数字。一旦你有了这两个数字，就必须将它们相加并记住结果。当我们提到“记住”这个操作时，在计算机语境下实际上指的是一个变量。

因此，变量可以简单地描述为存储定义值的内存单元。例如，如果你看加法的示例，可以假设有两个单元`a`和`b`。

## 标识符

记住内存地址并在每次需要时引用它们是很困难的。为了解决这个问题，引入了标识符的概念。标识符是赋予内存单元的名字。用作变量的标识符应该是有效的。有几条规则决定了标识符是否有效，如下：

1. 应该是字母、数字和下划线（`_`）的序列。
2. 不应包含空格、符号或标点符号。
3. 应该以下划线或字母开头。
4. 不应该以数字开头。
5. 不应该是关键字。章节末尾提供了保留关键字列表。请注意，某些编译器可能不支持以下划线开头的关键字。它们被留给编译器使用。此外，C++ 是区分大小写的。因此，`x`和`X`是不同的变量。

## 基础数据类型

回到加法示例，你天生知道你正在记住两个整数。对于计算机来说并非如此，因为在任何处理发生之前，你需要显式地声明一切。因此，你需要告诉计算机你准备在变量中存储什么类型的数据。只有在声明之后，计算机才会为变量分配内存。

下表显示了基础数据类型、它们的内存需求以及它们包含内容的简要描述。然而，请注意内存大小取决于机器和系统。表中的数值对于标准的 32 位机器是真实的。

| 数据类型 | 内存需求 | 描述 |
| :--- | :--- | :--- |
| `char` | 1 字节 | 任意字符 |
| `short int` | 2 字节 | 短整数 |
| `int` | 4 字节 | 标准整数 |
| `long` | 4 字节 | 长整数 |
| `float` | 4 字节 | 浮点数 |
| `double` | 8 字节 | 双精度浮点数 |
| `long double` | 8 字节 | 长双精度浮点数 |
| `bool` | 1 字节 | 布尔 |
| `wchar_t` | 2 字节/4 字节 | 宽字符 |

## 变量声明

可以使用以下语句声明变量：

`<数据类型> <标识符>`

示例：

`int a;`

该语句声明变量`a`将包含整数值。该语句有几种变体。你可以按照以下方式使用同一条语句定义变量。

`int a = 0;`

此声明将值`0`赋值给变量`a`。

此外，你还可以使用同一语句声明多个变量。示例所示：

`int a, b, c;`

在这种情况下，所有变量`a`、`b`和`c`都被声明为整数。

整数（`int`、`short`和`long`）可以声明为有符号的或无符号的。你需要在语句中如下方式使用`signed`和`unsigned`关键字：

```cpp
signed int a;
```

或者

```cpp
unsigned int a;
```

在没有关键字的情况下，系统假设该变量本质上是有符号的。你也可以在`char`上使用`signed`和`unsigned`关键字。如果你使用`unsigned char`，那么你只能在变量中存储字符。然而，如果你使用`signed char`，你就可以在变量中存储一个字节长度的整数。

# 变量的作用域

按照规则，你只有在声明变量后才能使用它。此外，还存在一个“作用域”的概念。作用域分为两种：全局和局部。如果一个变量声明在代码体之外，则说该变量具有全局作用域。结果，该变量对程序的所有函数都可用。

任何在代码体内部声明的变量本质上都是局部的，并且具有局部作用域。变量的作用域限制是变量所在的块，该块由闭合的大括号`{`和`}`定义。

## 变量的初始化

当你声明一个变量时，它包含垃圾值。换句话说，变量的值是不可知的。为了让变量变得可用且有用，你需要通过给它赋值一个值来定义它。变量的初始化可以通过两种方法完成。

根据第一方法，变量必须在声明时定义。

标准格式：

`<类型 标识符> <变量> = <值>`

示例实现：

```cpp
int a = 0;
```

另一种类型的初始化使用了构造函数方法。

标准格式：

`<类型 标识符> <变量>(值)`

示例实现：

```cpp
int a(0);
```

## 字符串

字符串是一种数据类型，用于存储非数值值。长度和值的数量大于或等于 1。C++ 标准库支持“字符串”数据类型。然而，为了使用库中包含的功能，你必须如下所示包含头文件`string`。

```cpp
#include<string>
```

字符串可以按以下方式声明和定义：

```cpp
string name = "John";
```

完成相同任务的另一种方法是：

```cpp
string name;
name = "John";
```

## 常量

包含固定值的表达式称为常量。

### 字面量

字面量用于表示源代码中的具体值。例如，在上一个示例中赋值给变量的整数如`0`就是一个字面量。有几种类型的字面量常量，将在后续章节中描述。

### 整数数字

它们是区分数字十进制特性的数值常量。请注意，为了表示一个数值常量，我们不需要使用任何特殊字符或引号。每当我们在系统中写下`1871`时，我们都在引用`1871`这个值。

除了十进制数（我们每个人都一直使用的数字）之外，C++ 还允许将八进制数（8 进制）和十六进制数（16 进制）作为严格常量。如果我们需要表示八进制数，需要在它前面放置一个`0`（零字符）。此外，为了表示十六进制数的特定目标，我们需要在数字前面放置字符`0x`（零，x）。

字面量常量和变量一样，被认为具有特定的类型。当然，数字字面量是`int`类型。在任何情况下，我们通过在其后附加`u`字符将其转为无符号形式，或通过附加`l`转换为长型形式。在两种情况下，后缀都可以使用大写或小写字母来确定。

### 浮点字面量

这些字面量以指数和数字的形式表示数字。它们可以包含小数点、一个`e`字符（指数的符号），在`e`字符之后会出现一个数字。此外，数字可以同时包含小数点和一个`e`字符。

示例：

```
3.14159 / 3.14159
6.02e23 / 6.02 x 10²³
1.6e-19 / 1.6 x 10^-19
```

在前面的示例中，可以看到浮点数是如何书写的。第一个示例使用小数点，而后两个数字使用`e`字符来表示 10 的次方，其中`x`是指数的次数。`double`是默认类型，用于浮点表示。

### 字符和字符串字面量

C++ 中也存在非数值常量。虽然字符是单个`char`，但字符串代表一个字符串。请注意，当我们说单个字符时，我们用单引号 (`'`) 将其括起来。另一方面，为了表示字符串（大部分包含多个字符），我们用双引号 (`"`) 将其括起来。

### 布尔字面量

只有两个合法的布尔字面量：`false`和`true`。这些可以通过布尔字面量`false`和`true`在 C++ 中表示为`bool`类型的估计值。

### 定义常量 (`#define`)

你可以为你经常使用的常量命名，而不需要依赖其他东西。你可以使用`#define`预处理器来描述这些常量。

该语言的语法如下：

```cpp
#define <标识符> <值>
```

示例：

```cpp
#define EXP 10
```

### 声明常量 (`const`)

你可以使用`const`关键字像声明变量一样声明常量，定义后无法更改。

## 运算符

当我们知道变量和常量的存在后，就可以开始操作它们。为了处理这些变量和常量，C++ 语言提供了运算符。与其他编程语言中运算符基本上是单词不同，C++ 中的运算符大部分由符号组成，这使得 C++ 代码更短、更全局，尽管最初需要一些学习精力。

### 赋值 (`=`)

此运算符将值分配给变量。

语法：

`<变量 标识符> = <值>`

示例：

```cpp
x = 0;
```

此声明将数字值`0`分配给变量`x`。运算符`=`的左侧被称为 lvalue（左值），右侧被称为 rvalue（右值）。lvalue 必须是一个变量，而 rvalue 可以是常量、变量或这些者的混合。分配时最重要的原则是从右到左的操作，即操作从右向左执行，而永远相反。

语法：

```cpp
<lvalue> = <rvalue>;
```

示例：

```cpp
x = y;
```

此声明将变量`y`(rvalue) 中包含的值赋予变量`x`(lvalue)。C++ 对于其他编程语言的一个特性是运算符操作可以作为 rvalue（或 rvalue 的一部分）用于另一种运算符操作。

示例：

```cpp
x = 7 + (y = 0);
```

在这个示例语句中，`0`分配给变量`y`，然后对这个值加上`7`。结果被分配给`x`。

后续语句在 C++ 中也是合法的：

```cpp
x = y = z = 0;
```

它将`0`分配给所有的三个变量：`x`、`y`和`z`。

C++ 语言支持的五种算术运算包括：加（`+`）、减（`-`）、乘（`*`）、除（`/`）和模（`%`）。其中你可能不那么熟悉的是取模运算符。该运算符将除法的余数作为结果。例如，如果你执行了以下操作：

```cpp
a = 21 % 4;
```

`21`除以`4`的余数是`1`。这就是该操作的输出。

## 复合赋值

复合运算符包括减法 (`-=`)、加法 (`+=`)、除法 (`/=`)、乘法 (`*=`)、`>>=`、`<<=`和取模 (`%=`)。此外，还可以使用位逻辑运算符。当我们我们需要通过对变量当前的值进行操作来调整其估算值时，可以使用复合赋值。

### 语法：

`<变量标识符><运算符> = <值>`

### 示例：

```cpp
x += 1
```

在上面的示例中，`x`的值增加了`1`。

## 递增与递减 (`++`, `--`)

为了减少使用的语句数量，提供了递增和递减操作。这些语句分别等于`+=1`和`-=1`。

在早期的 C 编译器中，这三种不同的表述可能会根据使用了哪一种而产生截然不同的可执行代码。如今，这种代码精简是由编译器完成的，因此这三种解释应该产生完全相同的可执行代码。

该操作的一个正常特性是，它既可以作为前缀，也可以作为后缀。这意味着它可以组合在变量标识符之前（`++a`），也可以在之后（`a++`）。虽然在像`a++`或`++a`这样的基础语句中，两者的重要性完全相同。然而，在不同的声明中，如果递增或递减操作的结果作为值在外部解释中被评估，它们在意义上可能会有关重要的区别。

当递增操作作为前缀使用（`++a`）时，值在语句结果被评估之前会增加，随后扩展后的值会在外部输出中被考虑。如果它被用作后缀（`a++`），则值在评估之后会进行扩展，因此在递增操作在外部表示评估之前，存储的值会被先评估。

## 关系与相等运算符

这些运算符包括不等于 (`!=`)、相等 (`==`)、小于 (`<`)、小于等于 (`<=`)、大于 (`>`) 和大于等于 (`>=`)。

为了评估两个解释之间的关系，我们可以使用关系操作和对应关系（相等）操作。关系操作的结果是一个布尔值。该结果可以是两个值之一：`false`或`true`。

我们可能需要查看两个解释，例如，为了知道它们是否等价，或者一个是否比另一个更。以下是 C++ 中可以使用的运算符列表：

### 示例：

```cpp
(7 == 3) // 此表达式的结果为 false
(6 > 5) // 此表达式的结果为 true
(3 != 4) // 此表达式的结果为 true
(6 >= 6) // 此表达式的结果为 true
(5 < 5) // 此表达式的结果为 false
```

# 逻辑运算符

C++ 编程语言支持三种逻辑运算，即：非（`!`）、与（`&&`）和或（`||`）。

`not`运算符（`!`）允许 C++ 执行布尔逻辑 NOT 操作。它只有一个操作数，它的主要功能是反转该值。如果操作数的值为`true`，则它被转换为`false`。相反，如果值为`false`，则被转换为`true`。本质上，它通过评估其操作数提供一个成比例的反转布尔收益。

另外两个操作`&&`和`||`使用两个变量。`and`操作（`&&`）与布尔逻辑 AND 操作相关。当两个操作数都为`true`时，该操作的结果为`true`。相反，`||`操作与布尔逻辑 OR 操作比较，如果两个操作数中至少有一个为`true`，则结果为真值。

## 条件运算符 (`?`)

该运算符通过评估一个声明，如果该输出为真则返回一个值，如果语句被评估为假则返回另一个值。

### 语法：

`测试条件 ? 为真时的结果 : 为假时的结果`

如果`测试条件`为`true`，语句将返回`resultIfTrue`。然而，如果`测试条件`为`false`，它将返回`resultIfFalse`。

## 逗号运算符 (`,`)

逗号操作（`,`）用于两个或多个被包含在通常语句位置的独立输出中。当一组声明必须被评估为一个值时，只考虑最右边的解释。

### 位运算符

位运算包括位与（`&`）、位或（`|`）、`~`、`^`、`>>`和`<<`。这些运算符根据表示它们存储属性的位设计来调整变量。

## 显式类型转换运算符

该运算符允许你将某种提供类型的数据转换为另一种类型。在 C++ 中有几种方法可以实现这一点。最简单的一种继承自 C 语言的方法是在要转换的声明之前，用新类型括在括号`()`之间。

### 示例

```cpp
int i;
float f;
i = int ( f );
```



上述代码声明了两个变量`i`和`f`。虽然`i`是整数，但`f`是浮点数。直接将`f`赋值给`i`。

## 运算符优先级

C++ 运算符优先级决定了在包含多个运算符的表达式中，运算符的执行顺序。优先级越高的运算符越先执行。如果两个运算符的优先级相同，则根据从左到右的结合性来执行。

以下是 C++ 运算符优先级的表格：

| 运算符 | 级别 |
| :--- | :--- |
| `()` `[]` `++` `--` `.` `->` `sizeof` `static_cast` `dynamic_cast` `const_cast` `reinterpret_cast` | 1 |
| `~` `++` `--` `+` `-` `!` `(type)` `*` `&` `=` | 2 |
| `*` `/` `%` | 3 |
| `+` `-` | 4 |
| `<<` `>>` | 5 |
| `<` `<=` `>` `>=` | 6 |
| `==` `!=` | 7 |
| `&` `=` | 8 |
| `<<` `>>` | 9 |
| `&` | 10 |
| `^` | 11 |
| `\|` | 12 |
| `&&` | 13 |
| `\|\|\|` | 14 |
| `?:` | 15 |
| `+=` `-=` `*=` `/=` `%=` `>>=` `<<=` `&=` `^=` `\|=` | 16 |
| `,` | 17 |

```cpp
x = 5 + 3 * 2; // 乘法先于加法
```

我们可以利用`cin`和提取操作符（`>>`）来获取字符串，就像处理基本变量一样：

```cpp
cin >> stringIn;
```

然而，正如所说的，`cin`提取在遇到任何明显的空白字符时就会停止读取。因此，在这种情况下，我们每次提取只能获取单个单词。

## 控制结构

系统的运行通常不局限于指令的线性分组。在执行过程中，它可能会发生分叉、重写代码或做出选择。因此，C++ 提供了控制结构，用于指定我们的系统必须执行的内容、何时执行以及在什么情况下执行。

我们在这一区域将看到的大部分控制结构，作为语言结构的一个主要方面，需要一个简单的解释。一个声明语句可以是简单语句（以分号结尾的简单指令），也可以是复合语句（组合在方括号中的几条指令）。如果我们需要声明是一个简单语句，就不需要用括号（`{}`）将其括起来。尽管如此，如果我们需要声明是一个复合声明，它必须封装在大括号（`{}`）之间，形成一个代码块。

### if-else 结构

`if`结构定义了一个条件和一组指令。如果满足条件，则执行`if`块。

`if`结构的语法如下：

```cpp
if (<condition>)
{
    //Code
}
```

在这里，`condition`是被不断评估的语句。如果该条件为真，则执行代码。如果它为假，则代码被忽略（不执行），系统将继续执行该条件结构之后的后续指令。

`if`结构的扩展版本是`if-else`结构。该结构的语法如下：

```cpp
if (<condition>)
{
    //Code If True
}
else
{
    //Code If False
}
```

如果该条件为真，则执行`code-if-true`。如果它为假，则`code-if-true`被忽略（不执行），系统将继续执行`code-if-false`。

示例：

```cpp
if (a == 0)
{
    cout<<”Value of a: 0“;
}
else
{
    cout<<”Value of a is not 0“;
}
```

### 循环

循环的作用是为了特定次数重复执行某段代码，或者当`while`条件满足时重复执行。

`while`结构的语法：

```cpp
while (<condition>)
{
    //Code
}
```

它的作用是在当声明中设置的条件为真时重复执行语句。

`do-while`循环的语法：

```cpp
do
{
    //Code
} while (<condition>);
```

它的作用与`while`循环完全相同，不同在于`do-while`循环中的条件是在代码执行之后评估的，而不是在之前评估的，这使得无论条件是否永远满足，代码都至少执行一次。

`do-while`循环通常用于需要控制循环结束的条件在循环语句内部被解决的情况，例如上一个用例，用户进入代码块的内容被用于判断循环是否需要结束。

`for`循环的语法：

```cpp
for (<initialization>; <condition>; <build>)
{
    //Code
}
```

它的主要功能是在条件有效时执行代码，这与`while`循环相似。尽管如此，`for`循环提供了特定的区域来包含初始化语句和递增/递减声明。因此，这种循环专门用于执行带有计数器的单调任务，计数器在每个周期中被初始化和扩展。

它按照以下方式符合预期：

1. **执行初始化**：大多数情况下，这是计数器变量的初始值设置。只执行一次。
2. **检查条件**：如果条件为真，循环继续。然而，如果条件为假，循环在执行完构建条件后结束。
3. **执行语句**：当然，它可以是单行代码，也可以是括号括起来的代码行，如`{ }`。
4. **最后**，执行`build`字段中确定的任何内容，然后循环返回第 2 步。

### 跳转语句

C++ 支持多种形式的跳转语句。下面将讨论这些语句。

#### break 语句

使用`break`，我们可以离开循环，无论其结束条件是否满足。它可以用于结束一个无限循环，或者将其限制在在正常结束之前结束。例如，我们将在其正常结束之前停止计数。

#### continue 语句

`continue`语句导致代码跳过当前循环中剩余的所有部分，就像到达了代码块的末尾一样，使其跳转到下一个循环的开始。

#### goto 语句

`goto`允许直接跳转到代码中的另一个点。你必须谨慎地使用此特性。执行它会导致无条件的跳转，跳过任何类型的设置限制。目标点通过一个名称来区分，该名称随后作为`goto`行的参数。名称由一个合法的标识符后跟冒号（`:`）组成。

#### exit() 函数

`exit()`是`stdlib`库中可用一个函数。它可以根据特定的代码结束当前执行。该函数的语法如下：

```cpp
void exit (int exitcode);
```

`exitcode`由工作框架使用并由调用函数使用。按照习惯，`exitcode`为`0`表示系统正常完成，其他值表示发生了错误。

示例：

```cpp
exit (0);
```

### Switch 结构

`switch`结构是特定的。它的目标是检查多个可能的值，类似于我们在本节开头使用的多个`if`和`else`指令。该结构的语法为：

```cpp
switch (<被监控的整数>)
{
    case value1:
        //code
        break;
    case value2:
        //code
        break;
    default:
        //code
        break;
}
```

`switch`结构在 C++ 语言中是特定的，因为它不使用块。相反，它使用标签。这使我们能够在为特定条件执行的相关代码之后放置`break`代码。

示例：

```cpp
int a;
cin >> a;
switch (a)
{
    case 0:
        cout <<”Entered value is 0”;
        break;
    case 1:
        cout << “Entered value is 1”;
        break;
    default:
        cout <<“用户输入的值不是 0 或 1”;
        break;
}
```

此外，请注意，如果你跳过了`break`语句，系统将执行真情况之后的所有情况。例如，如果你在上述代码中跳过了`break`语句且用户输入`0`，系统将执行所有情况。因此，三个语句将被打印。

### 函数

你可以使用函数来组织代码，这让你获得结构化编程可以提供的所有可能性。函数是从项目某处调用时执行的语句集合。以下是它的结构：

```cpp
<data type> <function identifier> (<parameter1>, <parameter2>, ...)
{
    //code
}
```

在这里，

● `data type`是函数返回的信息的数据类型。

● `function identifier`是调用函数的标识符。

- **参数（与数量相同）：** 每个参数都由数据类型和标识符组成。参数的声明方式与普通变量相同。它们允许在函数被调用时从调用函数处传递值。这些参数通常用逗号分隔。

- **代码语句**构成了函数体。

## 变量的作用域

在函数内部声明的变量在该函数块内是有效的，而在函数之外是无法被使用的。请考虑以下示例以更好地理解作用域：

```cpp
void func1()
{
  int a;
  //代码
}

void func2()
{
  int b;
  //代码
}
```

在上面的示例代码中，变量`a`只在`func1()`中可用，而`b`只在`func2()`中可用。因此，变量的作用域受限于它们被声明的块。考虑到，所有变量在声明时都有明确的作用域。当函数被调用时，这种作用域在函数外部是可见的。

## 带返回值的函数

当你查看函数的声明语法时，你会看到函数返回的数据类型。然而，某些函数可能不返回任何，在这种情况下将使用`void`数据类型。

假设我们需要创建一个函数来在屏幕上显示消息。我们不需要提供返回值。在这种情况下，函数应该使用`void`数据类型。`void`饰符也可以用于函数的参数列表中，明确表示函数在被调用时不需要实际参数。

## 按值传递与引用传递

在调用带参数的函数时，传递给函数的是值的副本。然而，变量本身并没有被发送。函数内部对变量值的任何修改都不会反映在原始变量上。相反，如果向函数发送变量的引用，函数内部对变量的修改将反映在原始变量上。

## 参数中的默认值

在声明函数时，我们可以为每个参数定义一个默认值。如果在调用函数时留空相关的参数，则该属性将被使用。要实现这一点，基本上需要在函数声明中使用赋值运算符为变量赋值。如果在调用函数时没有传递参数，则将使用默认值。然而，如果定义了值，此默认属性将被忽略，并使用传递的值。

## 重载函数

在 C++ 中，如果两个函数的参数类型或数量不同，则两个独立的函数可以使用相同的名称。这意味着只要它们的参数数量不同或数据类型不同，就可以为多个函数赋予相同的名称。

下面是一个示例实现：

```cpp
#include <iostream>

using namespace std;

float processnum (float x, float y)
{
  return (x/y);
}

int processnum (int x, int y)
{
  return (x+y);
}

int main () {
  int a=2, b=2;
  float c=4.0,m=4.0;
  cout << processnum (a, b)<<endl;
  cout << processnum (c, d)<<endl;
  return 0;
}
```

在这种情况下，我们声明并定义了两个同名的函数`processnum`。其中一个接受两个`int`类型参数，另一个接受两个`float`类型参数。编译器通过分析调用函数时传递的数据来确定在每种情况下引入哪一个。如果用两个`int`作为参数调用，它将调用声明中具有两个`int`参数的函数。另一方面，如果用两个`float`调用，它将调用模型中具有两个`float`参数的具体实例。

在第一次调用`processnum()`时，传递的两个参数都是`int`类型。随后调用了第二个声明的函数，它相加两个值并返回结果。然而，第二次调用传递了两个`float`类型参数。因此，调用了第一个模型的函数。

内联函数

`inline`饰符用于指示编译器在调用处直接替换函数体代码，以减少开销。这不需要考虑提供返回值。

标准语法：

```cpp
inline <数据类型> <标识符>( <参数> )
{
  //代码
}
```

## 递归

递归是在不需要外部干预的情况下调用函数的属性。它对于某些功能如排序或计算阶乘非常有用。

### 数组

数组是相同类型元素的排列，存储在连续的内存区域中，可以通过以下格式单独引用：

`arrayRef[i]`

这里`arrayRef`是任何数组，`i`是任何整数值，只要小于数组元素的数量即可。这意味着，例如，我们可以在数组中存储五个`int`类型的值，而不需要声明五个独立的变量。与普通变量一样，数组在使用之前必须声明。数组在 C++ 中的标准形式为：

`<数据类型> <标识符> [<元素数量>];`

这里`数据类型`是数组将持有的元素类型，`标识符`是赋予数组的唯一名称，`元素数量`表示数组中元素的数量。

## 数组初始化

在声明普通数组时（例如在函数内部），如果我们没有进行标记，其组件不会自然地初始化为任何值。因此，在向它们存储值之前，其内容将是不确定的。全局和静态性质的组件则会被自然地初始化为它们的默认值。因此，所有全局或静态数组的元素都初始化为 0。

例如，如果你想访问在上一节中定义的数组`num`的第一个元素，必须使用以下语句：

```
a = num [0];
```

在 C++ 中，从语言角度来说，跨越数组记录的范围是允许的。这可能会导致问题，因为访问超出范围的组件不会导致编译错误，但可能导致运行时错误。这种允许行为的背后的原因将在稍后我们开始使用指针时看到。

### 多维数组

多维数组可以被描述为“数组的数组”。例如，一个二维数组可以被想象成一个由组件组成的二维表格，每个组件都具有相同的统一信息类型。

多维簇并不限于两个索引（即两个维度）。它们可以包含所需的任意数量的记录。然而，请注意！簇所需的内存测量值会随着每一个一个维度的增加而迅速递增。

### 数组作为参数

在某些时刻，我们可能需要将数组作为参数传递给函数。在 C++ 中，通过值传递将整个内存块作为参数传递给函数是不现实的。然而，我们允许传递它的地址。在实践中，这样做的效果几乎相同，而且是一种速度更快、效率更高的操作。

记住将数组作为参数的最终目标，我们在声明函数时需要做的主要工作是在其参数中指定数组的组件类型、一个标识符和一对空括号`[]`。

### 字符序列

正如你所知，C++ 标准库实现了一个高效的字符串类，这对于处理和控制一系列字符非常有帮助。另一方面，由于字符串确实是字符的排列，我们同样可以将它们视为`char`组件的平铺数组来对待。

#### 空终止字符序列的初始化

由于字符簇是普通数组，它们遵循所有相同的相同标准。例如，如果我们需要引入一个具有预定字符顺序的字符数组，我们可以像处理其他数组一样这样做。该功能的一个示例实现如下：

```
char name[] = { 'J', 'o', 'h', 'n', '\0' };
```

在这种情况下，你声明了一个拥有 5 个元素的`char`数组。虽然你可以像上面那样初始化`char`数组，但可以使用字符串字面量用更好的方式来实现相同的功能。

#### 使用空终止字符序列

在 C++ 编程语言中定义字符串的标准方法是一个以空字符（`\0`）终止的字符序列。这也是字符串字面量所使用的格式。

## 指针

我们目前已经感知到变量是如何被视为内存单元，并通过它们的标识符来访问的。因此，我们不需要考虑内存中信息的物理区域。每当我们需要引用变量时，我们基本上使用了它的标识符。

你机器的内存可以被想象成一系列内存单元，每个单元的大小都是机器处理的忽略尺寸（一个字节）。内存单元在本质上是顺序的。因此，此块中的每个元素都比前一个元素加一。

### 引用运算符 (&)

当我们声明一个变量时，所需的内存测量会被分配到内存中的特定区域（其内存地址）。很大程度上，我们并不刻意在想象的内存单元网格中选择变量的精确区域。

幸运的是，这是工作框架在运行时自动完成的任务。尽管如此，有时我们可能对变量在运行时始终存储的位置感兴趣，以便与其相对位置进行操作。

在内存中标记变量的地址就是我们所说的变量的引用。这种对变量的引用可以通过在变量标识符之前放置一个安符（`&`），即引用运算符来获取，它可以实际上被解释为“……的位置”。

### 解引用运算符 (*)

我们最近看到，一个存储另一个变量引用的变量被称为指针。利用指针，我们可以专门获取存储在其指示的变量中的值。为了这样做，我们基本上需要在指针的标识符之前放置一个引用点（`*`），它充当解引用运算符，可以实际上意味着“……所指向的值”。

### 引用运算符与解引用运算符的对比

* `&`是引用运算符，可以被读取为“……的位置”
* `*`是解引用运算符，可以被读取为“……所指向的值”

### 指针与数组

数组的概念实际上与指针的概念紧密相关。实际上，簇的标识符等于其第一个组件的位置，因为指针等同于它指向的第一个组件的位置。说实话，它们是同一个概念。

随后的操作将是合：

```
p = num;
```

如果`p`是指针且`num`是数组，且两者类型相同，那么在该语句之后，`p`和`num`将是可以比较的并且具有相同的属性。主要的区别在于，我们可以通过另一个值改变指针`p`的值，而`num`将始终指向它被特征的固定数据类型的不同元素中的第一个。

因此，与传统的指针`p`不同，`num`是一个数组。因此，数组可以被视为一个常量指针。在这种情况下，随后的赋值将没有意义：

```
num = p;
```

由于`num`是一个数组，它作为一个常量指针工作，我们不能将值分配给常量。

### 指针指针

C++ 允许使用指向指针的指针，这些指针反过来指向信息（甚至指向不同的指针）。为了实现这一特定目标，我们只需要在声明中为每一级引用包含一个点（`*`）。

### 空指针



空指针是任何指针类型的指针，它有一个特殊值表示它没有指向任何合法的引用或内存地址。这个属性是向任何指针类型赋予零值的结果。

不要将空指针误认为空类型指针。空指针是不指向任何内容的指针。相反，空指针指向一个包含`void`类型值的位置。一个指的是指针本身存储的值，而另一个指的是它所指向的信息类型。

## 函数指针

C++ 允许对函数指针进行操作。这的常见用途是将能力作为参数传递给另一个函数，因为这些能力不能被解引用后传递。要声明一个能力的指针，我们需要像声明函数一样声明它，只是函数名被封装在括号`()`之间，并在名称之前嵌入一个星号（`*`）。

# 动态内存分配

最近，在我们之前所有的示例中，我们已经知道所需的内存量，并根据此估计声明了变量，甚至是数组。结果是程序所需的所有内存都在代码执行之前就已经分配好了。

同时，假设你面临一种需要可变测量值的情况，且该测量值必须在运行时解决。例如，在需要某些客户数据来确定所需的内存空间的情况下。

这种需求的答案是动态内存，C++ 允许使用`new`和`delete`运算符。

## 运算符`new`和`delete[]`

为了请求元素内存这一特定目标，我们利用`new`运算符。一个数据类型指定符跟在`new`运算符之后。然而，如果需要多个一个组件的组合，可以在部分`[]`中提到这些组件的数量。它返回一个指向新分配的内存块起始位置的指针。

### 语法：

```
<pointer identifier> = new <data type>
<pointer identifier> = new <type> [<number_of_elements>]
```

第一条语句用于分配内存以包含指定数据类型的单个组件。第二条语句用于分配一个指定数据类型组件组成的数组，其中`number_of_elements`是一个表示这些组件度量数量的整数值。

## `delete`和`delete[]`运算符

由于元素内存的需求通常被限制在代码中的特定时间段，一旦它不再被需要，就应该被释放，以便内存可以再次供不同的元素内存请求使用。这就是为什么提供了`delete`运算符的原因。

### 语法：

```
delete <pointer identifier>;
delete [] <pointer identifier>;
```

第一种表示应用于删除为单个组件分配的内存，第二种用于删除为组件数组分配的内存。传递作为参数进行删除的值必须是指向用`new`分配内存的指针，或者空指针（由于空指针，`delete`不产生任何影响）。

# 面向对象编程简介：类

类是信息结构的一种扩展概念，而不仅仅是持有信息。它可以同时持有函数和数据。另一方面，对象是类的实例化。对于变量来说，类是类型，而对象是变量。

类大部分使用关键字`class`声明，并带有如下语法：

```
class <className> {
    accessSpecifier_1:
    memberData;
    memberFunction;
    access_specifier_2:
    memberData;
    memberFunction;
} <objectName>;
```

其中`className`是类的标识符，`objectName`是该类对象的非强制名称标识符。呈现的形式可以包含部分，这些部分可以是数据成员或函数语句，并且带有指定符。

示例：

```cpp
int a;
```

在这里，`a`是`int`类的一个对象。

## 访问修饰符

这与信息结构的语句基本上相同，不同之处我们现在可以额外包含函数和数据部分，以及这种名为访问修饰符的新事物。获取访问权限或访问修饰符包括以下三个关键字之一：`private`、`public`或`protected`。这些指定符更改了访问其作用范围内的成员的权限。

- **Private (私有)**：类的此类成员仅从同类的不同成员内部或从它们的伴类可用。

- **Protected (保护)**：此类成员可以从同类的成员及其伴类可用，还可以从其派生类的部分可用。

- **Public (公共)**：此类成员在对象可见的任何地方可用。

默认情况下，类的所有成员对其所有成员来说都是私有的。

示例：

```cpp
class myRectangle {
    double a, b;
    public:
    void setValues (double, double);
    double func (void);
} myRect;
```

在这个示例中，`a`和`b`是私有的，而函数`setValues()`和`func()`是公共的。

## 构造函数和析构函数

你通常需要在创建方法期间引入变量或分配动态内存，以清理内存并避免在程序执行期间返回意外值。

考虑上一个示例，如果你在没有初始化它们的情况下将`a`和`b`作为参数传递给函数，那么函数获取的值将是垃圾值。你的代码可能会给出错误的结果或突然崩溃。

考虑到避免这种情况的最终目标，类可以包含一个名为`constructor`的特殊函数，它在该类的另一个对象被创建时自然地被调用。这个构造函数的名称必须与类名相同，且不能有任何返回类型。

示例：

```cpp
#include <iostream>
using namespace std;

class myRectangle {
    double x, y;
  public:
    myRectangle (double, double);
    double areaRect () {return (x*y);}
};

myRectangle :: myRectangle (double a, double b) {
  x = a;
  y = b;
}

int main ()
{
  myRectangle rectx (1,2);
  cout << "rect area: " << rectx.areaRect() << endl;
  return 0;
}
```

`main()`中的第一条语句实例化了`myRectangle`类。随对象创建传递的参数调用了构造函数，并将矩形的尺寸初始化为 1 和 2。因此，当调用`areaRect()`时，函数返回了正确的面积值 2。

构造函数不能像普通函数那样显式地调用。它们只在该类的另一个对象创建时被执行。你同样可以注意到，构造函数（类内部）或最后的构造函数定义都没有包含返回值，甚至`void`没有。

析构函数满足相反的功能。因此，当项目需要被销毁时它会被调用，可能是因为它的寿命已经结束（例如，它在函数内部被定义为局部变量且函数已关闭），或者由于它是动态分配的并通过`delete`运算符释放。

析构函数的名称与类名相同。然而，在名字之前有一个波浪号 (`~`)，它同样不返回结果。

### 构造函数重载

与其他函数一样，构造函数可以重载为多个名称相同但参数类型或数量不同的函数定义。记住，为了实现重载，编译器将调用与调用值参数匹配的一个。

### 默认构造函数

如果你在类定义中没有声明任何构造函数，编译器接受该类有一个无参数的默认构造函数。如果你没有创建自己的，编译器会为你创建一个默认构造函数。

如果你没有声明自己的，编译器会声明三个特殊的函数。这些是拷贝构造函数、默认析构函数和拷贝赋值运算符。

拷贝构造函数和拷贝赋值运算符另一个对象的信息复制到当前对象的成员。

## 类指针

指向类的指针是完全合法的。我们本质只需要考虑一旦声明，类就变成了一个实质的数据类型，因此可以使用类名作为指针的数据类型。

示例：

```cpp
myRectangle * pointerRect;
```

`pointerRect`是指向`myRectangle`类对象的指针。

与信息结构一样，为了特指指针指向对象的特定成员，我们可以使用间接运算符 (`->`)。

# 运算符重载

C++ 整合了使用标准运算符对类进行操作的替代方案，而不仅仅是基本数据类型。C++ 拥有一项功能，允许你通过规划准备好利用标准管理符执行操作的类，来重载运算符。

## 运算符重载

为了给某个运算符赋予特定目标以便在类中使用它，我们声明运算符函数，这些是函数一致的函数，其名称与我们需要重载的运算符符号所模拟的函数关键字相同。其格式为：

```cpp
<数据类型> <运算符> <运算符符号> (<参数>)

{

//代码
}
```

这里有一个重载加法运算符（`+`）的示例。我们将创建一个类来存储 2D 向量，随后我们将包含两个这样的向量：`a` (2,4) 和 `b` (3,4)。两个 2D 向量的相加是一个基础操作，就像将两个 x 方向相加得到相应的 x 方向一样。在点‘a’和‘b’上执行此项操作的结果应该是 (2+3, 4+4)，即等于 (5, 8)。

```cpp
#include <iostream>

using namespace std;

class myVector {
  public:
    int a, b;
    myVector () {};
    myVector (int, int);
    myVector operator + (myVector);
};

myVector :: myVector (int x, int y) {
  a = x;
  b = y;
}

myVector myVector :: operator+ (myVector myParam) { 
  myVector tempo;
  tempo.a = a + myParam.a;
  tempo.b = b + myParam.b;
  return (tempo);
}

int main () {
  myVector x (2, 4);
  myVector y (3, 4);
  myVector z;
  z = x + y;
  cout << z.a << "," << z.b;
  return 0;
}
```

## 关键字`this`

`this`单词表示指向正在持续执行其成员函数的对象的指针。它是指向对象本身的指针。

它还经常用作`operator=`函数的一部分，该函数通过引用返回对象（避免使用临时对象）。继之前看到的向量示例，我们可以像下面这样构造一个`operator=`能力。

实际上，这种能力与编译器为该类显式创建的代码非常相似，前提是我们没有排除一个`operator=`成员函数来复制该类的对象。

## 静态成员

类可以包含静态部分，可以是数据或函数。类的静态数据通常被称为“类变量”，因为对于该类的所有对象，都有一个独特的新值。它们的内容与该类的不同对象之间是不同的。

## 友元函数

在基本层面上，类的私有成员不能从声明它们的同一个类的外部访问。然而，这一标准并不影响友元函数。

如果我们需要声明一个外部函数为某个类的友元，这种方式允许该能力访问该类的私有和受保护成员，我们通过在类内部声明该外部能力的模型，并在其前面放置`friend`关键字来实现。

### 示例：

```cpp
#include <iostream>

using namespace std;

class myRectangle {
  int x, y;
public:
  void setValues (int, int);
  int func () {return (x * y);} friend myRectangle copy (myRectangle);
};

void myRectangle :: setValues (int a, int b) {
  x = a;
  y = b;
}

myRectangle copy (myRectangle rectParam) {
  myRectangle rects;
  rects.x = rectParam.x*2;
  rects.y = rectParam.y*2;
  return (rects);
}

int main () {
myRectangle rectx, recty;
  rectx.setValues (2,3);
  recty = copy (rectx);
  cout << recty.func();
  return 0;
}
```

`copy`函数是`myRectangle`的友元函数。从该函数内部，我们拥有了访问类私有成员`x`和`y`的能力。注意，在`copy()`语句中或其后在`func()`中的中使用，我们都没有将`copy`视为`myRectangle`类的一部分。它不是！它本质上在不属于类的一部分的情况下进入了它的私有和受保护成员。

友元函数可以用于，例如指导两个分离类之间的操作。在大多数情况下，友元函数的使用是面向对象的编程技术，因此在任何可能的情况下，最好使用同一类的部分来执行它们之间的操作。

## 友元类

通常，当我们有机会声明友元函数能力时，我们也可以将一个类声明为另一个类的友元，允许访问后者的受保护和私有成员。

### 示例：

```cpp
#include <iostream>

using namespace std;

class mySquare;

class myRectangle {
  int x, y;
public:
  int myArea () {return (x * y);}
  void convert (mySquare a);
};

class mySquare {
private:
  int x;
public:
  void setSide (int a)
  {x=a;}
  friend class myRectangle;
};

void myRectangle::convert (mySquare a) {
  x = a.x;
}

int main () {
mySquare sqr;
myRectangle rect;
  sqr.setSide(4);
  rect.convert(sqr);
  cout << rect.myArea();
  return 0;
}
```

在这个示例中，我们将`myRectangle`声明为`mySquare`的友元，以便`myRectangle`可以访问`mySquare`的私有成员`x`。

虽然基类的析构函数和构造函数本身不会被继承，当创建或销毁派生类的另一个对象时，析构函数和默认构造函数会被不断调用。如果基类没有默认构造函数，或者你需要在创建另一个派生对象时调用重载构造函数，你可以在确定类的每个构造函数中对其进行详细说明：

```
<派生构造函数名> (<参数>) : <基构造函数名> (<参数>) {

//Code
}
```

## 多继承

C++ 中有一个允许类可以继承多个类的规定。这可以通过在类声明中使用逗号分隔不同的基类来实现。例如，如果我们有一个特定的用于在屏幕上打印的类（`myOutput`），并且我们需要我们的类`myRectangle`和`myTriangle`同样继承它的成员（忽略`myPolygon`的成员），我们可以相应地对其进行组合。

# 实现多态

在进入这一部分之前，建议你对指针和类继承有实质性的理解。如果随后的解释中有任何部分让你感到不寻常，你应该检查显示的段落：

## 指向基类的指针

派生类的一个关键特性是，指向派生类的指针可以与指向其基类的指针兼容。多态是利用这种简单但强大且灵活特性的技巧，这种特性将面向对象的方法论发挥到了极致。

## 虚拟成员

类中一个在派生类中可以被重新分类的部分被称为虚拟成员。为了将类的某个部分声明为虚拟的特定目标，我们必须在该语句之前放置`virtual`关键字。

`virtual`关键字的作用是，允许确定类中与基类中同名的部分通过指针被正确调用，更准确地说，当指针的类型是指向基类的指针但指向的是派生类对象时如此。

## 抽象基类

理论基类和普通多态类之间的根本区别在于，由于理论基类中至少有一个部分需要使用，我们无法为其创建实例（对象）。尽管如此，一个不能实例化对象的类并非完全没用。我们可以创建指向它的指针并利用它所有的多态能力。

虚拟成员和动态类为 C++ 赋予了多态特性，使得面向对象的编程在大型活动中成为一种非常有用的工具。显然，我们已经看到了这些特性的简单应用，但这些特性可以应用于对象的表示或逐步分配的对象中。

# 函数模板和类模板

函数模板是可以与非特定数据类型工作的唯一函数。这允许我们创建一个函数布局，其用处可以调整到 hơn 一种类型或类，而无需为每种类型重新哈希整个代码。

在 C++ 中，这可以通过模板参数来实现。模板参数是一种特殊的参数，可以用于将类型作为参数传递：就像普通参数可以将值传递给函数一样，格式参数允许将相同类型传递给函数。这些模板可以像使用其他任何普通数据类型一样使用这些参数。

所使用的语法如下：

```
template <typename identifier> function_declaration;

template <class identifier> function_declaration;
```

上面所写的两个语句具有相同的含义和效果。唯一的区别在于关键字`typename`或`class`的使用。

### 示例：

为了说明函数模板的概念，让我们创建一个模板，返回传递给它的两个参数中值较大的一个。

```cpp
template <class eType>

eType GetMaxVal (eType x, eType y) {

return (x>y?x:y);

}

int a,b;

GetMaxVal <int> (a,b);
```

在这个示例中，使用了一个模板参数`eType`，它代表尚未指定的数据类型。该参数可以像任何其他数据类型一样用作函数的数据类型。`GetMaxVal`函数模板返回传递给它的两个参数中较大的值。为了调用此函数模板，你需要进行以下函数调用。

```
<函数名> <数据类型> (<参数>);
```

例如，如果你想为`int`调用`GetMaxVal`，那么你可以进行如下调用：

```
GetMaxVal <int>(a, b)
```

在这里，`a`和`b`是任意两个整数。

### 示例代码：



```cpp
#include <iostream>

using namespace std;

template <class X>

X GetMaxVal (X a, X b)

{

X val;
result = (a>b)? a : b;

return (result);
}

int main () {
  int x = 1, y = 2, z;
  long i=21, j=10, k;
  z=GetMaxVal<int>(x,y);
  k=GetMaxVal<long>(i,j);
  cout << z << endl;
  cout << k << endl;
  return 0;
}
```

在这个示例中，`X` 被用作数据类型。然而，你可以使用你喜欢的名称。对 `GetMaxVal` 的两次函数调用针对不同的数据类型 `int` 和 `long`。实际上，它也被用作创建新对象的数据类型。函数的输出是调用函数时的数据类型。

在上面的示例中，如果你调用该函数，编译器将隐式地使用 `int` 调用模板函数。对于带有 `x` 和 `y` 参数的函数，如果你使用 `long` 参数调用函数，编译器将使用 `long` 调用模板函数。因此，以下函数调用就足够了：

```
GetMaxVal (x, y);
```

然而，请注意在函数调用中不能可以使用不同类型。

### 类模板

就像函数模板一样，你也可以编写类模板。此类的成员使用用户定义的类型。

```cpp
template <class myType>
class myNums {

myType vals [2];

 public:
 myNums (myType one, myType two)

 {vals[0]=one; vals[1]=two;}

 myType getMaxVal ();

};
```

类模板可以通过以下方式创建不同类型的对象对：

```cpp
myNums<int> myintnum (334, 45);

myNums<double> myintfloat (1.0, 4.25);
```

```cpp
using namespace std;

namespace sample1
{
    double myvar = 5;
}

namespace sample2
{
    double myvar = 3.1416;
}

int main () {
    cout << sample1::var;
    cout<<"\n";
    cout << sample2::var;
    cout<<"\n"; 
    return 0;
}
```

在这种情况下，存在两个同名的变量：`myvar`。一个定义在命名空间 `sample1` 内部，另一个定义在 `sample2` 中。由于命名空间的存在，并不会发生重定义错误。

## using 关键字

`using` 单词用于将某个命名空间中的名称引入，以便与其他命名空间中的同名名称区分。

示例：

```cpp
#include <iostream>

using namespace std;

namespace sample1
{
    double x = 0.1;
    double y = 1.5;
}

namespace sample2
{
    double x = 1.1123;
    double y = 5.645;
}

int main () {
    using sample1::x;
    using sample2::y;
    cout << x;
    cout<<"\n";
    cout << y;
    cout<<"\n"; 
    cout << sample1::y;
    cout<<"\n"; 
    cout << sample2::x;
    cout<<"\n"; 
    return 0;
}
```

识别在此段代码中，`x`（无任何名称限定符）指向 `sample1::x`，而 `y` 指向 `sample2::y`，正如我们使用的声明所定义的那样。在任何情况下，我们都可以通过完全限定名访问 `sample1::y` 和 `sample2::x`。该关键字也可以作为指令引入整个命名空间：

示例：

```cpp
#include <iostream>

using namespace std;

namespace sample1
{
    int x = 56;
    int y = 70;
}

namespace sample2
{
    double x = 1.1125;
    double y = 5.5567;
}

int main () {
    using namespace sample1;
    cout << x;
    cout<<"\n"; 
    cout << y;
    cout<<"\n"; 
    cout << sample2::x;
    cout<<"\n"; 
    cout << sample2::y;
    cout<<"\n"; 
    return 0;
}
```

这将先打印 `sample1` 的值，然后打印 `sample2` 的值。

命名空间仅在声明它们的块内有效。例如，如果我们假设想要先使用一个命名空间的对象，稍后使用另一个命名空间的对象，我们可以这样做：

示例：

```cpp
#include <iostream>

using namespace std;

namespace sample1
{
    double x = 0;
}

namespace sample2
{
    double x = 1.1216;
}

int main () {
{
    {
        using namespace sample1;
        cout << x
        cout<<"\n";
    }
    {
        using namespace sample2;
        cout << x
        cout<<"\n";
    }
    return 0;
}
```

这段代码将打印 `sample1` 的 `x` 值，然后打印 `sample2` 的 `x` 值。

## 命名空间别名

我们可以按照以下配置为现有的命名空间声明别名：

`namespace newName = presentName;`

## namespace std

C++ 标准库中的所有文档都将其每一个元素都声明在 `std` 命名空间内。这就是为什么所有程序在开头都有一条指定代码正在使用 `std` 命名空间的语句。

http://www.onlamp.com/pub/a/mac/2001/12/07/apache.html

在尝试让你的系统运行顺畅时，请严格检查文件存储的位置以及 `localhost` 的地址。

## Linux 用户

其次，如果你在 Linux 系统上工作，那么为 PHP 配置系统可能会很棘手，因为可供你帮助的在线资源非常少。你可以尝试通过下面的链接来寻求帮助。

[`www.php-mysql-tutorial.com/wikis/php-tutorial/installing-php-and-mysql.aspx`](http://www.php-mysql-tutorial.com/wikis/php-tutorial/installing-php-and-mysql.aspx)

## Windows 用户

如果你是 Windows 用户，进行 PHP 编程对你来说要简单得多，考虑到有大量的在线帮助触手可及。设置 `Wampserver` 的第一步是下载该软件。你可以在 Google 上搜索并从官方网站下载它。

相信，你现在已经下载了 `Wampserver` 并对该软件了如指掌。这将为你在孤立的 PC（Windows 客户端）上提供一个服务器。现在，你已经有足够的设备来测试你的脚本了。假设你已经准备好了 `Wampserver`，你可以按照说明进行安装。

一旦主面板出现，查看菜单项中的停止和启动服务器的标签页。其他链接将带你进入文档查看器和系统帮助，以及与系统相关的其他功能。点击 `localhost`，你将看到一个页面。`localhost` 仅仅是指运行在你独立机器上的服务器。引用你服务器的另一种方法是使用 IP 地址 `127.0.0.1`。

到此时，你的服务器应该已经正常启动并运行了。如果你遇到任何问题，可以在在线论坛上寻找解决方案，或寻求专家帮助。

## PHP 中的变量

变量简单来说就是一个存储区域。你将物品放入你的存储区域（变量）中，以便你可以在项目中使用并控制它们。你通常需要存储的东西是数字和内容。

如果你能接受变量的概念，那么就可以继续下去了。如果不能，请考虑以下解释。假设你需要为你的着装创建一个记录。你雇佣了两个个人来帮助你，一个男人和一个女人。这两个个人将成为你的存储区域。他们将为你持有物品，而你只需数数你拥有什么。那么，这个男人和女人就是变量。

你检查你有多少件外套，然后将这些交给那个男人。你数数你有多少双鞋，并将这些交给那个女人。不幸的是，我们的记忆力不好。问题是，你的哪一个亲属（变量）持有层层衣服，哪一个持有鞋子？为了帮助你回忆，你可以给你的亲属起名字！你可以像这样称呼他们：

`miss_shoes`

`mr_coats`

尽管如此，给你的亲属（变量）起什么名字完全取决于你。如果愿意的话，它们也可以被这样称呼：

`boy_coats`

`girl_shoes`

但由于你的记忆力不好，最好为它们提供名字，以帮助你想起它们正在为你持有什么。你的亲属有些名字是不被允许称呼的。你不能以下划线（`_`）或数字开头。无论如何，大多数字符是可以的。

好了，你的亲属（变量）现在有了名字。尽管如此，仅仅给他们起个名字是不够的。他们将为你做一些工作，所以你必须让他们知道他们将要做什么。男人将拿着外套。无论如何，我们可以详细说明他将持有多少件覆盖。如果你有十层衣服要提供给他，那么你就使用下面显示的语法来“告诉”他：

```
mr_coats = 10
```

通过这种方式，变量名开头，后面跟着一个等号。在等号之后，你告诉你的变量它将做什么。在我们的情况下，是持有数字 `10`。顺便说，等号并不完全是等号。它被称为任务管理员。无论如何，在这个阶段不要为此压力。只需记住你需要等号来在变量中存储物品即可。

尽管如此，你正在学习 PHP，所以还有一些东西漏掉了。实际上是两件事。首先，你的亲属（变量）在开头需要一个美元符号（个人也是如此）。因此，实际语句应该类似于下面给出的语句：

```
$mr_coats = 10
```

如果你漏掉了美元符号，你的亲属将拒绝工作！但另一个缺失的东西是真正独特且细致的——分号。PHP 中的代码行末尾需要一个分号，如下面的语句所示：

```
$mr_coats = 10;
```

如果你在尝试运行代码时遇到任何解析错误，首先要检查的是是否在末尾漏掉了分号。这很简单，但可能会令人失望。下一个要检查的是你是否错过了寻找美元符号的重要机会。所以那个男人拿着十件外套。我们也可以对另一个个人（变量）做同样的事情。

```
$miss_shoes = 20;
```

通过这种方式，`$miss_shoes` 持有一个 `20` 的估计值。这种方式，`$miss_shoes` 持有一个 `20` 的估计值。正如我们在 PHP 中需要加内容那样，注意新变量前面的美元符号：

```
$total_items
```_items

```

这种方式，请注意 `$mr_coats + miss_shoes`。我们可以包含外套和鞋子。加法方式如下：

```

$total_items = 10 + 20;

```

再次，PHP 会看到加号并把它们相加。显然，你可以在加法公式中包含两个两个项。

```

$total_items = 10 + 20 + 9 + 50 + 1100;

```

尽管如此，想法是相同的。PHP 会看到加号并随后将它们相加。答案将被放入我们的变量中，即等号左侧。

## 将文本放入变量

在前面的部分中，你了解了如何将数字放入变量。尽管如此，你同样可以将内容放入变量中。假设你需要了解关于你拥有的外套或层衣的信息。你可以将我们的外套分类为冬季层、外套或夏季层。你可以选择对它们进行索引。你可以将直接内容放入你的变量中。放入数字的对比方法：

```

$coat_1 = " Summer Coats";

```

再次，我们的变量名以美元符号（`$`）开头。我们随后为它提供了名字 `coat_1`。等号位于变量名之后。在符号之后，再次是内容——冬季外套。无论如何，注意内容周围的双引号。如果你不将内容包含在引号内，你将得到不可预测的结果。在任何情况下可以使用单引号而不是双引号，如下语句所示：

```

$coat_1 = ' Summer Coats';

```

尽管如此，你不能这样做：

```

$coat_1 = Summer Coats";

```

在上面的行中，我们以单引号开始并以双引号结束。这将让你得到一个错误。

我们可以以相同的方式存储其他内容：

```

$coat_2 = "Coats";

$coat_3 = "Winter Coats";

```

简单来说，总结一下，变量是区域，它们拥有定义良好的容量。你利用这些容量区域来控制像内容和数字这样的东西。你将大量使用变量，在接下来的几页中，你将体会到它们在实践中是如何运作的。

# 在 PHP 中使用变量

首先，我们将检查如何访问变量中的内容。我们将在一个网页上查看我们的结果。所以，请先检查你是否可以让此脚本运行起来，考虑到我们在本章的后续部分将对其进行扩展。使用像 PHP 编程器或记事本这样的内容管理器可能会有所帮助。根据你的倾向，你可以复制并粘贴它。无论你采取何种方式，自己写一遍都会收获更多——除非你犯了错，否则通常是记在大脑里的！

```html

<html

<head>

<title>Practicing Variables</title>

</head>

<body>

<?php print("It is working!"); ?>

</body>

</html>

```

当你完成所有内容的编写后，最后将页面另存为 `variable.php`。此时，只需运行脚本即可。请记住：在保存工作时，请将其放在 WWW 目录中。要运行该页面，启动你的程序并在地址栏中输入这个：

http://localhost/variable.php

如果你在 www 文件夹内创建了一个文件夹，那么你在程序中排序的地址将类似于：

http://localhost/Foldername/variable.php

除此之外，你应该能看到你的程序运行结果显示了“It is working!”的内容。如果确实如此，恭喜你！你拥有了一个正在运行的服务器！如果你正在使用 Wampserver，你应该会在屏幕右下角看到一个图标。点击该图标并从任务栏菜单中选择“Start All Services”（启动所有服务）。

在整个程序中，重要的一行是：

```php

<?php print("It is working!"); ?>

```

脚本的其余部分都是 HTML 代码。我们来详细分析一下这里的 PHP 吧。我们将 PHP 放在了 HTML 页面的 BODY 部分。脚本同样也可以并且经常放在 HTML 页面的 HEAD 区域。你同样可以在没有 HTML 的情况下编写脚本。无论，在程序识别你的脚本之前，它需要一些帮助。你需要告诉它这是什么种脚本。程序通过搜索此标记（称为语法）来识别 PHP：

```php

<?php ?>

```

所以，你需要一个左边界部分（ < ）然后一个问号（ ? ）。在问号标记之后，编写 PHP（大写或小写均可）。在脚本完成后，放入另一个问号。最后，你需要一个右边界部分（ >）。你可以在起始和结束结构之间放置你想要的内容。

为了在页面上显示内容，我们使用了 `print( )`。你需要程序打印的内容放在圆括号之间。如果你打印的是字符串内容，你需要引号（单引号或双引号）。要打印变量内部的内容，只需在变量名前前加上美元符号 $。最后，代码行照常结束——以分号（`;`）结尾。

现在让我们调整这个基本页面，以便设置几个变量。我们先尝试一些内容。保持 HTML 不变，但将你的 PHP 从代码 1 改为代码 2。

代码 1：
```php

<?php print("It is working!"); ?>

```

代码 2：
```php

<?php

print("it Worked!");

?>

```

好了，这是一个没意义的改变！无论如何，将代码分布在多行上使其更容易查看和理解你在做什么。现在的代码只有一行。在接下来的代码中，我们在示例脚本中添加了一些更多的代码。

```php

<?php

$testing_string = "It is working!";

print("It is working!");

```

我们设置了一个名为 `$testing_string` 的变量。在等号之后，包含了“It is working!”的内容。该行随后以分号（`;`）结束。然而，在运行脚本之前，你必须在代码中添加以下 print 行：

```php

print($testing_string);

```

此时加入几行注释

```php

<?php

// -PHP 变量练习-

$testing_string = "It is working!";

print($testing_string);

?>

```

PHP 中的注释是为了你的方便。它们能帮助你记住代码应该做什么。可以通过编写两个斜杠来包含注释。这会告诉 PHP 忽略该行的其余任何内容。在两个斜杠之后，你可以编写任何想要的内容。包含注释的另一种方法是以下格式：

```php

/* <注释

*/



当你需要跨多行时，使用这种注释方式。无论你选择哪种技术，请确保在代码中添加了注释：它们确实很有帮助。特别是当你需要将代码发送给其他人时！

你是如何进展的？你应该看到完全相同的内容被打印到了页面上。此外，你可能在想——主要的挑战是什么？考虑到所有方面，你所做的仅仅是将一些内容传递给变量，然后让 PHP 打印变量的数据。这是一个巨大的进步：你的编程之旅现在开始了！

你可以将坐标内容组合起来，以便我们可以设置几个变量。考虑到所有方面，你所做的仅仅是将一些内容传递给变量，然后让 PHP 打印变量的数据。这是一个巨大的进步。你可以通过变量赋值来输出。假设你需要打印“My variable contains the”，你可以通过以下代码实现：

```php
<?php

$number_1 = 5;

$value_text = 'My variable contains ';

print ($value_text . $number_1);

?>
```

现在我们有了两个变量。新变量包含了字符串内容。在 PHP 中，通过使用点来输出。查看上面的脚本，然后再次尝试：

```php
<?php

$number_1 = 5;

$value_text = 'My variable contains '

?>
```

在代码中，你也可以这样做：

```php
<?php

$number_1 = 5;

print('My variable contains ' . $number_1);

?>
```

# 加法

好了，让我们对变量进行一些加法。在 PHP 中，加法使用加运算符 `+`。如果你有上一节的代码，请尝试将句号改为加号。运行代码，看看发生了什么。

要相加变量的值，你只需用加运算符分隔变量名。尝试此代码：

```php
<?php

$number_1 = 4;

$number_2 = 3;

$sum_value = $number_1 + $number_2;

$value_text = 'Result = ';

print ($value_text . $sum_value);

?>
```

在上面的脚本中，我们包含了第二个数字，并为其分配了一个值。

`$number_2 = 3;`

然后声明了第三个变量，我们将其命名为`sum_value`。在等号右侧，我们包含了第一个变量的值和第二个变量的值：

`$sum_value = $number_1 + $number_2;`

PHP 理解`$number_1`和`$number_2`变量中的内容，因为我们刚刚在上面的两行中已经告诉了它！它看到了加运算符，然后将两个变量值相加。它将加法的结果放在等号左侧的变量中，即我们的`$sum_value`。

等号右侧的加法操作首先计算（`$number_1 + $number_2`）。将操作的结果存入等号左侧的变量中（`$sum_value`）。显然，你可以包含两个以上的数字。

## 减法

我们并不打算通过让你面对大量的实质数学知识来让你感到负担！无论如何，你确实需要知道如何使用基础运算符。首要重要的是减法。减法与加法几乎相同，你在上一节中已经做过了。你使用的不是加号（`+`），而是减号（`-`）。将你的`$sum_value`行改为如下内容，并运行你的代码：

```php
$sum_value = $number_1 - $number_2;
```

`$sum_value`这一行与第一行几乎相同。我们现在使用的是减号而不是加法运算符。当你运行脚本时，你显然应该得到答案 1。再次，PHP 识别出名为`$number_1`和`$number_2`的变量中的内容。它之所以知道，是因为你在最初的两行中将数据值分配给了这些变量。

当 PHP 运行到减号时，它会为你执行减法，并将结果放入等号左侧的变量中。我们然后使用打印函数来显示变量中的内容。与加法一样，你可以一次减去多个数字。尝试一下这个：

```php
<?php

$number_1 = 3;

$number_2 = 4;

$number_3 = 30;

$sum_value = $number_3 - $number_2 - $number_1;

print ($sum_value);

?>
```

你应该得到的答案是 23。你同样可以把加法操作与减法混合。这里有一个示例：

```php
<?php

$number_1 = 3;

$number_2 = 4;

$number_3 = 30;

$sum_value = $number_3 - $number_2 + $number_1;

print ($sum_value);

?>
```

运行上面的代码。你得到了什么答案？它真的是你预期的答案吗？你认为它为什么打印了那个数字？如果你认为它可能打印出一个与你得到的不同的不同的响应，那么原因可能是我们安排整个表达式的方式。我们的意思是 30 - 4，然后加 3 吗？或者，我们的意思是加上 3 和 4，然后从 30 中减去它们？主要的整体将是 29，而第二个总和将是 23。

为了说明你的意思，你可以利用括号作为整体表达式的一部分。这里是表达式的两种不同形式。在你的代码中尝试这两种。无论如何，请注意括号的位置：

### 形式一
```php
$sum_value = ($number_3 - $number_2) + $number_1;
```

### 形式二
```php
$sum_value = $number_3 - ($number_2 + $number_1);
```

在你的表达式中使用括号通常是一个好主意，只需明确你需要让 PHP 计算的内容。这样你就不会得到异常的答案了！

使用括号的另一个由于许多人所谓的“运算符优先级”的直接结果。在 PHP 中，某些运算符（特别是数学函数）会在其他运算符之前计算。这意味着你可能会得到完全意外的答案！因此，在预期任何正确结果之前，务必验证表达式中所用运算符的执行顺序。

## 乘法

在 PHP 以及几乎所有其他编程语言中，都使用`*`运算符进行乘法。如果你看到`3 * 4`，意味着将 3 乘以 4。这里有一些代码供你尝试：

```php
<?php

$number_1 = 10;

$number_2 = 20;

$sum_value = $number_2 * $number_1;

print ($sum_value);

?>
```

在上面的代码中，我们只是将两个变量中的任何内容相乘。然后我们将结果分配给等号左侧的变量。你可能可以在运行代码之前就考虑到答案是什么！与减法和加法一样，你可以乘以两个以上的数字。

## 除法

在 PHP 中，使用`/`运算符将一个数字除以另一个数字。如果你看到`25/5`，意味着将 25 除以 5。使用下面代码自己尝试一下：

```php
<?php

$number_1 = 5;

$number_2 = 25;

$sum_value = $number_2/$number_1;

print ($sum_value);

?>
```

再次，你必须留意运算符优先级。尝试这段代码：

```php
<?php

$number_1 = 5;

$number_2 = 25;

$number_3 = 10;

$sum_value = $number_3 - $number_2/$number_1;

print ($sum_value);

?>
```

PHP 不会从左到右计算整个表达式！除法在减法之前执行。这将首先完成：

`$number_2/ $number_1`

而不是这样的：
`$number_3 - $number_2`

## 使用浮点数

浮点数是指带有小数点的数字。在 PHP 中，你可以像处理整数一样处理它们。如果你看到 3.5，它就是一个浮点数。这里有一个例子供你尝试：

```php
<?php

$number_1 = 3.5;

$number_2 = 2;

$sum_value = $number_1 * $number_2;

print ($sum_value);
```

乘法、减法、加法和除法都可以用于浮点数。正如处理整数一样，你也可以对浮点数执行这些操作。在 PHP 中，你可以将浮点数赋值给变量。

## 条件逻辑

条件逻辑实际上是关于询问一个条件是否为真或假，并根据条件的结果执行相应的代码。许多人称之为条件逻辑，它非常有用。在任何情况下，你确实需要知道如何使用基础运算符。你可以在日常生活中使用条件逻辑：

“如果我调大收音机的音量，邻居会生气吗？”

“如果我把所有的钱买一双新鞋，会让我开心吗？”

“如果我学习这门课程，它会提高我的水平吗？”

条件逻辑使用`if`语句。通常，你使用条件逻辑来测试变量中的内容。作为一个示例，再次考虑用户名。你可能有一个变量：

```php
$username = "regular_visitor";
```

你会使用一些条件逻辑来测试用户名是否正确。你需要询问：

“如果`$username`是真的，那么允许`$username`进入网站。”

在 PHP 中，你可以这样使用它：

```php
if ($username == "allowed") {

// 在这里编写允许进入网站的代码

}
```

在没有检查的情况下，`if`语句遵循以下语法：

```
if (<要检查的条件>) {

// 代码

}
```

这样你就不会得到异常的答案了！

```php
// 让客户端访问此站点的代码放在这里
```

沿着这些思路，也可以测试以下代码：

```php
if($username == "allowed") {

// 让客户端访问此站点的代码放在这里;

}
```

第一个的波浪部分路径反了（应该是先向左后向右），而第二个有两个左侧的波浪部分。

在两个圆括号部分之间的中间，你写下需要测试的条件。在上面的插图中，我们正尝试检查名为`$username`的变量是否具有值为 "allowed" 的值：

`($username = "allowed")`

再次强调，如果你没有正确写好圆括号部分，你将会得到一个逻辑错误！因此，`if`声明的语言结构如下：

```php
if(testing_condition) {

// 如果条件为真，则执行的代码

}
```

如果你需要测试由同一个变量标识的两个条件，可以使用`if-else`结构。`if else`结构的语言结构如下：

```php
if (testing_condition) {

// 如果条件为真，执行代码

}

else {

// 如果条件为假，执行代码

}
```

如果你仔细观察它，你会发现你最初有一个普通的`if`语句，后面跟着一个`"else"`部分。这里是`"else"`部分：

```php
else {

// 如果条件为假，则执行的代码

}
```

再次利用了左侧和右侧的波浪部分。你同样可以在你之前段落中研究过的`if`语句中包含`"else if"`部分。用于此目的的语法所示：

```php
else if (testing_condition) {

// 相应的代码

}
```

### 关系运算符

你在上一个段落中看到了如何测试变量内部的内容。你使用了`if`、`else`……`if`，以及`else`。你还使用了双重等号（`==`）来测试变量的值是否与给定条件相同。双重等号被称为比较运算符。有许多这样的“操作数”可以用于测试。这里是运算符的列表及其用途的概述。研究一下，之后我们将看到一些如何使用它们的示例。

| 运算符 | 目的 | 语法 |
| :--- | :--- | :--- |
| `==` | 等于 | `a == b` |
| `!=` | 不等于 | `a != b` |
| `>` | 大于 | `a > b` |
| `<` | 小于 | `a < b` |
| `>=` | 大于或等于 | `a >= b` |
| `<=` | 小于或等于 | `a <= b` |

这里是关于上述操作数的更多数据。

#### `==` (具有相同的值)
双重等号可以表示“具有估计值”或“具有相同的值”。在下面的示例中，名为`$variable_1`的变量与名为`$variable_2`的变量进行持续对比。

```php
if ($variable_1 == $variable_2) {

}
```

#### `!=` (值不相同)
你同样测试一个条件是否与另一个不同。在这种情况下，你需要感叹号/等号组合（`!=`）。例如，如果你正在尝试一个真实的用户名，你可以说：

```php
if ($which_user_entered != $user_name) {

print("你不是此站经过认证的客户端！");

}
```

上面的代码的意思是：“如果客户端输入的内容与变量获取的属性`$user_name`不相同，则打印某些内容。”

#### `<` (小于)
测试一个条件是否小于另一个。你需要测试一个条件是否为真。

#### `>` (大于)
测试一个条件是否大于另一个。你需要测试一个条件是否为真。

#### `<=` (小于或等于)
测试一个条件是否小于或等于另一个。你需要测试一个条件是否为真。

#### `>=` (大于或等于)
测试一个条件是否大于或等于另一个。在这种情况下，我们需要`switch`结构。

### Switch

你在上一个段落中看到如何测试变量内部的内容。你使用了`if`、`else`……`if`，以及`else`。你还可以使用`switch`结构来测试一个变量。`switch`结构类似于`if`语句。`else`。在情况下，我们需要一个`switch`结构：

```php
<?php

$new_picture = "image1";

switch ($new_picture) {

case 'dog':

print("图片 1");

break;

case 'cat':

print("图片 2");

break;

}

?>
```

在上面的代码中，`$new_picture`变量被持续对比。如果`$new_picture`的值是 'dog'，则打印 "图片 1"；如果是 'cat'，则打印 "图片 2"。

`break;`用于跳出`switch`语句。如果没有`break`，代码将继续向下执行。

```php
<?php

$new_picture = "dog";

switch ($new_picture) {

case 'dog':

print("图片 1");

case 'cat':

print("图片 2");

}

?>
```

在这种情况下，它会同时打印 "图片 1" 和 "图片 2"。

`default`默认值。当所有`case`都不匹配时，执行`default`代码。

```php
<?php

$page = "unknown";

switch ($page) {

case "home":

print("首页");

break;

case "about":

print("关于我们");

break;

default:

print("未找到的页面");

}

?>
```

`default`类似于`if`中的`else`。在情况下，我们需要一个`switch`结构。

# 逻辑运算符

你之前看到的 PHP 关联，还有许多人称为逻辑运算符的东西。你通常在同时测试多个条件时使用它们。例如，你可以验证用户名和密码是否都正确。

| 运算符 | 目的 | 语法 |
| :--- | :--- | :--- |
| `&&` | 两个都为真 | `a && b` |
| `||` | 一个或多个都为真 | `a \| b` |
| `AND` | 两个都为真 | `a AND b` |
| `XOR` | 仅一个为真 | `a XOR b` |
| `OR` | 一个或多个都为真 | `a OR b` |
| `!` | 取反 | `!a` |

新的操作数相当少，以至于遇到它们时可能会困惑。有些甚至功能相同！但它们非常有用，所以让我们更深入地研究。

#### `&&` 运算符

`&&`运算符意味着与。当你需要两个条件有效时使用它，例如我们的用户名和密码测试。老实说，你不希望在用户仅获得正确用户名或正确密码的情况下就给予访问权限。这里有一个示例代码来说明这个概念：

```php
$user_name = 'registered_user';

$pass_word ='secret_password';

if ($user_name =='registered_user' && $pass_word =='secret_password') {

print("欢迎用户！");

}

else {

print("用户名或密码错误！");

}
```

`if`语句的使用方式与之前相同。然而，请注意现在持续测试的是两个条件：

`$user_name == 'registered_user' && $pass_word =='secret_password’`

这句话的意思是：“如果用户名正确且密密钥也正确，那么给予用户访问权限。”这两个条件都必须放在你的`if`语句的圆括号之间。

# `||` 运算符

两条直线表示“或（OR）”。当你只需要条件中的其中一个为真时，请使用此运算符。例如，假设你需要在个人花费超过 500 英镑**或者**他们有一个特殊密钥的情况下允许他们使用 markdown。否则，他们将无法获得任何折扣。你可以这样编写代码：

```php
$total_expenditure =500;

$special_coupon_key =’98765’;

if ($total_spent == 500 | $special_coupon_key == ‘98765') {

    print("Discount applies!");

}

else {

    print("No discount!");

}
```



这一次我们尝试两个条件，并且只需要其中**任意一个**返回真值。如果两个条件都为真，则执行该代码。如果两者都为假，那么 PHP 将继续向下执行。

## AND 和 OR

这些与之前章节中讨论过的`&&`和`||`运算符相同。然而，它们存在细微的区别。作为初学者，你可以直接使用以下格式来实现 AND（与）：

```
$user_name == 'registered_user' && $pass_word =='secret_password'
```

以下语句也等同于：

```
$user_name == 'registered_user' AND $pass_word =='secret_password'
```

使用哪一个取决于你的喜好。`AND`比`&&`易读得多。同样，`OR`也比`||`易读得多。顺便提一下，区别在于运算符优先级。我们在之前检查变量时提到过这一点。它将在接后的章节中详细讨论。

## XOR

你可能不需要频繁使用这个运算符。无论如何，当你需要测试两个估计值中是否有一个是真的但**不是**两者都是时，可以使用它。如果两个条件相同，那么 PHP 将认为该声明为假。如果它们不同，则答案为真。假设你需要两个候选者之间选出一个获胜者。只有其中一个可以获胜。这是一个 XOR 情况！

```
$contestant_1 = true;
$contestant_2 = true;

if($contestant_1 XOR $contestant_2) {
    print("There can be only one winner!");
}
else {
    print("Both cannot be winners!");
}
```

在运行脚本之前，检查你是否能推出哪一个会被打印。

## ! 运算符

这被称为非（NOT）运算符。你利用它来测试某物是否**不是**其他东西。你同样可以使用它来反转或否定真或假的值。例如，如果你需要将变量重置为真（如果它被设置为假，反之亦然），可以使用此运算符来获得最佳结果。这里有一些可以尝试的代码：

```
$not_value = false;

if($not_value == false) {
    print(!$not_value);
}
```

上面的代码将打印数字 1。当我们在下面处理布尔值时，你就明白为什么了。我们在这里说：“如果`$test_value`为假，那么代码必须打印它**不是**的什么”。它不是的东西是真，所以它现在将获得这个属性。有点困惑吗？这是一个很微妙的概念。但它被证明是有用的！

## 布尔值

布尔值可以持有以下状态之一：true（真）和 false（假）。True 通常被赋值为 1，False 被赋值为 0。你设置它们与其他变量相似：

```
$t_value = 1;
$f_value = 0;
```

你可以用单词 "true" 和 "false" 替换 1 和 0（不带引号）。但请注意，如果你这样做了，尝试这个脚本，看看发生了什么：

```
<?php
$f_value = false;
$t_value = true;

print (" f_value = " . $f_value);
print ("t_value = " . $t_value);
?>
```

你应该发现`t_value`将打印 "1"，但`f_value`什么都不会打印。现在，在上面的脚本中将 true 替换为 1，false 替换为 0，看看打印出什么。布尔值在编程中非常常见，你经常看到这种代码：

```
$t_value = true;

if ($true_value) {
    print("True Value");
}
```

这是表示“如果`$t_value`持有布尔值 1，则执行打印语句”的简写方法。这等于：

```
if ($t_value == 1) {
    print("True");
}
```

NOT 运算符也用于这类 if 语句：

```
$t_value = true;

if (!$t_value) {
    print("True");
}
else {
    print("False");
}
```

在你的编程生涯中可能会经常遇到布尔值。最好掌握它们！

## 运算符优先级

这里是你遇到过的运算符列表以及它们的优先级。正如我们在数值计算中所看到的，不要过度担心这些，除非你确定你的数学是正确的。在这种情况下，你可能需要参考以下（从高优先级到低优先级）：

* `/`, `%`
* `-`, `+`
* `>`, `>=`, `<=`
* `!==`, `===`
* `&&`
* `||`
* `AND`
* `OR`
* `XOR`

你在列表中还没有遇到的运算符是`=`和`!=`。它们用于测试一个变量是否与另一个变量相等。例子如下：

```
$number_val = 2;
$text_val = 'two';

if ($number_val === $text_val) {
    print("Both are same!");
}
else {
    print("They are different!");
}
```

## PHP 和 HTML 表单

如果你了解 HTML，就会知道表单（FORM）标签可以与用户交互。表单的形式可以是单选按钮、文本框、下拉菜单、复选框。一个带有文本框和提交按钮的基础 HTML 结构可以通过以下方式创建：

```
<html>
<head>
<title>a BASIC Form in HTML</title>
</head>
<body>
<form NAME ="form_1" METHOD=" " ACTION="">
<input TYPE="text" VALUE ="user_credentials">
<input TYPE="Submit" Name="Submit_1" VALUE="Login_value">
</form>
</body>
</html>
```

我们不会解释所有的 HTML 组件，因为这是一本关于 PHP 的书。与上面有一些共同点是合理的。然而，我们将检查上面结构中的 METHOD、ACTION 和 SUBMIT 属性，因为它们是重要的。

### METHOD 属性

如果你看一眼上一节结构的第一行，你会发现使用了名为`METHOD`的属性：

```
<form NAME ="form_1" METHOD=" " ACTION="">
```

Method 属性用于告诉程序如何发送数据。你可以使用的两种最著名的技术是 GET 和 POST。在任何情况下我们的 METHOD 是明确的。所以将其转换为：

```
<form NAME ="form_1" METHOD="get" ACTION="">
```

为了查看使用 GET 有什么影响，再次保存你的工作，然后点击表单上的 Submit。这里需要注意的是位置栏。地址会被附加了以下字符串：

`?Submit_1=login_value`

这是利用`GET`系统的结果。结构中的信息会出现在地址栏中。你将看到一个由信息模拟的查询标记。`Submit_1`是表单上按钮的`NAME`（名称），而`Login_value`是按钮的`VALUE`（值）。这就是`GET`技术返回的内容。当你需要的返回信息不是需要保护的关键性数据时，你就使用`GET`系统。你同样可以使用`POST`作为`Method`（方法），而不是`GET`。请阅读下文以查看两者的区别。

### POST 属性

在在上一个节中，你已经看到了当你使用`GET`技术处理表单信息时，程序地址栏中发生了什么。`GET`的备选方案是使用`POST`。将你的`FORM`的第一行更改为如下内容：

```
<form NAME ="form_1" METHOD ="post" ACTION = "">
```

关闭你的程序并重新打开。再次加载你的页面，然后点击按钮。你的地址栏将看起来像这样，不再有`?Submit1=login`部分了。这是由于我们使用了`POST`作为策略。使用`POST`意味着结构信息不会被附加到地址栏的位置供所有人看到。

我们将在书中反复使用`POST`和`GET`。尽管如此，这取决于具体的操作。如果信息不敏感，则使用`GET`，否则使用`POST`。`Form`标签的另一个重要属性是`Action`。没有`Action`，你的表单将无法去任何地方！我们将在下一节中了解它是如何工作的。

#### ACTION 属性

`Action`属性是你表单的一个重要属性。也就是说，“你需要将表单发送到哪里？”。如果你漏掉了它，你的表单将无法去任何地方。你可以将表单信息发送到另一个`PHP`脚本、同一个`PHP`脚本、一个电子邮件地址、一个`CGI`脚本或其他形式的脚本。

在`PHP`中，一种常用的策略是将脚本发送到表单所在的同一个页面——即将其发送给自己。因此，你必须更改你到为止一直使用的表单结构。放置以下内容，并将`ACTION`行更改为如下：

```
<form Name ="form_1" Method ="post" ACTION = "next_page.php">
```

所以我们将把表单信息发送到与我们堆叠的完全相同的页面——发送给自己。我们将在页面上放置一些`PHP`来处理表单信息。无论如何，现在再次保存你的工作，然后点击提交。你不会看到任何异常，也不应该看到任何错误消息！当你的脚本设置了`Action`属性时，你就可以提交它。我们将在下一节中看到。

### SUBMIT 按钮

HTML`Submit`（提交）用于将信息提交到`ACTION`中指定的脚本。下面给出了说明其工作原理的示例代码：

```
<form Name ="form_1" Method ="post" ACTION = "next_page.php">
```

因此在`ACTION`属性中指定的页面是`next_page.php`。要提交此脚本，你需要一个 HTML`Submit`按钮：

```
<input TYPE = "Submit" Name = "Submit_1" VALUE = "Login_value">
```

你不需要对`Submit`进行任何特殊操作。所有的提交工作都会完成。如果`SUBMIT`的设置了`ACTION`，那么你的信息将被发送到某处。在任何情况下，`Submit`的`NAME`属性都起到了非常有用的作用。你可以利用这个`Name`测试表单是否真的被提交，或者客户端是否最近点击了刷新按钮。

这是至关重要的。你可以利用这个`Name`测试表单是否真的被提交，或者客户端是否最近点击了刷新按钮。无论如何，现在再次保存你的工作，然后点击提交。你不会看到任何异常，也不应该看到任何错误消息！当你的脚本设置了`Action`属性时，你就可以提交它。我们将在下一节中看到。

当一个`PHP`脚本与 HTML 一致，并且在`ACTION`属性中不断提交给自身时，你就会遇到这个问题。为了解决这个问题，你可以利用备选的`IF`语句进行简单的检查。你需要做的是检查是否点击了“提交”（Submit）。如果是的话，就继续执行你的代码。要检查是否点击了提交，请使用以下代码：

```
if( isset( $_post['submit_1'] ) { }
```

你必须思考`if`声明。无论如何，在圆括号中间我们使用了`isset()`。这是一个内置功能，用于检查变量是否已设置。在圆括号中间，你使用`isset()`编写你需要检查的内容。对于我们来说，这就是`$_post['submit']`。如果客户端最近刷新了页面，那么提交的值将不会被设置。如果客户端点击了提交按钮，那么`PHP`随之会返回一个值。将你的脚本从之前的页面转换为以下代码并进行尝试：

```
if (isset($_post['submit_1'])) {
    $my_user_name = $_post['user_name'];

    if ($my_user_name == "letme") {
        print ("Welcome User!");
    }
    else {
        print ("You cannot access the website.");
    }
}
```

### ACTION 属性

你不需要像我们之前做的那样将结构信息提交到同一个`PHP`页面。你可以将其发送到一个完全不同的`PHP`页面。要了解它是如何工作的，请尝试以下操作：

创建一个页面，并命名为`next_page_2.php`。这是你的 HTML。注意`ACTION`属性。

```
<html>
<head>
<title>另一个 HTML 表单</title>
</head>
<body>
<form name ="form_1" Method ="post" Action ="submit_form.php">
<input TYPE = "text" VALUE ="user_name" Name ="user_name">
<input TYPE = "Submit" Name = "Submit_1" VALUE = "Login_value">
</form>
</body>
</html>
```

现在创建另一个页面，并命名为`submit_form.php`：

```
<?php
$my_user_name = $_post['user_name'];

if ($my_user_name == "letme") {
    print ("Welcome User!");
}
else {
    print ("You cannot access this site.");
}
?>
```

在上面的`PHP`脚本中，注意没有 HTML 标签。此外，我们还忘记了检查是否点击了提交的代码。这是因为第一个页面中没有`PHP`代码。代码只有在点击提交时才会执行。

在另一个`PHP`脚本上展示结构是保持 HTML 和`PHP`分离的方法。然而这存在一个问题。脚本在另一个页面上执行。这意味着你的结构将会消失！

### 数据保留

如之前提到的，当`next_page.php`结构被提交时，客户端输入的点会被删除。你留下了 HTML 中所在的`VALUE`。对于我们来说，点击按钮时`user_name`仍然显示在文本框中。你可以轻松地保留客户端输入的信息。你的脚本现在应该像下面的连接。如果不是，请复制并粘贴此脚本并在你的服务器上测试。

如果你查看上面脚本 HTML 中文本框的`VALUE`，你会发现它被设置为`"user_name"`。由于结构再次在自身显示，当页面提交时，这个值将继续在文本框中重新显示。更遗憾的是，如果你留空`Value`属性释放，客户端输入的所有内容都将消失。这可能是非常恼人的，如果你要求客户端再次尝试的话。

更好的方法是 POST 回客户端输入的值。要将细微元素再次 POST 到结构中，从而保留客户端已编写的信息，你可以使用这个：

```
Value="<?php print $user_name ; ?>"
```

例如，`VALUE`现在是一行`PHP`代码。这行代码简单如下：

```
<?php
print $user_name ;
?>
```

这有点难以阅读，因为所有内容都在同一行上。

你还需要更改`HEAD`段中的`PHP`代码，以包含一个`else`结构：

```
if (isset($_post['submit_1']))
{
    $user_name = $_post['user_name'];

    if($user_name == "letme") {
        print ("Welcome User!");
    }
    else {
        print ("You cannot access this site");
    }
}
else {
    $user_name ="";
}
```

在结尾的`else`声明中，我们只是在按钮没有被点击时设置变量`$user_name`的值，即页面刷新时。尽管如此，与文本框（以及其他结构组件）存在一些安全问题。

同时，我们文本框的新行 HTML 看起来如下：

```
<input TYPE = "text" Name ='user_name' Value="<?php print $user_name ; ?>">
```

### 单选按钮 (Radio Buttons)

单选按钮是一种限制用户选择一个选项的方法。单选按钮的选项可以是男/女、是/否。要获取单选按钮的`PHP`代码，单，属性是`"sex"`。单选按钮的值为`"male"`，第二个单选按钮的值为`"female"`。这里是演示这种方法的`PHP`代码：

```
<?php
$selected_radio_button = $_post[sex];
print $selected_radio_button;
?>
```

这与之前看到的代码非常相似。再次，我们可以添加代码来检查是否点击了提交：

```
if (isset($_post['submit_1'])) {
    $selected_radio_button = $_post['sex'];
    print $selected_radio_button;
}
```



这正是我们之前使用的代码。再次，然而，`PHP` 并没有保留你的选择。单选按钮的答案比简单的文本框要难以预测一些。单选按钮有另一种状态 - 已选中或未选中。你需要设置客户端选择了哪个，这里你可以实现这一点的方法：

```php
<?php

$male_button_status = 'unchecked';

$female_button_status = 'unchecked';

if (isset($_post['submit_1'])) {

    $selected_radio_button = $_post['sex'];

    if ($selected_radio_button = 'male') {

        $male_button_status = 'checked';

    }

    else if ($selected_radio_button = 'female') {

        $female_button_status = 'checked';

    }

}

?>
```

### HTML 表单代码

```html
<form name ="form_1" strategy ="post" activity ="radio_button_page.php">

<input sort = "Radio" Name = “sex” value= "male"

<?php print $male_button_status; ?>

>male

<input sort = "Radio" Name = “sex” value= "female"

<?php print $female_button_status; ?>

>female

<p>

<input sort = "Submit" Name = "Submit_1" VALUE = "选择一个单选按钮。">

</form>
```

这仅仅是一个打印语句。打印出来的是变量中的值。变量中的内容将是"checked（已选中）"或"unchecked（未选中）"语句。具体哪一个取决于我们在页面最顶端那段很长的 PHP 逻辑。我们把那部分分开处理如何？

起初，我们在代码的最顶部有两个变量：

```php
$male_button_status = 'unchecked';

$female_button_status = 'unchecked';
```

这两个变量都被设置为了 unchecked。这只是为了防止页面在刷新时（而不是在点击了 Submit 提交按钮时）出现万一的情况。

接下来，我们来验证是否已经点击了 Submit：

```php
if (isset($_post['submit_1']){}
```

此操作的方法与之前完全相同。接下来的这一行将所选的单选按钮存入变量中也是如此：

```php
$selected_radio_button = $_post['sex’];
```

然后我们需要一些条件逻辑。我们必须将一个变量设置为"checked"，所以我们需要一个 `if, else … if` 结构：

```php
if ($selected_radio_button == 'male') {

}

else if ($selected_radio_button == 'female') {

}
```

无论我们在做什么，都是在使用名为 `$selected_radio_button` 的变量中的内容。如果它的是 "male"，你可以做一件事。相反，如果它是 "female"，则做另一种操作。下面的代码说明了如何实现。

```php
if ($selected_radio_button == 'male') {

    $male_button_status = 'checked';

}

else if ($selected_radio_button = 'female') {

    $female_button_status = 'checked';

}
```

如果点击了 "male" 单选按钮，`$male_button_status` 变量应该设置为 'checked'。如果点击了 "female" 备选项，`$female_button_status` 变量应该设置为 'checked'。

### 使用复选框

与单选按钮一样，复选框用于为访客提供多种可选方案。虽然单选按钮限制客户从给出的选项中选择一个，但通过复选框你可以选择多个。

如果客户不小心漏掉了输入某些感兴趣的点，你不需要复选框中的勾选标记消失。我们在单选按钮中看到过这可能包含一些可疑的代码。复选框同样如此。

当我们编写单选按钮代码时，我们给按钮设置了相同的 `NAME`。这是因为单选按钮只能选择一种替代方案。由于客户可以在复选框中选择多个选项，因此为它们提供独特的 `NAME` 值并将它们视为离散的元素是明智的。

在你的 PHP 代码中，步骤是检查每个复选框组件是否已勾选。这与单选按钮几乎相同。首先，我们设置了五个变量，并将每一个都设置为 unchecked，就像我们之前对单选按钮所做的一样：

```php
$check_box_1 = 'unchecked';

$check_box_2 = 'unchecked';

$check_box_3 = 'unchecked';

$check_box_4 = 'unchecked';

$check_box_5 = 'unchecked';
```

下面的代码检查提交按钮是否被点击。

```php
if (isset($_post['submit_1'])) {

}
```

而在另一段代码中，我们有另一种 `isset()` 用：

```php
if ( isset($_post['cb_1']) ) {

}
```

这一次，我们正在验证复选框是否被点击。我们这样做是因为 HTML 复选框的一个特性。万一它们没有被勾选，它们就没有任何值，因此什么都不会返回！万一尝试在不检查复选框是否勾选的情况下运行代码，那么你将需要处理大量的“不明确”错误。

然而，如果复选框被勾选，它将返回一个值。因此，`isset()` 功能将为真，`if` 代码将执行。

```php
if($cb_1 == 'val_1') {

    $cb_1 = 'checked';

}
```

这是另一个 If 语句！总之，我们只是在检查一个变量的值。我们必须理解它的内容。这个语句的意思是：“如果名为 `$cb_1` 的变量的值是 "value_1"，则执行某些代码。”我们需要执行的代码是将名为 `$cb_1` 的变量内容置为 "checked"。剩余的 `if` 语句都是相同的——结构中的每个复选框都对应一个。我们需要做的完全相反的操作是将变量的值打印到 HTML 结构中：

```html
<input sort = "checkbox" Name ='cb_1' value ="value_1"

<?php print $cb_1; ?>
```

visual Basic .NET

再次，这是你在单选按钮处看到的相同代码。PHP 部分是：

```php
<?php print $cb_1; ?>
```

所以我们只是在打印名为 `$cb_1` 的变量中的内容。这将是 "checked" 要不是 "unchecked"。复选框还有其他答案，但没有看起来是简单的！然而，这里的重点是运用你在条件逻辑章节中学到的概念。

# PHP 中的循环

那么什么是循环呢？循环就是环绕运行的东西。在计算机程序中也是如此。但编程循环会一直环绕，直到你告诉它停止。

我们将在本章检查几种类型的循环。然而，For 循环是最常用的，这就是为什么我们先讨论它。

## For 循环

For 循环是最常用的结构。它通常比它的对应品更容易实现且无错误。这里有一个小的循环示例。将其添加到新的脚本中然后...

```php
<?php

$start_val = 1;

$count_val = 1;

for($start_val; $start_val <= 10; $start_val++) {

print $count_val . "<br>";

$count_val = $count_val + 1;

}

?>
```

你是如何得到它的？你应该会在程序页面上看到 1 到 10 的数字。

For 循环的通用语法为：

```
for (起始值; 结束值; 更新值表达式) {

}
```

### 值

主条件是你告诉 PHP 循环变量初始值的地方。在这里，PHP 应该从什么值开始循环？我们使用了这个：

```php
$start_val = 1;
```

我们为名为 `$start_val` 的变量分配了一个 1 的值。像所有变量一样，你可以给变量命名。初始变量常用的名称是字母 i 或 j。你可以在循环开始之前设置起始条件，正如我们所做的：

```php
$start_val = 1;
```

另一方面，你可以将循环变量值直接放在“For 循环”代码中，如下所示：

```php
for($start_val = 1; $start_val <= 10; $start_val++) {
```

结果是相同的，因为这个循环的起始数字是 1。

接下来，你需要告知 PHP 何时结束循环。这可以是一个数字、字符串、布尔值以及任何其他表达式或条件。在这里，我们告诉 PHP，当变量 `$start_val` 的估值小于或等于 10 时，继续执行循环。

```php
for($start_val = 1; $start_val <= 10; $start_val++) {
```

当 `$start` 的估值达到 11 时，PHP 将结束循环并跳出作用域。

### 升级表达式

循环需要一种方法来获取循环变量的下一个数字，这在 `for` 结构中以更新表达式的形式给出。如果万一循环无法更新初始值，它将停留在初始值上。打个比方，你必须告诉循环如何循环运行。我们利用了这种方法：

```php
$start_val++
```

在许多编程语言（以及 PHP）中，双倍或更多次数运算符（`++`）表示加法（将值增加一）。这仅仅是这种操作的一种简便方法：

```php
$start_val = $start_val + 1
```

你可以利用双倍减小运算符（`--`）以相同的方式减少值，但我们不会介绍这一点。

所以，我们的整个循环的意思是：“从估值 1 开始，只要循环变量的值小于 11，就继续循环，每次执行循环时将初始值加一。”

循环每运行一次，我们两个波浪括号部分 `{ }` 之间的代码就会执行一次：

```php
print $count_val . "<br>";

$counter = $count_val + 1;
```

注意，我们只是每循环一次将计数器变量加 1，这与我们处理 `$start_val` 变量的方式完全相同。所以我们可以这样写：

```php
$count_val ++
```

效果是相同的。作为一个测试，尝试在循环外部将 `$count_val` 的估值设置为 11，目前它是 `$count_val = 0`。此时在循环内部，使用 `$counter--`（双倍减小符号）。你能想象出会发生什么吗？它会崩溃还是不会？另一方面，它会打印出内容吗？万一出现问题，最好保存好你的工作！

### While 循环

与使用 `for` 循环相比，你可以选择使用 `while` 循环。`while` 循环的结构比 `for` 循环简单，因为你只需要评估一个条件。只要条件为真，循环就会继续运行。当条件为假时，它跳出整个循环。这里是语法：

```php
while (testing_condition) {

    //Code

}
```

下面的代码演示了 `while` 循环的实现。

```php
$count_val = 1;

while ($count_val < 11) {

    print (" count_val = " . $count_val . "<br>");

    $count_val++;

}
```

要测试的条件是 `$count_val < 11`。每循环整个圈，都会检查该条件。如果 `count_val` 小于十一，则条件为真。当 `$counter` 大于十一时，条件为假。`while` 循环在条件为假时会停止继续运行。

如果你使用 `while` 循环，请小心不要导致死循环。如果条件在所有情况下都返回真，你就会创建一个死循环。

### Do-While 循环

这种类型的循环与整个循环几乎没有区别，只是条件是在最后进行检查的：

```php
do {

    //Code

}while (testing_condition)
```

区别在于，你的代码无论如何至少会执行一次。在普通的 `while` 循环中，在你的代码执行之前可能满足条件，循环将立即退出。然而在这里，条件是在循环代码执行一次后才检查的。

不要过度担心 `do...while` 循环。在实际编程目的中，请关注 `for` 循环。同时，还有另一种非常有用的循环类型，称为 For Each 循环。然而，它很少被使用，因此我们选择完全跳过对它的描述。

### Break 关键字

有时，你需要在整个循环执行之前跳出循环。或者，由于你的代码或客户端可能发生的错误，需要在不知道发生的情况下跳出。在这种情况下，你可以使用 `break` 关键字。幸运的是，这只需要编写 `break` 后跟一个分号。

## 数组

到目前，你必须理解什么是变量——简单的就是存储数字和文本的地方。问题是，变量在一次只能存储一个值。你可以在变量中存储一个数字，或一个字符串。数组类似于任何唯一的变量，它可以同时持有多个数字或多个字符串。如果你有一组项目（例如客户端请求），并且你必须对它们进行某些操作，那么这样做将非常麻烦：

```php
$order_1 = "Shoes Variety 1";

$order_2 = "Shoes Variety 2";

$order_3 = "Shoes Variety 3";

$order_4 = "Shoes Variety 4";
```

你可以遍历你的请求并找到特定的一个，或者访问并逐一修改。此外，假设你拥有的不是四个请求，而是数百个。

### 向数组添加元素

你可以使用两种基本方法向数组放置元素。

#### 方法一：在圆括号内指定

这种方法是在 `array()` 的圆括号之间编写你的值。在下面的代码中，我们建立了一个数组来存放衣柜里的外套类型：

```php
$coat_types = array("Winter Coats", "Summer Coats", "Short Coats", "Over Coats");
```

所以数组的名字是 `$coat_types`。在 `array()` 的圆括号之间，我们写了几个值。每个值由逗号区分。

数组的工作原理是有一个位置以及该位置的某些信息。在上面的数组中，“Winter Coat”位于位置 0，“Summer Coats”位于位置 1，“Short Coats”位于位置 2，“Over Coats”位于位置 3。

主位置始终是零，除非你告诉 PHP 其他设置。任何位置被称为键（key）。键随后关联有一个值。你可以通过以下方式指定你自己的数字键：

```php
$coat_types = array(1 => "Winter Coats", 2 => "Summer Coats", 3 => "Short Coats", 4 => "Over Coats");
```

所以，你为你的键写了一个数字。在上面的例子，第一个键当前是 1 而不是 0。键 1 下的内容是 "Winter Coats"。最后一个键是 4，键 4 下的内容是 "Over Coats"。

#### 方法二：给类赋值

另一种向数组放置值的方法，类似于下方的代码：

```php
$coat_types = array();

$coat_types[ ]="Winter Coats";

$coat_types[ ]="Summer Coats";
```

```php
$coat_types[]="Short Coats";

$coat_types[]="Over Coats";
```

在这里，数组最初通过 `$coat_types = array();` 创建。这告诉 PHP 你需要创建一个名为 `$coat_types` 的数组。要在这个集合中存储值，你首先对簇的名称进行排序，通过一对方括号部分来模拟：

`$coat_types[]`

在等号之后，你写下你想要在这个位置存储的内容。由于在方括号中间没有写任何数字，PHP 将分配数字 `0` 作为第一个键：

0=> "Winter Coats",
1=> "Summer Coats",
2=> "Short Coats",
3=> "Over Coats"

### 访问数组元素

实际上，你有几种方法可以实现这一点。然而，“键”（Key）是关键的。这里有一个示例供你尝试：

```php
<?php

$coat_types = array("Winter Coats", "Summer Coats", "Short Coats", "Over Coats");

print $coat_types[0];

?>
```

这个数组就是我们不久前设置的那个。要获取簇内部的内容，只需对你想要获取的键数字进行排序。在上面的代码中，我们正在打印数组中 `0` 位置（键）所包含的内容。你只需要按照如下方式将键数字放在你的显示名称的方括号之间：

`print $array_name[0];`

## 关联数组

你的簇键不需要像上一个部分那样是数字。它们也可以是字符串。这可以帮助你记住键中包含什么，或者它应该做什么。当你使用内容作为键时，你正在使用一个关联簇；当你使用数字作为键时，你正在使用一个标量数组。这里有一个设置了名字首名和姓氏合并的簇：

```php
$name = array( );

$name["nick"] = "Carter";

$name["richard"] = "Waters";
```



要获取关联数组中的值，只需引用键名即可：

`print $name["nick"];`

尽管如此，由于关联数组没有使用数字作为键，因此使用了另一种系统来循环遍历它们——`For Each` 循环。

## 数组排序

有时你可能需要对数组中的值进行排序。例如，假设你的数组元素不是有序的。像下面这一个：

```php
$name = array( );
$name["nick"] = "Carter";
$name["richard"] = "Waters";
```

要对此数组进行排序，你只需要使用 `asort()` 函数。这并不包括编写 `asort` 语句之外复杂的语句，它由圆括号部分模拟。在圆括号中间，为你的关联项进行排序：

`asort( $name);`

用于对显示值进行排序的不同函数包括：

- `rsort()` – 逆序排序标量数组
- `arsort()` - 逆序排序关联簇的值
- `krsort()` - 逆序排序关联簇的键

## 获取随机键

你可以从簇中获取一个随机键。这在某些编码场景中可能是很有用的。

```php
<?php
$number_array = array(1 => 1, 2 => 2, 3 => 3, 4 => 4, 5 => 5, 6 => 6);
$random_key_element = array_rand($number_array, 1);
print $random_key_element;
?>
```

提供比例键的函数是这个：

`array_rand($number_array, 1);`

你从 `array_rand()` 函数开始。在圆括号中间，你需要两个东西：你的数组名称以及你需要的键的数量。

## PHP 中的 Count 函数

当你需要返回数组中有多少个组件时，`count()` 函数非常有用。

要获取簇中有多少个组件，我们使用了这个：

`$array_count = count($coat_types);`

## 字符串处理

处理字符串内容并控制它们是你作为开发者所需的能力之一。如果客户端在你的结构上输入了细微元素，你就必须检查并接受这些信息。通常，这包括对这些文本进行某些操作。

这些操作的示例包括将字母从小写转换为大写或反之亦然、检查客户端拥有什么程序，或者从内容框输入的内容中删减空白。这些属于字符串控制的范畴。首先，我们看看如何更改字符的大小写。

### 更改字符的大小写

假设你的结构上有一个文本框，要求客户输入名字和姓氏。很有可能有人输入这样的内容：

jack waters

而不是这样的：

Jack Waters

所以你作为开发者的工作是将每个名字的首字母从小写改为大写。这在 PHP 中非常简单。它只是一个文本框和一个按钮。当你搭建它时，文本框中会填入 "jack waters"。我们需要的是在点击按钮时将其转换为 "Jack Waters"。下面是实现该功能的脚本。

```php
<?php
$name = 'jack waters';

if(isset($_post['submit_1'])) {
    $name = $_post['user_name'];
    $name = ucwords( $name );
}
?>
```

当页面加载时，这行语句验证了小写转换：

`$name = 'jack waters';`

我们需要的是将其转换为 "Jack Waters"。用于此操作的行是：

`$name = ucwords( $name );`

如果你只需要将字符串的首字母改为大写（例如对于一个句子），可以使用：

`ucfirst()`

### 修剪空格

你可能需要做的另一事情是从文本中修剪空格。这很简单，因为有一些 PHP 函数可以帮你这样做。假设客户输入了这样的：

" user_name "

从引号中看到内容前后都有空格。我们可以使用一个替代方案计算这个字符串有多少个字符：`strlen()`。正如其名所示，它给出字符串的长度。通过长度，我们指的是字符串有多少个字符。尝试这个脚本：

```php
<?php
$w_space = " user_name ";
$count_val = strlen($w_space);
print $count_val;
?>
```

当你运行脚本时，你会发现变量包含了 15 个字符。然而，user_name 只有 9 个字符。要去掉空格，你可以使用 `trim()` 函数。将你的脚本改为：

```php
<?php
$w_space = trim(" user_name ");
$count_val = strlen($w_space);
print $count_val;
?>
```

现在运行脚本，你应该应该发现变量拥有正确的字符数量——9。这是因为 `trim()` 函数删除了字符串两侧的任何空格。两个相关的函数是 `ltrim()` 和 `rtrim()`。第一个 `ltrim()` 去除字符串起始处的空格；第二个 `rtrim()` 去除字符串末尾的空格。

要拆分内容行，可以使用 `explode()` 函数。你最近向它传递了需要拆分的内容，以及用于拆分每个部分的字符。其语法结构如下：

`explode( separator, string_to_split )`

在 `explode()` 函数的圆括号中间，首先是你需要使用的分隔符 `separator`（用逗号表示），然后是你需要拆分的字符串。对于我们上面的那行代码，你可以这样操作：

```php
$line_text = "Numbers 1, 450, 3500, 264, 500, 7869";
$line_text = explode( "," , $line_text );
```

所以基本上我们是在说：“在内容中搜索逗号，并将该行内容拆分成特定的部分。”一旦 PHP 完成了任务，它会将所有部分放入等号（` = `）左侧的变量中，对我们来说这个变量就是 `$line_text`。这个变量将变成一个数组！

### 合并字符串

如果你在数组中有一行内容，你可以将它们合并在一起以构造成单行内容。这与 `explode` 是完全相反的。这次，请使用 `implode()`：

```php
$coat_type = array("Winter Coats", "Summer Coats", "Short Coats", "Over Coats");
$line_new = implode( ",", $coat_type);
```

在这里，我们有一个名为 `$coat_type` 的数组。在将数组重新连接到内容记录之前，需要对数组中的内容进行合并。`implode()` 函数负责合并。`implode()` 函数的结构与 `explode()` 。

`implode(separator, texts_to_join )`

因此，在上面的代码中，`implode()` 将所有内容合并并用逗号分隔每个部分。显然，你并不一定要使用逗号。你可以使用任何其他字符。

### PHP 中的转义字符

PHP 中的转义序列（Escape sequence）并不意味着逃离并“跑路”。它是一种防止 PHP 过早终止字符串的方法，或者用于验证你返回了正确的字符串数据。这是一个示例。尝试此脚本：

```php
<?php
$my_string = 'This is Sarah’s car';
print $my_string;
?>
```

验证你是否完全按照原样编写了脚本，带有所有的单引号标记。接下来，运行脚本。你将会发现 PHP 为你提供了一个错误信息。由于你有三个单引号标记，PHP 感到困惑，因为它不知道你的字符串是什么。为了解决这个问题，你可以在外层使用双引号。如下：

```php
$my_string = "This is Sarah’s car";
```

或者你也可以避开标点符号。通过在字符前面写一个 `\` 来转义该字符。如下：

```php
$my_string = 'This is Sarah\’s car';
```

如果你尝试那样操作，你会发现字符串打印得非常完美。

现在尝试此脚本：

```php
<?php
$new_string = 'mypath\';
print $new_string;
?>
```

再次，你将收到来自 PHP 的信息，指出代码中的错误。用双引号而不是单引号包裹它并再次运行脚本。字符串打印出来了吗？没有打印的原因是你没有转义转义字符。PHP 将其视为一个普通字符，并期望反斜杠后面有更微妙的元素。为了避免这种疏忽，你可以使用以下代码：

```php
$new_string = 'mypath\\';
```

现在我们在字符串末尾有两个反斜杠。当你运行脚本时，你会观察到它打印出了：

`mypath\`

如果你的 PHP 脚本没有返回它应该返回的内容，那么你可能需要使用斜杠来转义它们。在处理数据库工作时，你还需要转义某些字符，否则你将面临长长的错误信息和警告。

### 一些重要的字符串函数

与其列举所有你可以使用的可能的字符串函数，我们将为你提供一个简短的列表。如果你点击下面的链接，将会有如何使用每个字符串函数的案例。只需在需要时使用它们即可。

- `ord()`：确定字符的 ASCII 值
- `chr()`：将 ASCII 值转换为字符
- `similar_text()`：确定两个文本字符串之间的相似性
- `echo()`：用作 `print` 的替代方案
- `substr()`：返回字符串的子字符串
- `str_replace()`：执行一个字符串到另一个字符串的替换
- `str_repeat()`：执行指定次数的字符重复
- `strlen()`：返回字符串长度
- `str_word_count()`：返回字符串中的单词数

# PHP 中的函数

函数仅仅是一段代码。然而，它与你的主代码不同。你将其分离是因为它是合理的且有用的，而且你不仅使用一次，而是反复使用它。它是你认为有价值的并需要再次使用的代码。函数可以避免你重复编写代码。

假设你必须检查文本框中的内容。你需要从客户端输入的内容左侧和右侧删除任何空白。所以，如果他们输入了：

`" Jack Waters "`

你需要将其转换为：

`"Jack Waters"`

在任何情况下，你还需要检查客户端是否输入了任何内容。你可以利用 `trim()` 函数来实现这一目的。

```php
$entered_text = trim($_post['text']);

if ($entered_text == "") {
    $error_message = "Nothing written in the box";
}
```

```php
print_message();

function print_message() {
    print "Error!";
}
?>
```

如果你恰好使用的是 `PHP` 4 或更高版本，你不应该看到任何区别——无论如何，函数都会在函数定义的上方或下方被执行。然而，为了代码的整洁和连贯性，最好将函数的大部分放在脚本的顶部或底部。更出乎意料的是，你可以将其放在另一个 `PHP` 文档中。这时你可以利用一个名为 `include` 的备内置函数。

## 函数作用域 (Function Scope)

在编程中有一种被称为“作用域”（scope）的概念。这指的是变量在脚本的哪个位置是可见的。如果一个变量从任何地方可见，则认为它具有全局作用域。在 `PHP` 中，函数内部的变量从外部外部可见。此外，如果变量不是函数的一部分，函数就无法看到它。请尝试将这个脚本作为一个案例：

```php
<?php
$err_message = "Error Found!";

print_message();

function print_message( ) {
    print $err_message;
}
?>
```

这一次，我们设置了一个名为 `$err_message` 的变量来存储消息内容。它位于函数外部。运行该脚本，你将得到一个关于“Undefined variable”（未定义的变量）的 `PHP` 错误信息。

同样，尝试这个脚本：

```php
<?php
print_message();

print $err_text;

function print_message() {
    $err_text = "Error!";
}
?>
```

这一次，变量在函数内部。然而，我们试图从函数外部打印它。无论如何，你都会得到一个错误信息。这里有一个正确的写法：

```php
<?php
print_message();

function print_message() {
    $err_text = "Error!";
    print $err_text;
}
?>
```



[点击此处阅读更多...](http://www.amazon.com/gp/product/B015C4MHE0/ref=as_li_qf_sp_asin_il_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=B016QNZGXK&linkCode=as2&tag=wwwglobaliz07-20&linkId=6HFUR2GISA7ABPMK)

[](http://www.amazon.com/gp/product/B015C4MHE0/ref=as_li_qf_sp_asin_il_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=B016QNZGXK&linkCode=as2&tag=wwwglobaliz07-20&linkId=6HFUR2GISA7ABPMK) 入门 `jQuery`、`JavaScript` 和 `HTML5`

作者：Scott Sanderson

## 目录

- [第一章：引言](https://docs.google.com/document/d/1keHABpXmrn4pVW06cST-8ILc5UkATcAxxEmvwfk/edit#heading=h.2xcytpi)
- [第二章：HTML5 基础](https://docs.google.com/document/d/1T2xpmhSO1XMYQRSHqfGK5gROM6tcAqW6ZifJCs/edit#heading=h.ci93xb)
- [第三章：JavaScript 基础](https://docs.google.com/document/d/1T2xpmhSO1XMYQRSHqfGK5gROM6tcAqW6ZifJCs/edit#heading=h.3whml4)
- [第四章：CSS3 基础](https://docs.google.com/document/d/1T2xpmhSO1XMYQRSHqfGK5gROM6tcAqW6ZifJCs/edit#heading=h.bn6wsx)
- [第五章：HTML5 详解](https://docs.google.com/document/d/1T2xpmhSO1XMYQRSHqfGK5gROM6tcAqW6ZifJCs/edit#heading=h.q70q)
- [第六章：JavaScript 和 jQuery](https://docs.google.com/document/d/1T2xpmhSO1XMYQRSHqfGK5gROM6tcAqW6ZifJCs/edit#heading=h.3as4poj)
- [第七章：表单](https://docs.google.com/document/d/1T2xpmhSO1XMYQRSHqfGK5gROM6tcAqW6ZifJCs/edit#heading=h.1pxezwc)
- [第八章：Web 服务](https://docs.google.com/document/d/1T2xpmhSO1XMYQRSHqfGK5gROM6tcAqW6ZifJCs/edit#heading=h.49x2ik)
- [第九章：WebSocket 通信](https://docs.google.com/document/d/1T2xpmhSO1XMYQRSHqfGK5gROM6tcAqW6ZifJCs/edit#heading=h.2p2csry)
- [第十章：利用 Web 存储管理本地数据](https://docs.google.com/document/d/1T2xpmhSO1XMYQRSHqfGK5gROM6tcAqW6ZifJCs/edit#heading=h.147n2zr)
- [第十一章：离线 Web 应用](https://docs.google.com/document/d/1T2xpmhSO1XMYQRSHqfGK5gROM6tcAqW6ZifJCs/edit#heading=h.3o7alnk)
- [附录](https://docs.google.com/document/d/1T2xpmhSO1XMYQRSHqfGK5gROM6tcAqW6ZifJCs/edit#heading=h.23ckvvd)

Copyright 2015 by [Global Healing](http://www.globalhealing.com) 保留所有权利。

## 第一章：引言

如果有一个框架可以被认为是全面的，那么 `HTML5` 胜出了。尽管 `HTML5` 的规范尚未完全制定，但大多数浏览器都支持它。这意味着，如果你想立即开始创建自己的应用程序，但不知道如何操作以及从哪里开始，那么这本书正是为你准备的。这本书涵盖了从最基础到你所需的一切内容。然而，它并不是一本参考指南。我们希望为你提供实用的知识，让你尽可能地上手。前三章将向你介绍这些技术，为你提供一个起点。

## 第二章：HTML5 基础

`HTML`（超文本标记语言）是一种用于创建网页的语言。事实上，这种语言自第一个网页诞生以来就一直在使用。然而，随着更新、更好版本的语言推出，其功能也在演进。这种语言起源于 `SGML`（标准通用标记语言），它曾被用于文档出版。`HTML` 从 `SGML` 继承了格式化功能概念及其语法。

对于浏览器而言，`HTML` 使用最有趣且有益的方面之一是，浏览器同时支持向后兼容和向前兼容。虽然向后兼容通常很容易实现，但向前兼容是棘手的，因为在这种情况下，问题领域是无限的。然而，为了实现这一点，浏览器被设计为忽略它们不识别的标签。

多年来，`HTML` 一直满足着人们的需求。但随着时间的推移，人们觉得需要更多，而这种需求被名为 `XML`（可扩展标记语言）的技术出现所催化。尽管 `XML` 与 `HTML` 有许多相似之处，但两者之间存在许多根本区别。首先，`XML` 要求标签匹配，这意味着每个起始标签都必须存在一个结束标签。此外，`XML` 允许你创建自己的标签，因为它不像 `HTML` 那样拥有固定的标签集。

`XML` 中使用的标签是元标签或描述起始标签和结束标签之间包含数据的标签。为了确保 `XML` 文档的有效性，使用名为 `XSD`（XML 定义）的技术。然而，这种技术无法验证 `HTML` 文档，因为 `HTML` 文档缺乏良好的结构。

## 介绍

W3C（万维网联盟）引入 `XHTML` 是为了尝试修复 `HTML` 的缺陷。根据 `XHTML` 规范，`HTML` 文档被强制遵守用于 `XML` 的格式规范。因此，这允许使用 `XSD` 工具来对 `HTML` 文档进行验证。尽管在框架中集成 `XML` 解决了一些问题，但某些问题仍然层出不穷。现代一个令人震惊的问题之一是对多媒体集成的需求日益增长。虽然 `CSS` 执行了一定程度的格式化，但它已无法满足用户日益增长的需求。

为了给交互性和动画视觉提供支持，该组合中添加了一个名为 `JavaScript` 的可编程支持。然而，这种支持的初始版本对程序员来说难以理解，且执行速度缓慢。这导致了 `Flash` 等插件的引入，并获得了关注。这些插件完成了预期的任务，但浏览器与多媒体的集成在本质上仍然是松散的。

`HTML5` 并不是 `XHTML` 的演进形式。相反，`HTML5` 可以被更好地描述为 `HTML 4.01` 的重构形式，以及如何结合使用 `HTML`、`CSS` 和 `JavaScript` 来解决用户日益增长的需求。

## 语义化标记

`HTML5` 的基本特征是它强调行为、呈现和结构的分离。网站开发的语义化标记规定了文档的结构。换句话说，它规定了标签的含义以及它们将为你完成什么。另一方面，行为和呈现分别由 `CSS` 和 `JavaScript` 负责。

## HTML5 元素

在 `HTML` 中，一个元素简单来说就是包含一个起始标签、内容和一个结束标签的语句。因此，当你写下时：

```html
<div>
  <b>This is my world!</b>
</div>
```

在示例中，`div` 元素包含了从 `<div>` 到 `</div>` 的所有内容。因此，`<b>`-`</b>` 标签也是 `div` 元素的一部分。

在这里需要说明的是，`HTML5` 是不区分大小写的。因此，无论你将加粗标签写成 `<B>` 还是 `<b>`，浏览器都会认为它们是相同的。但是，W3C 标准建议对标签使用小写。

## 在 HTML5 中使用元素

`HTML5` 定义了超过 100 个元素。这些元素及其定义在附录中提供。

### 如何为元素添加属性？

额外数据可以以属性的形式添加到起始标签中。属性通常可以表示为 `name="value"`。属性名的值包含在引号内。对于起始标签，可以添加的属性数量没有限制。对于这些属性，属性有一个名称，但没有值。

示例：

```html
<div id="main" class="mainContent"></div>
```

在这里，`id` 和 `class` 是属性，其中 `id` 唯一标识元素，而 `class` 指定了该 `div` 所属的 `CSS` 样式。

### 布尔属性

可以使用几种类型的属性。最常用的类型之一是布尔属性。布尔属性可以从允许的值集中取值。一些可能的值包括：

- `Checked`
- `Disabled`
- `Selected`
- `Readonly`

有两种方法指示布尔属性的值：

```html
<input type="checkbox" name="vegetable" value="Broccoli" checked='' />
<input type="checkbox" name="vegetable" value="Broccoli" checked='checked' />
```

在第一种情况下，没有给出值，而是假设的。尽管后者看起来像是冗余的形式，但它是更推荐的形式，特别是当你使用 `jQuery` 时。

### 全局属性引用

`HTML5` 中有一组命名的属性，可以与任何元素一起使用。这些属性示例包括 `accesskey`、`spellcheck` 和 `draggable` 以及其他几个。

### 空元素

某些元素在任何情况下都不包含内容。这些元素包括 `<link>`、`<br>` 和 `<area>` 以及许多其他元素。

### 自闭合标签

如果你使用的元素不包含任何内容，可以使用自闭合标签。这种标签的示例是 `<br/>`。但是，请注意，像 `<div>` 这样的标签即使没有内容，也必须写成 `<div></div>`。

### 如何添加扩展属性

你作为作者定义的任何属性都称为扩展属性（expando attribute）。你可以为这个自定义属性命名，并在需要时根据需要为其分配一个值。

## 如何添加注释

可以使用 `!` 和两个连字符（`-`）来添加注释。添加注释的语法如下：

```html
<!--text -->
```

你还可以使用以下语法添加条件注释：

```html
<!--[if lte IE 7]><html class="no-js ie6" lang="en"><![endif]-->
```

此注释决定了使用的浏览器是否比 `IE7` 更早发布的早期版本。

## 如何创建 HTML 文档

`HTML` 文档可以简单地描述为一个包含元数据、内容和结构的框架。

`HTML` 文档必须以标签 `<!DOCTYPE html>` 开始。在 `HTML5` 中，该声明是指示浏览器应该在无奇怪模式（no-quirks mode）或 `HTML5` 兼容模式下运行。

下一个应该是 `<html>`。此元素内部包含了 `<head>` 和 `<body>` 元素。`<head>` 元素可以包含 `HTML` 文档的元数据，这些元数据是通过 `<meta>` 标签声明和定义的。`<head>` 元素包含 `<title>` 元素，其作用如下：

- 被搜索引擎使用
- 在浏览器工具栏显示
- 为页面提供默认名称

`<body>` 元素包含了要显示的任何信息。示例 `HTML` 文档如下：

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>TITLE OF DOC</title>
</head>
<body>
  CONTENT
</body>
</html>
```

注意：

1. `HTML` 语法中的特殊字符如 `>` 或 `<` 可以通过它们的名称或数字使用。附录包含了要使用的实体名称和数字。
2. 使用制表符、换行和空格创建的空白会被 `HTML` 归一化为单个空格。因此，如果你想使用多个空格，必须使用不换行空格。例如，如果你想显示 `10 mph` 使得 `10` 和 `mph` 之间不换行，你可以写 `10&nbsp;mph`。

## 如何嵌入内容

现在你已经知道如何创建内容的 `HTML` 文档，你可能想从其他源向文档嵌入内容。这些内容可以是另一个 `HTML` 文档或 `Flash` 应用。

### 内联框架

内联框架用于将 `HTML` 文档嵌入到当前文档的内容中。因此，这种元素创建了嵌套浏览器，多个网页在同一个窗口中加载。这些通过 `<iframe>` 元素实现。嵌套浏览器上下文可以使用以下方法导航：

- `window.parent` – 此 `WindowProxy` 对象表示父浏览器上下文。
- `window.top` – 此 `WindowProxy` 对象表示顶级上下文。
- `window.frameElement` – 这表示浏览器上下文容器，如果没有上下文容器，它将返回 `null`。

`<iframe>` 元素的语法如下：

```html
<iframe src="name"></iframe>
```

在这里，属性的名称定义了浏览器上下文的名称。这个名称可以是任何字符串，如 `sample.html`。然而，名称不应以下划线开头，因为以下划线开头的名称被留给了特殊键名，如 `_blank`。

### 沙箱

沙箱用于避免在你的 `HTML` 文档中引入弹出窗口或任何恶意软件。为了实现这一点，使用了 `sandbox` 属性。你可以按照以下方式使用该属性：

```html
<iframe sandbox="keywords" src="name"></iframe>
```

当你使用沙箱（sandboxing）时，被调用的上下文将受到若干限制。这些限制包括禁用表单、脚本、插件以及自身以外的任何框架。你可以使用等关键词强制系统覆盖这些限制：

- `allow-same-origin`
- `allow-scripts`
- `allow-forms`
- `allow-top-navigation`

可以使用空格分隔来同时使用多个关键词。

### 无缝嵌入

`seamless` 属性可以用于 `<iframe>` 元素，以一种方式嵌入内容，使得内容看起来就像是主内容的一部分。该属性可以如下所示使用：

```html
<iframe seamless="" src="name"></iframe>
<iframe seamless src="name"></iframe>
<iframe seamless="seamless" src="name"></iframe>
```

许多浏览器可能不支持此属性。因此，你可以使用 `CSS` 来实现类似的效果。

## 超链接

超链接可以使用 `<a>` 标签实现。该元素可以用于链接到外部（不同的 `HTML` 文档）以及内部（同一个 `HTML` 文档中的另一个位置）链接。

所有链接都有下划线，并且根据链接的性质，链接的颜色会发生变化。

- 蓝色 - 未访问的链接
- 紫色 - 已访问链接
- 红色 - 激活链接

`<a>` 元素的第一个属性是 `href`，其值为 `URL` 地址。

### 外部链接的语法：

```html
<a href="address">Text</a>
```

### 内部链接的语法：

```html
<a href="#id">Text</a>
```

这里的 `id` 是你希望链接跳转到的标签的 `id`。然而，如果你只使用 `#` 值，链接将跳转到页面顶部。

与 `<a>` 元素配合的另一个属性是 `target`，它允许你控制链接的行为。例如，如果你想让链接在另一个窗口中打开，则可以使用此属性指定该要求。可以使用以下值：

- `_blank`: 在新的浏览器窗口中打开链接。
- `_parent`: 在父窗口中打开链接。
- `_self`: 在当前窗口中打开链接，这是默认设置。
- `_top`: 在当前窗口的最顶层框架中打开链接。
- `<iframe_name>`: 在指定名称的 `<iframe>` 元素中打开链接。这通常用于菜单。

超链接还可以使用以下语法发送电子邮件：

```html
<a href="mailto:email address">Text</a>
```

当用户点击链接时，将向指定的电子邮件地址发送一封电子邮件。

## 嵌入图像

`<img>` 元素用于向 `HTML` 文档中添加图像。`<img>` 标签是一个空元素（void element），不需要闭合标签。

该元素所需的标签是 `src`，它指定存储图像的绝对地址或相对地址。与 `<img>` 标签配合的另一个属性是 `target`，用于指定在图像不可用时必须显示的文本。

### 语法：

```html
<img src="address" target="alternative text">
```



需要注意的是，你只是提供了图像的引用，实际上并没有将其嵌入 HTML 文档中。允许的图像格式有`jpeg`、`svg`、`png`和`gif`。

## 如何创建图像映射

`<map>`元素可以创建可点击的图像映射。为了在地图和图像之间建立链接，必须为地图设置一个`name`，并在`img`标签的`usemap`属性中使用该名称。

地图元素的区域使用`<area>`元素定义。这是一个用于定义地图区域的自闭合标签。地图区域可以使用`shape`、`href`、`alt`和`coords`属性设置。

`shape`属性可以取`poly`、`circle`、`rect`或`default`值。默认值将区域设置为图像的大小。`href`和`alt`属性的使用方法与`<a>`元素中相同。最后，`coords`属性根据所选形状按如下方式定义：

- `poly` – `x1, y1, x2, y2, … , xn, yn`
- `circle` – `x, y, radius`
- `rect` - `x1, y1, x2, y2`

对于多边形（polygon），起始和结束坐标应该是相同的。如果在此方面存在差异，则添加一个闭合值。

### 示例：

```
<img src ="worldmap.gif" width="145" height="126" alt="World Map" usemap ="#country" />

<map name="country">
  <area shape="circle" coords="105,50,30" href="China.html" alt="China" />
  <area shape="default" href="InvalidCountry.html" alt="Please Try Again" />
</map>
```

## 嵌入插件

插件同样可以使用`<embed>`和`<object>`元素嵌入到 HTML 文档中。尽管这两个元素执行的任务相似，但它们是由不同的浏览器创建的。因此，它们在 HTML5 中共存。`<embed>`元素提供了易用性，而`<object>`元素为用户提供了更多功能。这两个元素的语法如下：

### `<embed>`标签

```
<embed src="Flash.swf"> </embed>
```

`src`属性指定要嵌入文件的 URL 或地址。`<embed>`元素接受的其他属性包括：

- `type` – 用于指定内容的 MIME 类型
- `height` – 用于指定内容的高度（像素）
- `width` – 用于指定内容的宽度（像素）

### `<object>`标签

```
<object data="file.wav">
  <param name="autoplay" value="false" />
</object>
```

这种编程语言最重要的特性之一是它是无类型的。换句话说，在使用变量时没有必要指定其类型。例如，如果你给一个变量赋值了一个字符串，稍后也可以为该变量赋值一个整数。变量使用关键字`var`进行声明。

# 数据与表达式

任何程序都会对数据进行访问、操纵并向用户展示数据。数据以不同的类型和形式存在。这些数据可以很容易地分解为值。在 JavaScript 中，数据可以以原始值、对象或函数的形式表示。

最低层的数据表示被称为原始数据类型，包括`null`、`undefined`、`number`、`string`和`Boolean`。

JavaScript 中定义了多个内置对象。这些包括`Object`对象、全局对象、`Array`对象、`Function`对象、`Boolean`对象、`String`对象、`Math`对象、`Number`对象、`RegExp`对象、`Date`对象、`Error`对象和`JSON`对象。

任何可调用的对象称为函数。如果该函数与对象关联，则也被称为方法。

数据是通过表达式产生的，表达式是任何生成值的代码的名称。它可以直接赋一个值，也可以通过替换和计算由操作数和运算符组成的表达式来计算值。注意的是，操作数也可以是另一个表达式。

## 数字数据类型

数字数据类型是一种原始数据类型，它在内部存储为浮点数，即 64 位双精度数字。这 64 位字段存储了符号、指数和分数。虽然最左边的位保留给符号，`0`到`51`位留用于存储分数，`52-62`位用于指数。

由于系统的内存限制，`253`是可以存储的最大整数。需要注意的是，整数计算会产生一个精确的值。然而，小数数据的计算可能会给出不精确的结果。因此，这些值必须被截断。

除了数字和字符串外，JavaScript 还支持使用以下特殊字符：

- `undefined`指定该值尚未赋值。
- `NaN`代表“不是数字”（Not a Number）。
- `-Infinity`任何小于`-1.7976931348623157E + 10308`的数字都用`Infinity`表示。
- `Infinity` - 任何超过值`1.7976931348623157E + 10308`的数字都用`Infinity`表示。

## 字符串数据类型

字符串可以简单地描述为字符的集合。当你在引号内声明字符时，系统会将其解释为字符串。示例字符串包括：

- ‘Hello World!’
- “Hello World!”

然而，如果你想在字符串中包含引号作为字符，则必须在字符前添加`\`。示例字符串：

- ‘You\’re Welcome’
- “You\’re Welcome”

JavaScript 还支持其他转义序列，如用于制表符的`\t`和用于换行的`\n`。

## 布尔数据类型

布尔数据类型是一种二进制类型，返回`true`或`false`。这些运算符通常用于指示比较的结果。例如，

`10 > 5`将得到‘true’而`5 > 10`将得到‘false’。

## 数字数据类型上的操作

为了进行计算，使用了运算符。JavaScript 支持所有基本运算符，运算符优先级如下：

- 加法和减法的优先级相同。
- 乘法和除法的优先级相同。
- 乘法和除法的优先级高于加法和减法。
- 如果一个表达式包含多个相同优先级的运算符，则表达式从左到右求值。

除了基本运算符，JavaScript 还支持取模（`%`）运算符。该运算符执行除法并将余数作为结果。例如，`23%7`等于`2`。

## 一元运算符

虽然加法和减法等运算符执行需要操作数，但某些运算符只需要一个。此类运算符的示例是`typeof`，它返回数据的类型。例如，`typeof 12`返回‘number’。请注意，`+`和`-`也可以用一元运算符。当它们被用于指定数字的符号时如此。

# 逻辑运算符

JavaScript 中提供了三个逻辑运算符，分别为非（`!`）、或（`||`）和与（`&&`）。涉及这些运算符的操作结果是布尔（`true`或`false`）。这些操作的结果根据以下规则计算：

| 运算符 | 类型 | 描述 |
| :--- | :--- | :--- |
| AND (`&&`) | 二元运算符 | 两个条件都必须为真 |
| OR (`||`) | 二元运算符 | 至少一个条件必须为真 |
| NOT (`!`) | 一元运算符 | 确定的条件值取反 |

例如：

- ‘Red’ != ‘Blue’ && 5 > 1 = ‘true’
- ‘Red’ != ‘Blue’ && 5 < 1 = ‘false’
- ‘Red’ == ‘Blue’ && 5 < 1 = ‘false’

对于条件运算符，JavaScript 使用短路求值。换句话说，如果第一个条件的值被计算为‘false’，系统将不会评估另一个条件并直接给出结果。

# 在 JavaScript 中编写代码

任何后跟分号的语句被称为语句。语句可能可能不产生值，而表达式必须产生值。

## 变量

数据的操纵通过变量完成。数据存储在内存中，对该内存位置的命名称为变量。任何标识符通过通过关键字`var`来声明。变量的一个示例是：

```
var result;
```

该语句声明了`result`。你也可以通过以下方式定义变量：

```javascript
var result = 0;
```

或者

```javascript
var result = 23*6;
```

命名变量时必须遵循某些规则。这些规则是：

- 变量名可以是数字和字符的组合。
- 变量名不能以数字开头。
- 变量中允许的特殊字符是下划线（`_`）和美元符号（`$`）。
- 变量名中不应有空格。例如，“result value”是不允许的。
- JavaScript 关键字是被保留的，不能使用。

请注意 JavaScript 与 HTML 大大小敏感。因此`VAL`和`val`是两个不同的变量。此外，建议变量名应该描述其用途。例如，如果我们把变量命名为`result`，显而易见该变量将包含代码计算的结果。

JavaScript 的另一种约定是命名变量时，变量名的首字母小写。然而，变量名中的后续每个单词都以大字母开头。这种方法的示例是变量名`arrayResult`。除此之外，不建议使用下划线和美元符号。然而，它们被用于 jQuery 对象。

## 环境

变量集合及其包含的值形成了所谓的环境。因此，每当你在浏览器中加载新网页时，你都在创建一个新环境。以 Windows 8 为例，当应用程序启动时它会创建一个环境，当应用程序结束时该环境会被销毁。

## 函数

一组解决特定目的的语句被称为函数。使用函数的目的是代码复用。如果你的程序在内部多次使用某项功能，则将其实现为函数，并在需要时调用。由于函数是从代码内部调用的，可以将参数从代码发送函数。执行后，函数将值返回给调用函数。函数声明和定义的语法如下：

```javascript
function multiply(a, b){
  return a*b;
}
```

函数名称之前必须始终带有`function`关键字。变量`a`和`b`是传入函数的参数，函数返回通过计算`a*b`得到的值。这是一个简单的函数，但你可以根据所需的功能来实现复杂且大型的函数。

既然你已经实现了该函数，你可能在好奇是如何调用该函数的。这里有一个示例：

```javascript
var x=2;
var y=5
var c=multiply(x, y);
```

在这里，`x`和`y`是函数`multiply`将作为参数接收的参数。

JavaScript 是一种弱类型语言。这意味着，如果你传递给函数的参数比它预期的多，系统将仅使用所需的前`n`个参数并丢弃其余部分。这种功能的优势是，你可以使用已经实现的函数，并传递额外的参数来扩展函数并为其添加功能（注：原文为`pass the extra argument to scale the function`，意为扩展函数规模）。另一方面，如果你无意中传递了错误数量的参数，你将无法获得任何错误提示。

JavaScript 还提供了一些与用户交互的内置函数。这些函数如下：

### `alert`
此函数会弹出一个带有消息的警报，在用户点击 OK 按钮后系统继续运行。示例实现：

```javascript
alert(‘Alert message!’);
```

### `prompt`
此函数会向用户显示一个文本框并要求其提供输入。你可以在显示的文本框中提供默认值，用户可以点击 OK 按钮以接受输入的内容是正确的。示例实现：

```javascript
var result = prompt(‘Enter a value’, ‘default value’);
```

### `confirm`
此消息允许用户选择确认或取消（CANCEL）操作。示例实现：

```javascript
var result = confirm(‘Do you wish to proceed?’);
```

## 函数作用域 (Function Scope)
你定义的每个变量都拥有一个操作范围，即该变量所在的函数。这被称为局部作用域。与许多语言通过变量所在的花括号来定义局部作用域不同，JavaScript 的局部作用域与函数作用域相同。

此外，JavaScript 还支持全局作用域的概念，在其中变量可以被声明为全局变量，因此可以在程序的任何地方使用。

## 嵌套函数 (Nesting Functions)
函数可以在任何级别进行嵌套。换句话说，可以在另一个函数内部调用一个函数，而该函数可能又是从另一个函数调用的。但重要的是，变量的作用域是在声明它的函数内部。

## 数据类型之间的转换 (Conversion of One Data Type to Another)
上一个函数中讨论`prompt`函数返回一个字符串。然而，你要求用户输入一个数字。在这种情况下，可能需要从字符串到数字的转换。在 JavaScript 中可以使用以下函数将变量从一种类型转换为另一种：

### `Number`函数
此函数将将其提供的对象转换为数字数据类型。然而，如果函数无法执行转换，则返回`NaN`。

### `String`函数
此函数将将其提供的对象转换为字符串数据类型。

## 条件编程 (Conditional Programming)
在编写代码时，你可能会遇到几种情况，即如果条件为真，则执行一组指令；如果条件为假，则执行另一组指令。

### `if-else`
为了实现此类场景，你可以使用`if-else`结构。

语法：
```javascript
if(condition)
{
//code
}
else
{
//code
}
```

考虑这样一种场景：你使用`prompt`函数要求用户输入年龄。现在，在对提供的值执行任何计算之前，你必须验证年龄是否为有效数字。这是实现条件编程的理想场景。该场景的示例实现如下：

```javascript
var userAge = prompt(‘Enter your age: ', ‘’);
if(isNaN(userAge))
{
alert(‘Age entered is invalid!’);
}
else
{
//code 
}
```

在此示例代码中，`if`检查输入的值是否为数字。如果条件为真（即输入的对象不是数字），则会给用户一个警报消息。然而，如果条件为假，则执行`else`的代码。

这里需要注意的是，对于单语句，没有必要使用花括号。上述代码也可以写成：

```javascript
var userAge = prompt(‘Enter your age: ', ‘’);
if(isNaN(userAge))
alert(‘Age entered is invalid!’);
else
//code 
```

然而，使用花括号是一个良好的习惯，因为留下了以后添加额外代码的空间。

### `if-else if`
另一种条件编程结构是`if-else if`结构。该结构允许你声明多个条件及其相关的操作。语法为：

```javascript
if(condition)
{
//code
}
else if(condition)
{
//code
}
else
{
//code
}
```

### `Switch`
可以使用此结构实现多个`else if`。这种条件编程结构的执行开销较高，因为条件会按顺序检查其有效性。作为替代方案，可以使用另一个关键字`switch`，它以跳转表的形式实现多个条件。因此，`switch`的执行开销小于`if-else if`。

示例实现：

```javascript
var userChoice = prompt('Choose an alphabet: a, b, c', 'e');
switch (userChoice) {
case 'a':
alert('a chosen\n');
break;
case 'b':
alert('b chosen\n');
break;
case 'c':
alert('c chosen\n');
break;
default:
alert('None of the alphabets chosen\n');
break;
};
```

`switch`将用户输入的值与 case 值进行匹配。如果找到了匹配的值，则执行该 case。然而，如果没有 case 值匹配输入，则执行`default`case。此外，你也可以在 case 中使用条件，并执行符合条件的 case。

如果你在 case 后不使用`break`语句，则后续的所有 case 都将被执行。例如，如果用户为上述示例输入了‘b’且没有 break 语句，输出将是：

b chosen
c chosen
None of the alphabets chosen

此外，在`default`case 中使用`break`语句也是良好的习惯。

注意：
如果你想确定一个关键字是否已赋值了值，可以使用以下代码：

```javascript
if(c)
{
//code
}
else
{
//code
}
```



如果变量`c`被赋值了非空值，则`if`条件为真并执行相应的代码。相反，如果变量`c`的值为`undefined`或`null`，则执行`else`结构中的代码。

**注意：** 以下条件的值始终为真：

```
'' == 0
null == undefined
'123' == 123
false == 0
```

请注意，`JavaScript`在比较时会转换相关变量的类型以进行兼容。

然而，如果你想比较两个变量的值和类型，`JavaScript`提供了另一组运算符`===`和`!==`。当使用此运算符对上述示例值进行比较时，结果始终为假。

## 实现循环（Implementing Code Loops）

循环是任何编程语言中重要且常用的结构。当你需要按照给定次数执行同一组指令时，你会遇到几种情况。为了实现这种场景，必须使用循环。`JavaScript`可用的循环结构包括`for`、`while`和`do-while`。

`while`循环包含一个条件，只要该条件保持真，循环就会继续执行。`do-while`循环是`while`循环的变体。如果`while`中的条件为假，则`while`循环将完全不执行。相反，即使`while`条件为假，`do-while`循环至少执行一次。

### while循环的语法

```
while(condition)
{
//code
}
```

### do-while循环的语法

```
do
{
//code
}
while(condition)
```

`JavaScript`中提供的最后一种类型的循环是`for`循环。`for`循环允许你在同一语句中初始化循环变量、检查条件并修改循环变量。

### for循环的语法

```javascript
for(initialize; condition; modify)
{
//code
}
```

### 示例代码

```javascript
for(i=0; i<10; i=i+1)
{
//code
}
```

此循环将运行 10 次。

**注意：**

1. 如果在任何时刻你希望跳出循环，可以使用`break`语句。
2. 如果你没有指定条件，或者指定了一个始终为真的条件，循环将无限运行。

## 错误处理

异常可能会在代码的多个层级上发生。因此，最好是实现一种可以帮助你处理这些异常并避免崩溃的机制。

异常可以被视为非法操作或任何意料之外且不寻常的情况。异常的几个示例包括未经授权的内存访问。

你可以在执行任何操作之前验证变量的值，在自己的层面进行异常处理。例如，在执行除法之前，建议检查分母的值是否为零。任何涉及数字除以零的操作都会抛出`divide-by-zero`异常。

然而，还有其他无法通过这种方式处理的情况。例如，如果网络连接突然中断，你无法采取任何措施预处理这种情况。因此，对于此类情况，使用了`try`、`catch`和`finally`关键字。

预期抛出异常的代码放在`try`块中。此异常一旦发生会被`catch`块捕获，该块执行在捕获异常后应该立即执行的代码。`catch`后面可能紧跟`finally`块，该块执行最后的清理。此块在执行`try`和`catch`块后执行。

### 错误处理语法

```
try
{
//code
}
catch(exception name)
{
//code
}
finally
{
//code
}
```

## 数组

连续的相似对象集合被称为`array`。该数组被赋予一个名称，可以使用以下形式的索引器访问每个元素：

假设`arrName[]`是一个名称数组。元素`arrName[2]`指数组的第三个元素。

可以使用以下三种方法创建数组：

### 使用索引器插入项

可以使用`new`关键字创建数组，然后通过给数组的独立元素赋值来向数组中添加元素。`new`关键字使用同名的构造函数创建`Array`对象的实例。

**示例实现：**

```javascript
var arrName = new Array();
arrName[0] = 'Jack';
arrName[1] = 'Alex';
```

### 紧凑数组

第二种实现也使用`new`关键字。但在这种情况下，值作为`Array`对象构造函数的参数传递给元素。

**示例实现：**

```javascript
var arrName = new Array('Jack', 'Alex');
```

### 字面量数组

在这种类型的数组定义中，值在方括号内提供。

**示例实现：**

```javascript
var arrName = ['Jack', 'Alex'];
```

使用第一种定义的优点是它允许你在代码的任何地方为元素赋值。相反，第二和第三种类型的实现要求你预先拥有准确的元素列表。

所有对象都关联属性。其中一个对你有用的属性是`length`，它是一个只读值，调用它时返回数组中存在的元素数量。你可以在循环和条件中使用此属性。

对象也可以有自己的函数。这些函数被称为方法。`Array`可用的方法包括：

- `concat`: 返回一个数组，它是所提供的两个数组的连接。
- `indexOf`: 找到数组中相关元素的位置并返回其索引。
- `join`: 该方法连接数组中存在的所有值。然而，默认所有这些值都用逗号分隔。你也可以指定自定义的分隔符。
- `lastIndexOf`: 该方法的作用与`indexOf`类似。但它从数组的最后一个元素开始搜索。因此，它返回匹配指定标准的最后一个元素的索引。
- `pop`: 移除最后一个元素并返回其值。
- `push`: 将元素添加到数组末尾并返回长度。
- `reverse`: 反转数组元素的顺序。该方法修改原始数组。
- `shift`: 移除第一个元素并返回其值。如果数组为空，则返回`undefined`。
- `slice`: 该方法需要两个参数，起始索引和结束索引。创建一个包含从起始索引到结束索引-1元素的新数组。
- `sort`: 该方法对元素进行排序并修改原始数组。
- `splice`: 该方法在指定的数组中删除并添加元素。该方法取的参数是起始索引（开始删除的位置）、要删除的数量以及要添加的元素。如果传递的删除数量为 0，则不删除任何元素。相反，如果此值大于数组大小，则从起始索引开始的所有元素都被删除。
- `toString`: 该方法创建一个字符串，它是数组中所有元素的逗号分隔字符串。
- `unshift`: 该方法在数组第一个位置添加元素并返回修改后的长度。
- `valueOf`: 该方法返回一个字符串，它是数组中所有元素的逗号分隔字符串。

**注意：**

1. 在与函数工作时，你可以传递整个数组（使用数组名称）或数组的特定元素（使用索引器）。
2. 可以访问索引器修改元素。例如，`arrName[1] = 'Danny';`将`'Danny'`赋给数组的第二个元素。

## DOM 对象

在构建应用程序时，你需要访问的主要对象是相关的`DOM`对象。这种访问对于你控制并获取网页发生的事件是必要的。

`DOM`是层次结构的表示。这些对象可以使用内置的`document`变量进行访问。该变量引用`DOM`并执行搜索，可能会返回活动或静态`NodeList`。

### DOM可用的搜索方法

- `getElementById`: 该方法返回具有指定 ID 的第一个元素的引用。
- `getElementsByTagName`: 此方法返回具有指定标签名的活跃`NodeList`。
- `getElementsByName`: 此方法返回具有指定名称的活跃`NodeList`。这是处理单选项按钮（option buttons）的首选方法。
- `getElementsByClass`: 此方法返回具有指定类名的活跃`NodeList`。然而，该方法不支持 Internet Explorer 8 及更早版本。
- `querySelector`: 此方法接受 CSS 选择器作为参数，并返回第一个匹配的元素。然而，该方法不支持 Internet Explorer 7 及更早版本。
- `querySelectorAll`: 此方法接受 CSS 选择器作为参数，并返回所有匹配的元素。因此，它返回的是一个静态的`NodeList`。然而，该方法不支持 Internet Explorer 7 及更早版本。

## 事件

如果你将`JavaScript`看作一个引擎，那么事件就是为它提供运行所需的火花。事件可能发生在两种情况下。第一类事件是在用户交互期间发生的事件。用户可能会点击图像或输入文本。所有这些都被归类为事件。除此之外，系统状态的变化也被视为事件。例如，如果视频开始或停止，就说发生了一个事件。`DOM`允许你捕获事件并执行相应的代码。

在`JavaScript`中，事件基于发布-订阅方法论。在创建对象时，开发者可以发布与该对象相关的事件。此外，每当使用该对象时，都可以向该对象添加事件处理程序。事件处理程序函数会通知订阅的事件事件已触发。此通知包含了有关事件的信息，如鼠标位置和按键按下，以及与事件相关的其他细节。

### 捕获事件

在某些情况下，事件可能会绑定到按钮点击上，而该按钮可能位于超链接内部。在这种情况下，元素存在嵌套。因此，当事件触发时，它沿着`DOM`层次结构向下传递。这个过程被称为事件捕获（event capturing）。然而，一旦事件到达元素，它就会向上层次冒泡。这个过程被称为事件冒泡（event bubbling）。事件在层次结构中的移动为开发者提供了根据需要订阅或取消传播的机会。

### 订阅事件

可以使用`addEventListener`函数进行订阅过程。该函数需要三个参数：`event`、事件触发时需要调用的函数，以及一个决定函数在捕获或冒泡过程中是否被调用的布尔值（`true`–捕获，`false`–冒泡）。通常，此值设置为`false`。正如 W3C 标准中提到的，这是订阅的首选方法。

**示例代码：**

```javascript
var btn = document.getElementById('btnDownload');
btn.addEventListener('click', initiateDownload, false);
```

然而，也存在其他方法，包括为`html`标签提供在线订阅。这会将事件订阅到冒泡过程中。使用这种方法的优点是它是最古老且最广泛接受的方法。因此，你可以确定无论使用何种浏览器，这种方法都将有效。请查看下方的标签以了解如何实现此。

```html
<button id='btnDownload' onclick='initiateDownload();' >Download</button>
```

你也可以使用传统的订阅过程，通过`JavaScript`来订阅事件。

```javascript
var btn = document.getElementById('btnDownload');
btn.onclick = initiateDownload;
```

### 取消订阅

可以使用`removeEventListener`函数取消订阅，该函数接受与`addEventListener`相同的参数集。对于上一个示例中使用的`btn`变量，可以通过如下方式进行：

```javascript
var btn = document.getElementById('btnDownload');
btn.removeEventListener('click', initiateDownload, false);
```

### 如何取消传播？

使用`stopPropagation`函数执行此操作。可以通过如下方式实现：

```javascript
var btn = document.getElementById('btnDownload');
btn.addEventListener('click', initiateDownload, false);

function initiateDownload (e){
//download
e.stopPropagation();
}
```

### 如何阻止默认操作？

可以通过如下方式使用`preventDefault`函数来实现：

```javascript
var hyperlink = document.getElementById('linkSave');
hyperlink.addEventListener('click', saveData, false);

function saveData(e){
//save data
e.preventDefault();
}
```

`JavaScript`还提供了`this`关键字，如果你希望频繁访问触发事件的元素，则可以使用它。

## 窗口事件参考

当前浏览器窗口由`window`变量表示，它是`Window`对象的实例。以下事件与此对象相关联：

- `afterprint`
- `beforeonload`
- `beforeprint`
- `error`
- `blur`
- `haschange`
- `load`
- `message`
- `focus`
- `online`
- `offline`
- `pageshow`
- `pagehide`
- `redo`
- `popstate`
- `storage`
- `resize`
- `unload`
- `undo`

## 表单事件参考

在`HTML`表单内部发生的动作会触发以下事件：

- `change`
- `blur`
- `focus`
- `contextmenu`
- `forminput`
- `formchange`
- `invalid`
- `input`
- `submit`
- `select`

## 键盘事件参考

键盘触发以下事件：

- `keyup`
- `keypress`
- `keydown`

## 鼠标事件参考

鼠标触发以下事件：

- `click`
- `drag`
- `drop`
- `scroll`
- `dblclick`
- `dragenter`
- `dragstart`
- `dragend`
- `dragover`
- `dragleave`
- `mousemove`
- `mousedown`
- `mouseover`
- `mouseout`
- `mousewheel`
- `mouseup`

## 媒体事件参考

视频、音频等媒体元素也会触发以下事件：

- `canplay`
- `abort`
- `waiting`
- `durationchange`
- `canplaythrough`
- `ended`
- `emptied`
- `loadeddata`
- `error`
- `loadstart`
- `loadedmetadata`
- `play`
- `pause`
- `progress`
- `playing`
- `readyState`
- `ratechange`
- `seeking`
- `seeked`
- `suspend`
- `stalled`
- `volumechange`
- `timeupdate`

## CSS 基础

层叠样式表`CSS`提供了网页为人知的呈现效果。尽管`HTML`能够为网页提供基础结构，但`CSS`为开发者提供了大量的样式选择。此外，它快速且高效，这使其成为更受欢迎的设计工具。

`CSS`已知演变自`SGML`（标准化通用标记语言）。这些努力的目标是标准化网页的外观。该技术的最新版本是`CSS3`，它是 50 个模块的集合。

`CSS`最强大的特性是它的层叠能力。简单来说，它允许网页从多个样式表中获取样式，使得后续读取的表中的样式会覆盖从一个或多个之前的表中实现的样式。

### 如何定义和应用样式

样式的定义和应用涉及两个方面或部分：选择器和声明。选择器确定了需要样式的网页区域，而声明块描述了必须实现的样式规范。为了说明其工作原理，让我们考虑以下示例：

```css
body {
  color: white;
}
```

在这个示例中，选择器选择了网页的`body`，声明块定义了字体颜色改为白色。这是一个简单的示例，声明和选择器可以比这复杂得多。

### 如何添加注释

可以使用以下格式在样式表中添加注释：

```css
/*在此处编写注释*/
```

### 如何创建内联样式

每个元素都有一个关联的全局属性`style`。该全局属性可以在该元素的标签内进行操作，以修改该元素的外观。这种类型的样式不需要你指定选择器。只需要声明块即可。下面是这种操作方式的示例：

```html
<body style='color: white;'>
</body>
```

此 HTML 标签执行的功能与上一节中指定的 CSS 代码相同。使用这种方法的优处是，通过这种方式给出的样式信息会覆盖任何其他样式信息。因此，如果你需要为一个元素使用不同的样式，而文档的其他部分需要遵循不同的样式，那么你可以为文档使用样式表，并在其标签中为该元素指定样式。

### 如何使用嵌入式样式

实现与内联样式相同结果的另一种方法是在相关的元素内部使用`<style>`元素，用于定义其样式规范。以下是具体的实现方法：

```html
<!DOCTYPE html>
<html xmlns='http://www.w3.org/1999/xhtml'>
<head>
<title></title>
<style>
body {
color: white;
}
</style>
</head>
<body>
</body>
</html>
```



## 如何创建外部样式表

对于希望为整个网页或多个网页使用相同样式的情况，最佳方法是使用外部样式表。该外部样式表可以通过如下方式链接到 HTML 页面：

```html
<!DOCTYPE html>
<html xmlns='http://www.w3.org/1999/xhtml'>
<head>
<title></title>
<link rel='stylesheet' type='text/css' href='Content/mainstyle.css' />
</head>
<body>
</body>
</html>
```

你必须在`Content`文件夹中创建一个名为`mainstyle.css`的文件，并将指定的样式规则放入该文件中：

```css
body {
color: white;
}
```

## 定义媒体

需要注意的是，样式表可以包含你想要的任意数量的样式规则。除此，你还可以为不同的媒体链接不同的 CSS 文件。不同的媒体类型如下：

- `all`
- `embossed`
- `braille`
- `print`
- `handheld`
- `speech`
- `screen`
- `tv`
- `tty`

所使用的媒体可以通过以下方式定义：

```html
<link rel='stylesheet' type='text/css' href='Content/all.css' media='all' />
```

## 定义字符编码

你也可以使用以下格式定义所使用的字符编码：

**样式表：**
在样式表中的样式规则上方放置此行。

```css
@charset 'UTF-8';
```

**HTML 页面：**
你必须将此行放在`link`元素上方。

```html
<meta http-equiv='Content-Type' content='text/html;charset=UTF-8' >
```

## 导入样式表

随着你的网页变得复杂，所使用的样式表也会变得复杂。因此，你可能需要使用许多样式表。你可以使用以下方式将一个样式表中的样式规则导入到另一个样式表中：

```css
@import url('/Content/header.css');
```

在这里，导入了`header.css`，`url`提供了要导入的样式表的相对地址。

## 字体字体

可以使用以下格式导入字体：

```css
@font-face {
font-family: newFont;
src: url('New_Font.ttf'),
url('New_Font.eot'); /* IE9 */
}
```

## 选择器、优先级与级联

选择器有三种类型：类选择器、ID 选择器和元素选择器。元素选择器类型最简单，只需要命名需要使用的元素即可。例如，如果你想更改`body`的背景颜色，那么使用的元素选择器就是`body`。

在声明任何元素时，你可以使用`id`属性为其分配一个 ID。你可以使用以`#`开头的 ID 作为选择器。例如，如果你创建了一个 ID 为`btnID`的按钮，那么该按钮的 ID 选择器就是`#btnID`。同样，你可以使用`class`属性为元素分配一个类名。类名可以如下所示通过`.className`使用，即以点（`.`）前缀。

然而，如果你想选择网页上的所有元素，则对其使用星号（`*`）。

## 使用后代选择器和子元素选择器

你可能希望为选择器的后代应用特定的样式。这可以通过指定完整的选择器链来实现。实现方式如下：

```css
li a {
text-color: black;
}
```

另一方面，你可能只想在元素是选择器的直接子元素时对其应用样式。这可以通过指定用大于符号（`>`）分隔的父元素来实现，实现方式如下：

```css
li > a {
color: white;
}
```

## 伪元素和伪类选择器

现在你已经知道如何对特定元素应用样式，让我们继续为更具体的部分实现样式，例如第二个段落的第一行。为了给无法根据名称、内容分类或不是 DOM 树一部分的元素设置样式，可以使用伪类。可用的伪类包括：

- `:visited`
- `:link`
- `:hover`
- `:active`
- `:checked`
- `:focus`
- `:nth-child(n)`
- `:not`
- `:only-child`
- `:nth-child(formula)`
- `:lang(language)`
- `:first-of-type`
- `:only-of-type`

想要访问 DOM 树中特定的信息，可以使用伪元素。伪元素包括：

- `::first-letter`
- `::first-line`
- `::after`
- `::before`

## 分组选择器

多个选择器可以用于样式。这些选择器必须用逗号隔开。示例：

```css
body, button {
color: white;
}
```

## 使用相邻选择器

如果你想设置`div`的第一个相邻元素，选择器是在两个选择器之间使用加号（`+`）。示例：

```css
div + h1 {
color: white;
}
```

## 兄弟选择器

兄弟选择器与相邻选择器相似，不同在于它们会设置所有匹配的元素，而相邻选择器只设置第一个匹配的元素。示例：

```css
div ~ h1 {
color: white;
}
```

## 使用属性选择器

此选择器选择所有具有指定属性的元素。格式如下：

`a[title]`

此选择器将选择所有带有`title`属性的链接。此外，可以通过指定属性值将这种选择器修改为属性值选择器：

`a[title = value]`

## 器的内置样式

每个浏览器都有一个内置样式表，它应用于所有网页。事实上，该样式表在任何其他样式表之前应用。你可以通过工具中的辅助选项为浏览器定义自己的样式表。然而，用户样式表是针对特定的。因此，如果你打开另一个浏览器，你定义的样式表可能无效。

情况下，如果你希望你的自定义样式表覆盖 HTML 页面中的任何其他样式，你可以使用`!important`修饰符。该修饰符为指定的样式设置最高优先级。示例：

```css
body {
color: white !important;
}
```

## 样式的级联

样式的优先级和顺序根据以下参数决定：

- 重要性
- 优先级
- 文本顺序

## 现在你已经熟悉了选择器的使用，下一步是查看 CSS 属性。

## 颜色

网页中最重要的属性之一是颜色，它可以使用 ARGB、RGB 和颜色名称定义。RGB 值通常使用 0-255 之间的十进制数。

- `white` `#ffffff`
- `red` `#ff0000`
- `black` `#000000`
- `green` `#008000`

可以使用颜色值代替颜色名称。这种用法的示例如下：

```css
body {
color: #ffffff;
}
```

另一种指定颜色的方法是使用`rgb`函数，它使用 0-255 之间的数字或百分比来指定参数值。此类类型的声明示例所示：

```css
h1 { color: rgb(255,0,0); }
```

指定颜色的其他方法还有`RGBA`（接受 4 个值）和`HSL`（定义了色相、饱和度和亮度的值）。

## 透明度
透明度或不透明度由`0.0`（透明）到`1.0`（不透明）之间的值定义。

## 文本
对于文本，可以指定`font-face`和`font-size`。这些属性可以按以下方式定义：

```css
h1 { font-family: arial, verdana, sans-serif; }
h1 { font-size: 12px; }
```

## CSS 盒模型
`CSS Box Model`假设网页可以认为是由盒子组成的。这些盒子之间的间距由`margins`（外边距）和`padding`（内边距）设置决定。这些属性可以通过以下方式赋值：

```css
margin: 15px;
padding: 25px;
border: 10px;
```

## 定位 `<div>` 元素
用于创建页面布局的元素是`<div>`。虽然 HTML5 建议使用语义化标记代替`div`元素，但它们仍然用于无法使用语义化标记样式的内容。`div`元素可以被想象为一个矩形块，并按以下方式声明：

```html
<div>
<!--其他元素包含在这一区域内-->
</div>
```

用于定义`div`元素位置的属性包括：
- 可以使用像素单位的`top`、`bottom`、`left`和`right`属性定义`div`元素的位置。
- 使用`position`属性定义指定的指定是静态（`static`）还是相对（`relative`）。
- `float`属性可以允许元素浮向右侧或左侧，定义为`float: left`或`float: right`。
- `clear`属性在浮动元素之后放置一个清除元素。
- 你还可以通过`box-sizing`属性更改浏览器计算宽度的方式。该属性可以取三个值：`content-box`（默认设置）、`border-box`和`padding-box`。

### 居中内容
如果你使用固定宽度，可以使用`margin-left`和`margin-right`属性使`div`元素居中。如果你固定宽度并将边距设置为`auto`，边距上的额外空间将平均平分。可以通过以下方式实现：

```css
#container {
width: 850px;
margin-left: auto;
margin-right: auto;
}
```

## 第 5 章：HTML5 详解
本章专注于 HTML5 的基础知识以及如何使用它们来创建高性能的新一代页面。然而，该章解释的大多数元素包含了 HTML5 从其前身中继承的元素。本章将在你学习 HTML5 的道路上更进一步，引入了这项技术中新增的概念。

在上一章关于 CSS 的章节中，我们为你引入了`<div>`元素的概念。在创建页面布局方面，该元素优于所有的替代方案。虽然有些人人也使用`<table>`元素，但它通常不是推荐的解决方案，因为它难以维护和使用。不过，这两个概念在本章中都将详细阐述。

## 语义化标记
`<div>`和`<span>`元素是定位和格式化内容常用且推荐的元素。然而，建议你应该使用不同的`<div>`元素来指定页面的不同部分，如页眉（`header`）和页脚（`footer`）。这将允许你以更有组织的方式单独对它们进行定位。因此，W3C 为这些新元素命名为`<footer>`和`<header>`等名称。

## 浏览器支持
确实，你的 HTML 代码不会被你的任何用户读取。但是，还有其他工具和机器在不断解析你的代码。这些工具包括用于搜索索引网页的网页爬虫，以及`NVDA`（非视觉桌面访问）设备，许多有特殊需求的用户将其作为阅读和理解网页的替代方案。因此，它们要求你使用易于理解的标签。

### 如何创建 HTML5 文档
尽管上面的讨论明确提到了使用有意义标签的重要性，并禁止使用`<div>`和`<span>`等标签，但你可能仍然为了样式目的而使用它们。随着阅读，你会发现必须提供语义化标签来为你的标签提供含义。这里需要提到的是，应该谨慎使用语义化标签，如果你发现有定义自定义元素的需要，那么尽管使用`<div>`和`<span>`元素即可。但是，请务必为尽可能描述其含义的元素添加`ID`和`class-name`。

### 如何创建 HTML5 布局容器
布局容器，顾其实名，是一个包含页面布局的容器。换句话说，容器包含了布局的不同部分或其子元素，使得它们能够以灵活的方式进行定位。作为开发者，你可以根据类名和`ID`轻松地区分`<div>`元素。然而，对于浏览器来说并非如此。

因此，必须有一种方法让你请求浏览器解释元素。例如，你可能想让浏览器关注某个`<div>`元素。所有及更多内容可以通过布局容器来实现，以一种浏览器和用户都能理解的方式表达元素。

创建布局容器的常用元素包括：
- `<header>`：用于定义文档的页眉部分或顶部部分。该元素也可以定义在`<article>`内部。
- `<footer>`：用于定义文档的页脚部分或最底部部分。该元素也可以定义在`<article>`内部。
- `<nav>`：用于用于定义包含所有导航链接的部分。
- `<aside>`：该元素通常用于侧边栏，并将`<aside>`元素之外的内容与其隔离开。
- `<section>`：该元素定义整个区域的一部分，并用`<h1>`、`<h2>`、`<h3>`、`<h4>`、`<h5>`和`<h6>`命名。
- `<article>`：该元素定义了一个完整的内容单元，你可以将其从一个位置复制到另一个位置。此类单元的示例是博客文章。

## 使用角色 (Roles)
`role`属性可以在在`<div>`和`<aside>`元素内部。角色层级以及为了可访问性提供特定含义的角色在`WAI-ARIA`（Web 可访问倡议 - 富功能互联网应用程序）中定义。

父角色类之一是地标角色（`landmark`），它定义了网页上的导航地标。父角色类包括：
- `banner`：定义在不同网页之间不会变化的网站特定内容，如页眉。
- `application`：定义指定区域为网络应用程序。
- `contentinfo`：定义包含关于网页的信息，如版权信息。这些信息大部分是页脚内容的一部分。
- `complementary`：定义即使脱离页面时也有意义的页面部分。
- `main`：使用该子角色类定义主网页主要内容。
- `form`：定义预期接收网页输入的区域。
- `search`：该子角色类用于定义网页上用于从用户获取搜索查询并显示结果的位置。
- `navigation`：包含导航链接的区域是该子角色类的一部分。

这些角色可以用于提供语义。然而，HTML5 包含的新元素本身就具有语义化。尽管如此，HTML5 并没有提供某些实用工具，对于这些工具，可以使用`role`属性。

### 如何使用 `<div>` 元素控制格式？

如前所述，`<div>`元素本质上是不可见的，并且不为元素提供任何语义。然而，如果你只想将其用于格式化目的，那么它是实现此目的的完美选择。

### 如何添加主题分隔符？

可以使用空元素元素`<hr/>`来添加主题分隔符，它用于表示从一组内容到另一组内容的过渡。

### 如何对内容进行注释？

有几个元素可用于注释。这些包括你已经使用了多年的`<b>`和`<i>`。然而，除了它们所表示的样式之外，它们现在有了新的含义。例如，`<b>`元素表示“粗体”样式。此外，HTML5 增加了“对特定文本有特殊关注，但没有改变其语气、重要性水平或隐含意义”的含义。

虽然在 particular 语境下使用粗体样式更有意义，但你仍然可以使用该元素来表示评论中的产品名称或关键词。同样，`<strong>`元素指示内容的相对重要性，而`<i>`表示所涉及内容的语气或隐含意义的变化。此外，`<em>`元素用于读者将交替读读的文本。

### 如何使用 `<abbr>` 处理缩写词和缩略？

在 HTML 的之前的版本中，`<acronym>`元素用于此目的。然而，该元素已过时，用于此目的的新元素是`<abbr>`。它是一个内联元素，通常与`<em>`和`<strong>`等其他内联元素配合使用。

### 元素 - `<address>`

该元素用于定义网页所有者或作者的联系信息。

### 引用和引用

你可以使用`<blockquote>`元素表示特定文本是引用，它用于长引用；而`<q>`元素用于行内引用。你可以使用`cite`属性或`<cite>`元素提到引用的来源。然而，在`<q>`和`<blockquote>`元素内部使用`<cite>`元素被认为是更好的方法。请记住，`<cite>`元素只能提到作品名称，不包含作者名和出版地等其他信息元素。

### 如何在 HTML5 中记录代码？

有两个元素`<code>`和`<samp>`用于记录代码。`<code>`元素用于记录源代码，而`<sample>`元素用于代码的输出。下面提供了一个如何操作的 HTML 示例：

```html
<code class="maintainWhiteSpace">
echoContent('Screen');
function echoContent(name)
{
alert('This is' + name + '.');
}
</code>
<samp class="maintainWhiteSpace">
This is Screen.
</samp>
```

## `<pre>` 元素

这里需要说明的是，这些元素不会保留空格。因此，需要为此目的实现一个类。该类应该如下：

```css
style rule.
.maintainWhiteSpace {
white-space: pre;
}
```

某些浏览器可能不支持此样式规则。因此，对于此类浏览器，建议使用`<pre>`元素。因此，`<pre>`元素可以用于定义预格式规则。

## `<var>` 元素

该元素用于声明内部指定的文本是一个变量。示例：

```html
<p>
变量 <var>i</var> 代表循环执行的迭代次数。
</p>
```



## `<br />` 和 `<wbr />` 元素

`<br/>` 元素实现换行。另一方面，`<wbr/>` 实现换词。

## `<dfn>` 元素

有时你可能想要定义一个术语。可以使用 `<dfn>` 元素来实现，它接受标题作为其属性之一。

## 使用图表

图像和插图是任何网页内容的不可或缺的一部分。因此，每个图表也可以视为一个内容单元，它可能由标题和指向其所属页面的引用组成。为了定义一个或多个图像，使用了 `<figure>` 元素。`<figcaption>` 元素可以用于定义图片的标题。

然而，这里需要说明的是，`<figure>` 元素并没有赋予图片位置任何重要性，该位置与内容一起包含。然而，如果图片的位置和所在对你很重要，那么你必须考虑使用 `<div>` 元素。

## `<summary>` 和 `<details>` 元素

`<summary>` 元素包含网页内容的摘要，可以使用 `<details>` 元素以折叠列表的形式显示。因此，当你加载页面时，只会显示 `<summary>` 元素的内容，而当用户点击摘要时，会显示 `<details>` 元素的内容。

## 其他注释

除了上述提到的，还有几个可用的注释，包括：

* `<s>` - 用于删除线文本
* `<u>` - 用于下划线文本
* `<mark>` - 用于高亮文本
* `<ins>` - 用于指示文本已插入
* `<del>` - 用于指示文本已删除
* `<small>` - 用于指示文本必须以较小字体打印
* `<sub>` - 表示文本是下标
* `<sup>` - 表明文本是上标
* `<time>` - 用于指示文本表示时间和日期
* `<kbd>` - 用于指示文本是用户输入

## 语言元素

你可能需要在文本中使用源自中文、日语或韩语的字符。为了支持这种包含，可以使用 `<ruby>` 元素。在该元素内部，其他元素如 `<bdi>` 和 `<bdo>` 用于定义文本的隔离和方向。此外，`<rt>` 和 `<rp>` 元素也可以在 `<ruby>` 元素的文本中放置注释或括号。

## 使用列表

在 HTML 中，有几种元素用于定义无序列表、有序列表和描述列表。还存在第四类“自定义列表”，允许开发者进行自定义。所有这些列表的项目都使用 `<li>` 元素声明。此外，所有类型的列表都支持嵌套。

### 有序列表

有序列表使用 `<ol>` 元素声明，列表元素的“顺序”是通过对包含的元素自动编号来实现的。有序列表使用的属性包括：

* `start` - 用于设置列表的起始数字
* `reversed` - 用于声明列表是否按升序或降序排列
* `type` - 用于声明列表类型，可以是 A, a, 1 或 I。

### 无序列表

这种类型的列表使用 `<ul>` 元素声明，情况下元素没有编号。列表元素简单地表示为项目符号。

#### 描述列表

这种类型的列表使用 `<dl>` 元素声明。使用该元素，你可以提供包含零或多个术语的描述。此外，列表元素使用 `<dt>` 元素声明术语，使用 `<dd>` 元素给出术语的描述。

### 自定义列表

开发者可以使用 CSS 样式创建自定义列表。在这种情况下，可以为嵌套列表的每一层创建不同的样式规则。

## 使用表格

网页中安排和数据的另一种格式是表格。表格使用 `<table>` 元素声明，并以行-列的形式表示数据。表格的单元格使用 `<tr>` 和 `<td>` 元素定义。虽然 `<tr>` 用于行，而 `<td>` 用于列。

尽管 HTML5 表格是开发者可以使用的最强大的结构之一，但理解在何时以及如何最合适地使用表格至关重要。以下是不应该使用表格的原因：

- 为网页创建的表格在读取到 `</table>` 标签之前不会进行渲染。相反，如果使用 `<<div>>` 元素创建相同的结构，内容将在读取时立即进行渲染。
- 表格极难维护。
- 表格对于辅助功能设备来说难以解析。

### 示例实现

```html
<table>
<tr>
<td>Frank</td>
<td>1978</td>
</tr>
<tr>
<td>David</td>
<td>1967</td>
</tr>
<tr>
<td>Alex</td>
<td>1989</td>
</tr>
</table>
```

上面创建的表格看起来像这样：

| Frank | 1978 |
| David | 1967 |
| Alex | 1989 |

当你观察这个表格时，你一定已经意识到，如果不定义所谓的“表头（table headers）”，表格是不完整的。这可以使用 `<th>` 元素来实现。你可以同时创建垂直和水平的表头。例如，我们可以在上面使用的代码中定义以下表头：

```html
<table>
<tr>
<th>Name</th>
<th>Year of Birth</th>
</tr>
<tr>
<td>Franky</td>
<td>1978</td>
</tr>
<tr>
<td>David</td>
<td>1967</td>
</tr>
<tr>
<td>Alex</td>
<td>1989</td>
</tr>
</table>
```

此代码生成的表格将如下所示：

| Name | Year of Birth |
| Franky | 1978 |
| David | 1967 |
| Alex | 1989 |

在上面的案例中，表头仅仅是使用了更大的字体。然而，你可以通过样式规则按照你的想法对这些进行样式设置。可以通过如下实现：

```css
th {
  background-color: black;
  color: white
}
```

此样式规则将表格表头的单元格涂为黑色，并将文本写为白色。

大多数浏览器的默认行为是将所有 `<tr>` 元素自动放在 `<tbody>` 中，表示这是表格的主体。然而，显式定义 `<tbody>` 是一种良好的做法。此外，还可以显式地定义 `<thead>` 和 `<tfoot>`。可以使用 CSS 分别地对表格的头部、主体和页脚进行样式设置。按照规定，你可以有一个头部元素、一个或多个主体元素和一个页脚元素。

上面创建的表格必须添加的下一个重要内容特性是表格标题（table caption）。为了定义表格标题，使用了 `<caption>` 元素。

在某些情况下，你可能觉得需要对单独列进行样式设置。考虑到表格在 HTML 中本质上是以行为中心的，这似乎是一项困难的任务。虽然你有 `<tr>` 元素来识别行，但没有用于识别列的 `<tc>` 元素。`<td>` 元素识别单元格。然而，你仍然可以使用 `<colgroup>` 或 `<col>` 元素对单独列进行样式设置。`<table>` 元素可以包含 `<colgroup>` 元素，它包含了用于该组元素中某些列的 `<col>` 元素。此外，`<col>` 元素还具有 `span` 属性，用于定义属于该组的列。下面提供了一个示例实现，以解释它是如何运作的：

```html
<colgroup>
  <col span="2" class="vHeader" />
</colgroup>
```

用于为这组列设置样式的 CSS 样式规则可能如下所示：

```css
.vHeader {
  color: red;
}
```

虽然目前讨论的表格是普通表格，但 HTML5 也支持不规则表格，这可以描述为每行的列数不同的表格。`rowspan` 和 `colspan` 属性可以用于管理表格的布局。

# 第 6 章：JavaScript 和 jQuery

你一定已经习惯了 JavaScript 的威力。在 JavaScript 章节中，你已经学习了如何创建和添加 JavaScript 来使网页动态化。Web 开发最大的挑战是设计网页元素，让它们在任何浏览器上运行得良好，因为不同的浏览器对不同元素的支持不同，这使得寻找共同点变得困难。

本章将在 JavaScript 开发方面带你更进一步，教你如何创建对象并使用它们。此外，它还向你介绍了 jQuery 的概念，它试图创建浏览器兼容的代码。虽然它不能保证 100% 的浏览器兼容性，但它确实解决了这方面的日常问题。

## 如何创建 JavaScript 对象

从数字到字符串，JavaScript 中的任何内容都是对象。因此，了解如何有效地创建和处理这些对象是重要的。在 JavaScript 中创建对象的简单的方法是使用对象字面量语法。下面的示例说明了如何操作。

```javascript
var customer1 = {
  yearOfBirth: 2000,
  name: 'Alex',
  getCustomerInfo: function () {
    return 'Customer: ' + this.name + ' ' + this.yearOfBirth;
  }
};
```

这段代码创建了一个对象 `customer1`，拥有数据成员 `name` 和 `yearOfBirth` 以及成员函数 `getCustomerInfo`。

另一种创建对象的方法是使用函数：

```javascript
function getCustomer(myName, myYearBirth) {
  var newCust = new Object();
  newCust.name = myName;
  newCust.yearOfBirth = myYearBirth;
  newCust.getCustomerInfo = function () {
    return 'Customer: ' + this.name + ' ' + this.yearOfBirth;
  };
  return newCust;
}

var cust1 = getCustomer('Alex', 1978);
var cust2 = getCustomer('David', 1986);
```

虽然 JavaScript 不支持特定的 `class`，但你可以使用上述方法模拟类。

## 命名空间

实现命名空间没有特定的关键字。然而，可以使用类和对象的概念来实现命名空间。如果你将变量和方法归类到对象中并作为这些对象的实例进行访问，那么你只需将这些对象的名称放在全局命名空间中，从而将变量的作用范围缩小。

### 实现继承

你可以通过创建对象并根据共同特征对对象进行归类，在 JavaScript 中定义对象之间的继承关系。例如，如果你正在实现一个公司的员工对象。你可以为特定类型的对象创建对象，如 `managerTechnical`、`managerGeneral`、`technicalStaff`、`recruitmentStaff` 和 `officeStaff`，然后将它们归类为对象：`technicalStaff` 包括 `managerTechnical` 和 `technicalStaff`，而 `adminStaff` 包括 `managerGeneral`、`recruitmentStaff` 和 `officeStaff`。同样，也可以定义新函数。

- `CSS Methods`（CSS 方法）用于获取和设置 CSS 相关属性的方法。
- `Dimensions`（尺寸）用于访问和操作 DOM 元素尺寸的方法。
- `Deferred object`（延迟对象）能够注册多个回调函数，同时维护状态更改的数据并将其从一个回调传递到下一个回调。
- `Forms`（表单）用于控制表单相关控件的方法。
- `Traversing`（遍历）这是一组提供 DOM 遍历支持的方法。
- `Effects`（效果）用于为网页创建动画的方法。`Events`（事件）用于执行基于事件的操作的方法。
- `Selectors`（选择器）用于通过 CSS 选择器访问 DOM 元素的方法。
- `Offset`（偏移）用于定位 DOM 元素的方法。
- `Utilities`（工具）是一组工具方法。

在使用 `jQuery` 之前，你需要将其引入到项目中。一旦你安装了它并准备好将其用于项目，下一步就是学习如何使用它。

首先，你需要在按以下方式在需要它的网页上引用 `jQuery` 库：

```html
<script type="text/javascript" src="Scripts/qunit.js"></script>
<script src="Scripts/jquery-1.8.2.js"></script>
```

接下来需要知道的是你希望在 HTML 页面中使用的 `jQuery` 代码位于 `jQuery` 命名空间，其别名为 `$`。因此，在引用 `jQuery` 的功能时，你可以写 `jQuery.jFeature` 或 `$.jFeature`。

在开始在网页中使用它之前，你还需要按照如下方式更改 `default.js` 文件：

```javascript
function initialize() {
  txtInput = $('#txtInput');
  txtResult = $('#txtResult');
  clear();
}
```

这允许你通过匹配它们的 ID 来使用 `jQuery` 和 `CSS 选择器`。

此外，当你继续使用 `jQuery` 进行编码时，记住在进行任何更改后使用 `Ctrl+F5` 刷新屏幕，因为浏览器可能无法立即捕获 JavaScript 的修改。此外，尽可能使用 `jQuery` 对象，因为它们提供了跨浏览器兼容性。

可以通过以下方式从 `jQuery wrapper` 引用 DOM 对象：

```javascript
var domElement = $('#txtInput')[0];
```

这是一个在引用元素之前检查该元素是否存在的简单代码。

```javascript
var domElement;
if($('#txtInput').length > 0){
  domElement = $('#txtInput')[0];
}
```

## 如何创建用于引用 DOM 元素的 jQuery wrapper

可以通过以下方式从 DOM 元素引用创建 `jQuery wrapper`：

```javascript
var myDoc = $(document);
var inText = $(this).text();
```

第一条语句将封装的对象赋值给变量。另一方面，第二个语句封装了使用 `this` 引用的对象。

## 如何添加事件监听器

`jQuery` 提供了 `.on` 方法来订阅事件。此外，你可以使用 `.off` 方法取消订阅。这些方法可以使用如下方式：

```javascript
$('#btnSubmitInfo').on('click', onSubmit);
$('#btnSubmitInfo').off('click', onSubmit);
```

### 如何触发事件处理器

`jQuery` 提供了触发器或 `triggerHandler` 方法来触发事件处理器或处理器代码的执行。可以通过以下方式实现：

```javascript
$('#btnSubmitInfo').triggerHandler('click');
```

## 初始化代码

你经常会面临在加载 HTML 文档时运行初始化代码的需求。你可以通过以下方式使用 `jQuery` 实现：

```html
<script>
$(document).ready(function () {
  initializationFunction();
});
</script>
```

这可以放在 HTML 文档的底部。它将调用 `initializationFunction`。

# 第 7 章：表单

在之前的章节中，你已经学习了如何创建和操作 HTML 文档。为基础，我们现在可以学习表单，它是网页开发中最关键且常用的内容单元之一。

简单来说，表单是一种收集数据并将其发送到处理位置的方法（大多数情况下是服务器）。然而，由于我们还没有讨论服务器端脚本，我们将重点关注将数据发送到电子邮件地址。但需要注意的是，我们不建议这种做法，它仅用于理解目的。

## Web 通信

在处理表单工作之前，了解 HTTP 的一些基础是非常重要的。典型的 Web 通信包括以下活动：

1. 当用户浏览网页时，通过发送 `GET HTTP` 请求启动对 Web 服务器资源的访问请求。
2. 服务器处理请求，并使用 `HTTP 协议` 向浏览器发送响应。
3. 浏览器处理服务器响应，并以“表单”的形式呈现给用户。
4. 用户向表单输入内容，点击提交或回车键后，这些数据再次使用 `HTTP 协议` 发送到服务器。
5. 这些数据再次由服务器处理，服务器将其响应发布到浏览器，并显示在网页上。

## Web 服务器

Web 服务器最初设计用于接收和处理请求，并使用 `HTTP` 将结果发回浏览器。起初，当网页非常简单时，此类服务器能够处理大量的请求。随着时间的推移，发送和关闭连接的状态使得现代的 Web 服务器功能更强大。Web 服务器现在实现了所谓的“存活”。

### Web 浏览器

Web 浏览器是一个桌面应用程序，用于显示网页并管理用户交互。服务器之间的通信通过 `AJAX` 等技术建立。

### 数据如何提交到 Web 服务器

HTML 表单可以使用 `<form>` 元素按如下方式创建：

```html
<form method="post" action="getCustomerInformation.aspx" >
客户编号：
  <input type="text" name="Number" />
  <input type="submit" value="获取信息" />
</form>
```



此表单接收编号并返回显示详情的页面。然而，需要注意并不是所有元素都可以用于提交数据。允许的元素包括：

- `<textarea>`：接受多行输入
- `<button>`：可点击按钮，可以放置在任何内容或图像上。
- `<select>`：下拉列表，允许多次选择。选中的选项可以使用 jQuery `$('option:selected')` 识别。
- `<input type="checkbox">`：复选框，具有用于设置以及读取状态的值属性。识别已选复选框的 jQuery 是 `$('input[type=checkbox]:checked')`。
- `<input type="button">`：可点击按钮，带有文本提示。
- `<input type="datetime">`：控件，显示日期和时间（UTC）。
- `<input type="date">`：控件，仅日期。
- `<input type="email">`：文件选择字段，具有上传文件的浏览按钮。
- `<input type="color">`：颜色选择器。
- `<input type="hidden">`：隐藏输入字段。
- `<input type="datetime-local">`：控件，显示日期和时间（任何时区）。
- `<input type="month">`：月份-年份控件。
- `<input type="image">`：图像提交按钮。
- `<input type="password">`：带有掩码字符的密码字段。
- `<input type="number">`：数字字段。
- `<input type='range'>`：这是一个控件，接受数值并定义了允许的取值范围。
- `<input type='radio'>`：这是一个单选按钮，具有 `value` 属性用于设置和读取按钮状态。用于识别已选单选按钮的 jQuery 代码为 `$('input[type=radio]:checked')`。
- `<input type='search'>`：这是一个文本字段，用于输入搜索字符串。
- `<input type='reset'>`：这是一个按钮，可用于重置表单字段。
- `<input type='url'>`：这是一个 URL 字段。
- `<input type='tel'>`：这是一个电话字段。
- `<input type='submit'>`：这是一个提交按钮。
- `<input type='time'>`：这是一个控件，接受时间值。
- `<input type='text'>`：这是一个单行文本字段。
- `<input type='week'>`：这是一个周/年控件。

## `<label>` 元素

它是用于向用户传达元素含义的元素。该元素中的文本显示在文本框内，当用户点击它时，文本会自动移除。你也可以指定标签的样式。

## 指定父级表单

在某些情况下，表单的提交元素可能不在同一个结构中。因此，在这种情况下，收集数据可能是一项挑战。为了解决这个问题，HTML5 提供了一个名为 `id` 的属性，可以为多个表单元素设置该属性。这将允许一次性从不同的表单元素中收集数据。

## 如何触发表单提交

触发时，从表单或相同 `id` 的表单的提交元素收集的所有数据都将使用 HTTP 方法发送到服务器。`<input>` 元素可以触发表单提交。此外，你也可以使用 JavaScript 实现此目的。为了实现这一点，你必须给相关的表单赋予一个 `id`，即 `myFirstForm`。链接 HTML 文档的 `default.js` 文件必须包含以下代码：

```javascript
$(document).ready(function () {

  $('#myFirstButton').on('click', submitMyFirstForm);

});

function submitMyFirstForm() {

  $('#myFirstForm').submit();

}
```

如果表单的 `method` 属性没有赋予值，则它被设置为默认的 `GET`。此外，`action` 属性也会有一个默认值。因此，点击按钮将引用页面到相同的页面。然而，URL 现在将包含一个 `QueryString`，它是用户选择或输入的值的组合。例如，如果表单要求用户输入客户 ID，而用户输入了 1245，那么 `QueryString` 将是：

`customerID=1245`

此 `QueryString` 将按以下方式附加到 URL：

`Mywebpage.asp?customerID=1245`

这里同样需要提到的是，`QueryString` 是经过 URI 编码的。因此，特殊字符由特定值表示。例如，空格表示为 `+`，感叹号（`!`）表示为 `%21`。键-值对表示为 `name=value`，键-值对之间用 `&` 分隔。

## 如何序列化表单

你可以使用 jQuery 的 `serialize` 方法对表单进行序列化。可以通过如下方式：

```javascript
var myFormData = $('#myFirstForm').serialize();
```

你可以使用以下代码解码 URI 编码的字符串：

```javascript
var data = decodeURIComponent(myFormData);
```

## 使用 Autofocus 属性

默认情况下，焦点不会设置在表单的任何元素上。但你可以使用 `focus` 方法设置焦点，其实现方式如下：

```javascript
$('input[name="firstName"]').focus();
```

然而，你也可以通过以下方式设置自动聚焦：

```html
<input type="text" name="firstName" autofocus="autofocus"/>
```

## 如何使用数据提交约束

表单只有在满足以下约束条件时才能发送数据：

- 必须设置 `Name` 属性。
- 你必须已设置表单提交元素的值。
- `<form>` 元素必须定义了表单提交元素，且表单提交元素不应被禁用。
- 如果实现了多个提交按钮，则只有在点击激活的提交按钮时才会提交值。
- 选中复选框。
- 选中单选按钮。
- `<option>` 元素必须设置 `<option>` 元素。
- 如果有文件选择字段，必须选择其中一个字段。
- 对象元素的 `declare` 属性必须已设置。

始终记住，重置按钮不会发送任何数据，且表单不需要 ID 即可发送数据。

## 如何使用 POST 或 GET

有两种 HTTP 方法可将数据提交到服务器。这些方法是 `GET` 和 `POST`。在一种情况下，URL 会附加 `QueryString`。而在另一种情况下，信息是在消息体中发送的。

## 表单验证

理解 Web 应用程序所有安全问题的根源在于用户数据是有益的。当你决定向用户数据和交互开放应用程序时，你就让你的应用程序容易受到安全威胁。因此，你需要在处理收到的任何数据之前对其进行验证，以防止出现任何问题。验证可以在浏览器端或服务器端进行。然而，建议在服务器端进行验证。

`createServer` 函数返回一个服务器对象，该对象会调用 `listen` 函数。此函数在 `8080` 端口进行监听，并且主机的 IP 地址被设置为 `127.0.0.1`。因此，如果你的系统上安装了网络适配器，你的 Web 服务器将立即开始监听 Web 请求。最后一行会在屏幕上打印一条内容，告知用户服务器正在运行并监听请求。

一旦你创建了文件并按照上述说明保存了文件内容，你必须打开命令提示符并输入命令：

```
Node myFile.js
```

现在，保持命令提示符激活状态，你必须打开浏览器并输入地址：`http://localhost:8080/`

一旦发送请求并接收响应，该信息将通过控制台传递给用户。如果你成功完成了这一操作，那么你刚刚创建了你的第一个 Node.js 网站。如果你想停止运行代码，只需按 `Ctrl+C` 即可。

现在你已经了解了如何接收请求，是时候查看这些请求是如何被处理以及如何生成响应的。你可能需要使用 `url` 模块来解析 `QueryString`。

下面提到的代码展示了你如何解析 URL 字符串并根据它生成响应。

```javascript
var http = require('http');

var url = require('url');

http.createServer(function (request, response) {

var url_parts = url.parse(request.url, true);

response.writeHead(200, {'Content-Type': 'text/plain'});

response.end('Hey ' + url_parts.query.name + '.\n');

console.log('Handled request from ' + url_parts.query.name);

}).listen(8080, 'localhost');

console.log('Server is running at: http://localhost:8080/');
```

你可以以之前代码类似的方式测试这段代码的运行情况。

## 如何创建 Node.js 模块

你可以通过以函数形式编写代码，然后在主代码中调用这些模块来创建模块。

```javascript
var myHttp = require('http');

var myUrl = require('url');

function start(){

http.createServer(function (request, response) {

var url_parts = url.parse(request.url, true);

response.writeHead(200, {'Content-Type': 'text/plain'});

response.end('Hello ' + url_parts.query.name + '!\n');

console.log('Handled request from ' + url_parts.query.name);

}).listen(8080, 'localhost');

console.log('Server running at http://localhost:8080/');

}

exports.start = start;
```

当你将这段代码保存到文件中时，一个模块就被创建了。该模块可以被其他函数通过 `require` 函数使用。例如，如果文件被保存为 `sample1.js`，那么可以在另一个函数中使用以下方式调用 `start()`：

```javascript
var samplex = require('./sample1.js');

sample1.start();
```

# 如何创建一个 Node.js 包 (package)

模块的集合被称为应用程序。一旦你发布了你的包，它就可以被安装和使用。例如一个包含不同数学模块的包。

根目录必须包含以下内容：
- `README.md`
- `/packName`
- `/lib`
- `main.js`
- `/bin`
- `mod1.js`
- `mod2.js`

## 创建聚合模块 (Aggregate Module)

你可能希望只为用户提供一个对象。用户应该能够通过这个对象访问包的所有模块。为了实现这一点，必须在 `bin` 文件夹中创建一个 `main.js` 模块，该模块必须定义包含在 `module.exports` 中的模块。

# 如何创建 README.md 文件

`README.md` 文件是一个帮助文件，开发者可以使用作为使用你包的启动指南。该文件的扩展名为 `.md`，它是 mark-down 的缩写。这种格式为文件中编写的内容提供了可读性。

此类类型的示例文件所示：

```
samplePackage package

====================
```

在 `samplePackage` 中，可用函数有：
- `add` 执行两个数字的相加并显示结果。
- `sub` 执行一个数字减另一个数字并显示结果。

# 如何创建 package.json 文件

此文件包含包的元数据，可以使用命令手动创建：

```
npm init
```

此命令会创建该文件，稍后可以对其编辑。示例文件所示：

```json
{

  "name": "sampleFile",

  "version": "0.0.0",

  "description": "This is a sample file ",

  "main": "bin/main.js",

  "scripts": {

    "test": "echo \"This is a test file\" && exit 1"

  },

  "repository": "",

  "keywords": [

    "sample",

    "example",

    "add",

    "sub"

  ],

  "author": "XYZ",

  "license": "ABC"

}
```

除了测试脚本，你还可以提供 git 脚本，它们是目前最好的源码控制管理器。

# 如何发布包

如之前所述，包可以根据术语定义。一旦你发布了包，它就可以被安装和使用。考虑一个包含不同数学模块的包。

根目录必须包含以下内容：
- `README.md`
- `/packName`
- `/lib`
- `main.js`
- `/bin`
- `mod1.js`
- `mod2.js`

## 创建聚合模块

你可能希望只为用户提供一个对象。用户应该能够通过这个对象访问包的所有模块。为了实现这一点，必须在 `bin` 文件夹中创建一个 `main.js` 模块，该模块必须定义包含在 `module.exports` 中的模块。

# 如何创建 README.md 文件

`README.md` 文件是一个帮助文件，开发者可以使用作为使用你包的启动指南。该文件的扩展名为 `.md`，它是 mark-down 的缩写。这种格式为文件中编写的内容提供了可读性。

此类类型的示例文件所示：

```
samplePackage package

====================
```

在 `samplePackage` 中，可用函数有：
- `add` 执行两个数字的相加并显示结果。
- `sub` 执行一个数字减另一个数字并显示结果。

# 如何创建 package.json 文件

此文件包含包的元数据，可以使用命令手动创建：

```
npm init
```

此命令会创建该文件，稍后可以对其编辑。示例文件所示：

```json
{

  "name": "sampleFile",

  "version": "0.0.0",

  "description": "This is a sample file ",

  "main": "bin/main.js",

  "scripts": {

    "test": "echo \"This is a test file\" && exit 1"

  },

  "repository": "",

  "keywords": [

    "sample",

    "example",

    "add",

    "sub"

  ],

  "author": "XYZ",

  "license": "ABC"

}
```

除了测试脚本，你还可以提供 git 脚本，它们是目前最好的源码控制管理器。

# 如何发布包

如之前所述，包可以根据术语定义。一旦你发布了包，它就可以被安装和使用。考虑一个包含不同数学模块的包。

根目录必须包含以下内容：
- `README.md`
- `/packName`
- `/lib`
- `main.js`
- `/bin`
- `mod1.js`
- `mod2.js`

## 创建聚合模块

你可能希望只为用户提供一个对象。用户应该能够通过这个对象访问包的所有模块。为了实现这一点，必须在 `bin` 文件夹中创建一个 `main.js` 模块，该模块必须定义包含在 `module.exports` 中的模块。

# 如何创建 README.md 文件

`README.md` 文件是一个帮助文件，开发者可以使用作为使用你包的启动指南。该文件的扩展名为 `.md`，它是 mark-down 的缩写。这种格式为文件中编写的内容提供了可读性。

此类类型的示例文件所示：

```
samplePackage package

====================
```

在 `samplePackage` 中，可用函数有：
- `add` 执行两个数字的相加并显示结果。
- `sub` 执行一个数字减另一个数字并显示结果。

# 如何创建 package.json 文件

此文件包含包的元数据，可以使用命令手动创建：

```
npm init
```

此命令会创建该文件，稍后可以对其编辑。示例文件所示：

```json
{

  "name": "sampleFile",

  "version": "0.0.0",

  "description": "This is a sample file ",

  "main": "bin/main.js",

  "scripts": {

    "test": "echo \"This is a test file\" && exit 1"

  },

  "repository": "",

  "keywords": [

    "sample",

    "example",

    "add",

    "sub"

  ],

  "author": "XYZ",

  "license": "ABC"

}
```



除了测试脚本，你还可以提供`git`脚本，它们是目前最好的源码控制管理器。

### 1. 创建一个文件`myApp.js`并向该文件添加以下内容：

```javascript
var express = require('express');
var app = express();
```

### 2. 定义路由
你可以使用`myApp.Method()`语法来定义路由。

```javascript
app.get('/', function(request, response){
response.send('Hey World!');
});
```

上述代码将在接收到请求时发送响应`Hey World!`。

### 3. 监听请求
必须添加的最后一段代码用于监听请求。这段代码如下：

```javascript
var port = 8080;
app.listen(port);
console.log('Listening on port: ' + port);
```

### 4. 运行应用程序
一旦文件完成，你就可以保存它并使用命令`node app`运行它。现在，如果你打开浏览器并输入地址`localhost:8080/`，你将获得响应`Hey World!`。

### 5. 添加静态网页
你可以通过将`app.get`语句替换为`app.use(express.static(__dirname + '/public'))`来向应用程序添加网页。这将允许对多个网页使用相同的代码。该概念的示例实现下所示：

```html
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<title></title>
</head>
<body>
<form method="get" action="/submitHey">
Enter First Name: <input type="text" name="firstName" />
<input type="submit" value="Submit" />
</form>
</body>
</html>
```

请注意，`action`属性被设置为`/submitHey`。换句话说，服务器端会调用此资源，以处理通过`QueryString`传递给它的数据。`myApp.js`文件应包含以下内容：

```javascript
var express = require('express');
var app = express();
app.use(express.static(__dirname + '/public'));
app.get('/SubmitHey', function (request, response) {
response.writeHead(200, { 'Content-Type': 'text/html' });
response.write('Hey ' + request.query.userName + '!<br />');
response.end('Enjoy.');
console.log('Handled request from ' + request.query.userName);
});
var port = 8080;
app.listen(port);
console.log('Listening on port: ' + port);
```

该程序可以按照上述方式运行。

### 6. 使用`formidable`包
`formidable`包可以用于回传数据。虽然上一种方法使用了`GET`方法，但此方法使用了`POST`方法。

#### 6.1. 创建 HTML 表单
为了说明其工作原理，请创建一个如下所示的 HTML 表单：

```html
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<title></title>
</head>
<body>
<form method="post" action="/SubmitHeyPost">
Enter Name: <input type="text" name="firstName" />
<input type="submit" value="Submit" />
</form>
</body>
</html>
```

#### 6.2. 获取包
现在，在命令行提示符中，你需要输入命令来获取`formidable`包，命令为：

`npm info formidable`

#### 6.3. 修改`package.json`
你也可以按照以下方式修改`package.json`文件：

```json
{
"name": "HelloExpress",
"version": "0.0.0",
"description": "Sample Website",
"main": "index.js",
"scripts": {
"test": "echo \"Error: test not specified\" && exit 1"
},
"repository": "",
"author": "XYZ",
"license": "BSD",
"private": true,
"dependencies": {
"formidable": "1.x",
"express": "3.0.0"
}
}
```

#### 6.4. 安装包
现在你可以在命令行提示符中输入以下命令来安装`formidable`包：

`npm install`

此命令会在本地安装该包。因此，你需要在`myApp.js`中添加一行，允许文件引用该包：

```javascript
var formidable = require('formidable');
```

#### 6.5. 示例`myApp.js`
一个示例`myApp.js`文件应该如下：

```javascript
var express = require('express');
var app = express();
var formidable = require('formidable');
app.use('/forms', express.static(__dirname + '/public'));
app.post('/SubmitHeyPost', function (request, response) {
if (request.method.toLowerCase() == 'post') {
var form = new formidable.IncomingForm();
form.parse(request, function (err, fields) {
response.writeHead(200, { 'Content-Type': 'text/html' });
response.write('Hey ' + fields.userName + '!<br />');
response.end('Enjoy this POST.');
console.log('Handled request from ' + fields.userName);
});
}
});
app.get('/SubmitHey', function (request, response) {
response.writeHead(200, { 'Content-Type': 'text/html' });
response.write('Hey ' + request.query.userName + '!<br />');
response.end('Enjoy.');
console.log('Handled request from ' + request.query.userName);
});
var port = 8080;
app.listen(port);
console.log('Listening on port: ' + port);
```

#### 6.6. 运行应用程序
你现在可以以之前的方式运行应用程序。

### 7. 与 Web 服务交互
典型网站的一个巨大缺点是 HTML 是重绘的。用于发送请求的技术是`AJAX`（异步 JavaScript 和 XML）。在继续之前，了解 Web 服务的基础知识是重要的。客户端需要定期与 Web 服务通信。在这种情况下，任何人可以使用 Web 服务创建请求并接收响应。你可能听过“杂烩”（mashups）这个术语，这是一个描述组合多个 Web 服务的应用程序的术语。Web 服务分为两大类，即任意 Web 服务和`REST`（表述状态转移）。前者操作集是任意的，而后者存在统一的操作集。

### 8. 表述状态转移 (REST)
该框架使用标准的 HTTP 操作，将其映射到创建、删除、更新和检索操作。此外，`REST`不关注消息交互。相反，它的交互面向无资源。这可能就是`REST`概念因创建整洁 URL 而闻名的原因。`REST` URL 的示例包括`localhost:8080/Customers/2`（删除客户）和`localhost:8080/Vehicles?VIN=12`（用于检索通过`GET`方法传递参数的车辆信息）。

某些防火墙可能不允许使用`POST`和`GET`方法。因此，建议在`QueryString`中使用`verb`。URL 的示例如下：

`http://localhost:8080/Vehicles?verb=DELETE&VIN=987`

HTTP 协议还允许使用`HTTPS`版本来实现安全性。`REST`提供了许多优势，如连接简单、运行速度快和资源消耗少。

### 任意 Web 服务
这种类型的 Web 服务也称为大型 Web 服务。此类服务的示例是`WCF`（Windows 通信框架）。任意 Web 服务通过不将操作映射到协议的某些方面来扩展其操作领域。因此，它们提供了更多功能，包括许多安全机制和消息路由。

这种类型的 Web 服务拥有一种典型的接口格式，客户端可以使用它来读取和解析信息。因此，客户端可以立即调用该服务。一种常见的 API 格式是 Web 服务描述语言（WSDL）。对于任意 Web 服务，客户端必须借助`SOAP`（简单对象访问协议）消息来组装其请求。这种 Web 服务不使用`HTTP`协议，而是使用`TCP`。

## 如何使用 Node.js 创建 RESTful Web 服务
在之前提到的示例中，`samplePackage`可以暴露为 Web 服务。可以在该包上使用`GET`方法，并将操作作为参数传递。该包的一个良好的 RESTful 实现可能如下：

`http://localhost:8080/samplePackage?operation=add&x=1&y=5`

## 如何使用 AJAX 调用 Web 服务
可以使用`AJAX`异步调用 Web 服务，它实际上是`JavaScript`。与其向服务器发送调用并重绘 HTML 文档，`AJAX`只是向服务器进行回调。在这种情况下，屏幕不会重绘。下面给出一个示例实现：

可以使用以下代码创建一个`MyPage.html`：

```html
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<title></title>
<script type="text/javascript" src="/scripts/jquery-1.8.2.min.js"></script>
<script type="text/javascript" src="/scripts/default.js"></script>
</head>
<body>
<form id="myForm">
输入 X 的值:<input type="text" id="x" /><br />
输入 Y 的值:<input type="text" id="y" /><br />
操作结果: <span id="result"></span><br />
<button id="btnAdd" type="button">相加数字</button>
</form>
</body>
</html>
```

必须修改`default.js`文件，以包含处理这些函数所需的代码。请务必检查`jQuery`的版本，以及它是否与你在`default.js`文件中提到的版本名称匹配。此处使用的`<form>`元素是排列数据格式的手段，数据并不会实际通过表单发送到服务器。`JavaScript`和`jQuery`会访问输入的数据并执行`AJAX`调用。

## 如何使用 XMLHttpRequest
实际执行`AJAX`用的对象是`XMLHttpRequest`，它可以用于发送/接收 XML 和其他类型的数据。该对象可以使用以下方式：

```javascript
var xmlhttp=new XMLHttpRequest();
xmlhttp.open("GET","/add?x=50&y=1",false);
xmlhttp.send();
var xmlDoc=xmlhttp.responseXML;
```

第一行创建对象，第二行设置使用带有指定`QueryString`的`GET`方法，使用`'false`表示操作必须异步执行。下一行发送请求，最后一行将响应赋值给变量，稍后可以对其进行读取和解析以处理响应。

然而，生成的输出是 JSON 而不是 XML，因此`default.js`文件必须更改为：

```javascript
$(document).ready(function () {
$('#btnAdd').on('click', addTwoNum)
});
function addTwoNum() {
}
```



如需更多阅读，请在亚马逊搜索“A Simple Start to jQuery, JavaScript, and Html5 for Beginners”（作者为 Sanderson）。

# 初学者 Java

Java 编程入门（由软件工程师编写）

Scott Sanderson

## 目录

- [Java - 语法](https://docs.google.com/document/d/1yZF262caVNeIWUrxLPOzDJJG8ERkAwz-ZovtVSOMuuY/edit#heading=h.1fob9te)
- [第一个 Java 程序：](https://docs.google.com/document/d/1yZF262caVNeIWUrxLPOzDJJG8ERkAwz-ZovtVSOMuuY/edit#heading=h.3znysh7)
- [基本语法](https://docs.google.com/document/d/1yZF262caVNeIWUrxLPOzDJJG8ERkAwz-ZovtVSOMuuY/edit#heading=h.2et92p0)
- [Java 关键字：](https://docs.google.com/document/d/1yZF262caVNeIWUrxLPOzDJJG8ERkAwz-ZovtVSOMuuY/edit#heading=h.tyjcwt)
- [Java 中的注释](https://docs.google.com/document/d/1yZF262caVNeIWUrxLPOzDJJG8ERkAwz-ZovtVSOMuuY/edit#heading=h.3dy6vkm)
- [使用空行：](https://docs.google.com/document/d/1yZF262caVNeIWUrxLPOzDJJG8ERkAwz-ZovtVSOMuuY/edit#heading=h.1t3h5sf)
- [继承：](https://docs.google.com/document/d/1yZF262caVNeIWUrxLPOzDJJG8ERkAwz-ZovtVSOMuuY/edit#heading=h.4d34og8)
- [接口：](https://docs.google.com/document/d/1yZF262caVNeIWUrxLPOzDJJG8ERkAwz-ZovtVSOMuuY/edit#heading=h.2s8ey1)
- [对象与类](https://docs.google.com/document/d/1yZF262caVNeIWUrxLPOzDJJG8ERkAwz-ZovtVSOMuuY/edit#heading=h.17dpvu)
- [基本数据类型](https://docs.google.com/document/d/1yZF262caVNeIWUrxLPOzDJJG8ERkAwz-ZovtVSOMuuY/edit#heading=h.3rdcrjn)
- [变量类型](https://docs.google.com/document/d/1yZF262caVNeIWUrxLPOzDJJG8ERkAwz-ZovtVSOMuuY/edit#heading=h.26in1)
- [Java 中的运算符](https://docs.google.com/document/d/1yZF262caVNeIWUrxLPOzDJJG8ERkAwz-ZovtVSOMuuY/edit#heading=h.lnxb)
- [算术运算符](https://docs.google.com/document/d/1yZF262caVNeIWUrxLPOzDJJG8ERkAwz-ZovtVSOMuuY/edit#heading=h.35kun2)
- [关系运算符](https://docs.google.com/document/d/1yZF262caVNeIWUrxLPOzDJJG8ERkAwz-ZovtVSOMuuY/edit#heading=h.1ks4uv)
- [位运算符](https://docs.google.com/document/d/1yZF262caVNeIWUrxLPOzDJJG8ERkAwz-ZovtVSOMuuY/edit#heading=h.44sinio)
- [逻辑运算符](https://docs.google.com/document/d/1yZF262caVNeIWUrxLPOzDJJG8ERkAwz-ZovtVSOMuuY/edit#heading=h.2jxqq)
- [赋值运算符](https://docs.google.com/document/d/1yZF262caVNeIWUrxLPOzDJJG8ERkAwz-ZovtVSOMuuY/edit#heading=h.z37ya)
- [杂运算符](https://docs.google.com/document/d/1yZF262caVNeIWUrxLPOzDJJG8ERkAwz-ZovtVSOMuuY/edit#heading=h.3j2qq)
- [条件运算符 ](https://docs.google.com/document/d/1yZF262caVNeIWUrxLPOzDJJG8ERkAwz-ZovtVSOMuuY/edit#heading=h.1y81tw)
- [instanceof 运算符](https://docs.google.com/document/d/1yZF262caVNeIWUrxLPOzDJJG8ERkAwz-ZovtVSOMuuY/edit#heading=h.4i7oj)
- [Java 运算符优先级](https://docs.google.com/document/d/1yZF262caVNeIWUrxLPOzDJJG8ERkAwz-ZovtVSOMuuY/edit#heading=h.2xcytpi)
- [Java 中的循环](https://docs.google.com/document/d/1yZF262caVNeIWUrxLPOzDJJG8ERkAwz-ZovtVSOMuuY/edit#heading=h.1ci9xb)
- [while 循环](https://docs.google.com/document/d/1yZF262caVNeIWUrxLPOzDJJG8ERkAwz-ZovtVSOMuuY/edit#heading=h.3whml4)
- [分支语句](https://docs.google.com/document/d/1yZF262caVNeIWUrxLPOzDJJG8ERkAwz-ZovtVSOMuuY/edit#heading=h.2bnwsx)
- [Java 中的字符串](https://docs.google.com/document/d/1yZF262caVNeIWUrxLPOzDJJG8ERkAwz-ZovtVSOMuuY/edit#heading=h.qsh7q)
- [String 方法](https://docs.google.com/document/d/1yZF262caVNeIWUrxLPOzDJJG8ERkAwz-ZovtVSOMuuY/edit#heading=h.3aspoj)
- [数组](https://docs.google.com/document/d/1yZF262caVNeIWUrxLPOzDJJG8ERkAwz-ZovtVSOMuuY/edit#heading=h.1pxezwc)
- [正则表达式](https://docs.google.com/document/d/1yZF262caVNeIWUrxLPOzDJJG8ERkAwz-ZovtVSOMuuY/edit#heading=h.49x2ik)
- [正则表达式语法](https://docs.google.com/document/d/1yZF262caVNeIWUrxLPOzDJJG8ERkAwz-ZovtVSOMuuY/edit#heading=h.2p2csry)
- [Matcher 类的方法](https://docs.google.com/document/d/1yZF262caVNeIWUrxLPOzDJJG8ERkAwz-ZovtVSOMuuY/edit#heading=h.14n2zr)
- [Index 方法：](https://docs.google.com/document/d/1yZF262caVNeIWUrxLPOzDJJG8ERkAwz-ZovtVSOMuuY/edit#heading=h.3o7alnk)
- [PatternSyntaxException 类方法：](https://docs.google.com/document/d/1yZF262caVNeIWUrxLPOzDJJG8ERkAwz-ZovtVSOMuuY/edit#heading=h.23ckvvd)
- [方法](https://docs.google.com/document/d/1yZF262caVNeIWUrxLPOzDJJG8ERkAwz-ZovtVSOMuuY/edit#heading=h.ihv636)
- [文件处理](https://docs.google.com/document/d/1yZF262caVNeIWUrxLPOzDJJG8ERkAwz-ZovtVSOMuuY/edit#heading=h.32hioqz)
- [字节流](https://docs.google.com/document/d/1yZF262caVNeIWUrxLPOzDJJG8ERkAwz-ZovtVSOMuuY/edit#heading=h.1hmsyys)
- [FileOutputStream：](https://docs.google.com/document/d/1yZF262caVNeIWUrxLPOzDJJG8ERkAwz-ZovtVSOMuuY/edit#heading=h.41mghml)
- [异常处理](https://docs.google.com/document/d/1yZF262caVNeIWUrxLPOzDJJG8ERkAwz-ZovtVSOMuuY/edit#heading=h.2grqrue)

## [Throws 关键字](https://docs.google.com/document/d/1yZF262caVNeIWUrxLPOzDJJG8ERkAwz-ZovtVSOMuuY/edit#heading=h.vx1227)

## [Finally 关键字](https://docs.google.com/document/d/1yZF262caVNeIWUrxLPOzDJJG8ERkAwz-ZovtVSOMuuY/edit#heading=h.3fwokq0)

## [创建异常](https://docs.google.com/document/d/1yZF262caVNeIWUrxLPOzDJJG8ERkAwz-ZovtVSOMuuY/edit#heading=h.1v1yuxt)

## [常见异常](https://docs.google.com/document/d/1yZF262caVNeIWUrxLPOzDJJG8ERkAwz-ZovtVSOMuuY/edit#heading=h.4f1mdlm)

## [接口与包](https://docs.google.com/document/d/1yZF262caVNeIWUrxLPOzDJJG8ERkAwz-ZovtVSOMuuY/edit#heading=h.2u6wntf)

## [Java Applets](https://docs.google.com/document/d/1yZF262caVNeIWUrxLPOzDJJG8ERkAwz-ZovtVSOMuuY/edit#heading=h.19c6y18)

Copyright 2016 由 [Globalized Healing, LLC](http://www.globalizedhealing.com) 版权所有。

[点击此处获取免费的电子书！](https://globalizedhealing1.leadpages.net/kindle-books/)

## 简介

Java 是一种编程语言，由 Sun Microsystems 推出。这项由 James Gosling 发起，Java 的最终版本于 1995 年发布。然而，最初 Java 是作为 Sun 平台的一个组件发布的，被称为 `Java 1.0`。Java 的最新版本是 `Java Standard 6`。

Java 作为编程平台和语言的日益普及，导致了许多工具和配置的开发，并考虑到 Java。例如，`J2ME` 和 `J2EE` 是两种配置。Java 的最新版本被称为 `Java SE`、`Java EE` 或 `Java ME`。使用 Java 平台最大的优势是它允许你在任何地方运行代码，因此你只需要编写一次代码。

至于 Java 的特征，如下：

- **面向对象**：在 Java 中，一切都是对象。Java 可以有效地扩展到不可想象的维度，因为它基于对象模型。
- **平台无关**：与 `C` 和 `C++` 等许多其他编程语言不同，当 Java 聚合时，它被转换为独立于机器的字节码。相反，这种字节码通过网络传输并由虚拟机 `JVM` 解释。
- **简单**：Java 旨在易于学习。如果你理解 `OOP` 的基本概念，Java 将很容易掌握。
- **安全**：凭借 Java 的安全框架，能够创建不受病毒和篡改的程序。公钥加密被用作身份验证策略。
- **架构无关**：Java 编译器产生的对象格式与机器架构无关。编译后的代码可以在许多处理器上执行，要求是它们都具有 Java 运行时框架。
- **可移植性**：Java 代码是机器和平台无关的，使其非常紧凑。Java 编译器采用 `ANSI C` 子集，具有良好的可移植性。
- **健壮性**：Java 试图消除导致潜在系统故障的情况，主要强调运行时检查和编译时检查。
- **支持多线程**：凭借 Java 的多线程功能，可以编写同时执行许多任务的程序。这一特性允许设计师构建智能应用程序。
- **解释型代码**：Java 字节码被动态解释为本地机器码。这种方法更快，因为接口是增量且轻量级的。
- **高性能**：通过使用 `Just-In-Time` 编译器，Java 增强了系统的性能。
- **分布式**：Java 适用于网络环境。
- **动态**：Java 被认为比 `C` 或 `C++` 更具动态性，因为它适应开发环境。Java 项目可以携带大量的运行时数据，用于检查访问并在运行时响应。

## Java 历史

James Gosling 于 1991 年 6 月开始研究 Java 编程语言，用于他的许多顶盒项目之一。这种编程语言最初被称为 `Oak`。这个名字源于 Gosling 办公室外的一棵橡树。名字被改为 `Green`，随后从字典列表中随机选择并命名为 `Java`。

Sun 在 1995 年发布了第一个版本 `Java 1.0`。它保证了“编写一次，到处运行”。

## Java - 基础语法

一个基础 Java 程序可以分解为几个结构和元素。通常，它可以被描述为对象的集合，它们相互通信。

- **类**：类可以被描述为描绘对象行为的蓝图。
- **对象**：对象由两个部分组成：方法和属性。例如，如果你考虑一只小狗，它有以下属性：名字、颜色和品种。此外，它还有以下行为，包括汪汪、摇尾和吃。任何对象都只是类的实例。
- **实例变量**：每个对象都有一组变量。对象的状态是由程序执行期间分配给这些变量的属性组成的。
- **方法**：方法的定义。此外，一个类可以包含许多方法。逻辑在这些方法中编写，信息在这些方法中控制，所有的活动在这些方法中执行。

### 第一个 Java 程序

为了开始基础 Java 编程，让我们看看标准的 Hello World 程序。

```java
public class MyFirstJavaProgram {

    public static void main(String []args) {

        System.out.println("Say Hello World To The World!");

    }

}
```

### 步骤

1. 打开任何文本编辑器并将此代码粘贴到文件中。
2. 以`.java`扩展名保存文件。例如，你可以将文件保存为`Sample.java`。
3. 下一步是打开系统的命令提示符，将其引用切换到保存文件的目录。例如，如果你将文件保存在`C:\`，那么你必须将提示符带到同一个目录。
4. 为了编译代码，你必须输入以下：
```bash
javac Sample.java
```
5. 如果没有错误，将自动跳转到下一行。现在你可以使用以下命令执行代码：
```bash
java Sample.java
```



你应该能够在屏幕上看到以下输出。

`Say Hello World To The World!`

## 基础语法

关于 Java 程序，记住以下几点至关重要。

### 类名
对于所有类名，第一个字母都应该是大写。

如果使用了多个单词来构建一个类的名称，那么每个内部单词的第一个字母都应该是大写。例如，一个标准的类名如下：

`class Sampleclass`

### 区分大小写
Java 是区分大小写敏感的，这意味着标识符 `Hi` 和 `hi` 在 Java 中具有不同的含义。

### 方法名
所有的系统名称都应该以小写字母开头。如果使用了多个单词来构建方法名，那么每个内部单词的第一个字母都应该是大写。此惯例的示例如下：

`public void mysamplemethod ()`

### 文件名
系统记录名称必须与类名完全匹配。在保存文件时，你应该使用类名进行保存。记住 Java 是区分大小敏感的，并在名称末尾添加`".java"`。如果文档名和类名不匹配，你的系统将无法编译。以类名 `Sample` 为例。在这种情况下，你必须将文件命名为`sample.java`。

### `public static void main(string args[])`
Java 系统处理从 `main()` 函数开始，这是每个 Java 程序必不可少的组成。

## Java 标识符

所有的 Java 组件都需要名称。用于类、变量和策略的名称被称为标识符。在 Java 中，关于标识符有几个需要记住的。它们遵循以下标准：

- 所有标识符必须以字母（从`a`到`z`）、下划线（`_`）或特殊字符（`$`）开头。
- 在第一个字符之后，标识符可以是任何字符组合。
- 你不能使用关键字作为标识符。
- 最重要的是，标识符区分大小写。所以，`Sample` 与 `sample`。
- 标识符示例包括 `$salary`、`age`、`__1_value` 和 `_value`。
- 非法标识符示例包括 `compensation` 和 `123abc`。

## Java 修饰符

与任何编程语言一样，可以通过修饰符更改类和系统。修饰符分为两种：

- 访问修饰符：`public`、`default`、`protected` 和 `private`
- 非访问修饰符：`strictfp`、`final` 和 `abstract`

我们将在后续章节中研究更多关于修饰符的见。

## Java 变量

Java 支持多种类型的变量。这些类型的变量包括：

- 实例变量（非静态变量）
- 类变量（静态变量）
- 局部变量

## Java 数组

数组是连续的内存位置，存储相同类型的不同变量。另一方面，数组本身是内存中的一个对象。我们将在后续章节中研究如何声明、开发和实例化这些。

## Java 枚举

枚举在`java 5.0`中作为 Java 包的一部分引入。枚举限制变量只能具有少数预定义属性中的一个。此标识列表中的属性被称为枚举。通过使用枚举，可以减少代码中 bug 的数量。例如，如果我们考虑一个咖啡馆应用程序，可以将杯子尺寸限制为特大号、大、中号和小号。这将确保不会有人请求菜单或应用程序列出的尺寸之外的任何尺寸。

请注意，枚举可以单独单独声明，也可以在类内部声明。然而，在枚举体内部也可以创建方法、变量和构造函数。

## Java 关键字

Java 中的关键字或保留字在下表所示。按照规定，这些词不能用变量或常量的名称。

- `assert`
- `abstract`
- `break`
- `boolean`
- `case`
- `byte`
- `char`
- `catch`
- `const`
- `class`
- `default`
- `continue`
- `double`
- `do`
- `enum`
- `else`
- `final`
- `extends`
- `float`
- `finally`
- `goto`
- `for`
- `implements`
- `if`
- `instanceof`
- `import`
- `int`
- `long`
- `interface`
- `new`
- `native`
- `private`
- `package`
- `protected`
- `return`
- `public`
- `static`
- `short`
- `super`
- `strictfp`
- `synchronized`
- `switch`
- `throw`
- `this`
- `transient`
- `throws`
- `while`
- `try`
- `volatile`
- `void`

## Java 中的注释

与 C++ 和 C 一样，Java 支持两种类型的注释，即单行注释和多行注释。这些类型注释的语法如下：

单行注释：
`//<comment>`

多行注释：
`/*<comment>*/`

注释区域存在的所有字符都将被 Java 编译器简单忽略。

### 使用空行
任何仅由空白字符或注释组成的行都被视为空行。这些行直接被编译器忽略，不包含在可执行文件中。

## 继承

Java 支持继承。换句话说，在这个编程语言中可以从一个类派生另一个类。例如，如果你需要创建一个新类，它是现有类的扩展，你可以简单地从现有类派生新类。这允许新类访问已实现的元素。

### 接口
如前所述，Java 全关于对象之间的交互。不同对象之间通信的方式是在所谓的 `interface` 中定义的。此外，接口也是继承特性的重要方面。作为接口的一部分，声明了子类可以使用的方法。然而，声明为可用的所有方法必须在子类中实现。

# 对象与类

Java 是一种面向对象的编程语言。作为一个具有面向对象特性的问题，Java 支持以下核心概念：

- 继承
- 多态
- 抽象
- 封装
- 对象
- 消息传递
- 类
- 方法
- 实例

在此部分，我们将研究类和对象的概念。

- 类 - 类可以被描述为蓝图，声明并定义了对象将实现和使用的属性和方法。
- 对象 - 对象是具有状态的简单现实实体。

例如，如果你考虑一个现实实体，一只拉布多，那么这只狗就是一个对象。然而，它属于狗类。因此，关联类是 `Dog`。

### Java 中的对象
让我们深入研究什么是对象。如果我们考虑现实现实，我们可以在周围发现许多实体，汽车、人类、狗等等。事实上，任何现实实体都可以建模为对象。所有这些实体的一个共同点是它们包含状态和行为。如果我们考虑一只狗，它的状态是——品种、名字和颜色。然而，它的行为包括进食习惯以及跑步和汪叫等特征。

### Java 中的类
类是用于制作单个对象的蓝图。类的示例在下方：

```java
open class Dogs {

String breed;

String shade;

int age;

void eating (){ }

void barking (){ }

}
```

类可以包含任何的伴随变量种类。

- 局部变量

在方法、构造函数或代码块内部声明并使用的变量被称为局部变量。该变量在方法或作用域内部声明并实例化，并在方法执行结束时被销毁。

### 实例变量
实例变量是类内部、但在任何方法之外的变量。这些变量在类堆栈（加载）时被实例化。可以在该特定类的任何技术方法、构造函数或代码块中访问这些变量。

### 类变量
类变量是在类内部声明的、在任何方法之外的、且在其前面带有 `static` 关键字的变量。

一个类可以拥有任意数量的程序，以实现不同类型的功能。在上面的示例中，`eating()` 和 `barking()` 是所使用的方法。下面列出了研究 Java 语言中的类时需要检查的一些重要主题。

### 构造函数
在谈论类时，最重要的子主题中一个突出的是构造函数。每个类都有一个构造函数。如果我们没有显式地为类编写构造函数，Java 编译器会为该类生成一个默认构造函数。每当创建一个对象时，至少会调用一次构造函数。

构造的基本原理是它们的名称必须与类相同。一个类可以有多个构造函数，根据给定的参数和预期的返回类型，调用匹配的构造函数。下面是此类方法的示例实现：

```java
public class Puppies{

public Puppies(){

}

public Puppies(string puppyname){

}
```

上述类有两个构造函数。其中一个构造函数不需要参数。然而，另一个构造函数需要一个等于幼犬名称的 `string`。Java 还支持单例类，你有能力为一个类创建一个唯一的对象。

### 创建对象
如之前所述，类为对象的创建提供了蓝图。因此，从根本上对象是从类创建的。在 Java 中，使用 `new` 关键字来创建新对象。

创建任何对象都涉及三个步骤。这些步骤所示：

* **声明**：一个带有变量名和对象类型的变量断言。
* **实例化**：使用`"new"`关键字创建已声明类的对象。
* **初始化**：在`"new"`关键字之后紧跟一个对构造函数的调用。该调用实例化类并结果创建一个相同的对象。

下面提供了示例实现以便更好地理解该概念。

```java
public class Puppies{

public Puppies(string name){

System.out.println("Passed Name of the puppy is:" + name );

}

public static void main(string []args){

Puppies samplepuppy = new Puppies( "jimmy" );

}
```

如果我们编译并运行上面的项目，它将交付如下结果：

```
Passed Name of the puppy is: jimmy
```

### 访问实例变量和方法
变量和方法通过类的类的对象来访问。要访问变量，正确的方法应该是如下：

以下语句创建了一个对象。

```java
Newobject = new Constructormethod();
```

可以使用以下语句访问与对象相关的变量和方法：

```java
Newobject.variablesname;

Newobject.methodsname();
```

下面是该概念的示例实现：

```java
public class Dog{

int dogAge;

public dogAge(String dogname){

System.out.println("Dog Name Passed is :" + dogname );

}

public void initAge( int dogage ){

dogAge = dogage;

}

public int getDogAge( ){

System.out.println("Dog’s present age is:" + dogAge );

return dogAge;

}

public static void main(String []args){

Dog myDog = new Dog( "jimmy" );

myDog.initAge( 5 );

myDog.getDogAge( );

System.out.println("Variable dogAge Value is:" + myDog.dogAge );

}

}
```

编译并执行以下代码后，你将能够看到以下结果。

```
Variable dogAge Value is: 5
```

### 源文件声明指南
作为这一区域的最后一部分，我们现在来研究源文件的声明标准。这些准则在源文件中声明类、导入声明和包时是关键的。

* 每个源记录可以有一个突出的公共类（public class）。
* 一个源文档可以有多个非公共类。
* 公共类名必须是源文档的。源文件的文件名必须以 `.java` 字符串结尾。例如，如果类名是 `public class Employeerecord{}`，则源文档应保存为 `Employeerecord.java`。
* 如果类声明在包内部，那么包的声明应当是源记录中的第一个声明。
* 如果有导入语句，则它们必须写在包声明和类声明之间。如果没有包声明，则导入语句应当是源文件的第一行。
* 导入和包声明将指示源记录中显示的所有类。

类有几种访问级别。此外，还有不同类型的类，包括最终类（final classes）以及其他几种。除了上述类型的类之外，Java 还有一些不常见的类，称为内部类（Inner classes）和匿名类（Anonymous classes）。

### Java 包
基本上，它是一种分类类和接口的方法。在创建 Java 应用时，会有许多类和接口。在这种情况下，这些类是必不可少的并减轻负担。在 Java 中，如果给出一个完全限定名（包含类和包名），编译器就可以不费力地找到。例如，为了加载 `java_java/io` 中的所有类，你必须使用以下语句：

```java
import java.io.*;
```

```java
Employeerecord employee2 = new Employeerecord("Mary John");

employee1.employeeage(32);

employee1.empcompensation(5000);

employee2.employeeage(25);

employee2.empcompensation(2000);

employee1.printemp();

employee2.printemp();

}
}
```



编译并执行后，你将得到以下输出：

```
empname: Jack Wright
empage: 32
empcompensation: 5000
empname: Mary John
empage: 25
empcompensation: 2000
```

## 基本数据类型

变量仅是用于存储数值的内存区域。这意味着当你创建一个变量时，你就在内存中为了留了空间。根据变量的数据类型，工作框架会分配内存并选择什么可以放入所持有的内存中。因此，通过为变量指定不同的数据类型，你可以在这些变量中存储整数、小数或字符。

Java 中可以访问两种数据类型：

* 引用/对象数据类型
* 基本数据类型

## 基本数据类型

Java 支持八种基本信息类型。基本数据类型由语言预定义，并用口号命名。本节将详细讨论这些数据类型。

### byte

* `byte` 信息类型是一个 8 位的带符号补码整数。
* 最大值为 `2⁷ -1`，等于 `127`。该值也包含在这些值的范围内。
* 最小值为 `-2⁷`，等于 `-128`。
* 此类型变量中存储的默认值为 `0`。
* `byte` 信息类型用于在大量的数组中节省空间，主要用于数字的集合，因为一个字节比 `int` 小四倍。
* 示例：`byte x = 200, byte y = -20`

### short

* `short` 信息类型是一个 16 位的带符号补码数字。
* 最大值为 `2¹⁵ -1`，等于 `32,767`。该数字也包含在范围内。
* 最小值为 `-2¹⁵`，等于 `-32,768`。
* `short` 信息类型也可以像 `byte` 信息类型一样节省内存。一个 `short` 比 `int` 小 2 倍。
* 此数据类型的默认值为 `0`。
* 示例：`short x = 425164, short y = -76686`

### int

* `int` 信息类型是一个 32 位的带符号补码数字。
* 此数据类型的最大值为 `2³¹ -1`，等于 `2,147,483,647`。该数字也包含在此数据类型的范围内。
* 此数据类型的最小值为 `-2³¹`，等于 `-2,147,483,648`。
* `int` 大多数被用作默认信息类型，除非对内存有顾顾虑。
* 此数据类型的默认值为 `0`。
* 示例：`int x = 826378, int y = -64782`

### long

* `long` 信息类型是一个 64 位的带符号补码整数。
* 此数据类型的最大值为 `2⁶³ -1`，等于 `9,223,372,036,854,775,807`。
* 此数据类型的最小值为 `-2⁶³`，等于 `-9,223,372,036,854,775,808`。
* 当需要比 `int` 更宽的内存范围时使用这种类型。
* 这些数据类型的默认值为 `0l`。
* 示例：`long x = 174636l, int y = -536452l`

### float

* `float` 是一种数据类型，以其单精度性性称，32 位 IEEE 754 浮点。
* `float` 主要用于在浮点数的大数组中节省内存。
* 此数据类型的默认值为 `0.0f`。
* `float` 信息类型永远不会用于精确值，例如货币。
* 示例：`float x = 254.3f`

### double

* `double` 信息类型是具有双倍精度的 64 位 IEEE 754 浮点数。
* 此信息类型主要被用作小数属性的默认信息类型。
* `double` 信息类型永远不应该用于精确值，例如货币。
* 此数据类型的默认值为 `0.0d`。
* 示例：`double x = 321.4`

### boolean

* `boolean` 信息类型表示一个位的数据。
* 任何 `boolean` 变量都可以取两个值之一：`true` 或 `false`。
* 此信息类型用于跟踪真/假条件的基本标志。
* 此数据类型的默认值为 `false`。
* 示例：`boolean check = true;`

### char

* `char` 信息类型是单精度 16 位 Unicode 字符。
* 最大值为 `65535`。
* 最小值为 `0`。
* `char` 信息类型用于存储任何字符。
* 示例：`boolean check = true`

* `char` 信息类型是单精度 16 位 Unicode 字符。（注：此处原文存在重复，已按要求翻译）
* 最大值为 `65535`。
* 最小值为 `0`。
* `char` 信息类型用于存储任何字符。
* 示例：`boolean check = true`

*(注：由于原文中 `char` 之后的部分出现了重复，译文已根据原文结构进行对应处理)*

- 这些变量没有默认值。因此，在第一次使用之前，应该声明局部变量并赋予初始值。

### 示例实现

在这里，`age` 是一个局部变量。它在 `pupage()` 策略内部被定义，并且其作用范围仅限于此系统。

```java
public class myTest{
    open void newfunc(){
        int myvar = 1;
        myvar = myvar + 10;
        System.out.println("The value of myvar is: " + myvar);
    }
    public static void main(string args[]){
        mytest = new myTest ();
        mytest.myfunc();
    }
}
```

该代码执行的输出为：
```
The value of myvar is: 11
```

### 实例变量

- 实例变量的声明在类内部。但是，它是在系统、构造函数或任何作用域之外定义的。
- 实例变量在使用 `new` 关键字创建对象时创建，在对象销毁时销毁。
- 当内存中为对象分配空间时，会为每个变量值创建一个空间。
- 实例变量可以在类级别在使用前或后声明。
- 实例变量持有的值必须被多个方法、构造函数或部分引用，或者是在整个类中必须可用的对象关键部分。
- 可以为实例变量指定访问修饰符。
- 实例变量有默认值。对于数字，默认值是 `0`。然而，对于布尔值，它是 `false`，对于对象引用，它是无效的。值可以在赋值语句中或构造函数内部分配。
- 实例变量对于类中的所有方法、构造函数和作用域都是唯一的。通常，建议将这些变量设为 `private`（访问级别）。但是可以使用访问修饰符为这些变量赋予子类可见性。
- 可以通过在类内部调用变量名来获取实例变量。可以使用以下语句：`Objectreference.variablename`。

### 示例实现

```java
import java.io.*;

public class Employeerecord{
    public String empname;
    private double empcompensation;
    public Employee (String name){
        empname = name;
    }
    public void initsalary(double empsalary){
        empcompensation = empsalary;
    }
    public void printemployee(){
        System.out.println("Employee name  : " + empname );
        System.out.println("Employee salary :" + empcompensation);
    }
    public static void main(string args[]){
        Employeerecord employee1 = new Employeerecord("Mary");
        employee1.initsalary(7500);
        employee1.printemployee();
    }
}
```

编译和执行将产生相应的结果：
```
Employee name  : Mary
Employee compensation :7500.0
```

### 类/静态变量

- 类变量（也称为静态变量）在类中使用 `static` 关键字声明，但在构造函数、方法或作用域之外。
- 每个类只有一个类变量的副本，无论从它创建了多少个对象。
- 静态变量除了被声明为常量外很少使用。常量是声明为 `private/public`、`static` 和 `final` 的变量。常量变量从初始值开始从未显示出变化。
- 静态变量存储在静态内存中。除了声明为 `final` 并作为私有或公共外，很少使用静态变量。
- 静态变量在系统启动时创建，在执行停止时销毁。
- 可见性与实例变量相似。在任何情况下，大多数静态变量都声明为 `public`，因为它们必须允许类的客户端访问。
- 这些变量的默认值与实例变量相同。对于数字，默认值通常为 `0`。然而，布尔值的相同值是 `false`，对象引用为无效。值可以在赋值语句中或构造函数内部分配。此外，值可以在唯一的静态初始化块中指定。
- 可以通过类名调用获取静态变量：`Classname.variablename`。
- 在将类变量声明为 `public static final` 时，变量名（常量）必须全部大写。此外，静态变量不是都是公有的，且命名规范与局部和实例变量相同。

### 示例实现

```java
import java.io.*;

public class Employeerecord{
    private static double empcompensation;
    public static final String empdept = "HR ";
    public static void main(string args[]){
        empcomp = 7500;
        System.out.println(empdept+" Compensation: "+empcompensation);
    }
}
```

该代码的编译和执行将产生相应的结果：
```
HR Compensation: 7500
```

### 修饰符类型

修饰符是添加到定义中以改变其含义的短语。Java 编程语言具有广泛且混合的修饰符，包括：
- 非访问修饰符
- Java 访问修饰符

为了使用修饰符，您将其短语包含在类、变量或方法的定义中。修饰符位于声明剩余内容的之前。

#### 访问控制修饰符

Java 提供了各种访问修饰符来设置类、变量、程序和构造函数的访问级别。四种访问权限是：
- `Private`：类内部可见。
- `Default`：包内可见。不需要修饰符。
- `Secured`：所有子类和包可见。
- `Public`：对全世界可见。

#### 非访问修饰符

Java 提供了各种非访问修饰符来实现其他用途。
- `Static`：用于类变量和方法。
- `Final`：用于结束类和方法。
- `Abstract`：用于创建抽象方法和类。
- `Volatile` 和 `Synchronized`：这些修饰符通常用于线程。

# Java 中的运算符

Java 中的运算符集非常丰富。广泛来说，Java 中的运算符分为以下几类：
- 关系运算符
- 算术运算符
- 逻辑运算符
- 位运算符
- 杂运算符
- 赋值运算符

### 算术运算符

Java 中的运算方式与代数相似。它们与变量用于算术运算。以下是 Java 可用的算术运算符列表。

| 操作 | 运算符 | 描述 |
| :--- | :--- | :--- |
| 加法 | `+` | 两个变量相加 |
| 减法 | `-` | 两个变量相减 |
| 乘法 | `*` | 两个变量相乘 |
| 除法 | `/` | 两个变量相除 |
| 取模 | `%` | 结果为余数 |
| 递增 | `++` | 增加 1 |
| 递减 | `--` | 减少 1 |

### 关系运算符

Java 还支持多种关系运算符。Java 支持的关系运算符列表所示。

| 操作 | 运算符 | 描述 |
| :--- | :--- | :--- |
| 等于 | `==` | 比较两个变量值的相等性 |
| 不等于 | `!=` | 比较两个变量值的不等性 |
| 大于 | `>` | 检查一个值是否大于另一个值 |
| 小于 | `<` | 检查一个值是否小于另一个值 |
| 大于等于 | `>=` | 检查一个值是否大于或等于另一个值 |
| 小于等于 | `<=` | 检查一个值是否小于或等于另一个值 |

### 位运算符

Java 中提供的位运算运算符可以轻松地应用于多种数据类型。这些数据类型包括 `byte`、`short`、`long`、`int` 和 `char`。通常，任何位运算运算符都会按位执行相关操作。例如，考虑整数 `x`，其值为 `60`。因此，`x` 的二进制等价值为 `00111100`。考虑另一个变量 `y`，其值为 `13` 或 `00001101`。如果我们对这两个数字执行位与运算 `&`，你将得到以下结果：

```
x&y = 0000 1100
```

下表显示了 Java 中可用的位运算符列表。

| 运算 | 运算符 | 描述 |
| :--- | :--- | :--- |
| 二进制与 | `&` | 执行与逻辑运算 |
| 二进制或 | `|` | 执行或逻辑运算 |
| 二进制异或 | `^` | 执行异或逻辑运算 |
| 各位反码 | `~` | 对一元变量执行取反操作 |
| 二进制左移 | `<<` | 执行位的左移 |
| 二进制右移 | `>>` | 执行位的右移 |

除了上述运算符外，Java 还支持右移零填充运算符（`>>>`），它会将移位后的右侧填充零。

# 逻辑运算符

逻辑运算符是任何运算符集中不可或缺的一部分。Java 支持的逻辑运算符如表所示。

| 运算 | 运算符 | 描述 |
| :--- | :--- | :--- |
| 逻辑与 | `&&` | 如果两个条件都为真，则返回 True |
| 逻辑或 | `||` | 如果提到的一个或两个条件为真，则返回 True |
| 逻辑非 | `!` | 如果提到的条件为假，则返回 True |

# 赋值运算符

Java 语言支持以下赋值运算符：

| 运算 | 运算符 | 描述 |
| :--- | :--- | :--- |
| 赋值运算符 | `=` | 将右侧的值赋给左侧变量 |
| 加赋值运算符 | `+=` | 将右侧的值加左侧变量的值，并将结果赋给左侧变量 |
| 减赋值运算符 | `-=` | 将右侧的值减左侧变量的值，并将结果赋给左侧变量 |
| 乘赋值运算符 | `*=` | 将右侧的值乘以左侧变量的值，并将结果赋给左侧变量 |
| 除赋值运算符 | `/=` | 将右侧的值除以左侧变量的值，并将结果赋给左侧变量 |
| 取模赋值运算符 | `%=` | 取左侧和右侧的模（余），并将结果赋给左侧变量 |
| 左移赋值运算符 | `<<=` | 取左侧和右侧的左移，并将结果赋给左侧变量 |
| 右移赋值运算符 | `>>=` | 取左侧和右侧的右移，并将结果赋给左侧变量 |
| 位赋值运算符 | `&=` | 取左侧和右侧的位与结果，并将结果赋给左侧变量 |
| 位异或赋值运算符 | `^=` | 取左侧和右侧的位异或结果，并将结果赋给左侧变量 |
| 位或赋值运算符 | `|=` | 取左侧和右侧的位或结果，并将结果赋给左侧变量 |

# 杂项运算符

除了上述运算符，Java 还支持其他几种运算符。

## 条件运算符 ( ? : )

条件运算符是一个包含三个操作数的三元运算符。本质上，该运算符用于评估布尔表达式。该运算符测试第一个操作数或条件，如果条件为真，则将第二个值赋给变量。然而，如果条件为假，则将第三个操作数赋给变量。该运算符的语法如下：

```
variable a = (<condition>) ? truevalue : falsevalue
```

示例代码实现：

```java
public class myTest {
    public static void main(String args[]){
        int x, y;
        x = 5;
        y = (x == 5) ? 15: 40;
        System.out.println( "y = " + y );
        y = (x == 34) ? 60: 95;
        System.out.println( "x = " + y );
    }
}
```

该代码的编译和执行将产生以下结果：

```
y = 15
y = 95
```

## instanceof 运算符

只有对象引用变量可以使用此运算符。该运算符的目的是检查一个对象是否是某个现有类的实例。该运算符的语法如下：

```
(<object reference variable>) instanceof(<interface/class>)
```

下面给出了该运算符的用途示例实现：

```java
public class myTest {
    public static void main(String args[]){
        int x = 4;
        boolean resultant = x instanceof int;
        System.out.println( resultant );
    }
}
```



此代码的输出应为`true`。该运算符也可以用于比较。

## Java 运算符优先级

通常情况下，运算符会被组合使用。下表说明了运算符的顺序。例如，如果在同一个表达式中执行加法和乘法，乘法先执行。所有运算符的结合性是从左到右。然而，一元运算符和赋值运算符是从右到左。

| 运算符 | 类别 |
| :--- | :--- |
| `()` `[]` `.` (点运算符) | 后缀 |
| `++` `-` `~` | 一元 |
| `*` `/` `%` | 乘法 |
| `+` `-` | 加法 |
| `>>` `<<` | 移位 |
| `>=` `<=` | 关系 |
| `==` `!=` | 等于 |
| `&` | 位与 |
| `|` | 位或 |
| `^` | 位异或 |
| `&&` | 逻辑与 |
| `||` | 逻辑或 |
| `?:` | 条件 |
| `=` `+=` `/=` `>>=` `<<=` `&=` `^=` `|=` | 赋值 |
| `,` | 逗号 |

## Java 中的循环

循环是一种常见的编程场景。循环简单地描述为需要重复执行某段代码的情况。Java 支持三种循环结构：

- `for`
- `do...while`
- `while`

此外，还存在`foreach`循环结构。不过，该结构将在数组章节介绍。

### while 循环

`while`循环允许你执行特定次数的任务。该结构的语法如下：

```
while(布尔表达式) {
    //语句
}
```

执行时，如果布尔表达式的结果为真，则执行循环内部的操作。这将一直持续直到条件结果为假。这里循环的关键在于可能永远不运行。当尝试结果为假时，循环体将被跳过，执行`while`循环后的第一个语句。

示例：

```java
public class myTest {
    public static void main(String args[]) {
        int i=5;
        while(i<10) {
            System.out.print(" i = " + i );
            i++;
            System.out.print("\n");
        }
    }
}
```

这将产生相应的结果：

```
x = 5
x = 6
x = 7
x = 8
x = 9
x = 5
```

### do...while 循环

`do...while`循环与`while`循环相似，不同在于`do...while`循环确保至少执行一次。该结构的语法如下：

```
do {
    //Statements
} while(<booleanexpression>);
```

注意到，布尔声明出现在循环的末尾，因此代码在尝试布尔值之前会执行一次。如果布尔声明为真（`true`），控制流将向下执行，代码将再次执行一次。这种方法会一直重复直到布尔表达式为假（`false`）。

示例实现：

```java
public class myTest {
    public static void main(String args[]){
        int i = 1;
        do{
            System.out.print("i = " + i );
            i++;   
            System.out.print("\n");
        } while( i<1 );
    }
}
```

这将产生相应的的结果：

`i = 1`

### for 循环

`for`循环是一种迭代控制结构，允许你有效地构建一个需要执行特定次数的循环。当你知道某个任务需要重复多少次时，`for`循环结构非常有帮助。循环结构的语法如下：

`for`循环的标点符号为：

`for(initialization; Boolean_expression; redesign)`
{
    `/Statements`
}

以下是`for`循环中的控制流：

*   初始化步骤首先执行且仅执行一次。此步骤允许你声明并引入任何循环控制变量。你不需要在这里进行声明，只需一个分号即可。
*   接下来，评估布尔表达式。如果它为真，则执行循环体。如果它为假，则不执行循环体，且控制流跳转到`for`循环之后的后续语句。
*   在`for`循环体执行后，控制流将向下跳转到重赋值语句。该语句允许你更新任何循环控制变量。该语句可以留空，在布尔声明后跟一个分号即可。
*   再次评估布尔表达式。如果它为真，则执行循环并重进入范围。当布尔表达式为假后，`for`循环结束。

#### 示例实现

```java
public class myTest {
    public static void main(String args[]) {
        for(int i = 0; i < 5; i = i+1) {
            System.out.print("i = " + i );
            System.out.print("\n");
        }
    }
}
```

这将交付相应的结果：

`i = 0`
`i = 1`
`i = 2`
`i = 3`
`i = 4`

### Java 中 for 循环的扩展版本

从 Java 5 开始引入了增强`for`循环。这主要用于数组（`Arrays`）。该循环的语法如下：

`for(declaration : statement)`
{
    `//Statements`
}

*   **声明 (`Declaration`)**：新声明的变量，其类型与你正在访问的数组组件类型匹配。该变量在`for`块内部是可用的，其值与当前数组组件相同。
*   **表达式 (`Expression`)**：这评估你要遍历的对象。解释可以是一个数组变量，也可以返回数组的函数调用。

#### 示例实现：

```java
public class myTest {
    public static void main(String args[]){
        int [] mynumber = {0, 5, 10, 15, 20};
        for(int i : mynumber ){
            System.out.print( i );
            System.out.print(" ,");
        }
    }
}
```

这将交付相应的结果：

`0, 5, 10, 15, 20`

### break 关键字

`break`关键字用于停止整个循环的执行。`break`语句必须在任何循环或`switch`结构内部。`break`关键字将停止最深循环的执行，并开始执行大括号之后的下一行代码。使用该关键字的语法如下：

`break;`

#### 示例实现：

```java
public class myTest {
    public static void main(String args[]) {
        int [] mynumbers = {0, 5, 10, 15, 20};
        for(int i : mynumbers ) {
            if( i == 15 ) {
                break;
            }
            System.out.print( i );
            System.out.print("\n");
        }
    }
}
```

这将交付相应的结果：

`0`
`5`
`10`

### continue 关键字

`continue`语句可以作为任何循环控制结构的一部分。它导致循环快速跳转到循环的下一个语句。

*   在`for`循环中，`continue`关键字控制流快速跳转到重赋值语句。
*   在`while`或`do/while`循环中，控制流立即跳转到布尔表达式。

使用该关键字的语法如下：

`continue;`

#### 示例实现：

```java
public class myTest {
    public static void main(String args[]) {
        int [] mynumbers = {0, 5, 10, 15, 20};
        for(int i : mynumbers ) {
            if( i == 15 ) {
                continue;
            }
            System.out.print( i );
            System.out.print("\n");
        }
    }
}
```

## if 语句

`if`语句是一种决策构造，允许根据条件执行不同代码块。其基本语法如下：

```
if(condition) {
    //Statements when condition is true
} else {
    //Statements when condition is false
}
```

`if`语句可以嵌套使用，也可以在条件中使用逻辑运算符组合多个条件。

### 示例实现：

```java
public class myTest {
    public static void main(String args[]) {
        int x = 10;
        if(x < 20) {
            System.out.println("The if construct is executing!");
            if(x > 5) {
                System.out.println("The nested if construct is executing!");
            }
        } else {
            System.out.print("The else construct is executing!");
        }
    }
}
```

这将产生相应的结果：
`The if construct is executing!`
`The nested if construct is executing!`

## switch 语句

`switch`结构允许对变量与一系列值进行等效比较。每个值被称为一个`case`，并对每个`case`对正在交换的变量进行检查。使用此决策构造的语法如下：

```
switch(<condition>){
    case value1:
        //Statements
        break;
    case value2:
        //Statements
        break;
    default:
        //Optional
}
```

以下规则适用于`switch`结构：
- 作为`switch`解释部分的变量必须是`short`、`byte`、`char`或`int`类型。
- 你可以在`switch`内部包含任意数量的`case`解释。每个`case`后面都跟着一个待对比的值和一个冒号。
- `case`的值必须与`switch`中的变量类型相同，并且必须是一个常量或确切的值。
- 当正在交换的变量与某个`case`相同时，该`case`之后的声明将执行，直到遇到`break`。
- 当遇到`break`时，`switch`结束，控制流跳转到`switch`之后的行。
- 并不是每个`case`都需要包含`break`。如果没有出现`break`，控制流将继续渗透到后续的`case`，直到遇到`break`为止。
- `switch`语句可以有一个可选的`default`情况，它必须显示在`switch`的末尾。`default`情况用于在没有一个`case`为真时执行某些操作。`default`情况中不需要`break`。但是，根据惯例，建议使用。

### 示例实现

```java
public class myTest {
    public static void main(String args[]){
        char mygrade = 'A';
        switch(mygrade)
        {
            case 'A' :
                System.out.println("Excellent Performance!");
                break;
            case 'B' :
                System.out.println("Good Performance!");
                break;
            default :
                System.out.println("Failed");
        }
    }
}
```

使用不同的等级输入汇总并运行上述代码。对于`mygrade`的当前值，这将产生相应的结果：
`Excellent Performance!`

## Java 中的字符串

字符串（Strings）通常作为 Java 计算机程序的一部分，是字符的组合。在 Java 编程语言中，字符串与其他一切一样，都是对象。Java 平台提供了`String`类来创建和控制字符串。

### 实例化字符串

创建字符串最合适的方法是使用以下语句：

```java
String mystring = "Hi world!";
```

在代码中任何地方遇到确切的字符串时，编译器都会为该情况创建一个其值为"Hi world!"的`String`对象。

同样，与其他对象一样，你可以利用构造函数和`new`关键字来创建字符串。`String`类有 11 个构造函数，允许你利用不同的源（例如字符数组）提供字符串的初始估计。

```java
public class myStringdemo{
    public static void main(String args[]){
        char[] myarray = { 'h', 'i', '.'};
        String mystring = new String(myarray);
        System.out.println( mystring );
    }
}
```

这将交付相应的结果：
`hi.`

**注意**：`String`类是不可变的，因此一旦创建为`String`对象，其类型就无法更改。如果需要对字符字符串进行大量更改，那么你应该使用`StringBuffer`和`StringBuilder`类。

### 确定字符串长度

用于获取对象数据的方法称为访问器方法（accessor methods）。你可以与字符串一起使用的访问技术是`length()`函数，它提供字符串项中包含字符的比例返回。该函数可以如下所示使用：

```java
public class mystring {
    public static void main(String args[]) {
        String newstr = "I am hungry!";
        int strlen = newstr.length();
        System.out.println( "length = " + strlen );
    }
}
```

这将产生相应的结果：
`length = 12`

### 如何拼接字符串

`String`类包含一个用于连接两个字符串的函数：

```java
mystring1.concat(mystring2);
```

这返回另一个字符串，它是向`mystring1`的末尾添加了`mystring2`的字符串。你同样可以使用字符串字面量使用`concat()`系统，例如：

```java
"My name is ".concat("mary");
```

字符串通常还使用`+`运算符进行拼接，例如：

```java
"Hi," + " world" + "!"
```

导致：
`"Hi, world!"`

### 示例实现

```java
public class MyString {
    public static void main(String args[]) {
        String mystr = "Sorry";
        System.out.println("I " + "am " + mystr);
    }
}
```

这将交付相应的结果：
`I am Sorry`

### 格式化字符串

你有`format()`和`printf()`函数来打印带有设计的数字输出。`String`类的`format()`函数返回一个格式化的`String`对象。该函数可以如下所示使用：

```java
String fstr;
fstr = String.format("Float value " + "%f, and Integer value " + "%d", fVar, iVar);
System.out.println(fstr);
```



### String 方法

此部分包含了作为`String`类的方法列表。

- `compareTo(Object obj)` – 该函数将字符串与对象比较。
- `charAt(int index)` – 该函数返回索引处的字符。
- `compareToIgnoreCase(String mystr)` – 该函数执行两个字符串的字典比较。但是，该函数忽略大小写差异。
- `compareTo(String aString)` – 该函数执行字符串之间的字典比较。
- `contentEquals(StringBuffer strb)` – 该函数检查字符串是否与`StringBuffer`中的字符序列相同。成功返回`true`，失败返回`false`。
- `concat(String strnext)` – 该函数在末尾拼接另一个字符串。
- `copyValueOf(char[] mydata, int xoffset, int xcount)` – 该函数返回一个指示原始字符串字符序列的字符串。
- `copyValueOf(char[] newdata)` – 该函数将字符串拷贝到字符序列形式的字符缓冲区。
- `equals(Object aObject)` – 该函数将对象与字符串比较。
- `endsWith(String newsuffix)` – 该函数带有指定的后缀结束字符串。
- `getBytes()` – 使用此函数，可以将字符串编码为字节格式，存储在结果数组中。
- `equalsIgnoreCase(String aString)` – 该函数在不考虑字符大小的情况下对两个字符串进行比较。
- `getChars(int srcBegin, int sourceEnd, char[] dst, int destinationBegin)` – 该函数将从指定的起始字符到结束字符的字符拷贝到数组。
- `getBytes(String charsetnm)` – 使用此函数，可以将字符串使用命名字符集编码为字节格式，存储在结果数组中。
- `indexOf(int charx)` – 该函数返回函数调用中指定的相同字符的索引。
- `hashCode()` – 由字符串返回一个哈希值。
- `indexOf(String newstr)` - 该函数返回子字符串在字符串中首次出现的索引。
- `indexOf(int charx, int fromIndexloc)` – 该函数返回函数调用中指定的相同字符的索引。搜索从指定的索引开始。
- `String intern()` – 返回函数调用中给出的字符串对象的规范表示。
- `int indexOf(String newstr, int fromIndexloc)` - 此函数返回子字符串在字符串中首次位置的索引。搜索从指定的索引开始。
- `int lastIndexOf(int charx, int fromIndexloc)` - 此函数从指定的索引开始搜索字符，并返回最后一次找到的索引。
- `int lastIndexOf(int charx)` - 此函数反向搜索字符，并返回最后一次出现（或反向搜索中的首次出现）的索引。
- `int lastIndexOf(String newstr, int fromIndexloc)` – 此函数从指定的索引搜索子字符串，并返回最后一次出现的索引。
- `int lastIndexOf(String newstr)` - 此函数反向搜索子字符串，并返回最后一次出现（或反向搜索中的首次出现）的索引。
- `boolean matches(String aregex)` - 此函数检查字符串区域与正则表达式之间的相等性。
- `int length()` – 此函数计算并返回字符串长度。
- `boolean regionMatches(int totaloffset, String otherstr, int otheroffset, int strlen)` – 此函数检查字符串区域之间的相等性。
- `boolean regionMatches(boolean ignorecharcase, int totaloffset, String otherstr, int otheroffset, int strlen)` – 此函数检查字符串区域之间的相等性。
- `String replace(char oldCharx, char newCharx)` - 此函数查找匹配正则表达式的子字符串，然后将所有出现的地方替换为指定的字符串。函数返回执行所有替换后得到的所得字符串。
- `String replaceFirst(String newregex, String newreplacement)` – 此函数查找匹配正则表达式的子字符串，然后将第一次出现的地方替换为指定的字符串。
- `String replaceAll(String newregex, String xreplacement)` - 此函数查找匹配正则表达式的子字符串，然后将所有出现的地方替换为指定的字符串。
- `String[] split(String newregex, int xlimit)` – 此函数根据正则表达式和给定限制对字符串进行分割。
- `String[] split(String newregex)` - 此函数根据正则表达式对字符串进行分割。
- `boolean startsWith(String newprefix, int totaloffset)` – 此函数检查给定字符串在指定索引处是否具有前缀。
- `boolean startsWith(String newprefix)` – 此函数检查给定字符串是否以函数调用发送的前缀开头。
- `String substring(int beginIndexloc, int endIndexloc)` - 此函数返回一个字符串，它是指定字符串的子字符串。子字符串由起始索引到字符串结尾决定。
- `CharSequence subSequence(int beginIndexloc, int endIndexloc)` - 此函数返回一个字符序列，它是指定字符序列的子字符序列。子字符串由起始和结束索引决定。
- `char[] toCharArray()` – 此函数执行字符串到字符数组的转换。
- `String substring(int beginIndexloc, int endIndexloc)` – 此函数返回一个字符串，它是指定字符串的子字符串。子字符串由起始和结束索引决定。
- `String toLowerCase(Locale localenew)` - 此函数使用指定的区域规则将指定字符串中的所有字符转换为小写。
- `String toLowerCase()` - 此函数使用默认区域规则将指定字符串中的所有字符转换为小写。
- `String toUpperCase()` - 此函数使用默认区域规则将指定字符串中的所有字符转换为大写。
- `String toString()` – 此函数返回字符串本身。
- `String toUpperCase(Locale localenew)` – 此函数使用区域规则将指定字符串中的所有字符转换为大写。
- `static String valueOf(primitive data type x)` – 此函数返回原始数据类型的字符串表示。
- `String trim()` – 去除字符串前后的空白字符。

# 数组 (Arrays)

Java 支持类似于集群的信息结构。这种信息结构被称为数组。它能够存储相同数据类型组件的连续变尺寸累积。数组被用于存储信息的累积，但将其视作存储同类变量的展示通常更有价值。

与声明单个变量（例如，`num0`、`num1` 和 `num99`）相比，你可以声明一个数组变量。例如，一个包含四个元素的数组被声明为`arrayname[4]`。本章将讨论数组声明、访问和操作的所有方面。

## 如何声明数组变量

要将数组作为系统的一部分，必须声明一个变量来引用该数组。此外，你必须确定该变量可以引用的数组类型。以下是声明类型变量的语法：

`datatype[] myarray;`

### 示例实现：

随附的代码是该概念的说明：

```
double[] myarray;
```

## 创建数组

你可以利用`new`运算符配合以下语句来创建一个实例：

```
myarray = new datatype[sizeofarray];
```

上述声明执行了两件事：

* 它通过`new`运算符按照如下方式创建一个实例：
  `new datatype[arraysize];`
* 它将新创建数组的引用分配给变量`myarray`。

声明数组变量、创建实例并将展示的引用分配给变量可以合并在一个声明中，如下所示：

```java
datatype[] myarray = new datatype[sizeofarray];
```

另一方面，你也可以通过以下方式创建实例：

```java
datatype[] myarray = {val0, val1, ..., valk};
```

数组的元素从 0 开始；即，它们从 0 到`myarray.length-1`。

### 示例实现：

以下声明创建了一个 10 个元素的 double 类型数组：

`double[10]`

## 处理数组

在处理数组组件时，我们使用`for`或`foreach`，因为数组的组件具有相同类型且数组的大小是已知的。例如，随附的方法展示了 int 数组中的组件：

```java
public class Mytestarray {

    public static void main(string[] args) {

        double[] myarray = {0.5, 1.2, 2.2, 3.4, 4.7};

        for (int k = 0; k < myarray.length; k++) {

            System.out.println(myarray[k] + " ");

        }

        double aggregate = 0;

        for (int k = 0; k < myarray.length; k++) {

            aggregate += myarray[k];

        }

        System.out.println("Aggregate = " + aggregate);

        double maxval = myarray[0];

        for (int k = 1; k < myarray.length; k++) {

            if (myarray[k] > maxval)

                maxval = myarray[k];

        }

        System.out.println("Max Value is " + maxval);

    }

}
```

这将产生随附的结果：

```
0.5 1.2 2.2 3.4 4.7
Aggregate = 12.0
Max Value is 4.7
```

## foreach 循环

JDK 1.5 引入另一种`for`结构，被称为`foreach`循环或扩展`for`循环。这种结构允许你连续遍历整个数组，而无需额外的变量。

### 示例实现：

```java
public class Mytestarray {

    public static void main(string[] args) {

        double[] myarray = {0.5, 1.2, 2.2, 3.4, 4.7};

        for (double i: myarray) {

            System.out.println(i);

        }

    }

}
```

这将交付随附的结果：

```
0.5 1.2 2.2 3.4 4.7
```

## 将数组传递给方法：

通常，正如你可以将原始值传递给方法或函数一样，你也可以将数组传递给系统。例如，随附的方法展示了 int 数组中的组件：

```java
public static void printarr(int[] arr) {

    for (int k = 0; k < arr.length; k++) {

        System.out.print(arr[k] + " ");

    }

}
```

你可以通过传递一个数组来调用它。例如，下方的声明调用了`printarr`函数来显示数组的元素。

```java
printarr(new int[]{0, 3, 5, 3, 1});
```

这段代码的编译和执行将产生以下结果：

```
0 3 5 3 1
```

## 方法如何返回数组

系统同样可以返回一个数组。例如，下面演示的方法返回了另一个数组的反转后的数组：

```java
public static int[] revarr(int[] myarr) {

    int[] resultarr = new int[myarr.length];

    for (int k = 0, i = resultarr.length - 1; k <= myarr.length/2; k++, i-- ) {

        resultarr[j] = myarr[k];

    }

    return resultarr;

}
```

## Arrays 类

`java.util.arrays`类包含了不同的函数，用于对数组进行排序、查找数组值、查看数组以及向数组中填充组件。这些函数适用于所有原始数据类型。

* `public static boolean equals(long[] a, long[] a2)` - 如果两个指定的数组相互对等，则返回`true`。如果两个数组包含相同数量的组件，且两个数组中所有相关的组件都是等等的，则认为这两个数组是等等的。如果两个数组相等，则返回`true`。所有其他原始数据类型也可以使用相同的函数。
* `public static int binarysearch(object[] an, Object key)` - 利用二分查找在指定的`Object`数组中查找定义的值。在进行此调用之前，必须对数组进行排序。如果该键在列表中，则返回键的列表；通常情况下返回`(-(插入点 + 1))`。
* `public static void sort(Object[] a)` – 此函数可以用于对给定的数组进行升序排序。它也可以用于任何数据类型。
* `public static void fill(int[] an, int val)` - 为指定的 int 数组的每个组件分配详细的 int 值。相同的函数也可以用于其他数据类型的数组。

## 正则表达式

Java 包含了`java.util.regex`包来匹配正则表达式。Java 的正常输出在根本上与 Perl 编程语言相同，并且易于学习。正则表达式是一系列连续的字符序列，可以帮助你利用特定的语法来匹配或发现不同的字符串或字符串集。它们可以用于查找、修改或控制内容和信息。`java.util.regex`包本质上包含以下三个类：

* **Pattern 类**：`Pattern`实例是正则表达式的编译表示。`Pattern`类没有任何公共构造函数。要创建一个实例，你应该首先调用它的公共静态方法，这将返回一个`Pattern`对象。这些函数接受一个字符串作为第一个参数。
* **Matcher 类**：`Matcher`实例是翻译并并信息字符串执行匹配操作的引擎。与`Pattern`类一样，`Matcher`没有公共构造函数。你通过在`Pattern`对象上调用`matcher`方法获取`Matcher`对象。
* **Patternsyntaxexception**：`Patternsyntaxexception`对象是一个未检查的异常，用于显示正则表达式语句设计中的句结构错误。

### 捕获组

捕获组是一种将各种字符视为一个问题单元的方法。它们通过将要组合的字符放在一组括号内来实现。例如，正则表达式`(canine)`建立了一个包含字母 "d"、"o" 和 "g" 的单一分组。捕获组通过从左到右对它们的起始括号进行编号。例如，在表示`((A)(b(c)))`中，有四个这样的组：

* `(a)`
* `(c)`
* `(b(c))`
* `((a)(b(c)))`

要发现声明中可可用多少个捕获组，请在`matcher`对象上调用`groupcount`方法。`groupcount`方法返回一个`int`，表示`matcher`表达式中显示的捕获组数量。还有一个特殊的组，`group 0`，它可靠地代表整个输出。该组排除在`groupcount`报告的总数之外。

### 示例实现：

此示例代码模拟了如何从给定的字母数字字符串中提取数字字符串：

```java
import java.util.regex.matcher;

import java.util.regex.pattern;

public class Myregexmatches {

    public static void primary( String args[] ){

        String line = "Request for Qt3000! ";

        String example = "(.*)(\\d+)(.*)";

        Pattern myr = Pattern.compile(pattern);

        Matcher mym = myr.matcher(line);

        if (mym.find( )) {

            System.out.println("Value = " + mym.group(0) );

            System.out.println("Value = " + mym.group(1) );
```



`System.out.println("Value = " + mym.group(2) );`

```java
} else {
    System.out.print("No match found!");
}
```

## 正则表达式语法

下面是正则表达式语法的参考列表。

| 匹配 | 表达式 |
| :--- | :--- |
| 行开始 | `^` |
| 行结束 | `$` |
| 除换行符以外的字符 | `.` |
| 括号内的字符 | `[...]` |
| 不在括号内的字符 | `[^...]` |
| 字符串开始 | `\A` |
| 字符串结束 | `\z` |
| 除结尾以外的字符串结束 | `\Z` |
| 0 次或多次实例 | `*` |
| 1 次或多次实例 | `+` |
| 0 或 1 次实例 | `?` |
| 确定的 n 次 | `{n}` |
| n 次或更多实例 | `{n,}` |
| n 次到 m 次实例 | `{n, m}` |
| a 或 b 之一 | `a\|b` |
| 分组并记住文本 | `(re)` |
| 分组但不记入文本 | `(?: re)` |
| 独立模式，不支持回溯 | `(?> re)` |
| 单词字符 | `\w` |
| 非单词字符 | `\W` |
| 空白 | `\s` |
| 非空白 | `\S` |
| 数字 | `\d` |
| 非数字 | `\D` |
| 上次匹配结束的位置 | `\G` |
| 组 n 反引用 | `\n` |
| 单词边界（在括号内为退格符） | `\b` |
| 非单词边界 | `\B` |
| 回车、换行和制表符 | `\n`, `\t` 等 |
| 转义所有字符直到 `\E` | `\Q` |
| 结束以 `\Q` 开始的引号 | `\E` |

## Matcher 类的方法

### 索引方法

下表列出了在信息字符串中正确显示匹配位置的方法：

- `public int start(int bunch)`: 提供上次匹配中指定组的捕获内容的起始索引。
- `public int begin()`: 提供上次匹配的起始索引。
- `public int end(int bunch)`: 提供上次匹配中指定组的捕获内容的最后一个字符之后的结束索引。
- `public int end()`: 提供最后一个匹配字符之后的结束索引。

### 研究方法

研究方法调查字符串并返回一个布尔值表示是否找到了示例：

- `public boolean find()`：尝试在信息安排中发现匹配示例的后续子序列。

## 方法

- `public boolean lookingat()`：尝试从区域的开始处将信息排列与示例进行匹配。
- `public boolean matches()`：尝试将整个区域与示例进行匹配。
- `public boolean find(int begin)`：重置此匹配器，然后尝试从指定的列表开始，发现信息分组中匹配示例的后续子序列。

### 替换方法

替换方法是替换数据字符串中内容的有效方法：

- `public static String quotereplacement(string mystr)`：为被标记的 `String` 返回一个精确的替换 `String`。此方法创建一个 `String`，将作为 `Matcher` 类中 `appendreplacement` 系统中的问题替换 `s`。
- `public Stringbuffer appendtail(stringbuffer strbuff)`：执行一个末尾附加和替换步骤。
- `public Matcher appendreplacement(stringbuffer strbuff, String strsubstitution)`：执行一个非终端附加和替换步骤。
- `public String replacefirst(string strsubstitution)`：将数据序列中第一个匹配示例的子序列替换为指定的替换字符串。
- `public String replaceall(string strsubstitution)`：将数据序列中每个匹配示例的子序列替换为指定的替换字符串。

### begin 和 end 方法

以下是统计语句 "felines" 在数据字符串中出现次数的示例：

```java
import java.util.regex.pattern;
import java.util.regex.matcher;

public class Regexmatches {
    private static last String INPUT = "feline cattie feline";
    private static last String REGEX = "\\bcat\\b";

    public static void principle( String args[] ){
        Pattern myp = Pattern.compile(regex);
        Matcher mym = myp.matcher(input);
        int checkval = 0;

        while(mym.find()) {
            count++;
            System.out.println("match number "+count);
            System.out.println("start(): "+mym.start());
            System.out.println("end(): "+mym.end());
        }
    }
}
```

你可以看到此示例使用了单词边界来确保字母 "c" "a" "t" 不仅仅是长单词中的子字符串。它还提供了关于匹配发生在信息字符串中位置的有用数据。`begin` 技术返回上一次匹配操作中由给定组捕获的子序列的记录，而 `end` 提供最后一个匹配字符的相应返回，外加一。

### matches 和 lookingat 方法

`matches` 和 `lookingat` 方法都尝试将信息序列与示例进行匹配。区别在于，`matches` 要求匹配整个输入分组，而 `lookingat` 不需要。两种技术都可靠地从数据字符串开始开始。

### replacefirst 和 replaceall 方法

`replacefirst` 和 `replaceall` 程序替换匹配给定标准表示的内容。如其名称所示，`replacefirst` 替换第一次，而 `replaceall` 替换所有事件。

### appendreplacement 和 appendtail 方法

`Matcher` 类额外提供了 `appendreplacement` 和 `appendtail` 程序用于替换。

### PatternSyntaxException 类方法

`PatternSyntaxException` 是一种异常，它是未检查的。此异常表示正则表达式模式中的语法错误。`PatternSyntaxException` 类为开发者提供了以下方法供使用。

- `public int getIndex()`：此函数返回错误的索引。
- `public String getDescription()`：此函数返回错误的描述。
- `public String getMessage()`：此函数返回错误的描述和索引。
- `public String getPattern()`：此函数返回导致错误的正则表达式模式。

Java 方法是汇集以执行操作的说明的积累。例如，当你调用 `System.out.println` 函数时，框架执行几条语句以便在输出屏幕上显示消息。现在，你将学会如何带或不带返回值创建自己的方法，带或不带参数调用方法，使用相同名称的重载方法，以及在系统计划中应用方法。

### 如何创建方法

参考以下示例来明确方法的结构：

```java
public static int functionname(int x, int y) {
    //Statements
}
```

在这里，方法使用了以下元素：

- 修饰符：`public static`
- 返回值的数据类型：`int`
- 方法名：`functionname`
- 形式参数：`x`, `y`

此类结构也被称为函数（Functions）或过程（Procedures）。然而，这两者有一个不同的特性：

- 函数（Functions）：它们返回一个显式的值。
- 过程（Procedures）：它们不返回任何值。

函数定义由系统头和体组成。上述结构可以概括为以下安排：

`modifier returndatatype methodname (List of Parameter) { //Statements }`

上述结构包含了：

- 修饰符：它描述了进入方法的权限，且不是强制使用的。
- 返回类型：方法可以返回此数据类型的值。
- 方法名：这是方法名，由方法的名称和参数列表组成。
- 参数列表：参数的列表，包含方法参数的数据类型、请求和参数数量。方法也可以包含零个参数。
- 语句：方法体通过说明刻画了方法在做什么。

### 示例实现

这里是上述描述的方法 `maxval()` 的源代码。该技术接收两个参数 `number1` 和 `number2`，并提供两者之间的相应返回：

```java
public static int minval(int num1, int num2) {
    int minvalue;
    if (num1 > num2)
        minvalue = num2;
    else
        minvalue = num1;
    return minvalue;
}
```

### 调用方法

为了使用方法，必须对其进行调用。调用方法有两种方式，即技术返回一个值或没有（无返回值）。系统调用的方法很简单。当项目调用一个方法时，系统控制权转移到调用的方法。此调用的方法通过两种情况返回控制权给调用者。这些情况包括：

- 到达方法的闭括号。
- 执行了返回语句。

返回 `void` 的方法被视为声明的调用。让我们考虑一个示例：

```java
System.out.println("This is the end of the method!");
```

返回值的的方法可以通过示例看到：

```java
double resultant = sumval(4.2, 2.5);
```

### 示例实现

```java
public class Minnumber{
    public static void main(string[] args) {
        double x = 21.5;
        double y = 2.0;
        double z = minvalfunc (x, y);
        System.out.println("The returned value = " + z);
    }

    public static double minvalfunc (double num1, double num2) {
        double minvalue;
        if (num1 > num2)
            minvalue = num2;
        else
            minvalue = num1;
        return minvalue;
    }
}
```

这将产生相应的的结果：

```
The returned value = 2.0
```

### void 关键字

`void` 关键字允许我们创建不返回值的方法。在这里，在示例中我们正在考虑一个 void 方法。此函数是一个 `void` 方法，不返回任何值。对 `void` 系统的调用必须是一个声明，即 `rankpoints(657.3);`。它是以分号结尾的 Java 语句。

### 示例实现

```java
public class Myexample {
    public static void main(string[] args) {
        rankpoints(657.3);
    }

    public static void rankpoints(double valfoc) {
        if (valfoc >= 100.5) {
            System.out.println("A1 Rank");
        }
        else if (valfoc >= 55.4) {
            System.out.println("A2 Rank");
        }
        else {
            System.out.println("A3 Rank");
        }
    }
}
```

这将交付相应的结果：

```
A1 级
```

## 按值传递参数

在调用过程过程中工作时，需要传递内容。这些内容应当与函数调用中的特定参数在同一个请求中。参数可以通过引用或值来传递。按值传递参数意味着调用一个带有参数的方法。通过这种方式，内容值被传递给了参数。

### 示例实现

附带的项目演示了按值传递参数的说明。

```java
public class Myswapping {
    public static void main(string[] args) {
        double x = 0.43;
        double y = 34.65;
        System.out.println("Values of X and Y before swapping, x = " + x + " and y = " + y);
        myswapfunc (x, y);
        System.out.println("\nValues of X and Y after swapping: ");
        System.out.println("x = " + x + " and y is " + y);
    }

    public static void myswapfunc (int x, int y) {
        System.out.println("Inside the function: Values of X and Y before swapping, x = " + x + " y = " + y);
        System.out.println("Inside the function: Values of X and Y after swapping, x = " + x + " y = " + y);
    }
}
```

想要阅读更多内容，请在亚马逊搜索：“Java For Beginners A Simple Start To Java Programming Sanderson”
