

/* Determine index value. */
if (done == 1)
    index = mid;
/* Return index value. */
return index;
}
/*------------------------------------------*/

## 修改！

- 1. Modify either of the sequential search functions to search an array of characters. Write a driver to test your function.
- 2. Modify the sequential search on an ordered list to return a count of the number of times a specified value occurred in an ordered list.
- 3. Modify the binary search function so that it correctly searches a list that is in descending order instead of ascending order. Write a driver to test your function.

## 5.8 Two-Dimensional Arrays

A set of data values that is visualized as a row or column is easily represented by a one-dimensional array. However, there are many examples in which the best way to visualize a set of data is with a grid or a table of data, which has both rows and columns. An array with four rows and three columns is shown in the following diagram:

![](img/02c4582f051c5b51776411c92b079035_270_0.png)

In C, a grid or table of data is represented with a two-dimensional array. Each element in a two-dimensional array is referenced using an identifier followed by two subscripts—a row subscript and a column subscript. The subscript values for both rows and columns begin with 0, and each subscript has its own set of brackets. Thus, assuming that the previous array has an identifier x, the value in position x[2][1] is 6. Common errors in array references include using parentheses instead of brackets, as in X(2)(3), or using only one set of brackets or parentheses, as in X[2,3] or X(2,3).

![](img/02c4582f051c5b51776411c92b079035_270_1.png)

We can also visualize this grid or table of data as a one-dimensional array, where each element is also an array. Thus, the array in the previous diagram can be interpreted as a one-dimensional array with four elements, each of which is a one-dimensional array with three elements:

![](img/02c4582f051c5b51776411c92b079035_271_0.png)

By using this representation, the notation x[2][1] can be interpreted as referring to position [1] within the one-dimensional array represented by x[2]; thus, the value of x[2][1] is 6. In general, we prefer to discuss two-dimensional arrays in terms of a grid with rows and columns, as opposed to an array of arrays.

All values in an array must have the same type. An array cannot have a column of integers followed by a column of floating-point numbers, and so on.

## Definition and Initialization

To define a two-dimensional array, we specify the number of rows and the number of columns in the declaration statement. The row number is written first. Both the row number and the column number are in brackets, as shown in this statement:

```
int x[4][3];
```

A two-dimensional array can be initialized with a declaration statement. The values are specified in a sequence separated by commas, and each row is contained in braces. An additional set of braces is included around the complete set of values, as shown in the following statement:

```
int x[4][3]={{2, 3, -1}, {0, -3, 5}, {2, 6, 3}, {-2, 10, 4}};
```

If the initializing sequence is shorter than the array, then the rest of the values are initialized to zero. If the array is specified with the first subscript empty, but with an initialization sequence, the size is determined by the sequence. Thus, the array x can also be defined with the following statement:

```
int x[][3]={{2, 3, -1}, {0, -3, 5}, {2, 6, 3}, {-2, 10, 4}};
```

Arrays can also be initialized with program statements. For two-dimensional arrays, two nested for loops are usually required to initialize an array; i and j are commonly used as subscripts. To define and initialize an array such that each row contains the row number, use the following statements:

```
/* Declare variables. */
int i, j, t[5][4];
...
/* Initialize array. */
for (i=0; i<4; i++)
    for (j=0; j<3; j++)
        t[i][j] = i;
```

After these statements are executed, the values in the array t are as follows:

| 0 | 0 | 0 | 0 |
|---|---|---|---|
| 1 | 1 | 1 | 1 |
| 2 | 2 | 2 | 2 |
| 3 | 3 | 3 | 3 |
| 4 | 4 | 4 | 4 |

Two-dimensional arrays can also be initialized with values read from a data file. In the next set of statements, we assume that a data file contains 50 temperature values that we read and store in the array. Symbolic constants NROWS and NCOLS are used to represent the number of rows and columns. Changing the size of an array is easier to do when the numbers of rows and columns are specified as symbolic constants; otherwise, the change requires modifications to several statements. Here are the statements.

```
#define NROWS 10
#define NCOLS 5
#define FILENAME "engine1.txt"
...
/* Declare variables. */
int i, j;
double temps[NROWS][NCOLS];
FILE *sensor;
...
/* Open file and read data into array. */
sensor = fopen(FILENAME,"r");
for (i=0; i<NROWS-1; i++)
    for (j=0; j<NCOLS-1; j++)
        fscanf(sensor,"%lf",&temps[i][j]);
```

## PRACTICE!

Show the contents of the arrays defined in each set of statements. Use a question mark to indicate an element that has not been initialized.

- 1. int d[3][1]={{1}, {4}, {6}};
- 2. int g[6][2]={{5,2}, {-2,3}};
- 3. float h[4][4]={{0,0}};
- 4. int k, p[3][3]={{0,0,0}};
   ...
   for (k=0; k<2; k++)
       p[k][k] = 1;
- 5. int i, j, g[5][5];
   ...
   for (i=0; i<4; i++)
       for (j=0; j<4; j++)
           g[i][j] = i + j;
- 6. int i, j, g[5][5];
   ...
   for (i=0; i<4; i++)
       for (j=0; j<4; j++)
           g[i][j] = pow(-1,i+j);

## Computations and Output

Computations and output with two-dimensional arrays must always specify two subscripts when referencing an array element. To illustrate, consider a program that reads a data file containing power output for an electrical plant for an 8-week period. Each line of the data file contains seven values representing the daily power output for a week. The data are stored in a two-dimensional array. Then a report provides the average power for the first day of the week during the period, the average power for the second day of the week during the period, and so on. Here is the program:

```
/*---------------------------------------------*/
/* Program chapter5_6 */
/* */
/* This program computes power averages over ten weeks. */
/* */
#include <stdio.h>
#define NROWS 8
#define NCOLS 7
#define FILENAME "power1.txt"
int main(void)
{
    /* Declare variables. */
    int i, j;
    int power[NROWS][NCOLS], col_sum;
    FILE *file_in;

/* Read information from a data file. */
file_in = fopen(FILENAME,"r");
if (file_in == NULL)
printf("Error opening input file. \n");
else
{
for (i=0; i<=NROWS-1; i++)
for (j=0; j<NCOLS-1; j++)
fscanf(file_in,"%d",&power[i][j]);
/* Compute and print daily averages. */
for (j=0; j<=NCOLS-1; j++)
{
col_sum = 0;
for (i=0; i<=NROWS-1; i++)
col_sum += power[i][j];
printf("Day %d Average: %.2f \n",
j+1,(double)col_sum/NROWS)
}
/* Close file. */
fclose(file_in);
}
/* Exit program. */
return 0;
}/*--------------------------------------------------------------*/
```

Note that the daily averages are computed by adding each column and then dividing the column sum by the number of rows (which is also the number of weeks). The column number is then used to compute the day number. A sample output from this program is as follows:

```
Day 1: Average = 253.75
Day 2: Average = 191.50
Day 3: Average = 278.38
Day 4: Average = 188.63
Day 5: Average = 273.13
Day 6: Average = 321.38
Day 7: Average = 282.50
```

Writing information from a two-dimensional array to a data file is similar to writing information from a one-dimensional array. In both cases, a newline indicator must be used to specify when the values are to begin a new line. To write a set of distance measurements to a data file named dist1.txt with five values per line, use the following statements:

```
/* Declare variables. */
int i, j;
double dist[20][5];
```

