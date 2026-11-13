
```c
{
    res[i][j] = 0;
    for (k = 0; k < kres_cols; k++)
        res[i][j] += mat1[i][k] * mat2[k][j];
}
printf("\n The elements of the product matrix are ");
for (i = 0; i < kres_rows; i++)
{
    printf("\n");
    for (j = 0; j < kres_cols; j++)
        printf("\t %d", res[i][j]);
}
return 0;
}
```

Output
Enter the number of rows in the first matrix: 2
Enter the number of columns in the first matrix: 2
Enter the number of rows in the second matrix: 2
Enter the number of columns in the second matrix: 2
Enter the elements of the first matrix
1 2 3 4
Enter the elements of the second matrix
5 6 7 8
The elements of the product matrix are
19 22
43 50

## 3.11 PASSING TWO-DIMENSIONAL ARRAYS TO FUNCTIONS

There are three ways of passing a two-dimensional array to a function. First, we can pass individual elements of the array. This is exactly the same as passing an element of a one-dimensional array. Second, we can pass a single row of the two-dimensional array. This is equivalent to passing the entire one-dimensional array to a function that has already been discussed in a previous section. Third, we can pass the entire two-dimensional array to the function. Figure 3.31 shows the three ways of using two-dimensional arrays for inter-function communication.

![](img/be6359df08208122bec6fad1103de211_116_0.png)

Figure 3.31 2D arrays for inter-function communication

## Passing a Row

A row of a two-dimensional array can be passed by indexing the array name with the row number. Look at Fig. 3.32 which illustrates how a single row of a two-dimensional array can be passed to the called function.

| Calling function | Called function |
|---|---|
| main() | void func(int arr[]) |
| { | { |
| int arr[2][3] = ((1, 2, 3), (4, 5, 6)); | int i; |
| func(arr[1]); | for(i=0;i<3;i++) |
| } | printf("%d", arr[1][i] * 10); |
| | } |

Figure 3.32 Passing a row of a 2D array to a function

## Passing the Entire 2D Array

To pass a two-dimensional array to a function, we use the array name as the actual parameter (the way we did in case of a 1D array). However, the parameter in the called function must indicate that the array has two dimensions. Look at the following program which passes entire 2D array to a function.

## PROGRAMMING EXAMPLE

24. Write a program to fill a square matrix with value zero on the diagonals, 1 on the upper right triangle, and –1 on the lower left triangle.

```c
#include <stdio.h>
#include <conio.h>
void read_matrix(int mat[5][5], int);
void display_matrix(int mat[5][5], int);
main()
{
    int row;
    int mat[5][5];
    clrscr();
    printf("\n Enter the number of rows and columns of the matrix:");
    scanf("%d", &row);
    read_matrix(mat, row);
    display_matrix(mat, row);
    getch();
    return 0;
}
void read_matrix(int mat[5][5], int r)
{
    int i, j;
    for (i = 0; i < r; i++)
    {
        for (j = 0; j < r; j++)
        {
            if (i == j)
                mat[i][j] = 0;
            else if (i > j)
                mat[i][j] = -1;
            else
                mat[i][j] = 1;
        }
    }
}
void display_matrix(int mat[5][5], int r)
{
    int i, j;
    for (i = 0; i < r; i++)
    {
        printf("\n");
        for (j = 0; j < r; j++)
            printf("%5d", mat[i][j]);
    }
}
```

Output
Enter the number of rows and columns of the matrix: 2
0       1
-1      0

## 3.12 POINTERS AND TWO-DIMENSIONAL ARRAYS

Consider a two-dimensional array declared as

```c
int mat[5][5];
```

To declare a pointer to a two-dimensional array, you may write

```c
int (*ptr)[5];
```

Here int **ptr is an array of pointers (to one-dimensional arrays), while int mat[5][5] is a 2D array. They are not the same type and are not interchangeable.

Individual elements of the array mat can be accessed using either:

- mat[i][j]
- *(*(mat + i) + j) or
- *(mat[i] + j);

To understand more fully the concept of pointers, let us replace

```c
*(mat + row with x so the expression
*(*(mat + i) + j) becomes *(x + col)
```

Using arithmetic, we know that the address pointed to by (i.e., value of) x + col + 1 must be greater than the address x + col by an amount equal to sizeof(int).

Since mat is a two-dimensional array, we know that in the expression mat + row as used above, mat + row + 1 must increase in value by an amount equal to that needed to point to the next row, which in this case would be an amount equal to cols * sizeof(int).

Thus, in case of a two-dimensional array, in order to evaluate expression (for a row major 2D array), we must know a total of 4 values:

- 1. The address of the first element of the array, which is given by the name of the array, i.e., mat in our case.
- 2. The size of the type of the elements of the array, i.e., size of integers in our case.
- 3. The specific index value for the row.
- 4. The specific index value for the column.

Note that

```c
int (*ptr)[10];
```

declares ptr to be a pointer to an array of 10 integers. This is different from

```c
int *ptr[10];
```

which would make ptr the name of an array of 10 pointers to type int. You must be thinking how pointer arithmetic works if you have an array of pointers. For example:

```c
int *arr[10];
int **ptr = arr;
```

In this case, arr has type int **. Since all pointers have the same size, the address of ptr + i can be calculated as:

```c
addr(ptr + i) = addr(ptr) + [sizeof(int *) * 1]
= addr(ptr) + [2 * 1]
```

Since arr has type int **,

```
arr[0] = &arr[0][0],
arr[1] = &arr[1][0], and in general,
arr[i] = &arr[i][0].
```

According to pointer arithmetic, arr + i = &arr[1], yet this skips an entire row of 5 elements, i.e., it skips complete 10 bytes (5 elements each of 2 bytes size). Therefore, if arr is address 1000, then arr + 2 is address 1010. To summarize, &arr[0][0], arr[0], arr, and &arr[0] point to the base address.

```
&arr[0][0] + 1 points to arr[0][1]
arr[0] + 1 points to arr[0][1]
arr + 1 points to arr[1][0]
&arr[0] + 1 points to arr[1][0]
```

To conclude, a two-dimensional array is not the same as an array of pointers to 1D arrays. Actually a two-dimensional array is declared as:

```c
int (*ptr)[10];
```

Here ptr is a pointer to an array of 10 elements. The parentheses are not optional. In the absence of these parentheses, ptr becomes an array of 10 pointers, not a pointer to an array of 10 ints.

Look at the code given below which illustrates the use of a pointer to a two-dimensional array.

```c
#include <stdio.h>
int main()
{
    int arr[2][2] = {{1, 2}, {3, 4}};
    int i, j, (*ptr)[2];
    ptr = arr;
    for (i = 0; i < 2; i++)
    {
        for (j = 0; j < 2; j++)
            printf("%d", (*(ptr + i))[j]);
    }
    return 0;
}
```

# Output

1 2 3 4

The golden rule to access an element of a two-dimensional array can be given as

```c
arr[i][j] = *(*(arr + i))[j] = *(*(arr + i) + j) = *(arr[i] + j)
```

Therefore,

```
arr[0][0] = *(arr[0] = *(*(arr + 0) = *(arr[0] + 0)
arr[1][2] = *(*(arr + 1))[2] = *(*(arr + 1) + 2) = *(arr[1] + 2)
```

| If we declare an array of pointers using, | If we declare a pointer to an array using, |
|---|---|
| `data_type array_name[SIZE];` | `data_type (*array_name)[SIZE];` |
| Here SIZE represents the number of rows and the space for columns that can be dynamically allocated. | Here SIZE represents the number of columns and the space for rows that may be dynamically allocated (refer Appendix A to see how memory is dynamically allocated). |

## PROGRAMMING EXAMPLE

## 25. Write a program to read and display a 3 x 3 matrix.

```c
#include <stdio.h>
#include <conio.h>
void display(int (*)[3]);
int main()
{
    int i, j, mat[3][3];
    clrscr();
    printf("\n Enter the elements of the matrix");
    for (i = 0; i < 3; i++)
    {
        for (j = 0; j < 3; j++)
        {
            scanf("%d", &mat[i][j]);
        }
    }
    display(mat);
    return 0;
}
void display(int (*mat)[3])
{
    int i, j;
    printf("\n The elements of the matrix are");
    for (i = 0; i < 3; i++)
    {
        for (j = 0; j < 3; j++)
            printf("\t %d", *(*(mat + i) + j));
    }
}
```

**Output**
Enter the elements of the matrix
1 2 3 4 5 6 7 8 9
The elements of the matrix are
1 2 3
4 5 6
7 8 9

> **Note** A double pointer cannot be used as a 2D array. Therefore, it is wrong to declare: 'int *mat' and then use 'mat' as a 2D array. These are two very different data types used to access different locations in memory. So running such a code may abort the program with a 'memory access violation' error.
> A 2D array is not equivalent to a double pointer. A 'pointer to pointer of T' cannot serve as a '2D array of T'. The 2D array is equivalent to a pointer to row of T, and this is very different from pointer to pointer of T.
> When a double pointer that points to the first element of an array is used with the subscript notation ptr[0][0], it is fully dereferenced two times and the resulting object will have an address equal to the value of the first element of the array

## 3.13 MULTI-DIMENSIONAL ARRAYS

A multi-dimensional array in simple terms is an array of arrays. As we have one index in a one-dimensional array, two indices in a two-dimensional array, in the same way, we have n indices in an n-dimensional array or multi-dimensional array. Conversely, a n-dimensional array is specified
