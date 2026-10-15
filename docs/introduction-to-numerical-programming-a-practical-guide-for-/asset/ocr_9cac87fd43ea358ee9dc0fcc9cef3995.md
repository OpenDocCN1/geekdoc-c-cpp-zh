with the additional constraint

$y(1) = 1.$

(12.84)

The homogeneity of the Legendre equation guarantees that any solution multiplied by a constant remains a solution, too. Correspondingly, for even $n$, the procedure amounts to the straightforward propagation from an arbitrary initial value $\tilde{y}(0) = y_a$, which is finalized by rescaling the found solution, $\tilde{y}(x)$, with the end value $\tilde{y}(1)$, that is, $y(x) = \tilde{y}(x)/\tilde{y}(1)$. In such a manner, the unused boundary condition, $y(1) = 1$, is clearly satisfied. As for the odd $n$-solutions, they require the actual application of the shooting method, which implies the determination of the correct initial derivative $y'_a$ by iterative bisections of the interval $(-\infty, +\infty)$.

A program designed to calculate the Legendre polynomials by the shooting method is presented in Listing 12.15. In particular, for $n = 5$, an integration step size $h = 10^{-4}$, and a relative tolerance $\varepsilon = 10^{-4}$

# Listing 12.15 Legendre Polynomials by the Shooting Method (Python Coding)

```
# Legendre polynomials by the shooting method
from math import *
from ode import *
from specfunc import *

global n                                      # polynomial order
def Func(x, y, dy):                           # RHS of Legendre ODE
    return (2e0*x*dy - n*(n+1)*y) / (1e0 - x*x)

# main

n = 5                                         # order of Legendre polynomial
xa = 0e0                                      # boundary values
xb = 1e0; yb = 1e0
 eps = 1e-4                                    # tolerance for solution at xb
hx = 1e-4                                      # x-mesh step size

nx = int((xb-xa)/hx + 0.5) + 1                # number of x-mesh points

x = [0]*(nx+1); y = [0]*(nx+1)                # x-mesh, solution

for m in range(1,nx+1): x[m] = xa + (m-1)*hx   # generate x-mesh

if (n % 2 == 0):                              # even solutions: rescaling
    ya = 1e0; dy = 0e0
    Propag(x,y,nx,ya,dy,Func)
    for m in range(1,nx+1): y[m] /= y[nx]      # normalization
else:                                         # odd solutions: shooting
    ya = 0e0
    dy1 = -1e3; dy2 = 1e3                      # search initial derivative in [dy1,dy2]
    (dy, exist) = Shoot(x,y,nx,ya,yb,dy1,dy2,eps,Func)

out = open("shoot.txt","w")
out.write("dy = {0:8.5f}\n".format(dy))
out.write("      x          P{0:1d}            err\n".format(n))
for m in range(1,nx+1):
    (P, d) = Legendre(n,x[m])
    out.write(("{0:10.5f}{1:10.5f}{2:10.5f}\n").format(x[m],y[m],P-y[m]))
out.close()
```