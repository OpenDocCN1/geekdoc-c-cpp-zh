
// Fig. 13.22: BasePlusCommissionEmployee.cpp
// BasePlusCommissionEmployee 成员函数定义。
#include <iostream>
using std::cout;

// BasePlusCommissionEmployee 类定义
#include "BasePlusCommissionEmployee.h"

// 构造函数
BasePlusCommissionEmployee::BasePlusCommissionEmployee(
    const string &first, const string &last, const string &ssn,
    double sales, double rate, double salary )
    : CommissionEmployee( first, last, ssn, sales, rate )
{
    setBaseSalary( salary ); // 验证并存储基本工资
} // end BasePlusCommissionEmployee constructor

// 设置基本工资
void BasePlusCommissionEmployee::setBaseSalary( double salary )
{
    baseSalary = ( ( salary < 0.0 ) ? 0.0 : salary );
} // end function setBaseSalary

// 返回基本工资
double BasePlusCommissionEmployee::getBaseSalary() const
{
    return baseSalary;
} // end function getBaseSalary

// 计算收入；
// 重写 Employee 中的纯虚函数 earnings
double BasePlusCommissionEmployee::earnings() const
{
    return getBaseSalary() + CommissionEmployee::earnings();
} // end function earnings

// 打印 BasePlusCommissionEmployee 的信息
void BasePlusCommissionEmployee::print() const
{
    cout << "base-salaried ";
    CommissionEmployee::print(); // 代码复用
    cout << "; base salary: " << getBaseSalary();
} // end function print

Fig. 13.22 | BasePlusCommissionEmployee 类实现文件。

PlusCommissionEmployee 的信息。请回忆 CommissionEmployee 的 print 通过调用其基类（即 Employee）的 print 函数来显示员工的姓名和社保号码——这又是代码复用的一个例子。请注意 BasePlusCommissionEmployee 的 print 启动了一条跨越 Employee 层次结构全部三个层级的函数调用链。

### 13.6.6 演示多态处理

为了测试我们的 Employee 层次结构，图 13.23 中的程序创建了四个具体类 SalariedEmployee、HourlyEmployee、CommissionEmployee 和 BasePlusCommissionEmployee 的对象。程序操作这些对象，首先使用静态绑定，然后使用 Employee 指针的 vector 进行多态操作。行 31–38 创建了四个具体 Employee 派生类的对象。行 43–51 输出每个 Employee 的信息和收入。行 43–51 中的每个成员函数调用都是

```
// Fig. 13.23: fig13_23.cpp
// 单独处理 Employee 派生类对象
// 并使用动态绑定进行多态处理。
#include <iostream>
using std::cout;
using std::endl;
using std::fixed;

#include <iomanip>
using std::setprecision;

#include <vector>
using std::vector;

// 包含 Employee 层次结构中类的定义
#include "Employee.h"
#include "SalariedEmployee.h"
#include "HourlyEmployee.h"
#include "CommissionEmployee.h"
#include "BasePlusCommissionEmployee.h"

void virtualViaPointer( const Employee * const ); // 原型
void virtualViaReference( const Employee & ); // 原型

int main()
{
    // 设置浮点输出格式
    cout << fixed << setprecision( 2 );

    // 创建派生类对象
    SalariedEmployee salariedEmployee(
        "John", "Smith", "111-11-1111", 800 );
    HourlyEmployee hourlyEmployee(
        "Karen", "Price", "222-22-2222", 16.75, 40 );
    CommissionEmployee commissionEmployee(
        "Sue", "Jones", "333-33-3333", 10000, .06 );
    BasePlusCommissionEmployee basePlusCommissionEmployee(
        "Bob", "Lewis", "444-44-4444", 5000, .04, 300 );

    cout << "Employees processed individually using static binding:\n\n";

    // 使用静态绑定输出每个 Employee 的信息和收入
    salariedEmployee.print();
```

Fig. 13.23 | Employee 类层次结构驱动程序。 (第 1 部分，共 4 部分。)

```
44  cout << "\n earned $" << salariedEmployee.earnings() << "\n\n";
45  hourlyEmployee.print();
46  cout << "\n earned $" << hourlyEmployee.earnings() << "\n\n";
47  commissionEmployee.print();
48  cout << "\n earned $" << commissionEmployee.earnings() << "\n\n";
49  basePlusCommissionEmployee.print();
50  cout << "\n earned $" << basePlusCommissionEmployee.earnings()
51      << "\n\n";
52
53  // 创建四个基类指针的 vector
54  vector < Employee * > employees( 4 );
55
56  // 用 Employees 初始化 vector
57  employees[ 0 ] = &salariedEmployee;
58  employees[ 1 ] = &hourlyEmployee;
59  employees[ 2 ] = &commissionEmployee;
60  employees[ 3 ] = &basePlusCommissionEmployee;
61
62  cout << "Employees processed polymorphically using dynamic binding:\n\n";
63
64  // 调用 virtualViaPointer 打印每个 Employee 的信息
65  // 和收入，使用动态绑定
66  cout << "Virtual function calls made off base-class pointers:\n\n";
67
68  for ( size_t i = 0; i < employees.size(); i++ )
69      virtualViaPointer( employees[ i ] );
70
71  // 调用 virtualViaReference 打印每个 Employee 的信息
72  // 和收入，使用动态绑定
73  cout << "Virtual function calls made off base-class references:\n\n";
74
75  for ( size_t i = 0; i < employees.size(); i++ )
76      virtualViaReference( *employees[ i ] ); // 注意解引用
77
78  return 0;
79 } // end main
80
81  // 通过基类指针使用动态绑定调用 Employee 虚函数 print 和 earnings
82  void virtualViaPointer( const Employee * const baseClassPtr )
83  {
84      baseClassPtr->print();
85      cout << "\n earned $" << baseClassPtr->earnings() << "\n\n";
86  } // end function virtualViaPointer
87
88  // 通过基类引用使用动态绑定调用 Employee 虚函数 print 和 earnings
89  void virtualViaReference( const Employee &baseClassRef )
90  {
91      baseClassRef.print();
92      cout << "\n earned $" << baseClassRef.earnings() << "\n\n";
93  } // end function virtualViaReference
```

Employees processed individually using static binding:

salaried employee: John Smith
social security number: 111-11-1111
weekly salary: 800.00
earned $800.00

hourly employee: Karen Price
social security number: 222-22-2222
hourly wage: 16.75; hours worked: 40.00
earned $670.00

commission employee: Sue Jones
social security number: 333-33-3333
gross sales: 10000.00; commission rate: 0.06
earned $600.00

base-salaried commission employee: Bob Lewis
social security number: 444-44-4444
gross sales: 5000.00; commission rate: 0.04; base salary: 300.00
earned $500.00

Employees processed polymorphically using dynamic binding:

Virtual function calls made off base-class pointers:

salaried employee: John Smith
social security number: 111-11-1111
weekly salary: 800.00
earned $800.00

hourly employee: Karen Price
social security number: 222-22-2222
hourly wage: 16.75; hours worked: 40.00
earned $670.00

commission employee: Sue Jones
social security number: 333-33-3333
gross sales: 10000.00; commission rate: 0.06
earned $600.00

base-salaried commission employee: Bob Lewis
social security number: 444-44-4444
gross sales: 5000.00; commission rate: 0.04; base salary: 300.00
earned $500.00

Virtual function calls made off base-class references:

salaried employee: John Smith
social security number: 111-11-1111
weekly salary: 800.00
earned $800.00

hourly employee: Karen Price
social security number: 222-22-2222
hourly wage: 16.75; hours worked: 40.00
earned $670.00

(continued…)

**Fig. 13.23** | Employee 类层次结构驱动程序。 (第 3 部分，共 4 部分。)

```
commission employee: Sue Jones
social security number: 333-33-3333
gross sales: 10000.00; commission rate: 0.06
earned $600.00

base-salaried commission employee: Bob Lewis
social security number: 444-44-4444
gross sales: 500.00; commission rate: 0.04; base salary: 300.00
earned $500.00
```

Fig. 13.23 | Employee 类层次结构驱动程序。 (第 4 部分，共 4 部分。)

一个静态绑定的例子——在编译时，因为我们使用的是名称句柄（而不是在执行时可设定的指针或引用），编译器可以识别每个对象的类型以确定调用哪个 print 和 earnings 函数。

行 54 分配 vector employees，其中包含四个 Employee 指针。行 57 使 employees[0] 指向对象 SalariedEmployee。行 58 使 employees[1] 指向对象 HourlyEmployee。行 59 使 employees[2] 指向对象 CommissionEmployee。行 60 使 employees[3] 指向对象 BasePlusCommissionEmployee。编译器允许这些赋值，因为 SalariedEmployee 是一个 Employee，HourlyEmployee 是一个 Employee，CommissionEmployee 是一个 Employee，BasePlusCommissionEmployee 是一个 Employee。因此，我们可以将 SalariedEmployee、HourlyEmployee、CommissionEmployee 和 BasePlusCommissionEmployee 对象的地址赋给基类 Employee 指针（即使 Employee 是一个抽象类）。

行 68–69 中的循环遍历 vector employees 并为 employees 中的每个元素调用函数 virtualViaPointer（行 83–87）。函数 virtualViaPointer 在参数 baseClassPtr（类型为 const Employee * const）中接收 employees 元素中存储的地址。对 virtualViaPointer 的每次调用都使用 baseClassPtr 调用虚函数 print（行 85）和 earnings（行 86）。请注意，函数 virtualViaPointer 不包含任何 SalariedEmployee、HourlyEmployee、CommissionEmployee 或 BasePlusCommissionEmployee 类型信息。该函数只知道基类类型 Employee。因此，在编译时，编译器无法知道通过 baseClassPtr 调用哪个具体类的函数。然而，在执行时，每个虚函数调用都会在 baseClassPtr 当时指向的对象上调用该函数。输出说明确实调用了每个类的适当函数，并且每个对象的正确信息都被显示出来。例如，SalariedEmployee 显示了周薪，CommissionEmployee 和 BasePlusCommissionEmployee 显示了毛销售额。还请注意，在行 86 中多态地获取每个 Employee 的收入产生的结果与在行 44、46、48 和 50 中通过静态绑定获取这些员工收入的结果相同。所有对 print 和 earnings 的虚函数调用都在运行时使用动态绑定解析。

最后，另一个 for 语句（行 75–76）遍历 employees 并为 vector 中的每个元素调用函数 virtualViaReference（行 91–95）。函数 virtualViaReference 在其参数 baseClassRef（类型为 const Employee &）中接收通过解引用 employees 元素中存储的指针（行 76）形成的引用。对 virtualViaReference 的每次调用都通过引用 baseClassRef 调用虚函数 print（行 93）和 earnings（行 94）以演示多态 pro-

