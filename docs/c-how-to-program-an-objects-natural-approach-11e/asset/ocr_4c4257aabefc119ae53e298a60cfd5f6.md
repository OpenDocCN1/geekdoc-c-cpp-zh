# 10.6.1 Invoking Base-Class Functions from Derived-Class Objects

Figure 10.7 reuses Section 10.3’s `SalariedEmployee` and `SalariedCommissionEmployee` classes. The example demonstrates aiming base-class and derived-class pointers at base-class and derived-class objects. The first two are natural and straightforward:

+   - We aim a base-class pointer at a base-class object and invoke base-class functionality.
+   - We aim a derived-class pointer at a derived-class object and invoke derived-class functionality.

Then, we demonstrate the *is-a* relationship between derived classes and base classes by aiming a base-class pointer at a derived-class object and showing that the base-class functionality is available in the derived-class object.

```
```cpp
// fig10_07.cpp
// Aiming base-class and derived-class pointers at base-class
// and derived-class objects, respectively.
#include <format>
#include <iostream>
#include "SalariedEmployee.h"
#include "SalariedCommissionEmployee.h"

int main() {
   // create base-class object
   SalariedEmployee salaried{"Sierra Demo", 500.0};

   // create derived-class object
   SalariedCommissionEmployee salariedCommission{
      "Ivano La", 300.0, 5000.0, 0.4};

   // output objects salaried and salariedCommission
   std::cout << std::format("{\n}\n{\n}\n",
      "DISPLAY BASE-CLASS AND DERIVED-CLASS OBJECTS",
      salaried.toString(), // base-class toString
      salariedCommission.toString()); // derived-class toString

   // natural: aim base-class pointer at base-class object
   SalariedEmployee* salariedPtr{&salaried};
   std::cout << std::format("{\n}\n{\n}\n",
      "CALLING TOSTRING WITH BASE-CLASS POINTER TO",
      "BASE-CLASS OBJECT INVOKES BASE-CLASS FUNCTIONALITY",
      salariedPtr->toString()); // base-class version

   // natural: aim derived-class pointer at derived-class object
   SalariedCommissionEmployee* salariedCommissionPtr{&salariedCommission};

   std::cout << std::format("{\n}\n{\n}\n",
      "CALLING TOSTRING WITH DERIVED-CLASS POINTER TO",
      "DERIVED-CLASS OBJECT INVOKES DERIVED-CLASS FUNCTIONALITY",
      salariedCommissionPtr->toString()); // derived-class version
}
```
```

**Fig. 10.7** | Assigning addresses of base-class and derived-class objects to base-class and derived-class pointers. (Part 1 of 2.)