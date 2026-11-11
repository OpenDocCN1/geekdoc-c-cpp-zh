# CHAPTER 2:

# Basic Facilities

# Array

The Array is a data structure that holds a sequential collection of elements of the same data type.

For example, in the code below I declared two arrays of different data type: an array of characters and an array of integers.

```
```cpp
#include "stdafx.h"

#include <iostream>

int main(int argc, char* argv[])

{

        int i;

        int length;

        int sum = 0;

        char char_array[10] = { 'p', 's', 'y', 'c', 'h', 'o', 'l', 'o', 'g', 'y' };

    // total number of bytes allocated for that array

    //one char is one byte: the number of elements = number of bytes

        length = sizeof(char_array) ;

        std::cout << "Size of array of characters is " << length << std::endl;

        for (i = 0; i<length; i++)
```
```