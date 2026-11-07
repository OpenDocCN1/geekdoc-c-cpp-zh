# # Appendix A

# ## Errors and Error Messages

It is inevitable that you will have errors in your programs. It is especially true that beginning C++ programmers will have many errors in their programs, but it is equally true that expert C++ programmers experience errors in their code every day. Programming is just too complex for a programmer to not expect to have to deal with errors. In this appendix we discuss a few of the common errors you will come up against as you start learning C++. More importantly, we discuss how to interpret the error messages you will receive when the compiler finds errors in your code.

# ### Syntax Errors

The most common errors you will make as you first start learning C++ programming are *syntax errors*. A syntax error means that you didn't form a C++ statement correctly. An example of a common syntax error is leaving a semicolon off the end of a statement. Here is a C++ program with a semicolon left off one of the statements:

```
```cpp
// ErrorHandling.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
    cout << "Hello, World!" << endl
    Console::ReadKey();
}
```
```