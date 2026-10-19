# 26.4.4

# Solution via Inversion, Elimination

An elegant (but alas not most efficient) solution to (26.36) is by matrix inversion:

[R] = [F]⁻¹[V].
(26.37)

Because the inversion of even complex matrices is a standard routine in mathematical libraries, (26.37) is a direct solution for the R amplitude. Unless you need the inverse for other purposes (like calculating wave functions), a more efficient approach is to use Gaussian elimination to find an [R] that solves [F][R] = [V] without computing the inverse.

# Listing 26.2 Scatt.py solves the Lippmann–Schwinger integral equation for scattering from a delta-shell potential. The singular integral equations are regularized by a subtraction, converted to matrix equations using Gaussian grid points, and then solved with matrix library routines.

```
# Scatt.py: Soln p space Lippmann Schwinger for scattering

from visual import *
from visual.graph import *
import numpy.linalg as lina    # Numpy's LinearAlgebra

def gauss(npts, job, a, b, x, w):
    m = i = j = t = t1 = pp = p1 = p2 = p3 = 0.
    eps = 3.E-14                # Accuracy: ******ADJUST THIS******!
    m = (npts + 1)/2
    for i in arange(1, m + 1):
        t = cos(math.pi*(float(i) - 0.25)/(float(npts) + 0.5))
        t1 = 1
        while( (abs(t - t1)) >= eps):
            p1 = 1. ;  p2 = 0.
            for j in range(1, npts + 1):
                p3 = p2;  p2 = p1
                p1 = ((2.*float(j)-1)*t*p2 - (float(j)-1.)*p3)/(float(j))
                pp = npts*((t*p1 - p2)/(t*t - 1.))
                t1 = t;  t = t1 - p1/pp
            x[i - 1] = - t;  x[npts - i] = t
            w[i - 1] = 2./( (1. - t*t)*pp*pp)
            w[npts - i] = w[i - 1]
    if (job == 0):
        for i in range(0, npts):
            x[i] = x[i]*(b - a)/2. + (b + a)/2.
            w[i] = w[i]*(b - a)/2.
    if (job == 1):
        for i in range(0, npts):
            xi = x[i]
            x[i] = a*b*(1. + xi) / (b + a - (b - a)*xi)
            w[i] = w[i]*2.*a*b*b / ( (b + a - (b-a)*xi)*(b + a - (b-a)*xi) )
    if (job == 2):
        for i in range(0, npts):
            xi = x[i]
            x[i] = (b*xi + b + a + a) / (1. - xi)
            w[i] = w[i]*2.*(a + b)/((1. - xi)*(1. - xi))

graphscatt = gdisplay(x=0, y=0, xmin=0, xmax=6,ymin=0, ymax=1, width=600, height=400,
```