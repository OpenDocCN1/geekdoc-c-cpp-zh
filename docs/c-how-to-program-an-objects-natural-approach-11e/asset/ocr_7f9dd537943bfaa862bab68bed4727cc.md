```
```cpp
#include "Employee.h"

// constructor performs "constructor injection" to initialize
// the CompensationModel pointer to a CompensationModel implementation
Employee::Employee(std::string_view name, CompensationModel* modelPtr)
    : m_name{name}, m_modelPtr{modelPtr} {}

// set function performs "property injection" to change the
// CompensationModel pointer to a new CompensationModel implementation
void Employee::setCompensationModel(CompensationModel* modelPtr) {
    m_modelPtr = modelPtr;
}

// use the CompensationModel to calculate the Employee's earnings
double Employee::earnings() const {
    return m_modelPtr->earnings();
}

// return string representation of Employee object
std::string Employee::toString() const {
    return std::format("{}\n", m_name, m_modelPtr->toString());
}
```
```

**Fig. 10.21**  |  Class `Employee` member-function definitions. (Part 2 of 2.)

# 10.11.3 CompensationModel Implementations

Next, let’s define our CompensationModel implementations. Objects of these classes will be injected into Employee objects to specify how to calculate their earnings.

# Salaried Derived Class of CompensationModel

A salaried compensation model (Figs. 10.22–10.23) defines how to pay an Employee who receives a fixed salary. The class contains a m_salary data member and overrides interface CompensationModel’s earnings and toString member functions. **Salaried is declared final** (line 7), so it is a leaf node in the **CompensationModel** hierarchy. It may not be used as a base class.

```
```cpp
// Fig. 10.22: Salaried.h
// Salaried implements the CompensationModel interface.
#pragma once
#include <string>
#include "CompensationModel.h" // CompensationModel definition

class Salaried final : public CompensationModel {
public:
    explicit Salaried(double salary);
    double earnings() const override;
    std::string toString() const override;
private:
    double m_salary{0.0};
};
```
```

**Fig. 10.22**  |  Salaried implements the CompensationModel interface.