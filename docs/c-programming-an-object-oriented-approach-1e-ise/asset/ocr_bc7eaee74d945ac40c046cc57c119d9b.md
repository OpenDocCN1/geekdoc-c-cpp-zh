# EXAMPLE 10.25

Program 10.27 changes a binary string to a decimal integer. In this case, base is 2. We have used the *popFront* function we developed before (included in the header file). We have written a small function named *findValue* to change the extracted character to its integer value.

# **Program 10.27**  Changing a binary string to a decimal integer

```
```cpp
/**************************************************************
 * A program to change a binary string to a decimal integer.   *
 **************************************************************/
#include "customized.h"
#include <string>
#include <iostream>
using namespace std;
/**************************************************************
 * A function to change a numeric character to its equivalent  *
 * integer value.                                             *
 **************************************************************/
int findValue (char ch)
{
    return static_cast<int>(ch) - 48;
}

int main ()
{
    // Declaration, inputting, and validation of binary string
    string binary;
    do
    {
        cout << "Enter binary string: ";
        getline (cin, binary);
    } while (binary.find_first_not_of ("01") < binary.size());
    // Initialization and calculation of decimal integer
    int base = 2;
    int decimal = 0;
    while (!binary.empty())
    {
        decimal *= base;
        char ch = popFront (binary);
        decimal += findValue (ch);
    }
    cout << "Decimal value: " << decimal;
    return 0;
}
```
```