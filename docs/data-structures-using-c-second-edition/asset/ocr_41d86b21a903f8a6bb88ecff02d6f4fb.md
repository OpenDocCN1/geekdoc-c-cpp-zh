# # Complexity of Quick Sort

In the average case, the running time of quick sort can be given as o(n log n). The partitioning of the array which simply loops over the elements of the array once uses o(n) time.

In the best case, every time we partition the array, we divide the list into two nearly equal pieces. That is, the recursive call processes the sub-array of half the size. At the most, only log n nested calls can be made before we reach a sub-array of size 1. It means the depth of the call tree is o(log n). And because at each level, there can only be o(n), the resultant time is given as o(n log n) time.

Practically, the efficiency of quick sort depends on the element which is chosen as the pivot. Its worst-case efficiency is given as o(n^2). The worst case occurs when the array is already sorted (either in ascending or descending order) and the left-most element is chosen as the pivot.

However, many implementations randomly choose the pivot element. The randomized version of the quick sort algorithm always has an algorithmic complexity of o(n log n).

# # Pros and Cons of Quick Sort

It is faster than other algorithms such as bubble sort, selection sort, and insertion sort. Quick sort can be used to sort arrays of small size, medium size, or large size. On the flip side, quick sort is complex and massively recursive.

# # PROGRAMMING EXAMPLE

+   9. Write a program to implement quick sort algorithm.

```
```c
#include <stdio.h>
#include <conio.h>
#define size 100
int partition(int a[], int beg, int end);
void quick_sort(int a[], int beg, int end);
void main()
{
   int arr[size], i, n;
   printf("\n Enter the number of elements in the array: ");
   scanf("%d", &n);
   printf("\n Enter the elements of the array: ");
   for(i=0;i<n;i++)
   {
      scanf("%d", &arr[i]);
   }
   quick_sort(arr, 0, n-1);
   printf("\n The sorted array is: \n");
   for(i=0;i<n;i++)
   printf(" %d", arr[i]);
   getch();
}
int partition(int a[], int beg, int end)
{
   int left, right, temp, loc, flag;
   loc = left = beg;
   right = end;
   flag = 0;
   while(flag != 1)
   {
      while((a[loc] <= a[right]) && (loc!=right))
      right--;
```
```