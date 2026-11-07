

### *使用现有数组内容的副本初始化新数组*

第 38 行实例化了第三个名为 integers3 的数组，并用数组 integers1 的副本对其进行初始化。这会调用类 Array 的复制构造函数，将 integers1 的元素复制到 integers3 中。我们稍后将详细讨论复制构造函数。也可以将第 38 行写成如下形式来调用复制构造函数：

```
Array integers3 = integers1;
```

前面语句中的等号*不是*赋值运算符。当等号出现在对象的声明中时，它调用该对象的构造函数。这种形式可用于向构造函数指定一个参数——具体来说，就是 `=` 符号右侧的值。

第 40–42 行输出 integers3 的大小，然后使用 Array 重载的流插入运算符输出 integers3 的内容，以确认复制构造函数正确设置了 integers3 的元素。

### *使用重载的赋值运算符*

第 46 行通过将 integers2 赋值给 integers1 来测试重载的赋值运算符（=）。第 48–49 行显示两个 Array 对象的内容，以确认赋值成功。integers1 最初包含 7 个整数，但被调整为包含 integers2 中 10 个元素的副本。正如我们将看到的，重载的赋值运算符以对客户端代码透明的方式执行此调整大小操作。

### *使用重载的相等运算符*

第 54 行使用重载的相等运算符（==）来确认在第 46 行赋值后，对象 integers1 和 integers2 确实相同。

### *使用重载的下标运算符*

第 58 行使用重载的下标运算符来引用 integers1[5]——integers1 中一个在范围内的元素。该下标名称用作 *rvalue*（右值）来打印存储在 integers1[5] 中的值。第 62 行将 integers1[5] 用作赋值语句左侧的可修改 *lvalue*（左值），为 integers1 的元素 5 赋予新值 1000。我们将看到，在运算符确认 5 是 integers1 的有效下标后，operator[] 返回一个引用，用作可修改的 *lvalue*。

第 69 行尝试将值 1000 赋给 integers1[15]——一个*超出范围*的元素。在此示例中，operator[] 确定该下标超出范围，并抛出 out_of_range 异常。

有趣的是，*数组下标运算符 []* 并不局限于仅用于数组；它还可以用于从其他类型的*容器*类中选择元素，例如链表、字符串和字典。此外，当定义了重载的 operator[] 函数时，*下标不再必须是整数*——字符、字符串，甚至用户定义类的对象也可以使用。在第 22 章中，我们讨论了允许使用字符串下标的 STL map 类。

## 11.10.2 Array 类定义

现在我们已经了解了该程序如何运行，让我们逐步浏览类头文件（图 11.10）。当我们在头文件中引用每个成员函数时，我们会在图 11.11 中讨论该函数的实现。在图 11.10 中，第 34–35 行表示类 Array 的私有数据成员。每个 Array 对象由一个 size 成员（指示 Array 中的元素数量）和一个 int 指针组成——该指针指向由 Array 对象管理的动态分配的基于指针的整数数组。

图 11.10 | 带有重载运算符的 Array 类定义。

```cpp
// Fig. 11.10: Array.h
// Array class definition with overloaded operators.
#ifndef ARRAY_H
#define ARRAY_H

#include <iostream>
using namespace std;

class Array
{
   friend ostream &operator<<( ostream &, const Array & );
   friend istream &operator>>( istream &, Array & );
public:
   Array( int = 10 );                 // default constructor
   Array( const Array & );             // copy constructor
   ~Array();                           // destructor
   int getSize() const;                // return size

   const Array operator=( const Array & ); // assignment operator
   bool operator==( const Array & ) const; // equality operator

   // inequality operator; returns opposite of == operator
   bool operator!=( const Array &right ) const
   {
      return !( *this == right ); // invokes Array::operator==
   } // end function operator!=

   // subscript operator for non-const objects returns modifiable lvalue
   int &operator[]( int );

   // subscript operator for const objects returns rvalue
   int operator[]( int ) const;

private:
   int size; // pointer-based array size
   int *ptr; // pointer to first element of pointer-based array
}; // end class Array

#endif
```

图 11.11 | Array 类成员函数和友元函数定义。（第 1 部分，共 4 部分。）

```cpp
// Fig 11.11: Array.cpp
// Array class member- and friend-function definitions.
#include <iostream>
#include <iomanip>
#include <cstdlib> // exit function prototype
#include "Array.h" // Array class definition

using namespace std;

// default constructor for class Array (default size 10)
Array::Array( int arraySize )
{
   // validate arraySize
   if ( arraySize > 0 )
      size = arraySize;
   else
      throw invalid_argument( "Array size must be greater than 0" );

   ptr = new int[ size ]; // create space for pointer-based array

   for ( int i = 0; i < size; ++i )
      ptr[ i ] = 0; // set each pointer-based array element
} // end Array default constructor

// copy constructor for class Array;
// must receive a reference to prevent infinite recursion
Array::Array( const Array &arrayToCopy )
   : size( arrayToCopy.size )
{
   ptr = new int[ size ]; // create space for pointer-based array

   for ( int i = 0; i < size; ++i )
      ptr[ i ] = arrayToCopy.ptr[ i ]; // copy into object
} // end Array copy constructor

// destructor for class Array
Array::~Array()
{
   delete [] ptr; // release pointer-based array space
} // end destructor

// return number of elements of Array
int Array::getSize() const
{
   return size; // number of elements in Array
} // end function getSize

// overloaded assignment operator;
// const return avoids: ( a1 = a2 ) = a3
const Array& Array::operator=( const Array &right )
{
   if ( &right != this ) // avoid self-assignment
   {
      // for Arrays of different sizes, deallocate original
      // left-side array, then allocate new left-side array
      if ( size != right.size )
      {
         delete [] ptr; // release space
         size = right.size; // resize this object
```

图 11.11 | Array 类成员函数和友元函数定义。（第 2 部分，共 4 部分。）

类 Array 的默认构造函数将 Array 的大小设置为 10 个元素。默认构造函数（定义于图 11.1 的第 10–22 行）验证参数并将其赋给数据成员 size，使用 new 为此数组的内部基于指针的表示获取内存，并将 new 返回的指针赋给数据成员 ptr。然后构造函数使用 for 语句将数组的所有元素设置为零。如果某些成员稍后读取，则 Array 类可以不初始化其成员；但这被认为是一种不良的编程实践。数组以及一般的对象，应该在创建时正确初始化。

### Array 复制构造函数

图 11.10 的第 15 行声明了一个复制构造函数（定义于图 11.11 的第 26–33 行），它通过复制现有 Array 对象来初始化一个 Array。必须小心进行此类复制，以避免两个 Array 对象指向同一块动态分配内存的陷阱。如果编译器允许为此类定义默认的复制构造函数，则默认的逐成员复制恰恰会导致此问题。每当需要对象的副本时，都会调用复制构造函数，例如：

- 按值将对象传递给函数
- 按值从函数返回对象
- 用同一类的另一个对象的副本初始化对象。

当实例化一个 Array 类的对象并用另一个 Array 类的对象初始化时，会在声明中调用复制构造函数，如图 11.9 中的第 38 行声明。

Array 的复制构造函数使用成员初始化器（图 11.11 的第 27 行）将初始化器 Array 的大小复制到数据成员 size 中，使用 new（第 29 行）为此 Array 的内部基于指针的表示获取内存，并将 new 返回的指针赋给数据成员 ptr。¹ 然后复制构造函数使用 for 语句将初始化器 Array 的所有元素复制到新的 Array 对象中。类的对象可以查看该类的任何其他对象的私有数据（使用指示要访问哪个对象的句柄）。

> **软件工程观察 11.2**
>
> 复制构造函数的参数应为 const 引用，以允许复制 const 对象。

![](img/bfd978e7e9b192bab46ec2a89e481263_513_0.png)

> **常见编程错误 11.3**
>
> 复制构造函数必须通过引用接收其参数，而不是按值。否则，复制构造函数调用会导致无限递归（致命的逻辑错误），因为按值接收对象需要复制构造函数制作参数对象的副本。回想一下，任何时候需要对象的副本时，都会调用类的复制构造函数。如果复制构造函数按值接收其参数，则复制构造函数将递归调用自身来制作其参数的副本。

![](img/bfd978e7e9b192bab46ec2a89e481263_513_1.png)

