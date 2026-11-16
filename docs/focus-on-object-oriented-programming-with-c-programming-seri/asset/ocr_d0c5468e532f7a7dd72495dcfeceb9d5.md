```
// parray.h

#ifndef __PARRAY_H
#define __PARRAY_H

class PseudoArray {
private:
    int value0, value1, value2, value3;
public:
    PseudoArray(int v0, int v1, int v2, int v3);
    int getInt(int i);
    int operator[](int i);
};

#endif
```

```
// parray.cpp

#include "parray.h"

PseudoArray::PseudoArray(int v0, int v1, int v2, int v3) {
    value0 = v0;
    value1 = v1;
    value2 = v2;
    value3 = v3;
}

int PseudoArray::getInt(int i) {
    switch(i) {
        case 0 : return value0;
        case 1 : return value1;
        case 2 : return value2;
        case 3 : return value3;
        default: return value0;
    }
}

int PseudoArray::operator[](int i) {
    return getInt(i);
}
```