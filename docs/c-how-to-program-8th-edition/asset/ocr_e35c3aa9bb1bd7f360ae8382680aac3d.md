private and protected specifiers affect member access in derived classes. As shown in Fig. 12.5, lines 12–14, we assign values to data members `firstName`, `lastName` and `socialSecurityNumber` in the constructor body. Later in this section, we’ll return to using member-initializer lists in the constructor.

We do not validate the values of the constructor’s arguments first, last and ssn before assigning them to the corresponding data members. We certainly could validate the first and last names—perhaps by ensuring that they’re of a reasonable length. Similarly, a social security number could be validated to ensure that it contains nine digits, with or without dashes (e.g., 123–45–6789 or 123456789).

# CommissionEmployee Member Functions earnings and print

Member function earnings (lines 86–89) calculates a CommissionEmployee’s earnings. Line 88 multiplies the commissionRate by the grossSales and returns the result. Member function print (lines 92–98) displays the values of a CommissionEmployee object’s data members.

# Testing Class CommissionEmployee

Figure 12.6 tests class CommissionEmployee. Lines 11–12 instantiate object employee of class CommissionEmployee and invoke CommissionEmployee’s constructor to initialize the object with "Sue" as the first name, "Jones" as the last name, "222–22–2222" as the social security number, 10000 as the gross sales amount and .06 as the commission rate. Lines 19–24 use employee’s get functions to display the values of its data members. Lines 26–27 invoke the object’s member functions setGrossSales and setCommissionRate to change the values of data members grossSales and commissionRate, respectively. Line 31 then calls employee’s print member function to output the updated CommissionEmployee information. Finally, line 34 displays the CommissionEmployee’s earnings, calculated by the object’s earnings member function using the updated values of data members grossSales and commissionRate.

```
```cpp
// Fig. 12.6: fig12_06.cpp
// Testing class CommissionEmployee.
#include <iostream>
#include <iomanip>
#include "CommissionEmployee.h" // CommissionEmployee class definition
using namespace std;

int main()
{
   // instantiate a CommissionEmployee object
   CommissionEmployee employee(
      "Sue", "Jones", "222-22-2222", 10000, .06 );

   // set floating-point output format
   cout << fixed << setprecision( 2 );

   // get commission employee data
   cout << "Employee information obtained by get functions: \n"
        << "\nFirst name is " << employee.getFirstName()
```
```

**Fig. 12.6** | CommissionEmployee class test program. (Part 1 of 2.)