# Accessing Of Array

# Element:

```
/*Write a program to input values into
an array and display them*/
#include<stdio.h>

int main()
{
int arr[5],i; for(i=0;i<5;i++)
{
    printf("enter a value for arr[%d] \n",i);
    scanf("%d",&arr[i]);
}
}
```