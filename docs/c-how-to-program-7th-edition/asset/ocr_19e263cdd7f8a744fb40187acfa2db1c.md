Figure 8.7 passes the variable number to function cubeByReference using pass-by-reference with a pointer argument (line 15)—the address of number is passed to the function. Function cubeByReference (lines 21–24) specifies parameter nPtr (a pointer to int) to receive its argument. The function dereferences the pointer and cubes the value to which nPtr points (line 23). This directly changes the value of number in main.

![](bbox=[0.16, 0.215, 0.217, 0.256])

# Common Programming Error 8.5

Not dereferencing a pointer when it's necessary to do so to obtain the value to which the pointer points is an error.

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

// Calculate cube of *nPtr; modifies variable number in main
void cubeByReference( int *nPtr )
{
   *nPtr = *nPtr * *nPtr * *nPtr; // cube *nPtr
} // end function cubeByReference
```
```

```
```text
The original value of number is 5
The new value of number is 125
```
```

**Fig. 8.7**  Pass-by-reference with a pointer argument used to cube a variable’s value.

A function receiving an address as an argument must define a pointer parameter to receive the address. For example, the header for function cubeByReference (line 21) specifies that cubeByReference receives the address of an int variable (i.e., a pointer to an int) as an argument, stores the address locally in nPtr and does not return a value.

The function prototype for cubeByReference (line 7) contains int * in parentheses. As with other variable types, it isn’t necessary to include names of pointer parameters in function prototypes. Parameter names included for documentation purposes are ignored by the compiler.

Figures 8.8–8.9 analyze graphically the execution of the programs in Fig. 8.6 and Fig. 8.7, respectively.