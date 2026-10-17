
```cpp
// 在调用环境中处理抛出的异常。

#include <iostream>
#include <string>

using namespace std;

class myException
{
public:
    myException() : message("Something is wrong") {}
    myException(string str) : message(str) {}
    void what()
    {
        cout << message << endl;
    }
private:
    string message;
};

void func()
{
    int number;
    bool done = false;
    try
    {
        cout << "Line 8: Enter an integer: ";
        cin >> number;
        if (!cin)
        {
            throw myException("The input stream is in the fail state.");
        }
        cout << "Line 14: Number = " << number << endl;
        done = true;
    }
    catch (myException e)
    {
        cout << "Line 18: ";
        e.what();
        cout << "Line 19: Restoring the input stream." << endl;
        cin.clear();
        cin.ignore(100, '\n');
    }
    while (!done);
}

int main()
{
    try
    {
        func();
    }
    catch (myException e)
    {
        e.what();
    }
    return 0;
}
```

# 快速回顾

1. 异常是执行过程中可以检测到的不良情况。

2. 处理异常的一些典型方法是 `if` 语句或 `assert` 函数。

3. `assert` 函数可以检查表达式是否满足条件。如果不满足条件，它将终止程序。

4. `try`/`catch` 块用于处理异常。

5. 可能产生异常的语句放在 `try` 块中。如果发生异常，该块中的语句将不再执行。

6. `try` 块后面跟着一个或多个 `catch` 块。

7. `catch` 块指定它可以捕获的异常类型，并包含处理程序。

8. 如果 `catch` 块的头部包含省略号 `...`，则该 `catch` 块可以捕获所有类型的异常。

9. 如果 `try` 块中没有抛出异常，则与该 `try` 块关联的所有 `catch` 块都将被忽略，并从 `catch` 块之后继续执行。

10. 如果 `try` 块中抛出了异常，程序将按照 `try` 之后出现的顺序搜索 `catch` 块，寻找适当的异常程序。如果异常类型与某个 `catch` 块的类型匹配，则执行该 `catch` 块中的代码，后续 `catch` 块将不再忽略。

11. `catch` 块的数据类型指定了 `catch` 块可以捕获的异常类型。

12. `catch` 块最多有一个 `catch` 参数。

13. 如果在 `catch` 块头部仅指定了数据类型，即没有 `catch` 参数，那么抛出的值在 `catch` 块异常处理代码中无法访问。

14. 为了让异常在 `try` 块中发生被 `catch` 块捕获，必须在 `try` 块中抛出异常。

15. 抛出异常的通用语法是 `throw expression`；其中 `expression` 是常量值、变量或对象。被抛出的对象可以是特定对象也可以是匿名对象。

16. C++ 通过类层次结构提供了处理异常的支持。

17. `exception` 类是 C++ 提供的所有异常类的基类。

18. `what` 函数返回一个包含 C++ 内置异常类抛出的异常对象的字符串。

19. `exception` 类包含在 `exception.h` 头文件中。

20. 直接派自 `exception` 类的两个类是 `logic_error` 和 `runtime_error`。这两个类都定义在 `stdexception.h` 头文件中。

21. `invalid_argument` 类设计用于处理函数调用中使用的非法参数。

22. `out_of_range` 类处理 `out_of_range` 字符串错误。

23. 如果使用的长度超过字符串对象允许的最大长度，`length_error` 类负责处理操作对象长度超过最大允许大小时发生的错误。

24. 如果 `operator new` 无法分配内存空间，该运算符将抛出 `bad_alloc` 异常。

25. `runtime_error` 类用于处理只有在程序运行时才能检测到的错误。例如，对于算术溢和下溢异常，`overflow_error` 和 `underflow_error` 类派自 `runtime_error`。

26. `catch` 块通常处理异常，或部分处理异常后重新抛出相同的异常或抛出另一个异常，以便调用环境处理该异常。

27. C++ 允许程序员创建自己的异常类，以处理 C++ 异常类未涵盖的异常以及自定义的异常。

28. C++ 处理你定义的异常使用的机制与处理内置异常相同。但是，你必须使用 `throw` 语句来抛出你自己的异常。

29. 在 C++ 中，任何类都可以被视为异常类。它不需要继承自 `exception` 类。一个类是否成为异常取决于它是如何被使用的。

30. 重新抛出由 `catch` 块捕获的异常的通用语法是：

`throw;` （在这种情况下，重新抛出相同的异常）或：

`throw expression;` （其中 `expression` 是常量值、变量或对象）。被抛出的对象可以是特定对象，也可以是匿名对象。

31. 函数在它的头部使用 `throw` 子句来指定它所抛出的异常。

32. 当函数中抛出异常时，函数可以执行以下操作：什么都不做；部分处理异常并抛出相同的情况或新异常；或 `throw` 一个新异常。在这些情况下，函数调用栈都会被展开（unwound），以便异常能在 `try`/`catch` 块中被捕获。栈展开会一直持续，直到 `try`/`catch` 处理该异常或程序不再处理该异常。

33. 如果程序没有处理异常，则调用 `terminate` 函数来终止程序。

# 练习题

1. 判断以下陈述的对错。

   a. `catch` 块的列出顺序并不重要。

   b. 异常可以在发生它的函数中捕获，也可以在导致调用此方法的任何一个函数中捕获。

   c. 处理异常的一种方法是打印错误信息并退出程序。

   d. 所有异常都需要报告以避免编译错误。

2. `try` 块和 `catch` 块之间的区别是什么？

3. 如果抛出了异常但没有被捕获，会发生什么？

4. 如果 `try` 块中没有抛出异常，会发生什么？

5. 如果 `try` 块中抛出了异常，会发生什么？

6. 考虑以下 C++ 代码：

```cpp
double balance;
{
    cout << "Enter the balance: ";
    cin >> balance;
    cout << endl;

    if (balance < 1000.00)
        throw balance;

    cout << "Leaving the try block." << endl;
}
catch (double x) {
    cout << "Current balance: " << x << endl;
    cout << "Balance must be greater than 1000.00" << endl;
}
```

   a. 在这段代码中，识别 `try` 块。

   b. 在这段代码中，识别 `catch` 块。

   c. 在这段代码中，识别 `catch` 块的参数及其类型。

   d. 在这段代码中，识别 `throw` 语句。

7. 假设练习 6 给出的代码：

   a. 如果输入是 1200，输出是什么？

   b. 如果输入是 975，输出是什么？

   c. 如果输入是 -2000，输出是什么？

8. 考虑以下 C++ 代码：

```cpp
int lowerLimit;
try {
    cout << "Entering the try block." << endl;
    if (lowerLimit < 100)
        throw exception("Lower limit violation.");
    cout << "Exiting the try block." << endl;
} catch (exception eObj) {
    cout << "Exception: " << eObj.what() << endl;
}
cout << "After the catch block" << endl;
```

如果满足以下条件，输出是什么：

   a. `lowerLimit` 的值为 50？

   b. `lowerLimit` 的值为 150？

9. 考虑以下 C++ 代码：

```cpp
class myException {
public:
    myException() {
        message = "myException thrown!";
        cout << "Immediate attention required!" << endl;
    }
    myException(string msg) {
        message = msg;
        cout << "Attention required!" << endl;
    }
    string what () {
        return message;
    }
private:
    string message;
};
```

假设在用户程序中，`catch` 块如下：

```cpp
catch (myException mE)
cout << mE.what() << endl;
```

如果使用默认构造函数抛出异常，输出是什么？

如果使用带参数的构造函数抛出异常，输出是什么？

10. 如果你定义了自己的异常类，其中通常包含什么内容？

11. 使用什么类型的语句来抛出异常？

12. 定义一个异常类 `tornadoException`。该类应该有两个构造函数，包括默认构造函数。如果使用默认构造函数抛出异常，方法应返回“Tornado: Take cover immediately!"。另一个构造函数有一个 `int` 类型的参数 `m`。如果使用该构造函数抛出异常，方法应返回“Tornado: m miles away; approaching!"。

13. 编写一个 C++ 程序测试第 12 题指定的 `tornadoException` 类。

14. 假设异常类 `myException` 定义如下：

```cpp
class myException {
public:
    myException() {
        message = "myException thrown!";
        cout << "Immediate attention required!" << endl;
    }
    myException(string msg) {
        message = msg;
        cout << "Attention required!" << endl;
    }
    string what () {
        return message;
    }
private:
    string message;
};
```

假设在程序中，`catch` 块如下：

```cpp
catch (myException mE)
cout << mE.what() << endl;
```

如果使用默认构造函数抛出该异常，会产生什么输出？

15. 列举三种异常处理技术。

# 编程题

1. 编写一个程序，提示用户输入以英尺为单位的长度并输出相应的厘米长度。如果用户输入负数或非数字，抛出并处理适当的异常，并提示用户输入另一组数字。

2. 重做第 8 章的编程题 7，使你的程序处理除以零和无效输入等异常。

3. 编写一个程序，提示用户输入 12 小时制的时间。程序以 24 小时制输出时间。你的程序必须包含异常类：`invalidHr`、`invalidMin` 和 `invalidSec`。如果用户输入无效小时，程序应抛出并捕获 `invalidHr` 对象。对于分钟和秒的无效值也是类似。

4. 编写一个程序，提示用户输入数字格式（如 8-27-1980）的出生日期。程序以“August 27, 1980”的格式输出日期。你的程序必须至少包含两个异常类：`invalidDay` 和 `invalidMonth`。如果用户输入无效日期，程序应抛出并捕获 `invalidDay` 对象。对于月份和年份的无效值也是类似。（注意：你的程序必须处理闰年）。

# 第 17 章 递归

在本章中，你将：

- 学习递归定义

- 探索递归定义的边界情况和一般情况

- 发现什么是递归算法

- 学习递归函数

- 探索如何使用递归函数来实现递归算法

在之前的章节中，为了给问题设计解决方案，我们使用了最常用的技术，即迭代。然而，对于某些问题，使用迭代技术来解决方案会非常复杂。本章介绍了另一种称为递归的问题解决技术，并提供了几个示例来演示递归的工作原理。

## 递归定义

通过将问题还原为自身的更小版本来解决问题的过程被称为递归。递归是一种解决问题的非常强大的方法，如果不使用递归，这些问题的解决方案将非常复杂。让我们考虑一个大多数人都熟悉的问题。

在数学中，非负整数的阶乘定义如下：

```
0! = 1 (17-1)
n! = n × (n - 1)! if n > 0  (17-2)
```

在这个定义中，`0!` 被定义为 1；如果 `n` 是大于 0 的整数，我们首先找到 `(n - 1)`，然后将其乘以 `n`。为了找到 `(n - 1)`，我们再次应用定义。如果 `(n - 1) > 0`，则我们使用方程 17-2；否则，我们使用方程 17-1。因此，对于大于 0 的整数，`n!` 是通过找到 `(n - 1)`（即 `n!` 被还原为自身的更小版本）并将 `(n - 1)` 乘以 `n` 得到的。

让我们应用这个定义来找到 `3!` 这里，`n = 3`。因为 `n > 0`，我们使用方程 17-2 得到：

```
3! = 3 × 2
```

接下来，我们找到 `2!` 这里，`n = 2`。因为 `n > 0`，我们使用方程 17-2 得到：

```
2! = 2 × 1
```

现在，为了找到 `1!`，我们再次使用方程 17-2，因为 `n = 1 > 0`。

```
1! = 1 × 0
```

最后，我们使用方程 17-1 找到 `0!`，其结果为 1。将 `0!` 代入 `1!` 得到 `1! = 1`。这得到了 `2! = 2 × 1! = 2 × 1 = 2`，进而得到 `3! = 3 × 2! = 3 × 2 = 6`。

方程 17-1 中的解是直接的——也就是说，方程右侧不包含阶乘符号。方程 17-2 中的解是以其更小版本的形式给出的。方程 17-1 和 17-2 中的阶乘定义被称为递归定义。方程 17-1 是边界情况（即可以直接获得解的情况）；方程 17-2 被称为一般情况。

**递归定义：** 一种根据其自身的更小版本来定义某物的定义。

从之前的示例（阶乘）中可以清楚地看出：

1. 每一个递归定义必须有一个（或多个）边界情况。

2. 一般情况必须最终还原为边界情况。

3. 边界情况会停止递归。

计算机科学中的递归概念原理类似。在这里，我们谈论递归算法和递归函数。一种通过将问题还原为自身的更小版本来找到给定问题解决方案的算法被称为**递归算法**。递归算法必须有一个或多个边界情况，且通用解必须最终还原为边界情况。

调用 way自身的函数被称为**递归函数**。也就是说，递归函数的体包含一条语句，该语句在完成当前调用之前导致同一个函数再次执行。递归算法是通过递归函数实现的。

接下来，让我们编写实现阶乘函数的递归函数：

```cpp
int fact(int num)
{
    if (num == 0)
        return 1;
    else
        return num * fact(num - 1);
}
```

图 17-1 追踪了后续语句的执行过程：

```cpp
cout << fact(4) << endl;
```

![](img/abc25bb507ebb3eb05460d88ce0e0fde_1034_0.png)

图 17-1 `fact(4)` 的执行

之前的 `cout` 语句的输出：

24

在图 17-1 中，向下箭头表示对函数 `fact` 的连续调用，向上箭头表示返回给调用者的值，即调用函数。

让我们从前面的涉及阶乘函数的示例中注意以下几点。

- 从逻辑上讲，你可以认为递归函数拥有无限数量的自身副本。

- 每次对递归函数的调用——即每次递归调用——都有自己的代码和自己的参数集。

在完成特定的递归调用后，控制权返回到调用环境。当前的（递归）调用必须完全执行。

## 直接递归与间接递归

如果一个函数调用自身，它是直接递归的。例如，如果函数 A 调用函数 B，B 调用 A，那么 A 是间接递归的。例如，假设函数 A 调用 B，B 调用 C，C 调用 A，那么 A 是间接递归的。间接递归需要与直接递归相同的关注。必须识别边界情况并提供解决方案。

## 无限递归
