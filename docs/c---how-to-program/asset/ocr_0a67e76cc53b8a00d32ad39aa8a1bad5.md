function print (lines 93–99) displays the values of a CommissionEmployee object’s data members.

# Testing Class CommissionEmployee

Figure 19.6 test class CommissionEmployee. Lines 11–12 instantiate CommissionEmployee object employee and invoke the constructor to initialize the object with "Sue" as the first name, "Jones" as the last name, "222–22–2222" as the social security number, 10000 as the gross sales amount and .06 as the commission rate. Lines 19–24 use employee’s get functions to display the values of its data members. Lines 26–27 invoke the object’s member functions setGrossSales and setCommissionRate to change the values of data members grossSales and commissionRate, respectively. Line 31 then calls employee’s print member function to output the updated CommissionEmployee information. Finally, line 34 displays the CommissionEmployee’s earnings, calculated by the object’s earnings member function using the updated values of data members grossSales and commissionRate.

```
```cpp
// Fig. 19.6: fig19_06.cpp
// CommissionEmployee class test program.
#include <iostream>
#include <iomanip>
#include "CommissionEmployee.h" // CommissionEmployee class definition
using namespace std;

int main()
{
   // instantiate a CommissionEmployee object
   CommissionEmployee employee{
      "Sue", "Jones", "222-22-2222", 10000, .06 };

   // set floating-point output formatting
   cout << fixed << setprecision( 2 );

   // get commission employee data
   cout << "Employee information obtained by get functions:\n"
      << "\nFirst name is " << employee.getFirstName()
      << "\nLast name is " << employee.getLastName()
      << "\nSocial Security number is "
      << employee.getSocialSecurityNumber()
      << "\nGross sales is " << employee.getGrossSales()
      << "\nCommission rate is " << employee.getCommissionRate() << endl;

   employee.setGrossSales( 8000 ); // set gross sales
   employee.setCommissionRate( .1 ); // set commission rate

   cout << "\nUpdated employee information output by print function:\n"
      << endl;
   employee.print(); // display the new employee information

   // display the employee's earnings
   cout << "\n\nEmployee's earnings: $" << employee.earnings() << endl;
} // end main
```
```

**Fig. 19.6** | CommissionEmployee class test program. (Part 1 of 2.)