for the hand-picked arguments 0, π/2, π, 3π/2, and π. In the sample program from Listing 9.10, the model function is chosen to have two adjustable parameters,

F(x; a₁, a₂) = a₁ sin x + a₂ cos x,

and the evaluation of the basis functions F₁(x) = sin x and F₂(x) = cos x is carried out by the user function Func. The adjusted model parameters returned by MultiFit are a₁ = 0.999929 and a₂ = 1.000212, with the merit function χ² = 0.000000. It is noteworthy that the fitting procedure of the model function recovers within roundoff errors the coefficients of the original function f(x), which has provided the “observed” data.

Generalizing the model function to include more basis functions (1, sin x, cos x, sin 2x, cos 2x, etc.), the routine MultiFit can be used, in principle, to extract Fourier series coefficients from tabulated dependences (see Problem 9.9).

In the particular case of the polynomial regression, the model function having m adjustable parameters is a polynomial of degree (m − 1):

F(x; a) = Σ_{j=1}^{m} a_j x^{j-1}. (9.57)

# Listing 9.10 Application of Multilinear Regression (Python Coding)

```
# Multilinear fit
from math import *
from modfunc import *

def Func(x, func, npar):
    func[1] = sin(x)      # returns the basis functions sin(x) and cos(x)
    func[2] = cos(x)

# main

n = 5                                   # number of observed data
npar = 2                                # number of model parameters

x     = [0]*(n+1)                      # x-coordinates of observed data
y     = [0]*(n+1)                      # y-coordinates of observed data
sigmy = [0]*(n+1)                      # standard deviations of observed data
func  = [0]*(npar+1)                   # values of basis functions
a     = [0]*(npar+1)                    # model parameters
sigma = [0]*(npar+1)                   # uncertainties of parameters

x[1] = 0e000; y[1] = 1e000              # observed data generated from:
x[2] = 0.785; y[2] = 1.414              # f(x) = sin(x) + cos(x)
x[3] = 1.571; y[3] = 1e000
x[4] = 2.356; y[4] = 0e000
x[5] = 3.141; y[5] = -1e000

iOpt = 0                               # least squares fit: equal errors sigmy
chi2 = MultiFit(x,y,sigmy,n,iOpt,a,sigma,npar,Func)

print("Multilinear fit:")
for i in range(1,npar+1):
    print("[a{0:d}] = {1:8.4f} +/- {2:8.4f}".format(i,a[i],sqrt(sigma[i])))
print("Chi^2 = {0:8.4f}".format(chi2))
```