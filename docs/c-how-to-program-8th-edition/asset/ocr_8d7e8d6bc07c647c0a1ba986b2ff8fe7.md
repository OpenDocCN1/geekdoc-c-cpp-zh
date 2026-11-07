```
```cpp
10    // instantiate BasePlusCommissionEmployee object
11    BasePlusCommissionEmployee
12      employee( "Bob", "Lewis", "333-33-3333", 5000, .04, 300 );
13
14    // set floating-point output formatting
15    cout << fixed << setprecision( 2 );
16
17    // get commission employee data
18    cout << "\nEmployee information obtained by get functions: \n"
19      << "\nFirst name is " << employee.getFirstName()
20      << "\nLast name is " << employee.getLastName()
21      << "\nSocial security number is "
22      << employee.getSocialSecurityNumber()
23      << "\nGross sales is " << employee.getGrossSales()
24      << "\nCommission rate is " << employee.getCommissionRate()
25      << "\nBase salary is " << employee.getBaseSalary() << endl;
26
27    employee.setBaseSalary( 1000 ); // set base salary
28
29    cout << "\nUpdated employee information output by print function: \n"
30      << endl;
31    employee.print(); // display the new employee information
32
33    // display the employee's earnings
34    cout << "\nEmployee's earnings: $" << employee.earnings() << endl;
35 } // end main
```
```

```
```text
Employee information obtained by get functions:

First name is Bob
Last name is Lewis
Social security number is 333-33-3333
Gross sales is 5000.00
Commission rate is 0.04
Base salary is 300.00

Updated employee information output by print function:

base-salaried commission employee: Bob Lewis
social security number: 333-33-3333
gross sales: 5000.00
commission rate: 0.04
base salary: 1000.00

Employee's earnings: $1200.00
```
```

**Fig. 12.9** | *BasePlusCommissionEmployee class test program. (Part 2 of 2.)*

# *Exploring the Similarities Between Class BasePlusCommissionEmployee and Class CommissionEmployee*

Most of the code for class BasePlusCommissionEmployee (Figs. 12.7–12.8) is similar, if not identical, to the code for class CommissionEmployee (Figs. 12.4–12.5). For example, in class BasePlusCommissionEmployee, private data members firstName and lastName