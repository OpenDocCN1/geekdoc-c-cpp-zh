
调用的是在*基类* `CommissionEmployee` 中定义的 `toString` 版本。

### 让派生类指针指向派生类对象

类似地，第34–35行创建 `basePlusCommissionEmployeePtr`——一个指向 `BasePlusCommissionEmployee` 对象的指针——并用派生类对象 `basePlusCommissionEmployee` 的地址初始化它。第39行使用该指针在 `BasePlusCommissionEmployee` 对象上调用成员函数 `toString`。这会调用在*派生类* `BasePlusCommissionEmployee` 中定义的 `toString` 版本。

### 让基类指针指向派生类对象

第42行随后将派生类对象 `basePlusCommissionEmployee` 的地址赋给基类指针 `commissionEmployeePtr`，第46行使用该指针调用成员函数 `toString`。这种“交叉”是允许的，因为派生类对象*是*其基类的对象。尽管基类 `CommissionEmployee` 指针指向一个*派生类* `BasePlusCommissionEmployee` 对象，调用的却是*基类* `CommissionEmployee` 的 `toString` 成员函数，而不是 `BasePlusCommissionEmployee` 的 `toString` 函数——注意在这种情况下，既没有显示 `"base-salaried"`，也没有显示 `BasePlusCommissionEmployee` 的基本工资。

该程序中每次调用 `toString` 成员函数的输出表明，被调用的功能取决于用于调用函数的*指针类型*（或引用类型，你很快就会看到），*而不是*调用成员函数所针对的对象的类型。在[第12.4节](#)中，当我们介绍 `virtual` 函数时，将演示可以调用对象类型的功能，*而不是*调用指针类型（或引用类型）的功能。我们将看到，这对于实现多态行为至关重要——这是本章的关键主题。

## 12.3.2 让派生类指针指向基类对象

在[第12.3.1节](#)中，我们将派生类对象的地址赋给基类指针，并解释了C++编译器允许这种赋值，因为派生类对象*是*基类对象。在[图12.2](#)中我们采取相反的做法，让派生类指针指向基类对象。[*注意：* 本程序复用了[第11.3.5节](#)中类 `CommissionEmployee` 和 `BasePlusCommissionEmployee` 的最终版本。] [图12.2](#)的第7–8行创建一个 `CommissionEmployee` 对象。第12–13行尝试用基类对象 `commissionEmployee` 的地址创建并初始化一个 `BasePlusCommissionEmployee` 指针，但编译器产生错误，因为 `CommissionEmployee` *不是* `BasePlusCommissionEmployee`。

```cpp
// Fig. 12.2: fig12_02.cpp
// Aiming a derived-class pointer at a base-class object.
#include "CommissionEmployee.h"
#include "BasePlusCommissionEmployee.h"

int main() {
   CommissionEmployee commissionEmployee{
      "Sue", "Jones", "222-22-2222", 10000, .06};

   // aim derived-class pointer at base-class object
   // Error: a CommissionEmployee is not a BasePlusCommissionEmployee
   BasePlusCommissionEmployee* basePlusCommissionEmployeePtr
      {&commissionEmployee};
}
```

*Microsoft Visual C++ 编译器错误消息：*

```text
c:\examples\ch12\fig12_02\fig12_02.cpp(13):
   error C2440: 'initializing': cannot convert from 'CommissionEmployee *'
   to 'BasePlusCommissionEmployee *'
```

**图12.2 让派生类指针指向基类对象。**

考虑如果编译器允许这种赋值会有什么后果。通过一个 `BasePlusCommissionEmployee` 指针，我们可以对指针所指向的对象（即基类对象 `commissionEmployee`）调用每个 `BasePlusCommissionEmployee` 成员函数，包括 `setBaseSalary`。然而，`CommissionEmployee` 对象*不*提供 `setBaseSalary` 成员函数，也不提供可供设置的 `baseSalary` 数据成员。这可能导致问题，因为成员函数 `setBaseSalary` 会假定在 `BasePlusCommissionEmployee` 对象中的“通常位置”有一个要设置的 `baseSalary` 数据成员。这块内存不属于 `CommissionEmployee` 对象，因此成员函数 `setBaseSalary` 可能覆盖内存中的其他重要数据，可能是属于另一个对象的数据。

## 12.3.3 通过基类指针调用派生类成员函数

通过基类指针，编译器只允许我们调用*仅*基类成员函数。因此，如果基类指针指向派生类对象，并试图访问*仅派生类才有的成员函数*，就会发生编译错误。**图12.3** 展示了尝试通过基类指针调用仅派生类成员函数的后果。[*注意：* 我们再次复用**第11.3.5节**中类 `CommissionEmployee` 和 `BasePlusCommissionEmployee` 的版本。]

```cpp
// Fig. 12.3: fig12_03.cpp
// Attempting to invoke derived-class-only member functions
// via a base-class pointer.
#include <string>
#include "CommissionEmployee.h"
#include "BasePlusCommissionEmployee.h"
using namespace std;

int main() {
   BasePlusCommissionEmployee basePlusCommissionEmployee{
      "Bob", "Lewis", "333-33-3333", 5000, .04, 300};

   // aim base-class pointer at derived-class object (allowed)
   CommissionEmployee* commissionEmployeePtr{&basePlusCommissionEmployee};

   // invoke base-class member functions on derived-class
   // object through base-class pointer (allowed)
   string firstName{commissionEmployeePtr->getFirstName()};
   string lastName{commissionEmployeePtr->getLastName()};
   string ssn{commissionEmployeePtr->getSocialSecurityNumber()};
   double grossSales{commissionEmployeePtr->getGrossSales()};
   double commissionRate{commissionEmployeePtr->getCommissionRate()};

   // attempt to invoke derived-class-only member functions
   // on derived-class object through base-class pointer (disallowed)
   double baseSalary{commissionEmployeePtr->getBaseSalary()};
   commissionEmployeePtr->setBaseSalary(500);
}
```

*GNU C++ 编译器错误消息：*

```text
fig12_03.cpp:26:45: error: 'class CommissionEmployee' has no member named
   'getBaseSalary'
      double baseSalary{commissionEmployeePtr->getBaseSalary()};
                                      ^
fig12_03.cpp:27:27: error: 'class CommissionEmployee' has no member named
   'setBaseSalary'
      commissionEmployeePtr->setBaseSalary(500);
```

**图12.3 尝试通过基类指针调用仅派生类函数。**

第10–11行创建一个 `BasePlusCommissionEmployee` 对象。第14行创建 `commissionEmployeePtr`——一个指向 `CommissionEmployee` 对象的指针——并用派生类对象 `basePlusCommissionEmployee` 的地址初始化它。同样，这是允许的，因为 `BasePlusCommissionEmployee` 是 `CommissionEmployee`（从 `BasePlusCommissionEmployee` 对象包含 `CommissionEmployee` 对象所有功能的意义上说）。

第18–22行通过基类指针调用基类成员函数 `getFirstName`、`getLastName`、`getSocialSecurityNumber`、`getGrossSales` 和 `getCommissionRate`。所有这些调用都是允许的，因为 `BasePlusCommissionEmployee` 从 `CommissionEmployee` *继承*了这些成员函数。

我们知道 `commissionEmployeePtr` 指向一个 `BasePlusCommissionEmployee` 对象，因此在第26–27行尝试调用 `BasePlusCommissionEmployee` 成员函数 `getBaseSalary` 和 `setBaseSalary`。编译器对这两个调用都产生错误，因为这些函数*不是*基类 `CommissionEmployee` 的成员函数。该句柄只能用来调用那些*仅*属于该句柄关联类类型的函数。（在这种情况下，通过一个 `CommissionEmployee*`，我们只能调用 `CommissionEmployee` 成员函数 `setFirstName`、`getFirstName`、`setLastName`、`getLastName`、`setSocialSecurityNumber`、`getSocialSecurityNumber`、`setGrossSales`、`getGrossSales`、`setCommissionRate`、`getCommissionRate`、`earnings` 和 `toString`。）

### 向下转型

