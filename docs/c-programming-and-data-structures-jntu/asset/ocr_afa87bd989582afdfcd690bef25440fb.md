# # C.32 Solved Question Papers

```
Program:
/* Write a 'C' program that implements the selection sort method */
#include<stdio.h>
#include<conio.h>
Void main()
{
 Int a[20],I,j,temp,t,n,max;
 Clrscr();
 Temp=0;
 Printf("\n enter the no of elements in the list:");
 Scanf("%d",&n);
 Printf("\n enter the elements of the list\n");
 For(i=0;i<n;i++)
 Scanf("%d",&a[i]);
 For(i=n;i>1;i--)
 {
 Max=0;
 For(j=1;j<I;j++)
 If(a[j]>a[max])
 Max=j;
 Temp=a[i-1];
 A[i-1]=a[max];
 A[max]=temp;
 }
 Printf("\n elements in the ascending order are as follows:\n");
 For(i=0;i<n;i++)
 Printf("%d\n",a[i]);
 Getch();
 }
```

Advantage:
Selection sort minimizes data movement by putting one entry at its final position at every pass. Hence this algorithm is useful for continuous list of large elements where movement of entries is expensive.

Disadvantage:
If the elements are stored using linked lists, then insertion sort is more efficient than selection sort. It requires more comparisons than quick sort but is easy to implement than quick sort.

7. Define abstract data type.
Ans: An abstract data type (ADT) is a general way to group and operate on data, independent of any particular language. Two 'classic' ADTs are List and Stack. These concepts exist as general