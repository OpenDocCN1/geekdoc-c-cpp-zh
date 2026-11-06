type parameter must be unique in the template parameter list for a particular template definition. When the compiler detects a maximum invocation in the program source code, the type of the data passed to maximum is substituted for T throughout the template definition, and C++ creates a complete function for determining the maximum of three values of the specified data type—all three must have the same type, since we use only one type parameter in this example—then the newly created function is compiled. Thus, templates are a means of code generation.

Figure 6.27 uses the maximum function template (lines 17, 27 and 37) to determine the largest of three int values, three double values and three char values, respectively. The functions are created as a result of the calls in lines 17, 27 and 37—expecting three int values, three double values and three char values, respectively. The function template specialization created for type int replaces each occurrence of T with int as follows:

```
int maximum( int value1, int value2, int value3 )
{
    int maximumValue = value1;  // assume value1 is maximum

    // determine whether value2 is greater than maximumValue
    if ( value2 > maximumValue )
        maximumValue = value2;

    // determine whether value3 is greater than maximumValue
    if ( value3 > maximumValue )
        maximumValue = value3;

    return maximumValue;
}  // end function template maximum
```

```
// Fig. 6.27: fig06_27.cpp
// Function template maximum test program.
#include <iostream>
#include "maximum.h"  // include definition of function template maximum
using namespace std;

int main()
{
    // demonstrate maximum with int values
    int int1, int2, int3;

    cout << "Input three integer values: ";
    cin >> int1 >> int2 >> int3;

    // invoke int version of maximum
    cout << "The maximum integer value is: "
         << maximum( int1, int2, int3 );

    // demonstrate maximum with double values
    double double1, double2, double3;

    cout << "\n\nInput three double values: ";
    cin >> double1 >> double2 >> double3;
```

Fig. 6.27 | Demonstrating function template maximum. (Part 1 of 2.)