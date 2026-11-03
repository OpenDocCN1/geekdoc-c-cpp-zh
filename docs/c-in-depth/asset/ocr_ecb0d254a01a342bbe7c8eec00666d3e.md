```
```c
scanf("%d",&item);
for(i=0;i<SIZE;i++)
{
    if(item==arr[i])
    {
        printf("%d found at position %d\n",item,i+1);
        break;
    }
}
if(i==SIZE)
    printf("Item %d not found in array\n", item);
```
```

The item to be searched is compared with each element of the array, if the element is found, for loop is terminated through break statement. The control can come out of the loop in two cases, first if the item is found and loop is terminated through break and second if item is not found and the loop is fully executed. In the second case the value of i would be equal to SIZE. Here we are searching the item sequentially so this search is known as linear or sequential search.

# 7.1.5 1-D Arrays And Functions

# 7.1.5.1 Passing Individual Array Elements to a Function

We know that an array element is treated as any other simple variable in the program. So we can pass individual array elements as arguments to a function like other simple variables.

```
```c
/*P7.8 Program to pass array elements to a function*/
#include<stdio.h>
main()
{
    int arr[10],i;
    printf("Enter the array elements : ");
    for(i=0;i<10;i++)
    {
        scanf("%d",&arr[i]);
        check(arr[i]);
    }
}
check(int num)
{
    if(num%2==0)
        printf("%d is even\n",num);
    else
        printf("%d is odd\n",num);
}
```
```

# 7.1.5.2 Passing whole 1-D Array to a Function

We can pass whole array as an actual argument to a function. The corresponding formal argument should be declared as an array variable of the same data type.

```
```c
main()
{
```
```