# 2.7 STORAGE CLASS SPECIFIERS

There are four storage class specifiers, extern, register, auto, and static. Declarations with the auto or register storage class specifier result in automatic storage and those with the extern or static storage class specifier result in static storage. Out of these, extern, register, and auto have effects similar to that in C, but static is extended in C++ for use in some specific circumstances and is explained in detail in Chapter 3.

# 2.8 INITIALIZATION

When declaring a regular local variable, its value is, by default, undetermined. For a variable to store a concrete value as it is declared, it needs to be initialized. There are two ways of doing this in C++. These are discussed in Sections 2.8.1 and 2.8.2.

# 2.8.1 Normal Initialization

To understand the normal initialization method, consider the following code:

```
#include <iostream>
using namespace std;
void main()
{
    int i;
    i = 50;        // Some other code related to i
    int j;         // This will not work in C
    j = 20;
}
```

This method of initialization is the same as that in C. However, C++ has a philosophical diversion from C in this case. It assumes that if a variable is defined near to its usage, it is easier and more readable. So, it allows a variable definition to appear after executable statements. In C++, a variable can be defined anywhere in the program before its first usage. The declaration style that suits the programmer can be followed. Whether it is the C style of defining all variables before the actual program or the C++ style of postponing the defining of a variable until its first usage, it does not have any impact on the efficiency of the program.

# 2.8.2 Variable Initialization

In C++, variables can be initialized at run-time. Let us consider the following program:

```
//VarInitialization.cpp
#include <iostream>
using namespace std;
#include <cmath>        // This is math.h in C and in older C++
void main()
{
    int FirstVariable;
    FirstVariable = 50;
    // some other code related to FirstVariable
```