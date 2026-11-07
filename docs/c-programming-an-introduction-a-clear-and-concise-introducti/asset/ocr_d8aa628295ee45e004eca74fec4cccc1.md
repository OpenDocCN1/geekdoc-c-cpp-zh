```
```cpp
int grade;
inFile >> grade;
```
```

Then you can do whatever you need to do with the data you just read into the variable. Since the data in the file is stored one grade per line, to get the next grade, just use the above statement again:

```
```cpp
inFile >> grade;
```
```

Each time you read a value from the grades.txt file, an internal pointer automatically moves to the next value so that when you issue another input statement, a new data value will be read into the variable. If the data had been stored on one line, instead of on separate lines, we would have had to put a space between each value so that the compiler would know where to place the pointer to read the next value.

You can continue on in this fashion, reading data from the file and storing it in a variable until you are out of data to read. Before the program ends, you should close the file to ensure the file doesn't become corrupted. We saw how to close a file earlier:

```
```cpp
inFile.close();
```
```

Here is a program that reads and displays the first two grades from the grades.txt file:

```
```cpp
// ReadFile.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <fstream>
using namespace std;

int main(array<System::String ^> ^args)
{
    ifstream inFile("c:\\data\\grades.txt");
    int grade;
    inFile >> grade;
```
```