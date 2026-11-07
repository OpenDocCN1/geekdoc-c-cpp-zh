```
```cpp
cin >> rate;
while (balance < 10000)
{
    balance *= rate;
    ++years;
}
cout << "It will take " << years
     << " to reach $10,000.00." << endl;
Console::ReadKey();
return 0;
}
```
```

Here is the program rewritten with a do-while loop:

```
```cpp
// DoWhile.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <cstdlib>
#include <ctime>
using namespace std;

int main(array<System::String ^> ^args)
{
    double balance, rate;
    int years = 0;
    balance = 5000;
    // Enter 1.02 for 2%
    cout << "What is the interest rate? ";
    cin >> rate;
    do
    {
        balance *= rate;
        ++years;
    } while (balance < 10000);
```
```