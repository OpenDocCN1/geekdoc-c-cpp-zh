# Output with cout 1085

Here fmtflags is a typedef name for a bitmask type (the following Note) used to hold the format flags. The name is defined in the ios_base class.This version of set() is used for setting format information controlled by a single bit. The argument is fmtflags value that indicates which bit to set. The return value is a fmtflags number that you can then save that value if you want to restore the original settings. What value do you pass to set()? If you want to set number 11 to 1, you pass a number that has number 11 bit set to 1. The return value would have its number 11 bit assigned the prior value for that. Keeping track of bits (and indices) is tedious. However, you don't have to do that job; the ios_base class defines constants that repeat the bit values. Table 17.1 shows some of these definitions.

# Table 17.1 Formatting Constants

| Constant | Meaning |
|---|---|n| ios_base::boolalpha | Input and output bool values as true and false. |
| ios_base::showbase | Use C++ prefixes (0,Ox) on output. |
| ios_base::showpoint | Show trailing decimal point. |
| ios_base::uppercase | Use uppercase letters for hex output, E notation. |
| ios_base::showpos | Use + before positive numbers |

> Note
A bitmask type is a type that is used to store individual bit values. It could be an integer type, an enum, or an STL bit container. The main idea is that each bit is individually accessible and has its own meaning. The iostream package uses bit masks to store state information.

Because these formatting constants are defined within the ios_base class, you must use the scope-resolution operator with them. That is, you must use ios_base::uppercase, not just uppercase. If you don't use a directive or using declaration, you can use the scope-resolution operator to indicate that these names are in the std namespace, for use std::ios_base::showpos, and so on. Changes remain until they are overridden. Listing 17.8 uses little of these constants.

# Listing 17.8 setf.cpp

```
// setf.cpp -- using setf() to control formatting
#include <iostream>

int main()
{
    using std::cout;
    using std::endl;
    using std::ios_base;

    int temperature = 63;
```