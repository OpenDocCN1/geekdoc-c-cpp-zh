
```cpp
void doDivision() throw (divisionByZero)
{
    int dividend, divisor, quotient;                    //Line 6

    try                                             //Line 7
    {
        cout << "Line 8: Enter the dividend: ";       //Line 8
        cin >> dividend;                              //Line 9
        cout << endl;                                 //Line 10

        cout << "Line 11: Enter the divisor: ";       //Line 11
        cin >> divisor;                               //Line 12
        cout << endl;                                 //Line 13

        if (divisor == 0)                             //Line 14
            throw divisionByZero();                   //Line 15

        quotient = dividend / divisor;                //Line 16
        cout << "Line 17: Quotient = " << quotient    //Line 17
             << endl;
    }
    catch (divisionByZero)                            //Line 18
    {
        throw divisionByZero("Division by zero found!"); //Line 19
    }
}
```

**示例运行 1：** 在此示例运行中，用户输入以阴影显示。

第 8 行：输入被除数：`34`

第 11 行：输入除数：`5`

第 17 行：商 = 6

**示例运行 2：** 在此示例运行中，用户输入以阴影显示。

第 8 行：输入被除数：`56`

第 11 行：输入除数：`0`

第 4 行：在 main 中：发现除以零！

此程序的工作方式与示例 16-14 中的程序相同。唯一区别是，在这里，第 18 行中的 `catch` 块重新抛出一个不同的异常值，即一个 divisionByZero 对象。

示例 16-14 和 16-15 中的程序说明了函数如何重新抛出同一异常，或抛出另一个异常供调用函数处理。此机制非常有用，因为它允许程序在一个位置处理所有异常，而不是将异常处理代码分散到整个程序中。

## 异常处理技术

当程序中发生异常时，程序员通常有三种选择：终止程序、在程序中加入代码以从异常中恢复，或记录错误并继续。以下各节讨论这些情况。

### 终止程序

在某些情况下，最好在发生异常时让程序终止。假设你编写了一个从文件输入数据的程序。如果程序执行时输入文件不存在，那么继续运行该程序没有意义。在这种情况下，程序可以输出适当的错误消息并终止。

### 修复错误并继续

在其他情况下，你会希望处理异常并让程序继续。假设你有一个接收整数输入的程序。如果用户输入字母而不是数字，输入流将进入失败状态。在这种情况下，你可以加入必要的代码，持续提示用户输入数字，直到输入有效。示例 16-16 中的程序说明了这种情况。

### 示例 16-16

```cpp
// Handle exceptions by fixing the errors. The program continues to
// prompt the user until a valid input is entered.

#include <iostream>
#include <string>

using namespace std;

int main()
{
    int number;                            //Line 1
    bool done = false;                     //Line 2

    string str =
        "The input stream is in the fail state."; //Line 3

    do                                     //Line 4
    {                                      //Line 5
        try                                //Line 6
        {                                  //Line 7
            cout << "Line 8: Enter an integer: "; //Line 8
            cin >> number;                 //Line 9
            cout << endl;                  //Line 10
            if (!cin)                      //Line 11
                throw str;                 //Line 12

            done = true;                   //Line 13
            cout << "Line 14: Number = " << number
                 << endl;                  //Line 14
        }                                  //Line 15
        catch (string messageStr)          //Line 16
        {                                  //Line 17
            cout << "Line 18: " << messageStr
                 << endl;                  //Line 18
            cout << "Line 19: Restoring the "
                 << "input stream." << endl; //Line 19
            cin.clear();                   //Line 20
            cin.ignore(100, '\n');         //Line 21
        }                                  //Line 22
    } while (!done);                       //Line 23

    return 0;                              //Line 24
}
```

**示例运行：** 在此示例运行中，用户输入以阴影显示。

```
Line 8: Enter an integer: r5

Line 18: The input stream is in the fail state.
Line 19: Restoring the input stream.
Line 8: Enter an integer: d45

Line 18: The input stream is in the fail state.
Line 19: Restoring the input stream.
Line 8: Enter an integer: hw3

Line 18: The input stream is in the fail state.
Line 19: Restoring the input stream.
Line 8: Enter an integer: 48

Line 14: Number = 48
```

此程序提示用户输入一个整数。如果输入无效，标准输入流进入失败状态。在 **try** 块中，第 12 行的语句抛出一个异常，该异常是一个 string 对象。控制转移到 **catch** 块，异常被捕获并处理。第 20 行的语句将流恢复到正常状态，第 21 行的语句清除该行剩余的输入。**do...while** 循环继续提示用户，直到用户输入有效数字。

### 记录错误并继续

发生异常时终止的程序通常假定这种终止是相当安全的。然而，如果你的程序旨在运行核反应堆或持续监控卫星，那么发生异常时不能终止。这些程序应报告异常，但程序必须继续运行。

例如，考虑一个分析航空公司票务交易的程序。由于每天会发生大量票务交易，程序会在每天结束时运行，以验证当天的交易。这类程序处理交易并使用异常识别任何错误条目会耗费大量时间。相反，当发生异常时，程序应将异常写入文件，并继续分析交易。

### 栈展开

本章给出的示例展示了如何捕获和处理异常。特别是，你学习了如何在同一块中捕获和处理异常，以及在调用环境中处理已捕获的异常。

当在（比如）一个函数中抛出异常时，该函数可以执行以下操作：

- 什么都不做。
- 部分处理异常，并抛出同一异常或新异常。
- 抛出一个新异常。

在每种情况下，函数调用栈都会展开，以便异常可以在下一个 try/catch 块中被捕获。当函数调用栈展开时，未捕获异常和/或返回的函数会终止，其局部变量的内存会被销毁。栈展开会持续进行，直到某个 try/catch 处理该异常，或者程序不处理该异常。如果程序不处理该异常，则调用 `terminate` 函数终止程序。

示例 16-17 和 16-18 说明了异常如何传播。为此，让我们定义以下异常类：

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

> **注意** 在类 `myException` 的定义中，构造函数也可以写成如下形式：
>
> ```cpp
> myException() : message("Something is wrong!") {}
> myException(string str) : message(str) {}
> ```

示例 16-17 中的程序说明了在函数中抛出的异常如何在调用环境中得到处理。

### 示例 16-17

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
}
```
