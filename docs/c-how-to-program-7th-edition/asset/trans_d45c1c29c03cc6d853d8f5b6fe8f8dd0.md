
像 ! 这样的一元运算符可以以两种不同方式重载为带一个参数的全局函数——要么参数是对象（这需要复制该对象，因此函数的副作用不会作用于原对象），要么参数是对对象的引用（不复制原对象，因此该函数的所有副作用都会作用于原对象）。如果 s 是 String 类对象（或对 String 类对象的引用），那么 !s 会被视为已经编写了调用 operator!(s)，从而调用声明如下的全局 operator! 函数：

```cpp
bool operator!( const String & );
```

## 11.7 重载二元运算符

二元运算符可以重载为带一个参数的非静态成员函数，或重载为带两个参数的全局函数（其中一个参数必须是类对象或对类对象的引用）。

本章后面，我们将重载 < 以比较两个 String 对象。当把二元运算符 < 重载为 String 类的带一个参数的非静态成员函数时，如果 y 和 z 是 String 类对象，那么 y < z 会被视为已经编写了 y.operator<(z)，从而调用下面声明的 operator< 成员函数

```cpp
class String
{
public:
    bool operator<( const String & ) const;

}; // end class String
```

作为全局函数，二元运算符 < 必须接受两个参数——其中一个必须是该类的对象（或对对象的引用）。如果 y 和 z 是 String 类对象或对 String 类对象的引用，那么 y < z 会被视为程序中已经编写了调用 operator<(y, z)，从而调用声明如下的全局函数 operator<：

```cpp
bool operator<( const String &, const String & );
```

## 11.8 动态内存管理

标准 C++ 数组数据结构一旦创建，其大小就是固定的。大小在编译时用常量指定。有时在执行时动态确定数组的大小并随后创建该数组是很有用的。C++ 使你能够在程序中控制对象以及任何内置类型或用户定义类型的数组的内存分配和释放。这称为动态内存管理，通过运算符 new 和 delete 来执行。

你可以使用 new 运算符在执行时动态分配（即预留）保存对象或数组所需的确切内存量。对象或数组创建在自由存储区（也称为堆）中——这是分配给每个程序用于存储动态分配对象的内存区域。一旦在自由存储区中分配了内存，就可以通过 operator new 返回的指针访问它。当你不再需要该内存时，可以使用 delete 运算符释放（即归还）该内存，将其返回给自由存储区，之后这些内存可被将来的 new 操作重用。

（例如，char 被初始化为空字符 `'\0'`）。虽然数组名是指向数组第一个元素的指针，但以下写法对于动态分配的内存是不允许的：

```cpp
int gradesArray[] = new int[ 10 ];
```

### 使用 `delete []` 释放动态分配的数组

要释放 gradesArray 所指向的内存，请使用语句

```cpp
delete [] gradesArray;
```

如果该指针指向对象数组，则该语句首先对数组中的每个对象调用析构函数，然后释放内存。如果前面的语句没有包含方括号（[]）而 gradesArray 指向对象数组，则结果是未定义的。一些编译器只对数组中的第一个对象调用析构函数。对空指针（即值为 0 的指针）使用 delete 没有效果。

> **常见编程错误 11.6**
> 
> *对对象数组使用 `delete` 而不是 `delete []` 可能导致运行时逻辑错误。为确保数组中的每个对象都收到析构函数调用，请始终使用运算符 `delete []` 删除作为数组分配的内存。同样，请始终使用运算符 `delete` 删除作为单个元素分配的内存——使用运算符 `delete []` 删除单个对象的结果是未定义的。*

## 11.9 案例研究：Array 类

我们在第 7 章讨论了数组。数组不过是指向内存中某个空间的指针。基于指针的数组有许多问题，包括：

- 程序很容易“走出”数组的任一端，因为 C++ 不检查下标是否超出数组范围（尽管你仍然可以显式地这样做）。
- 大小为 *n* 的数组必须将其元素编号为 0，…，*n* – 1；不允许使用其他下标范围。
- 整个数组不能一次输入或输出；每个数组元素必须单独读取或写入（除非该数组是以空字符结尾的 C 字符串）。
- 两个数组不能用相等或关系运算符进行有意义的比较（因为数组名只是指向数组在内存中开始位置的指针，而两个数组总是位于不同的内存位置）。
- 当数组传递给设计用于处理任意大小数组的通用函数时，必须将数组的大小作为附加参数传递。
- 一个数组不能使用赋值运算符赋给另一个数组（因为数组名是 const 指针，而*常量*指针不能用于赋值运算符的左侧）。

C++ 提供了通过类和运算符重载来实现更稳健的数组功能的方法。你可以开发一个优于“原始”数组的数组类。在本例中，我们创建一个功能强大的 `Array` 类，它执行范围检查以确保下标保持在 `Array` 的边界内。该类允许使用赋值运算符将一个数组对象赋给另一个数组对象。Array 对象知道自身的大小，因此不需要将大小单独传递给接收 Array 参数的函数。可以使用流提取运算符和流插入运算符分别输入或输出整个 Array。可以使用相等运算符 == 和 != 比较 Array。回想一下，C++ 标准库类模板 vector（在第 7 章介绍）也提供了许多这些功能。第 22 章详细解释了类模板 vector。

这个示例将加深你对数据抽象的理解。类开发是一项有趣、富有创造性且具有智力挑战性的活动——始终以“打造有价值的类”为目标。图 11.6–11.8 的程序演示了 Array 类及其重载运算符。首先我们逐步讲解 main（图 11.8），然后考虑类定义（图 11.6）及其每个成员函数定义（图 11.7）。

```cpp
// Fig. 11.6: Array.h
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
   Array( int = 10 ); // default constructor
   Array( const Array & ); // copy constructor
   ~Array(); // destructor
   int getSize() const; // return size

   const Array &operator=( const Array & ); // assignment operator
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

图 11.6  |  带重载运算符的 Array 类定义。
