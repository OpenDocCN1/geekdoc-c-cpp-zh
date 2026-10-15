![](bbox=[0.32, 0.12, 0.68, 0.32])

FIGURE 6.4 Division of the search interval by the chord connecting the points (a_i, f(a_i)), și (b_i, f(b_i)) in the false position method.

The false position method is coded as routine FalsPos in Listing 6.3. The general construction principles, input/output parameters, and functionalities of this routine are identical with those of the function Bisect described in the previous section and, as such, the two routines are interchangeable in applications.

# Listing 6.3 Method of False Position (Python Coding)

```
================================================================================
def FalsPos(Func, a, b):
#--------------------------------------------------------------------------------
# Determines a real root x of function Func isolated in interval [a,b] by
# the false position method
# Error code: 0 - normal execution
#             1 - [a,b] does not isolate one root or contains several roots
#             2 - max. number of iterations exceeded
#--------------------------------------------------------------------------------
    eps = 1e-10                         # relative precision of root
    itmax = 100                         # max. no. of iterations

    x = a; fa = Func(x)                 # is a the root?
    if (fabs(fa) == 0e0): return (x,0)
    x = b; fb = Func(x)                 # is b the root?
    if (fabs(fb) == 0e0): return (x,0)

    if (fa*fb > 0): return (x,1)        # [a,b] does not contain a root
                                    # or contains several roots
    for it in range(1,itmax+1):
        x = (a*fb - b*fa)/(fb - fa)     # new approximation
        fx = Func(x)
        if (fa*fx > 0):
            dx = x - a; a = x; fa = fx  # choose new bounding interval
        else:
            dx = b - x; b = x; fb = fx
        if ((fabs(dx) <= eps*fabs(x)) or (fabs(fx) <= eps)): return (x,0)

    printf("FalsPos: max. no. of iterations exceeded !"); return (x,2)
```