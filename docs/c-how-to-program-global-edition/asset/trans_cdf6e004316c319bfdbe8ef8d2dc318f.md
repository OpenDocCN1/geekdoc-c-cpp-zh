
```cpp
#include "Employee.h"
#include "SalariedEmployee.h"
#include "CommissionEmployee.h"
#include "BasePlusCommissionEmployee.h"
using namespace std;

void virtualViaPointer( const Employee * const ); // prototype
void virtualViaReference( const Employee & ); // prototype

int main()
{
    // set floating-point output formatting
    cout << fixed << setprecision( 2 );

    // create derived-class objects
    SalariedEmployee salariedEmployee(
        "John", "Smith", "111-11-1111", 800 );
    CommissionEmployee commissionEmployee(
        "Sue", "Jones", "333-33-3333", 10000, .06 );
    BasePlusCommissionEmployee basePlusCommissionEmployee(
        "Bob", "Lewis", "444-44-4444", 5000, .04, 300 );

    cout << "Employees processed individually using static binding:\n\n";

    // output each Employee's information and earnings using static binding
    salariedEmployee.print();
    cout << "earned $" << salariedEmployee.earnings() << "\n\n";
    commissionEmployee.print();
    cout << "earned $" << commissionEmployee.earnings() << "\n\n";
    basePlusCommissionEmployee.print();
    cout << "earned $" << basePlusCommissionEmployee.earnings()
        << "\n\n";

    // create vector of three base-class pointers
    vector< Employee * > employees( 3 );

    // initialize vector with pointers to Employees
    employees[ 0 ] = &salariedEmployee;
    employees[ 1 ] = &commissionEmployee;
    employees[ 2 ] = &basePlusCommissionEmployee;

    cout << "Employees processed polymorphically via dynamic binding:\n\n";

    // call virtualViaPointer to print each Employee's information
    // and earnings using dynamic binding
    cout << "Virtual function calls made off base-class pointers:\n\n";

    for ( const Employee *employeePtr : employees )
        virtualViaPointer( employeePtr );

    // call virtualViaReference to print each Employee's information
    // and earnings using dynamic binding
    cout << "Virtual function calls made off base-class references:\n\n";
```
```cpp
    for ( const Employee *employeePtr : employees )
        virtualViaReference( *employeePtr ); // note dereferencing
} // end main

// call Employee virtual functions print and earnings off a
// base-class pointer using dynamic binding
void virtualViaPointer( const Employee * const baseClassPtr )
{
    baseClassPtr->print();
    cout << "\nearned $" << baseClassPtr->earnings() << "\n\n";
} // end function virtualViaPointer

// call Employee virtual functions print and earnings off a
// base-class reference using dynamic binding
void virtualViaReference( const Employee &baseClassRef )
{
    baseClassRef.print();
    cout << "\nearned $" << baseClassRef.earnings() << "\n\n";
} // end function virtualViaReference
```

员工使用静态绑定单独处理：

薪资员工：John Smith
社会安全号码：111-11-1111
周薪：800.00
赚取 $800.00

佣金员工：Sue Jones
社会安全号码：333-33-3333
毛销售额：10000.00；佣金率：0.06
赚取 $600.00

底薪加佣金员工：Bob Lewis
社会安全号码：444-44-4444
毛销售额：5000.00；佣金率：0.04；基本工资：300.00
赚取 $500.00

员工通过动态绑定进行多态处理：

通过基类指针进行的虚函数调用：

薪资员工：John Smith
社会安全号码：111-11-1111
周薪：800.00
赚取 $800.00

佣金员工：Sue Jones
社会安全号码：333-33-3333
毛销售额：10000.00；佣金率：0.06
赚取 $600.00

底薪加佣金员工：Bob Lewis
社会安全号码：444-44-4444
毛销售额：5000.00；佣金率：0.04；基本工资：300.00
赚取 $500.00

**图 20.17** | 员工类层次结构驱动程序。（第 3 部分，共 4 部分。）

通过基类引用进行的虚函数调用：
薪资员工：John Smith
社会安全号码：111-11-1111
周薪：800.00
赚取 $800.00

佣金员工：Sue Jones
社会安全号码：333-33-3333
毛销售额：10000.00；佣金率：0.06
赚取 $600.00

底薪加佣金员工：Bob Lewis
社会安全号码：444-44-4444
毛销售额：5000.00；佣金率：0.04；基本工资：300.00
赚取 $500.00

## 图 20.17 | 员工类层次结构驱动程序。（第 4 部分，共 4 部分。）

第 41 行创建了 vector employees，其中包含三个 Employee 指针。第 44 行将 employees[0] 指向对象 salariedEmployee。第 45 行将 employees[1] 指向对象 commissionEmployee。第 46 行将 employee[2] 指向对象 basePlusCommissionEmployee。编译器允许这些赋值，因为 SalariedEmployee 是 Employee，CommissionEmployee 是 Employee，而 BasePlusCommissionEmployee 也是 Employee。因此，即使 Employee 是抽象类，我们也可以将 SalariedEmployee、CommissionEmployee 和 BasePlusCommissionEmployee 对象的地址赋给基类 Employee 指针。

第 54-55 行遍历 vector employees 并为 employees 中的每个元素调用函数 virtualViaPointer（第 67-71 行）。函数 virtualViaPointer 在参数 baseClassPtr 中接收存储在 employees 元素中的地址。每次调用 virtualViaPointer 都使用 baseClassPtr 调用虚函数 print（第 69 行）和 earnings（第 70 行）。函数 virtualViaPointer 不包含任何 SalariedEmployee、CommissionEmployee 或 BasePlusCommissionEmployee 类型信息。该函数只知道基类类型 Employee。因此，编译器无法知道通过 baseClassPtr 调用哪个具体类的函数。然而在执行时，每个虚函数调用都正确地调用了 baseClassPtr 当前指向的对象的函数。输出说明每个类的适当函数确实被调用，并且每个对象的正确信息都被显示。例如，SalariedEmployee 显示周薪，而 CommissionEmployee 和 BasePlusCommissionEmployee 显示毛销售额。此外，在第 70 行多态地获取每个 Employee 的收入产生的结果与在第 33、35 和 37 行通过静态绑定获取这些员工收入的结果相同。所有对 print 和 earnings 的虚函数调用都在运行时通过动态绑定解析。

最后，第 61-62 行遍历 employees 并为每个 vector 元素调用函数 virtualViaReference（第 75-79 行）。函数 virtualViaReference 在其参数 baseClassRef（类型为 const Employee &）中接收对通过取消引用存储在每个 employees 元素中的指针（第 62 行）获得的对象的引用。每次调用 virtualViaReference 都通过 baseClassRef 调用虚函数 print（第 77 行）和 earnings（第 78 行），以证明使用基类引用也发生多态处理。

每次虚函数调用都在运行时调用 baseClassRef 所引用的对象的函数。这又是动态绑定的另一个例子。使用基类引用产生的输出与使用基类指针产生的输出相同。

## 20.7（可选）多态、虚函数和动态绑定“内部实现”

C++ 使多态编程变得容易。在 C 等非面向对象语言中当然也可以为多态编程，但这样做需要复杂且可能危险的指针操作。本节讨论 C++ 如何在内部实现多态、虚函数和动态绑定。这将使你对这些功能如何真正工作有坚实的理解。更重要的是，它将帮助你认识到多态的开销——以额外的内存消耗和处理器时间为代价。这可以帮助你确定何时使用多态以及何时避免它。C++ 标准库类如 array 和 vector 是在没有多态和虚函数的情况下实现的，以避免相关的执行时间开销并实现最佳性能。

首先，我们将解释编译器在编译时构建以支持执行时多态的数据结构。你会看到多态是通过三级指针，即三重间接来实现的。然后我们将展示执行中的程序如何使用这些数据结构来执行虚函数并实现与多态相关的动态绑定。我们的讨论解释了一种可能的实现；这不是语言要求。

当 C++ 编译具有一个或多个虚函数的类时，它会为该类构建一个虚函数表（vtable）。vtable 包含指向该类虚函数的指针。就像内置数组的名称包含数组第一个元素在内存中的地址一样，指向函数的指针包含执行函数任务的代码在内存中的起始地址。执行中的程序使用 vtable 在每次调用该类的虚函数时选择正确的函数实现。图 20.18 最左边的列说明了类 Employee、SalariedEmployee、CommissionEmployee 和 BasePlusCommissionEmployee 的 vtables。

### Employee 类虚函数表

在 Employee 类 vtable 中，第一个函数指针设置为 0（即 null ptr），因为函数 earnings 是纯虚函数，因此缺乏实现。第二个函数指针指向函数 print，该函数显示员工的姓名和社会安全号码。[注意：我们在此图中缩写了每个 print 函数的输出以节省空间。] 任何在其 vtable 中有一个或多个 null 指针的类都是抽象类。没有 null vtable 指针的类（如 SalariedEmployee、CommissionEmployee 和 BasePlusCommissionEmployee）是具体类。

### SalariedEmployee 类虚函数表

类 SalariedEmployee 重写函数 earnings 以返回员工的周薪，因此函数指针指向 SalariedEmployee 类的 earnings 函数。SalariedEmployee 也重写了 print，因此相应的函数指针指向 SalariedEmployee 成员函数，该函数打印“salaried employee: ”，后跟员工的姓名、社会安全号码和周薪。
