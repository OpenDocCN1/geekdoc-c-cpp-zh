Similarly, we can compute the rest of the elements in the product of A and B:

AB = C = \(\begin{bmatrix} 2 & 22 & -5 \\ -8 & 10 & -7 \end{bmatrix}\)

In this example, we cannot compute BA, because B does not have the same number of elements in each row as A has in each column.

An easy way to decide if a matrix product exists is to write the sizes of the two matrices side by side. If the two inside numbers are the same, the product exists; the two outside numbers determine the size of the product. To illustrate, in the previous example, the size of A is 2 x 3, and the size of B is 3 x 3. Therefore, if we want to compute AB, we write the sizes side by side:

![](bbox=[0.48, 0.28, 0.65, 0.32])

The two inner numbers are both the value 3, so AB exists, and its size is determined by the two outer numbers, 2 x 3. If we want to compute BA, we again write the sizes side by side:

![](bbox=[0.48, 0.4, 0.65, 0.44])

The two inner numbers are not the same, so BA does not exist.

We now present a function to compute the product C = AB. In this function, the arrays are each of size N x N, where N is a symbolic constant:

```
/*-----------------------------------------------*/
/* This function performs a matrix multiplication of   */
/* NxN matrices using sums of products. N is a symbolic */
/* constant that must be defined in the calling program. */
/*-----------------------------------------------*/
void matrix_mult(int a[N][N], int b[N][N], int c[N][N])
{
    /* Declare variables. */
    int i, j, k;

    /* Compute sums of products. */
    for (i=0; i<=N-1; i++)
        for (j=0; j<=N-1; j++)
        {
            c[i][j] = 0;
            for (k=0; k<=N-1; k++)
                c[i][j] += a[i][k]*b[k][j];
        }

    /* Void return. */
    return;
}
/*-----------------------------------------------*/
```