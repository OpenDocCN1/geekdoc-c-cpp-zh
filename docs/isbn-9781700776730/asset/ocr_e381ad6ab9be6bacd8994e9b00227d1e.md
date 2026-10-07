```
// parraydr.cpp

#include <iostream>
#include "array.h"

using namespace std;

int main() {
    PseudoArray pa(10, 20, 30, 40);

    for (int i = 0; i < 4; i++) {
        cout << "pa[" << i << "] == " << pa[i] << endl;
    }
    return 0;
}
```

# // array output

pa[0] == 10
pa[1] == 20
pa[2] == 30
pa[3] == 40

To get a data element we might have previously said:

```
cout << pa.getInt();
```

We can now say:

```
cout << pa[i];
```

We are using object pa as if it were an array! Overloading the subscript operator makes it possible to use array indexing rather than call member functions for an object of a class.

The overloaded subscript operator function can only be a class member:

```
pa[i] -> pa.operator[](i);
```