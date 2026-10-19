
## Exercise Show that after some rearrangement, (7.58)–(7.60) can be written as

S a₁ + Sₓ a₂ + Sₓₓ a₃ = Sᵧ , Sₓ a₁ + Sₓₓ a₂ + Sₓₓₓ a₃ = Sₓᵧ , Sₓₓ a₁ + Sₓₓₓ a₂ + Sₓₓₓₓ a₃ = Sₓₓᵧ . (7.61)

Here the definitions of the S’s are simple extensions of those used in (7.47)–(7.49) and are programmed in Fit.py shown in Listing 7.4. After placing the three unknown parameters into a vector a and the known three RHS terms in (7.61) into a vector b, these equations assume the matrix form

A x = b , A = [ S Sₓ Sₓₓ ; Sₓ Sₓₓ Sₓₓₓ ; Sₓₓ Sₓₓₓ Sₓₓₓₓ ] , x = [ a₁ ; a₂ ; a₃ ] , b = [ Sᵧ ; Sₓᵧ ; Sₓₓᵧ ] . (7.62)

The solution for the parameter vector a is obtained by solving the matrix equations. Although for 3 × 3 matrices, we can write out the solution in a closed form, for larger problems the numerical solution requires matrix methods.

### Listing 7.4 Fit.py performs a least-squares fit of a parabola to data using the NumPy linalg package to solve the set of linear equations S a = s.

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
ss = sx = sxx = sy = sxxx = sxy = sxxy = 0.

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

```
print('\n x vector via inverse')
print(xvec, '\n')
print('A=inverse(A)')
print(Itest, '\n')

xvec = solve(A, bvec)                # Solve via elimination
print('x Matrix via direct')
print(xvec, 'end= ')
print('FitParabola Final Results\n')
print('y(x) = a0 + a1 x + a2 x^2')      # Desired fit
print('a0 = ', x[0])
print('a1 = ', x[1])
print('a2 = ', x[2], '\n')
print(' i   xi      yi      yfit   ')
for i in range(0, Nd):
    s = xvec[0] + xvec[1]*x[i] + xvec[2]*x[i]*x[i]
    print(' %d %5.3f   %5.3f   %8.7f \n' %(i, x[i], y[i], s))
# red line is the fit, red dots the fits at y[i]
curve = xvec[0] + xvec[1]*t + xvec[2]*t**2
points = xvec[0] + xvec[1]*x + xvec[2]*x**2
p.plot(t, curve,'r', x, points, 'ro')
p.show()
```

## Linear Quadratic Fit Assessment

- 1. Fit the quadratic (7.57) to the following data sets [given as (x₁, y₁), (x₂, y₂), ...]. In each case, indicate the values found for the a’s, the number of degrees of freedom, and the value of χ².
  - a) (0, 1)
  - b) (0, 1), (1, 3)
  - c) (0, 1), (1, 3), (2, 7)
  - d) (0, 1), (1, 3), (2, 7), (3, 15)
- 2. Find a fit to the last set of data to the function
  - y = A e^{-b x²}.  (7.63)

Hint: A judicious change of variables will permit you to convert this to a linear fit. Does a minimum χ² still have meaning here?

### 7.8.2

## Problem 5: Nonlinear Fit to a Breit–Wigner

Problem  Remember how earlier in this chapter we interpolated the values in Table 7.1 in order to obtain the experimental cross section Σ as a function of energy. Although we did not use it, we also gave the theory describing these data, namely, the Breit–Wigner resonance formula (7.21):

f(E) = f_r / [(E - E_r)² + Γ²/4].  (7.64)

Your problem is to determine what values for the parameters E_r, f_r, and Γ in (7.64) provide the best fit to the data in Table 7.1.

Because (7.64) is not a linear function of the parameters ($E_r$, $\Sigma_0$, $\Gamma$), the three equations that result from minimizing $\chi^2$ are not linear equations and so cannot be solved by the techniques of linear algebra (matrix methods). However, in our study of the masses on a string problem, we showed how to use the Newton–Raphson algorithm to search for solutions of simultaneous nonlinear equations. That technique involved expansion of the equations about the previous guess to obtain a set of linear equations and then solving the linear equations with the matrix libraries. We now use this same combination of fitting, trial-and-error searching, and matrix algebra to conduct a nonlinear least-squares fit of (7.64) to the data in Table 7.1.

Recall that the condition for a best fit is to find values of the $M_p$ parameters $a_m$ in the theory $g(x, a_m)$ that minimize $\chi^2 = \sum_i [(y_i - g_i)/\sigma_i]^2$. This leads to the $M_p$ equations (7.44) to solve

\[ \sum_{i=1}^{N_D} \frac{[y_i - g(x_i)]}{\sigma_i^2} \frac{\partial g(x_i)}{\partial a_m} = 0 \;, \quad (m = 1, M_p) \. \tag{7.65} \]

To find the form of these equations appropriate to our problem, we rewrite our theory function (7.64) in the notation of (7.65):

\[ a_1 = f_r \;, \quad a_2 = E_R \;, \quad a_3 = \Gamma^2 / 4 \;, \quad x = E \;, \tag{7.66} \]

\[ \Rightarrow \quad g(x) = \frac{a_1}{(x - a_2)^2 + a_3} \. \tag{7.67} \]

The three derivatives required in (7.65) are then

\[ \frac{\partial g}{\partial a_1} = \frac{1}{(x - a_2)^2 + a_3} \;, \quad \frac{\partial g}{\partial a_2} = \frac{-2 a_1 (x - a_2)}{[(x - a_2)^2 + a_3]^2} \;, \quad \frac{\partial g}{\partial a_3} = \frac{-a_1}{[(x - a_2)^2 + a_3]^2} \. \tag{7.68} \]

Substitution of these derivatives into the best-fit condition (7.65) yields three simultaneous equations in $a_1$, $a_2$, and $a_3$ that we need to solve in order to fit the $N_D = 9$ data points $(x_i, y_i)$ in Table 7.1:

\[ \sum_{i=1}^{9} \frac{y_i - g(x_i, a)}{(x_i - a_2)^2 + a_3} = 0 \;, \]
\[ \sum_{i=1}^{9} \frac{y_i - g(x_i, a)}{[(x_i - a_2)^2 + a_3]^2} = 0 \;, \]
\[ \sum_{i=1}^{9} \frac{\{y_i - g(x_i, a)\}(x_i - a_2)}{[(x_i - a_2)^2 + a_3]^2} = 0 \. \tag{7.69} \]

Even without the substitution of (7.64) for $g(x, a)$, it is clear that these three equations depend on the $a$'s in a nonlinear fashion. That is okay because in Section 6.1.2 we derived the $N$-dimensional Newton–Raphson search for the roots of

\[ f_i(a_1, a_2, \dots, a_N) = 0 \;, \quad i = 1, N \;, \tag{7.70} \]

where we have made the change of variable $y_i \to a_i$ for the present problem. We use that same formalism here for the $N = 3$ Equation 7.69 by writing them as

```
$f_1(a_1, a_2, a_3) = \sum_{i=1}^{9} \frac{y_i - g(x_i, a)}{(x_i - a_2)^2 + a_3} = 0 , \qquad (7.71)$
```

```
$f_2(a_1, a_2, a_3) = \sum_{i=1}^{9} \frac{\{y_i - g(x_i, a)\}(x_i - a_2)}{[(x_i - a_2)^2 + a_3]^2} = 0 , \qquad (7.72)$
```

```
$f_3(a_1, a_2, a_3) = \sum_{i=1}^{9} \frac{y_i - g(x_i, a)}{[(x_i - a_2)^2 + a_3]^2} = 0 . \qquad (7.73)$
```

Because $f_r \equiv a_1$ is the peak value of the cross section, $E_R \equiv a_2$ is the energy at which the peak occurs, and $\Gamma = 2\sqrt{a_3}$ is the full width of the peak at half-maximum, good guesses for the $a$'s can be extracted from a graph of the data. To obtain the nine derivatives of the three $f$'s with respect to the three unknown $a$'s, we use two nested loops over $i$ and $j$, along with the forward-difference approximation for the derivative

```
$\frac{\partial f_i}{\partial a_j} \simeq \frac{f_i(a_j + \Delta a_j) - f_i(a_j)}{\Delta a_j} , \qquad (7.74)$
```

where $\Delta a_j$ corresponds to a small, say $\le 1\%$, change in the parameter value.

## Nonlinear Fit Implementation

Use the Newton–Raphson algorithm as outlined in Section 7.8.2 to conduct a nonlinear search for the best-fit parameters of the Breit–Wigner theory (7.64) to the data in Table 7.1. Compare the deduced values of $(f_r, E_R, \Gamma)$ to that obtained by inspection of the graph.
