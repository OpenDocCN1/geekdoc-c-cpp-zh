```
temp[i]=aWord[length-(i+1)];
```

When i =0, temp[i] will refer to the first character of the temp string.

At the same time (when i =0) the aWord [length-(i+1)] will refer to the aWord[13 − (0 + 1)] character and it will be aWord[12] that is the last character of the ‘Concatenation’ string.

When i=1, the temp [1] will refer to the second character of the temp string and aWord [13-(1+1)] will refer to the second from the end character of the ‘Concatenation’ string.

That way, we can copy all characters in reversed order.

When we have copied all the characters from the original string to the temp string, we need to add null to the end of the temp string, because a string in C++ must be terminated with null.

The line of code temp[length]='\0'; will do the job.

The whole code is included in [visual_studio_2017.zip](visual_studio_2017.zip).

```
```cpp
#include "stdafx.h" #include <stdio.h>

#include <cctype>

#include <cstring>

#include <iostream>

int main()
{
    char more = 'Y';

    char prompt1[] = "\nEnter a word not more than 20 characters and press enter.\n";

    char prompt3[] = "\nDo you want to continue? Y/N\n";

    char aWord[20];

    char aCopy[40];
```
```