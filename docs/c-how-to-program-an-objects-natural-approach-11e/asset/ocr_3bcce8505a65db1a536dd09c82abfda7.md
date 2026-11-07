+   - The class’s private section now declares overrides for the base class’s private pure virtual function `getPay` and protected virtual function `getString` (Fig. 20.18, lines 24–25). Again, we declared `getString` private because this class is `final`, so no other classes can derive from it.
+   - The class’s member-function implementations (Fig. 20.19) now include overridden function `getPay` (lines 42–44) to return the commission calculation result and overridden function `getString` (lines 47–52) to get a `CommissionEmployee`’s string representation. Function `getString` calls `Employee`’s protected `getString` to get part of the string representation.

```
```cpp
// Fig. 20.18: CommissionEmployee.h
// CommissionEmployee class derived from Employee.
#pragma once
#include <string>
#include <string_view>
#include "Employee.h" // Employee class definition

class CommissionEmployee final : public Employee {
public:
    CommissionEmployee(std::string_view name, double grossSales,
        double commissionRate);
    virtual ~CommissionEmployee() = default; // virtual destructor

    void setGrossSales(double grossSales);
    double getGrossSales() const;

    void setCommissionRate(double commissionRate);
    double getCommissionRate() const;
private:
    double m_grossSales{0.0};
    double m_commissionRate{0.0};

    // keyword override signals intent to override
    double getPay() const override; // calculate earnings
    std::string getString() const override; // string representation
};
```
```

**Fig. 20.18** | CommissionEmployee class derived from Employee.

```
```cpp
// Fig. 20.19: CommissionEmployee.cpp
// CommissionEmployee class member-function definitions.
#include <format>
#include <stdexcept>
#include "CommissionEmployee.h" // CommissionEmployee class definition

// constructor
CommissionEmployee::CommissionEmployee(std::string_view name,
    double grossSales, double commissionRate) : Employee{name} {
    setGrossSales(grossSales);
```
```

**Fig. 20.19** | CommissionEmployee class member-function definitions. (Part 1 of 2.)