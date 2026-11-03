
printf("[%d]", elements[i]);
}
void quickSort(int elements[], int maxsize)
{
    sort(elements, 0, maxsize - 1);
}
void sort(int elements[], int left, int right)
{
    int pivot, l, r;
    l = left;
    r = right;
    pivot = elements[left];
    while (left < right)
    {
        while ((elements[right] >= pivot) && (left < right))
            right--;
        if (left != right)
        {
            elements[left] = elements[right];
            left++;
        }
        while ((elements[left] <= pivot) && (left < right))
            left++;
        if (left != right)
        {
            elements[right] = elements[left];
            right--;
        }
    }
    elements[left] = pivot;
    pivot = left;
    left = l;
    right = r;
    if (left < pivot)
        sort(elements, left, pivot - 1);
    if (right > pivot)
        sort(elements, pivot + 1, right);
}

A sample output showing the result of the program is given below:

```
How many elements you want to sort: 6

Enter the values one by one:
Enter element 0 :74

Enter element 1 :39

Enter element 2 :32

Enter element 3 :35

Enter element 4 :97

Enter element 5 :84

Array before sorting:
[74], [39], [32], [35], [97], [84],

Array after sorting:
[32], [35], [39], [74], [84], [97],
```

## 2. Efficiency of quick sort

Let us now analyze the efficiency of the quick sort. The selection of the pivot plays a vital role in determining the efficiency of the quick sort. The main reasons for this are—the pivot may partition the list into two so that one partition is much bigger than the other and the partition may be in an unsorted fashion (which is possible to the maximum). We will analyze the quick sort from the comparison point of view. We will consider two possible cases here.

### Case 1:

In this case we will make two vital assumptions. These are:

- 1. The pivot, which we choose, will always be swapped into exactly the middle of the partition. To put it simple, the pivot (after swapping into its correct position) will have an equal number of elements both to its left and right.
- 2. The number of elements in the list is a power of 2. This means, if there are x elements in the array, we say that x = 2^y. This can be rewritten as y = log₂ x.

## Table 17.2

| Pass | Number of comparisons |
|------|-----------------------|
| 1 | x |
| 2 | 2 * (x / 2) |
| 3 | 4 * (x / 4) |
| 4 | 8 * (x / 8) |
| X | X * (x / x) |

Thus, the total number of comparisons would be O(x) + O(x) + ... + y terms. This is equivalent to O(x * y). Let us substitute y = log₂ x, so that we get O(x log x). Thus the efficiency of quick sort is O(x log x).

### Case II

Let us now forgo one of our assumptions, which we made earlier. We will assume that the pivot partitions the list into two so that one of the partitions has no elements while the other has all the other elements. This is the worst case possible. Here, the total number of comparisons at the end of the sort would have been: (x - 1) + (x - 2) + ... + 2 + 1 = ½(x - 1) * x = ½x² - ½x = O(x²). Thus, the efficiency of the quick sort in its worst case is O(x²).

## 17.2.4 Selection Sort

We will discuss the straight selection sort (also called push-down sorting) in this section. As the name suggests, the first element of the list is selected. It is compared repeatedly with all the elements. If any element is found to be lesser than the selected element, these two are swapped. This procedure is repeated till the entire array is sorted. Let us understand this with a simple example. Consider the list 74, 39, 35, 32, 97, 84. Table 17.3 gives the status of the list after each pass is completed.

## Table 17.3

| Pass | List after pass |
|------|-----------------|
| 1 | 32, 39, 35, 74, 97, 84 |
| 2 | 32, 35, 39, 74, 97, 84 |
| 3 | 32, 35, 39, 74, 97, 84 |
| 4 | 32, 35, 39, 74, 97, 84 |
| 5 | 32, 35, 39, 74, 84, 97 |

### 1. C program for selection sort

Let us assume that an array named elements[] will hold the array to be sorted and maxsize is the number of elements to be sorted. We will also assume that the sorting order is ascending in nature. The required C program is shown in Fig. 17.3.

```
```c
#include <stdlib.h>
#include <stdio.h>
#define MAXSIZE 500
void selection(int elements[], int maxsize);
int elements[MAXSIZE],maxsize;
int main()
{
int i;
printf("\nHow many elements you want to sort: ");
scanf("%d",&maxsize);
printf("\nEnter the values one by one: ");
for (i = 0; i < maxsize; i++)
{
printf ("\nEnter element %i :");
scanf("%d",&elements[i]);
}
printf("\nArray before sorting:\n");
for (i = 0; i < maxsize; i++)
printf("%d ",elements[i]);
printf ("\n");
selection(elements, maxsize);
printf("\nArray after sorting:\n");
for (i = 0; i < maxsize; i++)
{
printf("[%i]", elements[i]);
}
void selection(int elements[], int array_size)
{
int i, j, k;
int min, temp;
for (i = 0; i < maxsize-1; i++)
{
min = i;
for (j = i+1; j < maxsize; j++)
{
if (elements[j] < elements[min])
min = j;
}
temp = elements[i];
elements[i] = elements[min];
elements[min] = temp;
}
}
```
```

Fig. 17.3 C program for selection sorting

## 2. Efficiency of selection sort

Let us now analyze the efficiency of the selection sort. You can easily understand from the algorithm that the first pass of the program does (maxsize – 1) comparisons. The next pass does (maxsize – 2) comparisons and so on. Thus, the total number of comparisons at the end of the sort would be :

(maxsize – 1) + (maxsize – 2) + ... + 1 = maxsize * (maxsize – 1) / 2 = O(maxsize²)

Note that this efficiency is same as the worst case of quick sort.

## 17.2.5 Merge Sort

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
void smerge_sort(int *a, int *b, int *c, int n1, int n2, int *n);
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
for(i=0;i<n1;i++)
scanf("%d",&a[i]);
printf("\n\tDetails of 2nd array:");
printf("\nNumber of elements n2: ");
scanf("%d",&n2);
printf("Enter elements: ");
for(i=0;i<n2;i++)
scanf("%d",&b[i]);
smerge_sort(a, b, c, n1, n2, &n);
printf("\nResultant array after merge sort.\n");
for(i=0;i<n;i++)
printf("%d\t",c[i]);
getch();
}
void smerge_sort(int *a, int *b, int *c, int n1, int n2, int *n)
{
int i=0, j=0, k=0;
while(i<n1 && j<n2)
{
if(a[i]<b[j])
{
c[k]=a[i];
i++;
}
else
{
c[k]=b[j];
j++;
}
k++;
}
while(i<n1)
{
c[k]=a[i];
i++;
k++;
}
while(j<n2)
{
c[k]=b[j];
j++;
k++;
}
*n=k;
}
```

### Fig. 17.4 C program for merge sort

The output of the above code is:

Enter two sorted arrays
Details of 1st array:
Number of elements n1:5
Enter elements: 5 10 14 19 30
Details of 2nd array:
