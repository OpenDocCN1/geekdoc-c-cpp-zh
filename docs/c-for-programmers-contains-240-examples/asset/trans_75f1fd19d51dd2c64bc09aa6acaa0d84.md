

## new 在失败时返回 0

图 16.5 演示了 new 在分配请求内存失败时返回 0。行 13–24 中的 for 语句应循环 50 次，每次循环分配一个包含 50,000,000 个 double 值的数组（即 400,000,000 字节，因为 double 通常为 8 字节）。行 17 中的 if 语句测试每次 new 操作的结果，以确定 new 是否成功分配了内存。如果 new 失败并返回 0，行 19 打印错误消息，并且循环终止。[注：我们使用 Microsoft Visual C++ 6.0 运行此示例，因为 Microsoft Visual C++ 2005 在 new 失败时抛出 bad_alloc 异常而不是返回 0。]

输出显示程序仅执行了三次迭代后 new 就失败了，并且循环终止了。你的输出可能会因系统上可用的物理内存、用于虚拟内存的磁盘空间以及你使用的编译器而有所不同。

```
1  // Fig. 16.5: Fig16_05.cpp
2  // Demonstrating pre-standard new returning 0 when memory
3  // allocation fails.
4  #include <iostream>
5  using std::cerr;
6  using std::cout;
7
8  int main()
9  {
10     double *ptr[ 50 ];
11
12     // aim each ptr[i] at a big block of memory
13     for ( int i = 0; i < 50; i++ )
14     {
15         ptr[ i ] = new double[ 50000000 ]; // allocate big block
16
17         if ( ptr[ i ] == 0 ) // did new fail to allocate memory
18         {
19             cerr << "Memory allocation failed for ptr[" << i << "]\n";
20             break;
21         } // end if
22         else // successful memory allocation
23             cout << "ptr[" << i << "] points to 50,000,000 new doubles\n";
24     } // end for
25
26     return 0;
27 } // end main
```

ptr[0] points to 50,000,000 new doubles
ptr[1] points to 50,000,000 new doubles
ptr[2] points to 50,000,000 new doubles
Memory allocation failed for ptr[3]

Fig. 16.5 | Demonstrating pre-standard new returning 0 when memory allocation fails.

## new 在失败时抛出 bad_alloc

图 16.6 演示了 new 在分配请求内存失败时抛出 bad_alloc。try 块内部的 for 语句（行 20–24）应循环 50 次，每次循环分配一个包含 50,000,000 个 double 值的数组。如果 new 失败并抛出 bad_alloc 异常，循环终止，程序继续执行到行 28，catch 处理程序捕获并处理该异常。行 30–31 打印消息 "Exception occurred:"，随后打印函数 what 的基类异常版本返回的消息（即实现定义的异常特定消息，例如 Microsoft Visual C++ 2005 中的 "Allocation Failure"）。输出显示程序仅执行了三次循环迭代后 new 就失败并抛出了 bad_alloc 异常。你的输出可能会因系统上可用的物理内存、用于虚拟内存的磁盘空间以及你使用的编译器而有所不同。

```
// Fig. 16.6: Fig16_06.cpp
// Demonstrating standard new throwing bad_alloc when memory
// cannot be allocated.
#include <iostream>
using std::cerr;
using std::cout;
using std::endl;

#include <new> // standard operator new
using std::bad_alloc;

int main()
{
    double *ptr[ 50 ];

    // aim each ptr[i] at a big block of memory
    try
    {
        // allocate memory for ptr[ i ]; new throws bad_alloc on failure
        for ( int i = 0; i < 50; i++ )
        {
            ptr[ i ] = new double[ 50000000 ]; // may throw exception
            cout << "ptr[" << i << "] points to 50,000,000 new doubles\n";
        } // end for
    } // end try

    // handle bad_alloc exception
    catch ( bad_alloc &memoryAllocationException )
    {
        cerr << "Exception occurred: "
             << memoryAllocationException.what() << endl;
    } // end catch

    return 0;
} // end main
```

ptr[0] points to 50,000,000 new doubles
ptr[1] points to 50,000,000 new doubles
ptr[2] points to 50,000,000 new doubles
Exception occurred: bad allocation

Fig. 16.6 | new throwing bad_alloc on failure.

C++ 标准规定符合标准的编译器仍可继续使用在失败时返回 0 的版本的 new。为此，头文件 <new> 定义了对象 nothrow（类型为 nothrow_t），用法如下：

```
double *ptr = new( nothrow ) double[ 50000000 ];
```

前述语句使用不抛出 bad_alloc 异常的版本的 new（即 nothrow）来分配一个包含 50,000,000 个 doubles 的数组。

## 软件工程观察 16.8

> 为了使程序更健壮，请使用在失败时抛出 bad_alloc 异常的版本的 new。

## 使用函数 set_new_handler 处理 new 失败

处理 new 失败的另一个特性是函数 set_new_handler（原型在标准头文件 <new> 中声明）。该函数以其参数作为指向一个不带参数且返回 void 的函数的指针。此指针指向在 new 失败时将被调用的函数。这为你提供了处理程序中所有 new 失败的统一方法，无论失败发生在程序的何处。一旦 set_new_handler 在程序中注册了新的处理程序，operator new 在失败时不会抛出 bad_alloc；相反，它将错误处理推迟到 new-handler 函数。

如果 new 成功分配内存，它将返回指向该内存的指针。如果 new 失败分配内存且 set_new_handler 未注册 new-handler 函数，new 将抛出 bad_alloc 异常。如果 new 失败分配内存且已注册 new-handler 函数，则会调用 new-handler 函数。C++ 标准规定 new-handler 函数应执行以下任务之一：

- 1. 通过删除其他动态分配的内存（或告知用户关闭其他应用程序）来提供更多内存，然后返回到 operator new 再次尝试分配内存。
- 2. 抛出类型为 bad_alloc 的异常。
- 3. 调用函数 abort 或 exit（均在头文件 <cstdlib> 中找到）以终止程序。

图 16.7 演示了 set_new_handler。函数 customNewHandler（行 14–18）打印错误消息（行 16），然后通过调用 abort（行 17）终止程序。输出显示程序仅执行了三次循环迭代后 new 就失败并调用了函数 customNewHandler。你的输出可能会因系统上可用的物理内存、用于虚拟内存的磁盘空间以及你用来编译程序的编译器而有所不同。

```
1  // Fig. 16.7: Fig16_07.cpp
2  // Demonstrating set_new_handler.
3  #include <iostream>
4  using std::cerr;
5  using std::cout;
```

Fig. 16.7 | set_new_handler specifying the function to call when new fails. (Part 1 of 2.)

```
#include <new> // standard operator new and set_new_handler
using std::set_new_handler;

#include <cstdlib> // abort function prototype
using std::abort;

// handle memory allocation failure
void customNewHandler()
{
    cerr << "customNewHandler was called";
    abort();
} // end function customNewHandler

// using set_new_handler to handle failed memory allocation
int main()
{
    double *ptr[ 50 ];

    // specify that customNewHandler should be called on
    // memory allocation failure
    set_new_handler( customNewHandler );

    // aim each ptr[i] at a big block of memory; customNewHandler will be
    // called on failed memory allocation
    for ( int i = 0; i < 50; i++ )
    {
        ptr[ i ] = new double[ 50000000 ]; // may throw exception
        cout << "ptr[" << i << "] points to 50,000,000 new doubles\n";
    } // end for

    return 0;
} // end main
```

```
ptr[0] points to 50,000,000 new doubles
ptr[1] points to 50,000,000 new doubles
ptr[2] points to 50,000,000 new doubles
customNewHandler was called
```

Fig. 16.7 | set_new_handler specifying the function to call when new fails. (Part 2 of 2.)

## 16.12 类 auto_ptr 和动态内存分配

一种常见的编程实践是分配动态内存，将该内存的地址赋给指针，使用指针操作内存，并在不再需要内存时使用 delete 释放内存。如果在成功分配内存后但在 delete 语句执行之前发生异常，可能会发生内存泄漏。C++ 标准在头文件 <memory> 中提供了类模板 auto_ptr 来处理这种情况。

auto_ptr 类的对象维护指向动态分配内存的指针。当 auto_ptr 对象析构函数被调用时（例如，当 auto_ptr 对象离开作用域时），它对其指针数据成员执行 delete 操作。类模板 auto_ptr 提供了重载的运算符 * 和 ->，因此 auto_ptr 对象可以被使用

