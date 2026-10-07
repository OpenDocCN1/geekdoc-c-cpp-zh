Sum(),and then see how to convert it to an overloaded operator. Listing 11.1 shows the class declaration.

# Listing 11.1 mytime0.h

The Time class provides methods for adjusting and resetting times, for displaying time values, and for adding two times. Listing 11.2 shows the methods definitions; note how the AddMin() and Sum() methods use integer division and the modulus operator to adjust the minutes and hours values when the total number of minutes exceeds 59. Also because it is economical to use std::cout rather than the whole std namespace.

# Listing 11.2 mytime0.cpp

```
// mytime0.cpp -- implementing Time class
#include <iostream>
#include "mytime0.h"

Time::Time()
{
    hours = minutes = 0;
}

Time::Time(int h, int m)
{
    hours = h;
```