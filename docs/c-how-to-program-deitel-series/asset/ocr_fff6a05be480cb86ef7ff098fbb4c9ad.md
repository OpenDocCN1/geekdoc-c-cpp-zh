```
```cpp
// Fig. 8.7: fig08_07.cpp
// Pass-by-reference with a pointer argument used to cube a
// variable’s value.
#include <iostream>
using namespace std;

void cubeByReference( int * ); // prototype

int main()
{
   int number = 5;

   cout << "The original value of number is " << number;

   cubeByReference( &number ); // pass number address to cubeByReference

   cout << "\nThe new value of number is " << number << endl;
} // end main

// calculate cube of *nPtr; modifies variable number in main
void cubeByReference( int *nPtr )
{
   *nPtr = *nPtr * *nPtr * *nPtr; // cube *nPtr
} // end function cubeByReference
```
```

```
The original value of number is 5
The new value of number is 125
```

Fig. 8.7 | Pass-by-reference with a pointer argument used to cube a variable’s value.

A function receiving an address as an argument must define a pointer parameter to receive the address. For example, the header for function cubeByReference (line 21) specifies that cubeByReference receives the address of an int variable (i.e., a pointer to an int) as an argument, stores the address in nPtr and does not return a value.

Function cubeByReference’s prototype (line 7) contains int * in parentheses. As with other types, it’s necessary to include the names of pointer parameters in prototypes. Parameter names included for documentation purposes are ignored by the compiler.

# Insight: All Arguments Are Passed By Value

In C++, all arguments are always passed by value. Passing a variable by reference with a pointer does not actually pass anything by reference—a pointer to that variable is passed by value and is copied into the function’s corresponding pointer parameter. The called function can then access that variable in the caller simply by dereferencing the pointer, thus accomplishing pass-by-reference.

# Graphical Analysis of Pass-By-Value and Pass-By-Reference

Figures 8.8–8.9 analyze graphically the execution of Fig. 8.6 and Fig. 8.7, respectively. In the diagrams, the values in blue rectangles above a given expression or variable represent the value of that expression or variable. Each diagram’s right column shows functions cubeByValue (Fig. 8.6) and cubeByReference (Fig. 8.7) only when they’re executing.