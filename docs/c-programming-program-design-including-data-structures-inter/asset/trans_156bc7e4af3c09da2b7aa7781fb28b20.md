
```cpp
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
    throw myException("Exception generated in functionC.");
}
```

### 示例运行：

Exception generated in functionC. Caught in main.

在此程序中，main函数调用functionA，functionA调用functionB，functionB调用functionC。functionC函数创建并抛出类型为myException的异常。functionA和functionB函数不处理functionC抛出的异常。

main函数在try块中调用functionA，并捕获functionC抛出的异常。catch块头中的参数me捕获该异常的值，然后使用函数what返回存储在该对象中的字符串。catch块中的输出语句输出相应的消息。

示例14-19中的程序与示例14-18中的程序类似。这里，异常由直接调用环境捕获和处理。

## 示例14-19

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

### 示例运行：

Exception generated in functionC. Caught in functionB.

在此程序中，异常由functionB捕获和处理。尽管main函数包含try/catch块，但try块不会抛出任何异常，因为functionC抛出的异常已被functionB捕获和处理。

- 17. 类`exception`是C++提供的异常类的基类。
- 18. 函数`what`返回包含C++内置异常类抛出的异常对象的字符串。
- 19. 类`exception`包含在头文件`exception`中。
- 20. 直接派生自类`exception`的两个类是`logic_error`和`runtime_error`。这两个类都定义在头文件`stdexcept`中。
- 21. 类`invalid_argument`旨在处理函数调用中使用的非法参数。
- 22. 类`out_of_range`处理字符串下标`out_of_range`错误。
- 23. 如果使用了大于字符串对象允许的最大长度的长度，类`length_error`将处理当使用的长度大于被操作对象允许的最大长度时发生的错误。
- 24. 如果运算符`new`无法分配内存空间，它将抛出`bad_alloc`异常。
- 25. 类`runtime_error`旨在处理只能在程序执行期间检测到的错误。例如，为了处理算术上溢和下溢异常，从类`runtime_error`派生了`overflow_error`和`underflow_error`类。
- 26. catch块通常处理异常，或部分处理异常，然后要么重新抛出相同的异常，要么重新抛出另一个异常，以便调用环境处理该异常。
- 27. C++允许程序员创建自己的异常类，以处理C++异常类未涵盖的异常以及他们自己的异常。
- 28. C++使用与处理内置异常相同的机制来处理您定义的异常。但是，您必须使用`throw`语句抛出自己的异常。
- 29. 在C++中，任何类都可以被视为异常类。它不必继承自类`exception`。使一个类成为异常类的是它的使用方式。
- 30. 重新抛出catch块捕获的异常的通用语法是：

```cpp
throw;
```

在这种情况下，重新抛出相同的异常；或者：

```cpp
throw expression;
```

其中`expression`是一个常量值、变量或对象。被抛出的对象可以是特定对象或匿名对象。

- 31. 函数使用`throw`子句在其头部指定它抛出的异常。
- 32. 当函数中抛出异常时，函数可以执行以下操作：什么都不做；部分处理异常并抛出相同异常或新异常；或者抛出新异常。在上述每种情况下，函数调用栈都会展开，以便异常能在下一个`try/catch`块中被捕获。栈展开持续进行，直到某个`try/catch`处理了该异常，或者程序未处理该异常。
- 33. 如果程序未处理该异常，则调用`terminate`函数终止程序。

## 练习

- 1. 判断以下语句为真还是假。
  - a. `catch`块的列出顺序不重要。
  - b. 异常可以在其发生的函数中捕获，也可以在导致该函数被调用的任何函数中捕获。
  - c. 处理异常的一种方法是打印错误消息并退出程序。
  - d. 所有异常都需要被报告以避免编译错误。

- 2. `try`块和`catch`块之间的区别是什么？

- 3. 如果抛出了异常但未被捕获，会发生什么？

- 4. 如果`try`块中没有抛出异常，会发生什么？

- 5. 如果在`try`块中抛出了异常，会发生什么？

- 6. 以下C++代码有什么问题？同时，提供正确的代码。

```cpp
double balance = 25000;
double intRate;

catch (double x)
{
    cout << "Negative interest rate: " << x << endl;
}
try
{
    cout << "Enter the interest rate: ";
    cin >> intRate;
    cout << endl;

    if (intRate < 0.0)
        throw intRate;

    cout << "Interest: $" << balance * intRate / 100 << endl;
}
```

- 7. 以下C++代码有什么问题？同时，提供正确的代码。

```cpp
double radius;

try
{
    cout << "Enter the radius: ";
    cin >> radius;
    cout << endl;

    if (radius < 0.0)
        throw radius;

    cout << "Area: " << 3.1416 * radius * radius << endl;
    cout << "Entering the catch block." << endl;
}
catch (double x)
{
    cout << "Negative radius: " << x << endl;
}
```

- 8. 考虑以下C++代码：

```cpp
double balance;

try
{
    cout << "Enter the balance: ";
    cin >> balance;
    cout << endl;

    if (balance < 1000.00)
        throw balance;

    cout << "Leaving the try block." << endl;
}
catch (double x)
{
    cout << "Current balance: " << x << endl;
    cout << "Balance must be greater than 1000.00" << endl;
}
```

  - a. 在这段代码中，识别try块。
  - b. 在这段代码中，识别catch块。
  - c. 在这段代码中，识别catch块参数及其类型。
  - d. 在这段代码中，识别throw语句。

- 9. 假定练习8中给出的代码。

  - a. 如果输入是1200，输出是什么？
  - b. 如果输入是975，输出是什么？
  - c. 如果输入是−2000，输出是什么？

- 10. 考虑以下C++代码：

```cpp
int lowerLimit;
.
.
.
try
{
    cout << "Entering the try block." << endl;

    if (lowerLimit < 100)
        throw exception("Lower limit violation.");

    cout << "Exiting the try block." << endl;
}
catch (exception eObj)
{
    cout << "Exception: " << eObj.what() << endl;
}
cout << "After the catch block" << endl;
```

如果出现以下情况，输出是什么：

  - a. lowerLimit的值为50？
  - b. lowerLimit的值为150？

- 11. 考虑以下C++代码：

```cpp
int lowerLimit;
int divisor;
int result;

try
{
    cout << "Entering the try block." << endl;

    if (divisor == 0)
        throw 0;
    if (lowerLimit < 100)
        throw string("Lower limit violation.");

    result = lowerLimit / divisor;
    cout << "Exiting the try block." << endl;
}
catch (int x)
{
    cout << "Exception: " << x << endl;
    result = 120;
}
catch (string str)
{
    cout << "Exception: " << str << endl;
}

cout << "After the catch block" << endl;
```
