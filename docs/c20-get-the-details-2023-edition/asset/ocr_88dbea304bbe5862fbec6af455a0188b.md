# # 4.4 Designated Initialization

![](bbox=[0.294, 0.168, 0.7, 0.374])

*Cippi receives the divine touch*

Designated initialization is a special case of aggregate initialization. Writing about designated initialization therefore means writing about aggregate initialization.

# ## 4.4.1 Aggregate Initialization

First: what is an aggregate? Aggregates are arrays or class types. A class type is a class, a struct, or a union.

With C++20, the following condition must hold for class types being aggregates and supporting, therefore, aggregate initialization:

+   - No private or protected non-static data members
+   - No user-declared or inherited constructors
+   - No virtual, private, or protected base classes
+   - No virtual member functions

The following program exemplifies aggregate initialization.

**Aggregate initialization**

```
~~~cpp
// aggregateInitialization.cpp

#include <iostream>

struct Point2D{
    int x;
    int y;
};
~~~
```