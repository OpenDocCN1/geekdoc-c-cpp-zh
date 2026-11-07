

```cpp
private:
    std::array< short, digits > integer;
}; // end class HugeInt
#endif
```

*图 10.17 | HugeInt 类定义。（第2部分，共2部分）*

```cpp
// Fig. 10.18: HugeInt.cpp
// HugeInt member-function and friend-function definitions.
#include <cctype> // digit function prototype
#include "HugeInt.h" // HugeInt class definition
using namespace std;

// default constructor; conversion constructor that converts
// a long integer into a HugeInt object
HugeInt::HugeInt( long value )
{
   // initialize array to zero
   for ( short element = 0; element < digits; ++element )
      integer[ element ] = 0;

   // place digits of argument into array
   for ( size_t j = digits - 1; value != 0 && j >= 0; j-- )
   {
      integer[ j ] = value % 10;
      value /= 10;
   } // end for
} // end HugeInt default/conversion constructor

// conversion constructor that converts a character string
// representing a large integer into a HugeInt object
HugeInt::HugeInt( const string &number )
{
   // initialize array to zero
   for ( short element = 0; element < digits; ++element )
      integer[ element ] = 0;

   // place digits of argument into array
   size_t length = number.size();

   for ( size_t j = digits - 1, k = 0; j < digits; ++j, ++k )
   {
      if ( isdigit( number[ k ] ) ) // ensure that character is a digit
         integer[ j ] = number[ k ] - '0';
   } // end for
} // end HugeInt conversion constructor

// addition operator; HugeInt + HugeInt
HugeInt HugeInt::operator+( const HugeInt &op2 ) const
{
   HugeInt temp; // temporary result
   int carry = 0;

   for ( int i = digits - 1; i >= 0; i-- )
   {
      temp.integer[ i ] = integer[ i ] + op2.integer[ i ] + carry;

      // determine whether to carry a 1
      if ( temp.integer[ i ] > 9 )
      {
         temp.integer[ i ] %= 10;  // reduce to 0-9
         carry = 1;
      }
      else // no carry
         carry = 0;
   } // end for

   return temp;  // return copy of temporary object
} // end of function operator+

// addition operator; HugeInt + int
HugeInt HugeInt::operator+( int op2 ) const
{
   // convert op2 to a HugeInt, then invoke
   // operator+ for two HugeInt objects
   return *this + HugeInt( op2 );
} // end of function operator+

// addition operator;
// HugeInt + string that represents large integer value
HugeInt HugeInt::operator+( const string& op2 ) const
{
   // convert op2 to a HugeInt, then invoke
   // operator+ for two HugeInt objects
   return *this + HugeInt( op2 );
} // end of operator+

// overloaded output operator
ostream& operator<<( ostream& output, const HugeInt &num )
{
   int i;

   for ( i = 0; ( i < HugeInt::digits ) && ( 0 == num.integer[ i ] ); ++i )
      ; // skip leading zeros

   if ( i == HugeInt::digits )
      output << 0;
   else
      for ( ; i < HugeInt::digits; ++i )
         output << num.integer[ i ];

   return output;
} // end of function operator<<
```

*图 10.18 | HugeInt 成员函数和友元函数定义。（第1部分，共2部分）*
*（第2部分，共2部分）*

```cpp
// Fig. 10.19: fig10_19.cpp
// HugeInt test program.
#include <iostream>
#include "HugeInt.h"
using namespace std;

int main()
{
9   HugeInt n1( 7654321 );
10  HugeInt n2( 7891234 );
11  HugeInt n3( "9999999999999999999999999999" );
12  HugeInt n4( "1" );
13  HugeInt n5;
14
15  cout << "\nn1 is " << n1 << "\nn2 is " << n2
16       << "\nn3 is " << n3 << "\nn4 is " << n4
17       << "\nn5 is " << n5 << "\n\n";
18
19  n5 = n1 + n2;
20  cout << n1 << " + " << n2 << " = " << n5 << "\n\n";
21
22  cout << n3 << " + " << n4 << " = " << ( n3 + n4 ) << "\n\n";
23
24  n5 = n1 + 9;
25  cout << n1 << " + 9 = " << n5 << "\n\n";
26
27  n5 = n2 + "10000";
28  cout << n2 << " + " << "10000" << " = " << n5 << endl;
29 } // end main
```

```text
n1 is 7654321
n2 is 7891234
n3 is 9999999999999999999999999999
n4 is 1
n5 is 0

7654321 + 7891234 = 15545555

9999999999999999999999999999 + 1
= 10000000000000000000000000000

7654321 + 9 = 7654330

7891234 + 10000 = 7901234
```

*图 10.19 | HugeInt 测试程序。（第1部分，共2部分）*
*（第2部分，共2部分）*

**10.10（RationalNumber 类）** 创建一个 RationalNumber 类（分数），使其具备以下能力：

- a) 创建一个构造函数，该构造函数防止分数中的分母为0，约简或化简未化为最简形式的分数，并避免分母为负数。
- b) 为该类重载加法、减法、乘法和除法运算符。
- c) 为该类重载关系和相等性运算符。

**10.11（Polynomial 类）** 开发 Polynomial 类。Polynomial 的内部表示是一个项数组。每一项包含一个系数和一个指数，例如，项 `2x⁴` 的系数为2，指数为4。开发一个完整的类，包含适当的构造函数和析构函数，以及 set 和 get 函数。该类还应提供以下重载运算符能力：

- a) 重载加法运算符 (+)，实现两个 Polynomial 相加。
- b) 重载减法运算符 (-)，实现两个 Polynomial 相减。
- c) 重载赋值运算符，将一个 Polynomial 赋值给另一个。
- d) 重载乘法运算符 (*)，实现两个 Polynomial 相乘。
- e) 重载加法赋值运算符 (+=)、减法赋值运算符 (-=) 和乘法赋值运算符 (*=)。

## 11 面向对象编程：继承

> 除非你与他分割过遗产，否则不要说完全了解一个人。
>
> ——约翰·卡斯珀·拉瓦特

> 该方法是把所有与给定类相似的类的类定义为类的数量。
>
> ——伯特兰·罗素

> 从他人的书籍中汲取基本权威。
>
> ——威廉·莎士比亚

### 目标

在本章中，你将学习：

- 什么是继承，以及它如何促进软件重用。
- 基类和派生类的概念，以及它们之间的关系。
- 受保护成员访问说明符。
- 继承层次结构中构造函数和析构函数的用法。
- 在继承层次结构中，构造函数和析构函数被调用的顺序。
- `public`、`protected` 和 `private` 继承之间的区别。
- 使用继承来定制现有软件。

![](img/b42ba5cd262b1358d16610173f975e4d_517_0.png)

- 11.1 引言
- 11.2 基类和派生类
- 11.3 基类与派生类的关系
  - 11.3.1 创建和使用 CommissionEmployee 类
  - 11.3.2 不使用继承创建 BasePlusCommissionEmployee 类
  - 11.3.3 创建 CommissionEmployee–BasePlusCommissionEmployee 继承层次结构
  - 11.3.4 使用 protected 数据的 CommissionEmployee–BasePlusCommissionEmployee 继承层次结构
  - 11.3.5 使用 private 数据的 CommissionEmployee–BasePlusCommissionEmployee 继承层次结构
- 11.4 派生类中的构造函数和析构函数
- 11.5 public、protected 和 private 继承
- 11.6 继承的软件工程
- 11.7 总结

*总结 | 自测练习 | 自测练习答案 | 练习*

### 11.1 引言

本章继续讨论面向对象编程（OOP），引入*继承*——一种软件重用形式，通过创建新类来吸收现有类的功能，然后*定制*或增强这些功能。软件重用利用经过验证的高质量软件，在程序开发过程中节省时间。

创建类时，无需编写全新的数据成员和成员函数，你可以指定新类应当*继承*现有类的成员。这个现有类称为*基类*，新类称为*派生类*。其他编程语言（如 Java 和 C#）将基类称为*超类*，将派生类称为*子类*。派生类表示*更专门*的对象组。

C++ 提供 `public`、`protected` 和 `private` 继承。本章我们重点讨论 public 继承，并简要解释另外两种。对于*public 继承，派生类的每个对象同时也是该派生类的基类对象。* 然而，基类对象并不是其派生类的对象。例如，如果我们以 Vehicle 作为基类、Car 作为派生类，那么所有 Car 都是 Vehicle，但并非所有 Vehicle 都是 Car——例如，Vehicle 也可能是 Truck 或 Boat。

我们区分*is-a关系*和*has-a关系*。*is-a*关系表示继承。在*is-a*关系中，派生类的对象也可以被视为其基类的对象——例如，*Car* 是一种 *Vehicle*，因此 Vehicle 的任何属性和行为也是 Car 的属性和行为。相比之下，*has-a*关系表示*组合*，这在第9章已讨论。在*has-a*关系中，一个对象*包含*一个或多个其他类的对象作为成员。例如，一辆 Car 有许多组件——它*有*方向盘、*有*刹车踏板、*有*变速箱等。

### 11.2 基类和派生类

图 11.1 列出了基类和派生类的几个简单示例。基类往往*更通用*，而派生类往往*更具体*。

