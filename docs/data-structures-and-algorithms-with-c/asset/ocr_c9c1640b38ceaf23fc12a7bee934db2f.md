| 21 | 22 | 23 | 24 |
| 31 | 32 | 33 | 34 |
| Elements of the array | | | |
| 11 | 12 | 13 | 14 |
| 21 | 22 | 23 | 24 |
| 31 | 32 | 33 | 34 |

Note that p may now be used as an array of size 4.

In the second method, the numbers of rows, as well as a number of columns both, are unknown at compile time they will be known at the execution time. The following steps are used to create a two-dimensional array dynamically:

+   i) At first, an array of pointers is to be created dynamically. This array of pointers will have the same size as the number of rows of the two-dimensional array. The i th array element should point to the beginning of the i th row.
+   
+   ii) Allocate memory space for the entire array dynamically. The total space may be contiguous or may not be so. However, the minimum condition is that all the elements of each row must be allocated space contiguously.
+   
+   iii) The value of each element of the pointer array that created in the first step is to be properly initialized.

# Contiguous Allocation of Two-dimensional Array

In the contiguous allocation of memory space for the two-dimensional array, the whole array is allocated dynamically. The total memory space of two-dimensional array should be contiguous. An array of pointers is also to be created dynamically. This array of pointers will have the same size as the number of rows of the two-dimensional array and the i th array element should point to the beginning of the i th row.

![](bbox=[0.28, 0.55, 0.72, 0.7])

Note that the array of pointers can be represented by pointer to pointer.

# Example:

```
#include<stdio.h>
#include<stdlib.h>
main()
{
int **p, *q, m, n, i, j;
printf("Enter number of rows");
scanf("%d", &m);
printf("Enter number of columns");
```