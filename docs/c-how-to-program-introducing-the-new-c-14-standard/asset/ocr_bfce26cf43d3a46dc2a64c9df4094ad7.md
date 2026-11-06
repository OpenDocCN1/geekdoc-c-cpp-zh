```
```cpp
// Fig. 22.33: fig22_33.cpp
// Using strtoul.
#include <iostream>
#include <cstdlib> // strtoul prototype
using namespace std;

int main() {
   const char* string1{"1234567abc"};
   char* remainderPtr{nullptr};

   // convert a sequence of characters to unsigned long
   unsigned long x{strtoul(string1, &remainderPtr, 0)};

   cout << "The original string is \"" << string1
      << "\nThe converted value is " << x
      << "\nThe remainder of the original string is \"" << remainderPtr
      << "\"\nThe converted value minus 567 is " << x - 567 << endl;
}
```
```

```
```
The original string is "1234567abc"
The converted value is 1234567
The remainder of the original string is "abc"
The converted value minus 567 is 1234000
```
```

# Fig. 22.33 String-conversion function `strtoul`.