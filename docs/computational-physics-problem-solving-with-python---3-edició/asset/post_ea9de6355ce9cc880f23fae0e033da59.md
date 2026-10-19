
## 26.2.2 Delta-Shell Potential (Model)

To keep things simple and to have an analytic answer to compare with, we consider the local delta-shell potential:

$$V(r) = \frac{\lambda}{2\mu}\,\delta(r - b)\ .$$ (26.15)

This might be a good model for an interaction that occurs when two particles are predominantly a fixed distance $b$ apart. We use (26.4) to determine its momentum–space representation:

$$V(k', k) = \int_{0}^{\infty} \frac{\sin(k' r)}{k' k}\,\frac{\lambda}{2\mu}\,\delta(r - b)\,\sin(k r)\,dr = \frac{\lambda}{2\mu}\,\frac{\sin(k' b)\sin(k b)}{k' k}\ .$$ (26.16)

*Beware:* We have chosen this potential because it is easy to evaluate the momentum–space matrix element of the potential. However, its singular nature in $r$ space leads to (26.16) having a very slow falloff in $k$ space, and this causes the integrals to converge so slowly that numerics are not as precise as we would like.

If the energy is parameterized in terms of a wave vector $\kappa$ by $E_n = -\kappa^2 / 2\mu$, then for this potential there is, at most, one bound state and it satisfies the transcendental equation (Gottfried, 1966)

$$\mathrm{e}^{-2\kappa b} - 1 = \frac{2\kappa}{\lambda}\ .$$ (26.17)

Note that bound states occur only for attractive potentials. For the present case, this requires $\lambda < 0$.

**Exercise** Pick some values of $b$ and $\lambda$ and verify that (26.17) can be solved for $\kappa$.

## 26.2.3 Binding Energies Solution

An actual computation may follow two paths. The first calls subroutines to evaluate the determinant of the $[\mathbf{H} - E_n I]$ matrix in (26.14), and then to *search* for those values of energy for which the computed determinant vanishes. This provides $E_n$, but not wave functions. The other approach calls an eigenproblem solver that may give some or all eigenvalues and eigenfunctions. In both the cases, the solution is obtained iteratively, and you may be required to guess starting values for both the eigenvalues and eigenvectors. In Listing 26.1, we present our solution of the integral equation for bound states of the delta-shell potential using the NumPy matrix library and the *gauss* method for Gaussian quadrature points and weights.

### Listing 26.1 Bound.py solves the Lippmann–Schwinger integral equation for bound states within a delta-shell potential. The integral equations are converted to matrix equations using Gaussian grid points, and they are solved with linalg.

```
# Bound.py: Bound state solutn of Lippmann—Schwinger equation in p space
from visual import *
from numpy import*
from numpy.linalg import*

min1 =0.;   max1 =200.;  u =0.5;   b =10.

def gauss(npts,a,b,x,w):
    pp = 0.;  m = (npts + 1)//2;   eps = 3.E-10        # Accuracy: ADJUST!
    for i in range(1,m+1):
        t = cos(math.pi*(float(i)-0.25)/(float(npts) + 0.5))
        t1 = 1
        while((abs(t-t1)) >= eps):
            p1 = 1.;  p2 = 0.;
            for j in range(1,npts+1):
                p3 = p2
                p2 = p1
                p1=((2*j-1)*t*p2-(j-1)*p3)/j
            pp = npts*(t*p1-p2)/(t*t-1.)
            t1 = t;  t = t1 - p1/pp
        x[i-1] = -t
        x[npts-i] = t
        w[i-1] = 2./((1.-t*t)*pp*pp)
        w[npts-i] = w[i-1]
    for i in range(0,npts):
        x[i] = x[i]*(b-a)/2. + (b + a)/2.
        w[i] = w[i]*(b-a)/2.

for M in range(16, 32, 8):
    z=[-1024, -512, -256, -128, -64, -32, -16, -8, -4, -2]
    for lambd in z:
        A = zeros((M,M), float)                # Hamiltonian
        WR = zeros((M), float)                 # Eigenvalues , potential
        k = zeros((M), float); w = zeros((M),float);   # Pts & wts
        gauss(M, min1, max1, k, w)             # Call gauss points
        for i in range(0,M):                   # Set Hamiltonian
            for j in range(0,M):
                VR = lambd/2/u*sin(k[i]*b)/k[i]*sin(k[j]*b)/k[j]
                A[i,j] = 2./math.pi*VR*k[j]*k[i]*w[j]
                if (i == j):
                    A[i,j] += k[i]*k[i]/2/u
        Es, evectors = eig(A)
        realev = Es.real                        # Real eigenvalues
        for j in range(0,M):
            if (realev[j])>0:
                print(" M ",size, lambd, ReE = ",M,",lambd,",",realev[j])
                break
```

- 1. Write a program, or modify ours, to solve the integral equation (26.9) for the delta-shell potential (26.16). Either find the $E_n$’s for which the determinant vanishes or, find the eigenvalues and eigenvectors for this H.
- 2. Set the scale by setting $2\mu = 1$ and $b = 10$.
- 3. Set up the potential and Hamiltonian matrices $V(i, j)$ and $H(i, j)$ for Gaussian quadrature integration with at least $N = 16$ grid points.
- 4. Adjust the value and sign of λ for bound states. A good approach is to start with a large negative value for λ and then make it less negative. You should find that the eigenvalue moves up in energy.
- 5. *Note:* Your eigenenergy solver may return several eigenenergies. The true bound state will be at negative energy and change little as the number of grid points changes. The others are numerical artifacts.
- 6. Try increasing the number of grid points in steps of 8, for example, 16, 24, 32, 64, ..., and see how the energy changes.
- 7. Extract the best value for the bound-state energy and estimate its precision by seeing how it changes with the number of grid points.
- 8. If you are solving the eigenvalue problem, check your solution by comparing the RHS and LHS in the matrix multiplication [H][ψ_n] = E_n[ψ_n].
- 9. Verify that, regardless of the potential's strength, there is only a single bound state and that it gets deeper as the magnitude of λ increases. Compare with (26.17).

## 26.2.4 Wave Function (Exploration)

- 1. Determine the momentum–space wave function ψ_n(k) using an eigen problem solver. Does ψ_n(k) fall off at k → ∞? Does it oscillate? Is it well behaved at the origin?
- 2. Using the same points and weights as used to evaluate the integral in the integral equation, determine the coordinate-space wave function via the Bessel transform

ψ_n(r) = ∫_0^∞ dk ψ_n(k) \frac{\sin(kr)}{kr} k^2 .

Does ψ_n(r) fall off as you would expect for a bound state? Does it oscillate? Is it well behaved at the origin?
- 3. Compare the r dependence of this ψ_n(r) to the analytic wave function:

ψ_n(r) ∝ \begin{cases} e^{-\kappa r} - e^{\kappa r} , & \text{for } r < b , \\ e^{\kappa r} , & \text{for } r > b . \end{cases}

## 26.3 Scattering States of Nonlocal Potentials

Problem Again we have a particle interacting with the nonlocal potential discussed for bound states (Figure 26.3a), only now the particle has sufficiently high energy that it scatters from rather than binds with the medium. Your problem is to determine the scattering cross section for scattering from a nonlocal potential.

![](img/bccda43674e4a93dee81c749eba8d2f7_621_0.png)

Figure 26.3 (a) A projectile (dark particle at r) scattering from a dense medium. (b) The same process viewed in the CM system where the projectile and target always have equal and opposite momenta.

## 26.4 Lippmann–Schwinger Equation (Theory)

Because experiments measure scattering amplitudes and not wave functions, it is more direct to have a theory dealing with amplitudes rather than wave functions.³) An integral form of the Schrödinger equation dealing with the scattering amplitude R is the Lippmann–Schwinger equation:

```
R(k′, k) = V(k′, k) + (2/π) P ∫₀^∞ dp [p² V(k′, p) R(p, k) / ((k₀² − p²)/2μ)] , (26.20)
```

where the symbol P in (26.20) indicates the Cauchy principal-value prescription for avoiding the singularity arising from the zero of the denominator (we discuss how to do that next). As for the bound-state problem, this equation is for partial wave l = 0 and ħ = 1. In (26.20), the momentum k₀ is related to the energy E and the reduced mass μ by

```
E = k₀² / (2μ) , μ = (m₁ m₂)/(m₁ + m₂) . (26.21)
```

The initial and final COM momenta k and k′ are the momentum–space variables. The experimental observable that results from a solution of (26.20) is the diagonal matrix element R(k₀, k₀), which is related to the scattering phase shift δ₀ and thus the cross section:

```
R(k₀, k₀) = − tan δₗ / ρ , ρ = 2μ k₀ . (26.22)
```

Note that (26.20) is not just the evaluation of an integral, it is an integral equation in which R(p, k) is integrated over all p. Yet because R(p, k) is unknown, the integral cannot be evaluated until after the equation is solved!

> 3) To make the presentation simpler, but still perfectly valid, we solve for the reaction matrix R, but call it the scattering amplitude.
