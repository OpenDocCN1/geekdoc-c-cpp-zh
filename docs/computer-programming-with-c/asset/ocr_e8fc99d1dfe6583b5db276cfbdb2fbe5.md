```
```c
#include<stdio.h>
float max(float [], int);
void main()
{
    int n,i;
    float a[100];
    float res;
    printf("How many numbers do you want to enter? \n");
    scanf("%d",&n);
    printf("Enter %d numbers\n",n);
    for(i=0;i<=n-1;i++)
    {
        scanf("%f",&a[i]);
    }
    res= max(a,n);
    printf("Maximum is %f\n",res);
}
float max(float p[], int n)
{
int i;
float max=p[0];
for(i=1;i<=n-1;i++)
{
    if(max<p[i])
    {
        max=p[i];
    }
}
return max;
}
```
```

# Output

```
```text
How many numbers do you want to enter?
3
Enter 3 numbers
10 35 20
Maximum is 35.000000
```
```

# 7.6.1  Arrange n numbers in descending order using functions: An example

Let us create a function `sort_desc()` to arrange n numbers in descending order. Before we design the function, it should be noted that ‘arrays’ are always passed by address, unlike other variables which are passed by value. We will discuss a detailed difference between ‘call by address’ and ‘call by value’ in Chapter 8 of this textbook. However, the