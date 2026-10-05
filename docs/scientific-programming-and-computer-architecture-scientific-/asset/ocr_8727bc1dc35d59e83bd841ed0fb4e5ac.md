# 4.2. Optimizing memory access

On lines 8 and 12, the arrays b[] and a[] are initialized with random numbers. Initializing with simple numbers such as 0 or 1 gives timing numbers that are leading and not reproducible.

The mult4x20012() function is called $10^7$ times on line 15. The function calls cycle through the 150 formats for the first argument so that the function has to load a[] and c[] from L2 or L3 cache after each call. This pattern of function calls imitates the manner in which the function is called in the next stage.

$600 \times 200 \times 12$

The mult600x20012() function requires scratch space of $600 \times 12$ to store c[], which is unpacked to the array C[] in column-major format with the right leading dimension.

```
void mult600x20012(double *a, double *b,
               double *C, int ldC,
               double *scratch){
    double *c = scratch;
    for(int i=0; i < 7200; i++)
        c[i] = 0;
    for(int i=0; i < 150; i++)
        mult4x20012(a*i*800, b, c+i*48);
    unpackC(c, C, ldC);
}
```

The array[] stores a $600 \times 200$ matrix. The $600 \times 200$ matrix is thought of as 150 matrices of dimension $4 \times 12$ one below the other. These 150 submatrices must be lined up in a[], with each submatrix stored in the column-major format required by mult4x20012().

The array c[] stores a $600 \times 12$ matrix. The $600 \times 12$ matrix is thought of as 150 matrices of dimension $4 \times 12$ one below the other, and these submatrices are lined up in c[] with each submatrix in the format required by mult4x20012().

The function mult600x20012() makes 150 calls to mult4x200x12(). At the end it unpacks c[]. The function unpackC() listed below converts c[] to the column-major format of C.

```
void unpackC(double *c, double *C, int ldC){
```