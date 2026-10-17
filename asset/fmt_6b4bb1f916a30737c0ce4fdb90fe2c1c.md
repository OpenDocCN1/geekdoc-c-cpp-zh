
图 12.26 | 构造函数和析构函数调用顺序。（第 3 部分，共 3 部分。）

## 12.6 `public`、`protected` 和 `private` 继承

在从基类派生类时，基类可以通过 `public`、`protected` 或 `private` 继承。`protected` 和 `private` 继承使用较少，且应谨慎使用；本书中我们通常使用 `public` 继承。图 12.27 总结了每种继承类型的派生类中基类成员的可访问性。第一列包含基类的访问说明符。

从 `public` 基类派生时，基类的 `public` 成员变为派生类的 `public` 成员，基类的 `protected` 成员变为派生类的 `protected` 成员。基类的 `private` 成员永远不能直接从派生类访问，但可以通过调用基类的 `public` 和 `protected` 成员来访问。

从 `protected` 基类派生时，基类的 `public` 和 `protected` 成员变为派生类的 `protected` 成员。从 `private` 基类派生时，基类的 `public` 和 `protected` 成员变为派生类的 `private` 成员（例如，函数变为实用函数）。`private` 和 `protected` 继承不是 `is-a` 关系。

| 基类成员访问说明符 | 继承类型 |  |  |
| --- | --- | --- | --- |
|  | `public` 继承 | `protected` 继承 | `private` 继承 |
| `public` | 派生类中为 `public`。<br><br>可被成员函数、`friend` 函数和非成员函数直接访问。 | 派生类中为 `protected`。<br><br>可被成员函数和 `friend` 函数直接访问。 | 派生类中为 `private`。<br><br>可被成员函数和 `friend` 函数直接访问。 |
| `protected` | 派生类中为 `protected`。<br><br>可被成员函数和 `friend` 函数直接访问。 | 派生类中为 `protected`。<br><br>可被成员函数和 `friend` 函数直接访问。 | 派生类中为 `private`。<br><br>可被成员函数和 `friend` 函数直接访问。 |
| `private` | 在派生类中隐藏。<br><br>可通过基类的 `public` 或 `protected` 成员函数由成员函数和 `friend` 函数访问。 | 在派生类中隐藏。<br><br>可通过基类的 `public` 或 `protected` 成员函数由成员函数和 `friend` 函数访问。 | 在派生类中隐藏。<br><br>可通过基类的 `public` 或 `protected` 成员函数由成员函数和 `friend` 函数访问。 |

图 12.27 | 派生类中基类成员可访问性的汇总。

## 12.7 使用继承进行软件工程

在本节中，我们讨论使用继承来自定义现有软件。当我们使用继承从现有类创建新类时，新类继承现有类的数据成员和成员函数，如图 12.27 所描述。我们可以通过包含附加成员并重新定义基类成员来自定义新类以满足我们的需求。派生类程序员在 C++ 中无需访问基类的源代码即可完成此操作。派生类必须能够链接到基类的目标代码。这种强大的功能对独立软件供应商（ISVs）具有吸引力。ISVs 可以开发专有类以供销售或许可，并以目标代码格式提供给用户。然后用户可以从这些库类派生新类，快速且无需访问 ISV 的专有源代码。所有 ISV 需要提供的只是头文件。

有时很难体会到在工业界从事大规模软件项目设计人员所面临问题的范围。经验丰富的人说，有效的软件重用可以改善软件开发过程。面向对象编程促进了软件重用，从而缩短了开发时间并提高了软件质量。

可用的大量且有用的类库通过继承提供了软件重用的最大好处。正如独立软件厂商生产的即装即用软件随着个人电脑的到来而成为爆炸性增长的行业，对类库的创建和销售的兴趣也在呈指数级增长。应用程序设计人员用这些库构建他们的应用程序，而库设计人员则通过其库被包含在应用程序中而获得回报。随 C++ 编译器提供的标准 C++ 库往往比较通用且范围有限。然而，世界范围内对为各种各样的应用领域开发类库的投入是巨大的。

### 软件工程观察 12.9

> 在面向对象系统的设计阶段，设计人员经常确定某些类密切相关。设计人员应“提取”共同的属性和行为并将其放在基类中，然后使用继承形成派生类，使其具有超出基类继承的能力。

### 软件工程观察 12.10

> 创建派生类不会影响其基类的源代码。继承保持了基类的完整性。

### 软件工程观察 12.11

> 正如非面向对象系统的设计人员应避免函数的泛滥，面向对象系统的设计人员也应避免类的泛滥。类的泛滥会造成管理问题，并可能阻碍软件重用，因为客户端很难在庞大的类库中找到最合适的类。替代方案是创建提供更实质性功能的更少类，但此类类可能提供太多功能。

### 性能提示 12.3

> 如果通过继承产生的类比所需的大，即包含太多功能，可能会浪费内存和处理资源。从功能“最接近”所需内容的类继承。

阅读派生类定义可能会令人困惑，因为继承的成员在派生类中没有物理显示，但仍然存在。记录派生类成员时存在类似问题。

## 12.8 总结

本章介绍了继承——通过吸收现有类的成员数据和成员函数并对其进行增强以添加新功能来创建类的能力。通过使用员工继承层次结构的一系列示例，您学习了基类和派生类的概念，并使用 `public` 继承创建了从基类继承成员的派生类。本章介绍了访问说明符 `protected`——派生类成员函数可以访问受保护的基类成员。您学习了如何通过基类名和二进制作用域解析运算符（`::`）限定其名称来访问重新定义的基类成员。您还看到了继承层次结构中类的对象构造器和析构器的调用顺序。最后，我们解释了三种继承类型——`public`、`protected` 和 `private`——以及使用每种类型时基类成员在派生类中的可访问性。

在第 13 章《面向对象编程：多态性》中，我们将在继承的讨论基础上，通过引入多态性——面向对象概念，使我们能够以更通用方式处理由继承相关的大量类对象编写程序。学习完第 13 章后，您将熟悉类、对象、封装、继承和多态性——面向对象编程的基本概念。

# 13 面向对象编程：多态性

## 目标

在本章中您将学习：

- 多态性是什么，它如何使编程更方便，以及它如何使系统更具可扩展性和可维护性。
- 如何声明和使用虚函数来实现多态性。
- 抽象类和具体类之间的区别。
- 如何声明纯虚函数以创建抽象类。
- 如何使用运行时类型信息（RTTI）进行向下转换、`dynamic_cast`、`typeid` 和 `type_info`。
- C++ 如何在“幕后”实现虚函数和动态绑定。
- 如何使用虚析构函数确保对象上的所有适当析构函数都能运行。

> 一枚戒指统御众戒，
> 一枚戒指寻获众戒，
> 一枚戒指引众戒至，
> 并使它们在黑暗中缚之。
> — 约翰·罗纳德·鲁埃尔·托尔金

> 纯洁无辜的沉默
> 往往胜于言语
> 说服于失败之时。
> — 威廉·莎士比亚

> 一般性命题并不能决定具体案例。
> — 奥利弗·温德尔·霍姆斯

> 具有令人印象深刻身材的哲学家并不是在真空中思考。即使他最抽象的想法也在一定程度上受制于他生活时代已知或未知的东西。
> — 阿尔弗雷德·诺斯·怀特海

- 13.1 引言
- 13.2 多态性示例
- 13.3 继承层次结构中对象之间的关系
- 13.3.1 从派生类对象调用基类函数
- 13.3.2 将派生类指针指向基类对象
- 13.3.3 通过基类指针调用派生类成员函数
- 13.3.4 虚函数
- 13.3.5 基类和派生类对象及指针之间允许赋值的汇总
- 13.4 类型字段和 switch 语句
- 13.5 抽象类和纯虚函数
- 13.6 案例研究：使用多态性的工资系统
- 13.6.1 创建抽象基类 `Employee`
- 13.6.2 创建具体派生类 `SalariedEmployee`
- 13.6.3 创建具体派生类 `HourlyEmployee`
- 13.6.4 创建具体派生类 `CommissionEmployee`
- 13.6.5 创建间接具体派生类 `BasePlusCommissionEmployee`
- 13.6.6 演示多态处理
- 13.7 （可选）多态性、虚函数和动态绑定“幕后”
- 13.8 案例研究：使用多态性和运行时类型信息进行向下转换、`dynamic_cast`、`typeid` 和 `type_info` 的工资系统
- 13.9 虚析构函数
- 13.10 （可选）软件工程案例研究：将继承纳入 ATM 系统
- 13.11 总结

## 13.1 引言

在第 9–12 章中，我们讨论了包括类、对象、封装、运算符重载和继承在内的关键面向对象编程技术。我们现在继续研究 OOP，通过使用继承层次结构解释和演示多态性。多态性使我们能够“以一般方式编程”而不是“以具体方式编程”。特别是，多态性使我们能够编写处理属于同一类层次结构的类的对象的程序，就好像它们都是层次结构基类的对象一样。正如我们很快会看到的，多态性基于基类指针句柄和基类引用句柄工作，但不基于名称句柄。

考虑以下多态性示例。假设我们创建一个程序来模拟几种动物的运动，用于生物学研究。类 `Fish`、`Frog` 和 `Bird` 代表研究的三种动物类型。想象一下，这些类都继承自基类 `Animal`，该基类包含一个 `move()` 函数并维护动物的当前位置。每个派生类都实现了 `move()` 函数。我们的程序维护一个指向各种 `Animal` 派生类对象的指针向量。为了模拟动物的移动，程序每秒向每个对象发送相同的消息——即 `move()`。然而，每种特定的 `Animal` 类型对 `move()` 消息的响应方式各不相同——一条 `Fish` 可能会游两英尺，一只 `Frog` 可能会跳三英尺，而一只 `Bird` 可能会飞十英尺。程序以通用方式向每个动物对象发出相同的消息（即 `move()`），但每个对象都知道如何根据其特定的移动类型适当修改自己的位置。依赖每个对象知道如何“做正确的事情”（即，对同一函数调用做出对该类型对象适当的行为）是多态性的关键概念。发送给各种对象的同一条消息（在本例中为 `move()`）会产生“多种形式”的结果——因此得名多态性。

有了多态性，我们可以设计和实现易于扩展的系统——只要新类属于程序以通用方式处理的继承层次结构，就可以在几乎不修改程序的通用部分的情况下添加新类。程序中必须修改以适应新类的唯一部分是那些需要直接了解你添加到层次结构中的新类的部分。例如，如果我们创建继承自类 `Animal` 的类 `Tortoise`（它可能会对 `move()` 消息的响应为爬行一英寸），我们只需要编写 `Tortoise` 类和模拟中实例化 `Tortoise` 对象的部分。模拟中以通用方式处理每个 `Animal` 的部分可以保持不变。

我们首先通过一系列小而专注的示例开始，这些示例逐步引出对虚函数和动态绑定的理解——多态性的两个底层技术。然后我们介绍一个案例研究，重访第 12 章的 `Employee` 层次结构。在案例研究中，我们为层次结构中的所有类定义了一个共同的“接口”（即功能集）。员工之间的这种共同功能定义在所谓的抽象基类 `Employee` 中，类 `SalariedEmployee`、`HourlyEmployee` 和 `CommissionEmployee` 直接从其继承，而类 `BaseCommissionEmployee` 间接继承。我们很快就会看到是什么使一个类“抽象”或其相反——“具体”。

在这个层次结构中，每个员工都有一个 `earnings()` 函数来计算员工的周薪。这些 `earnings()` 函数因员工类型而异——例如，`SalariedEmployee` 无论工作小时数多少都按固定周薪支付，而 `HourlyEmployee` 按小时计酬并获得加班费。我们展示了如何以“通用”方式处理每个员工——即，使用基类指针调用多个派生类对象的 `earnings()` 函数。这样，你只需关心一种类型的函数调用，该调用可用于根据基类指针引用的对象执行几种不同的函数。

本章的一个关键特性是其（可选的）对多态性、虚函数和动态绑定“内部”工作原理的详细讨论，其中使用详细的图表来解释 C++ 中多态性的实现方式。

在执行多态处理时，有时我们需要以“具体”方式编程，这意味着需要在层次结构中对特定类型的对象执行操作——该操作不能普遍应用于几种类型的对象。我们重用 `Employee` 层次结构来演示运行时类型信息（RTTI）和动态转换的强大功能，这些功能使程序能够在执行时确定对象的类型并相应地对其进行操作。我们使用这些功能来确定特定员工对象是否为 `BasePlusCommissionEmployee`，然后给该员工的底薪增加 10% 的奖金。

## 13.2 多态示例

在本节中，我们讨论几个多态示例。有了多态，一个函数可以根据调用该函数的对象的类型导致不同的动作发生。这给了你极大的表达能力。如果类 `Rectangle` 派生自类 `Quadrilateral`，那么 `Rectangle` 对象是 `Quadrilateral` 对象的更具体版本。因此，可以对 `Quadrilateral` 类对象执行的任何操作（例如计算周长或面积）也可以对 `Rectangle` 类对象执行。这种操作也可以对其他类型的 `Quadrilateral` 执行，例如 `Squares`、`Parallelograms` 和 `Trapezoids`。当程序通过基类（即 `Quadrilateral`）指针或引用调用虚函数时，多态性就会发生——C++ 动态（即在执行时）为对象实例化的类选择正确的函数。你将在第 13.3 节看到一个说明此过程的代码示例。

作为另一个例子，假设我们设计一个操纵许多不同类型对象的视频游戏，包括类 `Martian`、`Venutian`、`Plutonian`、`SpaceShip` 和 `LaserBeam` 的对象。想象一下，这些类都继承自共同的基类 `SpaceObject`，该基类包含成员函数 `draw()`。每个派生类以适合该类的方式实现此函数。屏幕管理器程序维护一个容器（例如 `vector`），其中保存指向各种类对象的 `SpaceObject` 指针。为了刷新屏幕，屏幕管理器会定期向每个对象发送相同的消息——即 `draw()`。每种类型的对象以独特的方式响应。例如，`Martian` 对象可能会用适当数量的天线以红色绘制自己。`SpaceShip` 对象可能会将其绘制为银色飞行器。`LaserBeam` 对象可能会将其绘制为屏幕上的一道明亮红色光束。再次，发送给各种对象的同一条消息（在本例中为 `draw()`）会产生“多种形式”的结果。

多态屏幕管理器有助于以最少的代码修改将新类添加到系统中。假设我们想在视频游戏中添加类 `Mercurian` 的对象。为此，我们必须构建一个继承自 `SpaceObject` 的类 `Mercurian`，但提供成员函数 `draw()` 的自己的定义。然后，当容器中出现指向类 `Mercurian` 对象的指针时，你无需修改屏幕管理器的代码。屏幕管理器在容器中的每个对象上调用成员函数 `draw()`，而不管对象的类型，因此新的 `Mercurian` 对象只需“即插即用”。因此，在构建和包含类本身之外，无需修改系统，程序员就可以使用多态来适应额外的类，包括系统创建时甚至未曾设想的类。

### 软件工程观察 13.1

> 有了虚函数和多态性，你可以处理一般性问题，让执行时环境关心具体细节。你可以指示各种对象以适合这些对象的方式表现，而甚至不知道它们的类型（只要这些对象属于同一个继承层次结构，并且是通过共同的基类指针访问的）。

### 软件工程观察 13.2

> 多态性促进可扩展性：为调用多态行为而编写的软件独立于发送消息的对象的类型。因此，可以将能够响应现有消息的新类型对象合并到此类系统中，而无需修改基本系统。唯一需要修改以适应新类型的客户端代码是实例化新对象的代码。

## 13.3 继承层次结构中对象之间的关系

第 12.4 节创建了一个员工类层次结构，其中类 `BasePlusCommissionEmployee` 继承自类 `CommissionEmployee`。第 12 章的示例通过使用对象的名称调用其成员函数来操作 `CommissionEmployee` 和 `BasePlusCommissionEmployee` 对象。我们现在更详细地检查层次结构中类之间的关系。接下来的几节展示了一系列示例，演示了基类指针和派生类指针如何指向基类对象和派生类对象，以及如何使用这些指针调用操作这些对象的成员函数。在第 13.3.4 节中，我们演示了如何从指向派生类对象的基类指针获得多态行为。

在第 13.3.1 节中，我们将派生类对象的地址赋给基类指针，然后显示通过基类指针调用函数会调用基类功能——即，句柄的类型决定了调用哪个函数。在第 13.3.2 节中，我们将基类对象的地址赋给派生类指针，这会导致编译错误。我们讨论错误消息并调查编译器为何不允许此类赋值。在第 13.3.3 节中，我们将派生类对象的地址赋给基类指针，然后检查基类指针如何用于仅调用基类功能——当我们尝试通过基类指针调用派生类成员函数时，会出现编译错误。最后，在第 13.3.4 节中，我们通过将基类函数声明为 `virtual` 来引入虚函数和多态性。然后我们将派生类对象的地址赋给基类指针并使用该指针调用派生类功能——这正是我们实现多态行为所需的关键能力。

这些示例中的一个关键概念是演示派生类的对象可以被视为其基类的对象。这使得各种有趣的操作成为可能。例如，程序可以创建一个基类指针数组，这些指针指向许多派生类类型的对象。尽管派生类对象类型不同，但编译器允许这样做，因为每个派生类对象 *都是* 其基类的对象。然而，我们不能将基类对象视为其任何派生类的对象。例如，在第 12 章定义的层次结构中，`CommissionEmployee` 并不是 `BasePlusCommissionEmployee`——`CommissionEmployee` 没有 `baseSalary` 数据成员，也没有成员函数 `setBaseSalary()` 和 `getBaseSalary()`。*is-a* 关系仅从派生类到其直接和间接基类适用。

### 13.3.1 从派生类对象调用基类函数

图 13.1–13.5 中的示例演示了三种将基类指针和派生类指针指向基类对象和派生类对象的方法。前两种很直接——我们将基类指针指向基类对象（并调用基类功能），并将派生类指针指向派生类对象（并调用派生类功能）。然后，我们通过将基类指针指向派生类对象（并显示基类功能确实在派生类对象中可用）来演示派生类与基类之间的关系（即继承的 *is-a* 关系）。

类 `CommissionEmployee`（图 13.1–13.2），我们在第 12 章中讨论过，用于表示按销售额百分比获得报酬的员工。类 `BasePlusCommissionEmployee`

```cpp
// Fig. 13.2: CommissionEmployee.cpp
// Class CommissionEmployee member-function definitions.
#include <iostream>
using std::cout;

#include "CommissionEmployee.h" // CommissionEmployee class definition

// constructor
CommissionEmployee::CommissionEmployee(
    const string &first, const string &last, const string &ssn,
    double sales, double rate )
    : firstName( first ), lastName( last ), socialSecurityNumber( ssn )
{
    setGrossSales( sales ); // validate and store gross sales
    setCommissionRate( rate ); // validate and store commission rate
} // end CommissionEmployee constructor

// set first name
void CommissionEmployee::setFirstName( const string &first )
{
    firstName = first; // should validate
} // end function setFirstName

// return first name
string CommissionEmployee::getFirstName() const
{
    return firstName;
} // end function getFirstName

// set last name
void CommissionEmployee::setLastName( const string &last )
{
    lastName = last; // should validate
} // end function setLastName

// return last name
string CommissionEmployee::getLastName() const
{
    return lastName;
} // end function getLastName

// set social security number
void CommissionEmployee::setSocialSecurityNumber( const string &ssn )
{
    socialSecurityNumber = ssn; // should validate
} // end function setSocialSecurityNumber

// return social security number
string CommissionEmployee::getSocialSecurityNumber() const
{
    return socialSecurityNumber;
} // end function getSocialSecurityNumber

// set gross sales amount
void CommissionEmployee::setGrossSales( double sales )
{
   grossSales = ( sales < 0.0 ) ? 0.0 : sales;
} // end function setGrossSales

// return gross sales amount
double CommissionEmployee::getGrossSales() const
{
   return grossSales;
} // end function getGrossSales

// set commission rate
void CommissionEmployee::setCommissionRate( double rate )
{
   commissionRate = ( rate > 0.0 && rate < 1.0 ) ? rate : 0.0;
} // end function setCommissionRate

// return commission rate
double CommissionEmployee::getCommissionRate() const
{
   return commissionRate;
} // end function getCommissionRate

// calculate earnings
double CommissionEmployee::earnings() const
{
   return getCommissionRate() * getGrossSales();
} // end function earnings

// print CommissionEmployee object
void CommissionEmployee::print() const
{
   cout << "commission employee: "
        << getFirstName() << ' ' << getLastName()
        << "\nsocial security number: " << getSocialSecurityNumber()
        << "\ngross sales: " << getGrossSales()
        << "\ncommission rate: " << getCommissionRate();
} // end function print
```

**图 13.2 |** `CommissionEmployee` 类实现文件。（第 2 部分，共 2 部分。）

```cpp
// Fig. 13.3: BasePlusCommissionEmployee.h
// BasePlusCommissionEmployee class derived from class
// CommissionEmployee.
#ifndef BASEPLUS_H
#define BASEPLUS_H

#include <string> // C++ standard string class
using std::string;

#include "CommissionEmployee.h" // CommissionEmployee class declaration
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

**图 13.3 |** `BasePlusCommissionEmployee` 类头文件。（第 1 部分，共 2 部分。）

**图 13.3 |** `BasePlusCommissionEmployee` 类头文件。（第 2 部分，共 2 部分。）

```cpp
// Fig. 13.4: BasePlusCommissionEmployee.cpp
// Class BasePlusCommissionEmployee member-function definitions.
#include <iostream>
using std::cout;

// BasePlusCommissionEmployee class definition
#include "BasePlusCommissionEmployee.h"

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
    baseSalary = ( salary < 0.0 ) ? 0.0 : salary;
} // end function setBaseSalary

// return base salary
double BasePlusCommissionEmployee::getBaseSalary() const
{
    return baseSalary;
} // end function getBaseSalary

// calculate earnings
double BasePlusCommissionEmployee::earnings() const
{
    return getBaseSalary() + CommissionEmployee::earnings();
} // end function earnings

// print BasePlusCommissionEmployee object
void BasePlusCommissionEmployee::print() const
{
    cout << "base-salaried ";

    // invoke CommissionEmployee's print function
    CommissionEmployee::print();

    cout << "\nbase salary: " << getBaseSalary();
} // end function print
```

**图 13.4 |** `BasePlusCommissionEmployee` 类实现文件。（第 1 部分，共 2 部分。）

**图 13.4 |** `BasePlusCommissionEmployee` 类实现文件。（第 2 部分，共 2 部分。）

在图 13.5 中，第 19–20 行创建了一个 `CommissionEmployee` 对象，第 23 行创建了一个指向 `CommissionEmployee` 对象的指针；第 26–27 行创建了一个 `BasePlusCommissionEmployee` 对象，第 30 行创建了一个指向 `BasePlusCommissionEmployee` 对象的指针。第 37 和 39 行分别使用每个对象的名称（`commissionEmployee` 和 `basePlusCommissionEmployee`）来调用每个对象的 `print()` 成员函数。第 42 行将基类对象 `commissionEmployee` 的地址赋给基类指针 `commissionEmployeePtr`，第 45 行使用该指针在该 `CommissionEmployee` 对象上调用成员函数 `print()`。这调用了基类 `CommissionEmployee` 中定义的 `print()` 版本。类似地，第 48 行将派生类对象 `basePlusCommissionEmployee` 的地址赋给派生类指针 `basePlusCommissionEmployeePtr`，第 52 行使用该指针在该 `BasePlusCommissionEmployee` 对象上调用成员函数 `print()`。这调用了派生类 `BasePlusCommissionEmployee` 中定义的 `print()` 版本。第 55 行然后将派生类对象 `basePlusCommissionEmployee` 的地址赋给基类指针 `commissionEmployeePtr`，第 59 行使用该指针调用成员函数 `print()`。这种“crossover”是允许的，因为派生类的对象就是其基类的对象。注意，尽管基类

**图 13.5 |** 将基类和派生类对象的地址赋给基类和派生类指针。（第 1 部分，共 3 部分。）

```cpp
// Fig. 13.5: fig13_05.cpp
// Aiming base-class and derived-class pointers at base-class
// and derived-class objects, respectively.
#include <iostream>
using std::cout;
using std::endl;
using std::fixed;

#include <iomanip>
using std::setprecision;

// include class definitions
#include "CommissionEmployee.h"
#include "BasePlusCommissionEmployee.h"

int main()
{
   // create base-class object
   CommissionEmployee commissionEmployee(
      "Sue", "Jones", "222-22-2222", 10000, .06 );

   // create base-class pointer
   CommissionEmployee *commissionEmployeePtr = 0;

   // create derived-class object
   BasePlusCommissionEmployee basePlusCommissionEmployee(
      "Bob", "Lewis", "333-33-3333", 5000, .04, 300 );

   // create derived-class pointer
   BasePlusCommissionEmployee *basePlusCommissionEmployeePtr = 0;

   // set floating-point output formatting
   cout << fixed << setprecision( 2 );

   // output objects commissionEmployee and basePlusCommissionEmployee
   cout << "Print base-class and derived-class objects:\n\n";
   commissionEmployee.print(); // invokes base-class print
   cout << "\n\n";
   basePlusCommissionEmployee.print(); // invokes derived-class print

   // aim base-class pointer at base-class object and print
   commissionEmployeePtr = &commissionEmployee; // perfectly natural
   cout << "\n\nCalling print with base-class pointer to "
        << "\nbase-class object invokes base-class print function:\n\n";
   commissionEmployeePtr->print(); // invokes base-class print

   // aim derived-class pointer at derived-class object and print
   basePlusCommissionEmployeePtr = &basePlusCommissionEmployee; // natural
   cout << "\n\nCalling print with derived-class pointer to "
        << "\nderived-class object invokes derived-class "
        << "print function:\n\n";
   basePlusCommissionEmployeePtr->print(); // invokes derived-class print

   // aim base-class pointer at derived-class object and print
   commissionEmployeePtr = &basePlusCommissionEmployee;
   cout << "\n\nCalling print with base-class pointer to "
        << "\nderived-class object\ninvokes base-class print "
        << "function on that derived-class object:\n\n";
   commissionEmployeePtr->print(); // invokes base-class print
   cout << endl;
   return 0;
} // end main
```

**图 13.5 |** 将基类和派生类对象的地址赋给基类和派生类指针。（第 2 部分，共 3 部分。）

```text
打印基类和派生类对象：

佣金雇员：Sue Jones
社保号：222-22-2222
总销售额：10000.00
佣金率：0.06

带基本工资的佣金雇员：Bob Lewis
社保号：333-33-3333
总销售额：5000.00
佣金率：0.04
基本工资：300.00

调用 print（基类指针指向基类对象）时，将调用基类的 print 函数：

佣金雇员：Sue Jones
社保号：222-22-2222
总销售额：10000.00
佣金率：0.06

调用 print（派生类指针指向派生类对象）时，将调用派生类的 print 函数：

带基本工资的佣金雇员：Bob Lewis
社保号：333-33-3333
总销售额：5000.00
佣金率：0.04
基本工资：300.00

调用 print（基类指针指向派生类对象）时，将对该派生类对象调用基类的 print 函数：

佣金雇员：Bob Lewis
社保号：333-33-3333
总销售额：5000.00
佣金率：0.04
```

**图 13.5 |** 将基类和派生类对象的地址赋值给基类和派生类指针。（第 3 部分，共 3 部分。）

当 `CommissionEmployee` 指针指向派生类 `BasePlusCommissionEmployee` 对象时，会调用基类 `CommissionEmployee` 的 `print()` 成员函数（而不是 `BasePlusCommissionEmployee` 的 `print()` 函数）。本程序中每次 `print()` 成员函数调用的输出表明，被调用的功能取决于用于调用函数的句柄类型（即指针或引用类型），而不是句柄所指向对象的类型。在 13.3.4 节中，当引入虚函数时，我们将证明可以调用对象类型的功能，而不是句柄类型的功能。我们将看到，这对实现多态行为至关重要——这是本章的关键主题。

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_577_0.png)

### 13.3.3 通过基类指针调用派生类成员函数

通过基类指针，编译器只允许我们调用基类成员函数。因此，如果基类指针指向派生类对象，并试图访问仅存在于派生类的成员函数，就会发生编译错误。

图 13.7 显示了试图通过基类指针调用派生类成员函数的后果。注意：我们再次使用图 13.1–13.4 中的类 `CommissionEmployee` 和 `BasePlusCommissionEmployee`。第 9 行创建了 `commissionEmployeePtr`——一个指向 `CommissionEmployee` 对象的指针——第 10-11 行创建了一个 `BasePlusCommissionEmployee` 对象。第 14 行让 `commissionEmployeePtr` 指向派生类对象 `basePlusCommissionEmployee`。回顾 13.3.1 节，这种操作是允许的。
