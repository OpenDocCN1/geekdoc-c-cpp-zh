# Exercise Show that after some rearrangement, (7.58)–(7.60) can be written as

S a₁ + Sₓ a₂ + Sₓₓ a₃ = Sᵧ , Sₓ a₁ + Sₓₓ a₂ + Sₓₓₓ a₃ = Sₓᵧ , Sₓₓ a₁ + Sₓₓₓ a₂ + Sₓₓₓₓ a₃ = Sₓₓᵧ . (7.61)

Here the definitions of the S’s are simple extensions of those used in (7.47)–(7.49) and are programmed in Fit.py shown in Listing 7.4. After placing the three unknown parameters into a vector a and the known three RHS terms in (7.61) into a vector b, these equations assume the matrix form

A x = b , A = [ S Sₓ Sₓₓ ; Sₓ Sₓₓ Sₓₓₓ ; Sₓₓ Sₓₓₓ Sₓₓₓₓ ] , x = [ a₁ ; a₂ ; a₃ ] , b = [ Sᵧ ; Sₓᵧ ; Sₓₓᵧ ] . (7.62)

The solution for the parameter vector a is obtained by solving the matrix equations. Although for 3 × 3 matrices, we can write out the solution in a closed form, for larger problems the numerical solution requires matrix methods.

# Listing 7.4 Fit.py performs a least-squares fit of a parabola to data using the NumPy linalg package to solve the set of linear equations S a = s.

```
# Fit.py Linear least-squares fit; e.g. of matrix computation arrays
import pylab as p
from numpy import *
from numpy.linalg import inv
from numpy.linalg import solve

t = arange(1.0, 2.0, 0.1) # x range curve
x = array([1., 1.1, 1.24, 1.35, 1.451, 1.5, 1.92]) # Given x values
y = array([0.52, 0.8, 0.7, 1.8, 2.9, 2.9, 3.6]) # Given y values
p.plot(x, y, 'bo') # Plot data in blue
sig = array([0.1, 0.1, 0.2, 0.3, 0.2, 0.1, 0.1]) # error bar lengths
p.errorbar(x,y,sig) # Plot error bars
p.title('Linear Least Square Fit') # Plot figure
p.xlabel('x') # Label axes
p.ylabel('y')
p.grid(True) # plot grid
Nd = 7
A = zeros( (3,3), float ) # Initialize
bvec = zeros( (3,1), float )
ss = sx = sxx = sy = sxxx = sxy = sxy = sxxy = 0.

for i in range(0, Nd):
    sig2 = sig[i] * sig[i]
    ss += 1. / sig2; sx += x[i]/sig2; sy += y[i]/sig2
    rhl = x[i] * x[i]; sxx += rhl/sig2; sxxy += rhl * y[i]/sig2
    sxy += x[i]*y[i]/sig2; sxxx +=rhl*x[i]/sig2; sxxxx +=rhl*rhl/sig2

A = array([ [ss,sx,sxx], [sx,sxx,sxxx], [sxx,sxxx,sxxxx] ])
bvec = array([sy, sxy, sxxy])

xvec = multiply(inv(A), bvec) # Invert matrix
Itest = multiply(A, inv(A)) # Matrix multiply
```