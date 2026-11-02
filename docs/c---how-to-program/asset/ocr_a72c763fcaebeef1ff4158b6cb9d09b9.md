PlusCommissionEmployee’s information. Recall that CommissionEmployee’s print displays the employee’s first name, last name and social security number by invoking the print function of its base class (i.e., Employee)—yet another example of code reuse. Base-PlusCommissionEmployee’s print initiates a chain of functions calls that spans all three levels of the Employee hierarchy.

```
```cpp
// Fig. 20.15: BasePlusCommissionEmployee.h
// BasePlusCommissionEmployee class derived from CommissionEmployee.
#ifndef BASEPLUS_H
#define BASEPLUS_H

#include <string> // C++ standard string class
#include "CommissionEmployee.h" // CommissionEmployee class definition

class BasePlusCommissionEmployee : public CommissionEmployee
{
public:
    BasePlusCommissionEmployee( const std::string &, const std::string &,
        const std::string &, double = 0.0, double = 0.0, double = 0.0 );
    virtual ~CommissionEmployee() { } // virtual destructor

    void setBaseSalary( double ); // set base salary
    double getBaseSalary() const; // return base salary

    // keyword virtual signals intent to override
    virtual double earnings() const override; // calculate earnings
    virtual void print() const override; // print object
private:
    double baseSalary; // base salary per week
}; // end class BasePlusCommissionEmployee

#endif // BASEPLUS_H
```
```

**Fig. 20.15** | BasePlusCommissionEmployee class header.

```
```cpp
// Fig. 20.16: BasePlusCommissionEmployee.cpp
// BasePlusCommissionEmployee member-function definitions.
#include <iostream>
#include <iomanip>
#include "BasePlusCommissionEmployee.h"
using namespace std;

// constructor
BasePlusCommissionEmployee::BasePlusCommissionEmployee(
    const string &first, const string &last, const string &ssn,
    double sales, double rate, double salary )
    : CommissionEmployee( first, last, ssn, sales, rate )
{
    setBaseSalary( salary ); // validate and store base salary
} // end BasePlusCommissionEmployee constructor
```
```

**Fig. 20.16** | BasePlusCommissionEmployee class implementation file. (Part 1 of 2.)