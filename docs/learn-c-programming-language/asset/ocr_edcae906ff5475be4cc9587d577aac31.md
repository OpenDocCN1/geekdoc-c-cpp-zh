```
```cpp
int temp;

temp = x; /* save the value at address x */
x = y;    /* put y into x */
y = temp; /* put x into y */

return;
}
```
```

When the above code is compiled and executed, it produces the following result:

```
```
Before swap, value of a :100
Before swap, value of b :200
After swap, value of a :200
After swap, value of b :100
```
```

# Reference as Return Value

A C++ program can be made easier to read and maintain by using references rather than pointers. A C++ function can return a reference in a similar way as it returns a pointer.

When a function returns a reference, it returns an implicit pointer to its return value. This way, a function can be used on the left side of an assignment statement. For example, consider this simple program:

```
```cpp
#include <iostream>

#include <ctime>

using namespace std;

double vals[] = {10.1, 12.6, 33.1, 24.1, 50.0};

double& setValues( int i )
{
    return vals[i];   // return a reference to the ith element
}

// main function to call above defined function.
int main ()
```
```