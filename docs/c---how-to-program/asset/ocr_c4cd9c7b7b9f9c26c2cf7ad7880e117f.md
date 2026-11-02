# Overloaded square Functions

Figure 15.10 uses overloaded square functions to calculate the square of an int (lines 7–11) and the square of a double (lines 14–18). Line 22 invokes the int version of function square by passing the literal value 7. C++ treats whole-number literal values as type int by default. Similarly, line 24 invokes the double version of function square by passing the literal value 7.5, which C++ treats as a double value by default. In each case the compiler chooses the proper function to call, based on the type of the argument. The outputs confirm that the proper function was called in each case.

```
```cpp
// Fig. 15.10: fig15_10.cpp
// Overloaded square functions.
#include <iostream>
using namespace std;

// function square for int values
int square( int x )
{
    cout << "square of integer " << x << " is ";
    return x * x;
}

// function square for double values
double square( double y )
{
    cout << "square of double " << y << " is ";
    return y * y;
}

int main()
{
    cout << square( 7 ); // calls int version
    cout << endl;
    cout << square( 7.5 ); // calls double version
    cout << endl;
}
```
```

```
square of integer 7 is 49
square of double 7.5 is 56.25
```

Fig. 15.10 | Overloaded square functions.

# How the Compiler Differentiates Overloaded Functions

Overloaded functions are distinguished by their signatures—a combination of a function's name and its parameter types in order (but not its return type). The compiler encodes each function identifier with the number and types of its parameters (sometimes referred to as name mangling or name decoration) to enable type-safe linkage. This ensures that the proper overloaded function is called and that the argument types conform to the parameter types.

+   1. The C++ standard requires float, double and long double overloaded versions of the math library functions discussed in Section 5.3.