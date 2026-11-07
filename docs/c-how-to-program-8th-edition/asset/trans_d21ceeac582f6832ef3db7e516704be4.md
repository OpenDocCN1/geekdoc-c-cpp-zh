

> **错误预防提示 7.2**
> 
> 在第一章中，我们将看到如何开发一个表示“智能数组”的类，它会在运行时检查所有下标引用是否在边界内。使用这样的智能数据类型有助于消除错误。

## 7.4.8 静态局部数组与自动局部数组

第6章讨论了存储类别说明符 `static`。函数定义中的静态局部变量在程序运行期间存在，但仅在函数体内可见。

> **性能提示 7.1**
> 
> 我们可以将 `static` 应用于局部数组声明，这样每次程序调用函数时不会创建和初始化该数组，每次函数终止时也不会销毁它。这可以提高性能，尤其是在使用大型数组时。

程序在首次遇到静态局部数组的声明时对其进行初始化。如果你没有显式初始化静态数组，那么当数组被创建时，编译器会将数组的每个元素初始化为零。回想一下，C++ 不会对自动变量执行这种默认初始化。

图 7.12 演示了带有静态局部数组（第26行）的函数 `staticArrayInit`（第23–39行）以及带有自动局部数组（第45行）的函数 `automaticArrayInit`（第42–58行）。

```cpp
// Fig. 7.12: fig07_12.cpp
// Static arrays are initialized to zero.
#include <iostream>
using namespace std;

void staticArrayInit( void ); // function prototype
void automaticArrayInit( void ); // function prototype
const int arraySize = 3;

int main()
{
   cout << "First call to each function:\n";
   staticArrayInit();
   automaticArrayInit();

   cout << "\n\nSecond call to each function:\n";
   staticArrayInit();
   automaticArrayInit();
   cout << endl;
} // end main

// function to demonstrate a static local array
void staticArrayInit( void )
{
   // initializes elements to 0 first time function is called
   static int array1[ arraySize ]; // static local array

   // output contents of array1
   for ( int i = 0; i < arraySize; ++i )
      cout << "array1[" << i << "] = " << array1[ i ] << " ";

   cout << "\nValues on exiting staticArrayInit:\n";

   // modify and output contents of array1
   for ( int j = 0; j < arraySize; ++j )
      cout << "array1[" << j << "] = " << ( array1[ j ] += 5 ) << " ";
} // end function staticArrayInit

// function to demonstrate an automatic local array
void automaticArrayInit( void )
{
   // initializes elements each time function is called
   int array2[ arraySize ] = { 1, 2, 3 }; // automatic local array

   cout << "\n\nValues on entering automaticArrayInit:\n";

   // output contents of array2
   for ( int i = 0; i < arraySize; ++i )
      cout << "array2[" << i << "] = " << array2[ i ] << " ";

   cout << "\nValues on exiting automaticArrayInit:\n";

   // modify and output contents of array2
   for ( int j = 0; j < arraySize; ++j )
      cout << "array2[" << j << "] = " << ( array2[ j ] += 5 ) << " ";
} // end function automaticArrayInit
```

**图 7.12** | 静态数组初始化与自动数组初始化。（第1部分，共2部分。）

```text
First call to each function:

Values on entering staticArrayInit:
array1[0] = 0  array1[1] = 0  array1[2] = 0
Values on exiting staticArrayInit:
array1[0] = 5  array1[1] = 5  array1[2] = 5

Values on entering automaticArrayInit:
array2[0] = 1  array2[1] = 2  array2[2] = 3
Values on exiting automaticArrayInit:
array2[0] = 6  array2[1] = 7  array2[2] = 8

Second call to each function:

Values on entering staticArrayInit:
array1[0] = 5  array1[1] = 5  array1[2] = 5
Values on exiting staticArrayInit:
array1[0] = 10  array1[1] = 10  array1[2] = 10

Values on entering automaticArrayInit:
array2[0] = 1  array2[1] = 2  array2[2] = 3
Values on exiting automaticArrayInit:
array2[0] = 6  array2[1] = 7  array2[2] = 8
```

**图 7.12** | 静态数组初始化与自动数组初始化。（第2部分，共2部分。）

函数 `staticArrayInit` 被调用了两次（第13行和第17行）。编译器在第一次调用函数时将静态局部数组初始化为零。该函数打印数组，将每个元素加上5，然后再次打印数组。当第二次调用该函数时，静态数组中包含了第一次函数调用期间存储的修改后的值。函数 `automaticArrayInit` 也被调用了两次（第14行和第18行）。自动局部数组的元素在第45行被初始化为值 1、2 和 3。该函数打印数组，将每个元素加上5，然后再次打印数组。当第二次调用该函数时，数组元素被重新初始化为 1、2 和 3。该数组具有自动存储类别，因此每次调用 `automaticArrayInit` 时数组都会被重新创建并重新初始化。

> **常见编程错误 7.6**
> 
> *假设函数局部静态数组的元素在每次调用函数时都会被初始化，可能会导致程序中的逻辑错误。*

## 7.5 向函数传递数组

要将数组参数传递给函数，请指定不带任何方括号的数组名称。例如，如果数组 `hourlyTemperatures` 已声明为

```cpp
int hourlyTemperatures[ 24 ];
```

则函数调用

```cpp
modifyArray( hourlyTemperatures, 24 );
```

将数组 `hourlyTemperatures` 及其大小传递给函数 `modifyArray`。当向函数传递数组时，通常也会传递数组大小，以便函数能够处理数组中特定数量的元素。否则，我们需要将此信息构建到被调用的函数本身中，或者更糟糕的是，将数组大小放在全局变量中。在第7.11节中，当我们介绍 C++ 标准库类模板 `vector` 来表示一种更健壮的数组类型时，你会看到 `vector` 的大小是内置的——每个 `vector` 对象“知道”自己的大小，可以通过调用 `vector` 对象的 `size` 成员函数来获得。因此，当我们将 `vector` 对象传递给函数时，不必将 `vector` 的大小作为参数传递。

C++ 按引用将数组传递给函数——被调用的函数可以修改调用者原始数组中的元素值。数组名称的值是数组第一个元素在计算机内存中的地址。由于传递了数组的起始地址，被调用的函数确切地知道数组在内存中的存储位置。因此，当被调用的函数在其函数体中修改数组元素时，它修改的是数组中位于其原始内存位置的实际元素。

> **性能提示 7.2**
> 
> *按引用传递数组在性能方面是有意义的。按值传递需要复制每个元素。对于大型且频繁传递的数组，这将非常耗时，并且需要大量的存储空间来存储数组元素的副本。*

> **软件工程观察 7.2**
> 
> *可以通过将数组作为类的数据成员嵌入，并传递该类的对象（默认为按值传递）来按值传递数组。*

尽管整个数组是按引用传递的，但单个数组元素与简单变量一样是按值传递的。要将数组元素传递给函数，请在函数调用中使用数组元素的下标名称作为参数。在第6章中，我们展示了如何使用引用按引用传递单个变量和数组元素——在第8章中，我们将展示如何使用指针按引用传递它们。

为了使函数通过函数调用接收数组，函数的参数列表必须指定该函数期望接收一个数组。例如，函数 `modifyArray` 的函数头可以写成

```cpp
void modifyArray( int b[], int arraySize )
```

这表明 `modifyArray` 期望在参数 `b` 中接收整数数组的地址，并在参数 `arraySize` 中接收数组元素的数量。数组的大小在数组方括号中不是必需的。如果包含它，编译器会忽略它；因此，任意大小的数组都可以传递给函数。C++ 按引用将数组传递给函数——当被调用的函数使用数组名称 `b` 时，它引用的是调用者中的实际数组（即本节开头讨论的数组 `hourlyTemperatures`）。

请注意 `modifyArray` 函数原型的奇怪外观

```cpp
void modifyArray( int [], int );
```

这个原型本来可以写成（出于文档目的）

```cpp
void modifyArray( int anyArrayName[], int anyVariableName );
```

但正如我们在第3章中学到的，C++ 编译器会忽略原型中的变量名称。请记住，原型告诉编译器参数的数量和每个参数的类型（按参数预期出现的顺序）。

图 7.13 中的程序演示了传递整个数组与传递数组元素之间的区别。第19–20行打印整数数组 `a` 的五个原始元素。第25行将 `a` 及其大小传递给函数 `modifyArray`（第40–45行），该函数通过参数 `b` 将 `a` 的每个元素乘以2。然后，第29–30行在 `main` 中再次打印数组 `a`。如输出所示，`a` 的元素确实被 `modifyArray` 修改了。接下来，第33行打印 `a[3]` 的值，然后第35行将元素 `a[3]` 传递给函数 `modifyElement`（第49–53行），该函数将其参数乘以2并打印新值。当第36行在 `main` 中再次打印 `a[3]` 时，该值没有被修改，因为单个数组元素是按值传递的。

```cpp
// Fig. 7.13: fig07_13.cpp
// Passing arrays and individual array elements to functions.
#include <iostream>
#include <iomanip>
using namespace std;

void modifyArray( int [], int ); // appears strange; array and size
void modifyElement( int ); // receive array element value

int main()
{
```

**图 7.13** | 向函数传递数组和单个数组元素。（第1部分，共2部分。）

