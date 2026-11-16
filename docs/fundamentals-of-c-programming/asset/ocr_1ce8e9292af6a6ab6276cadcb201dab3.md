```
std::cin >> input;
// Report square root
std::cout << "Square root of " << input << " = "
<< square_root(input) << '\n';
}
```

Is Listing 9.24 (squarerootfunction.cpp) better than Listing 8.2 (standardsquareroot.cpp) which uses the standard sqrt function from the cmath library? Generally speaking, if you have the choice of using a standard library function or writing your own custom function that provides the same functionality, choose to use the standard library routine. The advantages of using the standard library routine include:

+   - Your effort to produce the custom code is eliminated entirely; you can devote more effort to other parts of the application’s development.
+   - If you write your own custom code, you must thoroughly test it to ensure its correctness; standard library code, while not immune to bugs, generally has been subjected to a complete test suite. Library code is used by many developers, and thus any lurking errors are usually exposed early; your code is exercised only by the programs you write, and errors may not become apparent immediately. If your programs are not used by a wide audience, bugs may lie dormant for a long time. Standard library routines are well known and trusted; custom code, due to its limited exposure, is suspect until it gains wider exposure and adoption.
+   - Standard routines are typically tuned to be very efficient; it takes a great deal of effort to make custom code efficient.
+   - Standard routines are well-documented; extra work is required to document custom code, and writing good documentation is hard work.

Listing 9.25 (squarerootcomparison.cpp) tests our custom square root function over a range of 1,000,000,000 floating-point values.

```
Listing 9.25: squarerootcomparison.cpp
#include <iostream>
#include <cmath>
// Consider two floating-point numbers equal when
// the difference between them is very small.
bool equals(double a, double b, double tolerance) {
return a == b || fabs(a - b) < tolerance;
}
double square_root(double x) {
// Compute a provisional square root
double root = 1.0;
do { // Loop until the provisional root
// is close enough to the actual root
root = (root + x/root) / 2.0;
} while (!equals(root*root, x, 0.0001));
return root;
}
```