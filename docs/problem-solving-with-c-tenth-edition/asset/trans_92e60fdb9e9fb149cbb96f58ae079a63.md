

以下是值的直方图：

```text
1:
2:
3: ***
4:
5:
6:
7: *
8:
9: *
10:
```

- 4. 定义一个名为 LinkedIntSet 的类。该类应像整数值的链表一样运行。然而，作为一个集合，集合中任何给定值的实例应只有一个。编写一个 addToSet 方法，如果该元素已先前添加到集合中，则抛出 ElementAlreadyExists 异常。编写一个简单的驱动程序来测试你的代码。

- 5. 栈在第 13 章和第 14 章中介绍。定义一个用于存储字符类型元素栈的栈类。栈对象应为固定大小；大小是创建栈对象的构造函数的参数。在程序中使用时，栈类对象将在以下情况下抛出异常：
  - 如果应用程序程序尝试向已满的栈上压入数据，则抛出 StackOverflowException
  - 如果应用程序程序尝试从空栈中弹出数据，则抛出 StackEmptyException

  定义 StackOverflowException 和 StackEmptyException 类是本项目的一部分。编写一个合适的测试程序。

- 6. 开发一个系统，用于将学生成绩输入到评分系统中。该系统应包含一个类，该类保存学生的姓名及其多项作业的成绩。在程序开始时，你应提示用户输入作业数量和每项作业的得分。然后你应提示用户输入每个学生的姓名和每项作业的成绩。你的程序应抛出多种不同的异常。
  - 如果作业数量小于 0，则应抛出异常。
  - 如果任何作业得分小于 0，则应抛出异常。
  - 如果作业得分的数量超过 100，则应抛出异常。
  - 如果为一名先前已输入到程序中的学生姓名输入成绩，则应抛出异常。
  - 如果输入的任何分数低于 0 或高于给定作业的最大分数，则应抛出异常。

- 7. 第 9 章中的编程项目 7 描述了一种技术，使用一维数组的包装函数来模拟二维数组。如果二维数组中所需条目的索引无效（例如超出范围），你被要求打印错误消息并退出程序。修改此程序（或首次实现）以便在行或列索引无效时抛出 ArrayOutOfRangeError 异常。你的程序应定义 ArrayOutOfRangeError 异常类。

![](img/88b1f375f11336dbd9dac8b1675d0698_961_0.png)

| Section | Page |
| --- | --- |
| **17.1 TEMPLATES FOR ALGORITHM ABSTRACTION** | 960 |
| Templates for Functions | 961 |
| *Pitfall:* Compiler Complications | 965 |
| Programming Example: A Generic Sorting Function | 967 |
| *Programming Tip:* How to Define Templates | 971 |
| *Pitfall:* Using a Template with an Inappropriate Type | 972 |
| **17.2 TEMPLATES FOR DATA ABSTRACTION** | 973 |
| Syntax for Class Templates | 973 |
| *Programming Example:* An Array Class | 976 |

![](img/88b1f375f11336dbd9dac8b1675d0698_962_0.png)

> All men are mortal.
> Aristotle is a man.
> Therefore, Aristotle is mortal.
>
> All X's are Y.
> Z is an X.
> Therefore, Z is Y.
>
> All cats are mischievous.
> Garfield is a cat.
> Therefore, Garfield is mischievous.

### A SHORT LESSON ON SYLLOGISMS

## INTRODUCTION

本章讨论 C++ 模板。模板允许你定义具有类型名参数的函数和类。这将使你能够设计可用于不同类型参数的函数，并定义比本章之前见过的更通用的类。

## PREREQUISITES

第 17.1 节使用第 2 章至第 5 章以及第 7 章的第 7.1、7.2 和 7.3 节的材料。它不使用任何关于类的材料。第 17.2 节使用第 2 章至第 7 章和第 10 章至第 12 章的材料。

## 17.1 TEMPLATES FOR ALGORITHM ABSTRACTION

我们之前许多 C++ 函数定义都有一个底层算法，该算法比我们在函数定义中给出的算法更通用。例如，考虑我们在第 5 章中首次讨论的函数 swapValues。参考起见，我们现在重复该函数定义：

```cpp
void swapValues(int& variable1, int& variable2)
{
    int temp;

    temp = variable1;
    variable1 = variable2;
    variable2 = temp;
}
```

请注意，函数 swapValues 仅适用于类型为 int 的变量。然而，函数体中给出的算法同样可以用来交换两个类型为 char 的变量中的值。如果我们还想用类型为 char 的变量使用函数 swapValues，我们可以通过添加以下定义来重载函数名：

```cpp
void swapValues(char& variable1, char& variable2)
{
    char temp;

    temp = variable1;
    variable1 = variable2;
    variable2 = temp;
}
```

但这两种 swapValues 函数定义存在低效且不令人满意之处：它们几乎相同。唯一的区别是一个定义在三个位置使用类型 int，另一个在相同三个位置使用类型 char。以这种方式继续，如果我们希望函数 swapValues 适用于类型为 double 的变量对，我们必须编写第三个几乎相同的函数定义。如果我们希望将 swapValues 应用于更多类型，几乎相同的函数定义数量会更大。这需要大量输入，并会使我们的代码充满大量看起来相同的定义。我们应该能够说以下函数定义适用于任何类型的变量：

```cpp
void swapValues(Type_Of_The_Variables& variable1,
    Type_Of_The_Variables& variable2)
{
    Type_Of_The_Variables temp;

    temp = variable1;
    variable1 = variable2;
    variable2 = temp;
}
```

正如我们将看到的，这样的情况是可能的。我们可以定义一个适用于所有类型变量的函数，尽管语法与上面所示有所不同。该语法在下一小节中描述。

### Templates for Functions

显示 17.1 显示了函数 swapValues 的 C++ 模板。此函数模板允许你交换任意两个变量的值，类型任意，只要两个变量具有相同类型。定义和函数声明以以下行开始

```cpp
template<class T>
```

这通常称为模板前缀，它告诉编译器随后的是一个模板定义或函数声明，并且 T 是一个类型参数。在此上下文中，单词 class 实际上意味着类型。¹ 正如我们将看到的，类型参数 T 可以被任何类型替换，无论该类型是否为类。在函数定义的主体中，类型参数 T 就像任何其他类型一样使用。

函数模板定义实际上是一组大的函数定义。对于显示 17.1 中所示的 swapValues 的函数模板，实际上为每种可能的类型名有一个函数定义。这些定义中的每一个都是通过将类型参数 T 替换为类型名得到的。例如，通过将 T 替换为类型名 double 得到以下函数定义：

```cpp
void swapValues(double& variable1, double& variable2)
{
    double temp;
    temp = variable1;
    variable1 = variable2;
    variable2 = temp;
}
```

### A template overloads the function name

通过将函数模板中的类型参数 T 替换为类型名 int 得到 swapValues 的另一个定义。通过将类型参数 T 替换为 char 得到另一个定义。显示 17.1 中所示的一个函数模板重载了函数名 swapValues，以便为每种可能的类型都有一个略有不同的函数定义。

编译器不会字面地为函数名 swapValues 的每种可能类型生成定义，但它会表现得好像已生成所有这些函数定义一样。每次使用模板的不同类型时都会生成单独的定义，但对于未使用的类型则不会。对于单个类型，无论使用模板的次数多少，只会生成一个定义。请注意，显示 17.1 中调用了两次函数 swapValues：一次参数类型为 int，另一次参数类型为 char。

考虑显示 17.1 中的以下函数调用：

```cpp
swapValues(integer1, integer2);
```

当 C++ 编译器处理到此函数调用时，它会注意到参数的类型——在此情况下为 int——然后它使用模板生成一个类型参数 T 被替换为类型名 int 的函数定义。类似地，当编译器看到函数调用

```cpp
swapValues(symbol1, symbol2);
```

> ¹ 事实上，ANSI 标准规定你可以在模板前缀中使用关键字 typename 而不是 class。虽然我们同意使用 typename 比使用 class 更有意义，但使用 class 已是根深蒂固的传统，因此为了与大多数其他程序员和作者保持一致，我们使用 class。

