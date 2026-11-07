neither `setGrossSales` and `setCommissionRate` member functions nor data members `m_grossSales` and `m_commissionRate` to set. If this were allowed, it could lead to problems because member functions `setGrossSales` and `setCommissionRate` would assume data members `m_grossSales` and `m_commissionRate` exist at their “usual locations” in a `SalariedCommissionEmployee` object. A `SalariedEmployee` object’s memory does not have these data members, so `setGrossSales` and `setCommissionRate` might overwrite other data in memory.

# 10.6.3 Derived-Class Member-Function Calls via Base-Class Pointers

The compiler allows us to invoke only base-class member functions via a base-class pointer. So, a compilation error occurs if a base-class pointer is aimed at a derived-class object and an attempt is made to access a derived-class-only member function. Figure 10.9 shows the compiler errors for invoking a derived-class-only member function via a base-class pointer (lines 22–24).

```
```cpp
// fig10_09.cpp
// Attempting to call derived-class-only functions
// via a base-class pointer.
#include <string>
#include "SalariedEmployee.h"
#include "SalariedCommissionEmployee.h"

int main() {
   SalariedCommissionEmployee salariedCommission{
      "Ivano Lai", 300.0, 5000.0, 0.04};

   // aim base-class pointer at derived-class object (allowed)
   SalariedEmployee* salariedPtr{&salariedCommission};

   // invoke base-class member functions on derived-class
   // object through base-class pointer (allowed)
   std::string name{salariedPtr->getName()};
   double salary{salariedPtr->getSalary()};

   // attempt to invoke derived-class-only member functions
   // on derived-class object through base-class pointer (disallowed)
   double grossSales{salariedPtr->getGrossSales()};
   double commissionRate{salariedPtr->getCommissionRate()};
   salariedPtr->setGrossSales(8000.0);
}
```
```

*GNU C++ compiler error messages:*

```
```text
fig10_09.cpp: In function ‘int main()’:
fig10_09.cpp:22:35: error: ‘class SalariedEmployee’ has no member named
‘getGrossSales’
   22 |     double grossSales{salariedPtr->getGrossSales()};
      |                       ~~~~~~~~~~~~^~~~~~~~~~~~~~~
```
```

**Fig. 10.9**  Attempting to call derived-class-only functions via a base-class pointer. (Part 1 of 2.)