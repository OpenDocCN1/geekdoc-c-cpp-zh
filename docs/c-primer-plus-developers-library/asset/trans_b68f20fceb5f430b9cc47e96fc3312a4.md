
本页有意留白

## 函数：C++ 的编程模块

本章你将学习以下内容：

-   函数基础
-   函数原型
-   按值传递函数参数
-   设计处理数组的函数
-   使用 const 指针参数
-   设计处理文本字符串的函数
-   设计处理结构的函数
-   设计处理 string 类对象的函数
-   调用自身的函数（递归）
-   函数指针

乐趣无处不在。仔细观察，你就能在函数中找到乐趣。C++ 自带一个包含大量有用函数的大型库（标准 ANSI C 库加上若干 C++ 类），但真正的编程乐趣来自编写自己的函数。（另一方面，真正的编程生产力可能来自进一步了解你能用 STL 和 BOOST C++ 库做什么。）本章和第 8 章“函数历险”将考察如何定义函数、如何向函数传递信息，以及如何从函数获取信息。在回顾函数如何工作之后，本章重点介绍如何将函数与数组、字符串和结构结合使用。最后，本章还会简要涉及递归和函数指针。如果你已经为 C 语言付出过努力，你会发现本章大部分内容都很熟悉。但不要被误导而产生虚假的精通感。C++ 对 C 函数能做的事情做了若干补充，第 8 章主要讨论这些补充。与此同时，让我们先关注基础知识。

### 函数回顾

让我们回顾一下你已经见过的关于函数的内容。要使用 C++ 函数，你必须做以下事情：

-   提供函数定义
-   提供函数原型
-   调用函数

如果你使用的是库函数，那么该函数已经为你定义并编译好了。此外，你可以而且应该使用标准库头文件来提供原型。剩下要做的只是正确地调用函数。本书到目前为止的示例已经多次这样做了。例如，标准 C 库包含用于查找字符串长度的 strlen() 函数。相关的标准头文件 cstring 包含 strlen() 以及其他几个字符串相关函数的函数原型。这项前期工作让你可以在程序中放心使用 strlen() 函数，而不必再担心其他问题。

但是，当你创建自己的函数时，你必须自己处理所有三个方面——定义、编写原型和调用。代码清单 7.1 用一个简短示例展示了这些步骤。

**代码清单 7.1** `calling.cpp`

```cpp
// calling.cpp -- defining, prototyping, and calling a function
#include <iostream>

void simple();    // function prototype

int main()
{
    using namespace std;
    cout << "main() will call the simple() function:\n";
    simple();     // function call
    cout << "main() is finished with the simple() function.\n";
    // cin.get();
    return 0;
}

// function definition
void simple()
{
    using namespace std;
    cout << "I'm but a simple function.\n";
}
```

下面是代码清单 7.1 中程序的输出：

```text
main() will call the simple() function:
I'm but a simple function.
main() is finished with the simple() function.
```

当控制权转移到 simple() 函数时，main() 中的程序执行会暂停。当 simple() 结束时，main() 中的程序执行会恢复。这个示例在每个函数定义内都放置了一条 using 指令，因为每个函数都使用了 cout。另一种做法是，程序可以在函数定义上方放置一条 using 指令，或者改用 std::cout。

现在让我们更详细地看看这些步骤。

### 定义函数

你可以把函数分为两类：没有返回值的函数和有返回值的函数。没有返回值的函数称为 void 类型函数，其一般形式如下：

```cpp
void functionName(parameterList)
{
    statement(s)
    return;          // optional
}
```

这里的 parameterList 指定传递给函数的参数（形参）的类型和数量。本章稍后会更全面地研究这个列表。可选的 return 语句标记函数的结束。否则，函数会在右花括号处终止。void 类型函数对应于 Pascal 过程、FORTRAN 子例程和现代 BASIC 子程序过程。通常，你使用 void 函数来执行某种操作。例如，一个按给定次数（n）打印 Cheers! 的函数可能如下所示：

```cpp
void cheers(int n)          // no return value
{
    for (int i = 0; i < n; i++)
        std::cout << "Cheers! ";
    std::cout << std::endl;
}
```

int n 参数列表意味着，当你调用 cheers() 时，它期望有一个 int 值作为实参传递给它。

有返回值的函数会产生一个值，并将其返回给调用它的函数。换句话说，如果函数返回 9.0 的平方根（sqrt(9.0)），那么函数调用的值就是 3.0。这样的函数被声明为与其返回值的类型相同。其一般形式如下：

```cpp
typeName functionName(parameterList)
{
    statements
    return value;    // value is type cast to type typeName
}
```

有返回值的函数要求你使用 return 语句，以便将值返回给调用函数。值本身可以是常量、变量或更一般的表达式。唯一的要求是，该表达式最终得到一个具有 `typeName` 类型或可转换为 `typeName` 类型的值。（如果声明的返回类型是，比如说，double，而函数返回一个 int 表达式，那么 int 值会被类型转换为 double 类型。）然后，函数将最终值返回给调用它的函数。C++ 确实对可以用作返回值的类型施加了一项限制：返回值不能是数组。其他一切都可以——整数、浮点数、指针，甚至结构和对象！（有趣的是，尽管 C++ 函数不能直接返回数组，但它可以返回作为结构或对象一部分的数组。）

作为程序员，你不需要知道函数如何返回值，但了解其方法可能会让你更清楚这个概念。（这也会给你提供一些与朋友和家人谈论的话题。）通常，函数通过将返回值复制到指定的 CPU 寄存器或内存位置来返回一个值。然后，调用程序检查该位置。返回函数和调用函数必须就该位置的数据类型达成一致。函数原型告诉调用程序应该期望什么，函数定义告诉被调用程序应该返回什么（见图 7.1）。在原型中提供与定义中相同的信息可能看起来像是额外工作，但这很有道理。当然，如果你想让快递员从你办公室的桌子上取走某样东西，那么如果你向快递员和办公室里的某个人都提供你想要的物品描述，就会提高任务正确完成的概率。

函数在执行 return 语句后终止。如果一个函数有多个 return 语句——例如，作为不同 `if else` 选择的替代分支——那么函数在执行到它遇到的第一个 return 语句后终止。例如，在下面的示例中，`else` 并不是必需的，但它确实有助于普通读者理解意图：

```cpp
int bigger(int a, int b)
{
    if (a > b )
        return a;    // if a > b, function terminates here
    else
        return b;    // otherwise, function terminates here
}
```

```c
double cube(double x);   // function prototype
int main()
{
    double q = cube(1.2);  // function call
    ...
}
double cube(double x)    // function definition
{
    return x * x * x;
}
```

![](img/9afc44517b591d64e2e19f623c9308ef_323_0.png)

图 7.1 典型的返回值机制。

（通常，函数中有多个 return 语句被认为可能造成混淆，一些编译器可能会发出警告。不过，这里的代码足够简单，容易理解。）

有返回值的函数与 Pascal、FORTRAN 和 BASIC 中的函数非常相似。它们向调用程序返回一个值，调用程序随后可以将该值赋给变量、显示该值，或以其他方式使用它。下面是一个返回 double 类型值立方的简单示例：

```c
double cube(double x)   // x times x times x
{
    return x * x * x;   // a type double value
}
```

例如，函数调用 cube(1.2) 返回 1.728。注意，这个 return 语句使用了一个表达式。函数计算该表达式的值（本例中为 1.728），并返回该值。

### 函数原型与函数调用

到现在为止，你已经熟悉了进行函数调用，但你可能对函数原型还不太适应，因为它通常隐藏在包含文件中。代码清单 7.2 展示了在程序中使用 cheers() 和 cube() 函数的情况；注意其中的函数原型。

