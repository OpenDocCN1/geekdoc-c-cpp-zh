# Algorithm for sroot

+   1. If argc is less than 2, display an “incorrect usage” error message and quit.

+   2. For each integer i in the range 1 through argc − 1:

+   a. Get inValue, the double equivalent to argument i.

+   b. If inValue > 0
+   Display inValue and its square root.
+   Else
+   Display an “invalid data” error message.

Encoding this algorithm in C++ is straightforward, as shown in Example 15.4.

# Example 15.4 Encoding sroot

```
/* Program to display the square roots of a sequence of values,
   specified by the user on the command line.

   Receive: One or more numeric (double) values
   Output: The square roots of the input values
   ------------------------------------------------------------ */

#include <iostream>               // cin, cout, <<, >>
#include <cmath>                  // sqrt()
#include <cstdlib>                // strtod()
using namespace std;

int main(int argc, char * argv[])
{
    if (argc < 2)
    {
        cout << "\n*** Usage: sroot List-of-Positive-Numbers \n\n";
        exit(1);
    }

    double inValue;               // double equivalent of an argument

    for (int i = 1; i < argc; i++)
    {
        inValue = strtod(argv[i], 0);
        cout <<"\n--> The square root of " << inValue
             << " is" << sqrt(inValue) << endl;
    }
}
```

# SAMPLE RUN:

./sqr t 1 2 3 4 5 6
--> The square root of 1 is 1