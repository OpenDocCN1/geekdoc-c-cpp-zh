
# 第 12 章 面对象编程：多态

## 12.9 强制类型转换、`dynamic_cast`、`typeid` 和 `type_info`

图 12.19 | 展示强制类型转换和运行时类型信息。（3 部分中的第 1 部分）

- 某些编译器要求在程序中使用之前必须先启用 RTTI。用于测试本书示例的编译器——GNU C++ 5.2.1、Visual C++ 2015 和 Xcode 7.2 Clang/LLVM——默认都启用了 RTTI。

```cpp
#include <iostream>
#include <iomanip>
#include <vector>
#include <typeinfo>
#include "Employee.h"
#include "SalariedEmployee.h"
#include "CommissionEmployee.h"
#include "BasePlusCommissionEmployee.h"
using namespace std;
int main() {
    // 设置浮点数格式
    cout << fixed << precision(2);
    // 创建并初始化三个基类指针的向量
    vector<Employee*> employees = {
        new SalariedEmployee("John", "Smith", "111-11-1111", 800),
        new CommissionEmployee("Sue", "Jones", "333-33-3333", 10000, .06),
        new BasePlusCommissionEmployee("Bob", "Lewis", "444-44-4444", 5000, .04, 300)
    };
    // 多态地处理 employees 向量中的每个元素
    for (Employee* employeePtr : employees) {
        cout << employeePtr->toString() << endl; // 输出员工
        // 尝试对指针进行向下类型转换
        BasePlusCommissionEmployee* derivedPtr =
            dynamic_cast<BasePlusCommissionEmployee*>(employeePtr);
        // 判断元素是否属于 BasePlusCommissionEmployee
        if (derivedPtr != nullptr) { // 对于“is a”关系为真
            double oldBaseSalary = derivedPtr->getBaseSalary();
            cout << "old salary: " << oldBaseSalary << endl;
            derivedPtr->setBaseSalary(1.10 * oldBaseSalary);
            cout << "new salary with 10% increase: " << derivedPtr->getBaseSalary() << endl;
        }
        cout << "earned " << employeePtr->earnings() << "\n\n";
    }
    // 释放向量元素指向的对象
    for (const Employee* employeePtr : employees) {
        cout << "deleting object of "
            << typeid(*employeePtr).name() << endl;
    }
}
```

图 12.19 | 展示强制类型转换和运行时类型信息。（3 部分中的第 2 部分）

`salaried employee: John Smith`
`social security number: 111-11-1111`
`weekly salary: 800.00`
`earned $800.00`

`commission employee: Sue Jones`
`social security number: 333-33-3333`
`gross sales: 10000.00; commission rate: 0.06`
`earned $600.00`

`base-salaried commission employee: Bob Lewis`
`social security number: 444-44-4444`
`gross sales: 5000.00; commission rate: 0.04; base salary: 300.00`
`old salary: 300.00`
`new salary with 10% increase is: $330.00`
`earned $330.00`

`deleting object of class SalariedEmployee`
`deleting object of class BasePlusEmployee`
`deleting object of class BasePlusCommissionEmployee`

图 12.19 | 展示强制类型转换和运行时类型信息。（3 部分中的第 3 部分）

### 使用 `dynamic_cast` 确定对象的类型

在这个示例中，我们遇到了一个 `BasePlusCommissionEmployee`，我们希望将其底薪增加 10%。为了处理 `BasePlusCommissionEmployee`，我们需要在执行时确定每个员工对象的特定类型，然后采取相应操作。这展示了程序在执行时确定对象类型（RTTI）以及能够正确作用于对象的动态转换的强大能力。

图 19 使用了 12.7 节中的员工层次结构，并将每个 `BasePlusCommissionEmployee` 员工的底薪增加了 10%。第 20–24 行创建并初始化了名为 `employees` 的三元素向量，它存储了指向 `Employee` 对象的指针。元素使用动态分配的 `SalaryEmployee`（图 12.11–12）、`CommissionEmployee`（图 12.13–14）和 `BasePlusCommissionEmployee`（图 12.15–16）对象初始化。图 19 的第 27–44 行遍历 `employees` 向量，通过调用成员函数 `toString`（第 28 行）显示每个 `Employee` 的信息。记住 `toString` 在基类中是虚函数，系统会调用相应的派生类对象的 `toString` 函数。

```cpp
// Fig. 19: fig12_19.cpp
// 展示强制类型转换和运行时类型信息。
// 注意：在编译此应用程序之前，你可能需要在编译器上启用 RTTI。
```
