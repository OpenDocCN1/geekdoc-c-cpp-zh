
```cpp
65 // set gross sales amount
66 void CommissionEmployee::setGrossSales( double sales )
67 {
68     grossSales = ( sales < 0.0 ) ? 0.0 : sales;
69 } // end function setGrossSales
70
71 // return gross sales amount
72 double CommissionEmployee::getGrossSales() const
73 {
74     return grossSales;
75 } // end function getGrossSales
76
77 // set commission rate
78 void CommissionEmployee::setCommissionRate( double rate )
79 {
80     commissionRate = ( rate > 0.0 && rate < 1.0 ) ? rate : 0.0;
81 } // end function setCommissionRate
82
83 // return commission rate
84 double CommissionEmployee::getCommissionRate() const
85 {
86     return commissionRate;
87 } // end function getCommissionRate
88
89 // calculate earnings
90 double CommissionEmployee::earnings() const
91 {
92     return getCommissionRate() * getGrossSales();
93 } // end function earnings
94
95 // print CommissionEmployee object
96 void CommissionEmployee::print() const
97 {
98     cout << "commission employee: "
99          << getFirstName() << ' ' << getLastName()
100         << "\nsocial security number: " << getSocialSecurityNumber()
101         << "\ngross sales: " << getGrossSales()
102         << "\ncommission rate: " << getCommissionRate();
103 } // end function print
```

**图 12.23** | CommissionEmployee 的构造函数和析构函数输出文本。（第 3 部分，共 3 部分。）

```cpp
1 // Fig. 12.24: BasePlusCommissionEmployee.h
2 // BasePlusCommissionEmployee class derived from class
3 // CommissionEmployee.
4 #ifndef BASEPLUS_H
5 #define BASEPLUS_H
6
7 #include <string> // C++ standard string class
8 #include "CommissionEmployee.h" // CommissionEmployee class declaration
9 using namespace std;
10
```

**图 12.24** | BasePlusCommissionEmployee 类头文件。（第 1 部分，共 2 部分。）

对于对象 employee2，BasePlusCommissionEmployee 和 CommissionEmployee 的析构函数按（该顺序）被调用。

```cpp
// Fig. 12.26: fig12_26.cpp
// Display order in which base-class and derived-class constructors
// and destructors are called.
#include <iostream>
#include <iomanip>
#include "BasePlusCommissionEmployee.h"
using namespace std;

int main()
{
   // set floating-point output formatting
   cout << fixed << setprecision( 2 );

   { // begin new scope
      CommissionEmployee employee1(
         "Bob", "Lewis", "333-33-3333", 5000, .04 );
   } // end scope

   cout << endl;
   BasePlusCommissionEmployee
      employee2( "Lisa", "Jones", "555-55-5555", 2000, .06, 800 );

   cout << endl;
   BasePlusCommissionEmployee
      employee3( "Mark", "Sands", "888-88-8888", 8000, .15, 2000 );
   cout << endl;
} // end main
```

```text
CommissionEmployee constructor:
commission employee: Bob Lewis
social security number: 333-33-3333
gross sales: 5000.00
commission rate: 0.04

CommissionEmployee destructor:
commission employee: Bob Lewis
social security number: 333-33-3333
gross sales: 5000.00
commission rate: 0.04

CommissionEmployee constructor:
commission employee: Lisa Jones
social security number: 555-55-5555
gross sales: 2000.00
commission rate: 0.06

BasePlusCommissionEmployee constructor:
base-salaried commission employee: Lisa Jones
social security number: 555-55-5555
```

**图 12.26** | 构造函数和析构函数的调用顺序。（第 1 部分，共 2 部分。）

| 基类成员访问说明符 | 继承类型 — 公有继承 | 继承类型 — 保护继承 | 继承类型 — 私有继承 |
|---|---|---|---|
| **公有** | 在派生类中为公有。<br><br>可被成员函数、友元函数和非成员函数直接访问。 | 在派生类中为保护。<br><br>可被成员函数和友元函数直接访问。 | 在派生类中为私有。<br><br>可被成员函数和友元函数直接访问。 |
| **保护** | 在派生类中为保护。<br><br>可被成员函数和友元函数直接访问。 | 在派生类中为保护。<br><br>可被成员函数和友元函数直接访问。 | 在派生类中为私有。<br><br>可被成员函数和友元函数直接访问。 |
| **私有** | 在派生类中隐藏。<br><br>可通过基类的公有或保护成员函数被成员函数和友元函数访问。 | 在派生类中隐藏。<br><br>可通过基类的公有或保护成员函数被成员函数和友元函数访问。 | 在派生类中隐藏。<br><br>可通过基类的公有或保护成员函数被成员函数和友元函数访问。 |

**图 12.27** | 派生类中基类成员可访问性总结。

从公有基类派生时，基类的公有成员成为派生类的公有成员，基类的保护成员成为派生类的保护成员。基类的私有成员永远不能直接从派生类访问，但可以通过对基类的公有和保护成员的调用来访问。

从保护基类派生时，基类的公有和保护成员成为派生类的保护成员。从私有基类派生时，基类的公有和保护成员成为派生类的私有成员（例如，这些函数成为工具函数）。私有和保护继承不是 *“是”* 关系。

### 12.7 使用继承的软件工程

在本节中，我们讨论使用继承来定制现有软件。当我们使用继承从现有类创建新类时，新类继承现有类的数据成员和成员函数，如图 12.27 所述。我们可以通过添加额外成员和重定义基类成员来定制新类以满足我们的需求。派生类程序员在 C++ 中做到这一点，无需访问基类的源代码。派生类必须能够链接到基类的目标代码。这种强大的能力对独立软件供应商（ISVs）很有吸引力。

ISV 可以开发专有类进行销售或许可，并以目标代码格式将这些类提供给用户。然后，用户可以快速地从这些库类中派生新类，而无需访问 ISV 的专有源代码。ISV 随目标代码一起需要提供的只是头文件。

有时学生很难体会行业大型软件项目设计者所面临问题的范围。有经验的人说，有效的软件重用能改进软件开发过程。面向对象编程促进了软件重用，从而缩短了开发时间并提高了软件质量。

大量有用类库的可用性通过继承实现了软件重用的最大效益。正如独立软件供应商生产的封装软件随着个人计算机的到来成为爆炸性增长的行业一样，类库的创建和销售的兴趣正在指数级增长。应用程序设计者使用这些库构建其应用，而库设计者因他们的库被包含在应用中而获得回报。随 C++ 编译器一起提供的标准 C++ 库往往相当通用且范围有限。然而，全世界有大量致力于为各种应用领域开发类库的努力。

> **软件工程观察 12.9**
>
> *在面向对象系统的设计阶段，设计者经常确定某些类是密切相关的。设计者应该“提取”共同的属性和行为，并将它们放入基类，然后使用继承形成派生类，赋予它们超出从基类继承的能力。*

![](img/023f159fdd47d944d48e08843cea732d_602_0.png)

> **软件工程观察 12.10**
>
> *派生类的创建不会影响其基类的源代码。继承保持了基类的完整性。*

![](img/023f159fdd47d944d48e08843cea732d_602_1.png)

> **性能提示 12.3**
>
> *如果通过继承产生的类比实际需要的更大（即包含太多功能），可能会浪费内存和处理资源。从功能“最接近”所需功能的类继承。*

![](img/023f159fdd47d944d48e08843cea732d_602_2.png)

阅读派生类定义可能会令人困惑，因为继承的成员没有物理地显示在派生类中，但它们确实存在。在记录派生类成员时也存在类似的问题。

### 12.8 小结

本章介绍了继承——通过吸收现有类的数据成员和成员函数并为其增添新功能来创建类的能力。通过使用雇员继承层次结构的系列示例，你学习了基类和派生类的概念，并使用公有继承创建了从基类继承成员的派生类。本章介绍了访问说明符 protected——派生类成员函数可以访问受保护的基类成员。你学习了如何通过用基类名和二元作用域解析运算符（::）限定重定义的基类成员的名字来访问它们。你还看到了顺序
