# Chapter 10

You can define the preprocessor symbols control whether or not the debug code is executed in the DebugStuff.h header:

```
// DebugStuff.h - Debugging control
#pragma once

#ifdef _DEBUG

#define CONSTRUCTOR_TRACE      // Output constructor call trace
#define FUNCTION_TRACE         // Trace function calls

#endif
```

Your control symbols are defined only if _DEBUG is defined, so none of the debug code is included in a release version of the program.

You can now try out the Name class with the following main() function:

```
// Ex10_01.cpp : Including debug code in a program

#include <iostream>
using namespace std;
#include "Name.h"

int main(int argc, char* argv[])
{
    Name myName("Ivor", "Horton");                 // Try a single object

    // Retrieve and store the name in a local char array
    char theName[10];
    cout << "\nThe name is " << myName.getName(theName);

    // Store the name in an array in the free store
    char* pName = new char[myName.getNameLength()+1];
    cout << "\nThe name is " << myName.getName(pName);

    cout << endl;
    return 0;
}
```

Now that all the code has been entered, double-checked, and is completely correct, all you have to do is run it to make sure. Hardly seems necessary.

# How It Works

Well it doesn’t-it doesn’t even compile, does it? The major problem is the Name constructor. The parameters are const, as they should be, but the data members are not. You could declare the data members as const, but anyway, you should be copying the name strings, not just copying the pointers. Amend the constructor definition to:

```
// Constructor
Name::Name(const char* pFirst, const char* pSecond)
```