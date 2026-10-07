
# 698 Performance, Reliability, and Availability Evaluation of Computational Systems

Modified:

06 June 2005

Author:

John Burkardt

```
Parameters:

Output, double CPU_TIME, the current reading of
the CPU clock, in seconds.
*/
double value;

value = ( double ) clock ( )
/ ( double ) CLOCKS_PER_SEC;

return value;
}
```

```c
****************************************************************
void daxpy ( int n, double da, double dx[], int incx,
double dy[], int inc )
```

****************************************************************
Purpose:

DAXPY computes constant times a vector plus a vector.

Discussion:

This routine uses unrolled loops for increments equal
to one.

Modified:

30 March 2007

Author:

FORTRAN77 original by Jack Dongarra, Cleve Moler,
Jim Bunch, Pete Stewart.
C version by John Burkardt

Reference:

Jack Dongarra, Cleve Moler, Jim Bunch, Pete Stewart,
# Linpack_Bench

LINPACK User's Guide,
SIAM, 1979.

Charles Lawson, Richard Hanson, David Kincaid, Fred Krogh,
Basic Linear Algebra Subprograms for Fortran Usage,
Algorithm 539,
ACM Transactions on Mathematical Software,
Volume 5, Number 3, September 1979, pages 308–323.

Parameters:

Input, N, the number of elements in DX and DY.

Input, double DA, the multiplier of DX.

Input, double DX[*], the first vector.

Input, int INCX, the increment between successive entries
of DX.

Input/output, double DX[*], the second vector.
On output, DY[*] has been replaced by DY[*] + DA * DX[*].

Input, int INCY, the increment between successive entries
of DY.

```c

/*
int i;
int ix;
int iy;
int m;

if ( n <= 0 )
{
  return;
}

if ( da == 0.0 )
{
  return;
}
/*
Code for unequal increments or equal increments
not equal to 1.
*/
if ( incx != 1 || incy != 1 )
{
  if ( 0 <= incx )
{
    ix = 0;
}
```

# 700 Performance, Reliability, and Availability Evaluation of Computational Systems

```c
else
{
ix = ( - n + 1 ) * incx;
}
if ( 0 <= incy )
{
iy = 0;
}
else
{
y = ( - n + 1 ) * incy;
}
for ( i = 0; i < n; i++ )
{
dy[i] = dy[i] + da * dx[ix];
ix = ix + incx;
yi = iy + incy;
}
/*
Code for both increments equal to 1.
*/
else
{
m = n % 4;
}
for ( i = 0; i < m; i++ )
{
dy[i] = dy[i] + da * dx[i];
}
for ( i = m; i < n; i = i + 4 )
{
dy[i] = dy[i] + da * dx[i];
dy[i+1] = dy[i+1] + da * dx[i+1];
dy[i+2] = dy[i+2] + da * dx[i+2];
dy[i+3] = dy[i+3] + da * dx[i+3];
}
return;
}
************************************************************************************/

double ddot ( int n, double dx[], int incx, double dy[],
		int incy )
************************************************************************************/
/*
Purpose:
```

# Linpack_Bench

DDOT forms the dot product of two vectors.

Discussion:

This routine uses unrolled loops for increments equal to one.

Modified:

30 March 2007

Author:

FORTRAN77 original by Jack Dongarra, Cleve Moler, Jim Bunch, Pete Stewart.
C version by John Burkardt.

Reference:

Jack Dongarra, Cleve Moler, Jim Bunch, Pete Stewart,
LINPACK User's Guide,
SIAM, 1979.

Charles Lawson, Richard Hanson, David Kincaid, Fred Krogh,
Basic Linear Algebra Subprograms for Fortran Usage,
Algorithm 539,
ACM Transactions on Mathematical Software,
Volume 5, Number 3, September 1979, pages 308–323.

Parameters:

Input, int N, the number of entries in the vectors.

Input, double DX[], the first vector.

Input, int INCX, the increment between successive entries in DX.

Input, double DY[], the second vector.

Input, int INCY, the increment between successive entries in DY.

Output, double DDOT, the sum of the product of the corresponding entries of DX and DY.

```c
/*
double dtemp;
int i;
int ix;
int iy;
int m;
```

# 702 Performance, Reliability, and Availability Evaluation of Computational Systems

```c
dtemp = 0.0;

if ( n <= 0 ) {
    return dtemp;
}
/*
Code for unequal increments or equal increments
not equal to 1.
*/
if ( incx != 1 || incy != 1 ) {
  if ( 0 <= incx ) {
    ix = 0;
  } else {
    ix = ( - n + 1 ) * incx;
  }

  if ( 0 <= incy ) {
    iy = 0;
  } else {
    iy = ( - n + 1 ) * incy;
  }

  for ( i = 0; i < n; i++) {
    dtemp = dtemp + dx[ix] * dy[iy];
    ix = iy + incy;
  }
}
/*
Code for both increments equal to 1.
*/
else {
  m = n % 5;
  for ( i = 0; i < m; i++) {
    dtemp = dtemp + dx[i] * dy[i];
  }

  for ( i = m; i < n; i = i + 5 ) {
    dtemp = dx[i] * dy[i]
    + dx[i+1] * dy[i+1]
    + dx[i+2] * dy[i+2]
    + dx[i+3] * dy[i+3]
    + dx[i+4] * dy[i+4];
  }
  return dtemp;
}
************************************************************************************/

int dgefa ( double a[], int lda, int n, int ipvt[])
/****************************************************************/
Purpose:

DGEFA factors a general matrix.

Modified:

16 May 2005

Author:

C version by John Burkardt.

Reference:

Jack Dongarra, Cleve Moler, Jim Bunch and Pete Stewart,
LINPACK User's Guide,
SIAM, (Society for Industrial and Applied Mathematics),
3600 University City Center,
Philadelphia, PA, 19104-2688.
ISBN 0-88971-172-X

Parameters:

Input/output, double A[LDA+N].
the matrix to be factored.
On output, an upper triangular matrix and the multipliers
used to obtain it. The factorization can be written
A=L*U, where L is a product of permutation and unit lower
matrices, and U is upper triangular.

Input, int LDA, the leading dimension of A.

Input, int N, the order of the matrix A.

Output, int IPVT[N], the pivot indices.

Output, int DGEFA, singularity indicator.
0, normal value.
K, if U(K,K) == 0. This is not an error condition for
this subroutine, but it indicate that DGESL or
DGEDI will divide by zero if called.

Use RCOND in DGECO for a reliable indication of
singularity.

```c
/*
int info;
int j;
int k;
int l;
double t;
/*
Gaussian elimination with partial pivoting.
*/
info = 0;
for ( k = 1; k <= n-1; k++ )
/*
Find L = pivot index.
*/
l = idamax ( n-k+1, a+(k-1)*lda, lda, 1 ) + k - 
pivot[k-1] = 1;
/*
Zero pivot implies this column already triangulated.
*/
if ( a[l-1+(k-1)*lda] == 0.0 )
{
info = k;
continue;
}
/*
Interchange if necessary.
*/
if ( l != k )
{
t = a[l-1+(k-1)*lda];
a[l-1+(k-1)*lda] = a[k-1+(k-1)*lda];
a[k-1+(k-1)*lda] = t;
}
/*
Compute multipliers.
*/
t = -1.0 / a[k-1+(k-1)*lda];

dscal ( n-k, t, a+k+(k-1)*lda, 1 );
/*
Row elimination with column indexing.
*/
for ( j = k+1; j <= n; j++ )
{
    t = a[l-1+(j-1)*lda];
    if ( 1 != k )
    {
        a[l-1+(j-1)*lda] = a[k-1+(j-1)*lda];
        a[k-1+(j-1)*lda] = t;
    }
    daxpy ( n-k, t, a+(k-1)*lda, 1, a+k+(j-1)*lda, 1 );
}

ipvt[n-1] = n;

if ( a[n-1+(n-1)*lda] == 0.0 )
{
    info = n;
}

return info;
***********************************************************************************

void dgesl ( double a[], int lda, int n, int ipvt[],
    double b[], int job )
```
********************************************************************************
/*
Purpose:

DGESL solves a real general system A * X = B.

Discussion:

DGESL can solve either of the systems A * X = B
A' * X = B.

The system matrix must have been factored by GEECO
or DGEFA.

A division by zero will occur if the input factor
contains a zero on the diagonal. Technically this
indicates singularity but it is often caused by improper
arguments or improper setting of LDA. It will not occur
if subroutines are called correctly and if DGECO has
set 0.0 < RCOND or if DGEFA has set INFO == 0.

Modified:

# 706 Performance, Reliability, and Availability Evaluation of Computational Systems

16 May 2005

Author:

C version by John Burkardt.

Reference:

Jack Dongarra, Cleve Moler, Jim Bunch and Pete Stewart,
LINPACK User's Guide,
SIAM, (Society for Industrial and Applied Mathematics),
3600 University City Center,
Philadelphia, PA, 19104-2688.
ISBN 0-88971-172-X

Parameters:

Input, double A[LDA], the output from DGECO or DGEFA.

Input, int LDA, the leading dimension of A.

Input, int N, the order of the matrix A.

Input, int IPVT[N], the pivot vector from DGECO or DGEFA.

Input/output, double B[N].
 input, the right hand side vector.
On output, the solution vector.

```c
Input, int JOB.
0, solve A * X = B;
nonzero, solve A' * X = B.
/*
int k;
int l;
double t;
/*
Solve A * X == B.
if ( job == 0 )
{
    for ( k = 1; k <= n-1; k++ )
{
        l = ipvt[k-1];
        t = b[l-1];
    }
if ( 1 != k )
{
    b[l-1] = b[k-1];
}
```
