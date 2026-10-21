# Chapter 10

You can now add a Name.cpp file to the project to hold the definitions for the member functions of Name. The constructor definitions are shown here:

```
// Name.cpp - Implementation of the Name class
#include "Name.h"                         // Name class definitions
#include "DebugStuff.h"                   // Debugging code control
#include <cstring>                         // For C-style string functions
#include <cassert>                         // For assertions
#include <iostream>
using namespace std;

// Default constructor
Name::Name()
{
#ifdef CONSTRUCTOR_TRACE
    // Trace constructor calls
    cerr << "\nDefault Name constructor called.";
#endif
    pFirstname = pSurname = "\0";
}

// Constructor
Name::Name(const char* pFirst, const char* pSecond):
                    pFirstname(pFirst), pSurname(pSecond)
{
    // Verify that arguments are not null
    assert(pFirst != 0);
    assert(pSecond != 0);

#ifdef CONSTRUCTOR_TRACE
    // Trace constructor calls
    cout << "\nName constructor called.";
#endif
}
```

Of course, you don’t particularly want to have Name objects that have null pointers as members, so the default constructor assigns empty strings for the names. You have used your own debug control symbol, CONSTRUCTOR_TRACE, to control output that traces constructor calls. Add the definition of this symbol to the DebugStuff.h header a little later. You could put anything at all as debug code here, such as displaying argument values, but it is usually best to keep it as simple as your debugging requirements allow; otherwise, your debug code may introduce further bugs. Here you just identify the constructor when it is called.

You have two assertions in the constructor to check for null pointers being passed as arguments. You could have combined these into one, but by using a separate assertion for each argument, you can identify which pointer is null (unless they both are, of course).

You might also want to check that the strings are not empty in an application by counting the characters prior to the terminating ‘\0’ for instance. However, you should not use an assertion to flag this. This sort of thing could arise as a result of user input, so ordinary program checking code should be added to deal with errors that may arise in the normal course of events. It is important to recognize the difference between bugs (errors in the code) and error conditions that can be expected to arise during normal operation of a program. The constructor should never be passed a null pointer, but a zero length name could