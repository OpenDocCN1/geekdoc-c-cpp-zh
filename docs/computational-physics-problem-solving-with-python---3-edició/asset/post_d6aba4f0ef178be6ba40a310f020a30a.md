
## 26.4.1 Singular Integrals (Math)

A singular integral

$$
\mathcal{G}=\int_{a}^{b} g(k)\,\mathrm{d}k,
\tag{26.23}
$$

is one in which the integrand \(g(k)\) is singular at a point \(k_0\) within the integration interval \([a,b]\), yet with the integral \(\mathcal{G}\) remaining finite. (If the integral itself were infinite, we could not compute it.) Unfortunately, computers are notoriously bad at dealing with infinite numbers, and if an integration point gets too near the singularity, overwhelming subtractive cancellation or overflow may occur. Consequently, we apply some results from complex analysis before evaluating singular integrals numerically.⁴

4) Singh and Thompson (1993) describe a different approach using Maple and Mathematica.

In Figure 26.4, we show three ways to avoid the singularity of an integrand. The paths in Figure 26.4a and b move the singularity slightly off the real \(k\)-axis by giving the singularity a small imaginary part \(\pm i\epsilon\). The Cauchy principal-value prescription \(\mathcal{P}\) in Figure 26.4c is seen to follow a path that “pinches” both sides of the singularity at \(k_0\), but does not pass through it:

$$
\mathcal{P}\int_{-\infty}^{+\infty} f(k)\,\mathrm{d}k = \lim_{\epsilon\to 0}\left[\int_{-\infty}^{k_0-\epsilon} f(k)\,\mathrm{d}k + \int_{k_0+\epsilon}^{+\infty} f(k)\,\mathrm{d}k\right].
\tag{26.24}
$$

The preceding three prescriptions are related by the identity

$$
\int_{-\infty}^{+\infty} \frac{f(k)\,\mathrm{d}k}{k - k_0 \pm i\epsilon} = \mathcal{P}\int_{-\infty}^{+\infty} \frac{f(k)\,\mathrm{d}k}{k - k_0} \mp i\pi f(k_0),
\tag{26.25}
$$

which follows from Cauchy's residue theorem.

![](img/bccda43674e4a93dee81c749eba8d2f7_622_0.png)

*Figure 26.4* Three different paths in the complex \(k'\) plane used to evaluate line integrals when there are singularities. Here the singularities are at \(k\) and \(-k\), and the integration variable is \(k'\).

## 26.4.2 Numerical Principal Values

A direct numerical evaluation of the principal value limit (26.24) is troublesome because of the large cancellations that occur near the singularity. A better algorithm follows from the mathematical theorem

$$
\mathcal{P}\int_{-\infty}^{+\infty} \frac{dk}{k - k_0} = 0.
\tag{26.26}
$$

This equation says that the curve of \(1/(k - k_0)\) as a function of \(k\) has equal and opposite areas on both sides of the singular point \(k_0\). If we break the integral up into one over positive \(k\) and one over negative \(k\), a change of variable \(k \to -k\) permits us to rewrite (26.26) as

$$
\mathcal{P}\int_{0}^{+\infty} \frac{dk}{k^2 - k_0^2} = 0.
\tag{26.27}
$$

We observe that the principal-value exclusion of the singular point's contribution to the integral is equivalent to a simple subtraction of the zero integral (26.27):

$$
\mathcal{P}\int_{0}^{+\infty} \frac{f(k)\,dk}{k^2 - k_0^2} = \int_{0}^{+\infty} [f(k) - f(k_0)]\frac{dk}{k^2 - k_0^2}.
\tag{26.28}
$$

Note that there is no \(\mathcal{P}\) on the RHS of (26.28) because the integrand is no longer singular at \(k = k_0\) (it is proportional to \(df/dk\)) and can therefore be evaluated numerically using the usual rules. The integral (26.28) is called the Hilbert transform of \(f\) and also arises in subjects like inverse problems.

## 26.4.3 Reducing Integral Equations to Matrix Equations (Method)

Now that we can handle singular integrals, we go back to reducing the integral equation (26.20) to a set of linear equations that can be solved with matrix methods. We start by rewriting the principal-value prescription as a definite integral (Haftel and Tabakin, 1970):

$$
R(k', k) = V(k', k) + \frac{2}{\pi}\int_{0}^{+\infty} \frac{dp\,p^2\, V(p, k)\, R(p, k)}{(k_0^2 - p^2)/(2\mu)} .
$$

We convert this integral equation \(R\) to linear equations by approximating the integral as a sum over \(N\) integration points (usually Gaussian) \(k_j\) with weights \(w_j\):

$$
R(k, k_0) \approx V(k, k_0) + \frac{2}{\pi}\sum_{j=1}^N \frac{k_j^2\, V(k, k_j)\, R(k_j, k_0)\, w_j}{(k_0^2 - k_j^2)/(2\mu)}
- \frac{2}{\pi}\, k_0^2\, V(k, k_0)\, R(k_0, k_0)\sum_{m=1}^N \frac{w_m}{(k_0^2 - k_m^2)/(2\mu)}.
\tag{26.30}
$$

We note that the last term in (26.30) implements the principal-value prescription and cancels the singular behavior of the previous term. Equation (26.30) contains the \((N + 1)\) unknowns \(R(k_j, k_0)\) for \(j = 0, \ldots, N\). We turn it into \((N + 1)\) simultaneous equations by evaluating it for \((N + 1)\) \(k\) values on a grid (Figure 26.2) consisting of the observable momentum \(k_0\) and the integration points:

$$
k = k_i = \begin{cases}
k_j, & j = 1, \ldots, N \quad (\text{quadrature points}),\\
k_0, & i = 0 \quad (\text{observable point}).
\end{cases}
\tag{26.31}
$$

There are now \((N + 1)\) linear equations for \((N + 1)\) unknowns \(R_i \equiv R(k_i, k_0)\):

$$
R_i = V_i + \frac{2}{\pi}\sum_{j=1}^N \frac{k_j^2\, V_{ij}\, R_j\, w_j}{(k_0^2 - k_j^2)/(2\mu)}
- \frac{2}{\pi}\, k_0^2\, V_{i0}\, R_0\sum_{m=1}^N \frac{w_m}{(k_0^2 - k_m^2)/(2\mu)}.
\tag{26.32}
$$

We express these equations in the matrix form by combining the denominators and weights into a single denominator vector \(D\):

$$
D_i = \begin{cases}
+\frac{2}{\pi}\frac{w_i k_i^2}{(k_0^2 - k_i^2)/(2\mu)}, & i = 1, \ldots, N,\\[2mm]
-\frac{2}{\pi}\sum_{j=1}^N \frac{w_j k_0^2}{(k_0^2 - k_j^2)/(2\mu)}, & i = 0.
\end{cases}
\tag{26.33}
$$

The linear equations (26.32) now assume the matrix form

$$
\mathbf R - \mathbf D \mathbf V \mathbf R = [\mathbf 1 - \mathbf D \mathbf V]\mathbf R = \mathbf V,
\tag{26.34}
$$

where \(\mathbf R\) and \(\mathbf V\) are column vectors of length \(N + 1\):

$$
[\mathbf R] = \begin{pmatrix} R_{0,0} \\ R_{1,0} \\ \vdots \\ R_{N,0} \end{pmatrix}, \qquad
[\mathbf V] = \begin{pmatrix} V_{0,0} \\ V_{1,0} \\ \vdots \\ V_{N,0} \end{pmatrix}.
\tag{26.35}
$$

We call the matrix \([\mathbf 1 - \mathbf D \mathbf V]\) in (26.34) the wave matrix \(\mathbf F\) and write the integral equation as the matrix equation

$$
[\mathbf F][\mathbf R] = [\mathbf V], \qquad F_{ij} = \delta_{ij} - D_j V_{ij}.
\tag{26.36}
$$

With \(\mathbf R\) the unknown vector, (26.36) is in the standard form \(\mathbf A\mathbf X = \mathbf B\), which can be solved by the mathematical subroutine libraries discussed in Chapter 6.

## 26.4.4 Solution via Inversion, Elimination

An elegant (but alas not most efficient) solution to (26.36) is by matrix inversion:

$$
[\mathbf R] = [\mathbf F]^{-1}[\mathbf V].
\tag{26.37}
$$

Because the inversion of even complex matrices is a standard routine in mathematical libraries, (26.37) is a direct solution for the \(\mathbf R\) amplitude. Unless you need the inverse for other purposes (like calculating wave functions), a more efficient approach is to use Gaussian elimination to find an \(\mathbf R\) that solves \([\mathbf F][\mathbf R] = [\mathbf V]\) without computing the inverse.

**Listing 26.2** *Scatt.py solves the Lippmann–Schwinger integral equation for scattering from a delta-shell potential. The singular integral equations are regularized by a subtraction, converted to matrix equations using Gaussian grid points, and then solved with matrix library routines.*

```python
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

graphscatt = gdisplay(x=0, y=0, xmin=0, xmax=6, ymin=0, ymax=1, width=600, height=400,
                      title='S Wave Cross Section vs E', xtitle='kb', ytitle='[sin(delta)]**2')
sin2plot = gcurve(color=color.yellow)
M = 27;      b = 10.0;      n = 26
k = zeros((M),float);      x = zeros((M),float);      w = zeros((M),float)
Finv = zeros((M,M),float);  F = zeros((M,M),float);  D = zeros((M),float)
V = zeros((M),float);      Vvec = zeros((n+1,1),float)
scale = n/2;               lambd = 1.5

gauss(n, 2, 0., scale, k, w)                     # Set up points & wts
ko = 0.02
for m in range(1,901):
    k[n] = ko
    for i in range(0, n):  D[i]=2/pi*w[i]*k[i]*k[i]/(k[i]*k[i]-ko*ko) #D
    D[n] = 0.
    for j in range(0,n):  D[n]=D[n]+w[j]*ko*ko/(k[j]*k[j]-ko*ko)
    D[n] = D[n]*(-2./pi)
    for i in range(0,n+1):
        for j in range(0,n+1):
            pot = -b*b * lambd * sin(b*k[i])*sin(b*k[j])/(k[i]*b*k[j]*b)
            F[i][j] = pot*D[j]
            if i==j: F[i][j] = F[i][j] + 1.
            V[i] = pot
    for i in range(0,n+1):  Vvec[i][0]= V[i]
    Finv = lina.inv(F)
    R = dot(Finv, Vvec)
    RN1 = R[n][0]
    shift = atan(-RN1*ko)
    sin2 = (sin(shift))**2
    sin2plot.plot(pos = (ko*b,sin2))               # Plot sin**2(delta)
    ko = ko + 0.2*pi/1000.
print("Done")
```

## 26.4.5 Scattering Implementation

For the scattering problem, we use the same delta-shell potential (26.16) discussed in Section 26.2.2 for bound states:

$$
V(k',k)=\frac{-|\lambda|}{2\mu k' k}\sin(k' b)\sin(k b).
\tag{26.38}
$$

This is one of the few potentials for which the Lippmann–Schwinger equation (26.20) has an analytic solution (Gottfried, 1966) with which to check:

$$
\tan\delta_0 = \frac{\lambda b\sin^2(kb)}{k b - \lambda b\sin(kb)\cos(kb)}.
\tag{26.39}
$$

Our results were obtained with \(2\mu = 1\), \(\lambda b = 15\), and \(b = 10\), the same as in (Gottfried, 1966). In Figure 26.5, we give a plot of \(\sin^2\delta_0\) vs. \(k b\), which is proportional to the scattering cross section arising from the angular momentum \(l = 0\) phase shift. It is seen to reach its maximum values at energies corresponding to resonances. In Listing 26.2, we present our program for solving the scattering integral equation using the NumPy Linear Algebra matrix library and the gauss method
