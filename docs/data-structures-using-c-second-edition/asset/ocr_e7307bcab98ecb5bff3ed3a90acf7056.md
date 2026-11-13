```
```c
#include <conio.h>
int main()
{
    int i, n, num, pos, arr[10];
    clrscr();
    printf("\n Enter the number of elements in the array : ");
    scanf("%d", &n);
    for(i=0;i<n;i++)
    {
        printf("\n arr[%d] = ", i);
        scanf("%d", &arr[i]);
    }
    printf("\n Enter the number to be inserted : ");
    scanf("%d", &num);
    printf("\n Enter the position at which the number has to be added : ");
    scanf("%d", &pos);
    for(i=n-1;i>=pos-1--)
        arr[i+1]=arr[i];
    arr[pos-1] = num;
    n = n+1;
    printf("\n The array after insertion of %d is : ", num);
    for(i=0;i<n;i++)
    {
        printf("\n arr[%d] = %d", i, arr[i]);
    }
    getch();
    return 0;
}
```
```

# Output

Enter the number of elements in the array : 5
arr[0] = 1
arr[1] = 2
arr[2] = 3
arr[3] = 4
arr[4] = 5
Enter the number to be inserted : 0
Enter the position at which the number has to be added : 3
The array after insertion of 0 is :
arr[0] = 1
arr[1] = 2
arr[2] = 0
arr[3] = 3
arr[4] = 4
arr[5] = 5

# 8. Write a program to insert a number in an array that is already sorted in ascending order.

```
```c
#include <stdio.h>
#include <conio.h>
int main()
{
    int i, j, n, num, arr[10];
    clrscr();
    printf("\n Enter the number of elements in the array : ");
    scanf("%d", &n);
    for(i=0;i<n;i++)
    {
        printf("\n arr[%d] = ", i);
        scanf("%d", &arr[i]);
    }
    printf("\n Enter the number to be inserted : ");
```
```