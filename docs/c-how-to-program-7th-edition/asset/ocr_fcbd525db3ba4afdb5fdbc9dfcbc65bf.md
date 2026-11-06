```
```cpp
const int increment; // const data member
}; // end class Increment

#endif
```
```

Fig. 10.7 | Increment class definition containing non-const data member count and const data member increment. (Part 2 of 2.)

```
```cpp
// Fig. 10.8: Increment.cpp
// Erroneous attempt to initialize a constant of a built-in data
// type by assignment.
#include <iostream>
#include "Increment.h" // include definition of class Increment
using namespace std;

// constructor; constant member "increment" is not initialized
Increment::Increment( int c, int i )
{
   count = c; // allowed because count is not constant
   increment = i; // ERROR: Cannot modify a const object
} // end constructor Increment

// print count and increment values
void Increment::print() const
{
   cout << "count = " << count << ", increment = " << increment << endl;
} // end function print
```
```

Fig. 10.8 | Erroneous attempt to initialize a constant of a built-in data type by assignment.

```
```cpp
// Fig. 10.9: fig10_09.cpp
// Program to test class Increment.
#include <iostream>
#include "Increment.h" // include definition of class Increment
using namespace std;

int main()
{
   Increment value( 10, 5 );

   cout << "After incrementing: ";
   value.print();

   for ( int j = 1; j <= 3; j++ )
   {
      value.addIncrement();
      cout << "After increment " << j << ": ";
      value.print();
   } // end for
} // end main
```
```

Fig. 10.9 | Program to test class Increment generates compilation errors. (Part 1 of 2.)