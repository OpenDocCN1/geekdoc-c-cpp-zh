

## 防错技巧 12.1

![](img/b42ba5cd262b1358d16610173f975e4d_563_0.png)

对派生类中每个被重写的函数都使用 C++ 的 `override` 关键字。这会强制编译器检查基类是否存在同名且参数列表相同（即签名相同）的成员函数。如果没有，编译器将生成错误。

现在，如果我们将基类 `CommissionEmployee` 指针指向派生类 `BasePlusCommissionEmployee` 对象，并且程序使用该指针调用 `earnings` 或 `print` 函数，则将调用 `BasePlusCommissionEmployee` 对象的相应函数。由于 `CommissionEmployee` 和 `BasePlusCommissionEmployee` 类的成员函数实现没有改变，因此我们复用图 11.14 和 11.15 中的版本。

```cpp
// Fig. 12.4: CommissionEmployee.h
// CommissionEmployee class header declares earnings and print as virtual.
#ifndef COMMISSION_H
#define COMMISSION_H

#include <string> // C++ standard string class

class CommissionEmployee
{
public:
    CommissionEmployee( const std::string &, const std::string &,
        const std::string &, double = 0.0, double = 0.0 );

    void setFirstName( const std::string & ); // set first name
    std::string getFirstName() const; // return first name

    void setLastName( const std::string & ); // set last name
    std::string getLastName() const; // return last name

    void setSocialSecurityNumber( const std::string & ); // set SSN
    std::string getSocialSecurityNumber() const; // return SSN

    void setGrossSales( double ); // set gross sales amount
    double getGrossSales() const; // return gross sales amount

    void setCommissionRate( double ); // set commission rate
    double getCommissionRate() const; // return commission rate

    virtual double earnings() const; // calculate earnings
    virtual void print() const; // print object
private:
    std::string firstName;
    std::string lastName;
    std::string socialSecurityNumber;
    double grossSales; // gross weekly sales
    double commissionRate; // commission percentage
}; // end class CommissionEmployee

#endif
```

**图 12.4** | CommissionEmployee 类头文件将 earnings 和 print 声明为虚函数。

```cpp
// aim base-class pointer at derived-class object and print
commissionEmployeePtr = &basePlusCommissionEmployee;
cout << "\nCalling virtual function print with base-class pointer"
     << "\nto derived-class object invokes derived-class "
     << "print function:\n\n";

// polymorphism; invokes BasePlusCommissionEmployee's print;
// base-class pointer to derived-class object
commissionEmployeePtr->print();
cout << endl;
} // end main
```

```
Invoking print function on base-class and derived-class
objects with static binding

commission employee: Sue Jones
social security number: 222-22-2222
gross sales: 10000.00
commission rate: 0.06

base-salaried commission employee: Bob Lewis
social security number: 333-33-3333
gross sales: 5000.00
commission rate: 0.04
base salary: 300.00

Invoking print function on base-class and derived-class
objects with dynamic binding

Calling virtual function print with base-class pointer
to base-class object invokes base-class print function:

commission employee: Sue Jones
social security number: 222-22-2222
gross sales: 10000.00
commission rate: 0.06

Calling virtual function print with derived-class pointer
to derived-class object invokes derived-class print function:

base-salaried commission employee: Bob Lewis
social security number: 333-33-3333
gross sales: 5000.00
commission rate: 0.04
base salary: 300.00

Calling virtual function print with base-class pointer
to derived-class object invokes derived-class print function:

base-salaried commission employee: Bob Lewis
social security number: 333-33-3333
gross sales: 5000.00
commission rate: 0.04
base salary: 300.00

Note that the base salary is now displayed
```

**图 12.6** | 通过指向派生类对象的基类指针调用派生类虚函数，演示多态性。（第 2 部分，共 2 部分）

以及 ThreeDimensionalShape。层次结构的下一层为二维形状（即 Circle、Square 和 Triangle）和三维形状（即 Sphere、Cube 和 Tetrahedron）定义了具体类。

## 纯虚函数

一个类通过将其一个或多个虚函数声明为“纯”虚函数而成为抽象类。纯虚函数是通过在其声明中加上“= 0”来指定的，例如

```cpp
virtual void draw() const = 0; // pure virtual function
```

“= 0”是一个纯说明符。纯虚函数通常不提供实现，尽管它们也可以提供实现。每个具体派生类必须用这些函数的具体实现重写基类的所有纯虚函数；否则，该派生类也是抽象的。虚函数与纯虚函数的区别在于：虚函数有实现，并给派生类重写该函数的选择权；相比之下，纯虚函数没有实现，并要求派生类重写该函数，该派生类才能成为具体类；否则派生类仍然是抽象的。

当基类为某个函数提供实现没有意义，但你又希望所有具体派生类都实现该函数时，应使用纯虚函数。回到之前关于太空对象的示例，基类 `SpaceObject` 为 `draw` 函数提供实现是没有意义的（因为如果不知道正在绘制的太空对象的具体类型，就无法绘制一个通用的太空对象）。一个可以定义为虚函数（而非纯虚函数）的示例是返回对象名称的函数。我们可以为一个通用的 `SpaceObject` 命名（例如称为“太空对象”），因此可以为该函数提供默认实现，并且该函数不需要是纯虚函数。然而，该函数仍然声明为虚函数，因为预期派生类会重写此函数，以便为派生类对象提供更具体的名称。

> **软件工程观察 12.9**
> 
> 抽象类为类层次结构中的各个类定义了共同的公共接口。抽象类包含一个或多个具体派生类必须重写的纯虚函数。

> **常见编程错误 12.2**
> 
> 在派生类中未能重写纯虚函数会使该类成为抽象类。试图实例化抽象类的对象会导致编译错误。

> **软件工程观察 12.10**
> 
> 抽象类至少有一个纯虚函数。抽象类还可以拥有数据成员和具体函数（包括构造函数和析构函数），这些成员和函数遵循派生类继承的常规规则。

虽然我们不能实例化抽象基类的对象，但可以使用抽象基类声明指针和引用，这些指针和引用可以指向任何具体类的对象

![](img/b42ba5cd262b1358d16610173f975e4d_571_0.png)

**图 12.7** Employee 层次结构 UML 类图。

> **软件工程观察 12.11**
> 
> 派生类可以从基类继承接口和/或实现。为实现继承而设计的层次结构往往将其功能放在层次结构的高层——一个丰富且非常通用的类继承在基类中定义的一个或多个成员/函数，派生类使用基类的定义。为接口继承而设计的层次结构往往将其功能放在层次结构的较低层——基类指定层次结构中每个类都应定义的一个或多个函数（即它们具有相同的原型），但各个派生类提供自己的函数实现。

接下来的章节将实现 Employee 类层次结构。前五节分别实现一个抽象类或具体类。最后一节实现一个测试程序，该程序构建所有这些类的对象并以多态方式处理这些对象。

### 12.6.1 创建抽象基类 Employee

类 Employee（图 12.9–12.10，稍后将详细讨论）除了提供各种操作 Employee 的数据成员的 get 和 set 函数外，还提供了 earnings 和 print 函数。earnings 函数当然普遍适用于所有雇员，但每次 earnings 的计算都取决于雇员的类。因此，我们将 earnings 声明为基类 Employee 中的纯虚函数，因为对该函数而言，*默认实现没有意义*——没有足够的信息来确定 earnings 应返回的金额。每个派生类都用适当的实现*重写* earnings。为了计算雇员的 earnings，程序将雇员对象的地址赋给基类 Employee *指针*，然后在该对象上调用 earnings 函数。我们维护一个 Employee 指针的 vector，每个指针都指向一个 Employee 对象。*当然，不可能存在 Employee 对象，因为 Employee 是抽象类——然而，由于继承，Employee 的所有具体派生类的所有对象仍然可以被认为是 Employee 对象。* 程序遍历该 vector，并为每个 Employee 对象调用 earnings 函数。C++ *以多态方式*处理这些函数调用。将 earnings 作为 Employee 中的纯虚函数，*强制*每个希望成为*具体类*的 Employee 直接派生类重写 earnings。

类 Employee 中的 print 函数显示雇员的名字、姓氏和社会安全号码。正如我们将看到的，Employee 的每个派生类都重写了函数

