```
// e3.cpp
#include <iostream>
#include "elevator.h"
using namespace std;
int main() {
    int i;
    Elevator *e[5];
    for (i = 0; i < 5; i++)
        e[i] = new Elevator;
    for (i = 0; i < 5; i++)
        cout << e[i]->getFloor() << endl;
    for (i = 0; i < 5; i++)
        delete e[i];
}
```

Below is a representation of the dynamic array created in the preceding program:

created on stack   created on heap

e
---
0 | •-----|------> [Elevator object]
1 | •-----|------> [Elevator object]
2 | •-----|------> [Elevator object]
3 | •-----|------> [Elevator object]
4 | •-----|------> [Elevator object]