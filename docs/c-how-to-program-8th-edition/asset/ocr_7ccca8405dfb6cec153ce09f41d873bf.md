```
```cpp
20    << "\nLast name is " << employee.getLastName()
21    << "\nSocial security number is "
22    << employee.getSocialSecurityNumber()
23    << "\nGross sales is " << employee.getGrossSales()
24    << "\nCommission rate is " << employee.getCommissionRate() << endl;
25
26 employee.setGrossSales( 8000 ); // set gross sales
27 employee.setCommissionRate( .1 ); // set commission rate
28
29 cout << "\nUpdated employee information output by print function: \n"
30      << endl;
31 employee.print(); // display the new employee information
32
33 // display the employee's earnings
34 cout << "\nEmployee's earnings: $" << employee.earnings() << endl;
35 } // end main
```
```

```
```text
Employee information obtained by get functions:

First name is Sue
Last name is Jones
Social security number is 222-22-2222
Gross sales is 10000.00
Commission rate is 0.06

Updated employee information output by print function:

commission employee: Sue Jones
social security number: 222-22-2222
gross sales: 8000.00
commission rate: 0.10

Employee's earnings: $800.00
```
```

Fig. 12.6 | *CommissionEmployee class test program.* (Part 2 of 2.)

# 12.4.2 Creating a BasePlusCommissionEmployee Class Without Using Inheritance

We now discuss the second part of our introduction to inheritance by creating and testing (a completely new and independent) class BasePlusCommissionEmployee (Figs. 12.7–12.8), which contains a first name, last name, social security number, gross sales amount, commission rate and *base* salary.

```
```cpp
// Fig. 12.7: BasePlusCommissionEmployee.h
// BasePlusCommissionEmployee class definition represents an employee
// that receives a base salary in addition to commission.
#ifndef BASEPLUS_H
#define BASEPLUS_H

#include <string> // C++ standard string class
using namespace std;
```
```

Fig. 12.7 | *BasePlusCommissionEmployee class header.* (Part 1 of 2.)