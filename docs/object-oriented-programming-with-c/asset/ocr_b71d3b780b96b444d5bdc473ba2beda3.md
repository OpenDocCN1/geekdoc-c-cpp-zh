+   1. For functions returning values, if a loop, a switch, or a goto exists.
+   2. For functions not returning values, if a return statement exists.
+   3. If functions contain static variables.
+   4. If inline functions are recursive.

> NOTE: _Inline_ expansion makes a program run faster because the overhead of a function call and return is eliminated. However, it makes the program to take up more memory because the statements that define the inline function are reproduced at each point where the function is called. So, a trade-off becomes necessary.

Program 4.1 illustrates the use of inline functions.

# Program 4.1 Inline Functions

```
#include <iostream>
using namespace std;

inline float mul(float x, float y)
{
    return(x*y);
}

inline double div(double p, double q)
{
    return(p/q);
}

int main( )
{
    float a - 12.345;
    float b - 9.82;
}
```