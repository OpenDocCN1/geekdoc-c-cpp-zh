

本章首先概述了异常处理的概念，然后演示了基本的异常处理技术。我们通过一个示例展示这些技术，该示例演示了处理函数尝试除以零时发生的异常。我们随后讨论了额外的异常处理问题，例如如何处理在构造函数或析构函数中发生的异常，以及如何处理 operator new 为对象分配内存失败时发生的异常。我们通过介绍 C++ 标准库为处理异常提供的几个类来结束本章。

## 16.2 异常处理概述

程序逻辑经常测试决定程序执行如何进行的条件。请考虑以下伪代码：

```
Perform a task

If the preceding task did not execute correctly
    Perform error processing

Perform next task

If the preceding task did not execute correctly
    Perform error processing

...
```

在该伪代码中，我们首先执行一个任务。然后我们测试该任务是否正确执行。如果没有，我们执行错误处理。否则，我们继续下一个任务。虽然这种形式的错误处理有效，但将程序逻辑与错误处理逻辑混合在一起会使程序难以阅读、修改、维护和调试——尤其是在大型应用程序中。

### Performance Tip 16.1

> 如果潜在问题很少发生，将程序逻辑和错误处理逻辑混合在一起会降低程序的性能，因为程序必须（可能频繁地）执行测试以确定任务是否正确执行以及是否可以执行下一个任务。

异常处理使您能够从程序执行的“主线”中移除错误处理代码，从而提高程序的清晰度并增强可修改性。程序员可以决定处理任何他们选择的异常——所有异常、特定类型的异常或一组相关类型的异常（例如，属于继承层次结构的异常类型）。这种灵活性降低了错误被忽视的可能性，从而使程序更加健壮。

对于不支持异常处理的编程语言，程序员通常会推迟编写错误处理代码，有时甚至忘记包含它。这会导致软件产品不够健壮。C++ 使您能够从项目开始之初就轻松处理异常。

## 16.3 示例：处理除以零的尝试

让我们考虑一个简单的异常处理示例（图 16.1–16.2）。本示例的目的是展示如何防止常见的算术问题——除以零。

在 C++ 中，使用整数算术进行除以零通常会导致程序过早终止。在浮点算术中，一些 C++ 实现允许除以零，在这种情况下，正无穷大或负无穷大分别显示为 INF 或 −INF。

在本示例中，我们定义了一个名为 `quotient` 的函数，它接收用户输入的两个整数，并将其第一个 int 参数除以第二个 int 参数。在执行除法之前，函数将第一个 int 参数的值转换为类型 double。然后，第二个 int 参数的值在计算中提升为类型 double。因此，函数 `quotient` 实际上使用两个 double 值执行除法并返回一个 double 结果。

尽管在浮点算术中允许除以零，但为本示例的目的，我们将任何除以零的尝试视为错误。因此，函数 `quotient` 在允许除法进行之前测试其第二个参数以确保其不为零。如果第二个参数为零，函数将使用异常向调用者指示发生了问题。调用者（本示例中的 `main`）然后可以处理异常，并允许用户在再次调用函数 `quotient` 之前输入两个新值。以这种方式，即使在输入不当值后，程序也可以继续执行，从而使程序更加健壮。

该示例包含两个文件。`DivideByZeroException.h`（图 16.1）定义了一个表示示例中可能出现的问题类型的异常类，而 `fig16_02.cpp`（图 16.2）定义了 `quotient` 函数和调用它的 `main` 函数。函数 `main` 包含演示异常处理的代码。

### 定义一个异常类来表示可能出现的问题类型

图 16.1 将类 `DivideByZeroException` 定义为标准库类 `runtime_error`（在头文件 `<stdexcept>` 中定义）的派生类。类 `runtime_error`——标准库类 `exception`（在头文件 `<exception>` 中定义）的派生类——是表示运行时错误的 C++ 标准基类。类 `exception` 是所有异常的标准 C++ 基类。（第 16.13 节详细讨论了类 exception 及其派生类。）典型的从 `runtime_error` 类派生的异常类仅定义一个构造函数（例如，第 12–13 行），该构造函数将错误消息字符串传递给基类 `runtime_error` 构造函数。每个直接或间接从 exception 派生的异常类都包含虚拟函数 what，它返回异常对象的错误消息。请注意，您不需要将自定义异常类（例如 DivideByZeroException）从 C++ 提供的标准异常类派生。但是，这样做允许程序员使用虚拟函数 what 获取适当的错误消息。我们在图 16.2 中使用此 DivideByZeroException 类的对象来指示尝试除以零时。

```cpp
// Fig. 16.1: DivideByZeroException.h
// Class DivideByZeroException definition.
#include <stdexcept> // stdexcept header file contains runtime_error
using std::runtime_error; // standard C++ library class runtime_error

// DivideByZeroException objects should be thrown by functions
// upon detecting division-by-zero exceptions
class DivideByZeroException : public runtime_error
{
public:
   // constructor specifies default error message
   DivideByZeroException()
      : runtime_error("attempted to divide by zero") { }
}; // end class DivideByZeroException
```

**Fig. 16.1** | Class `DivideByZeroException` definition.

from exception contains the virtual function what, which returns an exception object’s error message. Note that you are not required to derive a custom exception class, such as DivideByZeroException, from the standard exception classes provided by C++. However, doing so allows programmers to use the virtual function what to obtain an appropriate error message. We use an object of this DivideByZeroException class in Fig. 16.2 to indicate when an attempt is made to divide by zero.

### 演示异常处理

图 16.2 中的程序使用异常处理来包装可能抛出“除以零”异常的代码并处理该异常（如果发生）。应用程序使用户能够输入两个整数，这些整数作为参数传递给函数 quotient（第 13–21 行）。该函数将其第一个参数（分子）除以第二个参数（分母）。假设用户未将 0 指定为除法的分母，函数 quotient 将返回除法结果。但是，如果用户对分母输入 0，函数 quotient 将抛出异常。在示例输出中，前两行显示了成功的计算，接下来的两行显示了由于尝试除以零而导致的失败计算。当异常发生时，程序会通知用户错误并提示用户输入两个新整数。在讨论代码之后，我们将考虑产生这些输出的用户输入和程序控制流。

```
// Fig. 16.2: Fig16_02.cpp
// A simple exception-handling example that checks for
// divide-by-zero exceptions.
#include <iostream>
using std::cin;
using std::cout;
using std::endl;

#include "DivideByZeroException.h" // DivideByZeroException class

// perform division and throw DivideByZeroException object if
// divide-by-zero exception occurs
double quotient( int numerator, int denominator )
{
    // throw DivideByZeroException if trying to divide by zero
    if ( denominator == 0 )
        throw DivideByZeroException(); // terminate function

    // return division result
    return static_cast<double>( numerator ) / denominator;
} // end function quotient

int main()
{
    int number1; // user-specified numerator
    int number2; // user-specified denominator
    double result; // result of division

    cout << "Enter two integers (end-of-file to end): ";

    // enable user to enter two integers to divide
    while ( cin >> number1 >> number2 )
    {
        // try block contains code that might throw exception
        // and code that should not execute if an exception occurs
        try
        {
            result = quotient( number1, number2 );
            cout << "The quotient is: " << result << endl;
        } // end try

        // exception handler handles a divide-by-zero exception
        catch ( DivideByZeroException &divideByZeroException )
        {
            cout << "Exception occurred: "
                 << divideByZeroException.what() << endl;
        } // end catch

        cout << "\nEnter two integers (end-of-file to end): ";
    } // end while
```

Fig. 16.2 | Exception-handling example that throws exceptions on attempts to divide by zero. (Part 1 of 2.)

```
52      cout << endl;
53      return 0; // terminate normally
54  } // end main
```

Enter two integers (end-of-file to end): 100 7
The quotient is: 14.2857

Enter two integers (end-of-file to end): 100 0
Exception occurred: attempted to divide by zero

Enter two integers (end-of-file to end): ^Z

Fig. 16.2 | Exception-handling example that throws exceptions on attempts to divide by zero. (Part 2 of 2.)

### 将代码封闭在 try 块中

程序首先提示用户输入两个整数。整数在 while 循环的条件中输入（第 32 行）。用户输入表示分子和分母的值后，程序控制进入循环的主体（第 33–50 行）。第 38 行将这些值传递给函数 quotient（第 13–21 行），该函数要么除以整数并返回结果，要么在尝试除以零时抛出异常（即指示发生错误）。异常处理针对函数检测到错误但无法处理错误的情况。

C++ 提供 try 块以实现异常处理。try 块由关键字 try 组成，后跟定义可能发生异常的代码块的大括号 {}。try 块封装可能导致异常的语句以及如果发生异常应跳过的语句。

