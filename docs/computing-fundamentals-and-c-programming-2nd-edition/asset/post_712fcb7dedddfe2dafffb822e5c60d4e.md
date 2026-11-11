
- Bubble sort
- Selection sort
- Insertion sort

Other sorting techniques include Shell sort, Merge sort and Quick sort.

Searching is the process of finding the location of the specified element in a list. The specified element is often called the search key. If the process of searching finds a match of the search key with a list element value, the search is said to be successful; otherwise, it is unsuccessful. The two most commonly used search techniques are:

- Sequential search
- Binary search

A detailed discussion on these techniques is beyond the scope of this text. However, you may refer to the QR section for additional information.

## 9.5 TWO-DIMENSIONAL ARRAYS

LO 9.3

So far we have discussed the array variables that can store a list of values. There could be situations where a table of values will have to be stored. Consider the following data table, which shows the value of sales of three items by four salesgirls:

| | Item1 | Item2 | Item3 |
|---|---:|---:|---:|
| Salesgirl #1 | 310 | 275 | 365 |
| Salesgirl #2 | 210 | 190 | 325 |
| Salesgirl #3 | 405 | 235 | 240 |
| Salesgirl #4 | 260 | 300 | 380 |

The table contains a total of 12 values, three in each line. We can think of this table as a matrix consisting of four rows and three columns. Each row represents the values of sales by a particular salesgirl and each column represents the values of sales of a particular item.

In mathematics, we represent a particular value in a matrix by using two subscripts such as v<sub>ij</sub>. Here v denotes the entire matrix and v<sub>ij</sub> refers to the value in the i<sup>th</sup> row and j<sup>th</sup> column. For example, in the above table v<sub>23</sub> refers to the value 325.

C allows us to define such tables of items by using two-dimensional arrays. The table discussed above can be defined in C as

```c
int v[4][3];
```

Two-dimensional arrays are declared as follows:

```c
type array_name [row_size][column_size];
```

Note that unlike most other languages, which use one pair of parentheses with commas to separate array sizes, C places each size in its own set of brackets.

Two-dimensional arrays are stored in memory, as shown in Fig. 9.4. As with the single-dimensional arrays, each dimension of the array is indexed from zero to its maximum size minus one; the first index selects the row and the second index selects the column within that row.

![](img/11b034a94fc590add0a7808250a38792_316_0.png)

**Fig. 9.4** *Representation of a two-dimensional array in memory*

## WORKED-OUT PROBLEM 9.4

Write a program to compute and print a multiplication table for numbers 1 to 5 as shown below.

| | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| 1 | 1 | 2 | 3 | 4 | 5 |
| 2 | 2 | 4 | 6 | 8 | 10 |
| 3 | 3 | 6 | 9 | 12 | 15 |
| 4 | 4 | 8 | 12 | 16 | 20 |
| 5 | 5 | 10 | 15 | 20 | 25 |

The program shown in Fig. 9.5 uses a two-dimensional array to store the table values. Each value is calculated using the control variables of the nested for loops as follows:

```c
product[i][j] = row * column;
```

where i denotes rows and j denotes columns of the product table. Since the indices i and j range from 0 to 4, we have introduced the following transformation:

```c
row = i + 1;
column = j + 1;
```

### Program

```c
#define ROWS 5
#define COLUMNS 5
main()
{
```

(a) Total sales by m<sup>th</sup> girl = Σ<sub>j=0</sub><sup>2</sup> value[m][j] (girl_total[m])

(b) Total value of n<sup>th</sup> item = Σ<sub>i=0</sub><sup>3</sup> value[i][n] (item_total[n])

(c) Grand total = Σ<sub>j=0</sub><sup>2</sup> Σ<sub>i=0</sub><sup>3</sup> value[i][j]  
    = Σ<sub>i=0</sub><sup>3</sup> girl_total[i]  
    = Σ<sub>j=0</sub><sup>2</sup> item_total[j]

### Program

```c
#define MAXGIRLS 4
#define MAXITEMS 3
main()
{
    int value[MAXGIRLS][MAXITEMS];
    int girl_total[MAXGIRLS], item_total[MAXITEMS];
    int i, j, grand_total;
    /*........READING OF VALUES AND COMPUTING girl_total ...*/

    printf("Input data\n");
    printf("Enter values, one at a time, row-wise\n\n");

    for( i = 0 ; i < MAXGIRLS ; i++ )
    {
        girl_total[i] = 0;
        for( j = 0 ; j < MAXITEMS ; j++ )
        {
            scanf("%d", &value[i][j]);
            girl_total[i] = girl_total[i] + value[i][j];
        }
    }
    /*........COMPUTING item_total.........................*/

    for( j = 0 ; j < MAXITEMS ; j++ )
    {
        item_total[j] = 0;
        for( i = 0 ; i < MAXGIRLS ; i++ )
            item_total[j] = item_total[j] + value[i][j];
    }
}
```

initializes the elements of the first row to zero and the second row to one. The initialization is done row by row. The above statement can be equivalently written as

```c
int table[2][3] = {{0,0,0}, {1,1,1}};
```

by surrounding the elements of each row by braces.

We can also initialize a two-dimensional array in the form of a matrix as shown below:

```c
int table[2][3] = {
                    {0,0,0},
                    {1,1,1}
                  };
```

Note the syntax of the above statements. Commas are required after each brace that closes off a row, except in the case of the last row.

When the array is completely initialized with all values, explicitly, we need not specify the size of the first dimension. That is, the statement

```c
int table[][3] = {
        { 0, 0, 0 },
        { 1, 1, 1 }
    };
```

is permitted.

If the values are missing in an initializer, they are automatically set to zero. For instance, the statement

```c
int table[2][3] = {
        {1,1},
        {2}
    };
```

will initialize the first two elements of the first row to one, the first element of the second row to two, and all other elements to zero.

When all the elements are to be initialized to zero, the following short-cut method may be used.

```c
int m[3][5] = { {0}, {0}, {0} };
```

The first element of each row is explicitly initialized to zero while other elements are automatically initialized to zero. The following statement will also achieve the same result:

```c
int m[3][5] = { 0, 0, 0 };
```

## WORKED-OUT PROBLEM 9.6

A survey to know the popularity of four cars (Ambassador, Fiat, Dolphin and Maruti) was conducted in four cities (Bombay, Calcutta, Delhi and Madras). Each person surveyed was asked to give his city and the type of car he was using. The results, in coded form, are tabulated as follows:

| | | | | | | | | | | | |
|---|---|---|---|---|---|---|---|---|---|---|---|
| M | 1 | C | 2 | B | 1 | D | 3 | M | 2 | B | 4 |
| C | 1 | D | 3 | M | 4 | B | 2 | D | 1 | C | 3 |
| D | 4 | D | 4 | M | 1 | M | 1 | B | 3 | B | 3 |
| C | 1 | C | 1 | C | 2 | M | 4 | M | 4 | C | 2 |
| D | 1 | C | 2 | B | 3 | M | 1 | B | 1 | C | 2 |
| D | 3 | M | 4 | C | 1 | D | 2 | M | 3 | B | 4 |

### Program

```c
printf("----------------------------------------\n");
printf("City Ambassador Fiat Dolphin Maruti \n");
printf("----------------------------------------\n");
for ( i = 1 ; i <= 4 ; i++ )
{
    switch(i)
    {
        case 1 :  printf("Bombay  ");
                  break;
        case 2 :  printf("Calcutta ");
                  break;
        case 3 :  printf("Delhi   ");
                  break;
        case 4 :  printf("Madras  ");
                  break;
    }
    for( j = 1 ; j <= 4 ; j++ )
        printf("%7d", frequency[i][j] );
    printf("\n");
}
printf("----------------------------------------\n");
/* . . . . . . . . PRINTING ENDS. . . . . . . . . */
}
```

### Output

```
For each person, enter the city code
followed by the car code.
Enter the letter X to indicate end.
M 1 C 2 B 1 D 3 M 2 B 4
C 1 D 3 M 4 B 2 D 1 C 3
D 4 D 4 M 1 M 1 B 3 B 3
C 1 C 1 C 2 M 4 M 4 C 2
D 1 C 2 B 3 M 1 B 1 C 2
D 3 M 4 C 1 D 2 M 3 B 4    X
```

**POPULARITY TABLE**

| City | Ambassador | Fiat | Dolphin | Maruti |
|---|---:|---:|---:|---:|
| Bombay | 2 | 1 | 3 | 2 |
| Calcutta | 4 | 5 | 1 | 0 |
| Delhi | 2 | 1 | 3 | 2 |
| Madras | 4 | 1 | 1 | 4 |

**Fig. 9.7** *Program to tabulate a survey data*
