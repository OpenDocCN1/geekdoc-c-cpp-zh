
将成员函数 print 声明为虚函数（图 13.8 第 30–31 行和图 13.9 第 20–21 行）。因为函数 earnings 和 print 在类 CommissionEmployee 中是虚函数，所以类 BasePlusCommissionEmployee 的 earnings 和 print 函数会覆盖类 CommissionEmployee 的对应函数。现在，如果我们让一个基类 CommissionEmployee 指针指向派生类 BasePlusCommissionEmployee 对象，并且程序使用该指针调用函数 earnings 或 print，那么就会调用 BasePlusCommissionEmployee 对象的对应函数。类 CommissionEmployee 和 BasePlusCommissionEmployee 的成员函数实现没有更改，因此我们复用图 13.2 和图 13.4 的版本。

```cpp
// Fig. 13.8: CommissionEmployee.h
// CommissionEmployee class definition represents a commission employee.
#ifndef COMMISSION_H_
#define COMMISSION_H_

#include <string> // C++ standard string class
using namespace std;

class CommissionEmployee
{
public:
   CommissionEmployee( const string &, const string &, const string &,
      double = 0.0, double = 0.0 );

   void setFirstName( const string & ); // set first name
   string getFirstName() const; // return first name

   void setLastName( const string & ); // set last name
   string getLastName() const; // return last name

   void setSocialSecurityNumber( const string & ); // set SSN
   string getSocialSecurityNumber() const; // return SSN

   void setGrossSales( double ); // set gross sales amount
   double getGrossSales() const; // return gross sales amount

   void setCommissionRate( double ); // set commission rate
   double getCommissionRate() const; // return commission rate

   virtual double earnings() const; // calculate earnings
   virtual void print() const; // print CommissionEmployee object
private:
   string firstName;
   string lastName;
   string socialSecurityNumber;
   double grossSales; // gross weekly sales
   double commissionRate; // commission percentage
}; // end class CommissionEmployee

#endif
```

图 13.8 | CommissionEmployee 类头文件将 earnings 和 print 函数声明为虚函数。

```cpp
52  // aim base-class pointer at derived-class object and print
53  commissionEmployeePtr = &basePlusCommissionEmployee;
54  cout << "\n\nCalling virtual function print with base-class pointer"
55       << "\nto derived-class object invokes derived-class "
56       << "print function:\n\n";
57
58  // polymorphism; invokes BasePlusCommissionEmployee's print;
59  // base-class pointer to derived-class object
60  commissionEmployeePtr->print();
61  cout << endl;
62
63 } // end main
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
```

图 13.10 | 通过基类指针指向派生类对象来调用派生类虚函数，演示多态。（第 2 部分，共 2 部分。）

### 13.3.5 基类与派生类对象和指针之间允许的赋值总结

既然你已经看到一个完整应用程序以多态方式处理各种对象，我们总结一下用基类和派生类对象及指针能做什么、不能做什么。虽然派生类对象也是基类对象，但这两个对象仍然不同。如前所述，派生类对象可以被当作基类对象处理。这是一种逻辑关系，因为派生类包含基类的所有成员。然而，基类对象不能被视为派生类对象——派生类可以拥有额外的仅属于派生类的成员。因此，未经显式强制转换，不允许让派生类指针指向基类对象——这样的赋值会使基类对象上的仅属于派生类的成员未定义。强制转换使编译器免于发出错误消息的责任。从某种意义上说，通过使用强制转换，你是在说：“我知道我正在做的事情很危险，我对自己的行为负全责。”

我们已经讨论了将基类指针和派生类指针指向基类对象和派生类对象的四种方式：

- 1. 让基类指针指向基类对象很直接——通过基类指针进行的调用只会调用基类功能。
- 2. 让派生类指针指向派生类对象很直接——通过派生类指针进行的调用只会调用派生类功能。
- 3. 让基类指针指向派生类对象是安全的，因为派生类对象是其基类的对象。但是，该指针只能用于调用基类成员函数。如果你试图通过基类指针引用仅属于派生类的成员，编译器会报告错误。为避免此错误，必须将基类指针强制转换为派生类指针。然后可以使用派生类指针调用派生类对象的完整功能。这种技术称为向下转型，是一种潜在危险的操作——13.8 节演示如何安全地使用向下转型。如果虚函数在基类和派生类中定义（无论是通过继承还是重写），并且如果通过基类指针在派生类对象上调用该函数，那么会调用该函数的派生类版本。这是仅虚函数才会发生的多态行为的一个例子。
- 4. 让派生类指针指向基类对象会产生编译错误。is-a 关系仅适用于从派生类到其直接和间接基类，反之则不适用。基类对象不包含可以通过派生类指针调用的仅属于派生类的成员。

### 常见编程错误 13.1

在让基类指针指向派生类对象之后，试图用基类指针引用仅属于派生类的成员是编译错误。

### 常见编程错误 13.2

将基类对象当作派生类对象处理可能导致错误。

## 13.4 类型字段与 switch 语句

确定对象类型的一种方式是使用 switch 语句检查对象中某个字段的值。这使我们能够区分对象类型，然后为特定对象调用合适的操作。例如，在一个形状层次结构中，每个形状对象都有一个 shapeType 属性，switch 语句可以检查对象的 shapeType 以确定调用哪个 print 函数。

使用 switch 逻辑会使程序面临各种潜在问题。例如，你可能在需要时忘记包含类型测试，或者可能忘记测试 switch 语句中所有可能的情况。通过添加新类型来修改基于 switch 的系统时，你可能忘记在所有相关 switch 语句中插入新情况。每次添加或删除类都需要修改系统中的每个 switch 语句；追踪这些语句可能耗时且容易出错。

![](img/023f159fdd47d944d48e08843cea732d_629_0.png)

### 软件工程观察 13.6

*多态编程可以消除对 switch 逻辑的需求。通过使用多态机制执行等效逻辑，你可以避免通常与 switch 逻辑相关的各种错误。*

![](img/023f159fdd47d944d48e08843cea732d_629_1.png)

### 软件工程观察 13.7

*使用多态的一个有趣结果是程序呈现出更简单的外观。它们包含更少的分支逻辑和更简单的顺序代码。这种简化有助于测试、调试和程序维护。*

## 13.5 抽象类与纯虚函数

当我们把类视为一种类型时，我们假设程序会创建该类型的对象。然而，有些情况下，定义从不打算从中实例化任何对象的类是有用的。这样的类称为抽象类。因为这些类通常用作继承层次结构中的基类，所以我们称它们为抽象基类。这些类不能用于实例化对象，因为正如我们很快会看到的，抽象类是不完整的——派生类必须定义“缺失的部分”。我们将在 13.6 节构建使用抽象类的程序。

抽象类提供一个基类，其他类可以从它继承。可用于实例化对象的类称为具体类。这样的类定义它们声明的每个成员函数。我们可以有一个抽象基类 TwoDimensionalShape，并派生 Square、Circle 和 Triangle 等具体类。我们也可以有一个抽象基类 ThreeDimensionalShape，并派生 Cube、Sphere 和 Cylinder 等具体类。抽象基类过于通用，无法定义真实对象；在考虑实例化对象之前，我们需要更具体。例如，如果有人让你“画这个二维形状”，你会画什么形状？具体类提供使实例化对象合理所需的细节。

继承层次结构不需要包含任何抽象类，但许多面向对象系统的类层次结构以抽象基类为首。在某些情况下，抽象类构成层次结构的顶部几层。一个很好的例子是图 12.3 中的形状层次结构，它以抽象基类 Shape 开始。在该层次结构的下一层，我们还有两个抽象基类，即 TwoDimensional-
