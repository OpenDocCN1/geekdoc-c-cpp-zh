# 10.4 Dynamic Storage and Arrays 61

dynamic storage and assign an array pointer to it. The function calloc() allocates a block of storage until it is released by the free() function or the program terminates. The calloc() function is passed arguments telling it how many data cells are needed, and what their size is, in bytes. The address returned by the calloc() function must be converted to the declared data type of the pointer to which it is assigned.

# 10.4.1 One-Dimensional Arrays

Dynamic storage for a one-dimensional array is allocated as follows:

```
int *ptr;
xptr = (int *) calloc(5, sizeof(int));
```

This call to calloc() asks for five data cells of four bytes each. The address that is returned is converted to data type int *.

| | | | |
|---|---|---|---|
| xptr + 0 | 45 | 1000 |
| xptr | 1 | 86 | 1004 |
| xptr + 2 | 63 | 1008 |
| xptr + 3 | 96 | 1012 |
| xptr + 4 | 54 | 1016 |

The following code shows the dynamic storage allocation and prints the address of each element of the array.

```
#include <stdio.h>
#include <stdlib.h>
int main()
{
    int i, *arptr, arsize;
    scanf("%d", &arsize);
    arptr = (int *)calloc(arsize, sizeof(int));
    printf("The memory addresses are: ");
    for(i = 0; i < arsize; i++)
    {
        printf("%d ",", arptr);
        arptr++;
    }
    return 0;
}
```