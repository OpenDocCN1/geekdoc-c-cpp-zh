```
for(i=0; i<r; i++)
{
    printf("\n");
    for(j=0; j<c; j++)
        printf("%5d", mat[i][j]);
}
}
Output
Enter the number of rows and columns of the matrix: 2
0       1
-1      0
```

# 3.12 POINTERS AND TWO-DIMENSIONAL ARRAYS

Consider a two-dimensional array declared as

```
int mat[5][5];
```

To declare a pointer to a two-dimensional array, you may write

```
int (*ptr)[5];
```

Here int **ptr is an array of pointers (to one-dimensional arrays), while int mat[5][5] is a 2D array. They are not the same type and are not interchangeable.

Individual elements of the array mat can be accessed using either:

+   - mat[i][j]
+   - *(*(mat + i) + j) or
+   - *(mat[i]+j);

To understand more fully the concept of pointers, let us replace

```
*(multi + row with x so the expression
*(*(mat + i) + j) becomes *(X + col)
```

Using arithmetic, we know that the address pointed to by (i.e., value of) x + col + 1 must be greater than the address x + col by an amount equal to sizeof(int).

Since mat is a two-dimensional array, we know that in the expression multi + row as used above, multi + row + 1 must increase in value by an amount equal to that needed to point to the next row, which in this case would be an amount equal to cols * sizeof(int).

Thus, in case of a two-dimensional array, in order to evaluate expression (for a row major 2D array), we must know a total of 4 values:

+   1. The address of the first element of the array, which is given by the name of the array, i.e., mat in our case.
+   2. The size of the type of the elements of the array, i.e., size of integers in our case.
+   3. The specific index value for the row.
+   4. The specific index value for the column.

Note that

```
int (*ptr)[10];
```

declares ptr to be a pointer to an array of 10 integers. This is different from

```
int *ptr[10];
```

which would make ptr the name of an array of 10 pointers to type int. You must be thinking how pointer arithmetic works if you have an array of pointers. For example:

```
int * arr[10] ;
int ** ptr = arr ;
```