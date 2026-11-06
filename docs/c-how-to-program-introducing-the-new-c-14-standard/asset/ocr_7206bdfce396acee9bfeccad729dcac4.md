```
```cpp
// Exercise 6.2: ex06_02.cpp
#include <iostream>
using namespace std;

int cube(int y); // function prototype

int main() {
    int x{};

    for (x = 1; x <= 10; x++) { // loop 10 times
        cout << cube(x) << endl; // calculate cube of x and output results
    }
}

// definition of function cube
int cube(int y) {
    return y * y * y;
}
```
```

Fig. 6.30 Program for Exercise 6.2.

+   3. **6.3** Write a program that tests whether the examples of the math library function calls shown in **Fig. 6.2** actually produce the indicated results.

+   4. **6.4** Give the function header for each of the following functions:
+   
+      A. Function `hypotenuse` that takes two double-precision, floating-point arguments, `side1` and `side2`, and returns a double-precision, floating-point result.
+   
+      B. Function `smallest` that takes three integers, `x`, `y` and `z`, and returns an integer.
+   
+      C. Function `instructions` that does not receive any arguments and does not return a value. *[Note: Such functions are commonly used to display instructions to a user.]*
+   
+      D. Function `intToDouble` that takes an integer argument, `number`, and returns a double-precision, floating-point result.