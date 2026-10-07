

# Linpack_Bench 707

```c
b[k-1] = t;
}
daxpy ( n-k, t, a+k*(k-1)*lda, 1, b+k, 1 );
}
for ( k = n; k >= l; k-- )
{
nb[k-1] = b[k-1] / a[k-1+(k-1)*lda];
t = -b[k-1];
daxpy ( k-1, t, a+0+(k-1)+lda, 1, b, 1 );
}
/*
Solve A' * X = B.
else
{
for ( k = 1; k <= n; k++ )
{
t = ddot ( k-1, a+0+(k-1)+lda, 1, b, 1 );
b[k-1] = ( b[k-1] - t ) / a[k-1+(k-1)*lda);
}
for ( k = n-1; k >= 1; k-- )
{
nb[k-1] = b[k-1] + ddot ( n-k, a+k*(k-1)*lda, 1, b+k, 1 );
l = ipvt(k-1);
if ( 1 != k )
{
t = b[l-1];
b[l-1] = b[k-1];
b[k-1] = t;
}
}
return;
}
********************************************************************
void dscal ( int n, double sa, double x[], int incx )
****************************************************/
```

目的：

DSCAL 通过常数缩放向量。

修改：

# 计算系统的性能、可靠性与可用性评估

2007年3月30日

作者：

Jack Dongarra, Cleve Moler, Jim Bunch, Pete Stewart 编写的 FORTRAN77 原。
C 版本由 John Burkardt 编写。

参考：

Jack Dongarra, Cleve Moler, Jim Bunch, Pete Stewart,
LINPACK User's Guide,
SIAM, 1979.

Charles Lawson, Richard Hanson, David Kincaid, Fred Krogh,
Basic Linear Algebra Subprograms for Fortran Usage,
Algorithm 539,
ACM Transactions on Mathematical Software,
Volume 5, Number 3, September 1979, pages 308-323.

参数：

输入，int N，向量中的元素数量。

输入，double SA，乘法因子。

输入/输出，double X[*]，要缩放的向量。

输入，int INCX，X 中连续元素之间的步增量。

```c
int i;
int incx;
int m;

if ( n <= 0 )
{
else if ( incx == 1 )
{
m = n % 5;
}

for ( i = 0; i < m; i++ )
{
x[i] = sa * x[i];
}

for ( i = m; i < n; i = i + 5 )
{
x[i] = sa * x[i];
x[i+1] = sa * x[i+1];
x[i+2] = sa * x[i+2];
x[i+3] = sa * x[i+3];
x[i+4] = sa * x[i+4];
}
else {
  if ( 0 <= incx ) {
    ix = 0;
  } else {
    ix = ( - n + 1 ) * incx;
  }
  for ( i = 0; i < n; i++) {
    x[ix] = sa * x[ix];
    ix = ix + incx;
  }
}
return;
```

****************************************************************
int idamax ( int n, double dx[], int incx )
****************************************************************/*

目的：

IDAMAX 找到向量中绝对值最大的元素索引。

讨论：

警告：此索引是基于 1 的索引，而不是基于 0 的索引！

修改：

2007年3月30日

作者：

Jack Dongarra, Cleve Moler, Jim Bunch, Pete Stewart 编写的 FORTRAN77 原。
C 版本由 John Burkhardt 编写

# 710 计算系统的性能、可靠性与可用性评估

参考：

Jack Dongarra, Cleve Moler, Jim Bunch, Pete Stewart,
LINPACK User's Guide,
SIAM, 1979.

Charles Lawson, Richard Hanson, David Kincaid,
Fred Krogh,
Basic Linear Algebra Subprograms for Fortran Usage,
Algorithm 539,
ACM Transactions on Mathematical Software,
Volume 5, Number 3, September 1979, pages 308-323.

参数：

```c
输入，int N，向量中的元素数量。

输入，double X[*]，要检查的向量。
```

```c
输入，int INCX，SX 中连续元素之间的步增量。
```

```c
输出，int IDAMAX，绝对值最大元素的索引。
```

```c
double dmax;
int i;
int ix;
int value;

value = 0;

if ( n < 1 || incx <= 0 )
{
  return value;
}

value = 1;

if ( n == 1 )
{
  return value;
}

if ( incx == 1 )
{
  dmax = fabs(dx[0]);
  for ( i = 1; i < n; i++)
  {
    if ( dmax < fabs(dx[i]) )
    {
      value = i + 1;
      dmax = fabs(dx[i]);
    }
  }
}
else {
  ix = 0;
  dmax = fabs(dx[0]);
  ix = ix + incx;

  for ( i = 1; i < n; i++)
  {
    if ( dmax < fabs(dx[ix]) )
    {
      value = i + 1;
      dmax = fabs(dx[ix]);
    }
    ix = ix + incx;
  }
}
return value;
```

************************************
double r8_epsilon ( )
**************************************

目的：

R8_EPSON 是一个 2 的幂数。

讨论：

许可：

该代码根据 LGPL 分发。

修改：

2002年9月1日

作者：

John Burkardt

参数：

输出，double R8_EPSON，舍入误差。

```c
const double value = 2.2204604925031E-06;
return value;
}
********************************
double r8_max ( double x, double y )
********************************

目的：

R8_MAX 返回两个 R8 中的较大值。

修改：

2004年8月18日

作者：

John Burkardt

参数：

输入，double X, Y，要比较的量。

输出，double R8_MAX，X 和 Y 的最大值。

```c
double y;
if ( y < x )
{
value = x;
}
else
{
value = y;
}
return value;
```

********************
double r8_random ( int iseed[4] )
********************

目的：

R8_RANDOM 返回 0 到 1 之间的均匀分布随机数。

讨论：

此程序使用模数为 $2^{48}$ 的乘法同余方法，乘因子为 3395283406453（见 G.S. Fishman, 'Multiplicative congruential number generators with modulus 2**48: exhaustive analysis for b=32 and partial analysis for b=48', Math. Comp. 189, pp. 331-344, 1990）。

48 位整数存储在每个 12 位的元素中。因此，该程序可以在具有 32 位整数的机器上移植。

参数：

输入/输出，integer ISEED(4)。进入时，随机数生成器的种子；数组元素必须在 0 到 4095 之间，且 ISEED(4) 必须为奇数。退出时，种子种子。输出，double R8_RANDOM，下一个伪随机数。

```c
int ipw2 = 4096;
int it1;
int it2;
int it3;
int it4;
int m1 = 494;
int m2 = 322;
int m3 = 2508;
int m4 = 2549;
double r = 1.0 / 4096.0;
double value;

/* 将种子乘以模 2**48 的乘因子 */
it4 = iseed[3] * m4;
it3 = it4 / ipw2;
it4 = it4 - ipw2 * it3;
it3_ = it3 + iseed[2] * m4 + iseed[3] * m3;
it2_ = it3 / ipw2;
it3_ = it3 - ipw2 * it2;
it2_ = it2 + iseed[1] * m4 + iseed[2] * m3 + iseed[3] * m2;
it1_ = it2 / ipw2;
it2_ = it2 - ipw2;
it1_ = it1 + iseed[0] * m4 + iseed[1] * m3 + iseed[3] * m1;
it1_ = ( it1 % ipw2 );

/* 返回更新的种子
seed[0] = it1;
seed[1] = it2;
seed[2] = it3;
seed[3] = it4;
/* 48 位整数转换为区间 (0,1) 内的实数 */
value = r * ( double )( it1 )
+ r * ( double )( it2 )
+ r * ( double )( it3 )
+ r * ( double )( it4 )

return value;
}
***********************************
double *r8mat_gen ( int lda, int n )
**************************************************

目的：

R8MAT_GEN 生成随机的 R8MAT。

修改：

2005年6月6日

参数：

输入，integer LDA，矩阵的主维数。

输入，integer N，矩阵的阶。

输出，double R8MAT_GEN[LDA*N]，N  N 矩阵。

```c
{
double *a;
int i;
int init[4] = { 1, 2, 3, 1325 };
int j;

a = ( double * ) malloc ( lda * n * sizeof ( double ) );

for ( j = 1; j <= n; j++)
{
for ( i = 1; i <= n; i++)
{
  a[i-1+(j-1)*lda] = r0_random ( init ) - 0.5;
}
}

return a;
}
```

************************************************
void timestamp ( )
********************************

目的：

TIMESTAMP 将当前的 YMDHMS 日期作为时间戳打印。

示例：
31 May 2001 09:45:54 AM

许可：

该代码根据 GNU LGPL 许可证分发。

修改：

2003年9月24日

作者：

John Burkardt

参数：
无

```c
/*/
# define TIME_SIZE 40
```

