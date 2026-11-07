```
```cpp
while (temp != 0)
{
    digit = temp - (temp / 10) * 10;
    temp = temp / 10;

    if (digit % 2 == 0)
    {
        evensCount++;
        if (digit == 0)
            zerosCount++;
    }
    else
        oddsCount++;
}
}

int integerManipulation::getEvenCount()
{
    return evensCount;
}

int integerManipulation::getOddsCount()
{
    return oddsCount;
}

int integerManipulation::getZerosCount()
{
    return zerosCount;
}

int integerManipulation::sumDigits()
{
    cout << "See Programming Exercise 1 in Chapter 5." << endl;

    return 0;
}

integerManipulation::integerManipulation(long long n)
{
    num = n;
    revNum = 0;
    evensCount = 0;
    oddsCount = 0;
    zerosCount = 0;
}
```
```

The following program shows how to use this class in a program.

```
```cpp
//The user program that uses the class integerManipulation

#include <iostream>                         //Line 1
#include "integerManipulation.h"            //Line 2
```
```