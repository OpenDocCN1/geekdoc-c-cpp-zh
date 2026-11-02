```
```cpp
void setCommissionRate( double ); // set commission rate
double getCommissionRate() const; // return commission rate
void setBaseSalary( double ); // set base salary
double getBaseSalary() const; // return base salary
double earnings() const; // calculate earnings
void print() const; // print BasePlusCommissionEmployee object
private:
std::string firstName;
std::string lastName;
std::string socialSecurityNumber;
double grossSales; // gross weekly sales
double commissionRate; // commission percentage
double baseSalary; // base salary
}; // end class BasePlusCommissionEmployee
#endif
```
```

Fig. 19.7 | BasePlusCommissionEmployee class header. (Part 2 of 2.)

```
```cpp
// Fig. 19.8: BasePlusCommissionEmployee.cpp
// Class BasePlusCommissionEmployee member-function definitions.
#include <iostream>
#include <stdexcept>
#include "BasePlusCommissionEmployee.h"
using namespace std;

// constructor
BasePlusCommissionEmployee::BasePlusCommissionEmployee(
const string &first, const string &last, const string &ssn,
double sales, double rate, double salary )
{
firstName = first; // should validate
lastName = last; // should validate
socialSecurityNumber = ssn; // should validate
setGrossSales( sales ); // validate and store gross sales
setCommissionRate( rate ); // validate and store commission rate
setBaseSalary( salary ); // validate and store base salary
} // end BasePlusCommissionEmployee constructor

// set first name
void BasePlusCommissionEmployee::setFirstName( const string &first )
{
firstName = first; // should validate
} // end function setFirstName

// return first name
string BasePlusCommissionEmployee::getFirstName() const
{
```
```

Fig. 19.8 | BasePlusCommissionEmployee class represents an employee who receives a base salary in addition to a commission. (Part 1 of 3.)