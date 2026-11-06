
```cpp
int a = 5;

cout << (double) a << endl;        //outputs: 5.0
cout << (double) 34 << endl;       //outputs: 34.0
cout << (double)-34 << endl;       //outputs: -34.0
cout << a / 2 << endl;             //outputs: 2
cout << (double) a / 2 << endl;    //outputs: 2.5
return 0;
}
```

> **Notice:** In computer science, type casting is a way of converting a variable of one data type into another. Please note that `(double)` is not a function. It is just a way in C++ to turn an integer into a real.

> **Notice:** In C++, the result of the division of two integers is always an integer. Thus, in the expression `a / 2`, since variable `a` and number `2` are integers, the result is always an integer. As shown in the last statement, if you wish a result of type real you need to add the `(double)` casting operator in front of at least one of the operands of the division.

Moreover, the statement

```cpp
cout << (double) a / 2 << endl;
```

is equivalent to

```cpp
cout << a / (double) 2 << endl;
```

and to

```cpp
cout << (double) a / (double) 2 << endl;
```

and of course to

```cpp
cout << a / 2.0 << endl;
```

They all output the value of 2.5.

## Pi

```cpp
M_PI
```

This returns the value of π. It is defined in the cmath library.

### Example

```cpp
project_11_2e

#include <iostream>
#include <cmath>
using namespace std;
int main(){
  cout << M_PI << endl;    //outputs: 3.14159
  cout.precision(20);      //Set the maximum number of digits to display
  cout << M_PI << endl;    //outputs: 3.141592653589793116
  return 0;
}
```

> **Notice:** Please note that `M_PI` is a constant, not a function. This is why no parentheses are used.
> 
> **Notice:** The statement `cout.precision(20)` sets the maximum number of digits that the statement `cout` displays.

## Power

```cpp
pow( number, exp )
```

This returns the result of `number` raised to the power of `exp`. It is defined in the `cmath` library.

### Example

```cpp
#include <iostream>
#include <cmath>
using namespace std;
int main() {
  double a, b, c;

  a = 2;
  b = 3;
  cout << pow(a, b) << endl;      //outputs: 8.0

  c = pow(3, 2);
  cout << c << endl;              //outputs: 9.0
  return 0;
}
```

> **Notice:** Function `pow()` can be used to calculate the square root of a number as well. It is known from mathematics that `√x = x^(1/2)`. So, you can write `y = pow(x, 1/2)` to calculate the square root of `x`, or you can even write `y = pow(x, 1/3)` to calculate the cube root of `x`, and so on!

## Random

```cpp
rand()
```

This returns a pseudo-random integer in the range between 0 and RAND_MAX, where RAND_MAX is a constant of a value of at least 32767. Function `rand()` is defined in the `cstdlib` library.

### Example

```cpp
#include <iostream>
#include <cstdlib>
using namespace std;
```

```cpp
cout << sqrt(2) << endl;       //outputs: 1.41421
cout.precision(15);
cout << sqrt(2) << endl;       //outputs: 1.4142135623731
return 0;
}
```

> **Remember!** The statement `cout.precision(15)` sets the **maximum number of digits** that the statement `cout` displays.

## Tangent

```cpp
tan(number)
```

This returns the tangent of *number*. The value of *number* must be expressed in radians. Function `tan()` is defined in the `cmath` library.

### Example

```cpp
// project_11_2m
#include <iostream>
#include <cmath>
using namespace std;
int main() {
  double a;

  a = tan(10);
  cout << a << endl;       //outputs: 0.648361
  return 0;
}
```

## Exercise 11.2-1 *Calculating the Distance Between Two Points*

Write a C++ program that prompts the user to enter the coordinates *(x, y)* of two points and then calculates the straight line distance between them. The required formula is

\[d = \sqrt{(x_1 - x_2)^2 + (y_1 - y_2)^2}\]

### Solution

In this exercise, you need to use two functions: the `pow()` function, which returns the result of a number raised to a power; and the `sqrt()` function, which returns the square root of a number.

To simplify things, the terms \((x_1 - x_2)^2\) and \((y_1 - y_2)^2\) are calculated individually and the results are assigned to two temporary variables.

The C++ program is shown here.

```cpp
// project_11_2_1a
#include <iostream>
#include <cmath>
using namespace std;

int main() {
    double d, x1, x2, x_temp, y1, y2, y_temp;

    cout << "Enter coordinates for point A: ";
    cin >> x1;
    cin >> y1;

    cout << "Enter coordinates for point B: ";
    cin >> x2;
    cin >> y2;

    x_temp = pow(x1 - x2, 2);
    y_temp = pow(y1 - y2, 2);

    d = sqrt(x_temp + y_temp);

    cout << "Distance between points: " << d;
    return 0;
}
```

Now let’s see another approach. You should realize that it is actually possible to nest one function within another. Doing that, the result of the nested function is used as an argument for the outer function. This is a writing style that most programmers prefer to follow because it can save a lot of code lines. Of course, if you nest too many functions, no one will be able to understand your code. A nesting of up to four levels is quite acceptable. The C++ program that uses nested functions is shown here.

### project_11_2_1b

```cpp
#include <iostream>
#include <cmath>
using namespace std;
int main() {
    double d, x1, x2, y1, y2;

    cout << "Enter coordinates for point A: ";
    cin >> x1;
    cin >> y1;

    cout << "Enter coordinates for point B: ";
    cin >> x2;
    cin >> y2;

    d = sqrt(pow(x1 - x2, 2) + pow(y1 - y2, 2));

    cout << "Distance between points: " << d;
    return 0;
}
```

## **Exercise 11.2-2** *How Far Did the Car Travel?*

*A car starts from rest and moves with a constant acceleration along a straight horizontal road for a given distance. Write a C++ program that prompts the user to enter the acceleration and the distance the car traveled and then calculates the time traveled. The required formula is*

$S = u_0 + \frac{1}{2}at^2$

where

- **S** is the distance the car traveled, in meters (m)
- **u₀** is the initial velocity (speed) of the car, in meters per second (m/sec)
- **t** is the time the car traveled, in seconds (sec)
- **a** is the acceleration, in meters per second² (m/sec²)

### **Solution**

Since the car starts from rest, the initial velocity (speed) u₀ is zero. Thus, the formula becomes

$S = \frac{1}{2}at^2$

Now, if you solve for time, the final formula becomes

$t = \sqrt{\frac{2S}{a}}$

In C++, you can use the sqrt() function, which returns the square root of a number.

```cpp
// project_11_2_2
#include <iostream>
#include <cmath>
using namespace std;
int main() {
    double S, a, t;

    cout << "Enter acceleration: ";
    cin >> a;
    cout << "Enter distance traveled: ";
    cin >> S;

    t = sqrt(2 * S / a);

    cout << "Your car traveled for " << t << " seconds";
    return 0;
}
```

## 11.3 Review Questions: True/False

Choose **true** or **false** for each of the following statements.

- 1. In general, functions are small subprograms that solve small problems.
- 2. Every program must use Heron’s iterative formula to calculate the square root of a positive number.
- 3. The `abs()` function returns the absolute position of an item.
- 4. The statement `int(3.59)` returns a result of 3.6.
- 5. The `M_PI` constant is equal to 3.14.
- 6. The statement `pow(2, 3)` returns a result of 9.
- 7. The `rand()` function can also return negative random numbers.
- 8. There is a 50% possibility that the statement `y = rand() % 2` will assign a value of 1 to variable `y`.
- 9. The statement `round(3.59)` returns a result of 4.
- 10. To calculate the sinus of 90 degrees, you have to write `y = sin (M_PI / 2)`.
- 11. The statement `y = sqrt(-2)` is valid.
- 12. The following code fragment satisfies the property of definiteness.

    ```cpp
    double a, b, x;

    cin >> a;
    cin >> b;
    x = a * sqrt(b);
    cout << x << endl;
    ```

## 11.4 Review Questions: Multiple Choice

Select the correct answer for each of the following statements.

- 1. Which of the following calculates the result of the variable `a` raised to the power of 2?
  - a. `y = a * a;`
  - b. `y = pow(a, 2);`
  - c. `y = a * a / a * a;`
  - d. all of the above
- 2. What is the value of the variable `y` when the statement `y = abs(+5.2)` is executed?
  - a. -5.2
  - b. -5
  - c. 0.2
  - d. 5.2
  - e. 5
