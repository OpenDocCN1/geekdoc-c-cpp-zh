```
```c
j = i - 1;    // Assigning j to Last array element
i = 0;        // Assigning i to first array element
while (i < j)
{
    Temp = a[i];
    a[i] = a[j];
    a[j] = Temp;
    i++;
    j--;
}
printf("\nResult of an Reverse array is: ");
for (i = 0; i < Size; i++)
{
    printf("%d \t", a[i]);
}
return 0;
}
```
```

# 5.5 Finding Odd, Even, Prime from Array

```
```c
#include<stdio.h>
#include<conio.h>
void main()
{
    int arr[20],size,i,j,n;
    clrscr();
    printf("Enter number of elements you want to enter in array: ");
    scanf("%d",&size);
    printf("Enter elements in array: ");
    for(i=0;i<size;i++)
    {
        scanf("%d",&arr[i]);
    }
    for(i=0;i<size;i++)
    if(arr[i]%2 == 0)
    printf("%d No is Even",arr[i]);
    else
    printf("%d No is Odd",arr[i]);
    printf("Prime numbers are :- \n");
```
```