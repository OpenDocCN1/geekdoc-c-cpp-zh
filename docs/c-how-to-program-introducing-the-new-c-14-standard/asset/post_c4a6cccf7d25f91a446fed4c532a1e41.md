
## 11.3.2 Creating a `BasePlusCommissionEmployee` Class Without Using Inheritance

We now discuss the second part of our introduction to inheritance by creating and testing *a completely new and independent class* `BasePlusCommissionEmployee` (**Figs. 11.7–11.8**), which contains a first name, last name, social security number, gross sales amount, commission rate *and* base salary.

```cpp
// Fig. 11.7: BasePlusCommissionEmployee.h
// BasePlusCommissionEmployee class definition represents an employee
// that receives a base salary in addition to commission.
#ifndef BASEPLUS_H
#define BASEPLUS_H

#include <string> // C++ standard string class

class BasePlusCommissionEmployee {
public:
    BasePlusCommissionEmployee(const std::string&, const std::string&,
        const std::string&, double = 0.0, double = 0.0, double = 0.0);

    void setFirstName(const std::string&); // set first name
    std::string getFirstName() const; // return first name

    void setLastName(const std::string&); // set last name
    std::string getLastName() const; // return last name

    void setSocialSecurityNumber(const std::string&); // set SSN
    std::string getSocialSecurityNumber() const; // return SSN

    void setGrossSales(double); // set gross sales amount
    double getGrossSales() const; // return gross sales amount

    void setCommissionRate(double); // set commission rate
    double getCommissionRate() const; // return commission rate

    void setBaseSalary(double); // set base salary
    double getBaseSalary() const; // return base salary

    double earnings() const; // calculate earnings
    std::string toString() const; // create string representation
private:
    std::string firstName;
    std::string lastName;
    std::string socialSecurityNumber;
    double grossSales; // gross weekly sales
    double commissionRate; // commission percentage
    double baseSalary; // base salary
};

#endif
```

**Fig. 11.7** `BasePlusCommissionEmployee` class header.

```cpp
// Fig. 11.8: BasePlusCommissionEmployee.cpp
// Class BasePlusCommissionEmployee member-function definitions.
#include <iomanip>
#include <stdexcept>
#include <sstream>
#include "BasePlusCommissionEmployee.h"
using namespace std;

// constructor
BasePlusCommissionEmployee::BasePlusCommissionEmployee(
   const string& first, const string& last, const string& ssn,
   double sales, double rate, double salary) {
   firstName = first; // should validate
   lastName = last; // should validate
   socialSecurityNumber = ssn; // should validate
   setGrossSales(sales); // validate and store gross sales
   setCommissionRate(rate); // validate and store commission rate
   setBaseSalary(salary); // validate and store base salary
}

// set first name
void BasePlusCommissionEmployee::setFirstName(const string& first) {
   firstName = first; // should validate
}

// return first name
string BasePlusCommissionEmployee::getFirstName() const {
   return firstName;
}

// set last name
void BasePlusCommissionEmployee::setLastName(const string& last) {
   lastName = last; // should validate
}

// return last name
string BasePlusCommissionEmployee::getLastName() const {
   return lastName;
}

// set social security number
void BasePlusCommissionEmployee::setSocialSecurityNumber(
   const string& ssn) {
   socialSecurityNumber = ssn; // should validate
}

// return social security number
string BasePlusCommissionEmployee::getSocialSecurityNumber() const {
    return socialSecurityNumber;
}

// set gross sales amount
void BasePlusCommissionEmployee::setGrossSales(double sales) {
    if (sales < 0.0) {
        throw invalid_argument("Gross sales must be >= 0.0");
    }

    grossSales = sales;
}

// return gross sales amount
double BasePlusCommissionEmployee::getGrossSales() const {
    return grossSales;
}

// set commission rate
void BasePlusCommissionEmployee::setCommissionRate(double rate) {
    if (rate <= 0.0 || rate >= 1.0) {
        throw invalid_argument("Commission rate must be > 0.0 and < 1.0");
    }

    commissionRate = rate;
}

// return commission rate
double BasePlusCommissionEmployee::getCommissionRate() const {
    return commissionRate;
}

// set base salary
void BasePlusCommissionEmployee::setBaseSalary(double salary) {
   if (salary < 0.0) {
      throw invalid_argument("Salary must be >= 0.0");
   }

   baseSalary = salary;
}

// return base salary
double BasePlusCommissionEmployee::getBaseSalary() const {
   return baseSalary;
}

// calculate earnings
double BasePlusCommissionEmployee::earnings() const {
   return baseSalary + (commissionRate * grossSales);
}

// return string representation of BasePlusCommissionEmployee object
string BasePlusCommissionEmployee::toString() const {
   ostringstream output;
   output << fixed << setprecision(2); // two digits of precision
   output << "base-salaried commission employee: " << firstName << ' '
      << lastName << "\nsocial security number: " << socialSecurityNumber
      << "\ngross sales: " << grossSales
      << "\ncommission rate: " << commissionRate
      << "\nbase salary: " << baseSalary;
   return output.str();
}
```

Fig. 11.8 **BasePlusCommissionEmployee** class represents an employee who receives a base salary in addition to a commission.

### Defining Class `BasePlusCommissionEmployee`

The `BasePlusCommissionEmployee` header (**Fig. 11.7**) specifies class `BasePlusCommissionEmployee`'s **public** services, which include the `BasePlusCommissionEmployee` constructor (lines 11–12) and member functions `earnings` (line 32) and `toString` (line 33). Lines 14–30 declare `public` **get** and **set** functions for the class's `private` data members (declared in lines 35–40) `firstName`, `lastName`, `socialSecurityNumber`, `grossSales`, `commissionRate` and `baseSalary`. These variables and member functions encapsulate all the necessary features of a base-salaried commission employee. Note the similarity between this class and class `CommissionEmployee` (**Figs. 11.4–11.5**)—in this example, we do *not* yet exploit that similarity.

Class `BasePlusCommissionEmployee`'s `earnings` member function (defined in lines 93–95 of **Fig. 11.8**) computes the earnings of a base-salaried commission employee. Line 94 returns the result of adding the employee's base salary to the product of the commission rate and the employee's gross sales.

### Testing Class `BasePlusCommissionEmployee`

**Figure 11.9** tests class `BasePlusCommissionEmployee`. Lines 10–11 instantiate object `employee` of class `BasePlusCommissionEmployee`, passing `"Bob"`, `"Lewis"`, `"333-33-3333"`, `5000`, `.04` and `300` to the constructor as the first name, last name, social security number, gross sales, commission rate and base salary, respectively. Lines 15–22 use `BasePlusCommissionEmployee`'s **get** functions to retrieve the values of the object's data members for output. Line 23 invokes the object's `setBaseSalary` member function to change the base salary. Member function `setBaseSalary` (**Fig. 11.8**, lines 79–85) ensures that data member `baseSalary` is not assigned a negative value, because an employee's base salary cannot be negative. Lines 24–25 of **Fig. 11.9** invoke the object's `toString` member function to get the updated `BasePlusCommissionEmployee`'s information, and line 28 calls member function `earnings` to display the `BasePlusCommissionEmployee`'s earnings.

```cpp
// Fig. 11.9: fig11_09.cpp
// BasePlusCommissionEmployee class test program.
#include <iostream>
#include <iomanip>
#include "BasePlusCommissionEmployee.h"
using namespace std;

int main() {
   // instantiate BasePlusCommissionEmployee object
   BasePlusCommissionEmployee employee{ "Bob", "Lewis", "333-33-3333",
      5000, .04, 300};

   // get commission employee data
   cout << fixed << setprecision(2); // set floating-point formatting
   cout << "Employee information obtained by get functions: \n"
      << "\nFirst name is " << employee.getFirstName()
      << "\nLast name is " << employee.getLastName()
      << "\nSocial security number is "
      << employee.getSocialSecurityNumber()
      << "\nGross sales is " << employee.getGrossSales()
      << "\nCommission rate is " << employee.getCommissionRate()
      << "\nBase salary is " << employee.getBaseSalary() << endl;
   employee.setBaseSalary(1000); // set base salary
   cout << "\nUpdated employee information from function toString: \n\n"
      << employee.toString();

   // display the employee's earnings
   cout << "\n\nEmployee's earnings: $" << employee.earnings() << endl;
}
```

```text
Employee information obtained by get functions:

First name is Bob
Last name is Lewis
Social security number is 333-33-3333
Gross sales is 5000.00
Commission rate is 0.04
Base salary is 300.00

Updated employee information from function toString:

base-salaried commission employee: Bob Lewis
social security number: 333-33-3333
gross sales: 5000.00
commission rate: 0.04
base salary: 1000.00

Employee's earnings: $1200.00
```

Fig. 11.9 *BasePlusCommissionEmployee* class test program.
