
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

Fig. 19.6 | CommissionEmployee class test program. (Part 2 of 2.)

## 19.3.2 Creating a BasePlusCommissionEmployee Class Without Using Inheritance

We now discuss the second part of our introduction to inheritance by creating and testing (a completely new and independent) class BasePlusCommissionEmployee (Figs. 19.7–19.8), which contains a first name, last name, social security number, gross sales amount, commission rate and base salary.

```
1 // Fig. 19.7: BasePlusCommissionEmployee.h
2 // BasePlusCommissionEmployee class definition represents an employee
3 // that receives a base salary in addition to commission.
4 #ifndef BASEPLUS_H
5 #define BASEPLUS_H
6 
7 #include <string> // C++ standard string class
8 
9 class BasePlusCommissionEmployee
10 {
11 public:
12 BasePlusCommissionEmployee( const std::string &, const std::string &,
13     const std::string &, double = 0.0, double = 0.0, double = 0.0 );
14 
15 void setFirstName( const std::string & ); // set first name
16 std::string getFirstName() const; // return first name
17 
18 void setLastName( const std::string & ); // set last name
19 std::string getLastName() const; // return last name
20 
21 void setSocialSecurityNumber( const std::string & ); // set SSN
22 std::string getSocialSecurityNumber() const; // return SSN
23 
24 void setGrossSales( double ); // set gross sales amount
25 double getGrossSales() const; // return gross sales amount
```

Fig. 19.7 | BasePlusCommissionEmployee class header. (Part 1 of 2.)

```
26 void setCommissionRate( double ); // set commission rate
27 double getCommissionRate() const; // return commission rate
28
29 void setBaseSalary( double ); // set base salary
30 double getBaseSalary() const; // return base salary
31
32 double earnings() const; // calculate earnings
33 void print() const; // print BasePlusCommissionEmployee object
34 private:
35 std::string firstName;
36 std::string lastName;
37 std::string socialSecurityNumber;
38 double grossSales; // gross weekly sales
39 double commissionRate; // commission percentage
40 double baseSalary; // base salary
41 }; // end class BasePlusCommissionEmployee
42
43 #endif
```

Fig. 19.7 | BasePlusCommissionEmployee class header. (Part 2 of 2.)

```
1 // Fig. 19.8: BasePlusCommissionEmployee.cpp
2 // Class BasePlusCommissionEmployee member-function definitions.
3 #include <iostream>
4 #include <stdexcept>
5 #include "BasePlusCommissionEmployee.h"
6
7 using namespace std;
8
9 // constructor
10 BasePlusCommissionEmployee::BasePlusCommissionEmployee(
11 const string &first, const string &last, const string &ssn,
12 double sales, double rate, double salary )
13 {
14 firstName = first; // should validate
15 lastName = last; // should validate
16 socialSecurityNumber = ssn; // should validate
17 setGrossSales( sales ); // validate and store gross sales
18 setCommissionRate( rate ); // validate and store commission rate
19 setBaseSalary( salary ); // validate and store base salary
20 } // end BasePlusCommissionEmployee constructor
21
22 // set first name
23 void BasePlusCommissionEmployee::setFirstName( const string &first )
24 {
25 firstName = first; // should validate
26 } // end function setFirstName
27
28 // return first name
29 string BasePlusCommissionEmployee::getFirstName() const
30 {
```

Fig. 19.8 | BasePlusCommissionEmployee class represents an employee who receives a base salary in addition to a commission. (Part 1 of 3.)

```
```cpp
82  // return commission rate
83  double BasePlusCommissionEmployee::getCommissionRate() const
84  {
85      return commissionRate;
86  } // end function getCommissionRate
87
88  // set base salary
89  void BasePlusCommissionEmployee::setBaseSalary( double salary )
90  {
91      if ( salary >= 0.0 )
92          baseSalary = salary;
93      else
94          throw invalid_argument( "Salary must be >= 0.0" );
95  } // end function setBaseSalary
96
97  // return base salary
98  double BasePlusCommissionEmployee::getBaseSalary() const
99  {
100     return baseSalary;
101 } // end function getBaseSalary
102
103 // calculate earnings
104 double BasePlusCommissionEmployee::earnings() const
105 {
106     return baseSalary + ( commissionRate * grossSales );
107 } // end function earnings
108
109 // print BasePlusCommissionEmployee object
110 void BasePlusCommissionEmployee::print() const
111 {
112     cout << "base-salaried commission employee: " << firstName << ' '
113          << lastName << "\nsocial security number: " << socialSecurityNumber
114          << "\ngross sales: " << grossSales
115          << "\ncommission rate: " << commissionRate
116          << "\nbase salary: " << baseSalary;
117 } // end function print
```
```

Fig. 19.8 | BasePlusCommissionEmployee class represents an employee who receives a base salary in addition to a commission. (Part 3 of 3.)

## Defining Class BasePlusCommissionEmployee

The BasePlusCommissionEmployee header (Fig. 19.7) specifies class BasePlusCommissionEmployee's public services, which include the BasePlusCommissionEmployee constructor (lines 12–13) and member functions earnings (line 33) and print (line 34). Lines 15–31 declare public get and set functions for the class's private data members (declared in lines 36–41) firstName, lastName, socialSecurityNumber, grossSales, commissionRate and baseSalary. These variables and member functions encapsulate all the necessary features of a base-salaried commission employee. Note the similarity between this class and class CommissionEmployee (Figs. 19.4–19.5)—in this example, we do not yet exploit that similarity.

Class BasePlusCommissionEmployee's earnings member function (defined in lines 104–107 of Fig. 19.8) computes the earnings of a base-salaried commission employee.

Line 106 returns the result of adding the employee’s base salary to the product of the commission rate and the employee’s gross sales.

### Testing Class BasePlusCommissionEmployee

Figure 19.9 tests class BasePlusCommissionEmployee. Lines 11–12 instantiate object employee of class BasePlusCommissionEmployee, passing "Bob", "Lewis", "333-33-3333", 5000, .04 and 300 to the constructor as the first name, last name, social security number, gross sales, commission rate and base salary, respectively. Lines 19–25 use BasePlusCommissionEmployee's get functions to retrieve the values of the object's data members for output. Line 27 invokes the object's setBaseSalary member function to change the base salary. Member function setBaseSalary (Fig. 19.8, lines 89–95) ensures that data member baseSalary is not assigned a negative value, because an employee's base salary cannot be negative. Line 31 of Fig. 19.9 invokes the object's print member function to output the updated BasePlusCommissionEmployee's information, and line 34 calls member function earnings to display the BasePlusCommissionEmployee's earnings.

```
```cpp
1  // Fig. 19.9: fig19_09.cpp
2  // BasePlusCommissionEmployee class test program.
3  #include <iostream>
4  #include <iomanip>
5  #include "BasePlusCommissionEmployee.h"
6  using namespace std;
7
8  int main()
9  {
10     // instantiate BasePlusCommissionEmployee object
11     BasePlusCommissionEmployee
12        employee( "Bob", "Lewis", "333-33-3333", 5000, .04, 300 );
13
14     // set floating-point output formatting
15     cout << fixed << setprecision( 2 );
16
17     // get commission employee data
18     cout << "Employee information obtained by get functions: \n"
19        << "\nFirst name is " << employee.getFirstName()
20        << "\nLast name is " << employee.getLastName()
21        << "\nSocial security number is "
22        << employee.getSocialSecurityNumber()
23        << "\nGross sales is " << employee.getGrossSales()
24        << "\nCommission rate is " << employee.getCommissionRate()
25        << "\nBase salary is " << employee.getBaseSalary() << endl;
26
27     employee.setBaseSalary( 1000 ); // set base salary
28
29     cout << "\nUpdated employee information output by print function: \n"
30        << endl;
31     employee.print(); // display the new employee information
32
33     // display the employee's earnings
34     cout << "\n\nEmployee's earnings: $" << employee.earnings() << endl;
35  } // end main
```
```

Fig. 19.9 | BasePlusCommissionEmployee class test program. (Part 1 of 2.)
