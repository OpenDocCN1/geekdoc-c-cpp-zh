When an array of class objects comes into being. C++ calls the class default constructor once for each object in the array. In the case of the Elevator declaration above, C++ calls Elevator's default constructor 5 times, thus initializing objects e[0] through e[4] to the correct values.

If you want C++ to call a different constructor, you must explicitly initialize the array element directly in the array's declaration:

```
// e2.cpp

#include <iostream>
#include "elevator.h"

using namespace std;

int main() {
    Elevator e[5] = {
        Elevator(),
        Elevator(),
        Elevator(2, 5),
        Elevator(7, 3),
        Elevator()
    };
}
}
```

Note that sometimes braces are used as if we were initializing fields of a struct but some compilers are ok without them.

There is no easy way to initialize some array class objects using the default constructor and some using an alternate constructor. If you need to do that, it's probably best to use the default constructor for the entire array and then reinitialize selected objects as needed. Except for small arrays, this is probably too unwieldy to be of much practical use.

# Dynamic Arrays

Arrays of class objects may also be stored on the heap (free store) and addressed with pointers. The following program declares an array of pointers to Elevator objects. Storage for the array of pointers is allocated on the stack while storage for each of the actual Elevator objects is allocated on the heap.