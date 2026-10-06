# 7.5 Identification and Access of Derived-Class Member — 291

![](bbox=[0.1, 0.083, 0.769, 0.355])

**Figure 7.8:** The derivation relations among the classes, and the structure and memory allocation of the derived class.

The above statement declares that the base class of the derived class is a virtual base class. In multiple inheritance, the specified inheritance mode, the key word “virtual” takes effect only on the base class it follows closely. After declaring the virtual base class, the members of the virtual base class will maintain the same data copy in memory as the derived class in further derivations.

**Example 7.8:** Example of virtual base class.

Let us consider the problem mentioned before. Data member *nV* and function *fun* are declared in the base class *BO*. Class *B1* and *B2* both are derived publicly from *BO*. The difference from the previous example is that *BO* is declared as a virtual base class during the derivations. A new class *D1* is derived from *B1* and *B2* publicly. We do not add members with the same name in class *D1*. (If there is a member with the same name, it should obey the hiding rule.) So in class *D1*, members *nV* and *fun* in base class *BO* will have only one copy respective. The derivation relations among the classes and the structure and memory allocation of the derived class are shown in Figure 7.8.

There is only one copy of data member *nV* and function *fun* in the derived class *DI* after using the virtual base class mechanism. In the module, when creating objects of class *DI*, the members are accessible by using the term “object name . member name”.

```
//7_8.cpp
#include <iostream>
using namespace std;
class B0
//define base class B0
(
```