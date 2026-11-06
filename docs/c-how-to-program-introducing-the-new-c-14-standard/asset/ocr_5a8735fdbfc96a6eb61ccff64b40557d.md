**Figure 6.20** uses overloaded `square` functions to calculate the square of an `int` (lines 7–10) and the square of a `double` (lines 13–16). Line 19 invokes the `int` version of function `square` by passing the literal value `7`. C++ treats whole-number literal values as type `int`. Similarly, line 21 invokes the `double` version of function `square` by passing the literal value `7.5`, which C++ treats as a `double`. In each case the compiler chooses the proper function to call, based on the type of the argument. The last two lines of the output window confirm that the proper function was called in each case.

```
```cpp
// Fig. 6.20: fig06_20.cpp
// Overloaded square functions.
#include <iostream>
using namespace std;

// function square for int values
int square(int x) {
   cout << "square of integer " << x << " is ";
   return x * x;
}

// function square for double values
double square(double y) {
   cout << "square of double " << y << " is ";
   return y * y;
}

int main() {
   cout << square(7);   // calls int version
   cout << endl;
   cout << square(7.5); // calls double version
   cout << endl;
}
```
```

```
```text
square of integer 7 is 49
square of double 7.5 is 56.25
```
```

# Fig. 6.20 Overloaded `square` functions