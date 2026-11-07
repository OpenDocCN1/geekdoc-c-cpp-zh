

# 10.6.1 从派生类对象调用基类函数

图 10.7 复用了第 10.3 节的 `SalariedEmployee` 和 `SalariedCommissionEmployee` 类。该示例演示了将基类指针和派生类指针分别指向基类对象和派生类对象。前两种方式很自然且直接：

- 我们将基类指针指向基类对象，并调用基类功能。
- 我们将派生类指针指向派生类对象，并调用派生类功能。

然后，我们通过将基类指针指向派生类对象，并展示基类功能在派生类对象中可用，来演示派生类与基类之间的**is-a**关系。

```cpp
// fig10_07.cpp
// Aiming base-class and derived-class pointers at base-class
// and derived-class objects, respectively.
#include <format>
#include <iostream>
#include "SalariedEmployee.h"
#include "SalariedCommissionEmployee.h"

int main() {
   // create base-class object
   SalariedEmployee salaried{"Sierra Dembo", 500.0};

   // create derived-class object
   SalariedCommissionEmployee salariedCommission{
      "Ivano Lai", 300.0, 5000.0, 0.04};

   // output objects salaried and salariedCommission
   std::cout << std::format("{}\n{}\n{}\n",
      "DISPLAY BASE-CLASS AND DERIVED-CLASS OBJECTS:",
      salaried.toString(), // base-class toString
      salariedCommission.toString()); // derived-class toString

   // natural: aim base-class pointer at base-class object
   SalariedEmployee* salariedPtr{&salaried};
   std::cout << std::format("{}\n{}\n{}\n",
      "CALLING TOSTRING WITH BASE-CLASS POINTER TO",
      "BASE-CLASS OBJECT INVOKES BASE-CLASS FUNCTIONALITY:",
      salariedPtr->toString()); // base-class version

   // natural: aim derived-class pointer at derived-class object
   SalariedCommissionEmployee* salariedCommissionPtr{&salariedCommission};

   std::cout << std::format("{}\n{}\n{}\n",
      "CALLING TOSTRING WITH DERIVED-CLASS POINTER TO",
      "DERIVED-CLASS OBJECT INVOKES DERIVED-CLASS FUNCTIONALITY:",
      salariedCommissionPtr->toString()); // derived-class version

   // aim base-class pointer at derived-class object
   salariedPtr = &salariedCommission;
   std::cout << std::format("{}\n{}\n{}\n",
      "CALLING TOSTRING WITH BASE-CLASS POINTER TO DERIVED-CLASS",
      "OBJECT INVOKES BASE-CLASS FUNCTIONALITY:",
      salariedPtr->toString()); // base class version
}
```

**图 10.7** | 将基类和派生类对象的地址赋给基类和派生类指针。（第 1 部分，共 2 部分。）

**图 10.7** | 将基类和派生类对象的地址赋给基类和派生类指针。（第 2 部分，共 2 部分。）

```text
DISPLAY BASE-CLASS AND DERIVED-CLASS OBJECTS:
name: Sierra Dembo
salary: $500.00

name: Ivano Lai
salary: $300.00
gross sales: $5000.00
commission rate: 0.04

CALLING TOSTRING WITH BASE-CLASS POINTER TO
BASE-CLASS OBJECT INVOKES BASE-CLASS FUNCTIONALITY:
name: Sierra Dembo
salary: $500.00

CALLING TOSTRING WITH DERIVED-CLASS POINTER TO
DERIVED-CLASS OBJECT INVOKES DERIVED-CLASS FUNCTIONALITY:
name: Ivano Lai
salary: $300.00
gross sales: $5000.00
commission rate: 0.04

CALLING TOSTRING WITH BASE-CLASS POINTER TO DERIVED-CLASS
OBJECT INVOKES BASE-CLASS FUNCTIONALITY:
name: Ivano Lai
salary: $300.00
```

回想一下，`SalariedCommissionEmployee` 对象 *是一个* `SalariedEmployee`，并根据总销售额赚取佣金。`SalariedCommissionEmployee` 的 earnings 成员函数（图 10.5，第 49–52 行）重新定义了 `SalariedEmployee` 的版本（图 10.2，第 34 行），以包含佣金。`SalariedCommissionEmployee` 的 `toString` 成员函数（图 10.5，第 55–59 行）重新定义了 `SalariedEmployee` 的版本（图 10.2，第 37–40 行），以返回相同的信息以及雇员的佣金。

### 创建对象并显示其内容

在图 10.7 中，第 11 行创建了一个 `SalariedEmployee` 对象，第 14–15 行创建了一个 `SalariedCommissionEmployee` 对象。第 20 和 21 行使用每个对象的名称来调用其 `toString` 成员函数。

### 将基类指针指向基类对象

第 24 行用基类对象 `salaried` 的地址初始化 `SalariedEmployee` 指针 `salariedPtr`。第 28 行使用该指针从基类 `SalariedEmployee` 调用 `salaried` 对象的 `toString` 成员函数。

### 将派生类指针指向派生类对象

第 31 行用派生类对象 `salariedCommission` 的地址初始化 `SalariedCommissionEmployee` 指针 `salariedCommissionPtr`。第 36 行使用该指针从派生类 `SalariedCommissionEmployee` 调用 `salariedCommission` 对象的 `toString` 成员函数。

### 将基类指针指向派生类对象

第 39 行将派生类对象 `salariedCommission` 的地址赋给基类指针 `salariedPtr`。这种“跨界”是允许的，因为派生类对象*是*其基类的一个对象。第 43 行使用此指针调用 `toString`。即使基类 `SalariedEmployee` 指针指向一个 `SalariedCommissionEmployee` 派生类对象，调用的仍是*基类*的 `toString` 成员函数。总销售额和佣金率未显示，因为它们不是基类成员。

此程序的输出表明，所调用的函数取决于用于调用函数的指针类型（或引用类型，稍后你会看到），而不是被调用成员函数的对象类型。在第 10.7 节中，我们将看到虚函数使得调用对象类型的功能成为可能——这是实现运行时多态行为的重要方面。

## 10.6.2 将派生类指针指向基类对象

现在，让我们尝试将派生类指针指向基类对象（图 10.8）。第 7 行创建了一个 `SalariedEmployee` 对象。第 11 行尝试用基类 `salaried` 对象的地址初始化 `SalariedCommissionEmployee` 指针。编译器会生成错误，因为 `SalariedEmployee` *不是* `SalariedCommissionEmployee`。

```cpp
 1  // fig10_08.cpp
 2  // Aiming a derived-class pointer at a base-class object.
 3  #include "SalariedEmployee.h"
 4  #include "SalariedCommissionEmployee.h"
 5
 6  int main() {
 7      SalariedEmployee salaried{"Sierra Dembo", 500.0};
 8
 9      // aim derived-class pointer at base-class object
10      // Error: a SalariedEmployee is not a SalariedCommissionEmployee
11      SalariedCommissionEmployee* salariedCommissionPtr{&salaried};
12  }
```

Microsoft Visual C++ 编译器错误信息：

```text
fig10_08.cpp(11,63): error C2440: 'initializing': cannot convert from
'SalariedEmployee *' to 'SalariedCommissionEmployee *'
```

**图 10.8** | 将派生类指针指向基类对象。

考虑一下如果编译器允许这种赋值会有什么后果。通过 `SalariedCommissionEmployee` 指针，我们可以调用该类的任何成员函数，包括 `setGrossSales` 和 `setCommissionRate`，对指针所指向的对象——即基类对象 `salaried`。然而，`SalariedEmployee` 对象既没有 `setGrossSales` 和 `setCommissionRate` 成员函数，也没有要设置的数据成员 `m_grossSales` 和 `m_commissionRate`。如果允许这样做，可能会引发问题，因为成员函数 `setGrossSales` 和 `setCommissionRate` 会假定数据成员 `m_grossSales` 和 `m_commissionRate` 存在于 `SalariedCommissionEmployee` 对象的“通常位置”。`SalariedEmployee` 对象的内存中没有这些数据成员，因此 `setGrossSales` 和 `setCommissionRate` 可能会覆盖内存中的其他数据。

## 10.6.3 通过基类指针调用派生类成员函数

编译器只允许我们通过基类指针调用基类成员函数。因此，如果基类指针指向派生类对象，并尝试访问仅属于派生类的成员函数，就会发生编译错误。图 10.9 显示了通过基类指针调用仅属于派生类的成员函数（第 22–24 行）时的编译器错误。

```cpp
// fig10_09.cpp
// Attempting to call derived-class-only functions
// via a base-class pointer.
#include <string>
#include "SalariedEmployee.h"
#include "SalariedCommissionEmployee.h"

int main() {
   SalariedCommissionEmployee salariedCommission{
      "Ivano Lai", 300.0, 5000.0, 0.04};

   // aim base-class pointer at derived-class object (allowed)
   SalariedEmployee* salariedPtr{&salariedCommission};

   // invoke base-class member functions on derived-class
   // object through base-class pointer (allowed)
   std::string name{salariedPtr->getName()};
   double salary{salariedPtr->getSalary()};

   // attempt to invoke derived-class-only member functions
   // on derived-class object through base-class pointer (disallowed)
   double grossSales{salariedPtr->getGrossSales()};
   double commissionRate{salariedPtr->getCommissionRate()};
   salariedPtr->setGrossSales(8000.0);
}
```

*GNU C++ 编译器错误信息：*

```text
fig10_09.cpp: In function ‘int main()’:
fig10_09.cpp:22:35: error: ‘class SalariedEmployee’ has no member named
‘getGrossSales’
   22 |     double grossSales{salariedPtr->getGrossSales()};
      |                       ~~~~~~~~~~~~^~~~~~~~~~~~~~~
```

**图 10.9** 尝试通过基类指针调用仅属于派生类的函数。（第 1 部分，共 2 部分。）

