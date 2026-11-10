
## 10.13 count_numbers.c: USING A 2D ARRAY AS A COUNTER

Program 10.12 uses a 2D array to implement a frequency counter. The program accepts a set of integers as user input and sequentially assigns them to the first row of the array arr, but only after checking that the number doesn’t already exist there. The corresponding column of the next row maintains a count for the number. For instance, the first number is assigned to arr[0][0] and its count is saved in arr[1][0].

```c
/* count_numbers.c: Uses a 2D array as a frequency counter.
   First row stores number, second row stores frequency. */
#include <stdio.h>
int main(void)
{
    short i, imax = 0, tmp;
    short arr[2][50] = {{0}};        /* All array elements initialized */
    char is_found;

    printf("Key in some integers (q to quit): ");
    while (scanf("%hd", &tmp) == 1) {
        is_found = 'n';
        for (i = 0; i < imax; i++) {      /* Check whether number exists */
            if (arr[0][i] == tmp) {        /* If number found in array ... */
                arr[1][i]++;               /* ... then increment its count */
                is_found = 'y';
                break;                     /* Abandon further checking */
            }
        }
        if (is_found == 'n') {             /* If number not found in array ... */
            arr[0][i] = tmp;               /* ... add number to array ... */
            arr[1][i] = 1;                 /* ... and set its count to 1 */
            imax++;                        /* Increase limit of search */
        }
    }
    /* Print array contents in pairs */
    for (i = 0; i < imax; i++)
        printf("%5hd = %2hd\n", arr[0][i], arr[1][i]);
    return 0;
}
```

```
Key in some integers (q to quit): 11 33 22 -1 0 33 666 33 22 0 33 q
  11 =  1
  33 =  4
  22 =  2
  -1 =  1
   0 =  2
 666 =  1
```

PROGRAM 10.12: **count_numbers.c**

PROGRAM OUTPUT: **count_numbers.c**

Each number that is input is sequentially looked up in the first row of the array. This is how the program responds to the result of the search:

- If the number is found in that row, then its corresponding column in the second row is incremented (`arr[1][i]++`). The `for` loop is then terminated with **break** for the next number to be keyed in.
- If the number doesn’t exist in the first row, it is assigned to the next free element of that row. The count in the corresponding column of the second row is set to 1. The variable, `imax`, is then incremented for use by the next number to be added.

After all numbers have been input, the expression `imax - 1` evaluates to the number of elements used by the first row of `arr`. The last **for** loop uses this value to print the key-value pairs of only those array elements that have been utilized.

Note that even though the highest number input was 666, only 12 elements of the array were used. Program 10.10 (which used the number itself as the array index) would have needed an array of 666 elements. That program will still fail here because it can’t handle negative numbers, which this program does with ease.

## 10.14 MULTI-DIMENSIONAL ARRAYS

Multi-dimensional arrays in C can go beyond two dimensions. Every increase in dimension increases the number of subscripts by one, with the subscript on the right changing faster than the one on the left. A three-dimensional (3D) array can be treated as an array of arrays of arrays. In this case, only those elements accessed with the right-most subscript—with the other subscripts remaining unchanged—occupy consecutive memory cells.

While the principles of memory allocation and initialization remain unchanged for multi-dimensional arrays, visualization of an array becomes difficult when the number of dimensions exceeds three. A 3D array is declared in this manner:

```c
int max_temp[YEARS][MONTHS][DAYS];
```

This array can store the maximum daily temperature, grouped by month, for multiple years. Three loops are needed to initialize the elements:

```c
for (i = 0; i < YEARS; i++)
    for (j = 0; j < MONTHS; j++)
        for (k = 0; k < DAYS; k++)
            max_temp[i][j][k] = 0;
```

> *If all values are 0, simply …*
> *… initialize one element to 0*

The symbolic constants representing the subscripts, MONTHS and DAYS, would have the values 12 and 31, respectively. The month changes after every 31 elements, while the year changes after 31 × 12 elements. Because all months don’t have 31 days, special logic has to be built into a program to skip those elements that point to invalid days.

## 10.15 USING ARRAYS AS MATRICES

In mathematics, you would have encountered the *matrix* as a rectangular array of numbers or expressions. A matrix is represented by a name, say, A, having the dimensions *m × n*. Each element of the matrix is represented by the notation, say, aᵢ,ⱼ, where the subscripts *i* and *j* cannot exceed *m* and *n* respectively. This is how a 3 × 4 matrix named A is represented in mathematics:

$$A = \begin{bmatrix} a_{1,1} & a_{1,2} & a_{1,3} & a_{1,4} \\ a_{2,1} & a_{2,2} & a_{2,3} & a_{2,4} \\ a_{3,1} & a_{3,2} & a_{3,3} & a_{3,4} \end{bmatrix}$$

A two-dimensional array can easily implement a matrix except that the array index starts from 0 and not 1. Thus, the matrix element a₁,₁ is the same as the array element a[0][0]. In the general case, aₘ,ₙ is equivalent to a[m - 1][n - 1]. We’ll now examine three programs that use 2D arrays to implement the most commonly performed operations on matrices.

### 10.15.1 `matrix_transpose.c`: Transposing a Matrix

A matrix is *transposed* by swapping its rows and columns. Thus, the first row becomes the first column; the last row becomes the last column. Program 10.13 transposes the matrix represented by the 2D array, mat1, and saves the output in the array, mat2.

```c
/* matrix_transpose.c: Transposes a matrix;
   converts rows to columns and vice versa. */
#include <stdio.h>
#define COLUMNS 3
#define ROWS 3
int main(void)
{
    short mat1[ROWS][COLUMNS] = {{1, 2, 3},
                                 {4, 5, 6},
                                 {7, 8, 9}};
    short mat2[ROWS][COLUMNS];
    short i, j;
    for (i = 0; i < ROWS; i++)
        for (j = 0; j < COLUMNS; j++)
            mat2[i][j] = mat1[j][i];
    printf("Transposed matrix:\n");
    for (i = 0; i < ROWS; i++) {
        putchar('\n');
        for (j = 0; j < COLUMNS; j++)
            printf("%4hd", mat2[i][j]);
    }
    return 0;
}
```

PROGRAM 10.13: **matrix_transpose.c**

```
Enter 1 for addition or 2 for subtraction: 3
Illegal choice
Enter 1 for addition or 2 for subtraction: 1
Matrix after addition:
  13  13  13  13
  13  13  13  13
  13  13  13  13
Enter 1 for addition or 2 for subtraction: 2
Matrix after subtraction:
 -11  -9  -7  -5
  -3  -1   1   3
   5   7   9  11
```

PROGRAM OUTPUT: `matrix_add_subtract.c`

### 10.15.3 `matrix_multiply.c`: Multiplying Two Matrices

Matrix multiplication is not as straightforward as addition and subtraction. An *m × n* matrix can only be multiplied with an *n × p* matrix, which means that the number of columns of the first matrix must equal the number of rows of the second matrix. The resultant matrix has the dimensions *m × p*.

Matrix multiplication is performed by using the *dot-product* technique. The dot-product of two sets of numbers containing the same number of elements is the sum of the products of the corresponding elements. For matrices, the dot-product applies to the row elements of the first matrix and the column elements of the second matrix (Fig. 10.3).

| Matrix 1 | Matrix 2 | Matrix 3 |
|---|---|---|
| 1  2<br>3  4<br>5  6 | 6  5  4<br>3  2  1 | 12  9  6<br>30  23  16<br>48  37  26 |

**FIGURE 10.3**  Multiplying Two Matrices

The data for the matrices are obtained from the output of Program 10.15. The first element of matrix 3 (12) is evaluated by computing the dot-product of the first row of matrix 1 and the first column of matrix 2. For the second element (9), the dot-product is applied to the same row of matrix 1 and the second column of matrix 2. Thus, the first row of matrix 3 is evaluated in the following manner:

```
1 × 6 + 2 × 3 = 12    (mat3[0][0])
1 × 5 + 2 × 2 =  9    (mat3[0][1])
1 × 4 + 2 × 1 =  6    (mat3[0][2])
```

The second and third rows of matrix 3 are computed in a similar manner. Program 10.15 performs this dot-product evaluation where the matrix values are supplied by user input. The program also performs a compatibility test of the two matrices.
