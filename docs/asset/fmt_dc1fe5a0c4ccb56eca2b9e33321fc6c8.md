
```python
        u[i][j] = uij

    for j in range(2,ny):

        i = 1                                                   # left boundary

        uij = betXmin[j]*u[i+1][j] + gamXmin[j]

        eij = 1e0 - u[i][j]/uij if uij else uij - u[i][j]

        if (fabs(eij) > err): err = fabs(eij)

        u[i][j] = uij

        for i in range(2,nx):                                   # interior mesh points

            uij = (kx*(u[i-1][j] + u[i+1][j]) +

                   ky*(u[i][j-1] + u[i][j+1]) - f[i][j]) / kxy

            eij = 1e0 - u[i][j]/uij if uij else uij - u[i][j]    # local error

            if (fabs(eij) > err): err = fabs(eij)               # maximum error

            u[i][j] = uij

        i = nx                                                  # right boundary

        uij = betXmax[j]*u[i-1][j] + gamXmax[j]

        eij = 1e0 - u[i][j]/uij if uij else uij - u[i][j]

        if (fabs(eij) > err): err = fabs(eij)

        u[i][j] = uij

    j = ny                                                      # upper boundary

    for i in range(1,nx+1):

        uij = betYmax[i]*u[i][ny-1] + gamYmax[i]

        eij = 1e0 - u[i][j]/uij if uij else uij - u[i][j]

        if (fabs(eij) > err): err = fabs(eij)

        u[i][j] = uij

if (err <= eps): break                                          # convergence test

if (it >= itmax):

    print("PoissonXY: max. number of iterations exceeded !"); return 1

return 0
```

The routine `Poisson0` is designed to operate only with Dirichlet boundary conditions. Consequently, from the entire system (13.24)–(13.28), it needs to iterate only Equation 13.26 for the interior points of the domain. The routine receives the initial approximation of the solution, including the boundary values, by way of array `u[][]`, which also returns the solution upon execution. The Cartesian coordinates of the uniformly spaced mesh points are received via arrays `x[]` and `y[]`, with the parameters `nx` and `ny` passing the corresponding numbers of nodes, and `eps`, the relative tolerance to be applied to the solution.

The `PoissonXY` solver generalizes the functionalities of the routine `Poisson0`, being able to solve problems with mixed boundary conditions, based on the full set of discretized equations (13.24) through (13.28).

The argument list of the two Poisson solvers is similar, with the array `u[][]` passing on entry an initial approximation and returning on exit the final solution. The supplementary procedural arguments `Func`, `CondX`, and `CondY` of `PoissonXY` provide the actual names of the user routines returning the values of the right-hand-side function `f(x, y)` and, respectively, the coefficients defining the boundary conditions. Specifically, for a given `y`, the function `CondX` is expected to return the coefficients `alf_min`, `bet_min`, and `gam_min`, which define the conditions in the x-direction, normal to the left boundary, as well as `alf_max`, `bet_max`, and `gam_max`, corresponding to the right boundary. Similarly, for each given `x`, the function `CondY` is expected to return the coefficients defining the solution in the y-direction on the lower and, respectively, upper boundaries.

In the first phase, `PoissonXY` determines the auxiliary coefficients β̄ and γ̄ according to Equation 13.8 and stores the values of the right-hand-side function `f(x, y)`. Once the constant quantities are prepared, the routine enters the Gauss–Seidel loop, where the solution is updated at each iteration in sequence on the lower boundary, on the left boundary, at the interior mesh points, on the right boundary, and, finally, on the upper boundary. Along with the updated solution, also the maximum relative change of the solution components, as error estimate, is recorded in `err`. The Gauss–Seidel process is continued until `err` drops below the chosen tolerance `eps`. If the predefined maximum number of iterations is exceeded, an error message is issued and a nonzero error index is returned.

As an illustration for the use of the routine `PoissonXY`, we consider the toy problem associated with the Poisson equation:

∂²u/∂x² + ∂²u/∂y² = cos(x + y) − cos(x − y), (13.30)

which we solve in the domain 𝒟 = [−π, π] × [−π, π] subject to the boundary conditions:

u(±π, y) = 0,   y ∈ [−π, π],

u(x, ±π) = 0,   x ∈ [−π, π]. (13.31)

The analytical solution is u(x,y) = sin x sin y and can conveniently serve as reference for numerical solutions.

Program 13.3, coded to solve the above problem, defines the user functions `Func`, `CondX`, and `CondY`, which return, respectively, the values of the right-hand-side function of the PDE and the coefficients defining the boundary conditions. The program initializes the arrays `x[]` and `y[]` with the coordinates of the mesh points and starts the calculation with a trivial initial approximation, with all the solution components set to 0.

## Listing 13.3 Solution of the 2D Poisson Equation in Cartesian Coordinates (Python Coding)

```python
# Solves the 2D Poisson equation in a rectangular domain

from math import *

from pde import *

def Func(x, y):                     # RHS function for PoissonXY

    return cos(x+y) - cos(x-y)

def CondX(y):                       # Coefficients for left and right boundaries

    alf_min = 1e0; bet_min = 0e0; gam_min = 0e0

    alf_max = 1e0; bet_max = 0e0; gam_max = 0e0

    return (alf_min, bet_min, gam_min, alf_max, bet_max, gam_max)

def CondY(x):                       # Coefficients for lower and upper boundaries

    alf_min = 1e0; bet_min = 0e0; gam_min = 0e0

    alf_max = 1e0; bet_max = 0e0; gam_max = 0e0

    return (alf_min, bet_min, gam_min, alf_max, bet_max, gam_max)

#### main

xmin = -pi; xmax = pi; ymin = -pi; ymax = pi                 # domain boundaries

nx = 51; ny = 51                                             # number of mesh points

eps = 1e-5                                                   # relative solution tolerance

u = [[0]*(ny+1) for i in range(nx+1)]                       # solution

x = [0]*(nx+1); y = [0]*(ny+1)                               # mesh point coordinates

hx = (xmax-xmin)/(nx-1)

for i in range(1,nx+1): x[i] = xmin + (i-1)*hx               # x-mesh points

hy = (ymax-ymin)/(ny-1)

for j in range(1,ny+1): y[j] = ymin + (j-1)*hy               # y-mesh points

for j in range(1,ny+1):                                      # initial approximation of the solution

    for i in range(1,nx+1): u[i][j] = 0e0

PoissonXY(u,x,y,nx,ny,eps,Func,CondX,CondY)

out = open("Poisson.txt","w")                              # open output file

out.write("      x             y             u\n")

for j in range(1,ny+1):

    for i in range(1,nx+1):

        out.write(("{0:10.5f}{1:10.5f}{2:14.5e}\n").format(x[i],y[j],u[i][j]))

out.close()
```

The solution returned by the solver `PoissonXY` (or, alternatively, by `Poisson0`) on a 51 × 51-point grid (50 × 50 intervals), with a relative tolerance ε = 10⁻⁵, is written to an output file and is depicted in Figure 13.4. The numerical profile is found to accurately reproduce the exact solution of the problem.

When dealing with problems for elliptic equations on simply connected irregular domains (without interior holes), one way of describing the boundaries is to delimit the interior nodes on a regular discretization mesh by a couple of vectors, iₘᵢₙ and iₘₐₓ, whose components, iⱼᵐⁱⁿ and iⱼᵐᵃˣ, represent the limiting i-indexes on each horizontal line j. For such problems, however, defining normal derivatives to

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_541_0.png)

FIGURE 13.4 Solution of the boundary-value problem (13.30)–(13.31) for the Poisson equation.

边界相当复杂。为了清晰起见，我们将讨论限制在狄利克雷边界条件，即指定底部、左侧、右侧和顶部边界上的函数值：

$$u_{i,1}^{(r)} = u_{i,1}^0, \quad i = i_{\min}^1, \dots, i_{\max}^1, \quad j = 1,$$

$$u_{i_{\min},j}^{(r)} = u_{i_{\min},j}^0, \quad u_{i_{\max},j}^{(r)} = u_{i_{\max},j}^0, \quad j = 2, \dots, N_y - 1, \tag{13.32}$$

$$u_{i,N_y}^{(r)} = u_{i,N_y}^0, \quad i = i_{\min}^1, \dots, i_{\max}^1, \quad j = N_y.$$

相应地，解决此类问题所需迭代的唯一方程是域内部点的方程：
