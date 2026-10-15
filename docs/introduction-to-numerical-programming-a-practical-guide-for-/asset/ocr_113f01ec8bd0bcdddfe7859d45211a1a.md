# Listing 10.34 Integral over Toroidal Domain Using Cartesian Coordinates (Python Coding)

```
# Evaluates a 3D integral on a torus using Cartesian coordinates
from math import *
from integral import *

def Func(x, y, z):
    global R, r
    Rp = sqrt(x*x + y*y)                     # major radial distance
    dR = R - Rp
    rp = sqrt((dR*dR + z*z))                 # minor radial distance
    return (exp(-rp/r) - exp(-1e0) if rp <= r else 0e0)   # zero-padding

# main
R = 3e0; r = 1e0                            # major & minor torus radii
ax = ay = az = 0e0                          # bounding box: 1st octant
bx = by = R+r; bz = r                       # multiply results with 8
nx = ny = 200                               # equal density of mesh
nz = int(nx * r/(R+r))                      # points along x, y, z

I = 8e0 * qTrapz3D(Func, ax, bx, nx, ay, by, ny, az, bz, nz)
print("I Trapeze = ", I)
I = 8e0 * qSimpson3D(Func, ax, bx, nx, ay, by, ny, az, bz, nz)
print("I Simpson = ", I)
I = 8e0 * qGaussLeg3D(Func, ax, bx, nx, ay, by, ny, az, bz, nz)
print("I GaussLeg = ", I)                    # result = 9.510516...
```

to distinguish between interior and exterior points. Having in view the exact value of the integral (4π²Rr²(1 − 5/2 e⁻¹) ≈ 9.5105163) and using the same number of grid points (200 × 200 × 50), compare the obtained result in terms of exact significant digits with those provided by functions qSimpson3D and qGaussLeg3D.

# Solution

The Python integrator is to be found in Listing 10.33, being part of the module integral.py. Its C/C++ counterpart is included in the header file integral.h. The Python program performing the required integration is given in Listing 10.34 and the C/C++ version is available as supplementary material (P10-Integ3D1.py).

# PROBLEM 10.8

Write Python and C/C++ codes based on the adaptive 3D technique presented in Section 10.12 to integrate over a toroidal domain of radii R = 3 and r = 1 (see Figure 10.6) the integrand

f(x, y, z) = { (1 − r′/r)²   r′ ≤ r,  0   r′ > r, }

depending explicitly only on the distance r′ to the tube axis. Impose the relative precision ε = 10⁻⁶.

# Solution

The implementations are given in Listings 10.35 and 10.36.