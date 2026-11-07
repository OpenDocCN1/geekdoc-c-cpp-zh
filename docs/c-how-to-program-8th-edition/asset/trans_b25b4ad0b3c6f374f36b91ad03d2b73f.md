

```cpp
// throw, catch and rethrow exception
void throwException()
{
    // throw exception and catch it immediately
    try
    {
        cout << " Function throwException throws an exception\n";
        throw exception(); // generate exception
    } // end try
    catch ( exception & ) // handle exception
    {
        cout << " Exception handled in function throwException"
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
        cout << "\nException handled in main\n";
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

**图 16.3**  重新抛出异常。（第 2 部分，共 2 部分。）

## 16.5 异常规范

可选的异常规范（也称为抛出列表）列举了函数可以抛出的异常列表。例如，将

```
throw ( ExceptionA, ExceptionB, ExceptionC )
```

紧接在函数参数列表的右括号之后，表示该函数可以抛出 ExceptionA、ExceptionB 和 ExceptionC 类型或其派生类型的异常。如果函数抛出任何其他异常类型，异常处理机制会调用函数 `unexpected`，默认情况下该函数会终止程序。

不提供异常规范的函数可以抛出任何异常。在函数参数列表后放置 `throw()`——一个空的异常规范——表示该函数不抛出异常。如果函数尝试抛出异常，则会调用函数 unexpected。

1. 异常规范在新的 C++ 标准中已被弃用。我们将在第 23 章讨论新 C++ 标准的异常处理特性。大多数当前编译器会忽略异常规范。

## 16.6 处理意外异常

函数 unexpected 调用通过函数 `set_unexpected` 注册的函数（定义在头文件 <exception> 中）。如果没有以这种方式注册任何函数，默认会调用函数 terminate。调用函数 terminate 的情况包括：

- 1. 异常机制无法为抛出的异常找到匹配的 catch
- 2. 析构函数在栈展开期间尝试抛出异常
- 3. 在当前没有正在处理的异常时尝试重新抛出异常
- 4. 对函数 unexpected 的调用默认会调用函数 terminate

（C++ 标准文档第 15.5.1 节讨论了若干其他情况。）函数 `set_terminate` 可以指定在调用 terminate 时要调用的函数。否则，terminate 会调用 **abort**，后者终止程序，而不调用任何剩余的自动或静态存储类对象的析构函数。当程序过早终止时，这可能导致资源泄漏。

![](img/bfd978e7e9b192bab46ec2a89e481263_675_0.png)

> **常见编程错误 16.7**
> 
> *在未捕获异常的处理过程中中止程序，可能会使某个资源——例如文件流或 I/O 设备——处于其他程序无法获取该资源的状态。这称为资源泄漏。*

函数 set_terminate 和函数 set_unexpected 各自返回一个指针，分别指向 terminate 和 unexpected 最后调用的函数（第一次调用时返回 0）。这使你能够保存该函数指针，以便以后恢复。函数 set_terminate 和 set_unexpected 接受指向返回类型为 void 且不接受参数的函数的指针作为参数。

如果程序员定义的终止函数的最后一个动作不是退出程序，则会调用函数 abort 来结束程序执行。

## 16.7 栈展开

当异常被抛出但在某个特定作用域中未被捕获时，函数调用栈会“展开”，并尝试在下一个外层 try…catch 块中捕获该异常。展开函数调用栈意味着未捕获异常的函数会终止，该函数中的所有局部变量会被销毁，控制权返回到最初调用该函数的语句。如果 try 块包围了该语句，则会尝试捕获该异常。如果 try 块没有包围该语句，则会再次发生栈展开。如果没有 catch 处理程序捕获此异常，则会调用函数 terminate 来终止程序。图 16.4 的程序演示了栈展开。

```cpp
// Fig. 16.4: Fig16_04.cpp
// Demonstrating stack unwinding.
#include <iostream>
#include <stdexcept>
using namespace std;

// function3 throws runtime_error
void function3() throw ( runtime_error )
{
    cout << "In function 3" << endl;

    // no try block, stack unwinding occurs, return control to function2
    throw runtime_error( "runtime_error in function3" ); // no print
} // end function3

// function2 invokes function3
void function2() throw ( runtime_error )
{
    cout << "function3 is called inside function2" << endl;
    function3(); // stack unwinding occurs, return control to function1
} // end function2

// function1 invokes function2
void function1() throw ( runtime_error )
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

图 16.4 | 栈展开。（第 1 部分，共 2 部分。）

不接受参数并返回 void。这个指针指向如果 new 失败时将调用的函数。这为你提供了一种统一的方法来处理所有 new 失败，无论失败发生在程序中的何处。一旦 set_new_handler 在程序中注册了新的处理函数，operator new 在失败时不会抛出 bad_alloc；相反，它会将错误处理推迟给 new-handler 函数。

如果 new 成功分配内存，它会返回指向该内存的指针。如果 new 分配内存失败且 set_new_handler 没有注册 new-handler 函数，则 new 会抛出 bad_alloc 异常。如果 new 分配内存失败且已注册 new-handler 函数，则会调用该 new-handler 函数。C++ 标准规定 new-handler 函数应执行以下任务之一：

- 1. 通过删除其他动态分配的内存（或告诉用户关闭其他应用程序）来提供更多可用内存，并返回到 operator new 以再次尝试分配内存。
- 2. 抛出 bad_alloc 类型的异常。
- 3. 调用函数 abort 或 exit（二者都位于头文件 <cstdlib> 中）来终止程序。

图 16.6 演示了 set_new_handler。函数 customNewHandler（第 9–13 行）打印一条错误消息（第 11 行），然后调用 abort（第 12 行）来终止程序。输出显示循环迭代了四次后 new 失败并调用了函数 customNewHandler。你的输出可能会因系统中的物理内存、可用于虚拟内存的磁盘空间以及编译器而有所不同。

```cpp
1   // Fig. 16.6: Fig16_06.cpp
2   // Demonstrating set_new_handler.
3   #include <iostream>
4   #include <new>       // set_new_handler function prototype
5   #include <cstdlib>   // abort function prototype
6   using namespace std;
7
8   // handle memory allocation failure
9   void customNewHandler()
10  {
11      cerr << "customNewHandler was called";
12      abort();
13  } // end function customNewHandler
14
15  // using set_new_handler to handle failed memory allocation
16  int main()
17  {
18      double *ptr[50];
19
20      // specify that customNewHandler should be called on
21      // memory allocation failure
22      set_new_handler( customNewHandler );
```

图 16.6 | set_new_handler 指定在 new 失败时要调用的函数。（第 1 部分，共 2 部分。）

