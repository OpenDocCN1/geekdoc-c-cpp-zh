```
```cpp
int changeNumber(int number)
{
    return number *= 3;
}

int main()
{
    int number = 3;
    cout << changeNumber(number);
    cout << number;
    return 0;
}
```
```

The parameter number is said to be local to the function changeNumber(). What this means is that this variable is accessible only to code within the function definition, and once the function stops executing, its value is completely removed from memory.

To demonstrate how this works, let's rewrite the program above to demonstrate how local scope works. The complete program is listed below:

```
```cpp
// ScopeExample.cpp : main project file.

#include "stdafx.h"

using namespace System;
#include <iostream>
using namespace std;

int changeNumber(int number)
{
    number *= 3;
    cout << "The value of number in the changeNumber()"
    cout << " function is: " << number << endl;
```
```