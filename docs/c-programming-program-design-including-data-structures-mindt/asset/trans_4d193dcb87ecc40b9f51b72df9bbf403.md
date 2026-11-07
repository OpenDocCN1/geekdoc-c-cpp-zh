
```cpp
string what()
{
    return message;
}

private:
    string message;
};
```

> **注意**
>
> 在 `class myException` 的定义中，构造函数也可以写成如下形式：
>
> ```cpp
> myException() : message("Something is wrong!") {}
> myException(string str) : message(str) {}
> ```

例14-18中的程序说明了函数中抛出的异常如何在调用环境中得到处理。

## 例14-18

```cpp
// Processing exceptions thrown by a function in the calling
// environment.

#include <iostream>
#include "myException.h"

using namespace std;

void functionA() throw (myException);
void functionB() throw (myException);
void functionC() throw (myException);

int main()
{
    try
    {
        functionA();
    }
    catch (myException me)
    {
        cout << me.what() << " Caught in main." << endl;
    }

    return 0;
}

void functionA() throw (myException)
{
    functionB();
}

void functionB()
{
    try
    {
        functionC();
    }
    catch (myException me)
    {
        cout << me.what() << " Caught in functionB." << endl;
    }
}

void functionC() throw (myException)
{
    throw myException("Exception generated in function C.");
}
```

## 示例运行

在 functionC 中生成的异常。在 functionB 中被捕获。

在这个程序中，异常由 functionB 捕获并处理。尽管 main 函数包含 try/catch 块，但 try 块不会抛出任何异常，因为 functionC 抛出的异常已由 functionB 捕获并处理。

## 快速复习

- 1. 异常是在程序执行期间可以检测到的不希望发生的情况。

- 2. 处理异常的一些典型方法是使用 if 语句或 assert 函数。

- 3. assert 函数可以检查表达式是否满足所需条件。如果不满足条件，它会终止程序。

- 4. try/catch 块用于处理程序中的异常。

- 5. 可能生成异常的语句放在 try 块中。try 块还包含在发生异常时不应执行的语句。

- 6. try 块后跟一个或多个 catch 块。

- 7. catch 块指定它可以捕获的异常类型，并包含异常处理程序。

- 8. 如果 `catch` 块的头部用 `. . .`（省略号）代替参数，那么这个 `catch` 块可以捕获所有类型的异常。

- 9. 如果 `try` 块中没有抛出异常，则与该 `try` 块关联的所有 `catch` 块都会被忽略，程序执行将在最后一个 `catch` 块之后继续。

- 10. 如果 `try` 块中抛出异常，则该 `try` 块中的其余语句将被忽略。程序按 `try` 块之后出现的顺序搜索 `catch` 块，寻找合适的异常处理程序。如果抛出的异常类型与某个 `catch` 块中的参数类型匹配，则执行该 `catch` 块中的代码，并忽略该 `catch` 块之后的其余 `catch` 块。

- 11. `catch` 块参数的数据类型指定该 `catch` 块可以捕获的异常类型。

- 12. 一个 `catch` 块最多只能有一个 `catch` 块参数。

- 13. 如果 `catch` 块头部只指定了数据类型，也就是说没有 `catch` 块参数，那么在 `catch` 块的异常处理代码中可能无法访问抛出的值。

- 14. 为了使异常在 `try` 块中发生并被 `catch` 块捕获，该异常必须在 `try` 块中抛出。

- 15. 抛出异常的一般语法是 `throw expression;`，其中 `expression` 是常量值、变量或对象。被抛出的对象可以是特定对象，也可以是匿名对象。

- 16. C++ 通过类的层次结构提供处理异常的支持。

- 17. `class exception` 是 C++ 提供的异常类的基类。

- 18. 函数 `what` 返回包含 C++ 内置异常类抛出的异常对象的字符串。

- 19. 类 `exception` 包含在头文件 `exception` 中。

- 20. 直接从类 `exception` 派生的两个类是 `logic_error` 和 `runtime_error`。这两个类都定义在头文件 `stdexcept` 中。

- 21. 类 `invalid_argument` 用于处理函数调用中使用的非法参数。

- 22. 类 `out_of_range` 处理字符串下标 `out_of_range` 错误。

- 23. 如果使用的长度大于字符串对象允许的最大长度，类 `length_error` 处理此错误。

- 24. 如果运算符 `new` 无法分配内存空间，该运算符会抛出 `bad_alloc` 异常。

- 25. 类 `runtime_error` 用于处理只能在程序执行期间检测到的错误。例如，为了处理算术上溢和下溢异常，类 `overflow_error` 和 `underflow_error` 派生自类 `runtime_error`。

- 26. `catch` 块通常处理异常或部分处理异常，然后重新抛出同一异常或重新抛出另一个异常，以便调用环境处理该异常。

- 27. C++ 使程序员能够创建自己的异常类，以处理 C++ 异常类未覆盖的异常以及自己的异常。

- 28. C++ 处理你定义的异常所用机制与处理内置异常相同。但是，你必须使用 `throw` 语句抛出自己的异常。

- 29. 在 C++ 中，任何类都可以被视为异常类。它不必继承自类 `exception`。使一个类成为异常类的是它的使用方式。

- 30. 重新抛出由 `catch` 块捕获的异常的一般语法是 `throw;`（在这种情况下，重新抛出同一异常）或 `throw expression;`，其中 `expression` 是常量值、变量或对象。被抛出的对象可以是特定对象，也可以是匿名对象。

- 31. 函数在其头部使用 `throw` 子句指定它抛出的异常。

- 32. 当函数中抛出异常时，函数可以执行以下操作：不做任何事；部分处理异常并抛出同一异常或新异常；或抛出新的异常。在每种情况下，函数调用栈都会展开，以便异常可以在下一个 `try/catch` 块中被捕获。栈展开会持续进行，直到某个 `try/catch` 处理该异常，或者程序不处理该异常。

- 33. 如果程序不处理该异常，则调用函数 `terminate` 来终止程序。

## 练习

练习末尾括号中的数字指本章开头列出的学习目标。

- 1. 判断以下陈述为真或假。
  - a. 除以零是一种异常，而打开不存在的输入文件不是异常。
  - b. 假设你使用 **assert** 函数检查是否满足某些条件。如果不满足条件，则 **assert** 函数会终止程序。(2)
  - c. 处理异常的一种方法是打印错误消息并退出程序。(2)
  - d. 所有异常都需要报告以避免编译错误。(2)
  - e. 每个 `try` 块必须有一个 `catch` 块。(3)
  - f. `catch` 块的列出顺序并不重要。(3)
  - g. 如果在 `try` 块中抛出异常，则在执行 `catch` 块之后，该 `try` 块中的其余语句会被执行。(3)
  - h. 在 C++ 中，异常是一个值。(3)
  - i. `class invalid_range` 处理字符串下标 `out_of_range` 错误。(5)
  - j. 在 C++ 中，一个类可以被视为异常类。(6)
  - k. 异常类必须至少包含一个成员。(6)
  - l. 异常可以在发生它的函数中被捕获，也可以在导致调用该方法的任何函数中被捕获。(7)
  - m. 当函数调用栈展开时，未捕获异常的函数会终止，但其局部变量的内存仍保持分配。(9)

- 2. 什么样的语句放在 `try` 块中？(3)

- 3. 如果抛出异常但未被捕获会发生什么？(3)

- 4. 如果 `try` 块中没有抛出异常会发生什么？(3)

- 5. 一个 `catch` 块可以有多少个参数？(3)

- 6. 哪个 `catch` 块捕获所有类型的异常？(3)

- 7. 如果在 `catch` 块头部只指定了数据类型，也就是说没有 `catch` 块参数，会发生什么？(3)

- 8. 使用哪种类型的语句抛出异常？(4)

- 9. throw 语句抛出哪种类型的对象？(4)

- 10. 以下代码有什么问题？同时提供正确的代码。(3, 4)

    ```cpp
    double balance = 25000;
    double intRate;

    catch (double x)
    {
        cout << "Negative interest rate: " << x << endl;
    }
    ```

