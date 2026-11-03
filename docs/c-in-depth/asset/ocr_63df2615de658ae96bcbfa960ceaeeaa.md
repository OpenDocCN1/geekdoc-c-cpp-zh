```
```c
array */
#include<stdio.h>
main()
{
    int arr[5]={5,10,15,20,25};
    int i;
    for(i=0;i<5;i++)
    {
        printf("Value of arr[%d] = %d\t",i,arr[i]);
        printf("Address of arr[%d] = %u\n",i,&arr[i]);
    }
}
```
```

# Output:

Value of arr[0] = 5      Address of arr[0] = 2000
Value of arr[1] = 10     Address of arr[1] = 2002
Value of arr[2] = 15     Address of arr[2] = 2004
Value of arr[3] = 20     Address of arr[3] = 2006
Value of arr[4] = 25     Address of arr[4] = 2008

The name of the array ‘arr’ denotes the address of 0th element of array which is 2000. The address of 0th element can also be given by &arr[0], so arr and &arr[0] represent the same address. The name of an array is a constant pointer, and according to pointer arithmetic when an integer is added to a pointer then we get the address of next element of same base type. Hence (arr+1) will denote the address of the next element arr[1]. Similarly (arr+2) denotes the address of arr[2] and so on. In other words we can say that the pointer expression (arr+1) points to 1st element of array, (arr+2) points to 2nd element of array and so on.

| Expression | Meaning | Address | Value |
|---|---|---|---|
| arr | → Points to 0th element | → &arr[0] | → 2000 |
| arr+1 | → Points to 1st element | → &arr[1] | → 2002 |
| arr+2 | → Points to 2nd element | → &arr[2] | → 2004 |
| arr+3 | → Points to 3rd element | → &arr[3] | → 2006 |
| arr+4 | → Points to 4th element | → &arr[4] | → 2008 |

In general we can write-
The pointer expression (arr+i) denotes the same address as &arr[i]. Now if we dereference arr, then we get the 0th element of array, i.e. expression *arr or *(arr+0) represents 0th element of array. Similarly on dereferencing (arr+1) we get the 1st element and so on.

| Expression | Meaning | Equivalent | Value |
|---|---|---|---|
| *arr | → Value of 0th element | → arr[0] | → 5 |
| *(arr+1) | → Value of 1st element | → arr[1] | → 10 |
| *(arr+2) | → Value of 2nd element | → arr[2] | → 15 |
| *(arr+3) | → Value of 3rd element | → arr[3] | → 20 |
| *(arr+4) | → Value of 4th element | → arr[4] | → 25 |

In general we can write-
*(arr+i)    arr[i]
So in subscript notation the address of an array element is &arr[i] and its value is arr[i], while in pointer