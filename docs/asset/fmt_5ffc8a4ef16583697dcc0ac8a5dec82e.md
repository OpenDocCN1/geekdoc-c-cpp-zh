
```cpp
13     double sales, double rate, double salary )
14     // explicitly call base-class constructor
15     : CommissionEmployee( first, last, ssn, sales, rate )
16 {
17     setBaseSalary( salary ); // validate and store base salary
18
19     cout << "BasePlusCommissionEmployee constructor: " << endl;
20     print();
21     cout << "\n\n";
22 } // end BasePlusCommissionEmployee constructor
23
24 // destructor
25 BasePlusCommissionEmployee::~BasePlusCommissionEmployee()
26 {
27     cout << "BasePlusCommissionEmployee destructor: " << endl;
28     print();
29     cout << "\n\n";
30 } // end BasePlusCommissionEmployee destructor
31
32 // set base salary
33 void BasePlusCommissionEmployee::setBaseSalary( double salary )
34 {
35     baseSalary = ( salary < 0.0 ) ? 0.0 : salary;
36 } // end function setBaseSalary
37
38 // return base salary
39 double BasePlusCommissionEmployee::getBaseSalary() const
40 {
41     return baseSalary;
42 } // end function getBaseSalary
43
44 // calculate earnings
45 double BasePlusCommissionEmployee::earnings() const
46 {
47     return getBaseSalary() + CommissionEmployee::earnings();
48 } // end function earnings
49
50 // print BasePlusCommissionEmployee object
51 void BasePlusCommissionEmployee::print() const
52 {
53     cout << "base-salaried ";
54
55     // invoke CommissionEmployee's print function
56     CommissionEmployee::print();
57
58     cout << "\nbase salary: " << getBaseSalary();
} // end function print
```

图 12.26 演示了在继承层次结构中类的对象构造和析构函数的调用顺序。函数 `main`（第 15–34 行）首先在 `main` 内部的一个独立块中实例化 `CommissionEmployee` 对象 `employee1`（第 21–22 行，块范围为第 20–23 行）。该对象立即进出作用域（在对象创建后立即到达块末尾），因此 `CommissionEmployee` 构造函数和析构函数都被调用。接下来，第 26–27 行实例化 `BasePlusCommissionEmployee` 对象 `employee2`。这会调用 `CommissionEmployee` 构造函数以显示从 `BasePlusCommissionEmployee` 构造函数传递的值，然后执行 `BasePlusCommissionEmployee` 构造函数中指定的输出。第 30–31 行随后实例化 `BasePlusCommissionEmployee` 对象 `employee3`。同样，`CommissionEmployee` 和 `BasePlusCommissionEmployee` 构造函数都被调用。请注意，在每种情况下，`CommissionEmployee` 构造函数的函数体在 `BasePlusCommissionEmployee` 构造函数的函数体执行之前执行。当到达 `main` 的末尾时，对象 `employee2` 和 `employee3` 的析构函数被调用。也就是说，由于析构函数按其对应构造函数的相反顺序调用，因此对象 `employee3` 的 `BasePlusCommissionEmployee` 析构函数和 `CommissionEmployee` 析构函数按此顺序被调用，然后对象 `employee2` 的 `BasePlusCommissionEmployee` 和 `CommissionEmployee` 析构函数按此顺序被调用。

**图 12.26** | 构造函数和析构函数调用顺序。（第 1 部分，共 3 部分。）

```cpp
// Fig. 12.26: fig12_26.cpp
// Display order in which base-class and derived-class constructors
// and destructors are called.

#include <iostream>
using std::cout;
using std::endl;
using std::fixed;
#include <iomanip>
using std::setprecision;

// BasePlusCommissionEmployee class definition
#include "BasePlusCommissionEmployee.h"

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

   return 0;
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
gross sales: 2000.00
commission rate: 0.06
base salary: 800.00

CommissionEmployee constructor:
commission employee: Mark Sands
social security number: 888-88-8888
gross sales: 8000.00
commission rate: 0.15

BasePlusCommissionEmployee constructor:
base-salaried commission employee: Mark Sands
social security number: 888-88-8888
gross sales: 8000.00
commission rate: 0.15
base salary: 2000.00

BasePlusCommissionEmployee destructor:
base-salaried commission employee: Mark Sands
social security number: 888-88-8888
gross sales: 8000.00
commission rate: 0.15
base salary: 2000.00

CommissionEmployee destructor:
commission employee: Mark Sands
social security number: 888-88-8888
gross sales: 8000.00
commission rate: 0.15

BasePlusCommissionEmployee destructor:
base-salaried commission employee: Lisa Jones
social security number: 555-55-5555
gross sales: 2000.00
commission rate: 0.06
base salary: 800.00

CommissionEmployee destructor:
commission employee: Lisa Jones
social security number: 555-55-5555
gross sales: 2000.00
commission rate: 0.06
```
