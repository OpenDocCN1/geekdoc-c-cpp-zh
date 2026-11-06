to the many other recursion examples and exercises throughout the text.

+   31. 6.41 **(Recursive Greatest Common Divisor)** The greatest common divisor of integers `x` and `y` is the largest integer that evenly divides both `x` and `y`. Write a recursive function `gcd` that returns the greatest common divisor of `x` and `y`, defined recursively as follows: If `y` is equal to `0`, then `gcd(x, y)` is `x`; otherwise, `gcd(x, y)` is `gcd(y, x % y)`, where `%` is the remainder operator. *[Note: For this algorithm, `x` must be larger than `y`].*

+   32. 6.42 **(Distance Between Points)** Write function `distance` that calculates the distance between two points `(x1, y1)` and `(x2, y2)`. All numbers and return values should be of type `double`.

+   33. 6.43 What does the following program do?

```
```cpp
// Exercise 6.44: ex6_44.cpp
// What does this program do?
#include <iostream>
using namespace std;

int mystery(int, int); // function prototype

int main() {
    cout << "Enter two integers: ";
    int x(0);
    int y(0);
```
```