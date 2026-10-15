An alternative strategy would be to fill array (10.46) in a *column-wise left-to-right* manner. This would require, however, to fix the maximum number of halving iterations \(k_{\max}\) in advance and to evaluate *all* approximations on each column until convergence is met for some diagonal estimate \(R_{k,k}\). At this point, if \(k < k_{\max}\), the already-calculated estimates located beneath row \(k\) would become unnecessary, rendering the algorithm inefficient.

Romberg’s method (10.47)–(10.50) is implemented in function `qRomberg` (Listing 10.5), having the same parameters as routines `qTrapzCtrl` and `qSimpsonCtrl`. Instead of the triangular array of approximations \(R_{k,j}\), the implementation uses just two one-dimensional arrays for the two most recent consecutive rows, `r1` and `r2`, which are shifted at the end of each subinterval-halving iteration. Like in the case of the functions `qTrapzCtrl` and `qSimpsonCtrl`, the number of halving iterations is limited to 30, which corresponds to a maximum of \(2^{30}\) integration points (the largest power of 2 representable by a long-type variable in standard C).

Every halving iteration of the integration spacing starts with the evaluation of the integral based on the trapezoidal formula. The order of the basic quadrature is then raised recursively and the convergence of the process is checked. If the requested precision `eps` is not achieved after running through all Newton–Cotes formulas applicable for the current number of mesh points, the next halving step is prepared by doubling the number of subintervals (halving the mesh spacing). If convergence is not achieved within the \(k_{\max}\) allowed halving iterations, a warning message is issued.

```
```python
#===============================================================
def qRomberg(Func, a, b, eps = 1e-6):
#  Integrates function Func on interval [a,b] with relative precision eps
#  using the adaptive Romberg method
#===============================================================
    kmax = 30                              # max. no. of step halving iterations
    r1 = [0]*(kmax+1)                       # two consecutive lines
    r2 = [0]*(kmax+1)                       # from the method table

    h = b-a; n = 1
    r1[0] = 0.5*h*(Func(a) + Func(b))       # initial approximation
    for k in range(1,kmax+1):               # step halving loop
        sumf = 0e0
        for i in range(1,n+1): sumf += Func(a+(i-0.5)*h)
        r2[0] = 0.5*(r1[0] + h*sumf)        # trapezoid formula
        f = 1e0
        for j in range(1,k+1):               # increase quadrature order
            f *= 4
            r2[j] = (f*r2[j-1] - r1[j-1])/(f-1)  # new approximation

        if (k > 1):                          # convergence check
            if (fabs(r2[k]-r1[k-1]) <= eps*fabs(r2[k])): break
            if (fabs(r2[k]) <= eps and fabs(r2[k]) <= fabs(r2[k]-r1[k-1])): break
        h *= 0.5; n *= 2                    # halve integration step
        for j in range(0,k+1): r1[j] = r2[j] # shift table lines

    if (k >= kmax):
        print("qRomberg: max. no. of iterations exceeded !")
        k -= 1

    return r2[k]
```
```