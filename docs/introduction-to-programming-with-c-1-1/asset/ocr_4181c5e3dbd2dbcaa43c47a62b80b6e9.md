The above 4 steps has to be repeatedly executed as long as low is less than or equal to high. Finally, when the value of low exceeds the value of high indicates that key is not present in the array.

```
/*binary search program*/

#include<stdio.h>

void main()
{
    int a[5],n,i,key,found=0,low,high;

    printf("Enter the size of array\n");

    scanf("%d",&n);

    printf("enter array elements in ascending order\n");

    for(i=0; i<n;i++)
    {
        scanf("%d",&a[i]);
    }

    printf("Enter the element to be srearached\n");
    scanf("%d",&key);

    low=0;

    high=n-1;

    while(low<=high)   /*binary search*/
    {
        mid=(low+high)/2;   /*compute mid*/
        if(key==a[mid])  /*compare with mid if its equal stop searching*/
        {

```