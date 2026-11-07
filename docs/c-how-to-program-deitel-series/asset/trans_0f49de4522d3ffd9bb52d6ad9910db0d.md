

```cpp
// Fig. 10.12: fig10_12.cpp
// Single-argument constructors and implicit conversions.
#include <iostream>
#include "Array.h"
using namespace std;

void outputArray( const Array & ); // prototype

int main()
{
   Array integers1( 7 ); // 7-element Array
   outputArray( integers1 ); // output Array integers1
   outputArray( 3 ); // convert 3 to an Array and output Array's contents
} // end main

// print Array contents
void outputArray( const Array &arrayToOutput )
{
   cout << "The Array received has " << arrayToOutput.getSize()
        << " elements. The contents are:\n" << arrayToOutput << endl;
} // end outputArray
```

```
The Array received has 7 elements. The contents are:
      0       0       0       0       0       0       0

The Array received has 3 elements. The contents are:
      0       0       0
```

**图 10.12** | 单参数构造函数与隐式转换。

## 使用单参数构造函数阻止隐式转换

我们一直让每个单参数构造函数都以关键字 `explicit` 开头，原因是为了在不应允许隐式转换时，抑制通过转换构造函数进行的隐式转换。声明为 `explicit` 的构造函数不能用于隐式转换。在图 10.13 的示例中，我们使用了图 10.10 中 Array.h 的原始版本，其中第 14 行的单参数构造函数声明中包含关键字 `explicit`。

```cpp
explicit Array( int = 10 ); // default constructor
```

图 10.13 给出了图 10.12 中程序的一个稍作修改的版本。编译图 10.13 中的程序时，编译器会产生一条错误消息，指出第 13 行传递给 `outputArray` 的整数值无法转换为 `const Array &`。编译器错误消息（来自 Visual C++ 5）显示在输出窗口中。第 14 行演示了如何使用 explicit 构造函数创建一个包含 3 个元素的临时 Array 对象，并将其传递给函数 `outputArray`。

![](img/b42ba5cd262b1358d16610173f975e4d_504_0.png)

### 防错提示 10.4

除非单参数构造函数有意用作转换构造函数，否则始终在其上使用 `explicit` 关键字。

在这种情况下，它应该是一个 const 成员函数，因为获取子字符串不应修改原始 String 对象。

假设 string1 是一个包含字符串 "AEIOU" 的 String 对象。当编译器遇到表达式 `string1(2, 3)` 时，会生成成员函数调用

```
string1.operator()( 2, 3 )
```

该调用返回一个包含 "IOU" 的 String。

函数调用运算符的另一个可能用途是提供另一种数组下标表示法。与其使用 C++ 的双方括号表示法（例如 chessBoard[row][column]），你可能更希望重载函数调用运算符，以支持 chessBoard(row, column) 这种表示法，其中 chessBoard 是修改后的二维 Array 类的对象。练习 10.7 要求你构建这个类。函数调用运算符的主要用途是定义函数对象，我们将在第 16 章讨论。

## 10.15 小结

在本章中，你学习了如何重载运算符以用于类对象。我们演示了标准 C++ String 类，它大量使用重载运算符来创建一个健壮、可复用的类，从而取代 C 字符串。接下来，我们讨论了 C++ 标准对重载运算符的若干限制。然后，我们展示了一个 PhoneNumber 类，它重载了 << 和 >> 运算符，以方便输出和输入电话号码。你还看到了一个 Date 类，它重载了前缀和后缀自增（++）运算符，并且我们展示了区分自增（++）运算符前缀和后缀版本所需的特殊语法。

接下来，我们介绍了动态内存管理的概念。你了解到可以使用 new 和 delete 运算符分别动态创建和销毁对象。然后，我们介绍了一个综合性的 Array 类案例研究，它使用重载运算符和其他能力来解决基于指针的数组的各种问题。这个案例研究帮助你真正理解类和对象技术的本质——设计、使用和复用有价值的类。作为这个类的一部分，你看到了重载的流插入、流提取、赋值、相等和下标运算符。

你学习了将重载运算符实现为成员函数或非成员函数的原因。本章最后讨论了类型（包括类类型）之间的转换、单参数构造函数定义的某些隐式转换所带来的问题，以及如何通过使用 explicit 构造函数来防止这些问题。

在下一章中，我们将继续讨论类，介绍一种称为继承的软件复用形式。我们将看到，当多个类共享公共属性和行为时，可以在一个公共的“基类”中定义这些属性和行为，并将这些能力“继承”到新的类定义中，从而使你能够用最少的代码创建新类。

## 摘要

### 10.1 节 引言

- C++ 使你可以重载大多数运算符，使其对使用它们的上下文敏感——编译器会根据操作数的类型生成相应的代码。

DoubleSubscriptedArray 可以用作左值，并返回 int。该类还应提供以下运算符：==、!=、=、<<（用于按行和列格式输出 DoubleSubscriptedArray）以及 >>（用于输入整个 DoubleSubscriptedArray 的内容）。

## **10.8（Complex 类）**

考虑图 10.14–图 10.16 中所示的 Complex 类。该类支持对所谓的*复数*进行运算。这些数是形如 `realPart + imaginaryPart * i` 的数，其中 `i` 的值为

\[
\sqrt{-1}
\]

- a) 修改该类，通过重载的 `>>` 和 `<<` 运算符分别支持复数的输入和输出（应从类中移除 print 函数）。
- b) 重载乘法运算符，支持按代数方式实现两个复数的乘法。
- c) 重载 `==` 和 `!=` 运算符以支持复数的比较。

完成此练习后，你或许想阅读标准库中的 complex 类（来自头文件 `<complex>`）。

```cpp
// Fig. 10.14: Complex.h
// Complex class definition.
#ifndef COMPLEX_H
#define COMPLEX_H

class Complex
{
public:
   explicit Complex( double = 0.0, double = 0.0 ); // constructor
   Complex operator+( const Complex & ) const; // addition
   Complex operator-( const Complex & ) const; // subtraction
   void print() const; // output
private:
   double real; // real part
   double imaginary; // imaginary part
}; // end class Complex

#endif
```

**图 10.14** | *Complex 类定义。*

```cpp
// Fig. 10.15: Complex.cpp
// Complex class member-function definitions.
#include <iostream>
#include "Complex.h" // Complex class definition
using namespace std;

// Constructor
Complex::Complex( double realPart, double imaginaryPart )
   : real( realPart ),
     imaginary( imaginaryPart )
{
   // empty body
} // end Complex constructor

// addition operator
Complex Complex::operator+ ( const Complex &operand2 ) const
{
   return Complex( real + operand2.real,
                   imaginary + operand2.imaginary );
} // end function operator+

// subtraction operator
Complex Complex::operator- ( const Complex &operand2 ) const
{
   return Complex( real - operand2.real,
                   imaginary - operand2.imaginary );
} // end function operator-

// display a Complex object in the form: (a, b)
void Complex::print() const
{
   cout << '(' << real << ", " << imaginary << ')';
} // end function print
```

**图 10.15** | *Complex 类成员函数定义。*

```cpp
// Fig. 10.16: fig10_16.cpp
// Complex class test program.
#include <iostream>
#include "Complex.h"
using namespace std;

int main()
{
   Complex x;
   Complex y( 4.3, 8.2 );
   Complex z( 3.3, 1.1 );

   cout << "x: ";
   x.print();
   cout << "\ny: ";
   y.print();
   cout << "\nz: ";
   z.print();

   x = y + z;
   cout << "\n\nx = y + z:" << endl;
   x.print();
   cout << " ";
   y.print();
   cout << " ";
   z.print();

   x = y - z;
   cout << "\n\nx = y - z:" << endl;
   x.print();
   cout << " ";
   y.print();
   cout << " ";
   z.print();
   cout << endl;
} // end main
```

**图 10.16** | *Complex 类测试程序。（第 1 部分，共 2 部分。）*

