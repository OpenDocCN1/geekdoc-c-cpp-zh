```
//--------------------------------------------------------------------------------
{
    free((void*) (p+imin));                // compensate for offset
}

//================================================================================
int **IMatrix(int imin, int imax, int jmin, int jmax)
//--------------------------------------------------------------------------------
// Allocates an int matrix, with row and column indices in the range
// [imin,imax] x [jmin,jmax]
//--------------------------------------------------------------------------------
{
    int i, ni = imax-imin+1, nj = jmax-jmin+1;  // numbers of rows and columns
    int **p;
                                        // allocate array of row pointers
    p = (int**) malloc((size_t) (ni*sizeof(int*)));
    if (!p) {
        printf("Matrix: level 1 allocation error !\n");
        exit(1);
    }
    p -= imin;                              // adjust for row offset
                                        // assign block start to 1st row pointer
    p[imin] = (int*) malloc((size_t) (ni*nj*sizeof(int)));
    if (!p[imin]) {
        printf("Matrix: level 2 allocation error !\n");
        exit(2);
    }
    p[imin] -= jmin;                        // adjust 1st row pointer for column offset
                                        // define row pointers spaced by row length
    for (i=imin+1; i<=imax; i++) p[i] = p[i-1] + nj;
    return p;
}

//================================================================================
void FreeIMatrix(int **p, int imin, int jmin)
//--------------------------------------------------------------------------------
// Deallocates an int matrix allocated with IMatrix, with row and column
// offsets imin and jmin
//--------------------------------------------------------------------------------
{
    free((void*) (p[imin]+jmin));           // deallocate block
    free((void*) (p+imin));                 // deallocate array of row pointers
}

//================================================================================
dcmplx *CVector(int imin, int imax)
//--------------------------------------------------------------------------------
// Allocates a complex vector with indices in the range [imin,imax]
//--------------------------------------------------------------------------------
{
    dcmplx *p;
                                        // assign block start to array pointer
    p = (dcmplx*) malloc((size_t) ((imax-imin+1)*2*sizeof(double)));
    if (!p) {
        printf("CVector: allocation error !\n");
        exit(1);
    }
    return p - imin;                        // adjust for offset
}
```