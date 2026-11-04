initialized with the location of the variable str. The counts array has four integer values, all of which are initially 0.

The next portion of Listing 5.15 is a loop that uses the pointer ptr to iterate through each character of the variable str. During each iteration, the current character is passed to the charType() function, and the return value is used to increment the corresponding position in the counts array. The position of ptr is incremented by one and the while() executes again, until we reach the end of the hard-coded string.

The output from Listing 5.15 is here:

First Loop
VOWELS: 33
CONSONANT: 66
DIGITS: 4
OTHERS: 25

# FINDING A WORD IN A TEXT STRING IN C

The strchr() function locates the first occurrence of a character in a text string. Listing 5.16 displays the contents of FindChar1.c that illustrates how to find a character in a text string.

# LISTING 5.16: FindChar1.c

```
```c
#include <stdio.h>
#include <string.h>

#define SIZE 80

int main(void)
{
    char line[SIZE] = "New York Pizza";
```
```