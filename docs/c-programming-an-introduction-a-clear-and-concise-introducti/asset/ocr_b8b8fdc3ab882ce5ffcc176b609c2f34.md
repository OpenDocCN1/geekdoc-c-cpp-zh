is no more input and the program can continue with its processing.

Here's an example. We want a program that averages a set of test scores but we don't know how many test scores will be entered. In this type of program, a numerical value will have to do as the sentinel since the program will be reading numbers from the keyboard. For test scores, a good sentinel value is -1, since the lowest test score possible is a 0 (unless it's a really, really hard test).

A program that solves this problem follows:

```
```cpp
// AverageGrade.cpp : main project file.

#include "stdafx.h"

using namespace System;
#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
    int testScore, total, count;
    double average;
    total = 0;
    count = 0;
    cout << "Enter a test score (-1 to quit): ";
    cin >> testScore;
    while (testScore != -1)
    {
        total += testScore;
        ++count;
        cout << "Enter a test score (-1 to quit): ";
        cin >> testScore;
    }
    average = total / count;
    cout << endl << "The average test score is: "
         << average << endl;
    Console::ReadKey();
    return 0;
}
```
```