

```cpp
// Fig. 12.10: BasePlusCommissionEmployee.h
// BasePlusCommissionEmployee class derived from class
// CommissionEmployee.
#ifndef BASEPLUS_H
#define BASEPLUS_H

#include <string> // C++ standard string class
#include "CommissionEmployee.h" // CommissionEmployee class declaration
using namespace std;

class BasePlusCommissionEmployee : public CommissionEmployee
{
public:
   BasePlusCommissionEmployee( const string &, const string &,
      const string &, double = 0.0, double = 0.0, double = 0.0 );

   void setBaseSalary( double ); // set base salary
   double getBaseSalary() const; // return base salary

   double earnings() const; // calculate earnings
   void print() const; // print BasePlusCommissionEmployee object
private:
   double baseSalary; // base salary
}; // end class BasePlusCommissionEmployee

#endif
```

**图 12.10** | BasePlusCommissionEmployee 类定义，表示与 CommissionEmployee 类的继承关系。

```cpp
// Fig. 12.11: BasePlusCommissionEmployee.cpp
// Class BasePlusCommissionEmployee member-function definitions.
#include <iostream>
#include "BasePlusCommissionEmployee.h"
using namespace std;

// constructor
BasePlusCommissionEmployee::BasePlusCommissionEmployee(
   const string &first, const string &last, const string &ssn,
   double sales, double rate, double salary )
   // explicitly call base-class constructor
   : CommissionEmployee( first, last, ssn, sales, rate )
{
   setBaseSalary( salary ); // validate and store base salary
} // end BasePlusCommissionEmployee constructor

// set base salary
void BasePlusCommissionEmployee::setBaseSalary( double salary )
{
```

**图 12.11** | BasePlusCommissionEmployee 实现文件：派生类无法访问基类的私有数据。（第 1 部分，共 3 部分。）

```
C:\chhpt8_examples\ch12\Fig12_10_11\BasePlusCommissionEmployee.cpp(46) :
    error C2248: 'CommissionEmployee::commissionRate':
    cannot access private member declared in class 'CommissionEmployee'
```

**图 12.11** | *BasePlusCommissionEmployee 实现文件：派生类无法访问基类的私有数据。*（第 3 部分，共 3 部分。）

图 12.11 展示了 BasePlusCommissionEmployee 的成员函数实现。构造函数（第 8–15 行）引入了**基类初始化器语法**（第 12 行），它使用成员初始化器将参数传递给基类（CommissionEmployee）构造函数。C++ 要求派生类的构造函数必须调用其基类的构造函数，以初始化继承到派生类中的基类数据成员。第 12 行通过*显式*调用 CommissionEmployee 构造函数来实现这一点，将构造函数的参数 first、last、ssn、sales 和 rate 作为实参，用于初始化基类数据成员 firstName、lastName、socialSecurityNumber、grossSales 和 commissionRate。如果 BasePlusCommissionEmployee 的构造函数没有*显式*调用 CommissionEmployee 类的构造函数，C++ 会尝试隐式调用 CommissionEmployee 类的默认构造函数——但该类没有这样的构造函数，因此编译器会报错。回顾第 3 章可知，对于任何*没有*显式包含构造函数的类，编译器都会提供一个无参默认构造函数。但是，CommissionEmployee *确实*显式包含了一个构造函数，因此*不会*提供默认构造函数。

> **常见编程错误 12.1**
>
> 当派生类构造函数调用基类构造函数时，传递给基类构造函数的实参必须与某个基类构造函数所指定的形参数量和类型一致；否则会发生编译错误。

![](img/bfd978e7e9b192bab46ec2a89e481263_550_0.png)

> **性能提示 12.1**
>
> 在派生类构造函数中，在成员初始化器列表中显式调用基类构造函数并初始化成员对象，可以避免重复初始化：先调用默认构造函数，然后在派生类构造函数体中再次修改数据成员。

![](img/bfd978e7e9b192bab46ec2a89e481263_550_1.png)

## 访问基类私有成员导致的编译错误

编译器会针对图 12.11 中的第 36 行生成错误，因为基类 CommissionEmployee 的数据成员 commissionRate 和 grossSales 是私有的——不允许派生类 BasePlusCommissionEmployee 的成员函数访问基类 CommissionEmployee 的私有数据。由于相同原因，编译器还会在 BasePlusCommissionEmployee 的 print 成员函数第 43–46 行产生额外错误。可以看出，C++ 对访问私有数据成员实施了严格限制，因此即使是*与其基类关系密切的派生类，也不能访问基类的私有数据。*

## 避免 BasePlusCommissionEmployee 中的错误

我们在图 12.11 中特意包含了错误代码，以强调派生类的成员函数不能访问其基类的私有数据。BasePlusCommissionEmployee 中的错误本可以通过使用从 CommissionEmployee 类继承的 *get* 成员函数来避免。例如，第 36 行可以调用 getCommissionRate 和 getGrossSales，分别访问 CommissionEmployee 的私有数据成员 commissionRate 和 grossSales。类似地，第 43–46 行可以使用相应的 *get* 成员函数来获取基类数据成员的值。在下一个示例中，我们将展示如何使用 protected 数据也能避免本例中遇到的错误。

### 在派生类头文件中使用 #include 包含基类头文件

注意，我们在派生类的头文件中使用 #include 包含了基类的头文件（图 12.10 的第 8 行）。这样做有三个原因。首先，为了让派生类能在第 11 行使用基类的名称，我们必须告诉编译器基类存在——CommissionEmployee.h 中的类定义正是这样做的。

第二个原因是，编译器使用类定义来确定该类对象的大小（正如我们在 3.6 节所讨论的）。创建某类对象的客户端程序必须 #include 该类定义，以便编译器为该对象预留适当的内存。使用继承时，派生类对象的大小取决于其类定义中显式声明的数据成员，以及从其直接和间接基类继承的数据成员。在第 8 行包含基类的定义，使编译器能够确定基类数据成员的内存需求，这些数据成员会成为派生类对象的一部分，从而影响派生类对象的总体大小。

第 8 行的最后一个原因是让编译器能够判断派生类是否正确使用了基类的继承成员。例如，在图 12.10–12.11 的程序中，编译器使用基类头文件来确定派生类正在访问的数据成员在基类中是私有的。由于派生类无法访问这些成员，编译器会生成错误。编译器还使用基类的*函数原型*来验证派生类对继承的基类函数所进行的函数调用。

### 继承层次结构中的链接过程

在 3.7 节中，我们讨论了创建可执行 GradeBook 应用程序的链接过程。在那个示例中，你看到客户端的对象代码与 GradeBook 类的对象代码链接，同时还要与该示例或 GradeBook 类中使用的任何 C++ 标准库类的对象代码链接。

对于在继承层次结构中使用类的程序，链接过程与此类似。该过程需要程序中使用的所有类的对象代码，以及程序所使用的任何派生类的直接和间接基类的对象代码。假设客户端想要创建一个使用 BasePlusCommissionEmployee 类的应用程序，该类是 CommissionEmployee 的派生类（我们将在 12.4.4 节看到这样的示例）。在编译客户端应用程序时，客户端的对象代码必须与 BasePlusCommissionEmployee 和 CommissionEmployee 类的对象代码链接，因为 BasePlusCommissionEmployee 从其基类 CommissionEmployee 继承了成员函数。代码还会与在 CommissionEmployee 类、BasePlusCommissionEmployee 类或客户端代码中使用的任何 C++ 标准库类的对象代码链接。这使程序能够访问其可能使用的所有功能的实现。

