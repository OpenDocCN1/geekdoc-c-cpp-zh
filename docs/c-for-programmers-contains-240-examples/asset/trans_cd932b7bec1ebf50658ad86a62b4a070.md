

## 13.8 案例研究：使用多态性和运行时类型信息、向下转型、dynamic_cast、typeid 和 type_info 的工资系统

回顾第 13.6 节开头问题陈述中所述，对于当前工资期，我们的虚构公司决定通过将基本工资提高 10% 来奖励 BasePlusCommissionEmployees。在第 13.6.6 节中以多态方式处理 Employee 对象时，我们无需担心“具体细节”。现在，为了调整 BasePlusCommissionEmployees 的基本工资，我们必须在执行时确定每个 Employee 对象的具体类型，然后采取相应操作。本节演示了运行时类型信息（RTTI）和动态转换的强大功能，它们使程序能够在执行时确定对象的类型并据此操作该对象。

> [注意：某些编译器要求在使用 RTTI 之前必须先启用 RTTI。查阅编译器文档以确定您的编译器是否有类似要求。在 Visual C++ 2005 中，此选项默认启用。]

图 13.25 使用第 13.6 节中开发的 Employee 层次结构，并将每个 BasePlusCommissionEmployee 的基本工资提高 10%。第 31 行声明了存储指向 Employee 对象的指针的四元素向量 employees。第 34-41 行使用类 SalariedEmployee（图 13.15-13.16）、HourlyEmployee（图 13.17-13.18）、CommissionEmployee（图 13.19-13.20）以及 BasePlusCommissionEmployee（图 13.21-13.22）的动态分配对象的地址填充该向量。

```
1 // Fig. 13.25: fig13_25.cpp
2 // Demonstrating downcasting and runtime type information.
3 // NOTE: You may need to enable RTTI on your compiler
4 // before you can execute this application.
5 #include <iostream>
6 using std::cout;
7 using std::endl;
8 using std::fixed;
9 
10 #include <iomanip>
11 using std::setprecision;
12 
13 #include <vector>
14 using std::vector;
15 
16 #include <typeinfo>
17 
18 // include definitions of classes in Employee hierarchy
19 #include "Employee.h"
20 #include "SalariedEmployee.h"
21 #include "HourlyEmployee.h"
22 #include "CommissionEmployee.h"
23 #include "BasePlusCommissionEmployee.h"
24 
25 int main()
26 {
```

第 65 行在 employees[ i ] 指向的对象上调用成员函数 earnings。回顾一下，earnings 在基类中声明为 virtual，因此程序调用派生类对象的 earnings 函数——动态绑定的另一个例子。

第 69–76 行显示每个员工的对象的类型并使用 delete 运算符释放每个向量元素指向的动态内存。运算符 typeid（第 73 行）返回对类 type_info 的对象的引用，该对象包含有关其操作数的类型的信息，包括该类型的名称。调用时，type_info 成员函数 name（第 73 行）返回一个基于指针的字符串，其中包含传递给 typeid 的参数的类型名称（例如，"class BasePlusCommissionEmployee"）。要使用 typeid，程序必须包含头文件 <typeinfo>（第 16 行）。

### 可移植性提示 13.1

> type_info 成员函数 name 返回的字符串可能因编译器而异。

请注意，我们通过将 Employee 指针向下转型为 BasePlusCommissionEmployee 指针（第 50–52 行）避免了此示例中的几个编译错误。如果我们删除第 51 行的 dynamic_cast 并尝试将当前的 Employee 指针直接分配给 BasePlusCommissionEmployee 指针 derivedPtr，我们将收到编译错误。C++ 不允许程序将基类指针分配给派生类指针，因为 is-a 关系不适用——CommissionEmployee 不是 BasePlusCommissionEmployee。is-a 关系仅适用于派生类与其基类之间，而不适用于反向关系。

同样，如果第 58、60 和 62 行使用 employees 中的当前基类指针，而不是派生类指针 derivedPtr，来调用仅派生类函数 getBaseSalary 和 setBaseSalary，我们将在每一行都收到编译错误。正如你在第 13.3.3 节中所学，通过基类指针尝试调用仅派生类函数是不允许的。虽然第 58、60 和 62 行仅在 commissionPtr 不为 0 时执行（即可以执行转换时），但我们不能尝试在基类 Employee 指针上调用派生类 BasePlusCommissionEmployee 函数 getBaseSalary 和 setBaseSalary。请记住，使用基类 Employee 指针，我们只能调用在基类 Employee 中找到的函数——earnings、print 以及 Employee 的 get 和 set 函数。

## 13.9 虚析构函数

在使用多态性处理类层次结构的动态分配对象时可能会出现问题。到目前为止，你看到的是非虚析构函数——未使用关键字 virtual 声明的析构函数。如果使用指向该对象的基类指针显式销毁具有非虚析构函数的派生类对象，则 C++ 标准规定行为未定义。

解决此问题的简单方法是，在基类中创建虚析构函数（即使用关键字 virtual 声明的析构函数）。这使得所有派生类析构函数都变为虚函数，即使它们不与基类析构函数具有相同的名称。现在，如果通过将 delete 运算符应用于基类指针来显式销毁层次结构中的对象，则将根据基类指针指向的对象调用适当类的析构函数。请记住，当派生类对象被销毁时，派生类对象的基类部分也会被销毁，因此派生类和基类的析构函数都执行很重要。基类析构函数在派生类析构函数之后自动执行。

### 错误预防提示 13.2

> 如果一个类具有虚函数，即使该类不需要，也应提供虚析构函数。这可确保当通过基类指针删除派生类对象时，如果存在自定义派生类析构函数，将被调用。

### 常见编程错误 13.5

> 构造函数不能是虚函数。声明构造函数为虚函数是编译错误。

## 13.10（可选）软件工程案例研究：将继承纳入 ATM 系统

我们现在重新审视 ATM 系统设计，看看它如何从继承中受益。为了应用继承，我们首先寻找系统中类之间的共同点。我们创建继承层次结构以更高效、更优雅地建模相似（但不完全相同）的类，从而能够以多态方式处理这些类的对象。然后我们修改类图以纳入新的继承关系。最后，我们演示更新后的设计如何被翻译成 C++ 头文件。

在第 3.11 节中，我们遇到了在系统中表示金融交易的问题。我们没有创建一个类来表示所有交易类型，而是决定创建三个单独的交易类——BalanceInquiry、Withdrawal 和 Deposit——来表示 ATM 系统可以执行的交易。图 13.26 显示了这些类的属性和操作。请注意，它们有一个共同的属性（accountNumber）和一个共同的操作（execute）。每个类都需要属性 accountNumber 来指定交易适用的账户。每个类都包含操作 execute，ATM 调用它来执行交易。显然，BalanceInquiry、Withdrawal 和 Deposit 代表交易类型。图 13.26 揭示了交易类之间的共同点，因此使用继承来提取共同特征似乎是设计这些类的合适方法。我们将通用功能放在基类 Transaction 中，并从 Transaction 派生类 BalanceInquiry、Withdrawal 和 Deposit（图 13.27）。

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_614_0.png)

图 13.26 | 类 BalanceInquiry、Withdrawal 和 Deposit 的属性和操作。

