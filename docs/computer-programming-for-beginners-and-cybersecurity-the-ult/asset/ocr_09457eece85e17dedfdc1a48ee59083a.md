# Note

This program uses no user-defined functions.

The standard math library contains functions to perform each of the three calculations required.

These are:

+   - abs()
+   - sqrt()
+   - pow()

pow()

```
#include <iostream>

using namespace std;

#include <cmath>

void main(void)
{
    cout <<"The absolute value of -55 is "<<abs(-55)<< "\n";

    cout <<"The square root of 100 is "<<sqrt(100.0)<< "\n";

    cout <<"10 to the power of 5 is "<<pow(10,5)<< "\n";
}
```

The first thing to decide when writing this program is which header files to include.

To call abs(), sqrt(), and pow(), you need to include the header file cmath in a preprocessor directive.

You also need to include the header file iostream so that cin and cout statements can be used.

```
#include <iostream>
```