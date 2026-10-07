# APPENDIX D Answers

```
printf("\n\nThe total is %d\n", total);

return 0;
}
```

12. The code is as follows:

+   * Inputs integers and stores them in an array, stopping */
/* when a zero is entered. Finds and displays the array's */
/* largest and smallest values */
#include <stdio.h>

```
#define MAX 100

int array[MAX];
int count = -1, maximum, minimum, num_entered, temp;

int main(void) {

    puts("Enter integer values per line.");
    puts("Enter 0 when finished.");

    * Input the values */
    do {
        scanf("%d", &count);
        array[++count] = temp;
    } while (count < (MAX-1) && temp != 0 );

    num_entered = count;

    /* Find the largest and smallest. */
    /* First set maximum to a very small value, */
    /* and minimum to a very large value. */

    maximum = -32000;
    minimum = 32000;

    for (count = 0; count <= num_entered && array[count] != 0; count++) {
        if (array[count] > maximum)
            maximum = array[count];

        if (array[count] < minimum)
            minimum = array[count];
    }

    printf("\n\nThe maximum value is %d", maximum);
    printf("\n\nThe minimum value is %d\n", minimum);

    return 0;
}
```