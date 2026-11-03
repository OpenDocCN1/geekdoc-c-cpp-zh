# Program

```
```c
#include<stdio.h>
#include<omp.h>
void main()
{
int a[10],b[10],c[10],i, n;
int tid;
printf("\n Enter the number of elements");
scanf("%d",&n);
printf("\n Enter the element of 1st array");
for(i=0;i<n;i++)
    scanf("%d",&a[i]);
printf("Enter the elements of 2nd array");
for(i=0;i<n;i++)
    scanf("%d",&b[i]);
printf("\n Array A\n");
for(i=0;i<n;i++)
{
printf("a[%d]=%d\n",i,a[i]);
}
printf("\n Array B\n");
for(i=0;i<n;i++)
{
printf("b[%d]=%d\n",i,b[i]);
}
#pragma omp parallel for
for(i=0;i<n;i++)
{
tid=omp_get_thread_num();
c[i]=a[i]+b[i]; /* addition of array A and array B in parallel */
printf("\nc[%d]=%d,thread id=%d\n",i,c[i],tid);
}
printf("\n===the new Array C is===\n");
for(i=0;i<n;i++)
{
printf("%d",c[i]);  /* print resultant array C */
}
}
```
```