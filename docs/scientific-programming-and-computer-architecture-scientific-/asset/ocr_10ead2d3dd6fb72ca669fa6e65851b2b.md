# A.3. C/C++ versus Python versus MATLAB

```
def primes(n):
    assert n >= 3
    p = np.zeros((n+1), dtype = bool)
    p[0] = False
    p[1] = False
    p[2] = True
    ksqrt = 1
    for k in range(3,n+1):
        if ksqrt*ksqrt < k:
            ksqrt += 1
        p[k] = True
        for j in range(2,ksqrt+1):
            if p[j] and k%j == 0:
                p[k] = False
                break
    return p
```

With $n=107$, the program consumes $4.9 	imes 10^{11}$ cycles on a 3.6 GHz AVX2 machine (see table A.1). The same program in MATLAB consumes $4.7 	imes 10^{11}$ cycles. In C/C++, the program consumes $1.1 	imes 10^{10}$ cycles, which is less than $2.5\%$ of the time taken by Python or MATLAB.

In fact, a C/C++ speed of 40 is at the low end. Much of the overhead in interpreted languages is due to symbol-table lookup. In a simple program as such, the symbol-table lookup will be less expensive than in more complicated programs. In addition, the C/C++ compiler has not optimized this program for the instruction set architecture. So the vast range of optimizations possible in C/C++ kick kick.

However, if one limits oneself to a narrow idiom, relying mostly on BLAS/LAPACK routines and not much, Python and MATLAB can be as fast as C/C++. However, such a thing is too constraining and not possible to sustain in more complex programs. For even moderately complex programs, C/C++ can be faster than MATLAB by a factor of 1,000.$5$

> $5$For an example of a simple program that is several hundred times faster in C/C++ than in MATLAB, see (B. Sadiq and D. Viswanath, Finite difference weights, spectral differentiation,