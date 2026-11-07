maximum’s one type parameter T (line 3) is a placeholder for the type of data the function processes. Type parameter names in a template parameter list must be unique. When the compiler encounters a call to maximum, it substitutes the argument types in the call for T throughout the template definition, creating a complete function template specialization that determines the maximum of three values of the specified type. The values must have the same type because we use only one type parameter. We’ll use C++ standard library templates that require multiple type parameters in Chapter 13.

# Using Function Template maximum

Figure 5.13 uses the maximum function template to determine the largest of three int values, three double values and three char values, respectively (lines 15, 24 and 33). Each call uses arguments of a different type, so “behind the scenes,” the compiler creates a separate function definition for each—one expecting three int values, one expecting three double values and one expecting three char values, respectively.

```
```cpp
// fig05_13.cpp
// Function template maximum test program.
#include <iostream>
#include "maximum.h" // include definition of function template maximum
using namespace std;

int main() {
   // demonstrate maximum with int values
   cout << "Input three integer values: ";
   int int1, int2, int3;
   cin >> int1 >> int2 >> int3;

   // invoke int version of maximum
   cout << "The maximum integer value is: "
        << maximum(int1, int2, int3);

   // demonstrate maximum with double values
   cout << "\nInput three double values: ";
   double double1, double2, double3;
   cin >> double1 >> double2 >> double3;

   // invoke double version of maximum
   cout << "The maximum double value is: "
        << maximum(double1, double2, double3);

   // demonstrate maximum with char values
   cout << "\nInput three characters: ";
   char char1, char2, char3;
   cin >> char1 >> char2 >> char3;

   // invoke char version of maximum
   cout << "The maximum character value is: "
        << maximum(char1, char2, char3) << '\n';
}
```
```

**Fig. 5.13** | Function template maximum test program. (Part 1 of 2.)