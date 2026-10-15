
nn = [0, n, 2*n, 3*n]
col = ["", "blue", "green", "red"]
sty = [0, 1, 1, 1]
MultiPlot(x,y,y,nn,col,sty,3,10,
    0e0,0e0,0,0e0,0e0,0,0.10,0.45,0.15,0.85,
    "lambda (micron)","u","Spectral energy density")

MultiPlot(x,z,z,nn,col,sty,3,10,
    0e0,0e0,0,0e0,0e0,0,0.60,0.95,0.15,0.85,
    "lambda (micron)","du","Derivative of energy density")

#--------------------------------------------------------------------
T = 5778e0                     # temperature of sun's photosphere
lam0 = h*kB / (kB*T)           # reference wavelength
K = 8e0 * pi * kB * T / pow(lam0,4)   # factor of u(lam)

fmin = 1e10; fmax = -1e10       # positions of maximum and minimum of du
for i in range(1,n+1):
    lam = (i-1)*h; f = du(lam)
    if (f > fmax): fmax = f; lam_1 = lam          # maximum
    if (f < fmin): fmin = f; lam_2 = lam          # minimum

lam_max = 0.5e0 * (lam_1 + lam_2)               # find zero of du in [lam_1,lam_2]
(lam_max,iierr) = NewtonNumDrv(du,lam_1,lam_2,lam_max)   # initial approximation
print("Wien's law:")
print("T = {0:4.0f} K".format(T))
print("lambda_max = {0:e} m".format(lam_max))
print("lambda_max * T = {0:e} m K".format(lam_max * T))   # 2.897768e-3 m K

MainLoop()

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_185_0.png)

FIGURE 6.10 Planck's law of black-body radiation: spectral energy density u(λ, T) (left panel) and derivative ∂u(λ, T)/∂λ, for T = 4000, 5000, and 6000 K, corresponding to major peaks of increasing magnitude.

## PROBLEM 6.6

Find the intersection points of the following circle and parabola:

(x − 1)² + y² = 4²,

y = x² − 3,

by using the pair of routines Jacobian and NewtonSys from the modules roots.py and, respectively, roots.h. Use Figure 6.11 to find initial guesses for the coordinates of the intersection points.

### Solution

Rewrite the system of equations as

f₁(x₁,x₂) ≡ (x₁ − 1)² + x₂² − 4² = 0,
f₂(x₁,x₂) ≡ x₁² − x₂ − 3 = 0.

The Python implementation is given in Listing 6.20, the C/C++ version is available as supplementary material (P06-NewtonSys1.cpp), and the graphical output is depicted in Figure 6.11.

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_186_0.png)

FIGURE 6.11 Intersection points of the circle (x − 1)² + y² = 4² and the parabola y = x² − 3, to be determined by Program 6.20.

### Listing 6.20 Intersection Points of a Circle and a Parabola (Python Coding)

```
# Intersection of circle and parabola
from math import *
from roots import *

def Func(f, x, n):                # zeros: (-2.295, 2.267), (2.583, 3.673)
    f[1] = pow(x[1]-1,2) + x[2]*x[2] - 16e0
    f[2] = x[1]*x[1] - x[2] - 3e0

# main

n = 2
f = [0]*(n+1)
```

```
x = [0]*(n+1)
dx = [0]*(n+1)

x[1] = -5e0; x[2] = 5e0        # 1st initial approximation -> (-2.295, 2.267)
(dx,ierr) = NewtonSys(Func,x,n)
Func(f,x,n)

print("Solution 1:")
print("               x            dx            f")
for i in range(1,n+1):
    print("{0:d}  {1:15.7e}  {2:7.0e}  {3:7.0}".format(i,x[i],dx[i],f[i]))

x[1] = 5e0; x[2] = 5e0    # 2nd initial approximation -> (2.583, 3.673)
(dx,ierr) = NewtonSys(Func,x,n)
Func(f,x,n)

print("\nSolution 2:")
print("               x            dx            f")
for i in range(1,n+1):
    print("{0:d}  {1:15.7e}  {2:7.0e}  {3:7.0}".format(i,x[i],dx[i],f[i]))
```

## PROBLEM 6.7

Solve the system of nonlinear equations (S. M. Tang and W. C. Kok, J. Phys. A: Math. Gen, 18, 2691 (1985)):

f₁(x₁,x₂,x₃) ≡ x₃ − x₁x₂x₃ = 0,
f₂(x₁,x₂,x₃) ≡ x₁ + x₂ + x₃ = 0,
f₃(x₁,x₂,x₃) ≡ x₁x₂ + x₂x₃ + x₃x₁ = 0.

### Solution

The Python implementation is given in Listing 6.21 and the C/C++ version is available as supplementary material (P06-NewtonSys2.cpp).

### Listing 6.21   System of Three Nonlinear Equations (Python Coding)

```
# Newton-Raphson method for systems of non-linear equations
from math import *
from roots import *

def Func(f, x, n):                                   # zero: (0, 0, 0)
    f[1] = x[3] - x[1]*x[2]*x[3]
    f[2] = x[1] + x[2] + x[3]
    f[3] = x[1]*x[2] + x[2]*x[3] + x[3]*x[1]

# main

n = 3
f = [0]*(n+1)
x = [0]*(n+1)
dx = [0]*(n+1)

x[1] = 1e0; x[2] = 2e0; x[3] = 3e0                 # initial approximation

(dx,ierr) = NewtonSys(Func,x,n)
Func(f,x,n)
```

```
print("Solution:")
print("          x           dx           f")
for i in range(1,n+1):
    print("{0:d}  {1:15.7e}  {2:7.0e}  {3:7.0e}".format(i,x[i],dx[i],f[i]))
```

## References and Suggested Further Reading

Bakhvalov, N. S. 1977. *Numerical Methods: Analysis, Algebra, Ordinary Differential Equations.* Moscow: MIR Publishers.
Beu, T. A. 2004. *Numerical Calculus in C* (3rd ed., in Romanian). Cluj-Napoca: MicroInformatica.
Burden, R. and J. Faires. 2010. *Numerical Analysis* (9th ed.). Boston: Brooks/Cole, Cengage Learning.
Demidovich, B. and I. Maron. 1987. *Computational Mathematics* (4th ed.). Moscow: MIR Publishers.
Hecht, E. 2002. *Optics* (4th ed.). San Francisco: Addison-Wesley.
Mottmann, J. 1986. Locating an orbiting object. *American Journal of Physics* 54, 838–842.
Ortega, J. M. and W. C. Rheinboldt. 2000. *Iterative Solution of Nonlinear Equations in Several Variables.* New York: Society for Industrial and Applied Mathematics.
Press, W. H., S. A. Teukolsky, W. T. Vetterling, and B. P. Flannery. 2007. *Numerical Recipes* (3rd ed.): *The Art of Scientific Computing.* Cambridge: Cambridge University Press.
Toda, M., R. Kubo, and N. Saitô. 1998. *Statistical Physics I, Equilibrium Statistical Mechanics* (2nd ed.). Heidelberg: Springer.
Toma, M. and I. Odăgescu. 1980. *Numerical Methods and Subroutines* (in Romanian). Bucharest: Editura Tehnică.
Williams, D. R. 2013. NASA, Lunar and Planetary Science, Sun Fact Sheet. http://nssdc.gsfc.nasa.gov/planetary/factsheet/sunfact.html.

## 7

## Systems of Linear Equations

### 7.1 Introduction

Linear systems of equations are almost ubiquitous in applied mathematics. They may appear naturally in the mathematical formulation of the problem or, as a result of applying certain linear approximation methods for solving the original problem. Discretization of boundary value problems for differential equations by finite difference schemes or interpolation with piecewise smooth functions are just two typical examples of numerical methods leading to linear systems.

The methods for solving linear systems are certainly central to numerical analysis and can be essentially divided into two broad classes: direct methods and iterative methods.

Direct methods are finite algorithms for which the number of elementary operations required to obtain the solution directly depends on the size of the linear system. Direct methods are affected only by round-off errors, feature which makes them preferable when the system size and the number of elementary operations involved remain moderate. Despite its conceptual simplicity among the direct methods, the implementation of Cramer's rule (based on determinants) is not particularly efficient in terms of operations and, therefore, it is not recommendable in real-world applications. Examples of frequently used direct methods are Gaussian and Gauss–Jordan elimination, LU factorization, Cholesky decomposition, and so on.

Iterative methods enable finding solutions of linear systems as limits of virtually infinite iterative processes. Since only a finite number of iterations can be performed, the unavoidable roundoff errors are also accompanied by truncation errors. Among the advantages of iterative methods, the extreme simplicity and straightforward implementation outweigh the necessity of a more elaborate error control and make them suitable in cases that are intractable by direct methods. In addition, iterative methods can be used to refine solutions obtained by other methods. The most common examples of iterative algorithms are the Jacobi, Gauss–Seidel, and relaxation methods.

### 7.2 Gaussian Elimination with Backward Substitution

One of the classical direct methods for solving linear systems is known as Gaussian elimination, being named after Carl Friedrich Gauss, to whom it is attributed. Apparently, however, the method was already known in China over 2000 years ago, while Isaac Newton was using it at the beginning of the eighteenth century, almost 100 years before Gauss (Grcar 2011).

The basic concept of the Gaussian elimination implies two distinct phases: (1) transformation of the system by elementary row operations into an equivalent system with upper triangular coefficient matrix (with all entries below the main diagonal equal to 0); and (2) solution of the equivalent triangular system by specific recurrent techniques. The initial transformation of the system is equivalent to eliminating in sequence the unknowns from the successive equations and is therefore named forward elimination. The subsequent recurrent solution of the equivalent system with triangular matrix consists of expressing the
