# D.2. THE FLOATING-POINT TYPES

The first subtraction yields the correct answer. We now know that floating-point numbers (like .5) have exact internal representations while others are only approximations. The exact answer for the second subtraction should be 0.58, and if we round the reported result to 2 decimal places, the answer matches. Floating-point arithmetic often produces results that are close approximations of the true answer. What are the ramifications of this inexactness of floating-point numbers? Section 9.4.6 shows how the misuse of floating-point values can lead to logic errors in programs.

In C++ source code, literal numbers that contain decimal places are by default double. A float literals have an f or F suffix.

![](bbox=[0.181, 0.279, 0.868, 0.353])

In C++ we may assign a double literal to a float variable. The compiler automatically narrows the double to a float as Listing D.2 (assignfloat.cpp) shows:

# Listing D.2: assignfloat.cpp

```
#include <iostream>

using namespace std;

int main() {
    float number;
    number = 10.0; // OK, double literal assignable to a float
    cout << "number = " << number << endl;
}
```

The statement

number = 10.0;

assigns a double literal (10.0) to a float variable. You may instead explicitly use a float literal as:

number = 10.0f;