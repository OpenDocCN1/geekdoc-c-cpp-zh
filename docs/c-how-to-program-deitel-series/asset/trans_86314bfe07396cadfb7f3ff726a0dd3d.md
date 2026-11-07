
由函数 `quotient` 的 `throw` 语句（第14行）创建的 `DivideByZeroException` 对象，因此 catch 处理程序*不会*复制该异常对象。

`catch` 主体（第39–40行）打印基类 `runtime_error` 的 `what` 函数返回的错误信息——即 `DivideByZeroException` 构造函数（图17.1第11–12行）传递给 `runtime_error` 基类构造函数的字符串。

> **良好编程实践 17.1**
>
> *将每种抛出的异常类型与命名恰当的异常类型关联起来，可以提高程序的清晰度。*

## 17.3 重新抛出异常

函数可能会使用资源（如文件），并且如果发生异常，可能希望释放该资源（即关闭文件）。异常处理程序在收到异常后，可以释放资源，然后通过**重新抛出**异常的语句通知其调用者发生了异常：

```cpp
throw;
```

无论处理程序能否处理异常，处理程序都可以**重新抛出**异常，以便在处理程序之外进行进一步处理。下一个外围 try 块会检测到被重新抛出的异常，该外围 try 块之后列出的 catch 处理程序将尝试处理该异常。

> **常见编程错误 17.5**
>
> *在 catch 处理程序之外执行空的 `throw` 语句会放弃异常处理并立即终止程序。*

图 17.3 的程序演示了重新抛出异常。在 main 的 try 块（第29–34行）中，第32行调用函数 `throwException`（第8–24行）。`throwException` 函数也包含一个 try 块（第11–15行），其中第14行的 `throw` 语句抛出了标准库类 `exception` 的一个实例。函数 `throwException` 的 catch 处理程序（第16–21行）捕获该异常，打印错误信息（第18–19行），并重新抛出异常（第20行）。这会终止函数 `throwException`，并将控制权返回给 `main` 中 `try...catch` 块的第32行。该 try 块终止（因此第33行不执行），`main` 中的 catch 处理程序（第35–38行）捕获该异常并打印错误信息（第37行）。由于在本例中我们不在 catch 处理程序中使用异常参数，因此我们省略了异常参数名，只指定要捕获的异常类型（第16行和第35行）。

```cpp
// Fig. 17.3: fig17_03.cpp
// Rethrowing an exception.
#include <iostream>
#include <exception>
using namespace std;

// throw, catch and rethrow exception
void throwException()
{
   // throw exception and catch it immediately
   try
   {
      cout << "Function throwException throws an exception\n";
      throw exception(); // generate exception
   } // end try
   catch ( exception & ) // handle exception
   {
      cout << "\n Exception handled in function throwException"
           << "\n Function throwException rethrows exception";
      throw; // rethrow exception for further processing
   } // end catch

   cout << "This also should not print\n";
} // end of function throwException

int main()
{
   // throw exception
   try
   {
      cout << "\nmain invokes function throwException\n";
      throwException();
      cout << "This should not print\n";
   } // end try
   catch ( exception & ) // handle exception
   {
      cout << "\n\nException handled in main\n";
   } // end catch

   cout << "Program control continues after catch in main\n";
} // end main
```

```text
main invokes function throwException
   Function throwException throws an exception
   Exception handled in function throwException
   Function throwException rethrows exception

Exception handled in main
Program control continues after catch in main
```

**图 17.3** | 重新抛出异常。

## 17.4 栈展开

当异常在特定作用域内抛出但未被捕获时，函数调用栈会被“展开”，并尝试在下一个外层 try...catch 块中捕获该异常。展开函数调用栈意味着未捕获异常的函数会终止，该函数中所有已完成初始化的局部变量都会被销毁，控制权将返回到最初调用该函数的语句。如果该语句被 try 块包围，则尝试捕获异常。如果该语句未被 try 块包围，则再次发生栈展开。如果没有 catch 处理程序捕获该异常，程序将终止。图 17.4 的程序演示了栈展开。

```cpp
// Fig. 17.4: fig17_04.cpp
// Demonstrating stack unwinding.
#include <iostream>
#include <stdexcept>
using namespace std;

// function3 throws runtime error
void function3()
{
    cout << "In function 3" << endl;

    // no try block, stack unwinding occurs, return control to function2
    throw runtime_error( "runtime error in function3" ); // no print
} // end function3

// function2 invokes function3
void function2()
{
    cout << "function3 is called inside function2" << endl;
    function3(); // stack unwinding occurs, return control to function1
} // end function2

// function1 invokes function2
void function1()
{
    cout << "function2 is called inside function1" << endl;
    function2(); // stack unwinding occurs, return control to main
} // end function1

// demonstrate stack unwinding
int main()
{
    // invoke function1
    try
    {
        cout << "function1 is called inside main" << endl;
        function1(); // call function1 which throws runtime_error
    } // end try
    catch ( runtime_error &error ) // handle runtime error
    {
        cout << "Exception occurred: " << error.what() << endl;
        cout << "Exception handled in main" << endl;
    } // end catch
} // end main
```

```text
function1 is called inside main
function2 is called inside function1
function3 is called inside function2
In function 3
Exception occurred: runtime_error in function3
Exception handled in main
```

**图 17.4** | 栈展开。

在 main 中，try 块（第34–38行）调用 function1（第24–28行）。接着，function1 调用 function2（第17–21行），function2 又调用 function3（第8–14行）。function3 的第13行抛出了一个 `runtime_error` 对象。但是，由于第13行的 throw 语句不在任何 try 块内，因此发生栈展开——function3 在第13行终止，然后将控制权返回给 function2 中调用 function3 的语句（即第20行）。由于第20行不在任何 try 块内，因此再次发生栈展开——function2 在第20行终止，并将控制权返回给 function1 中调用 function2 的语句（即第27行）。由于第27行不在任何 try 块内，因此再次发生栈展开——function1 在第27行终止，并将控制权返回给 main 中调用 function1 的语句（即第37行）。第34–38行的 try 块包围了该语句，因此该 try 块之后的第一个匹配的 catch 处理程序（第39–43行）捕获并处理该异常。第41行使用 `what` 函数显示异常信息。

## 17.5 何时使用异常处理

异常处理旨在处理**同步错误**，这些错误在语句执行时发生，例如*数组下标越界*、*算术溢出*（即值超出可表示范围）、*除数为零*、*无效的函数参数*和*内存分配失败*（由于内存不足）。异常处理并非旨在处理与**异步事件**相关的错误（例如磁盘 I/O 完成、网络消息到达、鼠标点击和按键），这些事件与程序的控制流并行且独立地发生。

![](img/b42ba5cd262b1358d16610173f975e4d_785_0.png)

> **软件工程观察 17.4**
>
> 异常处理提供了一种统一的问题处理技术。这有助于程序员管理大型项目，并理解彼此的差错处理代码。

![](img/b42ba5cd262b1358d16610173f975e4d_785_1.png)

> **软件工程观察 17.5**
>
> 异常处理使预定义的软件组件能够将问题传递给特定于应用程序的组件，然后这些组件可以以特定于应用程序的方式处理问题。

异常处理对于处理程序与软件元素（如成员函数、构造函数、析构函数和类）交互时出现的问题也很有用。此类软件元素通常在出现问题时使用异常来通知程序。这使您能够为每个应用程序实现*定制的错误处理*。
