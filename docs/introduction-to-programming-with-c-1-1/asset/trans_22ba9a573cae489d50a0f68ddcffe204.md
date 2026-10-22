

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

    printf("Enter the element to be searched\n");
    scanf("%d",&key);

    low=0;

    high=n-1;

    while(low<=high)   /*binary search*/
    {
        mid=(low+high)/2;   /*compute mid*/
        if(key==a[mid])  /*compare with mid if its equal stop searching*/
        {

found=1;

break;

}
else if(key>a[mid])

low=mid+1;

else

high=mid-1;
}

if(found==1)

printf("element found at %d position\n",mid);
else

printf("element not found\n");
getch();
}
```

## Advantage
- Simple technique
- Very efficient searching technique

## Disadvantage
- The array elements should be sorted

## Sorting
It is the process of arranging the random numbers either in the ascending order or in the descending order. There are many different sorting techniques such as bubble sort, selection sort, merge sort etc.

## Bubble sort
Here, compare the adjacent elements. If the number to the left is greater than the number to the right, then exchange them. If the number to the left is not greater than the number to the right, then don’t exchange them. At the end of each pass largest element will be in its sorted position. This is also called as sinking sort.

```
/*bubble sort*/
#include<stdio.h>
#include<conio.h>
void main()
{
int i,j,n,a[20],temp;
clrscr();
printf("Enter the size: ");
scanf("%d",&n);
printf("Enter %d numbers \n",n);
for(i=0;i<n;i++)
scanf("%d",&a[i]);
for(i=1;i<n;i++)
{
  for(j=0;j<n-i;j++)
  {
    if(a[j]>a[j+1])
    {
        temp=a[j];
        a[j]=a[j+1];
        a[j+1]=temp;
    }
  }
}
printf("\nThe sorted array is \n");
for(i=0;i<n;i++)
printf("%d \n",a[i]);
getch();
}
```

## Advantage
- Very simple and easy to program
- Straight forward approach

## Disadvantage
- Less efficient
- It requires n-1 passes even if the elements are sorted

## Two dimensional arrays
Arrays with two sets of square brackets [][ ] are called two dimensional arrays. It’s used when the data items are arranged in row-wise and column wise in a tabular fashion. To identify an item we need to specify two indices: the first index identifies the row number and second index identify the column number of the item.

## Declaration of 2D array

### Syntax
```
Data_type array_name[exp1][exp2];
```
Where
- Data_type can be int, float, char etc
- Array name is the name of the array
- Exp1 and exp2 are constant expressions and must be enclosed within square brackets and no variables are allowed.

Ex:
```
int a[10][20];
```
the array a is an integer array with 10 rows and 20 columns. it reserves 10*20=200 locations contiguously one after the other.

## Initialization
```
Data_type array_name[exp1][exp2]={
    {a1,a2,............an},
    {b1,b2, ..........bn},
    .......................
    .......................
    {z1,z2,..............zn}
};
```
Where
- Data-type can be int,float etc
- Exp1 and exp2 are row and column numbers respectively
- A1 to an are the values assigned to 1st row, b1 to bn are the values assigned to 2nd row and so on.

Ex:
```
int a[4][3]={
    {11,22,33},
    {44,55,66},
    {77,88,99},
    {10,11,12},
};
```
Pictorial representation of above initialization is as shown below

columns

|   | 0 | 1 | 2 |
|---|---|---|---|
| 0 | 11 | 22 | 33 |
| 1 | 44 | 55 | 66 |
| 2 | 77 | 88 | 99 |
| 3 | 10 | 11 | 12 |

rows

Partial array initialization: if the numbers of values to be initialized are less than the size of the array, then the elements are initialized from left to right one after the other. The remaining locations will be initialized to zero automatically.

```
ex: int a[4][3]={  {11,22},
    {33,44},
    {55,66},
    {77,88}
};
```

## Reading and writing two-dimensional arrays
The elements of the matrix can be accessed in two different ways.
- Row major order
- Column major order

## Row major order
All elements are accessed one by one row wise. Here,
- Firstly, all elements in 0th row are accessed
- Secondly, all elements in 1st row are accessed
- Thirdly, all elements in 3rd row are accessed and so on.

## Column major order
All elements are accessed one by one column wise. Here,
- Firstly, all elements in 0th column are accessed
- Secondly, all elements in 1st column are accessed
- Thirdly, all elements in 3rd column are accessed and so on.

## Reading matrix in row major order
```
for(i=0; i<m; i++)        /*m rows*/
{
    for(j=0; j<n; j++)  /*n columns*/
    {
        scanf("%d",&a[i][j]);
    }
}
```

## Reading matrix in column major order
```
for(i=0; i<n; i++)        /*n columns */
{
    for(j=0; j<m; j++)  /*m rows */
    {
        scanf("%d",&a[i][j]);
    }
}
```

## Printing(writing) matrix
```
for(i=0; i<m; i++)        /*m rows*/
{
    for(j=0; j<n; j++)    /*n columns*/
    {
        printf("%d\t",a[i][j]);
    }
    printf("\n");
}
```

## Example programs
```
/*program to add two matrices*/
#include<stdio.h>

void main()
{
int a[10][10],b[10][10],c[10][10],m,n,i,j;
printf("enter the order of matrices\n");
scanf("%d%d",&m,&n);
printf("enter the elements of matrix a\n");
for(i=0; i<m; i++)
{
    for(j=0; j<n; j++)
    {
        scanf("%d",&a[i][j]);
    }
}

printf("enter the elements of matrix b\n");
for(i=0; i<m; i++)
{
    for(j=0; j<n; j++)
    {
        scanf("%d", &b[i][j]);
    }
}

for(i=0; i<m; i++)        /**addition**/
{
    for(j=0; j<n; j++)
    {
        c[i][j]=a[i][j]+b[i][j];
    }
}

printf("resultant matrix c is\n");
for(i=0; i<m; i++)
{
    for(j=0; j<n; j++)
    {
        printf("%d\t", c[i][j]);
    }
    printf("\n");
}
getch();
}
```

/*matrix multiplication*/
#include<stdio.h>
#include<conio.h>
void main()
{
int a[10][10],b[10][10],c[10][10]={0};
int m,n,p,q,i,j,k;
clrscr();
printf("\n Enter the order of the matrix A :");
scanf("%d%d",&m,&n);
printf("\n Enter the order of the matrix B :");
scanf("%d%d",&p,&q);
if(n!=p)
{
printf("multiplication not possible\n");
getch();
exit(0);
}
printf("\n Enter the elements of matrix A in row major order\n");
for(i=0;i<m;i++)
{
for(j=0;j<n;j++)
{
scanf("%d",&a[i][j]);
}
}
printf("\n Enter the elements of matrix B in column major order \n");
for(i=0;i<q;i++)
{
for(j=0;j<p;j++)
{
scanf("%d",&b[j][i]);
}
}
for(i=0;i<m;i++)
{
for(j=0;j<q;j++)
{
for(k=0;k<n;k++)
{
c[i][j]=c[i][j]+a[i][k]*b[k][j];
}
}
}
printf("\n Resultant matrix is \n");
for(i=0;i<m;i++)
{
for(j=0;j<q;j++)
{
printf("%d\t",c[i][j]);
}
printf("\n");
}
getch();
}
```

```
printf("enter the order of matrices\n");
scanf("%d%d",&m,&n);
printf("enter the elements of matrix a\n");
for(i=0; i<m; i++)
{
    for(j=0; j<n; j++)
    {
        scanf("%d",&a[i][j]);
    }
}
for(i=0; i<m; i++)
{
    for(j=0; j<n; j++)
    {
        b[j][i]=a[i][j];
    }
}
printf("resultant matrix is\n");
for(i=0; i<n; i++)
{
    for(j=0; j<m; j++)
    {
        printf("%d\t",b[i][j]);
    }
    printf("\n");
}
getch();
}
```

## Strings
A string is an array of characters terminated by NULL character which is denoted by the escape sequence '\0'.

Ex: “VTU” is stored as

| V | T | U | \0 |

Strings are treated as an array of characters. String variable can be declared as
```
char a[20];
```
the string variable a can hold maximum of 20 characters including null character.

## String initialization

## String input/output functions
- Formatted input function (scanf)
- Formatted output function (printf)
- Unformatted input function (gets)
- Unformatted output function (puts)

## Formatted input and output function (scanf,printf)
The format specifier used is %s.

## Working
- If white spaces are present before the string, then they are removed from the keyboard buffer
- All nonwhite space characters are copied into the array till it finds another white space. Then the copied string is terminated by '\0'. Remaining characters are left in the keyboard buffer.

```
char s1[15];
scanf("%s",s1);
printf("%s\n",s1);
```

