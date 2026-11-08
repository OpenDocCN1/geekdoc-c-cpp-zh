![](bbox=[0.285, 0.156, 0.778, 0.412])

# **39. Program to accept ten different numbers and print the array elements.**

```
```c
/* printing all elements of array */
#include<stdio.h>
#include<conio.h>

void main()
{
    int arr[10],i;
    clrscr();
    for(i=0;i<10;i++)
    {
        printf("Enter the %d element \n",i);
        scanf("%d",&arr[i]);
    }
    for(i=0;i<10;i++)
    {
        printf("The array element %d is %d\n",i,arr[i]);
    }
    for(i=0;i<10;i++)
    {
        printf("%d\t",arr[i]);
    }
    getch();
}
```
```