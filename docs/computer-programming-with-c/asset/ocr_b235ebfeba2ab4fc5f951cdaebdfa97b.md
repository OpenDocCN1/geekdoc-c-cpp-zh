```
```c
for (i=0;i<=n-2;i++)
{
    for(j=i+1;j<=n-1;j++)
    {
        if(a[i]>a[j])
        {
            /* Swap the 2 numbers */
            t=a[i];
            a[i]=a[j];
            a[j]=t;
        }
    }
}
printf("Ascending order is: \n");
for(i=0;i<=n-1;i++)
{
    printf("%d\n",a[i]);
}
```
```

# Output:

```
How many numbers you want to enter ?
5
Enter 5 numbers:
15 12 19 17 6
Ascending order is:
6
12
15
17
19
```

> **What is the change that I can make in this program to arrange numbers in descending order, instead of ascending?**
> 
> The program is arranging the numbers in ascending order because we are swapping the values of `a[i]` and `a[j]` if value of `a[i]` is greater than value of `a[j]`. As `a[i]` represents the number at a lower index in the array and `a[j]` represents the number at a higher index in the array, the swapping process ensures that the number at lower index is always less than number at higher index; thereby arranging the array in ascending order. In case of descending order we want the number at lower index of the array to be always greater than the number at higher index of the array. Hence we would swap `a[i]` and `a[j]` if `a[i]` is less than `a[j]` to arrange numbers in descending order. Therefore the only change that must be applied to the given program to arrange the numbers in descending order is that the condition in the `if` block responsible for swapping must now be specified as `a[i] < a[j]`.

![](bbox=[0.164, 0.765, 0.203, 0.801])