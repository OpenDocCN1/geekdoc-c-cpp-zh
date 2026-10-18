

这种替代形式仅适用于函数声明。*函数头必须始终列出形式参数名称。*

## PITFALL 参数顺序错误

当调用一个函数时，计算机用第一个参数替换第一个形式参数，用第二个参数替换第二个形式参数，依此类推。它不会检查合理性。如果你弄混了函数调用中参数的顺序，程序将不会按你期望的方式运行。为了了解可能出现什么问题，请考虑第 4.5 节中的程序。编写该程序的程序员在调用函数 `grade` 时粗心地颠倒了参数的顺序。函数调用应该是

```
letterGrade = grade(score, needToPass);
```

这是程序中唯一的错误。然而，由于这次粗心的错误，某个可怜的学生被错误地判定为课程不及格。函数 `grade` 很简单，你可能会期望程序员在测试程序时发现这个错误。然而，如果 `grade` 是一个更复杂的函数，这个错误很容易被忽视。

如果参数的类型与形式参数不匹配，编译器可能会给你一个警告信息。不幸的是，并非所有编译器都会给出此类警告信息。此外，在像下面这样的情况下

```cpp
//Determines user's grade. Grades are Pass or Fail.
#include <iostream>
using namespace std;

char grade(int receivedPar, int minScorePar);
//Returns 'P' for passing, if receivedPar is
//minScorePar or higher. Otherwise returns 'F' for failing.

int main( )
{
    int score, needToPass;
    char letterGrade;

    cout << "Enter your score"
         << " and the minimum needed to pass:\n";
    cin >> score >> needToPass;

    letterGrade = grade(needToPass, score);
```

函数定义中的声明和可执行语句与程序的主体部分相同。然而，除非你有理由这样做，否则最好先放置声明，如第 4.6 节所示。

由于函数在执行 `return` 语句之前不会返回值，因此函数必须在函数体中包含一个或多个 `return` 语句。函数定义可能包含多个 `return` 语句。例如，代码体中可能包含一个 `if-else` 语句，而 `if-else` 语句的每个分支可能包含不同的 `return` 语句，如第 4.5 节所示。

编译器会接受函数定义中任何合理的空格和换行符模式。然而，你应该对函数定义的缩进和布局使用与程序主体部分相同的规则。特别注意我们在函数定义中以及第 4.6 节中大括号 `{}` 的放置。标记函数体结束的开始和结束大括号各自单独占一行。这将函数体隔离开来。

空格和换行符

## 更多关于函数定义放置的内容

我们已经讨论了函数定义和函数声明通常放置的位置。在正常情况下，这些是函数声明和函数定义的最佳位置。然而，编译器会接受函数定义和函数声明

## DISPLAY 4.6 返回值的函数语法

```
Function Declaration

Type_Returned Function_Name(Parameter_List);
Function_Declaration_Comment

Function Definition

Type_Returned Function_Name(Parameter_List) ← function header
{
    Declaration_1
    Declaration_2
    ...
    Declaration_Last
    Executable_Statement_1
    Executable_Statement_2
    ...
    Executable_Statement_Last
}
body
Must include one or more return statements.
```

在某些其他位置。更精确的规则陈述如下：每个函数调用必须在其前面有该函数的函数声明或函数的定义。例如，如果你将所有函数定义放在程序主体之前，则无需包含任何函数声明。了解这一更一般的规则将有助于你理解在某些其他书籍中看到的 C++ 程序，但你应该遵循本书中程序的示例。我们使用的风格为学习如何构建你自己的函数库奠定了基础，而这正是大多数 C++ 程序员使用的风格。

## PROGRAMMING TIP 在分支语句中使用函数调用

`switch` 语句和多路 `if-else` 语句允许你在每个分支中放置多个不同的语句。然而，这样做会使 `switch` 语句或 `if-else` 语句难以阅读。查看第 3.7 节中的 `switch` 语句。选择 1、2 和 3 的每个分支都可以是一个单一的函数调用。这使得 `switch` 语句的布局和程序的整体结构清晰。如果我们将每个分支的代码放在 `switch` 语句中，而不是放在函数定义中，那么 `switch` 语句将成为不可理解的 C++ 语句的海洋。事实上，`switch` 语句甚至无法在一屏中显示。

## SELF-TEST EXERCISES

5. 以下程序产生的输出是什么？

```
#include <iostream>
using namespace std;
char mystery(int firstPar, int secondPar);
int main()
{
    cout << mystery(10, 9) << "ow\n";
    return 0;
}
char mystery(int firstPar, int secondPar)
{
    if (firstPar >= secondPar)
        return 'W';
    else
        return 'H';
}
```

- 6. 编写一个函数声明和函数定义，该函数接受三个参数，均为 `int` 类型，并返回其三个参数的总和。
- 7. 编写一个函数声明和函数定义，该函数接受一个 `int` 类型参数和一个 `double` 类型参数，并返回一个 `double` 类型的值，该值是两个参数的平均值。
- 8. 编写一个函数声明和函数定义，该函数接受一个 `double` 类型参数。函数如果其参数为正则返回字符值 `'P'`，如果其参数为零或负则返回 `'N'`。
- 9. 仔细描述传值参数机制。
- 10. 列出使用预定义（即库）函数和使用用户定义函数之间的相似之处和不同之处。
- 11. 编写一个名为 `inOrder` 的函数定义，该函数接受三个 `int` 类型参数。函数如果三个参数按升序排列则返回 `true`；否则返回 `false`。例如，`inOrder(1, 2, 3)` 和 `inOrder(1, 2, 2)` 都返回 `true`，而 `inOrder(1, 3, 2)` 返回 `false`。
- 12. 编写一个名为 `even` 的函数定义，该函数接受一个 `int` 类型参数并返回一个 `bool` 值。函数如果其一个参数为偶数则返回 `true`；否则返回 `false`。
- 13. 编写一个函数定义 `isDigit`，该函数接受一个 `char` 类型参数并返回一个 `bool` 值。函数如果参数是十进制数字则返回 `true`；否则返回 `false`。
- 14. 编写一个函数定义 `isRootOf`，该函数接受两个 `int` 类型参数并返回一个 `bool` 值。函数如果第一个参数是第二个参数的平方根则返回 `true`；否则返回 `false`。

## 4.4 程序抽象

> > 原因被隐藏，但结果是众所周知的。
> >
> > —OVID, *Metamorphoses IV*

## 黑盒类比

使用程序的人不需要知道程序是如何编码的。想象一下，如果你必须知道并记住你使用的编译器的代码，你的生活会多么痛苦。一个程序有其要完成的工作，例如编译你的程序或检查论文中的单词拼写。你需要知道程序的**工作**是什么，以便使用程序，但你不需要（或至少不应该）知道程序*如何*完成其工作。函数就像一个小型程序，应该以类似的方式使用。使用程序中函数的程序员需要知道*函数做什么*（例如计算平方根或将温度从华氏度转换为摄氏度），但不需要知道函数*如何*完成其任务。这通常被称为将函数视为*黑盒*。

称某物为**黑盒**是一种比喻，旨在传达一个物理设备的形象，你知道如何使用它，但其操作方法是个谜，因为它被封闭在一个黑盒子里，你看不到盒子内部（也不能撬开它！）。如果一个函数设计良好，程序员就可以像使用黑盒一样使用该函数。程序员需要知道的全部是，如果他或她将适当的参数放入黑盒中，那么适当的值将从黑盒中返回。设计函数使其可以作为黑盒使用，有时被称为**信息隐藏**，以强调程序员的行为就像函数体对他是隐藏的一样。

第 4.7 节包含函数 `newBalance` 的函数声明和两个不同的定义。正如函数声明注释所解释的，函数 `newBalance` 计算在加入简单利息后银行账户中的新余额。例如，如果一个账户开始时有 $100，并且 4.5% 的利息记入账户，则新余额为 $104.50。因此，以下代码将把 `vacationFund` 的值从 100.00 更改为 104.50：

```
vacationFund = 100.00;
vacationFund = newBalance(vacationFund, 4.5);
```

程序员使用第 4.7 节中所示的 `newBalance` 的两个实现中的哪一个并不重要。这两个定义产生返回完全相同值的函数。我们可以同样在函数定义的函数体上放置一个黑盒，以便程序员不知道使用的是哪个实现。为了使用函数 `newBalance`，程序员需要阅读的全部是函数声明和随附的注释。

以黑盒的方式编写和使用函数也称为**程序抽象**。在 C++ 编程中，更合适地称之为*函数抽象*。然而，*过程*是一个比*函数*更一般的术语。计算机科学家使用术语*过程*来指代所有“类似函数”的指令集，因此他们使用术语*程序抽象*。术语*抽象*旨在传达这样一个思想：当你将函数用作黑盒时，你抽象掉了函数体中包含的代码细节。你可以将这种技术称为*黑盒原则*或*原则*

