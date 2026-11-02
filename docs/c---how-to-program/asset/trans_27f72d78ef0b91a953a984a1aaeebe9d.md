
```cpp
// throw, catch and rethrow exception
void throwException()
{
    // throw exception and catch it immediately
    try
    {
        cout << "  Function throwException throws an exception\n";
        throw exception(); // generate exception
    } // end try
    catch ( exception & ) // handle exception
    {
        cout << "  Exception handled in function throwException"
             << "\n Function throwException rethrows exception";
        throw; // rethrow exception for further processing
    } // end catch

    cout << "This also should not print\n";
} // end function throwException

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

main invokes function throwException
Function throwException throws an exception
Exception handled in function throwException
Function throwException rethrows exception

Exception handled in main
Program control continues after catch in main

图22.3 | 重新抛出异常。（第2部分，共2部分。）

## 22.4 栈展开

当异常在特定作用域内抛出但未被捕获时，函数调用栈会“展开”，并尝试在下一个外层try...catch块中捕获该异常。展开函数调用栈意味着未捕获异常的函数终止，该函数中所有已完成初始化的局部变量被销毁，控制权返回到最初调用该函数的语句。如果try块包围了该语句，则会尝试捕获异常。如果try块未包围该语句，则再次发生栈展开。如果没有捕获处理程序最终捕获此异常，程序将终止。图22.4的程序演示了栈展开。

```cpp
// Fig. 22.4: fig22_04.cpp
// Demonstrating stack unwinding.
#include <iostream>
#include <stdexcept>
using namespace std;

// function3 throws runtime error
void function3()
{
    cout << "In function 3" << endl;

    // no try block, stack unwinding occurs, return control to function2
    throw runtime_error( "runtime_error in function3" ); // no print
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

```
function1 is called inside main
function2 is called inside function1
function3 is called inside function2
In function 3
Exception occurred: runtime_error in function3
Exception handled in main
```

图22.4 | 栈展开。（第2部分，共2部分。）

在main中，try块（第34–38行）调用function1（第24–28行）。接下来，function1调用function2（第17–21行），function2又调用function3（第8–14行）。function3的第13行抛出一个runtime_error对象。然而，由于没有try块包围第13行的throw语句，发生栈展开——function3在第13行终止，然后将控制权返回到function2中调用function3的语句（即第20行）。由于没有try块包围第20行，再次发生栈展开——function2在第20行终止，并将控制权返回到function1中调用function2的语句（即第27行）。由于没有try块包围第27行，再次发生栈展开——function1在第27行终止，并将控制权返回到main中调用function1的语句（即第37行）。第34–38行的try块包围了该语句，因此该try块之后的第一个匹配的catch处理程序（第39–43行）捕获并处理该异常。第41行使用what函数显示异常消息。

## 22.5 何时使用异常处理

异常处理专为处理同步错误而设计，此类错误在语句执行时发生，例如数组下标越界、算术溢出（即数值超出可表示的范围）、除以零、无效的函数参数以及内存分配失败（由于内存不足）。异常处理并非为处理与异步事件相关的错误而设计（例如磁盘I/O完成、网络消息到达、鼠标点击和按键），这些事件与程序的控制流并行发生且独立于控制流。

> 软件工程观察 22.4
> 异常处理提供了一种单一、统一的问题处理技术。这有助于大型项目中的程序员理解彼此的出错处理代码。

> 软件工程观察 22.5
> 异常处理使预定义的软件组件能够将问题传达给特定于应用的组件，然后后者可以以特定于应用的方式处理这些问题。

异常处理对于处理程序与软件元素（如成员函数、构造函数、析构函数和类）交互时出现的问题也很有用。此类软件元素通常使用异常在问题发生时通知程序。这使您可以为每个应用实现定制的错误处理。

### 软件工程观察 22.6

具有常见错误条件的函数应返回nullPtr、0或其他适当值（如bool），而不是抛出异常。调用此类函数的程序可以检查返回值以确定函数调用是成功还是失败。

复杂应用程序通常由预定义的软件组件和使用这些预定义组件的特定于应用的组件组成。当预定义组件遇到问题时，该组件需要一种机制将问题传达给特定于应用的组件——预定义组件无法预先知道每个应用如何处理出现的问题。

### C++11：声明不抛出异常的函数

从C++11开始，如果函数不抛出任何异常，也不调用任何会抛出异常的函数，则应明确声明该函数不抛出异常。这向客户端代码程序员表明，无需将对该函数的调用放入try块中。只需在原型和定义中的函数参数列表右侧添加noexcept。对于const成员函数，将noexcept放在const之后。如果声明为noexcept的函数调用了抛出异常或执行throw语句的另一个函数，则程序终止。我们在《C++程序设计教程（第9版）》的第24章中会进一步讨论noexcept。

## 22.6 构造函数、析构函数与异常处理

首先，让我们讨论一个我们已经提到但尚未满意解决的问题：在构造函数中检测到错误时会发生什么？例如，当构造函数接收到无效数据时，它应如何响应？由于构造函数无法返回值来指示错误，我们必须选择另一种方式来表示对象未被正确构造。一种方案是返回构造不当的对象，并希望使用它的人会进行适当的测试以确定其处于不一致状态。另一种方案是在构造函数之外设置某个变量。更可取的方案是要求构造函数抛出包含错误信息的异常，从而为程序处理该失败提供机会。

在构造函数抛出异常之前，对于作为正在构造对象的一部分且其构造函数已运行完毕的任何成员对象，会调用其析构函数。在捕获异常之前，会为try块中构造的每个自动对象调用析构函数。在异常处理程序开始执行时，保证栈展开已完成。如果因栈展开而调用的析构函数抛出异常，则程序终止。这与各种安全攻击有关。

### 错误预防提示 22.4

析构函数应捕获异常以防止程序终止。

### 错误预防提示 22.5

不要从具有静态存储期限的对象的构造函数中抛出异常。此类异常无法被捕获。

