```
// Fig. 21.8: Fig21_08.cpp
// Demonstrating class string insert member functions.
#include <iostream>
#include <string>
using namespace std;

int main() {
   string string1{"beginning end"};
   string string2{"middle"};
   string string3{"12345678"};
   string string4{"xx"};

   cout << "Initial strings:\nstring1: " << string1
      << "\nstring2: " << string2 << "\nstring3: " << string3
      << "\nstring4: " << string4 << "\n\n";

   // insert "middle" at location 10 in string1
   string1.insert(10, string2);

   // insert "xx" at location 3 in string3
   string3.insert(3, string4, 0, string::npos);

   cout << "Strings after insert:\nstring1: " << string1
      << "\nstring2: " << string2 << "\nstring3: " << string3
      << "\nstring4: " << string4 << endl;
}
```

```
Initial strings:
string1: beginning end
string2: middle
string3: 12345678
string4: xx

Strings after insert:
string1: beginning middle end
string2: middle
string3: 123xx45678
string4: xx
```

# Fig. 21.8 Demonstrating class `string` `insert` member functions.

The program declares, initializes then outputs `string` s `string1`, `string2`, `string3` and `string4`. Line 18 uses `string` member function `insert` to insert `string2`’s content before element 10 of `string1`.