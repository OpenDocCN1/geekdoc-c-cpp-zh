

```cpp
private:
    double baseSalary; // base salary
}; // end class BasePlusCommissionEmployee

#endif
```

**图 11.10** | 表明与类 `CommissionEmployee` 具有继承关系的 `BasePlusCommissionEmployee` 类定义（第2部分，共2部分）。

```cpp
// Fig. 11.11: BasePlusCommissionEmployee.cpp
// Class BasePlusCommissionEmployee member-function definitions.
#include <iostream>
#include <stdexcept>
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
    if ( salary >= 0.0 )
        baseSalary = salary;
    else
        throw invalid_argument( "Salary must be >= 0.0" );
} // end function setBaseSalary

// return base salary
double BasePlusCommissionEmployee::getBaseSalary() const
{
    return baseSalary;
} // end function getBaseSalary

// calculate earnings
double BasePlusCommissionEmployee::earnings() const
{
    // derived class cannot access the base class’s private data
    return baseSalary + ( commissionRate * grossSales );
} // end function earnings
```

**图 11.11** | `BasePlusCommissionEmployee` 实现文件：基类私有数据无法从派生类访问（第1部分，共2部分）。

![](img/b42ba5cd262b1358d16610173f975e4d_535_0.png)

**性能提示 11.1**

在派生类构造函数中，在成员初始化列表里显式调用基类构造函数并初始化成员对象，可以防止重复初始化——即先调用默认构造函数，然后在派生类构造函数体内再次修改数据成员。

## 访问基类私有成员导致的编译错误

编译器会针对图 11.11 中的第 37 行生成错误，因为基类 CommissionEmployee 的数据成员 commissionRate 和 grossSales 是私有的——派生类 BasePlusCommissionEmployee 的成员函数不允许访问基类 CommissionEmployee 的私有数据。由于同样的原因，编译器还会在 BasePlusCommissionEmployee 的 print 成员函数的第 44–47 行生成额外的错误。如你所见，C++ 对访问私有数据成员实施了严格限制，因此即使是派生类（与其基类关系密切）也不能访问基类的私有数据。

## 预防 BasePlusCommissionEmployee 中的错误

我们特意在图 11.11 中包含了错误代码，以强调派生类的成员函数不能访问其基类的私有数据。BasePlusCommissionEmployee 中的错误本可以通过使用从类 CommissionEmployee 继承的 get 成员函数来避免。例如，第 37 行可以调用 getCommissionRate 和 getGrossSales 来分别访问 CommissionEmployee 的私有数据成员 commissionRate 和 grossSales。同样，第 44–47 行可以使用适当的 get 成员函数来获取基类数据成员的值。在下一个示例中，我们还将展示使用 protected 数据如何帮助我们避免本例中遇到的错误。

## 在派生类头文件中使用 #include 包含基类头文件

请注意，我们在派生类的头文件中 #include 了基类的头文件（图 11.10 中的第 8 行）。这样做有三个原因。首先，为了让派生类在第 10 行使用基类的名称，我们必须告知编译器该基类存在——CommissionEmployee.h 中的类定义正是如此。

第二个原因是，编译器使用类定义来确定该类对象的大小（正如我们在第 3.6 节中讨论的）。创建某类对象的客户端程序会 #include 该类定义，以便编译器能够为该对象预留适当的内存。使用继承时，派生类对象的大小取决于其类定义中显式声明的数据成员，以及从其直接和间接基类继承的数据成员。在第 8 行包含基类定义，使编译器能够确定将成为派生类对象一部分的基类数据成员的内存需求，从而共同决定派生类对象的总大小。

第 8 行的最后一个原因是让编译器确定派生类是否正确使用了基类的继承成员。例如，在图 11.10–11.11 的程序中，编译器使用基类头文件来确定派生类访问的数据成员在基类中是私有的。由于这些成员对派生类不可访问，编译器会生成错误。编译器还使用基类的函数原型来验证派生类对继承的基类函数的调用。

## 继承层次中的链接过程

在第 3.7 节中，我们讨论了创建可执行的 GradeBook 应用程序的链接过程。在那个示例中，你看到客户端的目标代码与 GradeBook 类的目标代码以及客户端代码或 GradeBook 类中使用的任何 C++ 标准库类的目标代码链接在一起。

对于在继承层次中使用类的程序，链接过程类似。该过程需要程序中所有类的目标代码，以及程序所使用的任何派生类的直接和间接基类的目标代码。假设客户端想要创建一个使用类 BasePlusCommissionEmployee（它是 CommissionEmployee 的派生类，我们将在第 11.3.4 节中看到这样的示例）的应用程序。在编译客户端应用程序时，客户端的目标代码必须与类 BasePlusCommissionEmployee 和 CommissionEmployee 的目标代码链接，因为 BasePlusCommissionEmployee 从其基类 CommissionEmployee 继承了成员函数。该代码还与类 CommissionEmployee、类 BasePlusCommissionEmployee 或客户端代码中使用的任何 C++ 标准库类的目标代码链接。这为程序提供了访问其可能使用的所有功能的实现的权限。

## 11.3.4 使用 protected 数据的 CommissionEmployee–BasePlusCommissionEmployee 继承层次

第 3 章介绍了访问说明符 public 和 private。基类的 public 成员可以在其体内以及程序拥有指向该类或其派生类对象的句柄（即名称、引用或指针）的任何地方访问。基类的 private 成员只能在其体内以及该基类的友元中访问。在本节中，我们介绍访问说明符 **protected**。

使用 protected 访问提供了介于 public 和 private 访问之间的中间保护级别。为了使类 BasePlusCommissionEmployee 能够直接访问 CommissionEmployee 的数据成员 firstName、lastName、socialSecurityNumber、grossSales 和 commissionRate，我们可以在基类中将这些成员声明为 protected。基类的 protected 成员可以在该基类的体内，由该基类的成员和友元，以及由从该基类派生的任何类的成员和友元访问。

### 使用 protected 数据定义基类 CommissionEmployee

类 CommissionEmployee（图 11.12）现在将数据成员 firstName、lastName、socialSecurityNumber、grossSales 和 commissionRate 声明为 protected（第 31–36 行），而不是 private。成员函数实现与图 11.5 中的相同，因此此处不再显示 CommissionEmployee.cpp。

```cpp
// Fig. 11.12: CommissionEmployee.h
// CommissionEmployee class definition with protected data.
#ifndef COMMISSION_H
#define COMMISSION_H
```

**图 11.12** | 声明 protected 数据以允许派生类访问的 CommissionEmployee 类定义（第1部分，共2部分）。

