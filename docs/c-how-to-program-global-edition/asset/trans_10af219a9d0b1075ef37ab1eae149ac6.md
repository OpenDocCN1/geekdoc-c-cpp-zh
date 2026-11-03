

```cpp
virtual void draw() const;
```

将出现在基类 Shape 中。 前面的原型声明函数 draw 是一个虚函数，它不接受参数也不返回任何内容。 该函数被声明为 const，因为 draw 函数通常不会对调用它的 Shape 对象进行更改——虚函数不必是 const 函数。

> > **软件工程观察 20.5**
> > *一旦函数被声明为虚函数，它就会一直保持为虚函数，直到继承层次结构中的该点之后，即使在派生类重写该函数时没有显式声明为虚函数。*

> > **良好的编程实践 20.1**
> > *即使某些函数由于在类层次结构更高处所做的声明而隐式为虚函数，也应在类层次结构的每一级显式声明这些函数为虚函数，以提高程序的清晰度。*

> > **软件工程观察 20.6**
> > *当派生类选择不重写其基类的虚函数时，派生类只是继承其基类的虚函数实现。*

## *通过基类指针或引用调用虚函数*

如果程序通过指向派生类对象的基类指针（例如，shapePtr->draw()）或指向派生类对象的基类引用（例如，shapeRef.draw()）调用虚函数，程序将根据对象类型——而不是指针或引用类型——在动态（即执行时）选择正确的派生类 draw 函数。 在执行时（而不是编译时）选择要调用的适当函数称为动态绑定或后期绑定。

## *通过对象名称调用虚函数*

当通过引用特定对象的名称并使用点成员选择运算符（例如，squareObject.draw()）调用虚函数时，函数调用在编译时解析（这称为静态绑定），并且被调用的虚函数是为该特定对象的类定义（或继承）的函数——这不是多态行为。 因此，虚函数的动态绑定仅发生在指针上（并且，正如我们很快将看到的，引用上）。

## *CommissionEmployee 层次结构中的虚函数*

现在让我们看看虚函数如何在我们的员工层次结构中实现多态行为。 图 20.4–20.5 分别是类 CommissionEmployee 和 BasePlusCommissionEmployee 的头文件。 我们修改了它们，将每个类的 earnings 和 print 成员函数声明为 virtual（图 20.4 的第 29–30 行和图 20.5 的第 19–20 行）。 因为函数 earnings 和 print 在类 CommissionEmployee 中是虚函数，所以类 BasePlusCommissionEmployee 的 earnings 和 print 函数重写了类 CommissionEmployee 的函数。 此外，类 BasePlusCommissionEmployee 的 earnings 和 print 函数被声明为 override。

![](img/bf54db922e6fa8319cba11069e785521_804_0.png)

## **错误预防提示 20.1**

将 C++11 的 override 关键字应用于派生类中的每个被重写函数。 这会强制编译器检查基类是否具有同名和参数列表（即相同签名）的成员函数。 如果没有，编译器会生成错误。

现在，如果我们将基类 CommissionEmployee 指针指向派生类 BasePlusCommissionEmployee 对象，并且程序使用该指针调用 earnings 或 print 中的任一函数，则 BasePlusCommissionEmployee 对象的相应函数将被调用。 类 CommissionEmployee 和 BasePlusCommissionEmployee 的成员函数实现没有更改，因此我们重用图 19.14 和 19.15 的版本。

```
~~~cpp
1  // Fig. 20.4: CommissionEmployee.h
2  // CommissionEmployee class header declares earnings and print as virtual.
3  #ifndef COMMISSION_H
4  #define COMMISSION_H
5  
6  #include <string> // C++ standard string class
7  
8  class CommissionEmployee
9  {
10 public:
11    CommissionEmployee( const std::string &, const std::string &,
12       const std::string &, double = 0.0, double = 0.0 );
13 
14    void setFirstName( const std::string & ); // set first name
15    std::string getFirstName() const; // return first name
16 
17    void setLastName( const std::string & ); // set last name
18    std::string getLastName() const; // return last name
19 
20    void setSocialSecurityNumber( const std::string & ); // set SSN
21    std::string getSocialSecurityNumber() const; // return SSN
22 
23    void setGrossSales( double ); // set gross sales amount
24    double getGrossSales() const; // return gross sales amount
25 
26    void setCommissionRate( double ); // set commission rate
27    double getCommissionRate() const; // return commission rate
28 
29    virtual double earnings() const; // calculate earnings
30    virtual void print() const; // print object
31 private:
32    std::string firstName;
33    std::string lastName;
34    std::string socialSecurityNumber;
35    double grossSales; // gross weekly sales
36    double commissionRate; // commission percentage
37 }; // end class CommissionEmployee
38 
39 #endif
~~~
```

图 20.4 | CommissionEmployee 类头文件将 earnings 和 print 声明为 virtual。

```
~~~cpp
// Fig. 20.6: fig20_06.cpp
// Introducing polymorphism, virtual functions and dynamic binding.
#include <iostream>
#include <iomanip>
#include "CommissionEmployee.h"
#include "BasePlusCommissionEmployee.h"
using namespace std;

int main()
{
   // create base-class object
   CommissionEmployee commissionEmployee(
      "Sue", "Jones", "222-22-2222", 10000, .06 );

   // create base-class pointer
   CommissionEmployee *commissionEmployeePtr = nullptr;

   // create derived-class object
   BasePlusCommissionEmployee basePlusCommissionEmployee(
      "Bob", "Lewis", "333-33-3333", 5000, .04, 300 );

   // create derived-class pointer
   BasePlusCommissionEmployee *basePlusCommissionEmployeePtr = nullptr;

   // set floating-point output formatting
   cout << fixed << setprecision( 2 );

   // output objects using static binding
   cout << "\n\nPrinting function on base-class and derived-class "
      << "\nobjects with static binding:\n\n";
   commissionEmployee.print(); // static binding
   cout << "\n\n";
   basePlusCommissionEmployee.print(); // static binding

   // output objects using dynamic binding
   cout << "\n\nPrinting function on base-class and "
      << "derived-class \nobjects with dynamic binding";

   // aim base-class pointer at base-class object and print
   commissionEmployeePtr = &commissionEmployee;
   cout << "\n\nCalling virtual function print with base-class pointer"
      << "\nto base-class object invokes base-class "
      << "print function:\n\n";
   commissionEmployeePtr->print(); // invokes base-class print

   // aim derived-class pointer at derived-class object and print
   basePlusCommissionEmployeePtr = &basePlusCommissionEmployee;
   cout << "\n\nCalling virtual function print with derived-class "
      << "\npointer\nto derived-class object invokes derived-class "
      << "print function:\n\n";
   basePlusCommissionEmployeePtr->print(); // invokes derived-class print
~~~
```

**图 20.6** | 通过基类指针指向派生类对象来调用派生类虚函数以演示多态。 （第 1 部分，共 2 部分。）

```
    52
    53      // aim base-class pointer at derived-class object and print
    54      commissionEmployeePtr = &basePlusCommissionEmployee;
    55      cout << "\n\nCalling virtual function print with base-class pointer"
    56           << "\nto derived-class object invokes derived-class "
    57           << "print function:\n\n";
    58
    59      // polymorphism; invokes BasePlusCommissionEmployee's print;
    60      // base-class pointer to derived-class object
    61      commissionEmployeePtr->print();
    62      cout << endl;
    63   } // end main
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
    base salary: 300.00         Notice that the base salary is now displayed
```

**图 20.6** | 通过基类指针指向派生类对象来调用派生类虚函数以演示多态。 （第 2 部分，共 2 部分。）

