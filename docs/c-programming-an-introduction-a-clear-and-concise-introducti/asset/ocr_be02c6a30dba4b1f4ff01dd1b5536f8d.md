```
~~~cpp
// minMax.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <cstdlib>
#include <ctime>
using namespace std;

int main(array<System::String ^> ^args)
{
    int min, max;
    const int size = 100;
    int numbers[size];

    srand(time(NULL));
    // initialize the array
    for(int i = 0; i < size; ++i) {
        numbers[i] = rand() % 100 + 1;
    }
    min = numbers[0];
    max = numbers[0];
    // search for min and max
    for(int i = 0; i < (size-1); ++i) {
        if (numbers[i+1] < min)
            min = numbers[i+1];
        if (numbers[i+1] > max)
            max = numbers[i+1];
    }
    cout << "The minimum value in the array is "
         << min << endl
         << "The maximum value in the array is "
         << max << endl;
    // display the values
    for(int i = 0; i < size; ++i) {
        cout << numbers[i] << " ";
    }
    Console::ReadKey();
    return 0;
}
~~~
```