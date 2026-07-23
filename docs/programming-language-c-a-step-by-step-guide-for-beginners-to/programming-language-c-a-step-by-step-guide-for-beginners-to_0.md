# C 语言编程：初学者一周快速学会指南



![](img/Image0000.jpg)


## 目录
- 标题页
- 关于本书 - 什么是 C？
- 编程基础
- 数据类型
- 决策控制语句
- C 语言中逻辑运算符的使用
- 循环控制语句
- 分支控制语句
- 存储类
- 函数
- 指针
- 数组
- 字符串
- 结构体
- printf 和 scanf
- 预处理器指令
- 文件操作
- C – 类型定义, C – 联合体
- 关于作者

## 关于本书
`C 编程语言`向你介绍了最常用的编程语言，多年来，它一直是许多其他版本语言的基础。这是一本非常好的书，不仅适合初学者，也适合那些希望在操作各种计算机程序时，了解其后台运行机制的计算机用户。

在本书书中，你将学习`C 编程语言`包含的内容，学习如何编写条件、表达式、语句甚至是命令，以便该语言能够高效地执行其功能。你还将学习如何组织相关的表达式，以便在编译和执行后，计算机返回的是有用的结果而不是错误信息。此外，本书还详细介绍了`C 语言`中所需的数据类型以及如何表示这些数据类型。

简单来说，这是一本为程序员、修读其他计算机课程的学习者，以及其他想要精通最流行的计算机语言`C`工作原理的计算机用户编写的教程。

书籍内容如下：
- 什么是 C
- 编程基础
- 数据类型
- 标记与关键字
- 决策控制语句
- C 语言中逻辑运算符的使用
- 循环控制语句
- 分支控制语句
- 存储类
- 函数
- 指针
- 数组
- 字符串
- 结构体
- 预处理器指令
- 文件操作
- 类型定义 – 联合体

## 引言
`C 编程语言`向你介绍了最常用的编程语言，多年来，它一直是许多其他版本语言的基础。这是一本非常好的书，不仅适合初学者，也适合那些希望在操作各种计算机程序时，了解其后台运行机制的计算机用户。

在本书书中，你将学习`C 编程语言`包含的内容，学习如何编写条件、表达式、语句甚至是命令，以便该语言能够高效地执行其功能。你还将学习如何组织相关的表达式，以便在编译和执行后，计算机返回的是有用的结果而不是错误信息。此外，本书还详细介绍了`C 语言`中所需的数据类型以及如何表示这些数据类型。

简单来说，这是一本为程序员、修读其他计算机课程的学习者，以及其他想要精通最流行的计算机语言`C`工作原理的计算机用户编写的教程。

## 什么是 C？
`C` 是 1972 年在美国 AT&T 贝尔开发的编程语言。它由一个名为 `Dennis Ritchie` 的人设计并编写。`c` 如此受欢迎的原因可能是因为它可靠、简单且易于使用。此外，在一个新的语言、工具和技术不断涌现又消失的行业中，一种生存了三十多年的语言一定非常优秀。今天经常听到的一种观点是——“c 已经被 `c++` 和 `java` 等语言取代了，现在为什么要费心学习 `c` 呢”。

## 开始学习 c
与计算机通信涉及使用计算机能理解的语言，这立即排除了 `English` 作为与计算机通信的语言。然而，学习英语与编程的类比是：首先学习该语言使用的字母表，然后学习如何将这些字母组合成单词，进而将单词组合成句子。





# 如何在 C 程序中使用常量？

我们可以通过以下方式在 C 程序中定义常量：

1. 通过 `const` 关键字
2. 通过 `#define` 预处理器指令

请注意，当你在 C 程序中尝试在定义常量后修改常量值时，程序将会报错。

## C 语言中使用 CONST 关键字的示例程序：

```c
#include <stdio.h>
void main() {
    const int height = 100; /*整常量*/
    const float number = 3.14; /*实数常量*/
    const char letter = 'A'; /*字符常量*/
    const char letter_sequence[10] = "ABC"; /*字符串常量*/
    const char backslash_char = '\?'; /*特殊字符常量*/
    printf("value of height :%d \n", height );
    printf("value of number : %f \n", number );
    printf("value of letter : %c \n", letter );
    printf("value of letter_sequence : %s \n", letter_sequence);
    printf("value of backslash_char : %c \n", backslash_char);
}
```

**输出：**
```
value of height : 100
value of number : 3.140000
value of letter : A
value of letter_sequence : ABC
value of backslash_char : ?
```

## C 语言中使用 #DEFINE 预处理器指令的示例程序：

```c
#include <stdio.h>
#define height 100
#define number 3.14
#define letter 'A'
#define letter_sequence "ABC"
#define backslash_char '\?'
void main() {
    printf("value of height : %d \n", height );
    printf("value of number : %f \n", number );
    printf("value of letter : %c \n", letter );
    printf("value of letter_sequence : %s \n", letter_sequence);
    printf("value of backslash_char : %c \n", backslash_char);
}
```

**输出：**
```
value of height : 100
value of number : 3.140000
value of letter : A
value of letter_sequence : ABC
value of backslash_char : ?
```

## 整数常量构造规则

a) 整数常量至少包含一个数字。
b) 它不能包含小数点。
c) 它可以是正数也可以是负数。
d) 如果整数常量前面没有符号，假设为正数。
e) 整数常量内部不允许出现逗号或空格。
f) 整数量的允许范围为 `-2147483648` 到 `+2147483647`。
示例：`-426`, `+782`, `-8000`, `-7605`

## 实数常量构造规则

实数常量通常称为浮点常量。实数有两种的形式：小数形式和指数形式。

a) 实数常量至少包含一个数字。
b) 它必须包含小数点。
c) 它可以是正数也可以是负数。
d) 默认符号为正数。
e) 实数常量内部不允许出现逗号或空格。
示例：`+325.34`, `426.0`, `-48.5789`

## 字符常量构造规则

a) 字符常量是包含在单引号内的单个字母、单个数字或单个特殊符号。两个单引号都应向左对齐。例如，`'a'` 是有效的字符常量，而 `a` 不是。
b) 字符常量的最大长度为 1 个字符。
示例：`'A'`, `'T'`, `'S'`

## C 变量类型

在程序执行过程中可能会变化的实体被称为变量。变量名是被赋予内存位置的。这些位置可以包含整数、实数或字符常量。在任何语言中，支持的变量类型取决于它能处理的常量类型。这是因为特定类型的变量只能存储整数常量，实数变量只能存储实数常量，而字符变量只能存储字符常量。

三种 C 变量：
a) 整数 `x, y, z;`
b) 浮点 `z;`
c) 字符 `st-name[20];`

## 变量名构造规则

a) 变量名是 1 到 30 个字母、数字或下划线的任意组合。某些编译器允许变量名长度可达 247 个字符。尽管这样更安全。
b) 变量名必须以字母或下划线开头。
c) 变量名内部不允许出现逗号或空格。
d) 保留关键字不能作为变量名。





## 代码示例

```c
#include <stdio.h>
#include <stdlib.h>
int main(){
    setenv("DIR", "/usr/bin/example/", 50);
    printf("Directory name before modifying = %s\n", getenv("DIR"));
    putenv("DIR=/usr/home/");
    printf("Directory name after modifying = %s\n", getenv("DIR"));
    return 0;
}
```

**输出：**
`Directory name before modifying = /usr/bin/example/ Directory name after modifying = /usr/home/`

## C 语言变量声明与定义的区别

| 变量声明 | 变量定义 |
| :--- | :--- |
| 声明告诉编译器关于变量的数据类型和大小。 | 定义为变量分配内存。 |
| 变量在程序中可以被声明多次。 | 在程序中一个变量定义只能发生一次。 |
| 给变量分配属性和标识符。 | 为变量分配存储空间。 |

## C 关键字

关键字不能用作变量名，因为如果我们这样做，就正尝试给关键字赋予新的含义，这是计算机不允许的。某些 C 编译器允许你构建与关键字完全相同的变量名。然而，更安全的做法是不混淆变量名和关键字。关键字也被称为保留字。C 语言中只有 32 个关键字。

**可用关键字：**
`auto`, `double`, `break`, `else`, `case`, `enum`, `char`, `extern`, `const`, `float`, `continue`, `default`, `for`, `goto`, `if`, `int`, `struct`, `switch`, `register`, `typedef`, `union`, `unsigned`, `signed`, `void`, `volatile`, `volatile`, `while`.

## 第一个 C 程序

a) C 程序中的每条指令都写为一个独立的语句。因此，一个完整的 C 程序由一系列语句组成。
b) 程序中的语句必须按照我们希望它们执行的顺序出现，除非问题的逻辑要求跳转或将控制转移到顺序之外的语句。
c) 在两个单词之间可以插入空格以提高语句的可读性。然而，在变量、常量或关键字内部不允许有空格。
d) 所有的语句都用小写输入。
e) C 语言对语句编写的位置没有特殊规定。这就是为什么它通常被称为自由格式语言。
f) 每条 C 语句必须以 `;` 结尾，因此 `;` 充当语句终止符。

```c
#include<stdio.h>
main(){
    int total;
    printf("\n enter marks in exam");
    scanf("%d",&total);
    if (total>=100)
        printf("\n passed");
    else
        printf("\n failed");
}
```

**此程序的输出：**
Enter marks in exam
200
passed

## 程序解释

a) 程序开头有必要使用 `#include<stdio.h>`。`#include` 是一个预处理器指令。
b) `main()` 是一个函数。函数无非是一组语句。在 C C 程序中可以有多个函数。首先，我们将只关注一个函数。这个函数的名称必须是 `main()`，不能是其他任何。所有属于 `main()` 的语句都包含在一对括号 `{}` 中，如下所示：

```c
int main(){
    Statement 1
    Statement 2
    Statement 3
}
```
c) C 语言的输出可以使用 `printf()` 函数实现。`printf()` 的通用形式是：
- `%f` 用于打印实数
- `%d` 用于打印整数
- `%c` 用于打印字符
d) C 语言的输入可以使用 `scanf()` 函数实现。`scanf()` 的通用形式是：
- 格式字符串 `variable` 
- `%d` 用于 `int`
- `%f` 用于 `float`

## 示例程序

```c
#include<stdio.h>
main(){
    float f,c;
    printf("\n celcius");
    scanf("%d",&c);
    f=(9*c)/5;
    printf("%f");
}
```
**此程序的输出：**
celcius
68.000000

## 指令

C 语言中基本上三种类型的指令：

A) **声明指令**：用于声明 C 程序中使用的变量类型。
B) **算术指令**：用于对常量和变量进行算术运算。
C) **控制指令**：用于控制各种语句的执行顺序。

## 编写 C 程序的基础

以下是编写简单 C 程序时使用的一些命令和语法。让我们逐行查看。

| C 基础命令 | 解释 |
| :--- | :--- |
| `#include <stdio.h>` | 这是一个预处理器命令，在编译程序之前从 C 库包含输入输出头文件 (stdio.h)。 |
| `int main()` | 这是主函数，任何 C 程序的执行从这里开始。 |
| `{` | 表示主函数的开始。 |
| `/*某些注释*/` | 任何 C 程序 `/* */` 命令内部给的内容都不会被考虑编译和执行。 |
| `printf("Hello World! ")` | `printf` 命令将输出到屏幕上。 |
| `getch()` | 该命令等待键盘的任何字符输入。 |
| `return 0;` | 该命令终止 C 程序（主函数）并返回 0。 |
| `}` | 表示主函数的结束。 |





* 一旦在机器上安装了 C 编译器，你就可以按照下方链接所示创建、编译和执行 C 程序。
* 如果你不想在机器上安装 `C/C++` 编译器，可以参考在线编译器，它们可以在线编译并执行 `C/C++` 以及许多其他编程语言，并在屏幕上显示输出。有关更多信息，请在 Google 中搜索在线 `C/C++` 编译器。

# C 程序的基本结构

C 程序的结构由一组被称为协议（protocol）的规则定义，程序员在编写 C 程序时必须遵守这些规则。所有的 C 程序都包含下面提到的各个部分/区域。

1. 文档部分
2. 链接部分
3. 定义部分
4. 全局声明部分
5. 函数原型声明部分
6. 主函数
7. 用户定义函数部分

## 用于比较所有部分的 C 程序示例：
你可以通过下面的 C 程序与 C 程序的所有部分进行比较。

```c
#include <stdio.h>
int total = 0;
int sum (int, int);
int main () {
    printf ("This is a C basic program \n");
    total = sum (1, 1);
    printf ("Sum of two numbers : %d \n", total);
    return 0;
}
int sum (int a, int b) {
    return a + b;
}
```

**输出：**
```
This is a C basic program
Sum of two numbers : 2
```

## C 程序每个部分的描述：

* 让我们在下面详细查看 C 基础程序的每个部分。
* 请注意，除了 `main` 函数和链接部分外，C 程序可能不包含下面提到的所有部分。
* 此外，C 程序的结构可能并不按照下面提到的顺序。

| 部分 | 描述 |
| :--- | :--- |
| 文档部分 | 我们可以在此部分提供关于程序、创建或修改日期、作者名称等注释。位于 `/*` 和 `*/` 之间的字符、单词或任何内容，C 编译器在编译过程中都不会考虑。这些内容将在编译期间被 C 编译器忽略。 |
| 链接部分 | 执行 C 程序所需的头文件包含在此部分。 |
| 定义部分 | 在此部分中定义变量并为这些变量设置值。 |
| 全局声明部分 | 全局变量在此部分定义。当一个变量要在整个程序中使用时，可以在此部分定义。 |
| 函数原型声明部分 | 函数原型提供了关于函数的许多信息，如返回类型、函数内部使用的参数名。 |
| 主函数 | 每一个 C 程序都从 `main` 函数开始，该函数包含两个主要部分：声明部分和执行部分。 |
| 用户定义函数部分 | 用户可以在此部分定义自己的函数，根据用户需求执行特定任务。 |

## C 语言基础中的记忆要点：

1. C 编程是一种区分大小写的编程语言。
2. 每条 C 编程语句都以分号（`;`）结束，分称为语句终止符。
3. `printf()` 命令用于将输出打印到屏幕上。
4. C 程序使用 C 编译器编译，并在执行时显示输出。

# 数据类型

C 数据类型被定义为变量可以存储的以执行特定操作的数据存储格式。数据类型用于在程序中使用变量之前定义变量。变量、常量和数组的大小由数据类型决定。

## C – 数据类型：
C 语言中有四种数据类型。它们是：

| 类型 | 数据类型 |
| :--- | :--- |
| 基本数据类型 | `int`, `char`, `float`, `double` |
| 枚举数据类型 | `enum` |
| 派生数据类型 | `pointer`, `array`, `structure`, `union` |
| 空数据类型 | `void` |

## C 语言中的基本数据类型：

### 1.1 数据 数据类型：

* 整数数据类型允许变量存储数值。
* `int` 关键字用于引用整数数据类型。
* `int` 数据类型的存储大小为 2 或 4 或 8 字节。
* 它取决于我们所使用的 CPU 处理器。如果我们使用 16 位处理器，则将为 `int` 数据类型分配 2 字节（16 位）的内存。
* 同样，32 位处理器分配 4 字节（32 位）的内存，64 位处理器分配 8 字节（64 位）的内存给 `int` 数据类型。
* `int`（2 字节）可以存储从 -32,768 到 +32,767 的值。
* `int`（4 字节）可以存储从 -2,147,483,648 到 +2,147,483,647 的值。
* 如果你想使用超过上述限制的整数值，可以使用 `long int` 和 `long long int`，它们的限制非常高。

**注意：**
* 我们无法使用 `int` 数据类型存储小数。
* 如果我们使用 `int` 数据类型存储小数，小数将被截断，我们只得到整数部分。
* 在这种情况下，可以使用 `float` 数据类型在变量中存储小数。

### 字符数据类型：

* 字符数据类型允许变量存储字符。
* `char` 关键字用于引用字符数据类型。
* `char` 数据类型的存储大小为 1 字节。
* `char` 允许变量存储单个字符。

### 1.2 浮点类型（FLOATING POINT）：

* 浮点数据类型允许变量存储小数。
* `float` 关键字用于引用浮点数据类型。
* `float` 存储大小为 4 字节。

### 1.3 双精度（DOUBLE）：

* 双精度数据类型允许变量存储高精度的数值。
* `double` 关键字用于引用双精度类型。
* `double` 的存储大小为 8 字节。

## C 语言中的 SIZ() 函数：

`sizeof()` 函数用于查找变量分配的内存空间。

```c
#include <stdio.h>
int main() {
    int a;
    char b;
    float c;
    double d;
    printf("Storage size for int: %zu\n", sizeof(a));
    printf("Storage size for char: %zu\n", sizeof(b));
    printf("Storage size for float: %zu\n", sizeof(c));
    printf("Storage size for double: %zu\n", sizeof(d));
    return 0;
}
```

# C 语言中的修饰符（MODIFIERS）：

* 修饰符用于分配内存。
* 修饰符基本数据类型以增加或减少范围。
* 例如，`int` 的存储空间为 4 字节（32 位），使用 `long int` 可以将其范围增加到 8 字节。使用 `short int` 可以将其范围减少到 2 字节。

C 语言中有 5 种修饰符。它们是：
1. `short`
2. `long`
3. `signed`
4. `unsigned`
5. `long long`

下表给出了 16 位处理器上每种 C 数据类型的存储大小。请记住，`int` 和 `float` 数据类型的存储大小和范围取决于 CPU（8、16、32 和 64 位）。

| C 数据类型 / 存储大小 | 范围 |
| :--- | :--- |
| `char` / 1 | –128 to 127 |
| `int` / 2 | –32,768 to 32,767 |
| `float` / 4 | 1.175494e-38 to 3.402823e+38 |
| `double` / 8 | 2.225074e-308 to 1.797693e+308 |
| `long double` / 10 | 3.4022e-4932 to 1.1897e+4932 |
| `long int` / 4 | –2,147,483,648 to 2,147,483,647 |
| `short int` / 2 | –32,768 to 32,767 |
| `unsigned short int` / 2 | 0 to 65,535 |
| `signed short int` / 2 | –32,768 to 32,767 |
| `long long int` / 8 | –9,223372036854775808 to 9,223372036854775807 |
| `signed long int` / 4 | –2,147,483,648 to 2,147,483,647 |
| `unsigned long int` / 4 | 0 to 4,294,967,295 |





| `unsigned long long int / 8` | 2(power)64 –1 |

## 举型示例程序

```c
#include <stdio.h>
int main(){
    enum MONTH { Jan = 0, Feb, Mar };
    enum MONTH month = Mar;
    if(month == 0)printf("Value of Jan");
    else if(month == 1)printf("Month is Feb");
    if(month == 2)printf("Month is Mar");
}
```

**输出：**
```
Month is March
```

## C 语言中的派生类型

- 数组、指针、结构体和联合在 C 语言中被称为派生类型。
- 要了解更多关于派生类型的信息，请访问本教程中的 [C – 数组](http://fresh2refresh.com/c/c-array/) 、“ [C – 指针](http://fresh2refresh.com/c/c-pointer/) 、“ [C – 结构体](http://fresh2refresh.com/c/c-structures/) ” 和 “ [C – 联合](http://fresh2refresh.com/c/c-union/) ” 主题。

## C 语言中的 void 类型

- Void 是一个空数据类型，没有值。
- 它可以用于函数和指针。
- 请访问 “ [C – 函数](http://fresh2refresh.com/c/c-function/) ”，通过简单的值传递和引用传递调用示例程序来了解如何在函数中使用 void 类型。

## 标记（TOKENS）与关键字

C 标记、标识符和关键字是 C 程序的基础。本页将通过定义和简单的示例程序解释所有这些内容。

### C 标记

- C 标记是 C 语言中基本的构建块，它们组合在一起以编写一个 C 程序。
- C 程序中的每一个最小的独立单元都被称为 C 标记。
- C 标记共有六类。它们是：

### 标记示例程序

```c
#include<stdio.h>
int main(){
    int x, y, total;
    x = 10, y = 20;
    total = x + y;
    printf ("Total = %d \n", total)
}
```

### C 语言中的标识符

- C 程序中的每个程序元素都被赋予一个称为标识符的名称。
- 用于标识变量、函数和数组的名称是标识符的示例。例如，`x` 是上述程序中赋予整数变量的名字。

#### C 语言中构造标识符名称的规则

1. 第一个字符应该是字母或下划线。
2. 随后的字符可以是数字或字母。
3. 除了下划线外，不允许使用标点符号和特殊字符。
4. 标识符不应该是关键字。

### C 语言中的关键字

- 关键字是 C 编译器中预定义的单词。
- 每个关键字都用于在 C 程序中执行特定的功能。
- 由于关键字是编译器的引用名称，因此不能用作变量名。

## 决策控制语句

默认情况下，程序中的指令是按顺序执行的。然而，在实际的编程场景中，我们很少希望指令按顺序执行。很多时候，我们希望在某种特定情况下执行一组指令，而在另一种情况下执行另一组完全不同的指令。这种情况在 C 程序中通过决策控制语句来处理。正如前面提到的，C 语言可以实现决策控制语句，主要有三种决策控制语句：

a) `if` 语句
b) `if-else` 语句
c) 条件运算符

### `if` 语句

与大多数语言一样，C 使用关键字 `if` 来实现决策控制语句。关键字 `if` 告诉编译器后面的是一个决策控制语句。无论条件如何，如果为真（true），则不执行该语句，而是程序将跳过它。但我们如何在 C 中表示条件本身呢？我们如何评估它的真假？根据一般规则，我们使用 C 的关系运算符来表示条件。关系运算符允许我们比较两个值，以查看它们是否相等、不相等，或者一个是否大于另一个。以下是它们在 C 中的外观以及评估方式。

| 此表达式 | 结果 |
| :--- | :--- |
| `x == y` | 为真 |
| `x != y` | `x` 等于 `y` |
| `x < y` | `x` 不等于 `y` |
| `x > y` | `x` 小于 `y` |
| `x <= y` | `x` 大于 `y` |
| `x >= y` | `x` 小于或等于 `y` |





# 关系运算符

你应该熟悉关系运算符，除了等号运算符 `==` 和不等于运算符 `!=` 之外。请注意，`=` 用于赋值，而 `==` 用于两个量值之间的比较。

这里是一个简单的程序，演示了 `if` 和关系运算符的使用。

### a)
```c
#include<stdio.h>
main(){
    int a,b,c,big;
    printf("enter the value of a,b and c");
    scanf("%d%d%d",&a,&b,&c);
    big=a;
    if(b>big)
        big=b;
    if(c>big)
        big=c;
    printf("largest number=%d",big);
}
```
该程序的输出如下所示：
```
enter the value of a,b and c100 200 500
Largest number = 500
```
在执行此程序时，如果你输入 `enter the value of a,b and c`，你将通过 `printf()` 在屏幕上看到一条消息。最大的数字……

为了让你熟悉决策控制语句，下面又给出了例子。在继续阅读之前仔细学习它。

### b)
```c
#include<stdio.h>
main(){
    int a,b,c,small;
    printf("Enter the value of a,b and c");
    scanf("%d%d%d",&a,&b,&c);
    small=a;
    if(b<small)
        small=b;
    if(c<small)
        small=c;
    printf("smallest no=%d",small);
}
```
该程序的输出如下所示：
```
Enter the value of a,b and c50 100 150
Smallest no = 50
```
在执行此程序时，如果你输入 `enter the value of a,b and c`，你将通过 `printf()` 在屏幕上看到一条消息。最小的数字。

# if-else 语句

`if` 语句本身在当 `if` 后面的表达式求值为真时会执行单条语句或一组语句。当表达式求值为假时，它什么都不做。我们是否可以在表达式求为真时执行一组语句，而在表达式求为假时执行另一组语句？当然可以！这就是后续示例所示的 `else` 语句的作用：

### A)
```c
#include<stdio.h>
main(){
    int total;
    float percentage;
    printf("\n enter the total marks in exam");
    scanf("%d",& total);
    percentage= total/8;
    printf(" percentage =%f",percentage);
    if(percentage>=90)
        printf("\n1st divisioin ");
    if( percentage>=70)
        printf("\n 2nd division");
    if ( percentage>=50)
        printf( \n third division");
    else
        printf( "\n failed");
}
```
该程序的输出如下：
```
enter the total marks in exam580
Percentage = 72.000002
2nd division
```

### B)
```c
#include<stdio.h>
main(){
    int total;
    printf("\n enter total marks in exam");
    scanf("%d",&total);
    if (total>=100)
        printf("\n passed");
    else
        printf("\n failed");
}
```
该程序的输出：
```
enter total marks in exam:500
passed
```

# 值得注意的几点

A) `if` 之后到 `else` 之前（不包括 `else`）的语句组被称为 `if` 块，同样，`else` 之后的语句形成了 `else` 块。

B) 注意 `else` 写在 `if` 的下方。`if` 块中的语句和 `else` 块中的语句都向右缩进了。书中遵循这种格式约定是为了让你更好地理解程序的运行。

C) 如果 `if` 块中只有一条要执行的语句，`else` 块中也只有一条语句，我们可以省略这对大括号。

D) 与 `if` 语句一样，`else` 的默认范围也是 `else` 之后的第一条语句。要覆盖此默认范围，必须使用如上述示例所示的大括号。

# 嵌套 if-else

在 `if` 语句的体或 `else` 语句的体内编写整个 `if-else` 结构是完全可以的。这被称为 `if` 的嵌套。如下面的程序所示：

### a)
```c
#include <stdio.h>
int main(){
    int i ;
    printf(" enter either 1 or 2 ");
    scanf("%d", &i);
    if (i==1)
        printf(" you would go to heaven \n");
    else{
        if (i==2)
            printf("\n hell was created with you in mind ");
        else
            printf("\n how was mother earth");
    }
    return 0;
}
```
注意：第二个 `if-else` 结构嵌套在第一个 `else` 语句中。如果第一个 `if` 语句中的条件为假，则检查第二个 `if` 语句中的条件。如果它也为假，则执行 `else` 语句。你可以看到每当 `if-else` 结构嵌套在另一个 `if-else` 结构中时，通过缩进可以增加程序的清晰度。养成缩进的习惯，否则你以后写的程序将很难理解。

# C 语言中逻辑运算符的使用

这些运算符用于对给定表达式执行逻辑操作。C 允许使用逻辑运算符，即 `&&`、`||` 和 `!`。它们分别被读作 AND、OR 和 NOT。

| 运算符 | 说明 |
| :--- | :--- |
| `&&` | 当操作数均为真时返回真 |
| `||` | 当至少有一个操作数为真时返回真 |
| `!` | 反转逻辑状态 |

# 算术运算符

算术运算符用于执行数学计算，如加法、减法、乘法、除法和取模。

| 运算符 | 示例 |
| :--- | :--- |
| `+` | 加法 |
| `-` | 减法 |
| `*` | 乘法 |
| `/` | 除法 |
| `%` | 取模 |

### 赋值运算符

在 C 程序中，使用赋值运算符进行赋值。赋值运算符分为类：

### 赋值运算符
`=` - 示例：`sum=10;`（将 10 赋值变量 sum）

### 复合赋值运算符
`+=`, `-=`, `*=`, `/=`, `%=`, `&=`, `^=`

| 运算符 | 示例 |
| :--- | :--- |
| `+=` | `sum+=10`（等同于 `sum = sum +10`） |
| `-=` | `sum-=10`（等同于 `sum = sum -10`） |
| `*=` | `sum*=10`（等同于 `sum = sum *10`） |
| `/=` | `sum/=10`（等同于 `sum = sum /10`） |
| `%=` | `sum%=10`（等同于 `sum = sum%10`） |
| `&=` | `sum&=10`（等同于 `sum = sum &10`） |
| `^=` | `sum^=10`（等同于 `sum = sum ¹⁰`） |





# C 语言关系运算符示例程序

a) 在此程序中，关系运算符 `==` 用于比较两个值是否相等。
b) 如果两个值相等，则输出 `values are equal,`；否则，输出 `values are not equal,`。
c) 注意：应该使用双等号 `==` 来比较两个值。我们不应该使用单等号 `=`。

```c
#include<stdio.h>
int main () {
    int m=40,n=20;
    if ( m==n) {
        printf("\n m and n are equal");
    }
    {
        printf("\n m and n are not equal");
    }
}
```
**输出**
`M and n are not equal`

# 位运算符

这些运算符用于执行位操作。十进制值会被转换为二进制值（即比特位序列），位运算符在这些位上进行操作。
C 语言中的位运算符有 `&`（位与）、`|`（位或）、`^`（位异或）、`<<`（左移）和 `>>`（右移）。

### 位运算与位运算符的真表

| x | y | x/y | X&y | X^y |
| :--- | :--- | :--- | :--- | :--- |
| 0 | 0 | 0 | 0 | 0 |
| 0 | 1 | 1 | 0 | 1 |
| 1 | 0 | 1 | 0 | 1 |
| 1 | 1 | 1 | 1 | 0 |

以下是 C 语言中的位运算符及其名称：
a) `&` - 位与
b) `|` - 位或
c) `-` - 位反
d) `^` - 异或
e) `<<` - 左移
f) `>>` - 右移

考虑 `x=40` 且 `y=80`。这些值的二进制形式如下：
`X=00101000`
`Y=01010000`

以下是 `x` 和 `y` 的所有位运算：
A) `X&y= 00000000(binary)=0(decimal)`
B) `X|y= 01111000(binary)=120(decimal)`
C) `-x= 11111111111111111111111111111111111111111111111111=-41(decimal)`
D) `X^y= 01111000(binary)=120(decimal)`
E) `X<<1= 01010000(binary)= 80( decimal)`
F) `X>>1= 00010100( binary) = 20 ( decimal)`

注意：`40` 的二进制值为 `000000000000000000000000000000000000000000000000000000`，因此所有所有的 0 在位反操作中都会被转换。

### 位左移和右移 

在左移操作中，`x<<1` 中的 `1` 表示位将向左移动一位。如果我们使用 `x<<2`，则意味着位将移动 2 位。

CC 语言位运算的示例程序。
```c
#include<stdio.h>
main(){
    int m =40, n=80, AND_opr, OR_opr, XOR_opr, NOT_opr;
    AND_opr=(m&n);
    OR_opr =(m|n);
    NOT_opr =(-m);
    XOR_opr =(m^n);
    printf("\n AND_opr value= %d\n", AND_opr);
    printf("\n OR_opr value= %d\n", OR_opr); 
    printf("\n NOT_opr value= %d\n", NOT_opr);
    printf("\n XOR_opr value= %d\n", XOR_opr);
    printf("\n left_shift value= %d\n", m<<1);
    printf("\n right_shift value= %d\n", m>>1);
}
```
**输出**
`AND_opr value = 0`
`OR_opr value = 120`
`NOT_opr value = -41`
`XOR_opr value = 120`
`left_shift value = 80`
`right_shift value = 20`

# C 语言中的条件运算符

条件运算符在条件为真时返回一个值，在条件为假时返回另一个值。这种运算符也称为三元运算符。
语法：`条件?真值:假值`
示例：`a>100 ? 0:1`。在上面的示例中，如果 `a` 大于 `100`，则返回 `0`，否则返回 `1`。这等同于 if else 语句。

C 语言中条件/三元运算符的示例程序
```c
#include<stdio.h>
int main(){
    int x=1,y;
    y= ( x==1 ? 2:0);
    printf("\n x is %d ",x);
    printf("\n y is %d ",y);
}
```
**输出**
`x is 1`
`y is 2`

# 自增/自减运算符

自增运算符用于将变量增加一，自减运算符用于将变量减少一。
语法：
自增运算符：`++变量名` (或 `变量名++`)
自减运算符：`--变量名` (或 `变量名--`)
示例：`++i`, `i--`

C 语言中自增运算符的示例程序：
```c
#include<stdio.h>
int main (){
    int i=1;
    while (i<=10) {
        printf("%d ",i);
        i++;
    }
}
```
**输出**
`1 2 3 4 5 6 7 8 9`

b) 自减运算符的示例：
```c
#include<stdio.h>
int main (){
    int i=20;
    while (i>10) {
        printf("%d ",i);
        i--;
    }
}
```
**输出**
`20 19 18 17 16 15 14 13 12 11`

c) C 语言中前置自增运算符的示例程序：
```c
#include<stdio.h>
int main (){
    int i=0;
    while (++i<5) {
        printf("%d",i);
    }
    return 0;
}
```
**输出**
`1234`
步骤 1：在上面的程序中，`i` 的值通过自增运算符从 0 增加到 1。
步骤 2：自增的值 `1` 在循环表达式中与 5 进行比较。
步骤 3：将自增的值 `1` 赋值给变量 `i`。
上述三个步骤持续直到循环表达式为假，输出为 `1234`。

D) C 语言中前置自减运算符的示例程序：
```c
#include<stdio.h>
int main(){
    int i=10;
    while( --i>5) {
        printf("%d",i);
    }
    return 0;
}
```
**输出**
`9 8 6`
步骤 1：在上面的程序中，`i` 的值通过自减运算符从 10 减少到 9。
步骤 2：自减的值 `9` 在循环表达式中与 5 进行比较。
步骤 3：将自减的值 `9` 赋值给变量 `i`。
上述三个步骤持续直到循环表达式为假，输出为 `9,8,6`。

# C 语言特殊运算符

以下是 C 语言提供的某些特殊运算符。

| 运算符 | 说明 |
| :--- | :--- |
| `&` | 用于获取变量的地址。示例：`&a` 获取 `a` 的地址 |
| `*` | 用于变量指针。示例：`*a` 其中 `*` 是变量 `a` 的指针 |
| `sizeof()` | 给变量的大小。示例：`sizeof(char)` 得到 1 |

a) C 语言中 `&` 和 `*` 运算符的示例程序
```c
#include<stdio.h>
int main(){
    int *ptr,q;
    q=50;
    ptr=&q;
    printf("\n %d,* ptr );
    return 0;
}
```
**输出**
`50`

b) C 语言中 `sizeof()` 运算符的示例程序
```c
#include<stdio.h>
#include<limits.h>
int main(){
    int a;
    char b;
    float c;
    double d;
    printf ("\n storage size for int data type : %d ", sizeof(a));
    printf ("\n storage size for char data type : %c ", sizeof(b));
    printf ("\n storage size for float data type : %f ", sizeof(c));
    printf ("\n storage size for double data type : %f ", sizeof(d));
    return 0;
}
```
**输出**
`storage size for int data type:4, storage size for char data type:1 , storage size for float data type,:4, storage size for double data type : 8`

# 循环语句

C 语言中的循环语句用于执行循环操作直到给定条件为真。一旦条件变为假，控制就会离开循环语句。

### C 语言中的循环语句类型

C 语言中有 3 种类型的循环语句。它们是：
1. `for`
2. `while`
3. `do-while`

### FOR 循环
`for` 循环允许我们在单行内指定关于循环的三个点：
* 将循环计数器设置为初始值
* 测试循环计数器以确定其值是否已达到所需的次数
* 每执行一次循环内的程序，就增加循环计数器的值

语法：`for(初始化计数器; 测试计数器 ; 增加计数器){执行此;执行另一个...}`

### WHILE 循环
在编程中，经常需要执行固定次数的某些。
语法：`初始化计数器;While( 使用条件测试计数器){执行此;执行另一个;增加计数器;}`

### DO-WHILE 循环

用于确保循环体语句至少执行一次。
语法：`Do{此;以及另一个;以及另一个;} while( 此条件为真);`

#### A) C 语言 FOR 循环示例程序
在 for 循环语句中，循环执行直到条件变为假。
```c
#include <stdio.h>
int main(){
    int i;
    for(i=0;i<10;i++){
        printf("%d ",i);
    }
}
```
**输出**
`0 1 2 3 4 5 6 7 8 9`

#### B) C 语言 WHILE 循环示例程序
在 while 循环语句中，循环执行直到条件变为假。
```c
#include <stdio.h>
int main(){
    int i=3;
    while(i<10){
        printf("%d\n",i);
        i++;
    }
}
```
**输出**
`3 4 5 6 7 8 9`





# C 语言示例程序（DO WHILE 循环）

在 `do..while` 循环控制语句中，`while` 循环无论条件如何都会执行一次。从第二次开始，循环将一直执行，直到条件变为假。

```c
#include <stdio.h>
int main(){
    int i=1;
    do{
        printf("Value of i is %d\n",i);
        i++;
    }while(i<=4 && i>=2);
    }
```

**输出：**

| Value of i is 1 |
| Value of i is 2 |
| Value of i is 3 |
| Value of i is 4 |

# 分支语句

用于在系列语句块中执行特定语句块的语句称为分支语句。C 语言中有 4 种分支语句。它们是：

1. `switch`
2. `break`
3. `continue`
4. `goto`

## 1. C 语言中的 SWITCH CASE 语句：

允许我们从多个选择中做出决策的控制语句被称为 `switch`，或者更准确地说是 `switch case default`，因为这三个关键字共同组成了控制语句。

**语法：**
```c
_switch ( integer expression){
    case constant 1;do this;
    case constant 2;do this;
    case constant 3;do this;
    default;do this;
}
```

### 1) C 语言 SWITCH..CASE 语句的示例程序：

```c
#include <stdio.h>
int main (){
    int value = 3;
    switch(value){
        case 1:printf(“Value is 1 \n” );break;
        case 2:printf(“Value is 2 \n” );break;
        case 3:printf(“Value is 3 \n” );break;
        case 4:printf(“Value is 4 \n” );break;
        default :printf(“Value is other than 1,2,3,4 \n” );
    }
    return 0;
}
```

**输出：**

| Value is 3 |

## 2. C 语言中的 BREAK 语句：

我们经常遇到这样的情况：我们想要立即跳出循环，而不需要等待返回条件测试。`break` 允许我们这样做。当在任何循环内部遇到 `break` 时，控制会自动传递到循环后的第一个语句。`break` 通常与 `if` 关联使用。

### 2) C 语言 BREAK 语句的示例程序：

```c
#include <stdio.h>
int main(){
    int i;
    for(i=0;i<10;i++){
        if(i==5){
            printf("\nComing out of for loop when i = 5");
            break;
        }
        printf("%d ",i);
    }
}
```

**输出：**

| 0 1 2 3 4 Coming out of for loop when i = 5 |

## 3. C 语言中的 CONTINUE 语句：

在某些编程情况下，我们希望将控制权回到循环开头，跳过循环内部尚未执行的语句。`continue` 关键字允许我们这样做。当在任何循环内部遇到 `continue` 时，控制会自动传递到循环的开头。

### C 语言 CONTINUE 语句的示例程序：

```c
#include <stdio.h>
int main(){
    int i;
    for(i=0;i<10;i++){
        if(i==5 || i==6){
            printf("\nSkipping %d from display using \"continue \n",i);
            continue;
        }
        printf("%d ",i);
    }
}
```

**输出：**

| 0 1 2 3 4 Skipping 5 from display using continue |
| Skipping 6 from display using continue 7 8 9 |

## 4. C 语言中的 GOTO 语句：

在复杂的编程情况下，使用 `goto` 将控制权带到你想去的地方似乎简单。然而，几乎总是存在更优雅的方法通过 `if`、`while` 和 `switch` 编写相同的程序。这些结构更具逻辑性且易于理解。

### C 语言 GOTO 语句的示例程序：

```c
#include <stdio.h>
int main(){
    int i;
    for(i=0;i<10;i++){
        if(i==5){
            printf("\n are using goto statement when i = 5");
            goto HAI;
        }
        printf("%d ",i);
    }
    HAI: printf("\nNow we are inside label \"hai\" \n");
}
```

**输出：**

| 0 1 2 3 4 We are using goto statement when i = 5 Now, we are inside label “hai” |

# 存储类

变量的存储类告诉我们：

**A)** 变量存储在何处。
**B)** 如果没有专门指定初始值，变量的初始值是什么（即默认初始值）。
**C)** 变量的作用域是什么；即变量的值在哪个函数中可用可用。
**D)** 变量的生命周期是什么；即变量存在多久。

## C 语言中的存储类说明符类型：

C 语言中有 4 种可用的存储类说明符。它们是：

1. `Automatic`（自动）
2. `Register`（寄存器）
3. `Static`（静态）
4. `External`（外部）

*   **Automatic 存储类**：存储在内存中，初始值是不可预测的（垃圾值），作用域在函数内部，生命周期在函数执行结束。
*   **Register 存储类**：存储在 寄存器中，初始值是不可预测的，作用域在函数内部，生命周期在函数执行结束。
*   **Static 存储类**：存储在内存中，初始值为 0，作用域在函数内部，生命周期贯穿整个程序执行期间。
*   **External 存储类**：存储在内存中，初始值为 0，作用域是全局，生命周期贯穿整个程序。

### 1. AUTO 变量示例程序：

`auto` 变量的作用域在函数内部。它等于局部变量。所有局部变量默认都是 `auto` 变量。

```c
#include<stdio.h>
void increment(void);
int main(){
    increment();
    increment();
    increment();
    increment();
    return 0;
}
void increment(void){
    auto int i = 0 ;
    printf ( "%d ", i )
    i++;
}
```

**输出：**

| 0 0 0 0 |

### 2. STATIC 变量示例程序：

静态变量在不同函数调用之间保留值。

```c
//C static example
#include<stdio.h>
void increment(void);
int main(){
    increment();
    increment();
    increment();
    increment();
    return 0;
}
void increment(void){
    static int i = 0 ;
    printf ( "%d ", i )
    i++;
}
```

**输出：**

| 0 1 2 3 |

### 3. EXTERNAL 变量示例程序：

`extern` 变量的作用域贯穿主程序。它等于全局变量。外部变量的定义可能在 C 的任何地方。

```c
#include<stdio.h>
int x = 10;
int main(){
    printf("Value of x is %d", x);
    return 0;
}
```

**输出：**

| Value of x is 10 |

### 4. REGISTER 变量示例程序：

`register` 变量的作用域在函数内部。它等于局部变量。所有局部变量默认都是 `register` 变量。

```c
#include <stdio.h>
int main(){
    register int i;
    for(i=1; i<=5; i++){
        printf("Value of i is %d\n", i);
    }
    return 0;
}
```

**输出：**

| Value of i is 1 |
| Value of i is 2 |
| Value of i is 3 |
| Value of i is 4 |
| Value of i is 5 |





# 3. 函数声明、函数调用与函数定义

### A) 当函数名后跟着分号时，该函数被调用。例如：
```c
Int main (){Argentina();}
```

### B) 当函数名后跟着一对大括号且括号内包含一个或多个语句时，该函数被定义。例如：
```c
Void argentina(){
    Statements 1;
    Statements 2;
    Statements 3;
}
```

### C) 任何函数都可以从其他函数调用。即使是 `main()` 也可以从其他函数调用。例如：
```c
#include<stdio.h>
Void message()
Int main (){
    Message();
    Return0;
}
Void message(){
    Printf(“\n can not imagine without c”);
    Main();}
}
```### D) 函数可以被调用多次。例如：
```c
#include<stdio.h>
Void message(){
    Message();
    Message();
    Return0;
}
Void message(){
    Printf(“\n jewel thief”);
}
```

### E) 函数基本上分为两种：
- **库函数**：`printf()`, `scanf()` 等等。
- **用户定义函数**：`argentina()`, `brazil()` 等等。

---

## C 函数简单示例程序

* 如你所知，在 C 语言程序中，函数在调用之前应该进行声明和定义。
* 在下面的程序中，从 `main` 函数调用了函数 `square`。
*  `m` 的值作为参数传递给函数 `square`。在该函数中，该值与其相乘，并将结果 `p` 从 `square` 函数返回给 `main` 函数。

```c
#include<stdio.h>
// function prototype,也称为函数声明
float square ( float x );                 

// main function,程序从这里开始
int main( )
{
    float m, n ;
    printf ( "\nEnter some number for finding square \n");
    scanf ( "%f", &m )// function call
    n = square ( m ) ;                  
    printf ( "\nSquare of the given number %f is %f",m,n );
}
float square ( float x )   // function definition
{
    float p ;
    p = x * x ;
    return ( p ) ;
}
```

**输出:**
| 输入一个数字以计算平方 2 数字 2.000000 的平方是 4.000000 |

---

## 使用库函数：示例：
```c
#include<stdio.h>
#include<math.h>
Int main(){
    Float a=0.5;
    Float w, x y,z;
    W=sin(a);
    X=cos(a);
    Y=tan(a);
    Z=pow(a,2);
    Printf(“\n%f%f%f%f”,w,x,y,z);
    Return0;
}
```

---

## 函数的高级特性：
a) 函数的返回值
b) 按值或按引用调用函数
c) 递归

### 函数的返回值：
```c
#include<stdio.h>
Float square (float);
Int main(){
    Float a,b;
    Printf(“\n enter any number”);
    Scanf(“\n%f”,&a);
    B= square(a);
    Printf(“\n square of %f is %f”, a,b);
    Return 0;
}
Float square (float x){
    Float y;
    Y= x*x;
    Return(y);
}
```
**输出:**
- 输入任意数字 33 的平方是 9.000000
输入任意数字 1. 51.5 的平方是 2.250000
输入任意数字 2.52.5 的平方是 6.250000

---

## 按值调用

* 在按值调用的方法中，变量的值被作为参数传递给函数。
* 实参的值不能通过形参进行修改。
* 实参和形参会分配不同的内存。因为，实参的值被复制到了形参中。

**注意：**
* **实参** – 指在函数调用中使用的参数。
* **形参** – 指在函数定义中使用的参数。

### C 函数示例程序（使用按值调用）：
* 在此程序中，变量 `m` 和 `n` 的值被传递给函数 `swap`。
* 这些值被复制到 `swap` 函数的形参 `a` 和 `b` 中并使用。

```c
#include<stdio.h>
// function prototype,也称为函数声明
void swap(int a, int b);             

int main(){
    int m = 22, n = 44;
    // 按值调用 swap 函数
    printf(" values before swap  m = %d \nand n = %d", m, n);
    swap(m, n);                  
}
void swap(int a, int b){
    int tmp;
    tmp = a;
    a = b;
    b = tmp;
}
```
**输出:**
| 交换前的值 m = 22 \and n = 44 |

---

## 2. 按引用调用

* 在按引用的方法的方法，变量的地址被作为参数传递给函数。
* 实参的值可以被形参修改。
* 实参和形参不需要分配额外的内存。

### C 函数示例程序（使用按引用调用）：
```c
#include<stdio.h>
// function prototype,也称为函数声明
void swap(int *a, int *b);
int main(){
    int m = 22, n = 44;
    // 按引用调用 swap 函数
    printf(" values before swap  m = %d \and n = %d", m, n);
    swap(&m, &n);                  
}
void swap(int *a, int *b){
    int tmp;
    tmp = *a;
    *a = *b;
    *b = tmp;
}
```
**输出:**
| 交换前的值 m = 22 \and n = 44 |
| 交换后的值 m = 44 and n = 22 |

---

## 3. 递归

在 C 语言中，函数可以调用自身。如果函数体内的语句调用了自身，则该函数被称为递归。以下是计算阶乘的递归版本函数。

```c
#include<stdio.h>
Int main(){
    Float a,fact;
    Printf(“\ enter any value”);
    Scanf(“%d”,a);
    Fact=rec(a);
    Printf(“\n factorial value= %d”,fact);
    Return0;
}
Int rec (int x){
    Float f;
    If(x==1)
    Return(1);
    ElseF=x*rec(x-1);
    Return (f);
}
```
**输出:**
- 输入任意数字 1 1
- 输入任意数字 2 阶乘值 =2
- 输入任意数字 3 阶乘值 =3
- 输入任意数字 5 阶乘值 =120





## 1. 带参数和返回值

```c
#include<stdio.h>
#include<string.h>
int function(int, int[], char[]);
int main(){
    int i, a = 20;
    int arr[5] = {10,20,30,40,50};
    char str[30] = "\"fresh2refresh\"";
    printf("    ***修改前的值***\n");
    printf("value of a is %d\n",a);
    for (i=0;i<5;i++){
        // 访问每个变量
        printf("value of arr[%d] is %d\n",i,arr[i]);
    }
    printf("value of str is %s\n",str);
    printf("\n    ***修改后的值***\n");
    a= function(a, &arr[0], &str[0]);
    printf("value of a is %d\n",a);
    for (i=0;i<5;i++){
        // 访问每个变量
        printf("value of arr[%d] is %d\n",i,arr[i]);
    }
    printf("value of str is %s\n",str);
    return 0;
}
int function(int a, int *arr, char *str){
    int i;
    a = a+20;
    arr[0] = arr[0]+50;
    arr[1] = arr[1]+50;
    arr[2] = arr[2]+50;
    arr[3] = arr[3]+50;
    arr[4] = arr[4]+50;
    strcpy(str,"\"modified string\"");
    return a;
}
```

**输出:**
```
***修改前的值***
value of a is 20
value of arr[0] is 10
value of arr[1] is 20
value of arr[2] is 30
value of arr[3] is 40
value of arr[4] is 50
value of str is "fresh2refresh"

***修改后的值***
value of a is 40
value of arr[0] is 60
value of arr[1] is 70
value of arr[2] is 80
value of arr[3] is 90
value of arr[4] is 100
value of str is "modified string"
```

### b) 带参数且无返回值的示例程序
在此程序中，整数、数组和字符串被作为参数传递给函数。该函数的返回类型为 `void`，且无法从函数返回任何值。整数、数组和字符串的所有值都在函数内部进行处理和显示。

```c
#include<stdio.h>
void function(int, int[], char[]);
int main(){
    int a = 20;
    int arr[5] = {10,20,30,40,50};
    char str[30] = "\"fresh2refresh\"";
    function(a, &arr[0], &str[0]);
    return 0;
}
void function(int a, int *arr, char *str){
    int i;
    printf("value of a is %d\n\n",a);
    for (i=0;i<5;i++){
        // 访问每个变量
        printf("value of arr[%d] is %d\n",i,arr[i]);
    }
    printf("\nvalue of str is %s\n",str);
}
```

**输出:**
```
value of a is 20
value of arr[0] is 10
value of arr[1] is 20
value of arr[2] is 30
value of arr[3] is 40
value of arr[4] is 50
value of str is "fresh2refresh"
```

### 3. 无参数且无返回值的示例程序
在此程序中，没有值被传递给 `test` 函数，且该函数也没有向主函数返回任何值。

```c
#include<stdio.h>
void test();
int main(){
    test();
    return 0;
}
void test() {
    int a = 50, b = 80;
    printf("\nvalues : a = %d and b = %d", a, b);
}
```

**输出:**
```
values : a = 50 and b = 80
```

### c) 无参数且有返回值的示例程序
在此程序中，没有参数被传递给 `sum` 函数。但该函数会向主函数返回值。变量 `a` 和 `b` 的值在 `sum` 函数中求和，并将这些值的和返回给主函数。

```c
#include<stdio.h>
int sum();
int main(){
    int addition;
    addition = sum();
    printf("\nSum of two given values = %d", addition);
    return 0;
}
int sum() {
    int a = 50, b = 80, sum;
    sum = a + b;
    return sum;
}
```

**输出:**
```
Sum of two given values = 130
```

## 你知道函数可以返回多少个值吗？
C 函数可以返回多少个值？
- 通常情况下，函数返回一个值。
- 如果你想让函数返回多个值，你可以使用结构体（struct）或指针。
- 在 C99 标准中，可以使用块表达式（block expressions）来返回多个值。





```c
#include <stdio.h>
#include <stdlib.h>
int main(int argc, char *argv[]) { // 命令行参数
    if (argc != 5) {
        printf("Arguments passed through command line not equal to 5");
        return 1;
    }
    printf("\n Program name  : %s \n", argv[0]);
    printf("1st arg  : %s \n", argv[1]); argv[1]);
    printf("2nd arg  : %s \n", argv[2]);
    printf("3rd arg  : %s \n", argv[3]);
    printf("4th arg  : %s \n", argv[4]);
    printf("5th arg  : %s \n", argv[5]);
    return 0;
}
```
**OUTPUT:**
```
Program name : test
1st arg : this
2nd arg : is
3rd arg : a
4th arg : program
5th arg : (null)
```

## 可变长度参数

- 可变长度参数是 C 语言中由 `c99` 标准提供的一种高级概念。在 `c89` 标准中，只能向函数传递固定参数。
- 当函数接收到的参数数量在运行时变化时，可以使用可变长度参数。
- 它表示为 `...`。
- 需要包含 `stdarg.h` 头文件来使用可变长度参数。

### 可变长度参数示例程序：

```c
#include <stdio.h>
#include <stdarg.h>
int add(int num,...);
int main(){
    printf("The value from first call = %d\n", add(2,2,3));
    printf("The value from second call= %d \n", add(4,2,3,4,5));
    return 0;
}
int add(int num,...){
    va_list valist;
    int sum = 0;
    int i;
    va_start(valist, num);
    for (i = 0; i < num; i++){
        sum += va_arg(valist, int);
    }
    va_end(valist);
    return sum;
}
```
**OUTPUT:**
```
The value from first call = 5
The value from second call= 14
```

## C 语言中的指针

C 语言中的指针是存储另一个变量地址的变量。指针用于动态分配内存。指针可以是任何数据类型，如 `int`、`float`、`char`、`double` 等。

- **指针语法**: `data_type *var_name;` 示例：`int *p;` `char *p;` 其中 `*` 用于表示指针变量而不是普通变量。

### 关于 C 指针的关键点：

- 普通变量存储值，而指针变量存储地址。
- `&` 符号用于获取变量的地址。
- `*` 符号用于获取变量的值。
- 如果指针初始化为 `NULL`，意味着它没有指向任何地方。
- 两个指针相减可以知道之间有多少个元素。
- 但不允许进行指针加、乘、除法。

### 指针示例程序：

```c
#include <stdio.h>
int main(){
    int *ptr, q;
    q = 50;
    /* q 的地址赋值给 ptr */
    ptr = &q;/* 显示 q 的值 */
    printf("%d", *ptr);
    return 0;
}
```
**OUTPUT:**
```
50
```

因此对指针可以执行以下操作：
a) **指针加数字**: `int i=4,j,k; J=&i; J=j+1; K=j+3;`
b) **指针减去数字**
c) **一个指针减去另一个指针**:
```c
#include<stdio.h>
int main(){
    int arr[] = { 10,20,30,45,67,56,74};
    int * i,j;
    i=&arr[1];
    j=&arr[5];
    printf("\n %d", j-i);
}
```
d) **指针变量比较**:
```c
#include<stdio.h>
int main(){
    int arr[] = {10,20,36,72,45,36};
    int *j,*k;
    j=&arr[4];
    k=(arr+4);
    if(j==k)
        printf("\n 两个指针指向同一个位置");
    else
        printf("\n 两个指针没有指向同一个位置");
    return 0;
}
```

## 数组

数组是属于相同类型的变量集合。你可以在数组中存储一组相同类型的数据。数组示例：
```c
#include<stdio.h>
int main (){
    int x;
    x=5;
    printf("\n%d",x);
    return 0;
}
```
a) **数组声明**: `int marks[30]`
b) **向数组输入数据**:
```c
for(i=0;i<30;i++){
    printf("\n enter marks");
    scanf("%d",&marks[i]);
}
```
c) **从数组读取数据**:
```c
for(i=0;i<30;i++){
    sum=sum+marks[i];
}
avg=sum/30;
printf("\n average =%d", avg);
```
d) **数组初始化**:
```c
int num[6]={2,4,12,5,45};
float[]={12.3,34.2,-23.4,-11.3};
```
e) **边界检查**: 在 C 中，没有检查用于数组的下标是否超过了数组的大小。
```c
#include<stdio.h>
int main(){
    int num [40],i;
    for(i=0;i<40;++i)
        num[i]=i;
    return 0;
}
```

我们学习了数组：
a) 数组是相似元素的集合
b) 数组中的第一个元素编号为 0，所以最后一个元素的索引小于数组的大小。
c) 数组也称为下标变量。
d) 在使用数组之前，必须声明其类型和维度。
e) 无论数组多大，其元素始终存储在连续内存中。

### 数组的类型

数组有几种类型：
1. 一维数组
2. 二维数组
3. 三维数组
4. 多维数组等

#### 1. 一维数组
语法：`data_type array_name[size];` 示例：`int a[5];` `char str[10];`

**一维数组示例程序：**
```c
#include <stdio.h>
int main(){
    int a[5] = {10, 20, 30, 40, 50};
    int i;
    for(i=0; i<5; i++){
        printf("%d ", a[i]);
    }
    return 0;
}
```

#### 2. 二维数组
语法：`data_type array_name[rows][columns];` 示例：`int arr[2][3];`

**二维数组示例程序：**
```c
#include <stdio.h>
int main(){
    int arr[2][3] = {{1, 2, 3}, {4, 5, 6}};
    int i, j;
    for(i=0; i<2; i++){
        for(j=0; j<3; j++){
            printf("%d ", arr[i][j]);
        }
        printf("\n");
    }
    return 0;
}
```

#### 3. 字符串
字符串是以空字符（`\0`）终止的字符数组。语法：`char string_name[];` 示例：`char str[] = "Hello";`

**字符串示例程序：**
```c
#include <stdio.h>
int main(){
    char str[] = "Hello";
    printf("%s", str);
    return 0;
}
```




`printf()` 中使用的 `%s` 是用于打印字符串的格式说明符。相同的说明符也可以用于从关键字接收字符串，如下：

```c
#include<stdio.h>
int name(){
    char name[25];
    printf(\n enter your name”);
    scanf(“%s”,name);
    printf(“ hello  %s !\n”, name);
    return 0;
}
```
输出：
Enter your name  Debnath
Hello Debnath

**注意：** 使用 `scanf()` 输入字符串时，我们必须注意以下两点：
A) 字符串的长度不应超过字符数组的维度。这是因为 C 编译器不会对字符数组进行边界检查。
B) `scanf()` 无法接收多单词的字符串。因此，像 ‘Debnath’ 这样的名字是不被接受的。

解决这一局限制的方法是使用 `gets()` 函数。`gets()` 函数及其对应的 `puts()` 函数的用法所示：

```c
#include <stdio.h>
int main (){
    Char name[25];
    Printf(\n enter your full name “);
    Gets( name);
    Puts(“hello”);
    Puts(name)
    Return 0;
}
```
输出：
Enter your full name  Deb nath Roy
Hello !Debnath Roy

### 字符串指针
我们可以将一个 `char` 指针赋值给另一个 `char` 指针，例如：

```c
#include<stdio.h>
int main(){
    char str[]= “hello”;
    char str2[10];
    char *s=”good morning”;
    char *q;
    str2=str1;/*error*/
    q=s;/*works*/
    return 0;
}
```

### 标准库字符串函数
每个 C 编译器都提供了一系列实用的字符串处理库函数。列出更常用的函数及其用途：

| 函数 | 用途 |
| :--- | :--- |
| `strlen()` | 查找字符串长度 |
| `strlower()` | 将字符串转换为小写 |
| `strupper()` | 将字符串转换为大写 |
| `strcat()` | 将一个字符串附加到另一个字符串末尾 |
| `strcpy()` | 将一个字符串复制到另一个字符串 |
| `strcmp()` | 比较两个字符串 |
| `strrev()` | 反转字符串 |





# 声明结构

示例：
```c
ExampleStruct book{
    Char name;
    Float price;
    Int pages;
};
```

**注意：**
a) 结构类型声明中的结束大括号后面必须跟一个分号。
b) 重要的是，结构类型声明并没有告诉编译器在内存中预留任何空间。结构声明的作用仅仅是定义结构体的形式。
c) 通常，结构类型声明出现在源代码文件的顶部，在定义任何变量或函数之前。
d) 如果结构体变量初始化为值 `{0}`，则它的所有元素都被设置为 0。这是初始化结构体变量的一种方便方法。

# 访问结构元素

在声明了结构类型和结构体变量后，让我们看看如何访问结构体的元素。它们使用点 (`.`) 运算符。因此，要引用示例程序中定义的结构 `pages`，我们必须使用 `B1.pages`。同样地，要引用 `price`，我们将使用 `B1.price`。

## 结构元素是如何存储的

示例：
```c
#include<stdio.h>
int main(){
    struct book{
        Char name;
        Float price;
        Int pages;
    };
    struct book b1={'B',130.00,550};
    printf("\n address of name=%u",&b1.name);
    printf("\n address of price =%u", & b1.price);
    printf("\n address of pages =%u",&b1.pages);
    return 0;
}
```
**输出：**
```
Address of name =65518
Address of price=65519
Address of pages =65523
```
结构元素在内存中的存储所示：
`b1.name` | `b1.price` | `b1.pages`
`'b'` | `130.00` | `550`
`65518` | `65519` | `65523`

## 结构体数组

示例：
```c
#include<stdio.h>
void link float();
int main (){
    struct book{
        char name;
        float price;
        int pages;
    };
    struct book b[100];
    int i;
    for(i=0;i<=99;i++){
        printf (\n enter names, price, and pages");
        fflush(stdin);
        scanf(" %c%f%d",&b[i].name,&b[i].price,&b[i].pages);
    }
    for(i=0;i<=99;i++)
        printf("\n %C%f%d",b[i].name,b[i].price,b[i].pages);
    return 0;
}
void link float(){
    float a=0,*b;
    b=&a;
    a=*b
}
```

**注意：**
a) 结构体数组的声明方式：
`struct book b[100];`
这在内存中为 100 个 `struct book` 类型的结构体提供了空间。
b) 我们引用数组 `b` 中每个元素的语法与用于整型和字符型数组的语法相似。
c) 即使使用了结构体，也无法实现编程的便利性，因为需要处理大量的变量（用于存储百本书数据的 `b1` 到 `b100`）。因此，它允许我们创建一个结构体数组。
d) 在结构体数组中，数组的所有元素都存储在相邻的内存位置上。
e) `linkfloat()` 函数在这里的作用是什么？
它强制将浮点模拟器链接到应用程序中。没有必要调用此函数，只需在程序的任何地方定义它即可。

# 结构的附加功能

- 结构体变量的值可以使用赋值运算符赋予另一个相同类型的结构体变量。

## 赋值运算符用于逐个拷贝

示例：
```c
#include<stdio.h>
#include<string.h>
int main(){
    struct employee{
        char name[10];
        int age;
        float salary;
    };
    struct employee e1={"sanjay",30,5500.50};
    struct employee e2,e3;
    /*逐个拷贝*/
    strcpy(e2.name,e1.name);    /*e2.name=e1.name 是错误的*/
    e2.age=e1.age;
    e2.salary=e1.salary;
    /*一次性拷贝所有元素*/
    e3=e2;
    printf("\n %s %d %f", e1.name,e1.age,e1.salary);
    printf("\n %s %d %f ", e2.name,e2.age,e2.salary);
    printf("\n %s %d %f ", e3.name,e3.age,e3.salary);
    return 0;
}
```
**输出：**
```
Sanjay 30 5500.500000
Sanjay 30 5500.500000
Sanjay 30 5500.500000
```

## 嵌套结构

示例：
```c
#include<stdio.h>
int main(){
    struct address{
        char phone[15];
        char city[25];
        Int pin;
    };
    struct emp{
        char name[25];
        struct address a;
    };
    struct emp e={"jeru", {"531046","nagpur",10}};
    printf("name=%s phone=%s \n",e.name,e.a.phone);
    printf("\n city=%s pin=%d",e.a.city,e.a.pin);
    return 0;
}
```
**输出：**
```
Name=jeru phone=531046
City=Nagpur pin =10
```

## 结构体变量传递函数

示例：
```c
#include<stdio.h>
void display(char*,char*,int);
int main(){
    struct book{
        char name[25];
        char author[25];
        Int callno;
    };
    struct book b1={"let us", "YPK",101};
    display(b1.name,b1.author,b1.callno);
    return 0;
}
void display(char*s, char*t,int n){
    printf("%s %s %d \n", s, t, n);
}
```
**输出：**
```
Let us YPK 101
```

## 指向函数

示例：
```c
#include<stdio.h>
struct emp{
    int a;
    char ch;
    float s;
};
int main(){
    struct emp e;
    printf("\n %u %u ", &e.ch,&e.s);
    return 0;
}
```
**输出：**
- 使用 `TC/TC++` 编译器得到的地址为：`65518`, `65520`
- 使用 std 输出为：`242044`, `24502`

# printf()

**注意：** `printf()` 不仅可以打印变量的值，还可以打印表达式的结果。表达式就是常量、变量和运算符的有效组合。因此，`3`、`3+2`、`c` 和 `a+b*c` 都是有效的表达式。这些表达式的结果如下所示打印。

```c
printf("\n %d%d%d", 3,3+2,c,a+b*c);
```

**示例：**
```c
#include <stdio.h>
int main(){
    char ch = 'A';
    char str[20];
    float flt = 10.234;
    int no = 150;
    double dbl = 20.123456;
    printf("Character is %c \n", ch);
    printf("String is %s \n", str);
    printf("Float value is %f \n", flt);
    printf("Integer value is %d\n", no);
    printf("Double value is %lf \n", dbl);
    printf("Octal value is %o \n", no);
    printf("Hexadecimal value is %x \n", no);
    return 0;
}
```
**输出：**
```
Character is A
Float value is 10.234000
Integer value is 150
Double value is 20.123456
Octal value is 226
Hexadecimal value is 96
```
你可以看到输出与程序中 `printf` 语句双引号内放置的数据相同。

# scanf()

为了使程序通用化，程序本身在执行期间应该要求用户通过键盘提供 `p`、`n`、`r` 值。这可以通过名为 `scanf()` 的函数来实现。

示例：
```c
#include <stdio.h>
int main(){
    char ch;
    char str[100];
    printf("Enter any character \n");
    scanf("%c", &ch);
    printf("Entered character is %c \n", ch);
    printf("Enter any string ( upto 100 character ) \n");
    scanf("%s", str);
    printf("Entered string is %s \n", str);
}
```
**输出：**
```
Enter any character a
Entered character is a
Enter any string ( upto 100 character ) hai
Entered string is hai
```
**注意：**
- `scanf()` 语句中使用格式说明符 `%d`。这样输入的值就被作为整数接收，`%s` 用于字符串。
- 在 `scanf()` 语句中，变量名 `ch` 之前使用了取地址符 `&`。
- 这就像在指针中一样，用于指向变量。

关于指针如何运作的更多信息：
- `printf()` 用于显示输出，`scanf()` 用于读取输入。
- `printf()` 和 `scanf()` 函数在 C 库的 `stdio.h` 头文件中声明。
- C 语言中的所有语法（包括 `printf()` 和 `scanf()` 函数）都是大小写敏感的。

# 预处理器指令

在 C 程序被编译器编译之前，源代码会由一个名为预处理器的程序进行处理。这个过程被称为预处理。
- 预处理器中使用的命令称为预处理器指令，它们以 `#` 符号开头。

**c 预处理器的特性：**
a) 宏展开
b) 文件包含
c) 条件编译
d) 杂杂指令

编译后的 C 程序创建了 4 个内存区域。它们是：
1. **第一个区域** —— 这是存储程序执行代码的内存区域。
2. **第二个区域** —— 全局变量存储在这个内存区域中。
3. **第三个区域** —— 栈 (stack)
4. **第四个区域** —— 堆 (heap)

你知道 C 语言中栈内存和堆内存的区别吗？

| 栈 | 堆 |
| :--- | --- |
| 栈是在 C 程序执行期间存储“局部变量”、“函数调用返回地址”和“函数参数”的内存区域。 | 堆是运行时由动态内存分配函数使用的内存区域。 |





| CPU 的当前状态保存在栈内存中 | 链表是使用堆内存的一个示例。 |

# 你知道 C 语言中编译器与解释器之间的区别吗？

| 编译器 (Compilers) | 解释器 (Interpreters) |
| :--- | :--- |
| 编译器读取程序的完整源代码并转换为二进制代码。这个过程被称为编译。二进制代码也被机器码、可执行文件和对象代码。 | 解释器逐一行读取程序源代码并执行该行。这个过程被称为解释。 |
| 程序运行速度快。 | 程序运行速度慢。 |
| 执行一次。例如：C, C++ | 解释发生在程序的每一行。例如：BASIC |

## 宏展开 (Macro Expansion)

### 示例：
```c
#include<stdio.h>
#define UPPER 25
int main((){
    int i;
    for(i=1;i<=UPPER;i++)
        printf("%d\n");
    return 0;
}
```
这条语句被称为宏定义，或者通称为“宏”，它的作用是什么？在预处理期间，它会将程序中每个 `UPPER` 出现的地方替换为 `25`。

### 带参数的宏
我们目前为止使用的宏被称为简单宏。宏可以有参数，就像函数可以一样。这里有一个示例：
```c
#include<stdio.h>
#define AREA(x) (3.14*x*x)
int main(){
    float ri =60,r2=2.5,a;
    a=AREA(r1);
    printf("AREA of circle=%f\n",a);
    a=AREA(r2);
    printf(" AREA of circle=%f\n",a);
    return 0;
}
```
**输出：**
Area of circle=1220.656250
Area of circle= 19.625000

**注意：**
- **A)** 在定义宏时，注意不要在宏模板和它的参数之间留空格，例如：在定义中 `area` 和 `(x)` 之间不应有空格，`#define AREA(x) (3.14*x*x)`
- **B)** 整个宏展开应该包含在括号内。
- **C)** 宏可以分成多行，在每行的末尾有一个反斜杠 `\` `。
- **D)** 如果由于任何原因，你无法调试宏，那么你应该查看程序的展开代码，以查看宏是如何被展开的。

## 文件包含 (File Inclusion)

我们在本章中将探索的第二个预处理器指令是文件包含。该指令导致一个文件被包含在另一个文件中。
`#include"filename"`

### 何时以及为什么要使用此功能？
它可以用于以下两种情况：
- **A)** 将大型程序的不同部分分开是一项良好的编程习惯。这些文件在主程序文件的开头被 `#included`。
- **B)** 有些函数和某些宏定义，在我们编写的几乎每个程序中都需要它们。这些常用的函数和宏定义可以存储在一个文件中，并包含在我们编写的每个程序。
- **C)** 当我们创建想要分发给他人的函数库时。在这种情况下，函数定义在 “.c” 文件中，相应的原型声明和宏定义在 “.h” 文件中声明。

## 条件编译 (Conditional Compilation)

### C 语言中 #DEFINE, #INCLUDE 预处理器的示例程序：

- `#define` – 此宏定义常量值，并可以是任何基本数据类型之一。
- `#include <file_name>` – 文件“file_name”的源代码被包含在提到 `#include <file_name>` 的主 C 程序中。

```c
#include <stdio.h>
#define height 100
#define number 3.14
#define letter 'A'
#define letter_sequence "ABC"
#define backslash_char '\?'
void main(){
    printf("value of height     : %d \n", height );
    printf("value of number : %f \n", number );
    printf("value of letter : %c \n", letter );
    printf("value of letter_sequence : %s \n", letter_sequence);
    printf("value of backslash_char  : %c \n", backslash_char);
}
```
**输出：**
| value of height : 100 | value of number : 3.140000 | value of letter : A | value of letter_sequence : ABC | value of backslash_char : ? |

### 条件编译指令的示例程序：

#### A) C 语言中 #IFDEF, #ELSE 和 #ENDIF 的示例程序：

- “#ifdef” 指令检查特定宏是否已定义。如果已定义，则“If”句语句包含在源文件中。
- 否则，“else”句语句被包含在源文件中进行编译和执行。

```c
#include <stdio.h>
#define RAJU 100
int main(){
#ifdef RAJU
    printf("RAJU is defined. So, this line will be added in " \"this C file\n");
#else
    printf("RAJU is not defined\n");
#endif
    return 0;
}
```
**输出：**
| RAJU is defined. So, this line will be added in this C file |

#### C 语言中 #IFNDEF 和 #ENDIF 的示例程序：

- `#ifndef` 的作用恰好与 `#ifdef` 指令相反。如果特定宏未定义，则“If”句语句包含在源文件中。
- 否则，“else”句语句被包含在源文件中进行编译和执行。

```c
#include <stdio.h>
#define ROHIT 100
int main(){
#ifndef SELVA
    printf("SELVA is not defined. So, now we are going to " \"define here");
#endif
    return 0;
}
```
**输出：**
| SELVA is not defined. So, now we are going to define here |

### C 语言中 #IF, #ELSE AND #ENDIF 的示例程序：

- “#if” 指令检查特定宏是否已定义。如果已定义，则“If”句语句包含在源文件中。
- 否则，“else”句语句被包含在源文件中进行编译和执行。

```c
#include <stdio.h>
#define RAJU 100
int main(){
#ifdef RAJU
    printf("RAJU is defined. So, this line will be added in " \"this C file\n");
#else
    printf("RAJU is not defined\n");
#endif
    return 0;
}
```
（注：此处原文代码中误用了 #ifdef 而非 #if，翻译保留原样逻辑）

## 杂项指令 (Miscellaneous Directive)

### A) #undef
在某些情况下，可能希望一个定义的名称变为“未定义”。这可以通过 `#undef` 指令来实现。

C 语言中 UNDEF 的示例程序：
```c
#include <stdio.h>
#define height 100
void main(){
    printf("First defined value for height :%d\n",height);
    #undef height
    //重新定义值
    #define height 600
    printf("value of height after redefine:",height);
}
```
**输出：**
（注：此处逻辑输出结果）

### B) #pragma
这是另一个特殊目的指令，你可以用它开启或关闭某些功能。Pragma 随编译器而异。

- **a) #pragma startup 和 #pragma exit**: 这些指令允许我们指定在程序启动（main() 之前）或程序退出（程序终止之前）调用的函数。
- **b) #pragma warn**:编译时编译器报告程序中的错误和警告。

C 语言中 PRAGMA 的示例程序：
```c
#include <stdio.h>
void function1( );
void function2( );
#pragma startup function1
#pragma exit function2
int main( ){
    printf ( "\n Now we are in main function" ) ;
    return 0;
}
void function1( ){
    printf("\nFunction1 is called before main function");
}
void function2( ){
    printf ( "\nFunction2 is called just before end of " \"main function" ) ;
}
```

## 文件处理 (File Handling)

什么是文件 (FILE)?
文件是存储在磁盘等辅助存储设备上的字节集合。系统中有两种文件。它们是，

1.  文本文件 (ASCII)
2.  二进制文件

*   文本文件包含数字、字母和符号的 ASCII 码。
*   二进制文件包含字节集合（0 和 1）。二进制文件是文本文件的编译后版本。

C 编程中的基本文件操作：
在 C 编程语言中，可以对任何文件执行 4 种基本操作。它们是，

1.  打开/创建文件
2.  关闭文件
3.  读取文件
4.  向文件中写入





# C 语言中对文件执行的操作模式

打开文件有很多模式。根据文件的模式，可以以读取、写入或追加文本的方式打开。它们列举如下。

## C 语言打开文件、写入文件和关闭文件的示例程序

```c
/* * Open, write and close a file : */
# include <stdio.h>
#include <string.h>
int main( ){
    FILE *fp ;
    char data[50];
    // opening an existing file
    printf( "Opening the file test.c in write mode" ) ;
    fp = fopen("test.c", "w") ;
    if ( fp == NULL ){
        printf( "Could not open file test.c" )
        return 1;
    }
    printf( "\n Enter some text from keyboard to write in the file test.c" ) ;
    // getting input from user
    while ( strlen ( gets( data ) ) > 0 ){
        // writing in the file
        fputs(data, fp) ;
        fputs("\n", fp) ;
    }
    // closing the file
    printf("Closing the file test.c") ;
    fclose(fp) ;
    return 0;
}
```

**输出:**
```
Opening the file test.c in write mode
Enter some text from keyboard to write in the file test.c
Hai, How are you?
Closing the file test.c
```

## C 语言打开文件、读取文件和关闭文件的示例程序

这个文件处理 C 语言程序说明了如何读取文件内容。假设一个名为“test.c”的文件包含以下数据“Hai, How are you?”。让我们使用下面的 C 程序读取这些数据。

```c
/* Open, Read and close a file: reading string by string */
# include <stdio.h>
int main( ){
    FILE *fp ;
    char data[50] ;
    printf( "Opening the file test.c in read mode" ) ;
    fp = fopen( "test.c", "r" ) ;
    if ( fp == NULL ){
        printf( "Could not open file test.c" )
        return 1;
    }
    printf( "Reading the file test.c" ) ;
    while( fgets ( data, 50, fp ) != NULL )
        printf( "%s" , data ) ;
    printf("Closing the file test.c") ;
    fclose(fp) ;
    return 0;
}
```

**输出:**
```
Opening the file test.c in read mode
Reading the file test.c
Hai, How are you?
Closing the file test.c
```

## C 语言编程中 FOPEN(), FCLOSE(), GETS() 和 FPUTS() 函数的示例程序

```c
/* * Open, write and close a file : */
# include <stdio.h>
#include <string.h>
int main( ){
    FILE *fp ;
    char data[50];
    // opening an existing file
    printf( "Opening the file test.c in write mode" ) ;
    fp = fopen("test.c", "w") ;
    if ( fp == NULL ){
        printf( "Could not open file test.c" )
        return 1;
    }
    printf( "\n Enter some text from keyboard to write in the file test.c" ) ;
    // getting input from user
    while ( strlen ( gets( data ) ) > 0 ){
        // writing in the file
        fputs(data, fp) ;
        fputs("\n", fp) ;
    }
    // closing the file
    printf("Closing the file test.c") ;
    fclose(fp) ;
    return 0;
}
```

**输出:**
```
Opening the file test.c in write mode
Enter some text from keyboard to write in the file test.c
Hai, How are you?
Closing the file test.c
```

## C 语言编程中 PUTW(), GETW() 函数的示例程序

这个文件处理 C 语言程序说明了如何使用 `putw()` 函数写入文件，以及如何使用 `getw()` 函数读取同一文件。

```c
#include <stdio.h>
int main (){
    FILE *fp;
    int i=1, j=2, k=3, num;
    fp = fopen ("test.c","w");
    putw(i,fp);
    putw(j,fp);
    putw(k,fp);
    fclose(fp);
    fp = fopen ("test.c","r");
    while(getw(fp)!=EOF){
        num= getw(fp);
        printf(“Data in test.c file is %d \n”, num);
    }
    fclose(fp);
    return 0;
}
```

**输出:**
```
Data in test.c file is 1
2
3
```

## C 语言编程中 FGETC() 函数的示例程序

这个文件处理 C 语言程序说明了如何读取文件内容。假设一个名为“test.c”的文件包含以下数据“Hi, How are you?”。让我们使用 `fgetc()` 函数通过下面的 C 程序读取这些数据。

```c
/* Open, Read and close a file: reading string by string */
# include <stdio.h>
int main( ){
    FILE *fp ;
    char data[50];
    printf( "Opening the file test.c in read mode" ) ;
    fp = fopen( "test.c", "r" ) ;
    if ( fp == NULL ){
        printf( "Could not open file test.c" )
        return 1;
    }
    printf( "Reading the file test.c" ) ;
    while( fgets ( data, 50, fp ) != NULL )
        printf( "%s" , data ) ;
    printf("Closing the file test.c") ;
    fclose(fp) ;
    return 0;
}
```

**输出:**
```
Opening the file test.c in read mode
Reading the file test.c
Hi, How are you?
Closing the file test.c
```

## C 语言其他内置文件函数

C 语言提供了许多其他内置函数用于处理。它们列举如下。

### TYPEDEF 的示例程序

```c
#include <stdio.h>
#include <string.h>
typedef struct {
    int id;
    char name[20];
    float percentage;
} status;
int main(){
    status record;
    record.id=1;
    strcpy(record.name, "Binod");
    record.percentage=86.5;
    printf("%d \n", record.id);
    printf("%s \n", record.name);
    printf("%f \n", record.percentage);
    return 0;
}
```

**输出:**
```
1
Binod
86.500000
```

### C TYEDEF 的另一个示例程序

```c
#include <stdio.h>
#include <limits.h>
int main() {
    long long LLI;
    printf("Storage size: %ld \n", sizeof(LLI));
    return 0;
}
```

**输出:**
```
8
```

## 联合体 (UNION) 比 结构体 (STRUCTURE)

*   联合体和结构体的区别在于内存分配。
*   结构体为所有成员单独分配空间。
*   而联合体一次只分配一个成员的空间。结构体可以访问所有成员值。

### C 联合体的示例程序

```c
#include <stdio.h>
#include <string.h>
union student {
    char name[20];
    char subject[20];
    float percentage;
};
int main(){
    union student record1;
    union student record2;
    // 为 record1 联合体赋值
    strcpy(record1.name, "Amir");
    strcpy(record1.subject, "Maths");
    record1.percentage = 86.50;
    printf("Union record1 example\n");
    printf(" Name: %s \n", record1.name);
    printf(" Subject: %s \n", record1.subject);
    printf(" Percentage: %f \n", record1.percentage);

    // 为 record2 联合体赋值
    printf("Union record2 example\n");
    strcpy(record2.name, "Mani");
    printf(" Name: %s \n", record2.name);
    strcpy(record2.subject, "Physics");
    record2.percentage = 99.50;
    printf(" Percentage: %f \n", record2.percentage);
    return 0;
}
```

**输出:**
```
Union record1 example
 Name: Amir
 Subject: Maths
 Percentage: 86.500000
Union record2 example
 Name: Mani
 Percentage: 99.500000
```

**上述 C 联合体程序的解释:**
Record1 联合体变量：

*   “Amir” 被赋值给联合体成员 `record1.name` 。内存位置名称为 `record1.name`，存储在该位置的值为“Amir”。





* 接着，将“Maths”赋值给 union 成员 `record1.subject`。现在，内存位置名称变为 `record1.subject`，值为“Maths”（union 一时间只能包含一个成员）。
* 接着，将“86.50”赋值给 union 成员 `record1.percentage`。现在，内存位置名称变为 `record1.percentage`，值为“86.50”。
* 像这样，union 成员的名称和值每次在公共存储空间上都会被重写。
* 因此，我们始终只能访问最后一次被赋值的那个 union 成员。我们无法访问其他成员的值。
* 所以，输出中只显示 `record1.percentage` 的值。`record1.name` 和 `record1.percentage` 都是空的。
* 如果我们想使用 union 访问所有成员的值，我们必须在给其他成员赋值之前访问该成员，如此程序中的 `record2` union 变量所示。
* 在 `record2` 示例中，每个 union 成员在向其赋值后后立即被访问。
* 如果我们没有在给其他成员赋值之前访问它们，成员名称和值将被其他成员重写，因为所有成员都使用相同的内存。
* 我们无法同时访问 union 中的所有成员，但结构（structure）可以做到。

### 示例程序 – 声明 C union 的另一种方式：

```c
#include <stdio.h>
#include <string.h>
union student{
    char name[20];
    char subject[20];
    float percentage;
}record;
int main(){
    strcpy(record.name, "Rajib");
    strcpy(record.subject, "Maths");
    record.percentage = 86.50;
    printf(" Name       : %s \n", record.name);
    printf(" Subject    : %s \n", record.subject);
    printf(" Percentage : %f \n", record.percentage);
    return 0;
}
```

### 输出：
```
Name :Rajib
Subject :Maths
Percentage : 86.500000
```

### 注意：
* 我们一次只能访问 union 的一个成员。无法同时访问 union 中所有成员的值。
* 但结构可以同时访问所有成员的值。这是因为 `Union` 为其所有成员分配了一个公共存储空间。而 `Structure` 为其所有成员单独分配存储空间。

### C 语言中结构（structure）和 union 的区别：

| C 结构 | C union |
| :--- | :--- |
| 结构为所有成员单独分配存储空间。 | union 为所有成员分配一个公共存储空间。union 会发现哪一个成员比其他成员需要更大的存储空间，并分配相应的空间。 |
| 结构占用更高的内存空间。 | union 占用的内存空间比结构少。 |
| 我们可以一次访问结构的所有成员。 | 我们一次只能访问 union 的一个成员。 |
| 结构示例：`struct student { int mark; char name[6]; double average; };` | union 示例：`union student { int mark; char name[6]; double average; };` |
| 对于上述结构，内存分配如下：`int mark` – 2B，`char name[6]` – 6B，`double average` – 8B。总内存分配 = 2+6+8 = 16 Bytes | 对于上述 union，将分配 8 字节内存，因为 `double` 数据类型在所有数据类型中占据最大的内存空间。总内存分配 = 8 |

### 关于作者
Susanta Bouri
计算机科学硕士
Maulana Abul Kalam Azad University Of Technology,
西孟加拉邦（印度）

