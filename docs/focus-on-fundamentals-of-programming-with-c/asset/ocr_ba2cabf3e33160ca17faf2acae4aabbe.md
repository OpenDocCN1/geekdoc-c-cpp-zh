Our array looks like this before the call to swap() :

![](bbox=[0.2, 0.12, 0.74, 0.23])

Our array looks like this after the call to swap() :

![](bbox=[0.2, 0.31, 0.74, 0.45])

# Example: Merge Arrays

Here's a program to merge two sorted arrays into a single sorted array:

```
// Merge two sorted arrays into a single array.

#include <stdio.h>

void mergeTwoArrays(int a[], int b[], int c[], int maxA, int maxB);

int main(void) {
   int k;

   int a[5] = {1, 5, 9, 11, 17};
   int b[5] = {2, 4, 6, 8, 20};
   int c[10];

   mergeTwoArrays(a, b, c, 5, 5);

   for (k = 0; k < (10); k++) {
      printf("%5d", c[k]);
   }

   return 0;
}
```