```
```cpp
{
    cout << "Hello, World!" << endl;
    Console::ReadKey();
    return 0;
}
```
```

The error message you get when compiling this program is:

```
```text
1>----- Build started: Project: ErrorHandling, Configuration: Debug
Win32------
1> ErrorHandling.cpp
1>ErrorHandling.cpp(8): error C2065: 'cout' : undeclared identifier
1>ErrorHandling.cpp(8): error C2065: 'endl' : undeclared identifier
=========== Build: 0 succeeded, 1 failed, 0 up-to-date, 0 skipped
===========
```
```

This error message is a little less useful than the previous one, since it doesn't tell you what you did, it just lets you know that it doesn't recognize cout and endl. Anytime you see this error message, though, and the identifiers mentioned in the error message are system objects, such as cout and endl, then you can be sure you forgot to include the library that contains those objects.

A similar error message occurs when you try to use a variable in a program that hasn't been declared:

```
```cpp
// ErrorHandling.cpp : main project file.

#include "stdafx.h"
using namespace System;
#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
    int number1, number2;
    number1 = 12;
    number2 = 23;
```
```