# Listing 11.4  2D Monte Carlo Integration with Importance Sampling (Python Coding)

```
# Two-dimensional Monte Carlo quadrature with variance reduction
from math import *
from random import *
from randoml import *

def func(x,y):                                      # integrand
    return (x*x + y*y)*exp(-0.5e0*(x*x + y*y))/(4e0*pi)

# main

L = 8e0                                             # integration domain [-L,L] x [-L,L]
L2 = L * L                                          # area of sampling domain

n = 100000                                          # number of sampling points

seed()

f1 = f2 = 0e0                                       # quadrature with uniform sampling
for i in range(1,n+1):
    x = L * random(); y = L * random()
    f = func(x,y)                                   # integrand
    f1 += f; f2 += f * f                            # sums

f1 /= n; f2 /= n                                    # averages
s = 4e0 * L2 * f1                                   # integral
sigma = 4e0 * L2 * sqrt((f2-f1*f1)/n)               # standard deviation
print("Uniform sampling : s = ",s," +/- ",sigma)

f1 = f2 = 0e0                                       # quadrature with importance sampling
for i in range(1,n+1):
    (w, x, y) = randNrm2()                          # random numbers with normal distribution
    f = func(x,y) / w                              # integrand
    f1 += f; f2 += f * f                           # sums

f1 /= n; f2 /= n                                    # averages
s = f1                                              # integral
sigma = sqrt((f2-f1*f1)/n)                          # standard deviation
print("Gaussian sampling: s = ",s," +/- ",sigma)
```

sampling. A further confirmation of the better performance of the Gaussian sampling is provided by the linear fits of the log–log plots of the standard deviations as functions of the number of sampling points, which indicate a reduction of the uncertainties roughly by a factor of 2.9 when using normally instead of uniformly distributed random numbers.

Let us consider as an application of the Monte Carlo methodology to 3D quadratures the evaluation of the mass and mass center position of a torus of major radius R = 3 and minor radius r = 1 (see Figure 11.3). The torus is centered at the origin and is symmetric about the z-axis. A similar problem was treated in Chapter 10 by using deterministic quadratures. The equation of the toroidal surface is

\(\left(R - \sqrt{x^2 + y^2}\right)^2 + z^2 = r^2.\n\(11.24\)