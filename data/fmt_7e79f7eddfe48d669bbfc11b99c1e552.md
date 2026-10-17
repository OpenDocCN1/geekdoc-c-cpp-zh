
//--------------------------------------------------- pde.h ---------------------------------------------------
// Contains routines for solving partial differential equations.
// Part of the numxlib numerics library. Author: Titus Beu, 2013
//---------------------------------------------------
#ifndef _PDE_
#define _PDE_

#include <math.h>
#include "linsys.h"

//==================================================================================================================
int Poisson0(double **u, double x[], double y[], int nx, int ny,
             double eps, double Func(double,double))
//---------------------------------------------------
// Solves the 2D Poisson equation in Cartesian coordinates with Dirichlet
// boundary conditions on a regular grid with (nx x ny) nodes (x[],y[]) using
// the Gauss-Seidel method. The solution u[][] is converged with relative
// precision eps. An error index is returned: 0 - normal execution.
// Calls: Func(x,y) - RHS of Poisson equation
//---------------------------------------------------
{
    const int itmax = 10000;                         // max no. of iterations
    double **f;
    double eij, err, hx, hy, kx, ky, kxy, uij;
    int i, it, j;

    f = Matrix(1,nx,1,ny);

    hx = (x[nx]-x[1])/(nx-1); kx = 1e0/(hx*hx);       // mesh spacings
    hy = (y[ny]-y[1])/(ny-1); ky = 1e0/(hy*hy);
    kxy = 2e0*(kx + ky);

    for (j=2; j<=ny-1; j++)                          // RHS of PDE for interior points
        for (i=2; i<=nx-1; i++) f[i][j] = Func(x[i],y[j]);

    for (it=1; it<=itmax; it++) {                    // Gauss-Seidel iteration loop
        err = 0e0;
        for (j=2; j<=ny-1; j++) {
            for (i=2; i<=nx-1; i++) {                 // interior mesh points
                uij = (kx*(u[i-1][j] + u[i+1][j]) +
                       ky*(u[i][j-1] + u[i][j+1]) - f[i][j]) / kxy;
                eij = uij ? 1e0 - u[i][j]/uij : uij - u[i][j];   // local error
                if (fabs(eij) > err) err = fabs(eij);           // maximum error
                u[i][j] = uij;
            }
        }
        if (err <= eps) break;                       // convergence test
    }

    FreeMatrix(f,1,1);

    if (it > itmax) {
        printf("Poisson0: max. number of iterations exceeded !\n"); return 1;
    }
    return 0;
}
//==================================================================================================================

int PoissonXY(double **u, double x[], double y[], int nx, int ny,
    double eps, double Func(double,double),
    void CondX(double, double&, double&, double&, double&, double&, double&),
    void CondY(double, double&, double&, double&, double&, double&, double&))
//---------------------------------------------------------------
// Solves the 2D Poisson equation in Cartesian coordinates on a regular grid
// with (nx x ny) nodes (x[],y[]) using the Gauss-Seidel method. The solution
// u[i][j] is converged with relative precision eps.
// An error index is returned: 0 - normal execution.
// Calls: Func(x,y) - RHS of Poisson equation; boundary conditions:
//        CondX(y,alf_min,bet_min,gam_min,alf_max,bet_max,gam_max)
//        CondY(x,alf_min,bet_min,gam_min,alf_max,bet_max,gam_max)
//---------------------------------------------------------------
{
#define Save eij = uij ? 1e0 - u[i][j]/uij : uij - u[i][j]; \
    if (fabs(eij) > err) err = fabs(eij); \
    u[i][j] = uij;                 // error estimate and solution storage

const int itmax = 10000;                 // max no. of iterations
double **f;
double *betXmin, *betXmax, *gamXmin, *gamXmax;
double *betYmin, *betYmax, *gamYmin, *gamYmax;
double alf_min, bet_min, gam_min, alf_max, bet_max, gam_max;
double eij, err, hx, hy, kx, ky, kxy, uij;
int i, it, j;

f = Matrix(1,nx,1,ny);
betXmin = Vector(1,ny); betXmax = Vector(1,ny);
gamXmin = Vector(1,ny); gamXmax = Vector(1,ny);
betYmin = Vector(1,nx); betYmax = Vector(1,nx);
gamYmin = Vector(1,nx); gamYmax = Vector(1,nx);

hx = (x[nx]-x[1])/(nx-1); kx = 1e0/(hx*hx);                 // mesh spacings
hy = (y[ny]-y[1])/(ny-1); ky = 1e0/(hy*hy);
kxy = 2e0*(kx + ky);

for (j=2; j<=ny-1; j++)                 // RHS of PDE for interior points
for (i=2; i<=nx-1; i++) f[i][j] = Func(x[i],y[j]);

for (i=1; i<=nx; i++) {                 // boundary conditions
    // lower and upper boundaries
    CondY(x[i],alf_min,bet_min,gam_min,alf_max,bet_max,gam_max);
    betYmin[i] = bet_min/(alf_min*hy + bet_min);
    gamYmin[i] = gam_min/(alf_min + bet_min/hy);
    betYmax[i] = bet_max/(alf_max*hy + bet_max);
    gamYmax[i] = gam_max/(alf_max + bet_max/hy);
}
for (j=2; j<=ny-1; j++) {                 // left and right boundaries
    CondX(y[j],alf_min,bet_min,gam_min,alf_max,bet_max,gam_max);
    betXmin[j] = bet_min/(alf_min*hx + bet_min);
    gamXmin[j] = gam_min/(alf_min + bet_min/hx);
    betXmax[j] = bet_max/(alf_max*hx + bet_max);
    gamXmax[j] = gam_max/(alf_max + bet_max/hx);
}

for (it=1; it<=itmax; it++) {                 // Gauss-Seidel iteration loop
    err = 0e0;
    j = 1;
    // lower boundary
    for (i=1; i<=nx; i++) {
        uij = betYmin[i]*u[i][2] + gamYmin[i]; Save
    }
}

    for (j=2; j<=ny-1; j++) {

        i = 1;

        uij = betXmin[j]*u[i+1][j] + gamXmin[j]; Save                 // 左边界

        for (i=2; i<=nx-1; i++) {

            uij = (kx*(u[i-1][j] + u[i+1][j]) +

                   ky*(u[i][j-1] + u[i][j+1]) - f[i][j]) / kxy; Save

        }

        i = nx;

        uij = betXmax[j]*u[i-1][j] + gamXmax[j]; Save                 // 右边界

    }

    j = ny;

    for (i=1; i<=nx; i++) {

        uij = betYmax[i]*u[i][ny-1] + gamYmax[i]; Save                 // 上边界

    }

    if (err <= eps) break;                                         // 收敛测试

}

FreeMatrix(f,1,1);

FreeVector(betXmin,1); FreeVector(betXmax,1);

FreeVector(gamXmin,1); FreeVector(gamXmax,1);

FreeVector(betYmin,1); FreeVector(betYmax,1);

FreeVector(gamYmin,1); FreeVector(gamYmax,1);

if (it > itmax) {

    printf("PoissonXY: max. number of iterations exceeded !\n"); return 1;

}

return 0;

}

//==============================================================================

int Poisson2D(double **u, double x[], double y[],

              int imin[], int imax[], int nx, int ny, double eps,

              double Func(double,double))

//--------------------------------------------------------------------------------

// 在具有 (nx x ny) 个节点 (x[],y[]) 的规则网格上，采用直角坐标求解二维泊松方程，

// 沿 x 方向的限制索引由 imin[j] 和 imax[j] (j=1,ny) 指定，

// 使用 Gauss-Seidel 方法。

// 解 u[] [] 以相对精度 eps 收敛。

// 返回一个错误索引：0 - 正常执行。

// 调用：Func(x,y) - 泊松方程的右端项（RHS）

//--------------------------------------------------------------------------------

{

    const int itmax = 10000;                                    // 最大迭代次数

    double **f;

    double eij, err, hx, hy, kx, ky, kxy, uij;

    int i, it, j;

    f = Matrix(1,nx,1,ny);

    hx = (x[nx]-x[1])/(nx-1); kx = 1e0/(hx*hx);                  // 网格间距

    hy = (y[ny]-y[1])/(ny-1); ky = 1e0/(hy*hy);

    kxy = 2e0*(kx + ky);

    for (j=2; j<=ny-1; j++)                                      // 内部点的偏微分方程右端项

        for (i=imin[j]+1; i<=imax[j]-1; i++) f[i][j] = Func(x[i],y[j]);

    for (it=1; it<=itmax; it++) {                               // Gauss-Seidel 迭代循环

        err = 0e0;

for (j=2; j<=ny-1; j++) {

    for (i=imin[j]+1; i<=imax[j]-1; i++) {        // 内部网格点

        uij = (kx*(u[i-1][j] + u[i+1][j]) - f[i][j]) / kxy;

        if (i >= imin[j-1] && i <= imax[j-1]) uij += ky*u[i][j-1] / kxy;

        if (i >= imin[j+1] && i <= imax[j+1]) uij += ky*u[i][j+1] / kxy;

        eij = uij ? 1e0 - u[i][j]/uij : uij - u[i][j]; // 误差估计

        if (fabs(eij) > err) err = fabs(eij);        // 最大分量误差

        u[i][j] = uij;

    }

}

    if (err <= eps) break;                        // 收敛测试

}

FreeMatrix(f,1,1);

if (it > itmax) {

    printf("Poisson2D: max. number of iterations exceeded !\n"); return 1;

}

return 0;

}
