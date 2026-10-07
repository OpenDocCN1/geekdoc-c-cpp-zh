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

```
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
ot equal to 1.
*/
if ( incx != 1 || incy != 1 )
{
  if ( 0 <= incx )
{
    ix = 0;
}
```