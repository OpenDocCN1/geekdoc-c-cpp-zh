# 2. Efficiency of selection sort

Let us now analyze the efficiency of the selection sort. You can easily understand from the algorithm that the first pass of the program does (maxsize – 1) comparisons. The next pass does (maxsize – 2) comparisons and so on. Thus, the total number of comparisons at the end of the sort would be :

(maxsize – 1) + (maxsize – 2) + ... + 1 = maxsize * (maxsize – 1) / 2 = O(maxsize²)

Note that this efficiency is same as the worst case of quick sort.

# 17.2.5 Merge Sort

The merge sort technique sorts a given set of values by combining two sorted arrays into one larger sorted array.

Consider the sorted array, A, which contains p elements, and the sorted array B, containing q elements. The merge sort technique combines the elements of A and B into a single sorted array C with p + q elements.

The total number of comparisons in the merge sort technique to sort n data-items of an array is log n. The merge sort technique requires at most log n passes, so the complexity of the merge sort is O(n log n).

Consider an example, to merge two sorted arrays into a single sorted array by using the merge sort technique. The data items stored in an array A, are:
A={56,78}
The data items stored in an array, B, are:
B={45,67,89}
The data items of the C array after merging the two sorted arrays, A and B, are:
C={45, 56, 67, 78, 89}

The first data item of the A array is compared with the first data item of the B array. If the first data item of A is smaller than the first data item of B, then that data item from A is moved to the new array, C. If the data item of B is smaller than the data item of A, then it is moved to the array, C. This comparing of data items continues until one of the arrays ends.

The following code shows the implementation of merge sort technique.

```
#include<stdio.h>
#include<conio.h>
void smerge_(sort *a, int *b, int *c, int n1, int n2, int *n);
void main()
{
int n1=0, n2=0, n0,i=0;
int a[30], b[30], c[60];
clrscr();
printf("\nEnter two sorted arrays\n");
printf("\nDetails of 1st array:");
printf("\nNumber of elements n1: ");
scanf("%d",&n1);
printf("Enter elements: ");
for(i=0;i<n1;i++
```