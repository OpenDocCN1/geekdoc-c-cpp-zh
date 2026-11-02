
如果一个对象拥有成员对象，并且在外层对象完全构造之前抛出了异常，那么对于在异常发生之前已经构造完成的成员对象，将执行其析构函数。如果异常发生时对象数组只被部分构造，那么只会调用数组中已构造对象的析构函数。

> **错误预防提示 22.6**
> *当在 new 表达式中创建的对象，其构造函数抛出异常时，为该对象动态分配的内存会被释放。*

> **错误预防提示 22.7**
> *如果在初始化对象时发生问题，构造函数应抛出异常。在抛出异常之前，构造函数应释放其动态分配的任何内存。*

### 初始化局部对象以获取资源

异常可能会阻止通常用于释放资源（如内存或文件）的代码执行，从而造成资源泄漏，使其他程序无法获取该资源。解决此问题的一种技术是初始化一个局部对象来获取资源。当异常发生时，该对象的析构函数将被调用，并可以释放该资源。

## 22.7 异常与继承

各种异常类可以派生自一个共同的基类，正如我们在 22.2 节中讨论的那样：当时我们创建了类 DivideByZeroException，将其作为类 exception 的派生类。如果某个 catch 处理程序捕获的是对基类类型异常对象的引用，那么它也可以捕获对从该基类公有派生出的所有类的对象的引用——这允许对相关异常进行多态处理。

> **错误预防提示 22.8**
> *将继承与异常结合使用，使异常处理程序能够以简洁的表示法捕获相关错误。一种方法是分别捕获每一种指向派生类异常对象的引用类型，但更简洁的方法是改为捕获指向基类异常对象的指针或引用。此外，分别捕获指向派生类异常对象的指针或引用容易出错，尤其是当你忘记显式测试一种或多种派生类引用类型时。*

## 22.8 处理 new 失败

当运算符 new 失败时，它会抛出 bad_alloc 异常（定义在头文件 <new> 中）。在本节中，我们给出两个 new 失败的示例。第一个示例使用当 new 失败时抛出 bad_alloc 异常的 new 版本。第二个示例使用函数 set_new_handler 来处理 new 失败。[注意：图 22.5–22.6 中的示例会分配大量动态内存，这可能导致你的计算机变得迟缓。]

### new 在失败时抛出 bad_alloc

图 22.5 演示了 new 在无法分配所请求的内存时隐式抛出 bad_alloc。try 块内的 for 语句（第 16–20 行）应循环 50 次，并且在每一轮中分配一个包含 50,000,000 个 double 值的数组。如果 new 失败并抛出 bad_alloc 异常，循环终止，程序继续执行第 22 行，在那里 catch 处理程序捕获并处理该异常。第 24–25 行打印消息 "Exception occurred: "，随后是函数 what 的基类异常版本返回的消息（即由实现定义的、特定于异常的消息，例如 Microsoft Visual C++ 中的 "bad allocation"）。输出表明，程序在 new 失败并抛出 bad_alloc 异常之前只执行了四次循环迭代。根据你系统中的物理内存、可用于虚拟内存的磁盘空间以及所使用的编译器，你的输出可能有所不同。

```cpp
// Fig. 22.5: fig22_05.cpp
// Demonstrating standard new throwing bad_alloc when memory
// cannot be allocated.
#include <iostream>
#include <new> // bad_alloc class is defined here
using namespace std;

int main()
{
   double *ptr[ 50 ];

   // aim each ptr[i] at a big block of memory
   try
   {
      // allocate memory for ptr[ i ]; new throws bad_alloc on failure
      for ( size_t i = 0; i < 50; ++i )
      {
         ptr[ i ] = new double[ 50000000 ]; // may throw exception
         cout << "ptr[" << i << "] points to 50,000,000 new doubles\n";
      } // end for
   } // end try
   catch ( bad_alloc &memoryAllocationException )
   {
      cerr << "Exception occurred: "
           << memoryAllocationException.what() << endl;
   } // end catch
} // end main
```

```text
ptr[0] points to 50,000,000 new doubles
ptr[1] points to 50,000,000 new doubles
ptr[2] points to 50,000,000 new doubles
ptr[3] points to 50,000,000 new doubles
Exception occurred: bad allocation
```

**图 22.5** | new 在失败时抛出 bad_alloc。

### new 在失败时返回 nullptr

C++ 标准规定，程序员可以使用一个较旧版本的 new，它在失败时返回 `nullptr`。为此，头文件 `<new>` 定义了运算符 new（类型为 `nothrow_t`），其用法如下：

```cpp
double *ptr = new( nothrow ) double[ 50000000 ];
```

前面的语句使用不抛出 `bad_alloc` 异常（即 `nothrow`）的 new 版本，来分配一个包含 50,000,000 个 int 的数组。

![](img/d0d3b7423c2d9e5650be79209ea1885d_895_0.png)

### 使用函数 set_new_handler 处理 new 失败

处理 new 失败的另一个特性是函数 `set_new_handler`（原型位于标准头文件 `<new>` 中）。该函数接受一个指向函数的指针作为参数，该函数不接受任何参数并返回 void。这个指针指向在 new 失败时将被调用的函数。这为你提供了一种统一的方法来处理所有 new 失败，无论失败发生在程序中的何处。一旦 `set_new_handler` 在程序中注册了新的处理程序，运算符 new 在失败时就不会抛出 bad_alloc；相反，它会将错误处理推迟到 new 处理函数。

如果 new 成功分配内存，它会返回指向该内存的指针。如果 new 分配内存失败，并且 `set_new_handler` 没有注册 new 处理函数，那么 new 会抛出 `bad_alloc` 异常。如果 new 分配内存失败，并且已经注册了 new 处理函数，那么会调用该 new 处理函数。new 处理函数应执行以下任务之一：

- 1. 通过删除其他动态分配的内存（或告诉用户关闭其他应用程序）来提供更多可用内存，并返回到运算符 new 以再次尝试分配内存。
- 2. 抛出类型为 `bad_alloc` 的异常。
- 3. 调用函数 `abort` 或 `exit`（二者都位于头文件 `<cstdlib>` 中）来终止程序。这些内容已在 17.7 节中介绍。

图 22.6 演示了 `set_new_handler`。函数 `customNewHandler`（第 9–13 行）打印一条错误消息（第 11 行），然后调用 `abort`（第 12 行）来终止程序。输出表明，在 new 失败并调用函数 `customNewHandler` 之前，循环迭代了四次。根据你系统中的物理内存、可用于虚拟内存的磁盘空间以及你的编译器，你的输出可能有所不同。

```cpp
1 // Fig. 22.6: fig22_06.cpp
2 // Demonstrating set_new_handler
3 #include <iostream>
4 #include <new> // set_new_handler function prototype
5 #include <cstdlib> // abort function prototype
6 using namespace std;
7
8 // handle memory allocation failure
9 void customNewHandler()
10 {
11     cerr << "customNewHandler was called";
12     abort();
13 } // end function customNewHandler
14
15 // using set_new_handler to handle failed memory allocation
16 int main()
17 {
18     double *ptr[ 50 ];
19
20     // specify that customNewHandler should be called on
21     // memory allocation failure
22     set_new_handler( customNewHandler );
23
24     // aim each ptr[i] at a big block of memory; customNewHandler will be
25     // called on failed memory allocation
26     for ( size_t i = 0; i < 50; ++i )
27     {
28         ptr[ i ] = new double[ 50000000 ]; // may throw exception
29         cout << "ptr[" << i << "] points to 50,000,000 new doubles\n";
30     } // end for
31 } // end main
```

**图 22.6** | `set_new_handler` 指定 new 失败时要调用的函数。（第 1 部分，共 2 部分。）

```text
ptr[0] points to 50,000,000 new doubles
ptr[1] points to 50,000,000 new doubles
ptr[2] points to 50,000,000 new doubles
ptr[3] points to 50,000,000 new doubles
customNewHandler was called
```

**图 22.6** | `set_new_handler` 指定 new 失败时要调用的函数。（第 2 部分，共 2 部分。）

## 22.9 类 unique_ptr 与动态内存分配

一种常见的编程做法是：分配动态内存，将该内存的地址赋给一个指针，使用该指针操作内存，并在不再需要该内存时用 delete 释放它。如果在成功分配内存之后、delete 语句执行之前发生异常，就可能发生内存泄漏。C++11 在头文件 <memory> 中提供了类模板 unique_ptr 来处理这种情况。

类 unique_ptr 的对象维护一个指向动态分配内存的指针。当调用 unique_ptr 对象的析构函数时（例如，当 unique_ptr 对象离开作用域时），它会对其指针数据成员执行 delete 操作。类模板 unique_ptr 提供了重载运算符 * 和 ->，因此 unique_ptr 对象可以像普通指针变量一样使用。图 22.9 演示了一个 unique_ptr 对象，它指向一个动态分配的 Integer 类对象（图 22.7–22.8）。

```cpp
1 // Fig. 22.7: Integer.h
2 // Integer class definition.
3
4 class Integer
5 {
```

**图 22.7** | Integer 类定义。（第 1 部分，共 2 部分。）
