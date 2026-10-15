
Making f(x,y,z) = 1 at all interior points, the integral obviously represents the torus volume (2π²Rr² ≈ 59.217626), and this is a convenient test case for the program.

For 3D integrals defined in spherical coordinates, a quadrature formula similar to the one for Cartesian coordinates can be devised:

∫₀ᵃ ∫₀^π ∫₀^{2π} f(r,θ,φ) r² dr sinθ dθ dφ ≈ Σ_{i=1}^{n_r} w_i^{(r)} Σ_{j=1}^{n_θ} w_j^{(θ)} Σ_{k=1}^{n_φ} w_k^{(φ)} f(r_i,θ_j,φ_k), (10.87)

however, with weights also accounting for the supplementary r² and sinθ factors stemming from the volume element. In principle, the same one-dimensional schemes can be employed for the individual coordinates as for the Cartesian case. The integrator qSimpsonSph (Listing 10.20) is based on Simpson’s rule and expects, besides the user function Func describing the integrand, a single geometrical parameter, namely, the outer radial limit a. The number of integration points for r, θ, and φ (nr, nt, and np) must also be provided.

After retrieving generic abscissas and weights from routine xSimpson for all three spherical coordinates, function qSimpsonSph scales the radial weights wr by r², and the angular weights wt for the θ integration by sinθ. With the redefined weights, the subsequent triple summation remains similar to the one for Cartesian coordinates.

## Listing 10.20 Integrator in Spherical Coordinates Based on Simpson’s Rule (Python Coding)

```
#================================================================================
def qSimpsonSph(Func, a, nr, nt, np):
#--------------------------------------------------------------------------------
#  Integrates function Func(r,theta,phi) on [0,a] x [0,pi] x [0,2*pi]
#  in spherical coordinates using Simpson’s rule with (nr x nt x np) points
#--------------------------------------------------------------------------------
    if (nr % 2 == 0): nr += 1                # increment nr if even
    if (nt % 2 == 0): nt += 1                # increment nt if even
    if (np % 2 == 0): np += 1                # increment np if even

    r = [0]*nr; wr = [0]*nr
    t = [0]*nt; wt = [0]*nt
    p = [0]*np; wp = [0]*np

    (r,wr) = xSimpson(0e0,a,nr)              # generate integration points
    (t,wt) = xSimpson(0e0,pi,nt)
    (p,wp) = xSimpson(0e0,2e0*pi,np)

    for i in range(0,nr): wr[i] *= r[i] * r[i]      # factors from
    for j in range(0,nt): wt[j] *= sin(t[j])        # volume element

    s = 0e0
    for i in range(0,nr):
        sr = 0e0
        for j in range(0,nt):
            st = 0e0
            for k in range(0,np):
                st += wp[k] * Func(r[i],t[j],p[k])
            sr += wt[j] * st
        s += wr[i] * sr

    return s
```

For integrals in spherical coordinates extending over the entire space, Gaussian quadratures are better suited than classical formulas. In particular, the radial integration can be most conveniently performed using the Gauss–Laguerre formula 10.79, which is specifically designed for the semiinfinite interval [0, +∞), while the angular contributions can be efficiently evaluated using Gauss–Legendre quadratures. Maintaining the overall structure of qSimpsonSph, the routine qGaussSph (Listing 10.21) calls xGaussLag and xGaussLeg to generate the radial and, respectively, angular abscissas and weights.

In what follows, we consider as an example the wave function of the electron in a 2p state in the hydrogen atom (for quantum numbers n = 2, l = 1, and m = 0). Expressed in dimensionless radial units (see Fitts 2002), this wave function reads:

Ψ210(r,θ,φ) = 1/(4√2π) r e^(-r/2) cos θ.

Its norm is given by the integral of the probability density |Ψ210(r,θ,φ)|²,

∫₀^∞ ∫₀^π ∫₀^{2π} |Ψ210(r,θ,φ)|² r² dr sin θ dθ dφ = 1,

and, since it represents the total probability of finding the electron somewhere in space, it naturally amounts to 1. Program 10.22 comparatively evaluates the above integral using Simpson’s rule and

## Listing 10.21 Integrator in Spherical Coordinates Based on Gaussian Quadratures (Python Coding)

```
def qGaussSph(Func, nr, nt, np):
# Integrates function Func(r,theta,phi) on [0,inf] x [0,pi] x [0,2*pi]
# in spherical coordinates using Gauss-Laguerre and Gauss-Legendre formulas
# with (nr x nt x np) points
r = [0]*nr; wr = [0]*nr
t = [0]*nt; wt = [0]*nt
p = [0]*np; wp = [0]*np
(r,wr) = xGaussLag(0e0,nr)      # Gauss-Laguerre radial quadrature
(t,wt) = xGaussLeg(0e0,pi,nt)   # Gauss-Legendre angular quadratures
(p,wp) = xGaussLeg(0e0,2e0*pi,np)
for i in range(0,nr): wr[i] *= r[i] * r[i]      # factors from
for j in range(0,nt): wt[j] *= sin(t[j])        # volume element
s = 0e0
for i in range(0,nr):
    sr = 0e0
    for j in range(0,nt):
        st = 0e0
        for k in range(0,np):
            st += wp[k] * Func(r[i],t[j],p[k])
        sr += wt[j] * st
    s += wr[i] * sr
return s
```

## Listing 10.22 Integral in Spherical Coordinates (Python Coding)

```
# Evaluates a 3D integral using spherical coordinates
from math import *
from integral import *

def Func(r, theta, phi):              # probability density for 2p state
    c = 1e0/(32e0*pi)
    rcos = r * cos(theta)
    return c * rcos * rcos * exp(-r)

# main

a = 35e0                             # radial limit
nr = 150; nt = 60; np = 3
I = qSimpsonSph(Func,a,nr,nt,np)
print("I SimpsonSph = ",I)

nr = 3; nt = 9; np = 1
I = qGaussSph(Func,nr,nt,np)
print("I GaussSph   = ",I)
```

## Listing 10.23 Integrator in Cylindrical Coordinates Based on Simpson's Rule (Python Coding)

```
# ============================================================================
def qSimpsonCyl(Func, a, az, bz, nr, np, nz):
# ----------------------------------------------------------------------------
#   Integrates function Func(r,phi,z) on domain [0,a] x [0,2*pi] x [az,bz]
#   in cylindrical coordinates using Simpson's rule with (nr x np x nz) points
# ----------------------------------------------------------------------------
    if (nr % 2 == 0): nr += 1                 # increment nr if even
    if (np % 2 == 0): np += 1                 # increment np if even
    if (nz % 2 == 0): nz += 1                 # increment nz if even

    r = [0]*nr; wr = [0]*nr
    p = [0]*np; wp = [0]*np
    z = [0]*nz; wz = [0]*nz

    (r,wr) = xSimpson(0e0,a,nr)               # generate integration points
    (p,wp) = xSimpson(0e0,2e0*pi,np)
    (z,wz) = xSimpson(az,bz,nz)

    for i in range(0,nr): wr[i] *= r[i]       # factor from volume element

    s = 0e0
    for i in range(0,nr):
        sr = 0e0
        for j in range(0,np):
            sp = 0e0
            for k in range(0,nz):
                sp += wz[k] * Func(r[i],p[j],z[k])
            sr += wp[j] * sp
        s += wr[i] * sr

    return s
```

Gaussian quadratures. Concretely, to reproduce the result with seven exact figures, function qSimpsonSph needs to radially integrate out to a = 35 using n_r = 150, n_θ = 60, and n_φ = 3 nodes (the integrand lacks φ dependence). Given their remarkable properties, especially, the appropriateness of the Gauss–Laguerre formula for the radial contributions, the Gaussian quadratures achieve the same result with as few as n_r = 3, n_θ = 9, and n_φ = 1 integration points.

Combining functions qSimpson3D and qSimpsonSph, one can readily build an integrator for cylindrical coordinates based on Simpson’s rule (Listing 10.23).

## 10.12 Adaptive Multidimensional Integration

In the case of high-dimensional integrals with irregular boundaries and dispersed integrand values, the direct product technique, with zero padding on uniform meshes and regular extended boundaries, may become intractable if the grid is adjusted to the least convergent regions. In such cases, rather a methodology operating directly inside the irregular boundaries and featuring local mesh control is desirable. To this end, we will represent the integral as embedded, functionally coupled one-dimensional integrals, using the same one-dimensional adaptive integrator for each separate level of integration.

Concretely, a 2D integral in Cartesian coordinates may be regarded as an “outer” integral with respect to x, whose integrand is the “inner” integral with respect to y along a line of fixed x:

∫_{a_x}^{b_x} ∫_{a_y(x)}^{b_y(x)} f(x,y) dx dy = ∫_{a_x}^{b_x} F_x(x) dx, (10.88)
F_x(x) = ∫_{a_y(x)}^{b_y(x)} f(x,y) dy.

For each particular outer argument x_i ∈ [a_x, b_x] (see Figure 10.7), the inner integral F_x(x_i) may be evaluated on an independent grid, which is completely determined by the local behavior of the integrand and

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_389_0.png)

FIGURE 10.7 The “inner” integration with respect to y operates on independent adaptive grids for each single argument x_i of the “outer” integration.
