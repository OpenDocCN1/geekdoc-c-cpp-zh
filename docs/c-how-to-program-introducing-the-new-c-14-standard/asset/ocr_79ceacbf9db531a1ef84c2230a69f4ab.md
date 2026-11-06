`public` services also include member functions `setBaseSalary`, `getBaseSalary`, `earnings` and `toString` (lines 15–19).

**Figure 11.11** shows `BasePlusCommissionEmployee`'s member-function implementations. The constructor (lines 10–16) introduces **base-class initializer syntax** (line 14), which uses a member initializer to pass arguments to the base-class (`CommissionEmployee`).

```
```cpp
 1  // Fig. 11.10: BasePlusCommissionEmployee.h
 2  // BasePlusCommissionEmployee class derived from class
 3  // CommissionEmployee.
 4  #ifndef BASEPLUS_H
 5  #define BASEPLUS_H
 6
 7  #include <string> // C++ standard string class
 8  #include "CommissionEmployee.h" // CommissionEmployee class declaration
 9
10  class BasePlusCommissionEmployee : public CommissionEmployee {
11  public:
12      BasePlusCommissionEmployee(const std::string&, const std::string&,
13          const std::string&, double = 0.0, double = 0.0, double = 0.0);
14
15      void setBaseSalary(double); // set base salary
16      double getBaseSalary() const; // return base salary
17
18      double earnings() const; // calculate earnings
19      std::string toString() const; // create string representation
20  private:
21      double baseSalary; // base salary
22  };
23
24  #endif
```
```

**Fig. 11.10** `BasePlusCommissionEmployee` class definition indicating inheritance relationship with class `CommissionEmployee`.