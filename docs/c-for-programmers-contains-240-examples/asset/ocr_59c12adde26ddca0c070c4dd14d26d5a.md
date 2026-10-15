the object with "Sue" as the first name, "Jones" as the last name, "222-22-2222" as the social security number, 10000 as the gross sales amount and .06 as the commission rate. Lines 23–29 use employee’s get functions to display the values of its data members. Lines 31–32 invoke the object’s member functions setGrossSales and setCommissionRate to change the values of data members grossSales and commissionRate, respectively. Line 36 then calls employee’s print member function to output the updated CommissionEmployee information. Finally, line 39 displays the CommissionEmployee’s earnings, calculated by the object’s earnings member function using the updated values of data members grossSales and commissionRate.

```
1  // Fig. 12.6: fig12_06.cpp
2  // Testing class CommissionEmployee.
3  #include <iostream>
4  using std::cout;
5  using std::endl;
6  using std::fixed;
7
8  #include <iomanip>
9  using std::setprecision;
10
11 #include "CommissionEmployee.h" // CommissionEmployee class definition
12
13 int main()
14 {
15     // instantiate a CommissionEmployee object
16     CommissionEmployee employee(
17         "Sue", "Jones", "222-22-2222", 10000, .06 );
18
19     // set floating-point output formatting
20     cout << fixed << setprecision( 2 );
21
22     // get commission employee data
23     cout << "Employee information obtained by get functions: \n"
24         << "\nFirst name is " << employee.getFirstName()
25         << "\nLast name is " << employee.getLastName()
26         << "\nSocial security number is "
27         << employee.getSocialSecurityNumber()
28         << "\nGross sales is " << employee.getGrossSales()
29         << "\nCommission rate is " << employee.getCommissionRate() << endl;
30
31     employee.setGrossSales( 8000 ); // set gross sales
32     employee.setCommissionRate(.1); // set commission rate
33
34     cout << "\nUpdated employee information output by print function: \n"
35         << endl;
36     employee.print(); // display the new employee information
37
38     // display the employee's earnings
39     cout << "\n\nEmployee's earnings: $" << employee.earnings() << endl;
40
41     return 0;
42 } // end main
```

Fig. 12.6 | CommissionEmployee class test program. (Part I of 2.)