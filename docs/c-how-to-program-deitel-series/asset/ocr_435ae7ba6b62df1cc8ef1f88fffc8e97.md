```
```cpp
// Fig. 10.12: fig10_12.cpp
// Single-argument constructors and implicit conversions.
#include <iostream>
#include "Array.h"
using namespace std;

void outputArray( const Array & ); // prototype

int main()
{
   Array integers1( 7 ); // 7-element Array
   outputArray( integers1 ); // output Array integers1
   outputArray( 3 ); // convert 3 to an Array and output Array's contents
} // end main

// print Array contents
void outputArray( const Array &arrayToOutput )
{
   cout << "The Array received has " << arrayToOutput.getSize()
        << " elements. The contents are:\n" << arrayToOutput << endl;
} // end outputArray
```
```

```
```
The Array received has 7 elements. The contents are:
      0       0       0       0       0       0       0

The Array received has 3 elements. The contents are:
      0       0       0
```
```

**Fig. 10.12** | Single-argument constructors and implicit conversions.

# Preventing Implicit Conversions with Single-Argument Constructors

The reason we've been declaring every single-argument constructor preceded by the keyword `explicit` is to suppress implicit conversions via conversion constructors when such conversions should not be allowed. A constructor that's declared `explicit` cannot be used in an implicit conversion. In the example of Fig. 10.13, we use the original version of Array.h from Fig. 10.10, which included the keyword `explicit` in the declaration of the single-argument constructor in line 14.

```
```cpp
explicit Array( int = 10 ); // default constructor
```
```

Figure 10.13 presents a slightly modified version of the program in Fig. 10.12. When this program in Fig. 10.13 is compiled, the compiler produces an error message indicating that the integer value passed to `outputArray` in line 13 cannot be converted to a `const Array &`. The compiler error message (from Visual C++ 5) is shown in the output window. Line 14 demonstrates how the explicit constructor can be used to create a temporary Array of 3 elements and pass it to function `outputArray`.

![](bbox=[0.13, 0.882, 0.191, 0.926])

# Error-Prevention Tip 10.4

Always use the `explicit` keyword on single-argument constructors unless they're intended to be used as conversion constructors.