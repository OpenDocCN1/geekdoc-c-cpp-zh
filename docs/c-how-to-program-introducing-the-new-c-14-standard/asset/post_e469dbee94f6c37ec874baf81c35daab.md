
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

Fig. 6.30 Program for Exercise 6.2.

- 3. **6.3** Write a program that tests whether the examples of the math library function calls shown in **Fig. 6.2** actually produce the indicated results.
- 4. **6.4** Give the function header for each of the following functions:
  - A. Function `hypotenuse` that takes two double-precision, floating-point arguments, `side1` and `side2`, and returns a double-precision, floating-point result.
  - B. Function `smallest` that takes three integers, `x`, `y` and `z`, and returns an integer.
  - C. Function `instructions` that does not receive any arguments and does not return a value. *[Note: Such functions are commonly used to display instructions to a user.]*
  - D. Function `intToDouble` that takes an integer argument, `number`, and returns a double-precision, floating-point result.
- 5. **6.5** Give the function prototype (without parameter names) for each of the following:
  - A. The function described in **Exercise 6.4(a)**.
  - B. The function described in **Exercise 6.4(b)**.
  - C. The function described in **Exercise 6.4(c)**.
  - D. The function described in **Exercise 6.4(d)**.
- 6. **6.6** Write a declaration for double-precision, floating-point variable `lastVal` that should retain its value between calls to the function in which it’s defined.
- 7. **6.7** Find the error(s) in each of the following program segments, and explain how the error(s) can be corrected (see also **Exercise 6.46**):
  - A.

```cpp
void g() {
    cout << "Inside function g" << endl;
    void h() {
        cout << "Inside function h" << endl;
    }
}
```

  - B.

```cpp
int sum(int x, int y) {
    int result(0);
    result = x + y;
}
```

  - C.

```cpp
int sum(int n) { // assume n is nonnegative
    if (0 == n)
        return 0;
    else
        n + sum(n - 1);
}
```

  - D.

```cpp
void f(double a); {
    float a;
    cout << a << endl;
}
```

  - E.

```cpp
void product() {
    int a{0};
    int b{0};
    int c{0};
    cout << "Enter three integers: ";
    cin >> a >> b >> c;
    int result(a * b * c);
    cout << "Result is " << result;
    return result;
}
```

- 8. **6.8** Why would a function prototype contain a parameter type declaration such as `double&`?
- 9. **6.9** **(True/False)** All arguments to function calls in C++ are passed by value.
- 10. **6.10** Write a complete program that prompts the user for the radius of a sphere, and calculates and prints the volume of that sphere. Use an `inline` function `sphereVolume` that returns the result of the following expression: `(4.0 / 3.0 * 3.14159 * pow(radius, 3))`.

# Answers to Self-Review Exercises

- 1. **6.1**
  - A. functions, classes.
  - B. function call.
  - C. local variable.
  - D. `return`.
  - E. `void`.
  - F. scope.
  - G. `return;`, `return expression;` or encounter the closing right brace of a function.
  - H. function prototype.
  - I. `rand`.
  - J. `srand`.
  - K. global.
  - L. `static`.
  - M. recursive.
  - N. base.
  - O. overloading.
  - P. unary scope resolution operator (`::`).
  - Q. `const`.
  - R. template.
- 2. **6.2**
  - A. block scope.
  - B. block scope.
  - C. global namespace scope.
  - D. global namespace scope.
  - E. global namespace scope.
- 3. **6.3** See the following program:

```cpp
1    // Exercise 6.3: ex06_03.cpp
2    // Testing the math library functions.
    #include <iostream>
    #include <iomanip>
    #include <cmath>
    using namespace std;

    int main() {
        cout << fixed << setprecision(1);

        cout << "sqrt(" << 9.0 << ") = " << sqrt(9.0);
        cout << "\nexp(" << 1.0 << ") = " << setprecision(6)
             << exp(1.0) << "\nexp(" << setprecision(1) << 2.0
             << ") = " << setprecision(6) << exp(2.0);
        cout << "\nlog(" << 2.718282 << ") = " << setprecision(1)
             << log(2.718282)
             << "\nlog(" << setprecision(6) << 7.389056 << ") = "
             << setprecision(1) << log(7.389056);
        cout << "\nlog10(" << 10.0 << ") = " << log10(10.0)
             << "\nlog10(" << 100.0 << ") = " << log10(100.0);
        cout << "\nfabs(" << 5.1 << ") = " << fabs(5.1)
             << "\nfabs(" << 0.0 << ") = " << fabs(0.0)
             << "\nfabs(" << -8.76 << ") = " << fabs(-8.76);
        cout << "\nceil(" << 9.2 << ") = " << ceil(9.2)
             << "\nceil(" << -9.8 << ") = " << ceil(-9.8);
26      cout << "\nfloor(" << 9.2 << ") = " << floor(9.2)
27           << "\nfloor(" << -9.8 << ") = " << floor(-9.8);
28      cout << "\npow(" << 2.0 << ", " << 7.0 << ") = "
29           << pow(2.0, 7.0) << "\npow(" << 9.0 << ", "
30           << 0.5 << ") = " << pow(9.0, 0.5);
31      cout << setprecision(3) << "\nfmod("
32           << 2.6 << ", " << 1.2 << ") = "
33           << fmod(2.6, 1.2) << setprecision(1);
34      cout << "\nsin(" << 0.0 << ") = " << sin(0.0);
35      cout << "\ncos(" << 0.0 << ") = " << cos(0.0);
36      cout << "\ntan(" << 0.0 << ") = " << tan(0.0) <<
             endl;
37 }
```

```text
sqrt(9.0) = 3.0
exp(1.0) = 2.718282
exp(2.0) = 7.389056
log(2.718282) = 1.0
log(7.389056) = 2.0
log10(10.0) = 1.0
log10(100.0) = 2.0
fabs(5.1) = 5.1
fabs(0.0) = 0.0
fabs(-8.8) = 8.8
ceil(9.2) = 10.0
ceil(-9.8) = -9.0
floor(9.2) = 9.0
floor(-9.8) = -10.0
pow(2.0, 7.0) = 128.0
pow(9.0, 0.5) = 3.0
fmod(2.600, 1.200) = 0.200
sin(0.0) = 0.0
cos(0.0) = 1.0
tan(0.0) = 0.0
```

- 4. **6.4**
  - A. `double hypotenuse(double side1, double side2)`
  - B. `int smallest(int x, int y, int z)`
  - C. `void instructions()`
  - D. `double intToDouble(int number)`
- 5. **6.5**
  - A. `double hypotenuse(double, double);`
  - B. `int smallest(int, int, int);`
  - C. `void instructions();`
  - D. `double intToDouble(int);`
- 6. **6.6** `static double lastVal;`
- 7. **6.7**
  - A. *Error:* Function `h` is defined in function `g`.

    *Correction:* Move the definition of `h` out of the definition of `g`.
  - B. *Error:* The function is supposed to return an integer, but does not.

    *Correction:* Place a `return result;` statement at the end of the function’s body or delete variable `result` and place the following statement in the function:

```cpp
return x + y;
```

  - C. *Error:* The result of `n + sum(n - 1)` is not returned; `sum` returns an improper result.

    *Correction:* Rewrite the statement in the `else` clause as

```cpp
return n + sum(n - 1);
```

  - D. *Errors:* Semicolon after the right parenthesis that encloses the parameter list, and redefining the parameter `a` in the function definition.

    *Corrections:* Delete the semicolon after the right parenthesis of the parameter list, and delete the declaration `float a;`.
  - E. *Error:* The function returns a value when it isn’t supposed to.

    *Correction:* Eliminate the `return` statement or change the return type.
- 8. **6.8** This creates a reference parameter of type “reference to `double`” that enables the function to modify the original variable in the calling function.
- 9. **6.9** **False.** C++ enables pass-by-reference using reference parameters (and pointers, as we discuss in **Chapter 8**).
- 10. **6.10** See the following program:

```cpp
// Exercise 6.10 Solution: ex06_10.cpp
// Inline function that calculates the volume of a sphere
#include <iostream>
#include <cmath>
using namespace std;

const double PI{3.14159}; // define global constant PI

// calculates volume of a sphere
inline double sphereVolume(const double radius) {
    return 4.0 / 3.0 * PI * pow(radius, 3);
}

int main() {
    // prompt user for radius
    cout << "Enter the length of the radius of your sphere: ";
    double radiusValue;
    cin >> radiusValue; // input radius
}
```
