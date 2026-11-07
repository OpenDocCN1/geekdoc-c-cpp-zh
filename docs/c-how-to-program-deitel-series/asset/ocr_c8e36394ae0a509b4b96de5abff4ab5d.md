+   n) A function that calls itself either directly or indirectly (i.e., through another function) is a(n) ______ function.
+   o) A recursive function typically has two components—one that provides a means for the recursion to terminate by testing for a(n) ______ case and one that expresses the problem as a recursive call for a slightly simpler problem than the original call.
+   p) It’s possible to have various functions with the same name that operate on different types or numbers of arguments. This is called function ______.
+   q) The ______ enables access to a global variable with the same name as a variable in the current scope.
+   r) The ______ qualifier is used to declare read-only variables.
+   s) A function ______ enables a single function to be defined to perform a task on many different data types.

# ### 6.2

For the program in Fig. 6.33, state the scope (either function scope, global namespace scope, block scope or function-prototype scope) of each of the following elements:

+   a) The variable x in main.
+   b) The variable y in cube.
+   c) The function cube.
+   d) The function main.
+   e) The function prototype for cube.
+   f) The identifier y in the function prototype for cube.

```
```cpp
// Exercise 6.2: Ex06_02.cpp
#include <iostream>
using namespace std;

int cube( int y ); // function prototype

int main()
{
    int x = 0;

    for ( x = 1; x <= 10; x++ ) // loop 10 times
        cout << cube( x ) << endl; // calculate cube of x and output results
} // end main

// definition of function cube
int cube( int y )
{
    return y * y * y;
} // end function cube
```
```

**Fig. 6.33** | Program for Exercise 6.2.

# ### 6.3

Write a program that tests whether the examples of the math library function calls shown in Fig. 6.2 actually produce the indicated results.

# ### 6.4

Give the function header for each of the following functions:

+   a) Function hypotense that takes two double-precision, floating-point arguments, side1 and side2, and returns a double-precision, floating-point result.
+   b) Function smallest that takes three integers, x, y and z, and returns an integer.
+   c) Function instructions that does not receive any arguments and does not return a value. **Note:** Such functions are commonly used to display instructions to a user.
+   d) Function intToDouble that takes an integer argument, number, and returns a double-precision, floating-point result.