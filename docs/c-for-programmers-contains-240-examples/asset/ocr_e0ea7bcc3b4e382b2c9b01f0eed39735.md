Class `BasePlusCommissionEmployee` does not inherit class `CommissionEmployee`’s constructor. However, class `BasePlusCommissionEmployee`’s constructor (Fig. 12.15, lines 10–17) calls class `CommissionEmployee`’s constructor explicitly with member initializer syntax (line 14). Recall that `BasePlusCommissionEmployee`’s constructor must explicitly call the constructor of class `CommissionEmployee`, because `CommissionEmployee` does not contain a default constructor that could be invoked implicitly.

# Testing the Modified BasePlusCommissionEmployee Class

Figure 12.16 uses a `BasePlusCommissionEmployee` object to perform the same tasks that Fig. 12.2 performed on an object of the first version of class `BasePlusCommissionEmployee` (Figs. 12.7–12.8). Note that the outputs of the two programs are identical. We created the first class `BasePlusCommissionEmployee` without using inheritance and created this version of `BasePlusCommissionEmployee` using inheritance; however, both classes provide the same functionality. Note that the code for class `BasePlusCommissionEmployee` (i.e., the header and implementation files), which is 74 lines, is considerably shorter than the

```
```cpp
// Fig. 12.16: fig12_16.cpp
// Testing class BasePlusCommissionEmployee.
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
   // instantiate BasePlusCommissionEmployee object
   BasePlusCommissionEmployee
      employee( "Bob", "Lewis", "333-33-3333", 5000, .04, 300 );

   // set floating-point output formatting
   cout << fixed << setprecision( 2 );

   // get commission employee data
   cout << "Employee information obtained by get functions: \n"
      << "\nFirst name is " << employee.getFirstName()
      << "\nLast name is " << employee.getLastName()
      << "\nSocial security number is "
      << employee.getSocialSecurityNumber()
      << "\nGross sales is " << employee.getGrossSales()
      << "\nCommission rate is " << employee.getCommissionRate()
      << "\nBase salary is " << employee.getBaseSalary() << endl;

   employee.setBaseSalary( 1000 ); // set base salary
}
```
```

**Fig. 12.16** | protected base-class data can be accessed from derived class. (Part 1 of 2.)