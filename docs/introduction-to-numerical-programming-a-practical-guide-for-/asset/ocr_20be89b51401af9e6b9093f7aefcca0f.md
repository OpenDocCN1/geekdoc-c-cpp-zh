Define a user function Func to return the right-hand side of the equation. Start with the trivial initial approximation u⁰(x,y) = 0 for all (x,y) ∈ D, and use an integration mesh with 51 × 51 nodes (50 × 50 intervals) and a relative tolerance ε = 10⁻⁵. Compare the numerical solution with the exact one, u(x,y) = sin x sin y, and estimate the relative error from the maxima of the two solutions. Plot the numerical solution using the routine Contour from the libraries graphlib.py and, respectively, graphlib.h.

Double the number of intervals by taking 101 × 101 nodes and assess the reduction of the maximum error.

# Solution

The Python implementation is presented in Listing 13.19 and the C/C++ version is available as supplementary material (P13-Poisson0.cpp). The contour plot of the solution is shown in Figure 13.15.

# Listing 13.19 Solution of the Poisson Problem 13.143–13.144 (Python Coding)

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