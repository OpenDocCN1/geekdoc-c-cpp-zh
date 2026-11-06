```
```cpp
// Fig. 12.11: SalariedEmployee.h
// SalariedEmployee class derived from Employee.
#ifndef SALARIED_H
#define SALARIED_H

#include <string> // C++ standard string class
#include "Employee.h" // Employee class definition

class SalariedEmployee : public Employee {
public:
    SalariedEmployee(const std::string&, const std::string&,
        const std::string&, double = 0.0);
    virtual ~SalariedEmployee() = default; // virtual destructor

    void setWeeklySalary(double); // set weekly salary
    double getWeeklySalary() const; // return weekly salary

    // keyword virtual signals intent to override
    virtual double earnings() const override; // calculate earnings
    virtual std::string toString() const override; // string representation
private:
    double weeklySalary; // salary per week
};

#endif // SALARIED_H
```
```

Fig. 12.11 **SalariedEmployee** class header.

# SalariedEmployee Class Member-Function Definitions

**Figure 12.12** contains the member-function definitions for **SalariedEmployee**. The class’s constructor passes the first name, last name and social security number to the **Employee** constructor (line 12) to initialize the **private** data members that are inherited from the base class, but not directly accessible in the derived class. Function **earnings** (line 30) overrides pure **virtual** function **earnings** in **Employee** to provide a *concrete* implementation that returns the