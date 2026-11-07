```
```cpp
// set name
void Employee::setName(std::string_view name) {m_name = name;}

// get name
std::string Employee::getName() const {return m_name;}

// public non-virtual function; returns Employee's earnings
double Employee::earnings() const {return getPay();}

// public non-virtual function; returns Employee's string representation
std::string Employee::toString() const {return getString();}

// protected virtual function that derived classes can override and call
std::string Employee::getString() const {
    return std::format("name {}", getName());
}
```
```

**Fig. 20.15**  |  Abstract-base-class `Employee` member-function definitions. (Part 2 of 2.)

# Updated Class SalariedEmployee

Our restructured `SalariedEmployee` class (Figs. 20.16–20.17) has several key changes:

+   - The class’s header (Fig. 20.16) no longer contains prototypes for the `earnings` and `toString` member functions. These **public non-virtual** base-class functions are now inherited from `Employee`.
+   - The class’ private section now declares overrides for the base class’s private pure virtual function `getPay` and protected virtual function `getString` (Fig. 20.16, lines 19–20). Function `getString` is private in `SalariedEmployee` because this class is final, so no other classes can derive from it.
+   - The class’s member-function implementations (Fig. 20.17) now include overridden function `getPay` (line 27) to return the salary and overridden function `getString` (lines 30–33) to get a `SalariedEmployee`’s string representation. Note that a `SalariedEmployee`’s `getString` calls `Employee`’s protected `getString` to get part of the string representation.

```
```cpp
// Fig. 20.16: SalariedEmployee.h
// SalariedEmployee class derived from Employee.
#pragma once
#include <string> // ++ standard string class
#include <string_view>
#include "Employee.h" // Employee class definition

class SalariedEmployee final : public Employee {
public:
    SalariedEmployee(std::string_view name, double salary);
    virtual ~SalariedEmployee() = default; // virtual destructor

    void setSalary(double salary);
    double getSalary() const;
```
```

**Fig. 20.16**  |  `SalariedEmployee` class derived from `Employee`. (Part 1 of 2.)