vanishes at all n interpolation points xi. However, since its degree is at most (n − 1), Qn−1(x) has only (n − 1) zeros and therefore results to be identically zero, Qn−1(x) ≡ 0. Consequently, P~n−1(x) is identical with Pn−1(x), which proves the uniqueness of the Lagrange polynomial. It is, however, self-evident that an infinite number of polynomials of higher degree than n − 1, or, equivalently, having a higher number of adjustable parameters than the number of interpolation conditions, can be fitted to interpolate the data points.

Formula 9.16 indicates that the Lagrange polynomial essentially provides a nonlocal approximation, meaning that all the data points contribute to the interpolant, not only those in the close vicinity of the argument. The same nonlocality guarantees, on the one hand, the smoothness of the approximation by the continuity of the high-order derivatives, but, on the other hand, may induce artificial oscillations of the interpolation polynomial.

In the particular case of n = 2 interpolation points, (x1,y1) and (x2,y2), the Lagrange polynomial reduces to

P1(x) = (x − x2)/(x1 − x2) y1 + (x − x1)/(x2 − x1) y2   (9.17)

and, obviously describes the straight line passing through the two points.

In the case n = 3, the Lagrange interpolant corresponds to the parabola defined by the three data points (x1,y1), (x2,y2), and (x3,y3):

P2(x) = [(x − x2)(x − x3)]/[(x1 − x2)(x1 − x3)] y1 + [(x − x1)(x − x3)]/[(x2 − x1)(x2 − x3)] y2 + [(x − x1)(x − x2)]/[(x3 − x1)(x3 − x2)] y3.   (9.18)

The Lagrange interpolant (9.16) is coded in Listing 9.1. Upon receiving n data points in the arrays x and y, the function Lagrange returns the interpolant value for the argument xi. The variant Lagrange1, presented in Listing 9.2, receives additionally an array xi of ni interpolation arguments, for which it returns the interpolant values via the array yi. For efficiency reasons, the constant factors yi/∏j≠i (xi − xj) are calculated in advance.

In the sample program from Listing 9.3, the routine Lagrange (assumed to be contained in the module modfunc.py) interpolates a set of data points extracted from the function f(x) = 1/x and evaluates the interpolant for several arguments.

# Listing 9.1 Lagrange Interpolant (Python Coding)

```
#===============================================================================
def Lagrange(x, y, n, xi):
#-------------------------------------------------------------------------------
# Evaluates the Lagrange interpolating polynomial of n data points at xi
# x[] - x-coordinates of data points
# y[] - y-coordinates of data points
# n   - number of data points
# xi  - interpolation argument
#-------------------------------------------------------------------------------
    yi = 0e0
    for i in range(1,n+1):
        p = 1e0
        for j in range(1,n+1):
            if (j != i): p *= (xi - x[j])/(x[i] - x[j])
        yi += p * y[i]

    return yi
```