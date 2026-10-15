
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

第 65 行在 `employees[i]` 指向的对象上调用成员函数 `earnings`。回顾一下，`earnings` 在基类中声明为 `virtual`，因此程序调用派生类对象的 `earnings` 函数——动态绑定的另一个例子。

第 69–76 行显示每个员工的对象的类型并使用 `delete` 运算符释放每个向量元素指向的动态内存。运算符 `typeid`（第 73 行）返回对类 `type_info` 的对象的引用，该对象包含有关其操作数的类型的信息，包括该类型的名称。调用时，`type_info` 成员函数 `name`（第 73 行）返回一个基于指针的字符串，其中包含传递给 `typeid` 的参数的类型名称（例如，"class BasePlusCommissionEmployee"）。要使用 `typeid`，程序必须包含头文件 `<typeinfo>`（第 16 行）。

### 可移植性提示 13.1

> `type_info` 成员函数 `name` 返回的字符串可能因编译器而异。

请注意，我们通过将 `Employee` 指针向下转型为 `BasePlusCommissionEmployee` 指针（第 50–52 行）避免了此示例中的几个编译错误。如果我们删除第 51 行的 `dynamic_cast` 并尝试将当前的 `Employee` 指针直接分配给 `BasePlusCommissionEmployee` 指针 `derivedPtr`，我们将收到编译错误。C++ 不允许程序将基类指针分配给派生类指针，因为 is-a 关系不适用——`CommissionEmployee` 不是 `BasePlusCommissionEmployee`。is-a 关系仅适用于派生类与其基类之间，而不适用于反向关系。

同样，如果第 58、60 和 62 行使用 `employees` 中的当前基类指针，而不是派生类指针 `derivedPtr`，来调用仅派生类函数 `getBaseSalary` 和 `setBaseSalary`，我们将在每一行都收到编译错误。正如你在第 13.3.3 节中所学，通过基类指针尝试调用仅派生类函数是不允许的。虽然第 58、60 和 62 行仅在 `commissionPtr` 不为 0 时执行（即可以执行转换时），但我们不能尝试在基类 `Employee` 指针上调用派生类 `BasePlusCommissionEmployee` 函数 `getBaseSalary` 和 `setBaseSalary`。请记住，使用基类 `Employee` 指针，我们只能调用在基类 `Employee` 中找到的函数——`earnings`、`print` 以及 `Employee` 的 `get` 和 `set` 函数。

## 13.9 虚析构函数

在使用多态性处理类层次结构的动态分配对象时可能会出现问题。到目前为止，你看到的是非虚析构函数——未使用关键字 `virtual` 声明的析构函数。如果使用指向该对象的基类指针显式销毁具有非虚析构函数的派生类对象，则 C++ 标准规定行为未定义。

解决此问题的简单方法是，在基类中创建虚析构函数（即使用关键字 `virtual` 声明的析构函数）。这使得所有派生类析构函数都变为虚函数，即使它们不与基类析构函数具有相同的名称。现在，如果通过将 `delete` 运算符应用于基类指针来显式销毁层次结构中的对象，则将根据基类指针指向的对象调用适当类的析构函数。请记住，当派生类对象被销毁时，派生类对象的基类部分也会被销毁，因此派生类和基类的析构函数都执行很重要。基类析构函数在派生类析构函数之后自动执行。

### 错误预防提示 13.2

> 如果一个类具有虚函数，即使该类不需要，也应提供虚析构函数。这可确保当通过基类指针删除派生类对象时，如果存在自定义派生类析构函数，将被调用。

### 常见编程错误 13.5

> 构造函数不能是虚函数。声明构造函数为虚函数是编译错误。

## 13.10（可选）软件工程案例研究：将继承纳入 ATM 系统

我们现在重新审视 ATM 系统设计，看看它如何从继承中受益。为了应用继承，我们首先寻找系统中类之间的共同点。我们创建继承层次结构以更高效、更优雅地建模相似（但不完全相同）的类，从而能够以多态方式处理这些类的对象。然后我们修改类图以纳入新的继承关系。最后，我们演示更新后的设计如何被翻译成 C++ 头文件。

在第 3.11 节中，我们遇到了在系统中表示金融交易的问题。我们没有创建一个类来表示所有交易类型，而是决定创建三个单独的交易类——`BalanceInquiry`、`Withdrawal` 和 `Deposit`——来表示 ATM 系统可以执行的交易。图 13.26 显示了这些类的属性和操作。请注意，它们有一个共同的属性（`accountNumber`）和一个共同的操作（`execute`）。每个类都需要属性 `accountNumber` 来指定交易适用的账户。每个类都包含操作 `execute`，ATM 调用它来执行交易。显然，`BalanceInquiry`、`Withdrawal` 和 `Deposit` 代表交易类型。图 13.26 揭示了交易类之间的共同点，因此使用继承来提取共同特征似乎是设计这些类的合适方法。我们将通用功能放在基类 `Transaction` 中，并从 `Transaction` 派生类 `BalanceInquiry`、`Withdrawal` 和 `Deposit`（图 13.27）。

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_614_0.png)

图 13.26 | 类 `BalanceInquiry`、`Withdrawal` 和 `Deposit` 的属性和操作。

UML 规定了一种称为*泛化*的关系来对继承建模。图 13.27 是对基类 `Transaction` 及其三个派生类之间的继承关系建模的类图。带有三角空心箭头的箭头表示类 `BalanceInquiry`、`Withdrawal` 和 `Deposit` 派生自类 `Transaction`。类 `Transaction` 被称为其派生类的泛化。这些派生类被称为类 `Transaction` 的*特化*。

类 `BalanceInquiry`、`Withdrawal` 和 `Deposit` 共享整数属性 `accountNumber`，因此我们将这一公共属性提取出来并放在基类 `Transaction` 中。我们不再在每个派生类的第二个分隔栏中列出 `accountNumber`，因为这三个派生类从 `Transaction` 继承了该属性。但请记住，派生类不能访问基类的私有属性。因此，我们在类 `Transaction` 中包含公共成员函数 `getAccountNumber`。每个派生类都继承该成员函数，使派生类能够在执行交易时按需访问其 `accountNumber`。

根据图 13.26，类 `BalanceInquiry`、`Withdrawal` 和 `Deposit` 还共享操作 `execute`，因此基类 `Transaction` 应包含公共成员函数 `execute`。然而，在类 `Transaction` 中实现 `execute` 没有意义，因为该成员函数提供的功能取决于实际交易的具体类型。因此，我们在基类 `Transaction` 中将成员函数 `execute` 声明为纯虚函数。这使 `Transaction` 成为抽象类，并强制任何派生自 `Transaction` 且必须是具体类（即 `BalanceInquiry`、`Withdrawal` 和 `Deposit`）的类实现纯虚成员函数 `execute`，以使派生类成为具体类。UML 要求我们将抽象类名（以及纯虚函数——UML 中的*抽象操作*）用斜体表示，因此 `Transaction` 及其成员函数 `execute` 在图 13.27 中以斜体显示。请注意，操作 `execute` 在派生类 `BalanceInquiry`、`Withdrawal` 和 `Deposit` 中并未使用斜体。每个派生类都以适当的实现覆盖基类 `Transaction` 的 `execute` 成员函数。请注意，图 13.27 在类 `BalanceInquiry`、`Withdrawal` 和 `Deposit` 的第三个分隔栏中包含了操作 `execute`，因为每个类对被覆盖的成员函数都有不同的具体实现。

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_615_0.png)

图 13.27 | 对基类 `Transaction` 与派生类 `BalanceInquiry`、`Withdrawal` 和 `Deposit` 之间的泛化关系建模的类图。

正如你在本章中所学，派生类可以从基类继承接口或实现。与为实现继承而设计的层次结构相比，为接口继承而设计的层次结构往往将其功能置于层次结构的较低位置——基类表示层次结构中每个类都应定义的一个或多个函数，但各个派生类提供自己的函数实现。为 ATM 系统设计的继承层次结构利用了这种类型的继承，它为 ATM 提供了一种以“一般”方式执行所有交易的优雅方法。每个派生自 `Transaction` 的类都继承了一些实现细节（例如数据成员 `accountNumber`），但将继承纳入我们系统的主要好处是派生类共享一个公共接口（例如纯虚成员函数 `execute`）。ATM 可以将 `Transaction` 指针指向任何交易，当 ATM 通过该指针调用 `execute` 时，适合该交易的 `execute` 版本（即在该派生类的 `.cpp` 文件中实现的版本）会自动运行。例如，假设用户选择执行余额查询。ATM 将 `Transaction` 指针指向类 `BalanceInquiry` 的一个新对象；编译器允许这样做，因为 `BalanceInquiry` 是一种 `Transaction`。当 ATM 使用该指针调用 `execute` 时，将调用 `BalanceInquiry` 版本的 `execute`。

这种多态方法也使系统易于扩展。如果我们希望创建一种新的交易类型（例如资金转账或账单支付），只需创建一个额外的 `Transaction` 派生类，用适合新交易类型的版本覆盖 `execute` 成员函数。我们只需要对系统代码进行最少的修改，以允许用户从主菜单选择新的交易类型，并让 ATM 实例化并执行新派生类的对象。ATM 可以使用当前代码执行新类型的交易，因为它以相同的方式执行所有交易。

正如你在本章前面所学到的，像 `Transaction` 这样的抽象类是你永远不会打算为其实例化对象的类。抽象类只是在继承层次结构中为其派生类声明公共属性和行为。类 `Transaction` 定义了作为具有账号并执行操作的交易意味着什么的概念。你可能会想，如果 `execute` 缺乏具体实现，为什么我们还要费心在类 `Transaction` 中包含纯虚成员函数 `execute`。从概念上讲，我们包含该成员函数是因为它是所有交易的定义性行为——执行。从技术上讲，我们必须将成员函数 `execute` 包含在基类 `Transaction` 中，以便 ATM（或任何其他类）可以通过 `Transaction` 指针或引用多态地调用每个派生类对此函数的覆盖版本。

派生类 `BalanceInquiry`、`Withdrawal` 和 `Deposit` 从基类 `Transaction` 继承属性 `accountNumber`，但类 `Withdrawal` 和 `Deposit` 包含额外的属性 `amount`，这使它们区别于类 `BalanceInquiry`。类 `Withdrawal` 和 `Deposit` 需要这个额外的属性来存储用户希望提取或存入的金额。类 `BalanceInquiry` 不需要这样的属性，只需要一个账号即可执行。尽管三个 `Transaction` 派生类中有两个共享此属性，但我们不会将其放在基类 `Transaction` 中——我们只将所有派生类共有的特性放在基类中，这样派生类就不会继承不必要的属性（和操作）。

图 13.28 展示了我们模型的更新类图，该图包含继承并引入了类 `Transaction`。我们对类 `ATM` 和类 `Transaction` 之间的关联进行建模，以表明在任何给定时刻，要么正在执行交易，要么没有执行（即系统中一次存在零个或一个 `Transaction` 类型的对象）。因为 `Withdrawal` 是 `Transaction` 的一种类型，我们不再直接在类 `ATM` 和类 `Withdrawal` 之间绘制关联线——派生类 `Withdrawal` 继承了基类 `Transaction` 与类 `ATM` 的关联。派生类 `BalanceInquiry` 和 `Deposit` 也继承此关联，这取代了先前省略的类 `BalanceInquiry` 和 `Deposit` 与类 `ATM` 之间的关联。再次注意使用三角空心箭头来表示类 `Transaction` 的特化，如图 13.27 所示。

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_617_0.png)

图 13.28 | ATM 系统的类图（包含继承）。请注意，抽象类名 `Transaction` 以斜体显示。

我们还在类 `Transaction` 和 `BankDatabase` 之间添加了一个关联（图 13.28）。所有交易都需要对 `BankDatabase` 的引用，以便访问和修改账户信息。每个 `Transaction` 派生类都继承此引用，因此我们不再对类 `Withdrawal` 和 `BankDatabase` 之间的关联建模。请注意，类 `Transaction` 和 `BankDatabase` 之间的关联取代了先前省略的类 `BalanceInquiry` 和 `Deposit` 与 `BankDatabase` 之间的关联。

我们还在类 `Transaction` 和 `Screen` 之间包含一个关联，因为所有交易都通过 `Screen` 向用户显示输出。每个派生类都继承此关联。因此，我们不再包含先前在 `Withdrawal` 和 `Screen` 之间建模的关联。类 `Withdrawal` 仍然参与与 `CashDispenser` 和 `Keypad` 的关联。我们不会将这些关联移到基类 `Transaction` 中。

该动作，因为与键盘（`Keypad`）的关联仅适用于取款（`Withdrawal`）和存款（`Deposit`）类，而与现金分配器（`CashDispenser`）的关联仅适用于取款类。

我们包含继承的类图（图13.28）也对存款（`Deposit`）和余额查询（`BalanceInquiry`）进行了建模。我们显示了存款类与存款槽（`DepositSlot`）和键盘（`Keypad`）之间的关联。注意，余额查询类除了从`Transaction`类继承的关联外，不参与任何其他关联——`BalanceInquiry`仅与`BankDatabase`和`Screen`交互。

图9.20中的类图展示了带有可见性标记的属性和操作。现在我们展示图13.29中的修改后的类图，其中包含了抽象基类`Transaction`。这个简化的图没有显示继承关系（这些关系出现在图13.28中），而是显示了我们系统中采用继承之后的属性和操作。注意，抽象类名`Transaction`和`Transaction`类中的抽象操作名`execute`以斜体显示。为了节省空间，如

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_618_0.png)

我们在图4.20中所做的那样，我们不包含图13.28中通过关联显示的属性——不过，我们会在附录E的C++实现中包含它们。我们还省略了所有操作参数，正如我们在图9.20中所做的那样——合并继承并不会影响已经在图6.34–6.37中建模的参数。

## 软件工程观察 13.12

> 一个完整的类图显示了类之间的所有关联以及每个类的所有属性和操作。当类属性、操作和关联的数量相当大时（如图13.28和图13.29所示），一种有助于提高可读性的良好做法是将这些信息分成两个类图——一个侧重于关联，另一个侧重于属性和操作。然而，在检查以这种方式建模的类时，必须同时考虑两个类图才能获得类的完整视图。例如，必须参考图13.28来观察`Transaction`与其派生类之间的继承关系，而图13.29中省略了该关系。

## 实现融入继承的ATM系统设计

- 1. 如果类A是类B的泛化，那么类B派生自（并且是类A的特化）。例如，抽象基类`Transaction`是类`Withdrawal`的泛化。因此，类`Withdrawal`派生自（并且是）类`Transaction`的特化。图13.30包含了类`Withdrawal`的头文件的一部分，其中类定义表明了`Withdrawal`和`Transaction`之间的继承关系（第9行）。

```
// Fig. 13.30: Withdrawal.h
// Definition of class Withdrawal that represents a withdrawal transaction
#ifndef WITHDRAWAL_H
#define WITHDRAWAL_H
#include "Transaction.h" // Transaction class definition
// class Withdrawal derives from base class Transaction
class Withdrawal : public Transaction
{
}; // end class Withdrawal
#endif // WITHDRAWAL_H
```
