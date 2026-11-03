+   1. We will take 74 as the pivot and move it to position so that the new list becomes—39, 35, 32, 74, 97, 84. Note that the elements to the left are lesser than 74. Also, these elements (39, 35 and 32) are yet to be sorted. Similarly, the elements 97 and 84, which are right to the pivot, are yet to be sorted.
+   2. Now take the partitioned list—39, 35, 32. Let us take 39 as the pivot. Moving it to the correct position gives—35, 32, 39. The partition to the left is 35, 32. There is no right partition. Reapply the process on the partition, we get 32, 35. Thus, we have 32, 35, 39.
+   3. Apply the process to the right partition of 74 which is 97, 84. Taking 97 as the pivot and positioning it, we get 74, 84, 97.
+   4. Assembling all the elements from each partition, we get the sorted list.

# 1. C program for quick sort

The quick sort is a very good example for recursive programming. Let us assume that an array named elements[] will hold the array to be sorted and maxsize is the number of elements to be sorted. We will also assume that the sorting order is ascending in nature. The required C program is shown in Fig. 17.2.

```
#include <stdlib.h>
#include <stdio.h>

#define MAXSIZE 500
void quickSort(int elements[], int maxsize);
void sort(int elements[], int left, int right);

int elements[MAXSIZE];

int main()
{
    int i, maxsize;
    printf("\nHow many elements you want to sort: ");
    scanf("%d",&maxsize);
    printf("\nEnter the values one by one: ");
    for (i = 0; i < maxsize; i++)
    {
        printf ("\nEnter element %i : ");
        scanf("%d",&elements[i]);
    }
    printf("\nArray before sorting:\n");
    for (i = 0; i < maxsize; i++)
    {
        printf("[%d] ",elements[i]);
    }
    printf ("\n");
    quickSort(elements, maxsize);
    printf("\nArray after sorting:\n");
    for (i = 0; i < maxsize; i++)
```