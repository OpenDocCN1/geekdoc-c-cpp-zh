
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

图13.5 | 将基类和派生类对象的地址赋值给基类和派生类指针。（第3部分，共3部分。）

当 CommissionEmployee 指针指向派生类 BasePlusCommissionEmployee 对象时，会调用基类 CommissionEmployee 的 print 成员函数（而不是 BasePlusCommissionEmployee 的 print 函数）。本程序中每次 print 成员函数调用的输出表明，被调用的功能取决于用于调用函数的句柄类型（即指针或引用类型），而不是句柄所指向对象的类型。在13.3.4节中，当引入虚函数时，我们将证明可以调用对象类型的功能，而不是句柄类型的功能。我们将看到，这对实现多态行为至关重要——这是本章的关键主题。

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_577_0.png)

## 13.3.3 通过基类指针调用派生类成员函数

通过基类指针，编译器只允许我们调用基类成员函数。因此，如果基类指针指向派生类对象，并试图访问仅存在于派生类的成员函数，就会发生编译错误。

图13.7 显示了试图通过基类指针调用派生类成员函数的后果。注意：我们再次使用图13.1–13.4中的类 CommissionEmployee 和 BasePlusCommissionEmployee。第9行创建了 commissionEmployeePtr——一个指向 CommissionEmployee 对象的指针——第10-11行创建了一个 BasePlusCommissionEmployee 对象。第14行让 commissionEmployeePtr 指向派生类对象 basePlusCommissionEmployee。回顾13.3.1节，这种操作是允许的，

```cpp
// Fig. 13.7: fig13_07.cpp
// Attempting to invoke derived-class-only member functions
// through a base-class pointer.
#include "CommissionEmployee.h"
#include "BasePlusCommissionEmployee.h"

int main()
{
    CommissionEmployee *commissionEmployeePtr = 0; // base class
    BasePlusCommissionEmployee basePlusCommissionEmployee(
        "Bob", "Lewis", "333-33-3333", 5000, .04, 300 ); // derived class

    // aim base-class pointer at derived-class object
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
    return 0;
} // end main
```

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_577_1.png)

### Borland C++ 命令行编译器的错误消息：

```
Error E2316 Fig13_07\fig13_07.cpp 26: 'getBaseSalary' is not a member of 'CommissionEmployee' in function main()
Error E2316 Fig13_07\fig13_07.cpp 27: 'setBaseSalary' is not a member of 'CommissionEmployee' in function main()
```

### Microsoft Visual C++ 2005 编译器的错误消息：

```
C:\cppfp_examples\ch13\Fig13_07\fig13_07.cpp(26) : error C2039:
'getBaseSalary' : is not a member of 'CommissionEmployee'
    C:\cppfp_examples\ch13\Fig13_07\CommissionEmployee.h(10) :
    see declaration of 'CommissionEmployee'
C:\cppfp_examples\ch13\Fig13_07\fig13_07.cpp(27) : error C2039:
'setBaseSalary' : is not a member of 'CommissionEmployee'
    C:\cppfp_examples\ch13\Fig13_07\CommissionEmployee.h(10) :
    see declaration of 'CommissionEmployee'
```

### GNU C++ 编译器的错误消息：

```
fig13_07.cpp:26: error: 'getBaseSalary' undeclared (first use this function)
fig13_07.cpp:26: error: (Each undeclared identifier is reported only once for each function it appears in.)
fig13_07.cpp:27: error: 'setBaseSalary' undeclared (first use this function)
```

图13.7 | 试图通过基类指针调用仅存在于派生类的函数。（第2部分，共2部分。）

因为 BasePlusCommissionEmployee 是一种 CommissionEmployee（即 BasePlusCommissionEmployee 对象包含 CommissionEmployee 对象的全部功能）。第18-22行通过基类指针调用了基类成员函数 getFirstName、getLastName、getSocialSecurityNumber、getGrossSales 和 getCommissionRate。所有这些调用都是合法的，因为 BasePlusCommissionEmployee 从 CommissionEmployee 继承了这些成员函数。我们知道 commissionEmployeePtr 指向的是一个 BasePlusCommissionEmployee 对象，所以在第26-27行，我们试图调用 BasePlusCommissionEmployee 的成员函数 getBaseSalary 和 setBaseSalary。编译器对这两个调用都产生了错误，因为它们不是对基类 CommissionEmployee 的成员函数进行的。句柄只能用于调用与该句柄关联的类类型的成员函数。（在本例中，通过 CommissionEmployee *，我们只能调用 CommissionEmployee 的成员函数 setFirstName、getFirstName、setLastName、getLastName、setSocialSecurityNumber、getSocialSecurityNumber、setGrossSales、getGrossSales、setCommissionRate、getCommissionRate、earnings 和 print。）

如果我们将基类指针显式强制转换为派生类指针，编译器确实允许通过指向派生类对象的基类指针访问仅存在于派生类的成员——这种技术称为向下转型。正如你在13.3.1节所学，可以让基类指针指向派生类对象。然而，正如我们在图13.7中所演示的，基类指针只能用于调用在基类中声明的函数。向下转型允许对基类指针所指向的派生类对象执行派生类特有的操作。向下转型后，程序可以调用基类中没有的派生类函数。我们将在13.8节中展示向下转型的具体示例。

### 软件工程观察 13.3

> 如果派生类对象的地址已经赋值给其某个直接或间接基类的指针，则可以将该基类指针强制转换回派生类类型的指针。实际上，要向该派生类对象发送基类中不存在的消息，就必须这样做。

## 13.3.4 虚函数

在13.3.1节中，我们将基类 CommissionEmployee 指针指向派生类 BasePlusCommissionEmployee 对象，然后通过该指针调用了成员函数 print。回想一下，句柄类型决定了调用哪个类的功能。在那个例子中，即使指针指向的是拥有自己定制 print 函数的 BasePlusCommissionEmployee 对象，CommissionEmployee 指针仍然在 BasePlusCommissionEmployee 对象上调用了 CommissionEmployee 的成员函数 print。使用虚函数时，被指向对象的类型（而非句柄类型）决定了要调用哪个版本的虚函数。

首先，我们考虑为什么虚函数是有用的。假设有一组形状类，如 Circle、Triangle、Rectangle 和 Square，都派生自基类 Shape。这些类中的每一个都可能被赋予通过成员函数 draw 绘制自身的能力。虽然每个类都有自己的 draw 函数，但每种形状的绘制函数差别很大。在一个绘制一组形状的程序中，能够将所有形状泛化地视为基类 Shape 的对象将会很有用。然后，要绘制任何形状，我们只需使用基类 Shape 指针调用函数 draw，并让程序基于基类 Shape 指针在任何给定时刻所指向对象的类型，动态地（即在运行时）决定使用哪个派生类的 draw 函数。

为了实现这种行为，我们在基类中将 draw 声明为虚函数，并在每个派生类中覆盖 draw，以绘制相应的形状。从实现的角度来看，覆盖函数与重定义函数并无不同（后者是我们迄今为止一直使用的方式）。派生类中被覆盖的函数与基类中被覆盖的函数具有相同的签名和返回类型（即原型）。如果我们没有将基类函数声明为 virtual，我们便可以重定义该函数。相比之下，如果我们将基类函数声明为 virtual，我们就可以覆盖该函数，以实现多态行为。我们通过在基类中函数原型前加上关键字 virtual 来声明虚函数。例如，

```
virtual void draw() const;
```

该声明将出现在基类 Shape 中。上述原型声明函数 draw 是一个虚函数，它不接受任何参数，也不返回任何内容。该函数被声明为 const，因为 draw 函数通常不会修改调用它的 Shape 对象——虚函数并不一定是 const 函数。

### 软件工程观察 13.4

> 一旦一个函数被声明为 virtual，从那时起，它在整个继承层次结构中始终保持为 virtual，即使当派生类覆盖它时并未显式地声明为 virtual。
