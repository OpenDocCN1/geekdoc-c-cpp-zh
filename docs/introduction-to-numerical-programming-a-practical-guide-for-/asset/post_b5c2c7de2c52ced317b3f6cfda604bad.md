
of sufficiently accurate results generally implies a tremendous number of operations and conveying vast amounts of data. By comparison with the deterministic numerical methods, the success of the Monte Carlo method is mainly due to the more advantageous scaling of the computational effort with increasing problem size. In fact, while being the most inefficient quadrature method for one-dimensional integrals, with increasing dimensionality, the Monte Carlo method progressively exceeds the deterministic methods.

The main uses of the Monte Carlo method can be broadly categorized into optimization, numerical integration, and generation of samples from probability distributions. In applied mathematics, the Monte Carlo method reveals its efficiency most clearly in applications such as the evaluation of multidimensional integrals with complex boundaries, the solution of large linear systems, or the solution of Dirichlet problems for differential equations. In this chapter, we specifically focus on the integration of functions.

## 11.2 Integration of Functions

In the Monte Carlo method, the integral of a function *f* over a multidimensional domain 𝒟 is simply estimated by the product of the arithmetic mean of the function and the domain volume *V*,

$$\int_{\mathcal{D}} f\,dV \approx V\langle f\rangle \pm \sigma,$$  (11.1)

where the average ⟨*f*⟩ is calculated for *n* random points, **x**₁, …, **x**ₙ, sampling *randomly* and *uniformly* the domain 𝒟. The statistical uncertainty associated with the result of the integration is specified by the *standard deviation* σ,

$$\sigma = V\sqrt{\frac{\langle f^2\rangle-\langle f\rangle^2}{n}}=\frac{V}{\sqrt n}\sigma_f,$$  (11.2)

or its square, σ², called *variance*. The standard deviation,

$$\sigma_f=\sqrt{\left\langle(f-\langle f\rangle)^2\right\rangle}=\sqrt{\langle f^2\rangle-\langle f\rangle^2},$$

occurring in the above expression, measures the deviation of the integrand *f* from its mean ⟨*f*⟩ within the integration domain. The averages ⟨*f*⟩ and ⟨*f*²⟩ are given, respectively, by

$$\langle f\rangle=\frac{1}{n}\sum_{i=1}^{n}f(\mathbf{x}_i),\qquad \langle f^2\rangle=\frac{1}{n}\sum_{i=1}^{n}f^2(\mathbf{x}_i).$$  (11.3)

Expression 11.2 of the standard deviation σ illustrates two important features of the Monte Carlo integration. The first refers to the *n*⁻¹ᐟ² scaling of the uncertainty σ. As expected, the larger the number of sampling points, the more precise the result of the integration, even if the decrease of σ is rather slow. By comparison, the error of the basic trapezoidal formula, the most rudimentary of the Newton–Cotes quadrature family, features an *n*⁻² dependence and the required numerical effort for achieving the same precision in a *one-dimensional* integration proves to be definitely lower than for the Monte Carlo method. However, the advantage of the more favorable scaling of the operation count for the classical quadrature formulas vanishes in multidimensional cases. It can be easily seen that the remainder of a *d*-dimensional integration scheme based on a conventional one-dimensional integrator, characterized by *n* function evaluations for each dimension, increases as *n*⁻²ᐟᵈ. On the contrary, the *n*⁻¹ᐟ² dependence of the uncertainty σ is conserved irrespective of the dimensionality, so that, for *d* > 4, the Monte Carlo method becomes more efficient.

at least 32,767 in any standard implementation of the C/C++ compiler. To generate real random numbers in the standard interval [0,1), the values returned by rand() have to be simply divided by (RAND_MAX+1):

```
// Generates random floating point numbers in the range [0,1)
#define random() ((double)rand()/(RAND_MAX+1))
```

The macros seed() and random() will be assumed in what follows to be included in the header file random.h.

As a first, elementary example of Monte Carlo quadrature, we consider the integral

∫₀¹ x e⁻ˣ dx = 1 − 2e⁻¹ ≈ 0.26424. (11.7)

The corresponding program (Listing 11.1) does not actually implement the Monte Carlo methodology as a distinct procedure, since a suchlike routine lacks practical interest, as the whole idea of using the Monte Carlo method for performing one-dimensional integration. Instead, the main program is kept simple, with a view to emphasizing the general concept. Here, n represents the number of sampling points, s is the integral estimate, and sigma represents the associated standard deviation. The variables f1 and f2 are used to store, respectively, the average ⟨f⟩ and the average squared function ⟨f²⟩.

The results of the program execution for different numbers of integration points n are compiled in the first three columns of Table 11.1. Along with the increase of n, the estimates of the integral converge toward the exact value, with obviously decreasing associated uncertainty estimates σ. As will be shown in the next section, the standard deviations σ scale indeed as n⁻¹/² and a comparison with any

### Listing 11.1 Monte Carlo Integration of a Function (Python Coding)

```
# One-dimensional Monte Carlo quadrature
from math import *
from random import *

def func(x): return x * exp(-x)                     # integrand

# main

n = eval(input("n = "))                           # number of sampling points

seed()

f1 = f2 = 0e0                                      # quadrature with uniform sampling
for i in range(1,n+1):
    x = random()                                   # RNG with uniform distribution
    f = func(x)                                    # integrand
    f1 += f; f2 += f * f                           # sums

f1 /= n; f2 /= n                                   # averages
s = f1                                             # integral
sigma = sqrt((f2-f1*f1)/n)                         # standard deviation
print("s = ",s,"+/-",sigma)
```

**TABLE 11.1** Monte Carlo Estimates of the Integral \(I=\int_0^1 xe^{-x}\,dx\) and Associated Standard Deviations \(\sigma\), Calculated Using Random Sequences with the Distributions \(w(x)=1\) and, Respectively, \(w(x)=(3/2)x^{1/2}\)

| \(n\) | \(w(x)=1\): \(I\) | \(w(x)=1\): \(\sigma\) | \(w(x)=(3/2)x^{1/2}\): \(I\) | \(w(x)=(3/2)x^{1/2}\): \(\sigma\) |
|---:|---:|---:|---:|---:|
| 10 | 0.25108 | 0.03855 | 0.26860 | 0.00727 |
| 100 | 0.26252 | 0.01085 | 0.26397 | 0.00285 |
| 1000 | 0.26622 | 0.00336 | 0.26458 | 0.00089 |
| 10,000 | 0.26544 | 0.00105 | 0.26423 | 0.00027 |

classical one-dimensional quadrature formula proves the latter to be significantly more efficient. While the Monte Carlo integration can be yet improved, its full potential comes to light only in the evaluation of multidimensional integrals.

## 11.3 Importance Sampling

Having in view that the uncertainty \(\sigma\) (11.2) of the Monte Carlo quadrature is directly related to the variance of the integrand \(\sigma_f\), which measures the deviation of the integrand from its average value, to increase the precision and efficiency of the quadrature, one can apply a general strategy, known as *variance reduction*. More precisely, we discuss a technique called *importance sampling*.

Essentially, one introduces a positive *weight function*, \(w(x)\), normalized to unity over the interval \([0,1]\),

\[\int_0^1 w(x)\,dx=1,\tag{11.8}\]

by which integrand (11.5) is multiplied and divided:

\[I=(b-a)\int_0^1\frac{f((b-a)x+a)}{w(x)}w(x)\,dx.\]

Performing the change of variable \(d\xi=w(x)dx\) or, in integral form,

\[\xi(x)=\int_0^x w(x')\,dx',\tag{11.9}\]

with the boundary conditions \(\xi(0)=0\) and \(\xi(1)=1\) (to comply with normalization (11.8)), the integral becomes

\[I=(b-a)\int_0^1\frac{f((b-a)x(\xi)+a)}{w(x(\xi))}\,d\xi.\tag{11.10}\]

The conservation of the integration domain upon the change of variable is a direct consequence of the normalization of \(w(x)\). To evaluate this integral, one can directly apply the Monte Carlo method described in the preceding section, by averaging the new integrand, \(f/w\), over a set of *uniformly distributed* sampling points \(\xi_i\) from the interval \([0,1]\):

\[I\approx\frac{b-a}{n}\sum_{i=1}^{n}\frac{f((b-a)x(\xi_i)+a)}{w(x(\xi_i))}.\tag{11.11}\]

The performed change of variable may seem at first glance to turn the quadrature more complicated. The advantages of this technique become apparent only if one chooses the weight function \(w(x)\), in as
