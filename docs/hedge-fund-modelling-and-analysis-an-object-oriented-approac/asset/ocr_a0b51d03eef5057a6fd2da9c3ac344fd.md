Obviously in all cases the prototype function for the constructor must match the function definition. The above constructor can also be written using the following notation:

```
AClass::AClass(int x, int y, int z)
{
    m_x(x);
    m_y(y);
    m_z(z);
}
```

It is also possible to initialise member variables using the colon operator (:), that is:

```
AClass::AClass : x(5)
{
}
```

Any additional member variables are initialised by separating with commas, for example:

```
AClass::AClass : x(5), y(4), z(3)
{
}
```

# 1.10.8 A More Detailed Class Example

Source 1.27 shows a more detailed example of a class dealing with bank accounts and balances. Many of the issues already discussed are covered in the example as well as some new concepts.

```
SOURCE 1.27: A DETAILED IMPLEMENTATION OF A BANK ACCOUNT AND BALANCES CLASS

// Bank.h
#pragma once

#include <string>
using std::string;

class Bank
```