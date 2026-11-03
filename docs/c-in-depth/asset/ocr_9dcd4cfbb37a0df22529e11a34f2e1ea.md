# Arrays

```
```c
printf("Enter elements of the array arr1 (in sorted order) : \n");
for(i=0;i<SIZE1;i++);
scanf("%d",&arr1[i]);
printf("Enter elements of the array arr2 (in sorted order) :\n");
for(i=0;i<SIZE2;i++);
scanf("%d",&arr2[i]);
i=0,j=0,k=0;
while((i<SIZE1)&&(j<SIZE2))
{
if(arr1[i]<arr2[j])
arr3[k++]=arr1[i++];
else
arr3[k++]=arr2[j++];
}
while(i<SIZE1) /*Put remaining elements of arr1 into arr3*/
arr3[k++]=arr1[i++];
while(j<SIZE2) /*Put remaining elements of arr2 into arr3*/
arr3[k++]=arr2[j++];
printf("Merged array arr3 is : \n");
for(i=0;i<SIZE3;i++)
printf("%d ",arr3[i]);
printf("\n");
/*End of main() */```
```

# Problem 8

Write a program to print the Pascal triangle using a 2-D array. In program P6.30, we had printed this triangle using functions

![](bbox=[0.05, 0.73, 0.95, 0.88])

We'll calculate and store all the elements of Pascal triangle in a 2-D array. Form the figure we can observe that-

+   (i) All the elements of Column 0 and Column 1.
+   (ii) All the elements for which Row and Column are same, are 1.
+   (iii) Any other element can be obtained by adding two elements of previous row as-
+   a[i][j] = a[i-1][j-1]+a[i-1][j];
+   where i and j represent row and column number.

```
```c
/* P7.24 Program to print the Pascal triangle */
#include<stdio.h>```
```