

Employee 对象没有提供 setBaseSalary 成员函数，也没有提供可供设置的 baseSalary 数据成员。这可能导致问题，因为成员函数 setBaseSalary 会假定在 BasePlusCommissionEmployee 对象的“通常位置”存在一个可供设置的 baseSalary 数据成员。该内存并不属于 CommissionEmployee 对象，因此成员函数 setBaseSalary 可能会覆盖内存中的其他重要数据，这些数据可能属于另一个对象。

// Fig. 20.2: fig20_02.cpp
// Aiming a derived-class pointer at a base-class object.
#include "CommissionEmployee.h"
#include "BasePlusCommissionEmployee.h"

int main()
{
CommissionEmployee commissionEmployee(
"Sue", "Jones", "222-22-2222", 10000, .06);
BasePlusCommissionEmployee *basePlusCommissionEmployeePtr = nullptr;

// aim derived-class pointer at base-class object
// Error: a CommissionEmployee is not a BasePlusCommissionEmployee
basePlusCommissionEmployeePtr = &commissionEmployee;
} // end main

Microsoft Visual C++ 编译器错误消息：

```
C:\examples\ch20\Fig20_02\fig20_02.cpp(14): error C2440: '=' :
 cannot convert from 'CommissionEmployee *' to 'BasePlusCommissionEmployee *'
Cast from base to derived requires dynamic_cast or static_cast
```

图 20.2 | 让派生类指针指向基类对象。

## 20.3.3 通过基类指针调用派生类成员函数

通过基类指针，编译器只允许我们调用基类成员函数。因此，如果基类指针指向派生类对象，并试图访问仅属于派生类的成员函数，就会发生编译错误。

图 20.3 展示了试图通过基类指针调用派生类成员函数的后果。[注意：我们再次复用 19.3.5 节中 CommissionEmployee 和 BasePlusCommissionEmployee 类的版本。] 第 11 行创建 commissionEmployeePtr——一个指向 CommissionEmployee 对象的指针——第 12～13 行创建一个 BasePlusCommissionEmployee 对象。第 16 行让基类 commissionEmployeePtr 指向派生类对象 basePlusCommissionEmployee。回想 20.3.1 节的内容，这是允许的，因为 BasePlusCommissionEmployee 对象是一个 CommissionEmployee（从 BasePlusCommissionEmployee 对象包含 CommissionEmployee 对象的全部功能这个意义上说）。第 20～24 行通过基类指针调用基类成员函数 getFirstName、getLastName、getSocialSecurityNumber、getGrossSales 和 getCommissionRate。所有这些调用都是允许的，因为 BasePlusCommissionEmployee 从 CommissionEmployee 继承了这些成员函数。我们知道 commissionEmployeePtr 指向一个 BasePlusCommissionEmployee 对象，因此在第 28～29 行，我们试图调用 BasePlusCommissionEmployee 的成员函数 getBaseSalary 和 setBaseSalary。编译器对这两个调用都生成错误，因为这些调用*不是*针对基类 CommissionEmployee 的成员函数进行的。句柄*只*能用来调用属于该句柄关联类类型的那些函数。（在本例中，通过 CommissionEmployee * 只能调用 CommissionEmployee 的成员函数 setFirstName、getFirstName、setLastName、getLastName、setSocialSecurityNumber、getSocialSecurityNumber、setGrossSales、getGrossSales、setCommissionRate、getCommissionRate、earnings 和 print。）

```
// Fig. 20.3: fig20_03.cpp
// Attempting to invoke derived-class-only member functions
// via a base-class pointer.
#include <string>
#include "CommissionEmployee.h"
#include "BasePlusCommissionEmployee.h"
using namespace std;

int main()
{
   CommissionEmployee *commissionEmployeePtr = nullptr; // base class ptr
   BasePlusCommissionEmployee basePlusCommissionEmployee(
      "Bob", "Lewis", "333-33-3333", 5000, .04, 300 ); // derived class

   // aim base-class pointer at derived-class object (allowed)
   commissionEmployeePtr = &basePlusCommissionEmployee;

   // invoke base-class member functions on derived-class
   // object through base-class pointer (allowed)
   string firstName = commissionEmployeePtr->getFirstName();
   string lastName = commissionEmployeePtr->getLastName();
   string ssn = commissionEmployeePtr->getSocialSecurityNumber();
   double grossSales = commissionEmployeePtr->getGrossSales();
   double commissionRate = commissionEmployeePtr->getCommissionRate();

   // attempt to invoke derived-class-only member functions
   // on derived-class object through base-class pointer (disallowed)
   double baseSalary = commissionEmployeePtr->getBaseSalary();
   commissionEmployeePtr->setBaseSalary( 500 );
} // end main
```

GNU C++ 编译器错误消息：

> fig20_03.cpp:28:47: 错误：'class CommissionEmployee' 没有名为 'getBaseSalary' 的成员
> fig20_03.cpp:29:27: 错误：'class CommissionEmployee' 没有名为 'setBaseSalary' 的成员

图 20.3 | 试图通过基类指针调用仅属于派生类的函数。

### 向下转型

编译器允许从指向派生类对象的基类指针访问仅属于派生类的成员，*前提是我们显式地将该基类指针强制转换为派生类指针*——这称为向下转型。如你所知，可以让基类指针指向派生类对象。然而，正如我们在图 20.3 中所示，基类指针只能用来调用基类中声明的函数。向下转型允许对基类指针所指向的派生类对象执行派生类特有的操作。向下转型之后，程序可以调用基类中没有的派生类函数。向下转型是一种潜在危险的操作。20.8 节演示如何安全地使用向下转型。

### 软件工程观察 20.3

> > *如果将派生类对象的地址赋给了其某个直接或间接基类的指针，那么将该基类指针强制转换回派生类类型的指针是可以接受的。事实上，要调用基类中未出现的派生类成员函数，必须这样做。*

## 20.3.4 虚函数与虚析构函数

在 20.3.1 节中，我们让一个基类 CommissionEmployee 指针指向派生类 BasePlusCommissionEmployee 对象，然后通过该指针调用成员函数 print。回想一下，句柄的类型决定了调用哪个类的功能。在那种情况下，CommissionEmployee 指针在 BasePlusCommissionEmployee 对象上调用了 CommissionEmployee 的成员函数 print，尽管该指针指向的是一个拥有自己自定义 print 函数的 BasePlusCommissionEmployee 对象。

### 软件工程观察 20.4

> > *使用虚函数时，决定调用哪个版本的虚函数的是对象的类型，而不是用于调用成员函数的句柄类型。*

### 虚函数为何有用

首先，我们考虑虚函数为何有用。假设 Circle、Triangle、Rectangle 和 Square 等形状类都派生自基类 Shape。这些类中的每一个都可能通过成员函数 draw 获得绘制自身的能力，但每个形状的函数差别很大。在绘制一组形状的程序中，能够将所有形状一般地当作基类 Shape 的对象来处理会很有用。然后，要绘制任何形状，我们可以简单地使用基类 Shape 指针调用函数 draw，并让程序根据基类 Shape 指针在任意给定时刻所指向的对象的类型，动态地（即在运行时）确定使用哪个派生类的 draw 函数。这就是多态行为。

### 声明虚函数

为了实现这种行为，我们在基类中将 draw 声明为虚函数，并在每个派生类中重写 draw 以绘制相应的形状。从实现的角度来看，重写函数与重新定义函数没有区别（这就是我们到目前为止一直采用的方法）。派生类中被重写的函数与其在基类中被重写的函数具有相同的签名和返回类型（即原型）。如果我们不将基类函数声明为虚函数，我们可以重新定义该函数。相比之下，如果我们将基类函数声明为虚函数，我们就可以重写该函数以实现多态行为。在基类中，我们通过在函数原型前加上关键字 virtual 来声明虚函数。例如，

