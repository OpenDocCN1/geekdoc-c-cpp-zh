# Listing 2.15 Functions for Dynamic Allocation of Vectors and Matrices (memalloc.h Partial)

```
//----------------------------------------- memalloc.h -----------------------------------------
// Functions for dynamic memory allocation of vectors and matrices
//-----------------------------------------------------------------------------------------------
#ifndef _MEMALLOC_
#define _MEMALLOC_

#include <stdlib.h>
#include <stdio.h>
#include <complex>

using namespace std;
typedef complex<double> dcmplx;

double *Vector(int imin, int imax)
// Allocates a double vector with indices in the range [imin,imax]
...
void FreeVector(double *p, int imin)
// Deallocates a double vector allocated with Vector, with offset imin
...
double **Matrix(int imin, int imax, int jmin, int jmax)
// Allocates a double matrix, with row and column indices in the range
// [imin,imax] x [jmin,jmax]
...
void FreeMatrix(double **p, int imin, int jmin)
// Deallocates a double matrix allocated with Matrix, with row and column
// offsets imin and jmin
...
int *IVector(int imin, int imax)
// Allocates an int vector with indices in the range [imin,imax]
...
void FreeIVector(int *p, int imin)
// Deallocates an int vector allocated with IVector, with offset imin
...
int **IMatrix(int imin, int imax, int jmin, int jmax)
// Allocates an int matrix, with row and column indices in the range
// [imin,imax] x [jmin,jmax]
...
void FreeIMatrix(int **p, int imin, int jmin)
// Deallocates an int matrix allocated with IMatrix, with row and column
// offsets imin and jmin
...
dcmplx *CVector(int imin, int imax)
// Allocates a complex vector with indices in the range [imin,imax]
...
void FreeCVector(dcmplx *p, int imin)
// Deallocates a complex vector allocated with CVector, with offset imin
...
dcmplx **CMatrix(int imin, int imax, int jmin, int jmax)
// Allocates a complex matrix, with row and column indices in the range
// [imin,imax] x [jmin,jmax]
...
void FreeCMatrix(dcmplx **p, int imin, int jmin)
// Deallocates a complex matrix allocated with CMatrix, with row and column
// offsets imin and jmin
...
#endif
```