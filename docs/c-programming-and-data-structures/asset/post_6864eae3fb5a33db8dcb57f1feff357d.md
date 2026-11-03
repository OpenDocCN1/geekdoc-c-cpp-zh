
## EXAMPLE 3.6 Write a program for finding the desired kᵗʰ smallest element in an array.

- 1. Set the size n of an array.
- 2. Store n elements in the array.
- 3. Read and store elements of the array in an ascending order.
- 4. Print the kᵗʰ elements of sorted array.

A program is given in Fig. 3.6.

```
Program
#include <stdio.h>
#include <conio.h>
void main()
{
    int *arr,i,j,n,temp,k;
    clrscr();
    printf("Enter the number of elements in the array:");
    scanf("%d",&n);
    arr=(int*)malloc(sizeof(int)*n);
    for(i=0;i<n;i++)
    {
        printf("Enter a number:");
        scanf("%d",&arr[i]);
    }
    for(i=0;i<n;i++)
    {
        for(j=i+1;j<n;j++)
        {
            if(arr[i]>arr[j])
            {
                temp=arr[i];
                arr[i]=arr[j];
                arr[j]=temp;
            }
        }
    }
    printf("\nElements of array after sorting:");
    for(i=0;i<n;i++)
    {
        printf("\n%d",arr[i]);
    }
    printf("\n\nWhich smallest element do you want to determine?");
    scanf("%d",&k);
    if(k<=n)
        printf("\nDesired smallest element is %d.",arr[k-1]);
    else
        printf("\nPlease enter a valid value for finding the particular\nsmallest element");
    getch();
}
```

Output
Enter the number of elements in the array:5
Enter a number:33
Enter a number:32
Enter a number:46
Enter a number:58
Enter a number:47
Elements of array after sorting:
32
33
46
47
58
Which smallest element do you want to determine?3
Desired smallest element is 46.

Fig. 3.6 Program to determine Kth smallest element in an array

## 3.5 TWO-DIMENSIONAL ARRAYS

So far we have discussed the array variables that can store a list of values. There could be situations where a table of values will have to be stored. Consider the following data table, which shows the value of sales of three items by four sales girls:

|  | Item1 | Item2 | Item3 |
|---|---|---|---|
| Salesgirl #1 | 310 | 275 | 365 |
| Salesgirl #2 | 210 | 190 | 325 |
| Salesgirl #3 | 405 | 235 | 240 |
| Salesgirl #4 | 260 | 300 | 380 |

The table contains a total of 12 values, three in each line. We can think of this table as a matrix consisting of four rows and three columns. Each row represents the values of sales by a particular salesgirl and each column represents the values of sales of a particular item.

In mathematics, we represent a particular value in a matrix by using two subscripts such as v_ij. Here v denotes the entire matrix and v_ij refers to the value in the i th row and j th column. For example, in the above table v_23 refers to the value 325

C allows us to define such tables of items by using two-dimensional arrays. The table discussed above can be defined in C as v[4][3]

Two-dimensional arrays are declared as follows:

```
type array_name [row_size][column_size];
```

Note that unlike most other languages, which use one pair of parentheses with commas to separate array sizes, C places each size in its own set of brackets.

Two-dimensional arrays are stored in memory, as shown in Fig. 3.7. As with the single-dimensional

![](img/fe6da5f61b1e2c77309bbee135b45e35_199_0.png)

Fig. 3.7 Representation of a two-dimensional array in memory

arrays, each dimension of the array is indexed from zero to its maximum size minus one; the first index selects the row and the second index selects the column within that row.

## EXAMPLE 3.7

Write a program using a two-dimensional array to compute and print the following information from the table of data discussed above:

- (a) Total value of sales by each girl.
- (b) Total value of each item sold.
- (c) Grand total of sales of all items by all girls.

The program and its output are shown in Fig. 3.8. The program uses the variable value in two-dimensions with the index i representing girls and j representing items. The following equations are used in computing the results:

(a) Total sales by mth girl = Σ_{j=0}^{2} value[m][j]      (girl_total[m])
(b) Total value of nth item = Σ_{i=0}^{3} value[i][n]      (item_total[n])
(c) Grand total = Σ_{i=0}^{3} Σ_{j=0}^{2} value[i][j]
      = Σ_{i=0}^{3} girl_total[i]
      = Σ_{j=0}^{2} item_total[j]

```
Program
    #define MAXGIRLS 4
    #define MAXITEMS 3
    main()
    {
        int value[MAXGIRLS][MAXITEMS];
        int girl_total[MAXGIRLS], item_total[MAXITEMS];
        int i, j, grand_total;
        /*......READING OF VALUES AND COMPUTING girl_total .....*/
        printf("Input data\n");
        printf("Enter values, one at a time, row-wise\n\n");
        for( i = 0 ; i < MAXGIRLS ; i++ )
        {
            girl_total[i] = 0;
            for ( j = 0 ; j < MAXITEMS ; j++ )
            {
                scanf("%d", &value[i][j]);
                girl_total[i] = girl_total[i] + value[i][j];
            }
        }
        /*.....COMPUTING item_total.............*/
        for ( j = 0 ; j < MAXITEMS ; j++ )
        {
            item_total[j] = 0;
            for ( i = 0 ; i < MAXGIRLS ; i++ )
            {
                item_total[j] = item_total[j] + value[i][j];
            }
        }
        /*.....COMPUTING grand_total.............*/
        grand_total = 0;
        for ( i = 0 ; i < MAXGIRLS ; i++ )
        {
            grand_total = grand_total + girl_total[i];
        }
        /* .....PRINTING OF RESULTS.............*/
        printf("\n GIRLS TOTALS\n");
        for ( i = 0 ; i < MAXGIRLS ; i++ )
        {
            printf("Salesgirl[%d] = %d\n", i+1, girl_total[i] );
        }
        for ( j = 0 ; j < MAXITEMS ; j++ )
        {
            printf("\nItem[%d] = %d\n", j+1, item_total[j] );
        }
        printf("\nGrand Total = %d\n", grand_total);
    }
```

Output

Input data
Enter values, one at a time, row wise

- 310 275 365
- 210 190 325
- 405 235 240
- 260 300 380

## GIRLS TOTALS

- Salesgirl[1] = 950
- Salesgirl[2] = 725
- Salesgirl[3] = 880
- Salesgirl[4] = 940

## ITEM TOTALS

- Item[1] = 1185
- Item[2] = 1000
- Item[3] = 1310

Grand Total = 3495

> Fig. 3.8 Illustration of two-dimensional arrays

## Arrays 3.17

## EXAMPLE 3.8

|   | 1 | 2 | 3 | 4 | 5 |
| --- | --- | --- | --- | --- | --- |
| 1 | 1 | 2 | 3 | 4 | 5 |
| 2 | 2 | 4 | 6 | 8 | 10 |
| 3 | 3 | 6 | . | . | . |
| 4 | 4 | 8 | . | . | . |
| 5 | 5 | 10 | . | . | 25 |

The program shown in Fig. 9 uses a two-dimensional array to store the table tables. Each value is calculated using the control variables of the nested loops as follows:

product[i][j] = row * column

where i denotes rows and j denotes columns of the product table. Since the indices i and j range from 0 to 4, we have introduced the following transformation:

```
#define ROWS 5
#define COLUMNS 5
main()
{
int row, column, product[ROWS][COLUMNS];
int i, j ;
printf("MULTIPLICATION TABLE\n");
printf(" ");
for ( j = 1 ; j < COLUMNS ; j++ )
printf("%4d", j ) ;
printf("\n");
printf("--------------------------------------\n");
for ( i = 0 ; i < ROWS ; i++ )
{
row = i + 1 ;
printf("%2d |", row) ;
for ( j = 1 ; j < COLUMNS ; j++ )
{
column = j ;
product[i][j] = row * column ;
printf("%4d", product[i][j]) ;
}
printf("\n");
}
printf("\n");
}
```

(Contd.)

## 3.6 INITIALIZING TWO-DIMENSIONAL ARRAYS

Like the one-dimensional arrays, two-dimensional arrays may be initialized by following their declaration with a list of initial values enclosed in braces.

```
int table[2][3] = { 0,0,0,1,1,1};
```

initializes the elements of the first row to zero and the second row to one. The initialization is done row by row. The above statement can be equivalently written as

```
int table[2][3] = {{0,0,0}, {1,1,1}};
```

by surrounding the elements of each row by braces.

We can also initialize a two-dimensional array in the form of a matrix as shown below:

```
int table[2][3] = {
  {0,0,0},
  {1,1,1}
};
```

Note the syntax of the above statements. Commas are required after each brace that closes off a row, except in the case of the last row.

When the array is completely initialized with all values, explicitly, we need not specify the size of the first dimension. That is, the statement

```
int table [] [3] = {
  { 0, 0, 0 },
  { 1, 1, 1 }
};
```

is permitted.

If the values are missing in an initializer, they are automatically set to zero. For instance, the statement

```
int table[2][3] = {
  {1,1},
  {2}
};
```

will initialize the first two elements of the first row to one, the first element of the second row to two, and all other elements to zero.

When all the elements are to be initialized to zero, the following short-cut method may be used.

```
int m[3][5] = { {0}, {0}, {0}};
```

The first element of each row is explicitly initialized to zero while other elements are automatically initialized to zero. The following statement will also achieve the same result:

```
int m [3] [5] = { 0, 0 };
```

|   | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
|1|1|2|3|4|5|
|2|2|4|6|8|10|
|3|3|6|9|12|15|
|4|4|8|12|16|20|
|5|5|10|15|20|25|

Fig. 3.9 Program to print multiplication table using two-dimensional array
