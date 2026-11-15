# Transpose

The **transpose** of a matrix is a new matrix in which the rows of the original matrix are the columns of the new matrix. We use a superscript $T$ after a matrix name to refer to the transpose. For example, consider the following matrix and its transpose:

![](bbox=[0.36, 0.175, 0.8, 0.255])

If we consider a couple of the elements, we see that the value in position (3, 1) has now moved to position (1, 3) and that the value in position (4, 2) has now moved to position (2, 4). In fact, we have interchanged the row and column subscript so that we are moving the value in position $(i, j)$ to position $(j, i)$. Also, note that the size of the transpose is different than the size of the original matrix (unless the original matrix is a square matrix).

We now develop a function that generates the transpose of a matrix. The formal arguments of the function must include two-dimensional arrays that represent the original matrix and the matrix that is to contain the transpose of the original matrix. To allow some flexibility with this function, we assume that we have defined symbolic constants that specify the number of rows and the number of columns in the original matrix. These symbolic constants are NROWS and NCOLS. Because using a symbolic constant is equivalent to using the value it has been given, we can then use NROWS and NCOLS in the array definition and in the prototype statement. Note that the function does not return a value; hence, the return type is void. Also note that the symbolic constants NROWS and NCOLS must be defined in a program that uses this function:

```
```c
/*-------------------------------------------------------------*/
/* This function generates a matrix transpose. NROWS and */
/* NCOLS are symbolic constants that must be declared */
/* in the calling program. */
/*-------------------------------------------------------------*/
void transpose(int b[NROWS][NCOLS], int bt[NCOLS][NROWS])
{
    /* Declare variables. */
    int i, j;

    /* Transfer values to the transpose matrix. */
    for (i= 0; i<NROWS-1; i++)
    for (j=0; j<=NCOLS-1; j++)
    bt[j][i] = b[i][j];

    /* Void return. */
    return;
}
/*-------------------------------------------------------------*/
```
```