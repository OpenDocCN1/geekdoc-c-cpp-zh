
void Jacobian(double x[], double **jac, int n,
                void Func(double[],double[],int))
//-------------------------------------------------------------
// Calculates the Jacobian of a system of n real functions with n variables
// using central finite differences
// x[]      - point at which the Jacobian is evaluated
// jac[][]  - Jacobian
// n        - space dimension
// Func     - user function returning the function values at point x
//            void Func(double f[], double x[], int n);
//-------------------------------------------------------------
{
    const double eps = 1e-10;
    int i, j;
    double h, h2, *fm, *fp, x0;

    fm = Vector(1,n);
    fp = Vector(1,n);

    for (j=1; j<=n; j++) {                         // loop over coordinates
        x0 = x[j];                                 // store x[j]
        h = x0 ? eps*fabs(x0) : eps;               // step-size
        x[j] = x0 - h; Func(fm,x,n);               // decrement x[j]
        x[j] = x0 + h; Func(fp,x,n);               // increment x[j]
        h2 = 1e0/(2e0*h);
        for (i=1; i<=n; i++) jac[i][j] = (fp[i] - fm[i]) * h2;   // Jacobian
        x[j] = x0;                                 // restore x[j]
    }

    FreeVector(fm,1);
    FreeVector(fp,1);
}

//=====================================================================
int NewtonSys(void Func(double [], double [], int),
              double x[], double dx[], int n)
//-------------------------------------------------------------
// Determines a n-dimensional real zero of a system of n real functions by
// Newton-Raphson method.
// Func - user function returning the function values f[] for arguments x[]
//        void Func(double f[], double x[], int n);
// x[]  - initial approximation (input), solution (output)
// dx[] - error estimates of the solution components (output)
// n    - order of system
// ierr - error code: 0 - normal execution
//                1 - max. number of iterations exceeded
// Calls: Jacobian - computes Jacobian
//        MatInv   - inverts (n x n) matrix (in linsys.h)
//-------------------------------------------------------------
{
    const double eps = 1e-14;                     // precision for cumulated error
    const int itmax = 100;                        // max. no. of iterations
    double *f, **jac;
    double det, err, sum;
    int i, ierr, it, j;

    f   = Vector(1,n);
    jac = Matrix(1,n,1,n);

    for (it=1; it<=itmax; it++) {
        Func(f,x,n);                                 // functions
        Jacobian(x,jac,n,Func);                      // Jacobian
        MatInv(jac,n,det);                           // inverse Jacobian

        if (det) {                                   // corrections
            for (i=1; i<=n; i++) {                   // non-singular Jacobian
                sum = 0e0;
                for (j=1; j<=n; j++) sum -= jac[i][j] * f[j];
                dx[i] = sum;
            }
        } else { for (i=1; i<=n; i++) dx[i] = -f[i]; }   // singular Jacobian

        err = 0e0;
        for (i=1; i<=n; i++) {
            x[i] += dx[i];                           // new approximation
            err += fabs(f[i]);                       // cumulate error
        }
        if (err <= eps) break;                       // check convergence
    }

    FreeVector(f,1);
    FreeMatrix(jac,1,1);

    ierr = 0;
    if (it >= itmax)
        { ierr = 1; printf("NewtonSys: max. no. of iterations exceeded !\n"); }
    return ierr;
}
#endif

## 6.10 Problems

The Python and C/C++ programs for the following problems may import the functions developed in this chapter from the modules roots.py and roots.h, respectively, which are available as supplementary material. For creating runtime plots, the graphical routines contained in the libraries graphlib.py and graphlib.h may be employed.

### PROBLEM 6.1

Using the routine Bisect, write a C/C++ program (analogous to the Python program 6.2) for finding the zeros of the function

f(x) = (x⁴ − 5x² + 4) sin 2x.

Consider the search interval [−3.5, 3.5] and, prior to applying the bisection method, separate the zeros in subintervals of width h = 0.1. For each found zero, check the accuracy by evaluating the corresponding function value.

# Solution

The implementation is shown in Listing 6.16.

## Listing 6.16　Real Roots of Functions (C/C++ Coding)

```
// Real roots of a real function by the bisection method
#include <stdio.h>
#include <math.h>
#include "roots.h"

double func(double x)
{
    return (x*x*x*x - 5e0*x*x + 4e0) * sin(2e0*x);
}

int main()
{
    double a, b, h, x, xmin, xmax;
    int ierr;

    xmin = -3.5e0;                         // limits of root search domain
    xmax =  3.5e0;
    h = 0.1e0;                            // width of root separation intervals

    a = xmin;
    while (a < xmax) {                    // root separation loop
        b = a + h;                         // search interval [a,b]
        ierr = Bisect(func,a,b,x);
        if ((ierr == 0) && (x != b))
            printf("x = %8.5f in (%6.2f,%6.2f)  f(x) = %7.0e\n",x,a,b,func(x));
        a = b;                             // shift left boundary
    }
}
```

### PROBLEM 6.2

Modify the routines `Bisect` and `Secant` in such a way as to return the number of iterations they require to achieve convergence, namely the final value of the iteration counter `it`. For instance, declare it global, return it via the parameter list, or, simply print out its values in the routines.

Use the modified routines comparatively to solve the equation

$$x - \sin x - 0.25 = 0,$$

and assess the convergence speed of the two methods, using the search interval $[-30, 30]$ for the bisection method, and the initial approximation $x_0 = -30$ for the secant method.

# Solution

Python and C/C++ sample programs are provided as supplementary material in the files `P06-CompareZeros.py` and `P06-CompareZeros.cpp`.

### PROBLEM 6.3

*Kepler’s equation* (derived by Johannes Kepler in 1609) plays a central role in classical celestial mechanics, because it enables the calculation of angular positions for orbiting objects. For an elliptical orbit, it relates the *mean anomaly* $M$, the *eccentric anomaly* $E$, and the eccentricity $e = \sqrt{1 - b^2/a^2}$ ($a > b$ are semiaxes):

$$M = E - e \sin E. \tag{6.58}$$

The “anomalies” are defined by astronomers as angular positions: the mean anomaly M is the angular position of the object on a fictitious circular orbit, and, assuming constant angular velocity, it can be related to the lapse of time since the passage through the perihelion:

M = 2π/T (t − t0),  (6.59)

where T is the orbital period and t0 is the time when the object was at the perihelion.

For the Halley comet (Mottmann 1986), the relevant parameters have the values: e = 0.9672671, T = 75.9600 years, and t0 = 1986.1113 years (on February 9, 1986).

- a. Find the eccentric anomaly E of the Halley comet on April 1, 1986, for t = 1986.2491. To this end, plot the function
- f(E) = E − e sin E − M,  (6.60)
- for E ∈ [0,1] to make sure that the interval contains a single zero and determine it by Newton’s method.
- b. Plot E = E(t) for a whole period of revolution by using Newton’s method to solve
- E − e sin E − M(t) = 0,  (6.61)
- with a time step Δt = T/100. Use as initial approximation for each new moment of time, ti = t0 + (i − 1)Δt, the previous value E(ti−1), starting with E(t0) = 0.

# Solution

The Python implementation is given in Listing 6.17, the C/C++ version is available as supplementary material (P06-Kepler.cpp), and the graphical output is depicted in Figure 6.8.

## Listing 6.17 Solution of Kepler’s Equation (Python Coding)

```
# Solution of Kepler's equation
from math import *
from roots import *
from graphlib import *

pi2 = 2e0 * pi

def Func(E):
    global e, M                 # eccentricity, mean anomaly
    f = E - e * sin(E) - M
    df = 1e0 - e * cos(E)
    return (f, df)

# main
n = 101
x = [0]*(n+1); y = [0]*(n+1)

GraphInit(1200,600)

e = 0.9672671e0                # Halley comet (Mottmann 1986):
                               # eccentricity
T = 75.96e0                    # period
t0 = 1986.1113e0               # time at perihelion
#------------------------------------------------------------
t = 1986.2491e0
M = pi2 / T * (t - t0)         # mean anomaly
```
