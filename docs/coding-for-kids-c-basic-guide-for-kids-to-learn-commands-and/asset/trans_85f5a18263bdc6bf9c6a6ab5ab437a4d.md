
double*，分别。

用于声明指针的星号（*）仅表示它是一个指针（它是其类型复合说明符的一部分）。不应将其与解引用运算符混淆，后者同样用星号（*）书写。它们只是由同一符号表示的两个不同事物。

## 实践代码

```cpp
// my first pointer
#include <iostream>
using namespace std;

int main ()
{
    int firstvalue, secondvalue;
    int* mypointer;

    mypointer = &firstvalue;
    *mypointer = 10;
    mypointer = &secondvalue;
    *mypointer = 20;
    cout << "firstvalue is " << firstvalue << '\n';
    cout << "secondvalue is " << secondvalue << '\n';
    return 0;
}
```

## 输出

firstvalue is 10  
secondvalue is 20

## 第6章：控制语句和循环

在编程语言中，控制语句用于控制程序的流程。它们只不过是程序中用于根据特定条件将控制权传递给另一条语句的一个术语或一组语句。控制语句会评估结果，并根据提供的条件执行必要的语句。

控制语句，也称为 if 语句、if-else 语句、break 语句、continue 语句、for 循环、while 循环和 do-while 循环，是控制程序流程以执行某段代码的语句。本章将讨论 C++ 语言中可用的一些重要控制语句。

### 6.1 语句与流程控制

简单的 C++ 语句是程序的单条指令，例如前面讨论的变量声明和表达式。语句总是以分号（;）结尾，并且按照它们在程序中出现的相同顺序运行。

另一方面，程序并不局限于按顺序执行的一组语句。程序在执行过程中可以重复某些代码部分，或做出决策并产生分支。C++ 为此包含流程控制语句，这些语句指定我们的程序必须做什么、何时做以及在什么条件下做。

本节讨论的许多流程控制语句都需要一个通用（子）语句。该语句可以是简单的 C++ 语句，也可以是复合语句，例如后跟分号（;）的单条指令。复合语句是一组语句（每条语句都以分号结尾），它们全部组合在一个块中，并包含在花括号中：{ }

整个块被视为单条语句（由多个子语句组成）。当通用语句出现在流程控制语句的语法中时，它可以是简单语句或复合语句。

### 6.2 选择语句：if 和 else

当且仅当满足条件时，使用 if 关键字执行一条语句或一个块。其语法如下：

`if (condition) statement`

在此情况下，被求值的表达式称为 condition。如果该条件为真，则执行语句。如果为假，则不会执行该语句（它将被忽略），程序将直接继续执行选择语句之后的代码。

例如，下面的代码段仅当变量 x 中存储的值为 200 时，才打印消息（x is 200）：

```cpp
if (x == 200)
cout<< "x is 200";
```

如果 x 不恰好等于 200，则忽略该语句，并且不打印任何内容。

如果希望在满足条件时执行不止一条语句，请将它们包裹在花括号（{}）中，形成一个块：

```cpp
if (x == 200)
{
cout<< "x is ";
cout<< x;
}
```

通过使用 else 关键字提供替代语句，带 if 的选择语句还可以定义条件不满足时发生的情况。其语法如下：

`if (condition) statement1 else statement2`

如果条件为真，则执行 statement1；如果条件为假，则执行 statement2。

为了验证一个值范围，可以将多个 if + else 结构串联起来。考虑以下情形：

```cpp
if (x > 0)
cout<< "x is positive";
else if (x < 0)
cout<< "x is negative";
else
cout<< "x is 0";
```

通过串联两个 if-else 结构，这会打印 x 是正数、负数还是零。同样，通过将语句组合成用花括号包围的块，本来可以针对每种情况执行不止一条语句。

#### switch 语句

switch 语句的语法有点奇怪。其目标是在一组可能的常量表达式中找到一个值。它类似于串联 if-else 语句，但仅适用于常量表达式。最常见的语法是：

```text
switch (expression)
{
    case constant1:
        group-of-statements-1;
        break;
    case constant2:
        group-of-statements-2;
        break;
    .
    .
    .
    default:
        default-group-of-statements
}
```

switch 会分析 expression，并检查它是否等于 constant1；如果相等，则执行 group-of-statements-1，直到遇到 break 语句。当程序看到这个 break 语句时，会跳转到 switch 语句的末尾（右花括号处）。

如果 expression 不等于 constant1，则将其与 constant2 比较。如果等于，则执行 group-of-statements-2，直到发现 break。

最后，如果 expression 的值与前面给出的任何常量都不匹配（常量的数量可以是任意的），程序将执行 default 后面的语句。

由于使用标签而不是块，switch 语句具有一种可追溯到 C 编译器早期时代的奇怪语法。在最常见的应用（见上文）中，特定标签的每组语句之后都需要 break 语句。如果没有指定 break，则 case 之后的所有语句（包括任何其他标签下的语句）同样会被执行，直到 switch 块结束或遇到跳转语句（例如 break）。

对于检查范围或非常量值，最好使用 if 和 if else 语句的串联。

### 6.3 迭代语句（循环）

循环会重复执行一条语句，直到满足某个条件或达到指定次数。关键字 while、do 和 for 用于引入它们。

#### while 循环

while 循环是最基本的循环类型。其语法如下：

```text
while (expression) statement
```

只要上面的 expression 为真，while 循环就会重复执行该语句。如果在某次语句执行后 expression 不再为真，循环终止，程序继续执行循环之后的代码。考虑以下 while 循环倒计时的示例：

```cpp
// custom countdown using while
#include <iostream>
using namespace std;

int main ()
{
    int n = 10;

    while (n>0) {
        cout << n << ", ";
        --n;
    }

    cout << "liftoff!\n";
}
```

在 main 中，第一条语句将 n 设置为 10。在倒计时中，这是第一个数字。然后 while 循环开始：如果该值满足条件 n>0（即 n 大于零），则执行条件之后的块，并且只要条件（n>0）为真，这个过程就会继续。

使用 while 循环时，请记住循环必须在某个时刻结束。因此，语句必须改变条件中检查的值，以迫使它在某个时刻变为假。否则，循环将无限循环下去。本示例中的循环包含 --n，它将条件中求值的变量（n）的值减一，使得在特定次数的循环迭代后条件（n>0）变为假。更准确地说，经过十次迭代后，n 等于 0，表明条件不再为真，while 循环终止。

#### do-while 循环

do-while 循环是一种在执行某件事的同时进行另一件事的循环。其语法如下：

```text
do statement while (condition);
```

它的行为类似于 while 循环，区别在于条件是在语句执行之后而不是执行之前求值。do-while 循环确保语句至少执行一次，即使条件从未满足。例如，下面的示例应用程序会重复用户输入的任何文本，直到用户说 goodbye：
