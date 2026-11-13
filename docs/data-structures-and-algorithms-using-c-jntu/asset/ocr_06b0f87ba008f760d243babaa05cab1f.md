Example 16.8 explains the radix sort.

# Example 16.8

Let DATA be an array of elements such as [82, 43, 64, 11, 56, 75, 49, 63, 99, 78, 70, 18, 61].

First pass:

| Pocket | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|---|
| | 70 | 11 | 82 | 43 | 64 | 75 | 56 | 78 | 49 | 99 |
| | 61 | | | 63 | | | | | |

First unit digits in the sequence are sorted. Now the array at this stage will be

70 11 61 82 43 63 64 75 56 78 18 49 99

Second pass: Now comparing the 10-digit values of numbers in the sequence.

Pocket: 0 1 2 3 4 5 6 7 8 9

| Pocket | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|---|
| | 11 | | | | 43 | 56 | 61 | 70 | 82 | 99 |
| | 18 | | | | 49 | | 63 | 75 | | |
| | | | | | | 64 | 78 | | | |

Combining all the 10 pockets gives the resultant sequence:

11 18 43 49 56 61 63 64 70 75 78 82 99

# Program 16.7

```
/*To Sort The Given List Using RADIX SORT*/
#include<iostream.h>
#include<conio.h>
#include<math.h>
void radixsort(int a[],int m,int n)
{
int temp,i,j,k,y,digit,b[50],p,q;
y=1;
for(i=1;i<=n;i++)
{
q=1,y+=,p=pow(10,y);
for (j=0;j<=9;j++)
{
for (k=1;k<=n;k++)
{
digit=(a[k]/p)%10;
if (digit==j)
b[q++]=a[k];
}
}
for (temp=1;temp<=n;temp++)
a[temp]=b[temp];
}
```