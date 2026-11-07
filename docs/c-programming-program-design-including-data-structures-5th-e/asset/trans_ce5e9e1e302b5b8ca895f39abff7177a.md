

## 记录错误并继续

当异常发生时程序终止，这种程序通常认为终止是相当安全的。然而，如果你的程序是为运行核反应堆或持续监控卫星而设计的，那么它不能在发生异常时终止。这类程序应报告异常，但程序必须继续运行。

例如，考虑一个分析航空公司票务交易的程序。由于每天都会发生大量票务交易，每天结束时都会运行一个程序来验证当天的交易。这类程序处理这些交易需要耗费大量时间，并使用异常来识别任何错误条目。相反，当异常发生时，程序应将异常写入文件，并继续分析交易。

## 栈展开

本章给出的示例展示了如何捕获和处理异常。特别是，你学习了如何在同一个块中捕获和处理异常，以及如何在调用环境中处理已捕获的异常。

当在（比如）函数中抛出异常时，该函数可以执行以下操作：

- 不做任何事。
- 部分处理异常，并抛出同一异常或新异常。
- 抛出新异常。

在每种情况下，函数调用栈都会展开，以便异常能在下一个 try/catch 块中被捕获。当函数调用栈展开时，未捕获和/或重新抛出异常的函数会终止，其局部变量的内存会被销毁。栈展开会一直继续，直到某个 try/catch 处理该异常，或者程序不处理该异常。如果程序不处理该异常，则会调用函数 `terminate` 来终止程序。

示例 15-17 和 15-18 说明了异常是如何传播的。为此，让我们定义以下异常类：

```cpp
// User-defined myException class.

#include <string>

using namespace std;

class myException
{
public:
    myException()
    {
        message = "Something is wrong!";
    }

    myException(string str)
    {
        message = str;
    }

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
> 在类 `myException` 的定义中，构造函数也可以写成如下形式：
>
> ```cpp
> myException() : message("Something is wrong!") {}
> myException(string str) : message(str) {}
> ```

示例 15-17 中的程序说明了在函数中抛出的异常如何在调用环境中被处理。

### 示例 15-17

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

void functionB() throw (myException)
{
    functionC();
}

void functionC() throw (myException)
{
    throw myException("Exception generated in function C.");
}
```

**示例运行：**

在 functionC 中生成异常。在 main 中捕获。

在这个程序中，函数 main 调用 functionA，functionA 调用 functionB，functionB 调用 functionC。函数 functionC 创建并抛出一个 myException 类型的异常。函数 functionA 和 functionB 不处理 functionC 抛出的异常。

函数 main 在 try 块中调用 functionA，并捕获 functionC 抛出的异常。catch 块头部中的参数 me 捕获异常的值，然后使用函数 what 返回存储在该对象中的字符串。catch 块中的输出语句输出相应消息。

示例 15-18 中的程序与示例 15-17 中的程序类似。这里，异常由直接调用环境捕获并处理。

### 示例 15-18

```cpp
// Processing exceptions, thrown by a function, in the
// immediate calling environment.

#include <iostream>
#include "myException.h"

using namespace std;

void functionA();
void functionB();
void functionC() throw (myException);

int main()
{
    try
    {
        functionA();
    }
    catch (myException e)
    {
        cout << e.what() << " Caught in main." << endl;
    }

    return 0;
}

void functionA()
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
    throw myException("Exception generated in functionC.");
}
```

**示例运行：**

在 functionC 中生成异常。在 functionB 中捕获。

在这个程序中，异常由 functionB 捕获并处理。尽管函数 main 包含 try/catch 块，但 try 块不会抛出任何异常，因为 functionC 抛出的异常已由 functionB 捕获并处理。

## 快速回顾

- 1. 异常是在程序执行期间可以检测到的不希望出现的情况的发生。
- 2. 处理异常的一些典型方法是使用 `if` 语句或 `assert` 函数。
- 3. 函数 `assert` 可以检查表达式是否满足所需条件。如果条件不满足，它会终止程序。
- 4. `try/catch` 块用于处理程序内的异常。
- 5. 可能生成异常的语句放在 `try` 块中。`try` 块还包含在发生异常时不应执行的语句。
- 6. `try` 块后面跟一个或多个 `catch` 块。
- 7. `catch` 块指定它可以捕获的异常类型，并包含异常处理程序。
- 8. 如果 `catch` 块的头部包含 `...`（省略号）来代替参数，那么这个 `catch` 块可以捕获所有类型的异常。
- 9. 如果 `try` 块中没有抛出异常，那么与该 `try` 块关联的所有 `catch` 块都会被忽略，程序执行会在最后一个 `catch` 块之后继续。
- 10. 如果 `try` 块中抛出异常，则 `try` 块中的其余语句会被忽略。程序会按 `try` 块之后 `catch` 块出现的顺序搜索这些 `catch` 块，寻找合适的异常处理程序。如果抛出的异常类型与某个 `catch` 块中的参数类型匹配，则执行该 `catch` 块中的代码，并且该 `catch` 块之后的其余 `catch` 块会被忽略。
- 11. `catch` 块参数的数据类型指定了该 `catch` 块可以捕获的异常类型。
- 12. 一个 `catch` 块最多可以有一个 `catch` 块参数。
- 13. 如果 `catch` 块头部只指定了数据类型，也就是说，如果没有 `catch` 块参数，那么在 `catch` 块的异常处理代码中可能无法访问抛出的值。
- 14. 要使异常在 `try` 块中发生并被 `catch` 块捕获，该异常必须在 `try` 块中抛出。
- 15. 抛出异常的一般语法是：

  ```cpp
  throw expression;
  ```

  其中 `expression` 是常量值、变量或对象。被抛出的对象可以是特定对象，也可以是匿名对象。
- 16. C++ 提供通过类层次结构处理异常的支持。
- 17. **exception 类**是 C++ 提供的异常类的基类。
- 18. 函数 `what` 返回一个字符串，其中包含 C++ 内置异常类所抛出的异常对象。
- 19. **exception 类**包含在头文件 `exception` 中。
- 20. 直接派生自 **exception 类**的两个类是 `logic_error` 和 `runtime_error`。这两个类都定义在头文件 `stdexcept` 中。
- 21. **invalid_argument 类**旨在处理函数调用中使用的非法参数。
- 22. **out_of_range 类**处理字符串下标 `out_of_range` 错误。
- 23. 如果为字符串对象使用了超过其允许最大长度的长度，则 **length_error 类**处理以下错误：所使用的长度大于被操作对象允许的最大大小。
- 24. 如果运算符 `new` 无法分配内存空间，该运算符会抛出 `bad_alloc` 异常。
- 25. **runtime_error 类**旨在处理只能在程序执行期间检测到的错误。例如，为了处理算术溢出和下溢异常，`overflow_error` 和 `underflow_error` 类派生自 **runtime_error 类**。
- 26. `catch` 块通常处理异常，或部分处理异常，然后重新抛出同一异常或重新抛出另一个异常，以便调用环境处理该异常。
- 27. C++ 使程序员能够创建自己的异常类，以处理 C++ 异常类未覆盖的异常以及自己的异常。
- 28. C++ 使用与处理内置异常相同的机制来处理你定义的异常。但是，你必须使用 `throw` 语句抛出自己的异常。
- 29. 在 C++ 中，任何类都可以被视为异常类。它不必继承自 **exception 类**。一个类之所以成为异常类，在于它如何被使用。
- 30. 重新抛出 `catch` 块捕获的异常的一般语法是：

  ```cpp
  throw;
  ```

  （在这种情况下，会重新抛出同一异常）或：

  ```cpp
  throw expression;
  ```

  其中 `expression` 是常量值、变量或对象。被抛出的对象可以是特定对象，也可以是匿名对象。

