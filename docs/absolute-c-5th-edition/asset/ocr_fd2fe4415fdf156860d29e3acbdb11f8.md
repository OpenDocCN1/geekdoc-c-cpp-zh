# Programming with Inheritance

Display 14.10 Interface for the Derived Class PFArrayDbak (part 2 of 2)

```
// If backup has never been invoked, this empties the partially
// filled array.
PFArrayDBak& operator = (const PFArrayDBak& rightSide);

~PFArrayDBak(();
private:
    double *b; // for a backup of main array.
    int usedB; //backup for inherited member variable used.

#endif //PFRAYDHD
```

Display 14.11 Implementation for the Derived Class PFArrayDbak (part 1 of 2)

```
// This is the file pfarraybak.cpp.
// This is the implementation of the class PFArrayDbak.
// The interface for the class PFArrayDbak is in the file pfarraybak.h.
#include "pfarraybak.h"
#include <iostream>
using std::cout;

PFArrayDBak::PFArrayDbak() : PFArrayD(), usedB( 0)
{
    b = new double[capacity];
}
PFArrayDBak::PFArrayDbak(int capacityValue) :
    PFArrayDbak(capacityValue), usedB(0)
{
    b = new double[capacity];
}

PFArrayDBak::PFArrayDbak(const PFArrayDbak& oldObject)
    : PFArrayDbak(oldObject), usedB(0)
{
    b = new double[capacity];
    usedB = oldObject.usedB;
    for (int i = 0; i < usedB; i++)
        b[i] = oldObject.b[i];
}

void PFArrayDbak::backup( )
{
    usedB = used;
    for (int i = 0; i < usedB; i++)
        b[i] = a[i];

```

> Note that b is a copy of the array. We do not want to use b = a;

(continued)