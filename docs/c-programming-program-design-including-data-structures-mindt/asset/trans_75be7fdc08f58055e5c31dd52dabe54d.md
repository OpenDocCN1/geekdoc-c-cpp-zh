

```cpp
catch (divisionByZero divByZeroObj)                 //Line 11
{                                                   //Line 12
        cout << "Line 13: In main: "              //Line 13
             << divByZeroObj.what() << endl;       //Line 14
}                                                   //Line 14

        return 0;                                  //Line 15
}                                                   //Line 16

void doDivision() throw (divisionByZero)            //Line 17
{                                                   //Line 18
        int dividend, divisor, quotient;            //Line 19

        try                                         //Line 20
        {                                           //Line 21
                cout << "Line 22: Enter the dividend: "; //Line 22
                cin >> dividend;                    //Line 23
                cout << endl;                       //Line 24

                cout << "Line 25: Enter the divisor: ";  //Line 25
                cin >> divisor;                     //Line 26
                cout << endl;                       //Line 27

                if (divisor == 0)                   //Line 28
                        throw divisionByZero();    //Line 29

                quotient = dividend / divisor;      //Line 30
                cout << "Line 31: Quotient = " << quotient //Line 31
                     << endl;                       //Line 32
        }                                           //Line 32
        catch (divisionByZero)                       //Line 33
        {                                           //Line 34
                throw divisionByZero("Division by zero found!"); //Line 35
        }                                           //Line 36
}                                                   //Line 37
```

**示例运行 1：**在此示例运行中，用户输入以阴影显示。

```text
Line 22: Enter the dividend: 28
Line 25: Enter the divisor: 6
Line 31: Quotient = 4
```

**示例运行 2：**在此示例运行中，用户输入以阴影显示。

```text
Line 22: Enter the dividend: 35
Line 25: Enter the divisor: 0
Line 13: In main: Division by zero found!
```

该程序的工作方式与示例 14-15 中的程序相同。唯一的区别是，此处第 33 行的 catch 块重新抛出了一个不同的异常值，也就是一个对象。

示例 14-15 和 14-16 中的程序说明了函数如何重新抛出相同的异常，或者抛出另一个异常供调用函数处理。这种机制非常有用，因为它允许程序在同一个位置处理所有异常，而不是将异常处理代码分散到整个程序中。

## 异常处理技术

当程序中发生异常时，程序员通常有三种选择：终止程序、在程序中加入用于从异常中恢复的代码，或者记录错误并继续运行。以下各节将分别讨论这些情况。

### 终止程序

在某些情况下，发生异常时让程序终止是最好的选择。假设你编写了一个从文件中输入数据的程序。如果程序执行时输入文件不存在，那么继续运行程序就没有意义。在这种情况下，程序可以输出适当的错误消息并终止。

### 修复错误并继续运行

在其他情况下，你可能希望处理异常并让程序继续运行。假设有一个以整数作为输入的程序。如果用户输入了字母而不是数字，输入流就会进入失败状态。这种情况下，你可以加入必要的代码，持续提示用户输入数字，直到输入有效为止。示例 14-17 中的程序说明了这种情况。

### 示例 14-17

```cpp
// Handle exceptions by fixing the errors. The program
// continues to prompt the user until a valid input is entered.

#include <iostream>                              //Line 1

using namespace std;                              //Line 2

int main()                                         //Line 3
{                                                  //Line 4
    int number;                                    //Line 5
    bool done = false;                             //Line 6

    char str[] =
        "The input stream is in the fail state.";  //Line 7

    do                                              //Line 8
    {                                               //Line 9
        try                                         //Line 10
        {                                           //Line 11
            cout << "Line 12: Enter an integer: "; //Line 12
            cin >> number;                          //Line 13
            cout << endl;                           //Line 14
            if (!cin)                         //Line 15
                throw str;                     //Line 16

            done = true;                       //Line 17
            cout << "Line 18: Number = " << number  //Line 18
                 << endl;
        }                                  //Line 19
        catch (const char messageStr[])     //Line 20
        {                                  //Line 21
            cout << "Line 22: " << messageStr  //Line 22
                 << endl;
            cout << "Line 23: Restoring the "  //Line 23
                 << "input stream." << endl;
            cin.clear();                    //Line 24
            cin.ignore(100, '\n');          //Line 25
        }                                  //Line 26
    }                                  //Line 27
    while (!done);                     //Line 28

    return 0;                          //Line 29
}                                  //Line 30
```

**示例运行：**在此示例运行中，用户输入以阴影显示。

```text
Line 12: Enter an integer: c4

Line 22: The input stream is in the fail state.
Line 23: Restoring the input stream.
Line 12: Enter an integer: s7

Line 22: The input stream is in the fail state.
Line 23: Restoring the input stream.
Line 12: Enter an integer: 28

Line 18: Number = 28
```

该程序提示用户输入一个整数。如果输入无效，标准输入流就会进入失败状态。在 try 块中，第 16 行的语句抛出一个异常，该异常是一个字符串。控制权转移到 catch 块，异常随后被捕获并处理。第 24 行的语句将输入流恢复到正常状态，第 25 行的语句清除该行中剩余的输入。do...while 循环会继续提示用户输入，直到用户输入一个有效数字。

### 记录错误并继续运行

发生异常时终止的程序通常假定这种终止是相对安全的。但是，如果程序用于运行核反应堆或持续监控卫星，那么发生异常时就不能终止。这些程序应该报告异常，但程序必须继续运行。

例如，考虑一个分析航空公司票务交易的程序。由于每天会发生大量票务交易，因此每天结束时都会运行一个程序来验证当天的交易。这类程序如果使用异常来识别错误条目，将需要大量时间来处理交易。相反，发生异常时，程序应该将异常写入文件，并继续分析这些交易。

## 栈展开

本章中的示例展示了如何捕获和处理异常。具体来说，你已经学习了如何在同一个块中捕获并处理异常，以及如何在调用环境中处理捕获到的异常。

当异常在某个函数中被抛出时，该函数可以执行以下操作：

- 什么也不做。
- 对异常进行部分处理，然后抛出相同的异常或一个新异常。
- 抛出一个新异常。

在上述每种情况下，函数调用栈都会展开，以便在下一个 try/catch 块中捕获异常。当函数调用栈展开时，未捕获异常和/或未重新抛出异常的函数会终止，其局部变量所占用的内存也会被销毁。栈展开会持续进行，直到某个 try/catch 处理该异常，或者程序没有处理该异常。如果程序没有处理该异常，就会调用 `terminate` 函数来终止程序。

示例 14-18 和 14-19 说明了异常是如何传播的。为此，我们先定义下面的异常类：

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
```

