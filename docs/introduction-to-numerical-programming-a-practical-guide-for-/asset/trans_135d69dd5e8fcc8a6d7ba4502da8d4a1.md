

static int init = 1;
int i;

if (init)
    { a = CVector(1,nx); b = CVector(1,nx); c = CVector(1,nx); init = 0; }

lam = ht/(4e0*hx*hx);

b[1] = 1e0; c[1] = 0e0;                 // build coefficients of discretized system
Psii = Psi[1];
for (i=2; i<=(nx-1); i++) {
    PsiI = Psii; Psii = Psi[i];           // save initial wave packet values
    W = 2e0*lam + 0.5e0*ht*V[i];
    a[i] = -lam;
    b[i] = dcmplx(W,-1e0);
    c[i] = -lam;
    Psi[i] = lam*PsiI - dcmplx(W,1e0)*Psii + lam*Psi[i+1]; // constant term
}
a[nx] = 0e0; b[nx] = 1e0;

    TriDiagSys(a,b,c,Psi,nx);              // solve tridiagonal discretized system
                                        // solution Psi: propagated wave packet
}

//==============================================================================
int PropagQGS(double Psi[], double Chi[], double V[], int nx, double hx,
              double ht)
//-----------------------------------------------------------------------------
// Propagates the solution PSI = Psi + i Chi of the 1D Schrodinger equation
//   i d/dt PSI(x,t) = [-(1/2) d2/dx2 - V(x)] PSI(x,t),
// over the time interval ht. Uses the Crank-Nicolson scheme on a grid with
// nx nodes and spacing hx and solves the discretized system by Gauss-Seidel
// iterations. Uses real arithmetic.
//-----------------------------------------------------------------------------
{
    const double eps = 1e-6;                     // relative tolerance
    const int itmax = 100;                       // max no. of iterations
    static double *Psi0, *Chi0, *W;
    double err, erri, lam, Psii, Chii;
    static int init = 1;
    int i, it;

    if (init) {
        Psi0 = Vector(1,nx); Chi0 = Vector(1,nx); W = Vector(1,nx); init = 0;
    }

    lam = ht/(4e0*hx*hx);

    for (i=2; i<=nx-1; i++) {                    // explicit 0th-order approximations
        W[i] = 0.5e0*ht*V[i] + 2e0*lam;
        Psi0[i] = Psi[i] - lam*(Chi[i-1] + Chi[i+1]) + W[i]*Chi[i];
        Chi0[i] = Chi[i] + lam*(Psi[i-1] + Psi[i+1]) - W[i]*Psi[i];
    }

    for (it=1; it<=itmax; it++) {                // Gauss-Seidel iteration loop
        err = 0e0;
        for (i=2; i<=nx-1; i++) {
            Psii = Psi0[i] - lam*(Chi[i-1] + Chi[i+1]) + W[i]*Chi[i];
            Chii = Chi0[i] + lam*(Psi[i-1] + Psi[i+1]) - W[i]*Psii;
            // local error estimate based on probability density
erri = fabs((Psii+Psii+Chii*Chii) - (Psi[i]*Psi[i]+Chi[i]*Chi[i]));
if (erri > err) err = erri;                // maximum error estimate
Psi[i] = Psii;
Chi[i] = Chii;
}
    if (err <= eps) break;                // convergence test
}

if (it > itmax) {
    printf("PropagQMGS: max. number of iterations exceeded !\n"); return 1;
}
return 0;
}
//================================================================================
void PropagWave(double u0[], double u1[], double u[], int nx, double c,
                double hx, double ht)
//--------------------------------------------------------------------------------
// Propagates the solutions u0[] and u1[] of the wave equation
//   d2u/dt2 = c^2 d2u/dx2,   c - phase velocity (constant)
// over the time interval ht, using the explicit difference scheme on a
// spatial grid with nx nodes and spacing hx. Returns the solution in u[].
//--------------------------------------------------------------------------------
{
    double lam, lam2;
    int i;

    lam = c*ht/hx; lam = lam*lam;
    lam2 = 2e0*(1e0 - lam);

    u[1] = u0[1]; u[nx] = u0[nx];                // Dirichlet boundary conditions
    for (i=2; i<=nx-1; i++)      // propagate solution at interior points
        u[i] = lam*u1[i-1] + lam2*u1[i] + lam*u1[i+1] - u0[i];
}
#endif

## 13.7 问题

以下问题的Python和C/C++程序可以从本章开发的模块中导入相应函数，分别是 pde.py 和 pde.h，这些模块作为补充材料提供。为了创建运行时绘图，可以使用 graphlib.py 和 graphlib.h 库中包含的图形例程。

### 问题13.1

使用第13.2节所述的 Poisson0 例程来求解与泊松方程相关的以下问题：

∂²u/∂x² + ∂²u/∂y² = cos(x + y) − cos(x − y)      (13.143)

在区域 D = [−π, π] × [−π, π] 中，边界条件为

u(±π, y) = 0,   y ∈ [−π, π],
u(x, ±π) = 0,   x ∈ [−π, π].      (13.144)

定义一个用户函数 Func 来返回方程右端的值。从对所有 (x,y) ∈ D 成立的平凡初始近似 u⁰(x,y) = 0 开始，使用 51 × 51 个节点（50 × 50 个区间）的积分网格，并设置相对容差 ε = 10⁻⁵。将数值解与精确解 u(x,y) = sin x sin y 进行比较，并从两个解的最大值估计相对误差。使用 graphlib.py 库中的 Contour 例程绘制数值解，C/C++ 版本则使用 graphlib.h 库。

通过取 101 × 101 个节点将区间数加倍，并评估最大误差的减小情况。

# 解答

Python 实现见清单 13.19，C/C++ 版本见补充材料（P13-Poisson0.cpp）。解的等高线图如图 13.15 所示。

### 清单 13.19 泊松问题13.143–13.144的求解（Python代码）

```
# Solves the 2D Poisson equation in a rectangular domain
from math import *
from pde import *
from graphlib import *

def Func(x, y):                     # RHS function for Poisson0
    return cos(x+y) - cos(x-y)

# main

xmin = -pi; xmax = pi; ymin = -pi; ymax = pi               # domain boundaries
nx = 51; ny = 51                                          # number of mesh points
eps = 1e-5                                                # relative solution tolerance

u = [[0]*(ny+1) for i in range(nx+1)]                     # solution
x = [0]*(nx+1); y = [0]*(ny+1)                            # mesh point coordinates

hx = (xmax-xmin)/(nx-1)
for i in range(1,nx+1): x[i] = xmin + (i-1)*hx            # x-mesh points
hy = (ymax-ymin)/(ny-1)
for j in range(1,ny+1): y[j] = ymin + (j-1)*hy            # y-mesh points

for j in range(1,ny+1):                   # initial approximation of the solution
    for i in range(1,nx+1): u[i][j] = 0e0   # and boundary conditions

Poisson0(u,x,y,nx,ny,eps,Func)

out = open("Poisson.txt","w")                           # open output file
out.write("      x           y           u\n")
for j in range(1,ny+1):
    for i in range(1,nx+1):
        out.write(("{0:10.5f}{1:10.5f}{2:14.5e}\n").format(x[i],y[j],u[i][j]))
out.close()

umin = umax = u[1][1]                                     # minimum and maximum of the solution
for j in range(1,ny+1):
    for i in range(1,nx+1):
        if (u[i][j] < umin): umin = u[i][j]
        if (u[i][j] > umax): umax = u[i][j]
```

```
GraphInit(800,800)
Contour(0,nx,ny,xmin,xmax,ymin,ymax,umin,umax, \
        0.15,0.85,0.15,0.85,"x","y","Poisson")
MainLoop()
```

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_589_0.png)

**图13.15** 离散化泊松问题13.143–13.144的有限差分解（问题13.1）。

### 问题13.2

考虑与泊松方程相关的以下问题：

$$\frac{\partial^2u}{\partial x^2}+\frac{\partial^2u}{\partial y^2}=-\left[\cos(x+y)+\cos(x-y)\right] \tag{13.145}$$

在区域 $\mathcal{D}=[-\pi,\pi]\times[-\pi/2,\pi/2]$ 中，边界条件为

$$u(\pm\pi,y)=\cos y,\quad y\in[-\pi/2,\pi/2],$$
$$u(x,\pm\pi/2)=0,\quad x\in[-\pi,\pi]. \tag{13.146}$$

使用第13.2节所述的 PoissonXY 例程求解此问题，定义用户函数 Func、CondX 和 CondY，分别返回方程右端项和边界系数。从对所有 $(x,y)\in\mathcal{D}$ 成立的平凡初始近似 $u^0(x,y)=0$ 开始。使用 51 × 26 个节点（50 × 25 个区间）的积分网格，并设置相对容差 $\varepsilon=10^{-5}$。将数值解与精确解 $u(x,y)=\cos x\cos y$ 进行比较，并从两个解的最大值估计相对误差。使用 graphlib.py 库中的 Contour 例程绘制数值解，C/C++ 版本则使用 graphlib.h 库。

在两个方向上都将网格区间数加倍（取 101 × 51 个节点），并在精度方面与之前的估计进行比较。

