
```
Virtual function calls made off base-class references:

salaried employee: John Smith
social security number: 111-11-1111
weekly salary: 800.00
earned $800.00

commission employee: Sue Jones
social security number: 333-33-3333
gross sales: 10000.00; commission rate: 0.06
earned $600.00

base-salaried commission employee: Bob Lewis
social security number: 444-44-4444
gross sales: 5000.00; commission rate: 0.04; base salary: 300.00
earned $500.00
```

图 13.17 | Employee 类层次结构驱动程序。（第 4 部分，共 4 部分。）

第 41 行分配了 vector employees，它包含三个 Employee 指针。第 44 行让 employees[0] 指向对象 salariedEmployee。第 45 行让 employees[1] 指向对象 commissionEmployee。第 46 行让 employees[2] 指向对象 basePlusCommissionEmployee。编译器允许这些赋值，因为 SalariedEmployee 是一种 Employee，CommissionEmployee 是一种 Employee，BasePlusCommissionEmployee 也是一种 Employee。因此，即使 Employee 是抽象类，我们也可以将 SalariedEmployee、CommissionEmployee 和 BasePlusCommissionEmployee 对象的地址赋给基类 Employee 指针。

第 54–55 行的循环遍历 vector employees，并对 employees 中的每个元素调用函数 virtualViaPointer（第 67–71 行）。函数 virtualViaPointer 在参数 baseClassPtr 中接收存储在某个 employees 元素中的地址。每次调用 virtualViaPointer 都使用 baseClassPtr 调用虚函数 print（第 69 行）和 earnings（第 70 行）。函数 virtualViaPointer 不包含任何 SalariedEmployee、CommissionEmployee 或 BasePlusCommissionEmployee 类型信息。该函数只知道基类类型 Employee。因此，编译器无法知道要通过 baseClassPtr 调用哪个具体类的函数。然而在执行时，每次虚函数调用都会调用 baseClassPtr 当时所指向对象上的函数。输出表明，确实调用了每个类相应的函数，并且显示了每个对象的正确信息。例如，SalariedEmployee 显示周薪，CommissionEmployee 和 BasePlusCommissionEmployee 显示总销售额。此外，在第 70 行以多态方式获取每个 Employee 的 earnings，与在第 33、35 和 37 行通过静态绑定获取这些员工的 earnings 产生相同的结果。所有对 print 和 earnings 的虚函数调用都在运行时通过动态绑定解析。

最后，另一个 for 语句（第 61–62 行）遍历 employees，并对 vector 中的每个元素调用函数 virtualViaReference（第 75–79 行）。函数 virtualViaReference 在其参数 baseClassRef（类型为 const Employee &）中接收一个引用，该引用指向通过解引用每个 employees 元素中存储的指针而获得的对象（第 62 行）。每次调用 virtualViaReference 都通过引用 baseClassRef 调用虚函数 print（第 77 行）和 earnings（第 78 行），以证明多态*处理也会通过基类引用发生。* 每次虚函数调用都会在运行时调用 `baseClassRef` 所引用的对象上的函数。这是*动态绑定*的另一个例子。使用基类引用产生的输出与使用基类指针产生的输出完全相同。

## 13.7（可选）多态、虚函数与动态绑定（“底层揭秘”）

C++ 使多态易于编程。当然，在 C 等非面向对象语言中也可以为多态编程，但这样做需要复杂且可能危险的指针操作。本节讨论 C++ 如何在内部实现多态、虚函数和动态绑定。这将使你扎实地理解这些能力实际上如何工作。更重要的是，它将帮助你认识多态的开销——就额外的内存消耗和处理器时间而言。这将帮助你确定何时使用多态、何时避免使用它。正如你将在第 22 章看到的，STL 组件是在*没有*多态和虚函数的情况下实现的——这样做是为了避免相关的执行时开销，并达到最佳性能，以满足 STL 的独特需求。

首先，我们将解释编译器在*编译时*构建的数据结构，以在执行时支持多态。你将看到，多态是通过三级指针实现的，即*三重间接寻址*。然后，我们将展示正在执行的程序如何使用这些数据结构来执行虚函数，并实现与多态相关的动态绑定。我们的讨论解释了一种可能的实现；这并不是语言要求。

当 C++ 编译一个具有一个或多个虚函数的类时，它会为该类构建一个[虚函数表 (vtable)](#)。正在执行的程序使用 `vtable` 在该类的某个虚函数每次被调用时选择正确的函数实现。图 13.18 最左列展示了类 Employee、SalariedEmployee、CommissionEmployee 和 BasePlusCommissionEmployee 的 `vtables`。

### Employee 类 vtable

在类 Employee 的 `vtable` 中，第一个函数指针被设为 0（即空指针）。这样做是因为函数 earnings 是纯虚函数，因此*缺少实现*。第二个函数指针指向函数 print，它显示员工的全名和社会安全号码。[*注意：* 为节省篇幅，我们缩写了本图中每个 print 函数的输出。] 任何在其 `vtable` 中有一个或多个空指针的类都是*抽象*类。没有任何空 `vtable` 指针的类（如 SalariedEmployee、CommissionEmployee 和 BasePlusCommissionEmployee）是*具体*类。

### SalariedEmployee 类 vtable

类 SalariedEmployee 重写函数 earnings，以返回员工的周薪，因此该函数指针指向类 SalariedEmployee 的 earnings 函数。SalariedEmployee 还重写 print，因此相应的函数指针指向 SalariedEmployee 成员函数，该函数打印 "salaried employee: "，后跟员工姓名、社会安全号码和周薪。

为了调整 BasePlusCommissionEmployee 的基本工资，我们必须在执行时确定每个 Employee 对象的具体类型，然后采取适当的操作。本节演示 **运行时类型信息 (RTTI)** 和 **动态转换** 的强大能力，它们使程序能够在执行时确定对象的类型，并据此对该对象进行操作。

> 注意：某些编译器要求先启用 RTTI，然后才能在程序中使用它。在 Visual C++ 2010 中，此选项默认启用。

图 13.19 使用第 13.6 节开发的 Employee 层次结构，并将每个 BasePlusCommissionEmployee 的基本工资增加 10%。第 21 行声明了包含三个元素的 vector employees，它存储指向 Employee 对象的指针。第 24–29 行用类 SalariedEmployee（图 13.13–13.14）、CommissionEmployee（图 13.13–13.14）和 BasePlusCommissionEmployee（图 13.15–13.16）的动态分配对象的地址填充该 vector。

```cpp
// Fig. 13.19: fig13_19.cpp
// Demonstrating downcasting and runtime type information.
// NOTE: You may need to enable RTTI on your compiler
// before you can execute this application.
#include <iostream>
#include <iomanip>
#include <vector>
#include <typeinfo>
#include "Employee.h"
#include "SalariedEmployee.h"
#include "CommissionEmployee.h"
#include "BasePlusCommissionEmployee.h"
using namespace std;

int main()
{
   // set floating-point output formatting
   cout << fixed << setprecision( 2 );

   // create vector of three base-class pointers
   vector < Employee * > employees( 3 );

   // initialize vector with various kinds of Employees
   employees[ 0 ] = new SalariedEmployee(
      "John", "Smith", "111-11-1111", 800 );
   employees[ 1 ] = new CommissionEmployee(
      "Sue", "Jones", "333-33-3333", 1000, .06 );
   employees[ 2 ] = new BasePlusCommissionEmployee(
      "Bob", "Lewis", "444-44-4444", 5000, .04, 300 );

   // polymorphically process each element in vector employees
   for ( size_t i = 0; i < employees.size(); ++i )
   {
      employees[ i ]->print(); // output employee information
      cout << endl;
   }
}
```

**图 13.19** | 演示向下转型和运行时类型信息。（第 1 部分，共 2 部分。）
