where the points external to the domain 𝒟 can be discriminated by using the Heaviside function

```
H(x) = { 0 if x < 0, 1 if x ≥ 0. } (11.19)
```

The corresponding Monte Carlo quadrature formula is thus

```
I ≈ 4/n Σ_{i=1}^n H[1 - (x_i^2 + y_i^2)] = 4 n_i / n, (11.20)
```

and it implies n random sampling points (x_i, y_i), uniformly distributed within the square 	ilde{D}. In this case, the sum has obviously the significance of the number n_i of points interior to the circular sector D and its area is, as can be seen, proportional to the ratio between n_i and the total number of sample points n. In other words, the area of the circular sector is proportional with the probability of generating interior sampling points. A simple calculation shows that the mean integrand and the mean squared integrand are equal in this case, that is, ⟨H⟩ = ⟨H²⟩ = n_i / n.

Program 11.3 precisely implements the discussed ideas. The estimates for the unit circle area are listed in Table 11.2 for several numbers of sampling points. For n = 50,000, the expected π value is reproduced with four exact decimal digits, even though the associated standard error σ suggests a poorer estimate.

Pursuing the idea that for a uniform sampling of the extended domain 	ilde{D}, the ratio of the volumes V and 	ilde{V} is approximated by the ratio n_i / n of the corresponding numbers of sampling points; the above

# Listing 11.3 Monte Carlo Evaluation of the Area of the Unit Circle (Python Coding)

```
# Monte Carlo calculation of the unit circle area
from math import *
from random import *

# main

n = eval(input("n = "))                     # number of sampling points

seed()

ni = 0                                       # number of interior points
for i in range(1,n+1):
    x = random(); y = random()
    if (x*x + y*y <= 1e0): ni += 1           # add interior point

fi = ni/n                                    # fraction of interior points
s = 4e0 * fi                                 # integral
sigma = 4e0 * sqrt((fi - fi*fi)/n)           # standard deviation
print("Unit circle area = ",s,"+/- ",sigma)
```

# TABLE 11.2 Monte Carlo Estimates of the Integral I = ∫∫_{x²+y²≤1} dx dy and Associated Standard Deviations σ

| n | I | σ | n | I | σ |
|---|---|---|---|---|---|
| 100 | 3.20000 | 0.16000 | 5,000 | 3.14400 | 0.02320 |
| 500 | 3.22400 | 0.07074 | 10,000 | 3.15520 | 0.01633 |
| 1000 | 3.12800 | 0.05223 | 50,000 | 3.14128 | 0.00734 |