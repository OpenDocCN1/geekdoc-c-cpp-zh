Switch
ONE
Switch
TWO

If you “comment out” the code snippet for srand() in Listing 3.23, the new output will be something like this:

Switch
TWO
Switch
TWO
Switch
TWO

Alternatively you could place the switch() statement inside a while loop, with the appropriate exit condition, in order to generate multiple output values (instead of launching the code multiple times).

# WORKING WITH ARRAYS OF NUMBERS

Listing 3.20 displays the contents of Factorial2.c that illustrates how to calculate the factorial value of a positive integer using an iterative solution.

# LISTING 3.20: Factorial2.c

```
#include <stdio.h>

int main()
{
    int result=1, num=5;

    for(int i=1; i<=num; i++)
    {
        result *= i;
    }
```