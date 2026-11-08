Listing 24.36 shows the implementation of radix sort using C:

# Listing 24.36: Showing the Code for Radix Sort

```
```c
#include "stdio.h"
#define MAX 100
#define SHOWPASS

void Radix_Sort(int *a, int n)
{
    int i, b[MAX], m = 0, exp = 1;
    for (i = 0; i < n; i++)
    {
        if (a[i] > m)
        {
            m = a[i];
        }
    }

    while (m / exp > 0)
    {
        int box[10] = { 0 };
        for (i = 0; i < n; i++)
            box[a[i] / exp % 10]++;
        for (i = 1; i < 10; i++)
            box[i] += box[i - 1];
        for (i = n - 1; i >= 0; i--)
            b[--box[a[i] / exp % 10]] = a[i];
        for (i = 0; i < n; i++)
            a[i] = b[i];
        exp *= 10;

        #ifdef SHOWPASS
        printf("\n\npass...\n");
        for (i = 0; i < n; i++)
        {
            printf("%d\t", a[i]);
        }
        #endif
    }
}

void main()
{
    int array[MAX];
    int i, n;
    printf("\nenter the number of array elements (n<%d) . . .", MAX);
    scanf("%d", &n);
    printf("\nenter the array elements. . .");
    for (i = 0; i < n; i++)
        scanf("%d", &array[i]);
    Radix_Sort(array,0, num);
    printf("\n\nthe sorted array is. . .");
    for (i = 0; i < n; i++)
    {
        printf("%d\t", array[i]);
    }
}
```
```