d. 20 bytes

e. 20 bytes

+   10. a. A

+   b. A

+   c. 0 (NULL)

+   d. This is beyond the end of the string, so it could have any value.

+   e. 73

+   f. This contains the address of the first element of the string.

# Exercises

+   1. char letter = '$';

+   2. char array[] = "Pointers are fun!"

+   3. char *array = "Pointers are fun!"

+   4. The code is as follows:

```
char *ptr;
ptr = malloc(81);
gets(ptr);
```

+   5. The following is one possible answer. A complete program is provided:

```
#include <stdio.h>

#define SIZE 10

/* function prototypes */
void copyarrays(int [], int []);

int main(void )\n{
int ctr0=0;
int a[SIZE] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
int b[SIZE];

/* values before copy */
for (int ctr = 0; ctr < SIZE; ctr ++)
{
printf("%a[%d] = %d, b[%d] = %d\n",
ctr, a[ctr], ctr, b[ctr]);
}
copyarrays(a, b);

/* values after copy *//
```