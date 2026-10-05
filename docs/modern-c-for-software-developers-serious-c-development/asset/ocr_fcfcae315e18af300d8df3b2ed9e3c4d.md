```
// executes at compile-time; value n is set at compile-time
const int n = 100;
constexpr prod1 = square(n);

cout << prod1 << endl;
static_assert(prod1 == 10000); //succeeds
```

```
// executes at run-time; y is initialized at run-time
int y = 10;
square(y);

//static_assert(y == 100); // fails
cout << y << endl; // OK

}
```

When the arguments of a constexpr function are constexpr values, the constexpr function produces a compile-time constant. When called with non-constexpr arguments the function produces a value at run time like a regular function. This dual behaviour saves us from having to write constexpr and non-constexpr versions of the same function.

# Restrictions On Constexpr Functions

constexpr functions that have constexpr arguments and only call other constexpr functions will be evaluated at compile-time. constexpr functions cannot be virtual or allocate and de-allocate memory.

# Arrays And constexpr Functions

Prior to C++11, the declaration of an array could not contain the return value of a function. With C++11, this is now possible, providing that the function is a constexpr function that can be evaluated at compile-time:

```
#include <iostream>
constexpr int getDefaultArraySize(int base_size)
{
  return 2 * base_size;
}
```