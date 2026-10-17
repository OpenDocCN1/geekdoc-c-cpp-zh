
```c
#include <stdio.h>
#include <conio.h>
void main() {
    char a[] = "king";
    char *p = "queen";
    a = "queen";
    p = "king";
    printf("\n %s", a);
}
```

答：代码报错。需要左值。

## 18 使用预处理器指令

### 目标

- 18.1 使用包含指令
- 18.2 使用宏替换指令
- 18.3 使用编译器控制指令

C 语言促进了使用预处理语句，这些语句在程序翻译成机器语言之前执行。换句话说，程序中的预处理语句不是程序语句；它们是指令。这些语句始终以哈希（`#`）符号开头，且永远以分号（`;`）结尾。在程序中，你可以通过使用预处理器指令在 C 语言源码中为编译器提供各种指令。例如，通过使用 `#include` 预处理器指令，你可以指令编译器包含头文件。在 C 中，预处理器作为一个独立的程序在编译翻译时调用。预处理器指令编译器执行特定操作。例如，预处理器允许你向源文件插入或定义宏的值。表 1 列出了 C 语言中常用的预处理器指令及其功能。

| 表 1：常用的预处理器指令及其功能 |
| :--- | :--- |
| 指令 | 功能 |
| `#include` | 指定要包含的文件 |
| `#define` | 定义宏替换 |
| `#undef` | 取消宏定义 |
| `#ifdef` | 测试宏是否定义 |
| `#ifndef` | 测试宏是否未定义 |
| `#if` | 测试编译时条件 |
| `#endif` | 指定 `#if` 的结束 |
| `#else` | 当 `#if` 测试失败时指定替代方案 |
| `#ifelse` | 当条件不为真时指定操作 |
| `#ifelif` | 当有多个决策点时允许采取一个操作 |

关于预处理器指令的简短说明（计算机概念与 C 编程 (VTU, 1/2月 2005)）

# 446 ► 第 18 章

表 1 中列出的指令分为以下几类：

- 文件包含指令
- 宏替换指令
- 编译器控制指令

本章将帮助你探索各种预处理器指令，例如 `#include`、`#define`、`#endif`、`#ifdef` 和 `#line`，这些在前面的页面已经进行了分类。你可以在本章中找到许多演示预处理器指令实现的程序。

### 18.1 使用文件包含指令

C 语言提供了 `#include` 指令将文件包含在程序的源文件中。一个包含函数或宏定义的外部文件可以作为程序的一部分被包含，这样你就不需要重写这些函数或宏定义。

这是通过 `#include "header filename"` 实现的，其中 `filename` 是包含所需定义或函数的文件名。此时，预处理器会将该文件的整个内容插入到程序的源代码中。当 `filename` 被包含在双引号内时，搜索器会首先在当前目录中搜索该文件，然后在标准目录中搜索。

或者，这也可以用于 `#include <filename>` 形式，即不使用双引号。在这种情况下，只会在标准目录中搜索文件，且这种包含声明仅用于标准头文件。允许包含文件的嵌套，前提是被包含的文件可以包含其他文件。然而，一个文件不能包含自身。如果被包含的文件不是，则会报告错误并终止编译。

► 列表 1：使用 `#include` 指令

```c
#include <stdio.h>
#include <io.h>
/* 演示 #include 指令的使用 */
int main() {
    clrscr();
    printf("program demonstrates the use of the file inclusion\ndirective");
```

在列表 1 中，`stdio.h` 文件是一个系统文件，它通过 `#include` 指令被包含在程序中。`main()` 函数中使用的 `printf()` 函数在 `std.h` 文件中声明。因此，在列表 1 中，你不需要编写 `printf()` 函数的实现；相反，你只需使用 `printf()` 函数在控制台上显示文本。

> 介绍 C 语言提供的头文件（计算机概念与 C 编程 (VTU, 2006年7月/8月)）

![](img/655987774ce63b710f1a1b263f2c84e0_465_0.png)

# 使用预处理器指令

在理解文件包含指令的实现后，现在让我们探索宏替换指令。

### 18.2 使用宏替换指令

宏定义是一个程序中的标识符被替换为由一个或多个标记组成的预定义字符串的过程。C 语言提供了 `#define` 指令来完成此任务。`#define` 语句通常被称为宏定义（或简单称为宏），其语法遵循 `#define` 指令的格式：

```c
#define identifier string
```

如果前面的语句包含在程序的开头，预处理器会将源代码中 `identifier` 的每次出现处都替换为该字符串。字符串可以是任何文本，而标识符必须是有效的 C 标识。你可以定义以下任一宏：

- 简单宏
- 带参数的宏
- 嵌套宏

让我们详细讨论其中的每一个。

#### 定义简单宏

在本小节中，你将学习如何使用 `#define` 指令定义简单宏。在定义宏时，你需要为该标识符提供一个标识符和一个该标识符的值。列表 2 显示了如何使用 `#define` 指令创建一个简单宏：

► 列表 2：定义简单宏

```c
#include <stdio.h>
/* 使用 #define 指令 */
#define VAL 35
#define HELLO "HELLO"
int main() {
	int res;
	clrcr();
	res = VAL-5;
	printf("res = VAL-5: %d\n", res);
	printf(HELLO);
	getch();
}
```

输出：

```
res = VAL-5: res = 30
HELLO
```

在列表 2 中，定义了以下宏：

```c
#define VAL 35
#define HELLO "HELLO"
```

`VAL` 被定义为整数 35，`HELLO` 是一个包含 "HELLO" 值的字符串。每当 `VAL` 和 `HELLO` 变量在程序中出现时，它们会被替换为指定的值。`res` 整型变量被声明并赋值为比 `VAL` 变量值少 5。因此，显示 30 作为 `res` 变量的值。此外，`HELLO` 变量的值也显示为 HELLO。你必须注意，预处理器指令不是 C 语句，因此它们不以分号结尾。`#include` 指令告诉编译器在编译程序之前将指定文件的所有内容包含在源文件中。

你还可以使用 `#undef` 指令取消由 `#define` 指令分配给变量的值。

```c
#include <stdio.h>
/* 使用 #undef 指令 */
#define VAL 35
#undef VAL
#define VAL 40
int main() {
    }
```

在前面的代码段中，首先使用 `#define` 指令定义 `VAL` 变量的值值为 35。随后，使用 `#undef` 指令取消 `VAL` 变量的定义。然后，再次将 `VAL` 变量的值定义为 40。

你已经学习了如何定义宏。现在让我们学习如何定义带参数的宏。

#### 定义带参数的宏

与函数类似，你也可以定义接受参数的宏。使用以下语法来定义宏：

```c
#define identifier (expression)
```

当调用宏时，预处理器用实际参数替换表达式。例如：

```c
#define CUBE(x) (x*x*x)
```

如果提供了代码语句 `volume = CUBE(side);`，那么编译器将其解释为 `volume = (side * side * side)`。

参数的每次出现都应该使用括号。而且整个字符串应该放在括号内。例如，预处理器将其展开为 `printf("price x quantity=%f", price x quantity);`。

列表 3 显示了如何定义带参数的宏：

► 列表 3：带参数的宏

```c
#include <stdio.h>
#define A(x) (3.14*x*x)
/* 演示定义带参数的宏 */
int main() {
    float r, area ;
    clrscr();
    printf("Give radius: ");
    scanf("%f", &r);
    area = A(r);
    printf("Area of circle with radius %5.2f = %8.2f",r,area);
    getch();
}
```

输出：

```
Give radius:10
Area of circle with radius 10.00 = 314.16
```

在列表 3 中，`#define` 指令用于定义一个宏参数，即 `A(x)`，其中 `x` 是参数。根据传递作为参数的值计算圆面积后，变量被赋值。在执行列表 3 提供的代码期间，用户必须提供半径的输入，面积将作为输出显示在控制台上。

在创建了带参数的宏后，现在让我们讨论如何创建嵌套宏。

#### 定义嵌套宏

当一个宏定义在另一个宏内部时，它被称为嵌套宏。例如：

```c
#define M S
#define N+1 ((x))
#define SQUARE(x) ((x) * (x))
#define CUBE(x) (SQUARE(x) * (x))
#define SIXTH(x) (CUBE(x) * CUBE(x))
```

在嵌套宏中，宏可以作为其他宏的参数。

列表 4 显示了如何声明嵌套宏：

► 列表 4：显示星形三角形的多行宏

```c
#include <stdio.h>
/* 演示如何定义嵌套宏 */
```

# 第 18 章

输出：

行数 = 8

***

****

*****

******

*******

********

*********

n***

在列表 4 中，定义了一个嵌套宏，用于根据用户输入的输入指定的行数显示由星号组成的三角形。

在理解了宏替换指令后，现在让我们来探索 C 语言中的编译器控制指令。

## 使用编译器控制指令

- `#ifdef`
- `#ifundef`
- `#if`
- `#else`
- `#endif`

编译器控制指令用于在特定条件下条件地包含头文件或在指定条件下定义宏。编译器控制指令如下：

让我们讨论如何使用这些编译器控制指令中的每一个。

### `#ifdef` 指令

`#ifdef` 指令用于验证宏是否已定义。如果该标识符被定义为宏，则编译器将翻译后续条件后的代码行。考虑一种你需要定义 USD 和 UKP 货币汇率的情况。在这种情况下，你创建了两个头文件来为 USD 和 UKP 定义宏。列表 5 提供了定义 USD 宏的代码：

#### 列表 5：file1.h 头文件

```c
#define USD 1
```

基于同样的原理，你在 file2.h 文件中定义了 UKP 宏，如列表 6所示所示

#### 列表 6：file2.h 头文件

```c
#define UKP 1
```

在定义了 USD 和 UKP 的宏后，现在只包含 file1 头文件并分配汇率。列表 7 显示了使用 `#ifdef` 指令来定义 `currency_rate` 宏：

#### 列表 7：`#ifdef` 指令的使用

```c
#include <stdio.h>
#include <file1.h>
#ifdef
#define currency_rate 46
#endif
#ifdef UKP
#define currency_rate 100
#endif
main() {
    int rs;
    rs = 10 * currency_rate;
    printf("%d\n", rs);
    getch();
}
```

```
输出:
460
```

`#ifdef` 指令用于验证指定的标识符是否定义。例如，在列表 7 中，`USD` 和 `UKP` 标识符指定在 `#ifdef` 指令之后。因此，`#ifdef` 指令会检查这些标识符是否已定义。此外，我们只包含了包含 `USD` 宏的 file1 头文件；因此，C 编译器定义的 `currency_rate` 变量值为 46。最后，该值乘以 10 并显示输出结果。

![](img/655987774ce63b710f1a1b263f2c84e0_470_0.png)

在理解了 `#ifdef` 指令的实现后，现在让我们讨论 `#ifndef` 指令。

#### `#ifndef` 指令

与 `#ifdef` 指令类似，`#ifndef` 指令也验证宏是否已定义。然而，`#ifndef` 指令验证的是与 `#ifdef` 指令验证的相反条件。换句话说，如果宏未定义，则 `#ifndef` 指令认为该条件为真，并执行 `#ifndef` 条件后的代码语句。让我们考虑列表 7 并 `#ifdef` 指令替换为 `#ifndef` 指令。列表 8 显示了 `#ifndef` 指令的使用：

#### 列表 8：`#ifndef` 指令的使用

```c
#include <stdio.h>
#include <file.h>
#ifndef USD
#define currency_rate 46
#endif
#ifndef UKP
#define currency_rate 100
#endif
main() {
  int rs;
  clrscr();
  rs = 10 * currency_rate;
  printf("%d\n", rs);
  getch();
}
```

```
输出:
1000
```

在列表 8 中，`USD` 在 file1 头文件中被定义，因此条件返回为假。所以，检查 `#ifndef` 指令指定的下一个条件，由于 `UKP` 未被定义，该条件返回为真。因此，`currency_rate` 被定义为值 10，然后该值被乘以 100。输出显示为 1000。

在理解了 `#ifndef` 指令的实现后，现在让我们讨论 `#if` 指令。

#### `#if` 指令

`#if` 指令允许你通过关系运算符（如 `&&` 或 `||`）定义更具通用的条件。如果指定的条件为真，则执行后续的代码语句。列表 9 显示了 `#if` 指令的使用：

```c
#include <stdio.h>
#include <file.h>
#if (1>0) && defined(USD)
#define currency_rate 46
#endif
#if (defined(UKP))
#define currency_rate 100
#endif
main() {
  int rs;
  clrscr();
  rs = 10 * currency_rate;
  printf("%d\n", rs);
  getch();
}
```

```
输出:
460
```

在列表 9 中，`(1>0)` 和 `defined(USD)` 条件为真，因此 `currency_rate` 被定义为 46。然后该值乘以 10，并显示 460。

在理解了 `#if` 指令的实现后，现在让我们讨论 `#ifelse` 指令。

#### `#ifelse` 指令

`#ifelse` 指令用于在条件为真或假时提供相应的操作。如果条件为真，则执行 `#ifelse` 指令中的代码语句。如果条件为假，则执行 `#else` 结构中的代码语句。列表 10 显示了 `#ifelse` 指令的使用：

#### 列表 10：`#ifelse` 指令的使用

```c
#include <stdio.h>
#include <file.h>
#if (USD)
#define currency_rate 46
#else
#define currency_rate 100
#endif
void main() {
  int rs;
  clrscr();
  rs = 10 * currency_rate;
  printf("%d\n", rs);
  getch();
}
```

```
输出:
460
```

在列表 10 中，`defined(USD)` 条件提供在 `#if` 指令之后。如果条件为真，则执行 `#if` 结构中的语句；否则，执行 `#else` 结构。条件结果为真，因此 `currency_rate` 被定义为 46。此外，该值乘以 10 并显示 460 作为输出。

在理解了 `#ifelse` 指令的实现后，现在让我们讨论 `#ifelif` 指令。

#### `#ifelif` 指令

`#ifelif` 指令允许你在存在多个条件时定义操作。`#ifelif` 指令类似于 `#else` 指令，但它跟在 `#if` 之后。你必须注意 `#ifelif` 指令用于多个条件。你可以编写一个使用 `#ifelif` 指令的程序如列表 11 所示：

#### 列表 11：`#ifelif` 指令的使用

```c
#include <stdio.h>
#include <file.h>
#if defined(USD)
    #define currency_rate 46
#elif defined(UKP)
    #define currency_rate 100
else
    #define currency_rate 1
#endif
main() {
    int rs;
    clrscr();
    rs = 10 * currency_rate;
    printf("%d\n", rs);
    getch();
}
```

```
输出:
460
```

在列表 11 中，如果 `USD` 已定义，则汇率为 46；如果 `UKP` 已定义，则汇率为 100；否则汇率为 1。

这结束了对编译器控制指令的讨论。

## 总结

本章探索了三种预处理器指令，即文件包含、宏替换和编译器控制指令。在文件包含部分，你学习了如何使用 `#include` 指令包含标准库或用户开发的头文件。在宏替换部分，你学习了 `#define` 和 `#undef` 指令，它们可以在不同情况下定义或取消宏。在编译器控制指令部分，你学习了 `#ifdef`, `#ifndef`, `#if`, `#ifelse` 和 `#ifelif` 指令，它们允许你根据特定条件条件地包含头文件或定义宏。在本章结束时，你已经能够创建演示这些指令的程序。

## 快速复习
