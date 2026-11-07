

```cpp
14    char getData() const
15    {
16       return letter;
17    } // end function getData
18 protected: // accessible to derived classes
19    char letter; // inherited by derived class
20 }; // end class Base2

23 #endif // BASE2_H
```

**图 23.8** | 演示多重继承——Base2.h。（第 2 部分，共 2 部分。）

类 Derived（图 23.9–23.10）通过*多重继承*同时继承自类 Base1 和类 Base2。类 Derived 有一个名为 real 的 double 类型私有数据成员（图 23.9，第 20 行）、一个用于初始化类 Derived 全部数据的构造函数，以及一个公有成员函数 getReal()，该函数返回 double 变量 real 的值。

```cpp
1  // Fig. 23.9: Derived.h
2  // Definition of class Derived which inherits
3  // multiple base classes (Base1 and Base2).
4  #ifndef DERIVED_H
5  #define DERIVED_H

7  #include <iostream>
8  #include "Base1.h"
9  #include "Base2.h"
10 using namespace std;

12 // class Derived definition
13 class Derived : public Base1, public Base2
14 {
15    friend ostream &operator<<( ostream &, const Derived & );
16 public:
17    Derived( int, char, double );
18    double getReal() const;
19 private:
20    double real; // derived class's private data
21 }; // end class Derived

23 #endif // DERIVED_H
```

**图 23.9** | 演示多重继承——Derived.h。

```cpp
1  // Fig. 23.10: Derived.cpp
2  // Member-function definitions for class Derived
3  #include "Derived.h"

5  // constructor for Derived calls constructors for
6  // class Base1 and class Base2.
```

**图 23.10** | 演示多重继承——Derived.cpp。（第 1 部分，共 2 部分。）

```cpp
int main()
{
   Base1 base1( 10 ); // create Base1 object
   Base2 base2( 'Z' ); // create Base2 object
   Derived derived( 7, 'A', 3.5 ); // create Derived object

   // print data members of base-class objects
   cout << "Object base1 contains integer " << base1.getData()
      << "\nObject base2 contains character " << base2.getData()
      << "\nObject derived contains:\n" << derived << "\n\n";

   // print data members of derived-class object
   // scope resolution operator resolves getData ambiguity
   cout << "Data members of Derived can be accessed individually:"
      << "\n   Integer: " << derived.Base1::getData()
      << "\n   Character: " << derived.Base2::getData()
      << "\nReal number: " << derived.getReal() << "\n\n";
   cout << "Derived can be treated as an object of either base class:\n";

   // treat Derived as a Base1 object
   Base1 *base1Ptr = &derived;
   cout << "base1Ptr->getData() yields " << base1Ptr->getData() << '\n';

   // treat Derived as a Base2 object
   Base2 *base2Ptr = &derived;
   cout << "base2Ptr->getData() yields " << base2Ptr->getData() << endl;
} // end main
```

```text
Object base1 contains integer 10
Object base2 contains character Z
Object derived contains:
   Integer: 7
   Character: A
Real number: 3.5

Data members of Derived can be accessed individually:
   Integer: 7
   Character: A
Real number: 3.5

Derived can be treated as an object of either base class:
base1Ptr->getData() yields 7
base2Ptr->getData() yields A
```

**图 23.11** | 演示多重继承。（第 2 部分，共 2 部分。）

第 16–18 行显示每个对象的数据值。对于对象 base1 和 base2，我们调用各自的 getData 成员函数。即使本示例中有两个 getData 函数，这些调用也没有二义性。在第 16 行，编译器知道 base1 是类 Base1 的对象，因此调用类 Base1 的 getData。在第 17 行，编译器知道 base2 是类 Base2 的对象，因此调用类 Base2 的 getData。第 18 行使用重载的流插入运算符显示对象 derived 的内容。

### 解决派生类从多个基类继承同名成员函数时产生的二义性问题

第 22–25 行再次使用类 Derived 的 get 成员函数输出对象 derived 的内容。但这里存在一个二义性问题，因为该对象包含两个 getData 函数：一个继承自类 Base1，另一个继承自类 Base2。使用作用域解析运算符即可轻松解决这个问题。表达式 derived.Base1::getData() 获取继承自类 Base1 的变量的值（即名为 value 的 int 变量），而 derived.Base2::getData() 获取继承自类 Base2 的变量的值（即名为 letter 的 char 变量）。调用 derived.getReal() 可以无二义性地打印 real 中的 double 值——在该类层次结构中没有其他同名成员函数。

### 演示多重继承中的 Is-A 关系

单继承中的 is-a 关系同样适用于多重继承关系。为了演示这一点，第 29 行将对象 derived 的地址赋给 Base1 指针 base1Ptr。这是允许的，因为类 Derived 的对象同时也是类 Base1 的对象。第 30 行通过 base1Ptr 调用 Base1 的成员函数 getData，以仅获取对象 derived 中 Base1 部分的值。第 33 行将对象 derived 的地址赋给 Base2 指针 base2Ptr。这是允许的，因为类 Derived 的对象同时也是类 Base2 的对象。第 34 行通过 base2Ptr 调用 Base2 的成员函数 getData，以仅获取对象 derived 中 Base2 部分的值。

## 23.8 多重继承与虚基类

在第 23.7 节中，我们讨论了多重继承，即一个类从两个或多个类继承的过程。例如，C++ 标准库中使用多重继承来形成类 basic_iostream（图 23.12）。

![](img/b42ba5cd262b1358d16610173f975e4d_990_0.png)

**图 23.12** | 使用多重继承形成类 basic_iostream。

类 basic_ios 是 basic_istream 和 basic_ostream 的基类，这两个类都是通过单继承形成的。类 basic_iostream 同时继承自 basic_istream 和 basic_ostream。这使得类 basic_iostream 的对象能够提供 basic_istream 和 basic_ostream 的功能。在多重继承层次结构中，图 23.12 所描述的继承被称为菱形继承。

由于类 basic_istream 和 basic_ostream 都继承自 basic_ios，因此 basic_iostream 存在一个潜在的问题。类 basic_iostream 可能包含类 basic_ios 成员的两份副本——一份通过类 basic_istream 继承，另一份通过类 `basic_ostream` 继承。这种情况将是*有二义性的*，并会导致编译错误，因为编译器将不知道应使用类 `basic_ios` 的哪个版本的成员。在本节中，你将看到使用虚基类如何解决继承间接基类重复副本的问题。

### *菱形继承中出现二义性时产生的编译错误*

图 23.13 演示了*菱形继承*中可能出现的*二义性*。类 Base（第 8–12 行）包含一个 `virtual` 函数 `print`（第 11 行）。类 DerivedOne（第 15–23 行）和 DerivedTwo（第 26–34 行）都公有继承自 Base，并重写了函数 `print`。类 DerivedOne 和类 DerivedTwo 各自包含一个*基类子对象*——即本例中类 Base 的成员。

```cpp
// Fig. 23.13: fig23_13.cpp
// Attempting to polymorphically call a function that is
// multiply inherited from two base classes.
#include <iostream>
using namespace std;

// class Base definition
class Base
{
public:
    virtual void print() const = 0; // pure virtual
}; // end class Base

// class DerivedOne definition
class DerivedOne : public Base
{
public:
    // override print function
    void print() const
    {
        cout << "DerivedOne\n";
    } // end function print
}; // end class DerivedOne

// class DerivedTwo definition
class DerivedTwo : public Base
{
public:
    // override print function
    void print() const
    {
        cout << "DerivedTwo\n";
    } // end function print
}; // end class DerivedTwo

// class Multiple definition
class Multiple : public DerivedOne, public DerivedTwo
{
```

**图 23.13** | 试图以多态方式调用一个多重继承的函数。（第 1 部分，共 2 部分。）

