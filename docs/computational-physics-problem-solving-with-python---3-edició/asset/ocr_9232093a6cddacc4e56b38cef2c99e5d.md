# Listing 26.1 Bound.py solves the Lippmann–Schwinger integral equation for bound states within a delta-shell potential. The integral equations are converted to matrix equations using Gaussian grid points, and they are solved with linalg.

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

+   1. Write a program, or modify ours, to solve the integral equation (26.9) for the delta-shell potential (26.16). Either find the $E_n$’s for which the determinant vanishes or, find the eigenvalues and eigenvectors for this H.
+   2. Set the scale by setting $2\mu = 1$ and $b = 10$.
+   3. Set up the potential and Hamiltonian matrices $V(i, j)$ and $H(i, j)$ for Gaussian quadrature integration with at least $N = 16$ grid points.