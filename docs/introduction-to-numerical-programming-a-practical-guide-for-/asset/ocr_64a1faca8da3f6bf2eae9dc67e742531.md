The above sequence can be actually described in terms of the iterative process:

T0 = h0/2 [f(a) + f(b)],   h0 = b - a,   n0 = 1,   (10.29)
T_k = 1/2 [ T_{k-1} + h_{k-1} sum_{i=1}^{n_{k-1}} f(a + (i - 1/2)h_{k-1}) ],   (10.30)
h_k = h_{k-1}/2,   n_k = 2n_{k-1},   k = 1,2,...

where h_k = (b - a)/n_k is the mesh spacing after the halving step k, with n_k = 2^k representing the corresponding number of subintervals or, equivalently, the number of new integration points relevant for the next approximation of the integral.

The recursive process (10.29)-(10.30) is typically continued until two consecutive approximations of the integral become indistinguishable to a given accuracy, that is, until their relative difference, |T_k - T_{k-1}| / |T_k|, considered as an estimate of the relative error, drops under a predefined tolerance ε. To avoid the singular division in the particular situation when T_k = 0, the convergence criterion may be conveniently formulated as |T_k - T_{k-1}| ≤ ε |T_k|.   (10.31)

The function qTrapzCtrl (Listing 10.3) implements the described adaptive algorithm based on the trapezoidal rule. To ensure that, during the recursive process, the current number of subintervals, n, as a power of 2, does not exceed the maximum representable value of type long (2^31 - 1 for standard C/C++ implementations), the number of halving iterations is limited by kmax to 30. However, if, due to weak convergence, the kmax iterations are exhausted without the quadrature having achieved the requested accuracy eps, the step-halving loop is left with counter k incremented to kmax+1 and an error message is issued. Another, yet more versatile variant of treating the absence of convergence would be to return an error index to the calling program unit, leaving on its behalf the action to be taken.

# Listing 10.3 Adaptive Integrator Based on the Trapezoidal Rule (Python Coding)

```
# =================================================================================
def qTrapzCtrl(Func, a, b, eps = 1e-6):
# ----------------------------------------------------------------------------------
# Integrates function Func on interval [a,b] with relative precision eps
# using the adaptive trapezoidal rule
# ----------------------------------------------------------------------------------
    kmax = 30                     # max. no. of step halving iterations

    h = b-a; n = 1
    t0 = 0.5*h*(Func(a) + Func(b))                # initial approximation

    for k in range(1,kmax+1):                     # step halving loop
        sumf = 0e0
        for i in range(1,n+1): sumf += Func(a+(i-0.5)*h)
        t = 0.5*(t0 + h*sumf)                     # new approximation
        if (k > 1):                               # convergence check
            if (fabs(t-t0) <= eps*fabs(t)): break
            if (fabs(t) <= eps and fabs(t) <= fabs(t-t0)): break # integral ~= 0
        h *= 0.5; n *= 2                          # halve integration step
        t0 = t

    if (k >= kmax): print("qTrapzCtrl: max. no. of iterations exceeded !")

    return t
```