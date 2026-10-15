# 24.- Exercises for the student

Add the numbers from 1 to 100 using an array and show the result on the screen.

```
/* add numbers from 1 to 100 */

#include <stdio.h>

int main (void)
{
    int i;
    int numbers [200];
    float sum;

    /* fill array data */
    for (i = 1; i <= 100; i = i + 1)
    {
        numbers [i] = i;
    }

    /* calculate the sum of all the numbers */
    sum = 0;
    for (i = 1; i <= 100; i = i + 1)
    {
        sum = sum + numbers [i];
    }

    printf ("\nThe sum of the numbers from 1 to 100 is:% f \n", sum);

    return 0;
}
```