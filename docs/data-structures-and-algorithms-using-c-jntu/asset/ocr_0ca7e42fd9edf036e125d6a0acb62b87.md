![](bbox=[0.15, 0.08, 0.85, 0.38])

# Figure 16.11 Trace of heap sort

Figure 16.11 shows various stages in heap sort. The root element is deleted and again reheap is performed. In Figure 16.11(b), 95 is deleted and reheap is performed to make the next highest element as root, i.e. 88. In Figure 16.11(c) 88 is deleted and reheap is performed and the remaining element to make the next highest element is root, i.e. 84. This is continued in this way until only one element exists in the tree.

# Program 16.8

```
#include <iostream.h>
#include<conio.h>
int i,j,k,flag;
void swap(int* x,int*y)
{
int temp;
temp=*x;
*x=*y;
*y=temp;
}
void adjust(int a[],int i,int n)
{
k=a[i];
flag=1;
j=2*k;
while(j<=n&&flag)
{
if(j<n&&a[j]<a[j+1])
j++;
if(k>=a[j])
flag=0;
else
```