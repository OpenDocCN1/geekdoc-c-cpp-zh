# 700 Performance, Reliability, and Availability Evaluation of Computational Systems

```
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
		\int incy )
************************************************************************************/
/*
Purpose:
```