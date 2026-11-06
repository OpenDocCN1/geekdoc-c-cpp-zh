```
```cpp
// Fig. 17.9: fig17_09.cpp
// Demonstrating unique_ptr.
#include <iostream>
#include <memory>
using namespace std;

#include "Integer.h"

// use unique_ptr to manipulate Integer object
int main() {
   cout << "Creating a unique_ptr object that points to an Integer\n";

   // "aim" unique_ptr at Integer object
   unique_ptr<Integer> ptrToInteger{make_unique<Integer>(7)};

   cout << "\nUsing the unique_ptr to set the Integer\n";
   ptrToInteger->setInteger(99); // use unique_ptr to set Integer value

   // use unique_ptr to get Integer value
   cout << "Integer after setInteger: " << (*ptrToInteger).getInteger()
      << "\n\nTerminating program" << endl;
}
```
```

```
```text
Creating a unique_ptr object that points to an Integer
Constructor for Integer 7

Using the unique_ptr to set the Integer
Integer after setInteger: 99

Terminating program
Destructor for Integer 99
```
```

# **Fig. 17.9** `unique_ptr` object manages dynamically allocated memory.

Line 17 uses the `unique_ptr` overloaded `->` operator to invoke function `setInteger` on the `Integer` object that `ptrToInteger` manages. Line 20 uses the `unique_ptr` overloaded `*` operator to dereference `ptrToInteger`, then uses the dot (`.`) operator to invoke function `getInteger` on the `Integer` object. Like a regular pointer, a