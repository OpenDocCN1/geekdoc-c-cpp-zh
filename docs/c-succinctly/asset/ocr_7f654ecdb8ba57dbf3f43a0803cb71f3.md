# Functions

There are two types of functions in C++: stand-alone functions and member functions. The main difference between them is that a member function belongs to a class, structure, or union, whereas a stand-alone function does not.

Stand-alone functions are the most basic types of functions. They can be declared in namespaces, they can be overloaded, and they can be inline. Let's look at a few.

**Sample: FunctionsSample\\Utility.h**

```
```cpp
#pragma once

namespace Utility
{
        inline bool IsEven(int value)
        {
                return (value % 2) == 0;
        }

        inline bool IsEven(long long value)
        {
                return (value % 2) == 0;
        }

        void PrintIsEvenResult(int value);
        void PrintIsEvenResult(long long value);

        void PrintBool(bool value);
}
```
```

**Sample: FunctionsSample\\Utility.cpp**

```
```cpp
#include "Utility.h"
#include <iostream>
#include <ostream>

using namespace std;
using namespace Utility;

void Utility::PrintIsEvenResult(int value)
{
        wcout << L"The number " << value << L" is "
                << (IsEven(value) ? L"" : L"not ") << L"even."
                << endl;
}

void Utility::PrintIsEvenResult(long long value)
{
        wcout << L"The number " << value << L" is "
                << (IsEven(value) ? L"" : L"not ") << L"even."
                << endl;
}

void Utility::PrintBool(bool value)
{
```
```