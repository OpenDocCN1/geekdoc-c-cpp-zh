
# 9.6 Custom Functions vs. Standard Functions

Armed with our knowledge of function definitions, we can rewrite Listing 8.1 (computeresquareoot.cpp) so the program uses a custom square root function. Listing 9.18 (squarerootfunction.cpp) shows one possibility.

```
Listing 9.18: squarerootfunction.cpp
#include <iostream>

using namespace std;

double square_root(double x) {
    double diff;
    // Compute a provisional square root
    double root = 1.0;
    do {
        // Loop until the provisional root
        // is close enough to the actual root
        root = (root + x) / 2.0;
        cout << "root is " << root << endl;
        // How bad is the approximation?
        diff = root * root - x;
    } while (diff > 0.0001 || diff < -0.0001);
    return root;
}

int main() {
    double input;
    // Get value from the user
    cout << "Enter number: ";
    cin >> input;
    // Report square root of
    cout << "Square root of " << input << " = " << square_root(input) << endl;
}
```

Is Listing 9.18 (squarerootfunction.cpp) better than using Listing 8.2 (standardsquareoot.cpp) which uses the standard sqrt function from the math library? Generally speaking, you have the choice of using a standard library function or writing your own custom function that provides the same functionality, choose to use the standard library. The advantages of using a standard library include:

- *Your effort to produce the custom code is eliminated entirely; you can devote more to other parts of your application's development.*
- If you write your own custom code, you must thoroughly test it to ensure its correctness: standard library code, while not immune to bugs, has been subjected to a comprehensive test suite. Standard library code is used by many programmers; your code is exercised only by the programs you write, and errors may not appear immediately. If your programs are not used by a wide audience, bugs may lie dormant for a long time. Standard library routines are well known and trusted; custom code, due to its limited exposure, is suspect until its wider exposure and adoption.
- *Standard routines are typically tuned to be very efficient; it takes a great deal of effort to make custom code efficient.*
- *Standard routines are well-documented; extra work is required to document custom code, and writing good documentation is hard work.*

Listing 19: squarootcomparison.cpp tests our custom square root function over a range of 1,000,000,000 floating-point values.

```
Listing 19: squarootcomparison.cpp
#include <iostream>
#include <cmath>

using namespace std;

// Compare two floating-point numbers equal when
// the difference between them is very small.
bool equals(double a, double b, double tolerance) {
    return a == b || fabs(a - b) < tolerance;
}

double square_root(double x) {
    // Compute a provisional square root
    double root = 1.0;
    do {
        // Loop until the provisional root
        // is close enough to the actual root
        root = (root + x /root) / 2.0;
    } while (!equals(root+root, x, 0.0001));
    return root;
}

int main() {
    for (double d = 0.0; d < 100000.0; d += 0.001) {
        if (equals(square(d), sqrt(d), 0.001)) {
            cout << d << " Expected: " << sqrt(d) << " , but computed "
                 << square_root(d) << endl;
        }
    }
}
```

Listing 19.9 (squarootcomparison.cpp) uses our equals function from Listing 9.16 (floatequals.cpp).
The third parameter specifies a tolerance; if the difference between the two parameters is less than the tolerance, the first two parameters are considered equal. Our custom square_root function uses the equals function. The main function uses the equals function as well. Observe, hover, that the tolerance used within the square root is smaller than the tolerance main uses to check the result. The main function, therefore, uses a less strict notion of equality.

The output of Listing 19.9 (squarootcomparison.cpp):

```
0: Expected 0, but computed 0.0078125
0.0001: Expected 0.01, but computed 0.0116755
0.0008: Expected 0.0282843, but computed 0.0298389
0.0009: Expected 0.03, but computed 0.0313164
0.001: Expected 0.0316228, but computed 0.0327453
```

shows that our square root function produces results of main's acceptable tolerance for few values. Five wrong answers out of one billion tests represents a 0.000005% error rate. This error rate is very small, our square_root function is not perfect. One of values that causes the function to fail may very important to a particular application, so our function is not trustworthy.

# 9.7 Summary

- *The development of larger, more complex programs is more manageable when the program consists of multiple programmer-defined functions.*
- *Every function has one definition but can have many invocations.*
- *A function definition includes the function's name, parameters, return type, and body.*
- *A function name, like a variable name, is an identifier.*
- *Formal parameters are the parameters as they appear in a function's definition; actual parameters are the arguments supplied by the caller.*
- *Formal parameters are essentially local to the function; actual parameters may be variables, expressions, or literal values.*
- *The values of the actual parameters are copied into the formal parameters when a function is invoked.*
- *Callers pass values to the number of parameters specified in the function definition. The types of the actual parameters must be compatible with the types of the formal parameters.*
- *With C++ pass-by-value mechanism, modifying a parameter will not affect the caller's variable.*
- *Variables declared within a function are local to that function.*
- *When a particular function is finished, space allocated for its variables is freed up.*

# 9.8 Exercises

1. Is the following a legal C++ program?
```
int proc(int x) {
    return x + 2;
}
int proc(int n) {
    return 2*n + 1;
}
int main() {
    int x = proc(5);
}
```

2. Is the following a legal C++ program?
```cpp
int proc(int x) {
    return x + 2;
}
int main() {
    int x = proc(5),
    y = proc(4);
}
```

3. Is the following a legal C++ program?
```cpp
#include <iostream>
void proc(int x) {
    std::cout << x + 2 << std::endl;
}
int main() {
    int x = proc(5);
}
```

4. Is the following a legal C++ program?
```cpp
#include <iostream>
void proc(int x) {
    std::cout << x + 2 << std::endl;
}
int main() {
    proc(5);
}
```

5. Is the following a legal C++ program?
```cpp
#include <iostream>

int proc(int x, int y) {
    return 2*x + y;
}

int main() {
    std::cout << proc(5, 4) << std::endl;
}
```

6. Is the following a legal C++ program?
```cpp
#include <iostream>

int proc(int x, int y) {
    return 2*x + y;
}

int main() {
    std::cout << proc(5, 4) << std::endl;
}
```

7. Is the following a legal C++ program?
```cpp
#include <iostream>

int proc(int x) {
    return 2*x*x;
}

int main() {
    std::cout << proc(5, 4) << std::endl;
}
```

8. Is the following a legal C++ program?
```cpp
#include <iostream>

proc(int x) {
    std::cout << 2*x+x << std::endl;
}

int main() {
    proc(5);
}
```

9. The programmer was expecting the following program to print 200. What does it print instead? Why does it print what it does?
```cpp
#include <iostream>

void proc(int x) {
```
