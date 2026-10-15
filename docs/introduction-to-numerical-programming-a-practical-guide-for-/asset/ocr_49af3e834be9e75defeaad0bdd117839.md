![](bbox=[0.32, 0.14, 0.68, 0.34])

FIGURE 13.5 Integration grid and bounding line indexes, i_min and i_max, for a disk-like integration domain. Filled circles represent boundary values and empty circles indicate values that need to be calculated.

# Listing 13.4 Solver for the 2D Poisson Equation on an Irregular Domain (Python Coding)

```
# ============================================================================
# def Poisson2D(u, x, y, imin, imax, nx, ny, eps, Func):
# ----------------------------------------------------------------------------
# Solves the 2D Poisson equation in Cartesian coordinates on a regular grid
# with (nx x ny) nodes (x[],y[]), with limiting indexes along x specified by
# imin[j] and imax[j] (j=1,ny), using the Gauss-Seidel method. The solution
# u[][] is converged with relative precision eps.
# An error index is returned: 0 - normal execution.
# Calls: Func(x,y) - RHS of Poisson equation
# ----------------------------------------------------------------------------
    itmax = 10000                                      # max no. of iterations

    f = [[0]*(ny+1) for i in range(nx+1)]

    hx = (x[nx]-x[1])/(nx-1); kx = 1e0/(hx*hx)          # mesh spacings
    hy = (y[ny]-y[1])/(ny-1); ky = 1e0/(hy*hy)
    kxy = 2e0*(kx + ky)

    for j in range(2,ny):                              # RHS of PDE for interior points
        for i in range(2,nx): f[i][j] = Func(x[i],y[j])

    for it in range(1,itmax+1):                        # Gauss-Seidel iteration loop
        err = 0e0
        for j in range(2,ny):
            for i in range(imin[j]+1,imax[j]):         # interior mesh points
                uij = (kx*(u[i-1][j] + u[i+1][j]) - f[i][j]) / kxy
                if (i >= imin[j-1] and i <= imax[j-1]): uij += ky*u[i][j-1] / kxy
                if (i >= imin[j+1] and i <= imax[j+1]): uij += ky*u[i][j+1] / kxy

                eij = 1e0 - u[i][j]/uij if uij else uij - u[i][j]
                if (fabs(eij) > err): err = fabs(eij)      # max. component error
                u[i][j] = uij

        if (err <= eps): break                         # convergence test
```