another iteration is performed. This continues until the value of number becomes 11. When the condition is tested, the value is false because 11 is not less than or equal to 10, it is greater, so control falls to the statement after the closing curly brace.

This next example also doesn’t do anything very important but it again demonstrates the common components of while loops. We want to write a program that sums the integers 1 through 10. Our loop-control variable will again be named number. It is initialized to the value 1 and is incremented by 1 each iteration. We also need to initialize a second variable (sum) outside of the loop to hold the sum of the numbers as we work through them.

Here is the program:

```
```cpp
// WhileLoop.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
    int number, sum;
    number = 1;
    sum = 0;
    while (number <= 10)
    {
        sum += number;
        ++number;
    }
    cout << "The sum of 1 - 10 is " << sum << endl;
    Console::ReadKey();
    return 0;
}
```
```