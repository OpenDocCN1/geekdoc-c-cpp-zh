# 23.6.5

# Imposing Boundary Conditions

The procedure to impose Dirichlet’s boundary conditions for the 2D case is essentially the same as that for the 1D case (Section 23.4.2.2), with it now applied to all nodes that lie on the boundary Γ.

Listing 23.2 The code LaplaceFEM_2D.py solves the 2D Laplace equation using a finite elements method.

```
# LaplaceFEM_2D.py solve 2D Laplace Eq via Finite elements method;
    utf-8coding

from numpy import *
from numpy.linalg import solve
import pylab as p
from mpl_toolkits.mplot3d import Axes3D

# Num squares, nodes, triangles, mesh coords, Initialization

Width = 1.;    Height = 1.; Nx = 20;  Ny = 20; U0 = 100
Xurc = Width;  Yurc = Height;  Yllc = 0;   Xllc = 0
Ns = Nx * Ny;  Nn = (Nx + 1)*(Ny + 1)
Dx = (Xurc-Xllc)/Nx;   Dy = (Yurc-Yllc)/Ny;   Ne = 2 * Ns
ge = zeros(Ne, float)
x = zeros(Ne, float);      y = zeros(Ne, float)
Ebcnod = zeros(Ne, int);   Ebcval = zeros(Ne, int)
node = zeros((Ne + 1, Ne + 1), int)

for i in range(1, Nn + 1):
    x[i] = (i - 1) % (Nx + 1) * Dx
    y[i] = floor((i - 1) / (Nx + 1)) * Dy

# Connectivity Information
for i in range(1, Ns + 1):
    node[2 * i - 1, 1] = i + floor((i - 1) / Nx)
    node[2 * i - 1, 2] = node[2 * i - 1, 1] + 1 + Nx + 1
    node[2 * i - 1, 3] = node[2 * i - 1, 1] + 1 + Nx + 1 - 1
    node[2 * i, 1] = i + floor((i - 1) / Nx)
    node[2 * i, 2] = node[2 * i, 1] + 1
    node[2 * i, 3] = node[2 * i, 1] + 1 + Nx + 1

# Dirichlet Boundary Conditions
Tnebc = 0
for i in range(0, Nn):
    if x[i] == Xllc or x[i] == Xurc or y[i] == Yllc:
        Tnebc = Tnebc + 1
        Ebcnod[Tnebc] = i
        Ebcval[Tnebc] = 0
    elif y[i] == Yurc:
        Tnebc = Tnebc + 1
        Ebcnod[Tnebc] = i
        Ebcval[Tnebc] = U0

# Initialize A matrix, b vector, form matrix
A = zeros((Nn + 1, Nn + 1), float)
b = zeros((Nn + 1, Nn + 1), float)
for e in range(1, Ne):
    x21 = x[node[e, 2]] - x[node[e, 1]]
    x31 = x[node[e, 3]] - x[node[e, 1]]
    x32 = x[node[e, 3]] - x[node[e, 2]]
    x13 = x[node[e, 1]] - x[node[e, 3]]
    y12 = y[node[e, 1]] - y[node[e, 2]]
```