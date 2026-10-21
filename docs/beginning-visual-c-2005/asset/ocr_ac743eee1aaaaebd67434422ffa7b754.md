The compiler is able to deduce the type argument in all instances where the generic functions are used but you could specify the explicitly if you wanted to. For example, you could write the previous statement like this:

```
ListElements(RemoveElement<String^>(MaxElement<String^>(strings), strings));
```

# A Calculator Program for the CLR

Let’s re-implement the calculator as a C++/CLI example. We’ll assume the same program structure and hierarchy of functions as you saw for the native C++ program but the functions will be declared and defined as C++/CLI functions. A good starting point is the set of function prototypes at the beginning of the source file(I have used Ex6_11 as the CLR project name:

```
// Ex6_11.cpp : main project file.
// A CLR calculator supporting parentheses

#include "stdafx.h"
#include <cstdlib>                              // For exit()

using namespace System;
String^ eatspaces(String^ str);                 // Function to eliminate blanks
double expr(String^ str);                      // Function evaluating an expression
double term(String^ str, int^ index);          // Function analyzing a term
double number(String^ str, int^ index);        // Function to recognize a number
String^ extract(String^ str, int^ index);       // Function to extract a substring
```

All the parameters are now handles; the string parameters are type String^ and the index parameter that records the current position in the string is also a handle of type int^. Of course, a string is returned as a handle of type String^.

The main() function implementation looks like this:

```
int main(array<System::String ^> ^args)
{
    String^ buffer;     // Input area for expression to be evaluated

    Console::WriteLine(L"Welcome to your friendly calculator.");
    Console::WriteLine(L"Enter an expression, or an empty line to quit.");

    for(;;)
    {
        buffer = eatspaces(Console::ReadLine());        // Read an input line

        if(String::IsNullOrEmpty(buffer))               // Empty line ends calculator
            return 0;

        Console::WriteLine(L"  = {0}\n\n",expr(buffer)); // Output value of expression
    }
    return 0;
}
```