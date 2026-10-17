
**Fig. 12.19** | Demonstrating downcasting and runtime type information. (Part I of 3)

1. 一些编译器需要在程序中使用 RTTI 之前启用 RTTI。用于测试本书示例的编译器——GNU C++ 5.2.1、Visual C++ 2015 和 Xcode 7 Clang/LLVM——默认情况下均启用了 RTTI。

# 608 第12章 面向对象编程：多态

```
// Fig. 12.19: fig12_19
// Demonstrating downcasting and runtime type information.
// NOTE: You may need to enable RTTI on your compiler
// before you can compile this application.
```

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
    // set floating-point output formatting
    cout << setprecision(2);

    // create and initialize vector of three base-class pointers
    vector<Employee*> employees = {
        new SalariedEmployee("John", "Smith", "111-11-1111", 800),
        new CommissionEmployee("Sue", "Jones", "333-33-3333", 10000, 0.06),
        new BasePlusCommissionEmployee("Bob", "Lewis", "444-44-4444", 5000, .04, 300)
    };

    // will process each element in vector employees
    for (Employee* employeePtr : employees) {
        cout << employeePtr->toString() << endl; // output employee

        // attempt to downcast pointer
        BasePlusCommissionEmployee* derivedPtr =
            dynamic_cast<BasePlusCommissionEmployee*>(employeePtr);

        if (derivedPtr != nullptr) { // true for "is a" relationship
            double oldBaseSalary = derivedPtr->getBaseSalary();
            cout << "old base salary: " << oldBaseSalary << endl;
            derivedPtr->setBaseSalary(1.10 * oldBaseSalary);
            cout << "new base salary with 10% increase: " << derivedPtr->getBaseSalary() << endl;
        }

        cout << "earned " << employeePtr->earnings() << "\n\n";
    }

    // release objects pointed to vector's elements
    for (const Employee* employeePtr : employees) {
        // output class name
        cout << typeid(*employeePtr).name() << endl;
        delete employeePtr;
    }
}
```
