
#ifndef `_LINSYS_`

#define `_LINSYS_`

#include <stdio.h>

#include <math.h>

#include "memalloc.h"

//================================================================================================

```c
void Gauss(double **a, double **b, int n, int m, double &det)
```
```c
//-----------------------------------------------------------------------------------------------
// Solves matrix equation a x = b by Gaussian elimination with partial
// pivoting on columns.
// a   - coefficient matrix (n x n); destroyed on exit
// b   - matrix of constant terms (n x m); solution x on exit
// det - determinant of coefficient matrix (output).
//-----------------------------------------------------------------------------------------------
{
#define Swap(a,b) { t = a; a = b; b = t; }
    double amax, sum, t;
    int i, imax, j, k;
    det = 1e0;
    for (k=1; k<=n; k++) {                      // FORWARD ELIMINATION
        amax = 0e0;                             // determine pivot row with
        for (i=k; i<=n; i++)                    // max. element on column k
            if (amax < fabs(a[i][k])) { amax = fabs(a[i][k]); imax = i; }
        if (amax == 0e0)
            { printf("Gauss: singular matrix !\n"); det = 0e0; return; }
        if (imax != k) {                        // interchange rows imax and k
det = -det;                                 // to put pivot on diagonal
for (j=k; j<=n; j++) Swap(a[imax][j],a[k][j])
for (j=1; j<=m; j++) Swap(b[imax][j],b[k][j])
}
det *= a[k][k];                              // multiply determinant with pivot
t = 1e0/a[k][k];                             // divide pivot row by pivot
for (j=k+1; j<=n; j++) a[k][j] *= t;
for (j= 1; j<=m; j++) b[k][j] *= t;
for (i=k+1; i<=n; i++) {                     // reduce non-pivot rows
    t = a[i][k];
    for (j=k+1; j<=n; j++) a[i][j] -= a[k][j]*t;
    for (j= 1; j<=m; j++) b[i][j] -= b[k][j]*t;
}
}
for (k=n-1; k>=1; k--)                       // BACKWARD SUBSTITUTION
    for (j=1; j<=m; j++) {
        sum = b[k][j];
        for (i=k+1; i<=n; i++) sum -= a[k][i]*b[i][j];
        b[k][j] = sum;
    }
}
```

//==============================================================================

```c
void GaussJordan0(double **a, double **b, int n, int m, double &det)
```
```c
//--------------------------------------------------------------------------------
// Solves matrix equation a x = b by Gauss-Jordan elimination with partial
// pivoting on columns.
// a  - coefficient matrix (n x n); destroyed on exit
// b  - matrix of constant terms (n x m); solution x on exit
// det - determinant of coefficient matrix (output).
//--------------------------------------------------------------------------------
{
#define Swap(a,b) { t = a; a = b; b = t; }
double amax, t;
int i, imax, j, k;
det = 1e0;
for (k=1; k<=n; k++) {                       // FORWARD ELIMINATION
    amax = 0e0;                              // determine pivot row with
    for (i=k; i<=n; i++)                     // max. element on column k
        if (amax < fabs(a[i][k])) { amax = fabs(a[i][k]); imax = i; }
    if (amax == 0e0)
        { printf("GaussJordan0: singular matrix !\n"); det = 0e0; return; }
    if (imax != k) {                         // interchange rows imax and k
        det = -det;                          // to put pivot on diagonal
        for (j=k; j<=n; j++) Swap(a[imax][j],a[k][j])
        for (j=1; j<=m; j++) Swap(b[imax][j],b[k][j])
    }
    det *= a[k][k];                          // multiply determinant with pivot
    t = 1e0/a[k][k];                         // divide pivot row by pivot
    for (j=k+1; j<=n; j++) a[k][j] *= t;
    for (j= 1; j<=m; j++) b[k][j] *= t;
}
for (i=1; i<=n; i++)
    // 归约非主元行
    if (i != k) {
        t = a[i][k];
        for (j=1; j<=n; j++) a[i][j] -= a[k][j]*t;
        for (j=1; j<=m; j++) b[i][j] -= b[k][j]*t;
    }
}
```

//==============================================================================

```c
void GaussJordan1(double **a, double **b, int n, int m, double &det)
```
```c
//------------------------------------------------------------------------------
// 通过带列部分主元的 Gauss-Jordan 消去法求解矩阵方程 a x = b。
// a  - 系数矩阵 (n x n); 退出时为 a^(-1)
// b  - 常数项矩阵 (n x m); 退出时为解 x
// det - 系数矩阵的行列式 (输出)。
//------------------------------------------------------------------------------
{
#define Swap(a,b) { t = a; a = b; b = t; }
    double amax, t;
    int i, imax, j, k;
    int *ipivot;
    ipivot = IVector(1,n);                         // 存储主元行
    det = 1e0;
    for (k=1; k<=n; k++) {                         // 正向消去
        amax = 0e0;                                // 确定具有
        for (i=k; i<=n; i++)                       // 第 k 列最大元素的行
            if (amax < fabs(a[i][k])) { amax = fabs(a[i][k]); imax = i; }
        if (amax == 0e0)
            { printf("GaussJordan1: singular matrix !\n"); det = 0e0; return; }
        ipivot[k] = imax;                          // 存储主元行索引
        if (imax != k) {                           // 互换行 imax 和 k
            det = -det;                            // 使主元位于对角线上
            for (j=1; j<=n; j++) Swap(a[imax][j],a[k][j])
            for (j=1; j<=m; j++) Swap(b[imax][j],b[k][j])
        }
        det *= a[k][k];                            // 用主元乘以行列式
        t = 1e0/a[k][k];                           // 用主元除主元行
        a[k][k] = 1e0;                             // 单位矩阵的对角元素
        for (j=1; j<=n; j++) a[k][j] *= t;
        for (j=1; j<=m; j++) b[k][j] *= t;
        for (i=1; i<=n; i++)                       // 归约非主元行
            if (i != k) {
                t = a[i][k];
                a[i][k] = 0e0;                     // 单位矩阵的非对角元素
                for (j=1; j<=n; j++) a[i][j] -= a[k][j]*t;
                for (j=1; j<=m; j++) b[i][j] -= b[k][j]*t;
            }
    }
    for (k=n; k>=1; k--) {                         // 重新排列逆矩阵的列
imax = ipivot[k];
    if (imax != k)
        for (i=1; i<=n; i++) Swap(a[i][imax],a[i][k])
    }
    FreeIVector(ipivot,1);
}
```

//==============================================================================

```c
void GaussJordan(double **a, double **b, int n, int m, double &det)
```
```c
//------------------------------------------------------------------------------
// 通过带完全主元的 Gauss-Jordan 消去法求解矩阵方程 a x = b。
// a  - 系数矩阵 (n x n); 退出时为 a^(-1)
// b  - 常数项矩阵 (n x m); 退出时为解 x
// det - 系数矩阵的行列式 (输出)。
//------------------------------------------------------------------------------
{
#define Swap(a,b) { t = a; a = b; b = t; }
    double amax, t;
    int i, imax, j, jmax, k;
    int *ipivot, *jpivot, *npivot;
    ipivot = IVector(1,n); jpivot = IVector(1,n);     // 主元行和列
    npivot = IVector(1,n);                             // 标记已使用的主元列
    for (i=1; i<=n; i++) npivot[i] = 0;
    det = 1e0;
    for (k=1; k<=n; k++) {                             // 正向消去
        amax = 0e0;                                    // 确定主元
        for (i=1; i<=n; i++) {                         // 遍历行
            if (npivot[i] != 1)
                for (j=1; j<=n; j++) {                 // 遍历列
                    if (npivot[j] == 0)                // 尚未进行主元选择？
                        if (amax < fabs(a[i][j]))
                            { amax = fabs(a[i][j]); imax = i; jmax = j; }
                    if (npivot[j] > 1) {
                        printf("GaussJordan: singular matrix 1 !\n");
                        det = 0e0; return;
                    }
                }
        }
        if (amax == 0e0)
            { printf("GaussJordan: singular matrix 2 !\n"); det = 0e0; return; }
        ipivot[k] = imax; jpivot[k] = jmax;            // 存储主元行和列
        ++(npivot[jmax]);                              // 标记已使用的主元列
        if (imax != jmax) {                            // 互换行 imax 和 jmax
            det = -det;                                // 使主元位于对角线上
```
