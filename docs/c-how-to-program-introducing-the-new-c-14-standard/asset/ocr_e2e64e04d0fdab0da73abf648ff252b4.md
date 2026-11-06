```
```cpp
// Fig. 12.19: fig12_19.cpp
// Demonstrating downcasting and runtime type information.
// NOTE: You may need to enable RTTI on your compiler
// before you can compile this application.
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
   cout << fixed << setprecision(2);

   // create and initialize vector of three base-class pointers
   vector<Employee*> employees{
      new SalariedEmployee("John", "Smith", "111-11-1111", 800),
      new CommissionEmployee("Sue", "Jones", "333-33-3333", 10000, .06),
      new BasePlusCommissionEmployee(
         "Bob", "Lewis", "444-44-4444", 5000, .04, 300)};

   // polymorphically process each element in vector employees
   for (Employee* employeePtr : employees) {
      cout << employeePtr->toString() << endl; // output employee
   }

   // attempt to downcast pointer
   BasePlusCommissionEmployee* derivedPtr =
      dynamic_cast<BasePlusCommissionEmployee*>(employeePtr);
```
```