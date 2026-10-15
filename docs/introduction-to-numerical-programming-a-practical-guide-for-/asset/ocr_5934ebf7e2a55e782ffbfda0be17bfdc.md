One can notice, though, that, as a difference relative to the function Bisect, the routine FalsPos updates after each partitioning of the bounding interval not only the boundaries $a_i$ and $b_i$, but also the corresponding function values, $f(a_i)$ and $f(b_i)$ (fa and fb in the code), since these are involved in calculating the next partitioning point $x_{i+1}$.

Even though the false position method is generally more efficient than the bisection method in terms of interval divisions necessary to achieve a given accuracy, it is likewise considered useful mainly for determining initial approximations for iterative methods, which converge more rapidly in the vicinities of the roots.

# 6.4 Method of Successive Approximations

One of the most representative numerical methods for finding zeros of real-valued functions is the *method of successive approximations*. Its importance, nevertheless, extends beyond the particular field of transcendental equations, since it actually represents a general strategy of solving mathematical problems by means of sequences of approximations that recursively converge to the solution. The classes of problems to which the method of successive approximations is applicable include among others differential, integral, and integro-differential equations.

Let us consider the transcendental equation

$$f(x)=0,$$

where $f(x)$ is a continuous real-valued function defined in some interval $[a,b]$. The method of successive approximations requires transforming the equation into the equivalent form

$$x=\varphi(x),$$

so that Equations 6.12 and 6.13 have the same roots. Obviously, it is always possible to cast Equation 6.12 under form (6.13) and this is feasible even if the function $f(x)$ does not explicitly contain the term $x$, for example by adding it to both sides of the equation.

Let $x_0$ be an initial approximation of the exact root $\xi$ of Equation 6.13. By replacing it in the right-hand side function $\varphi(x)$, one obtains a new approximation of the root:

$$x_1=\varphi(x_0).$$

Iterating this procedure, there results a sequence of numbers:

$$x_{i+1}=\varphi(x_i),\quad i=0,1,2,\ldots$$

If this sequence converges, then the limit $\xi=\lim x_i$ exists. Passing in Equation 6.14 to the limit and assuming $\varphi(x)$ to be continuous, we find

$$\lim_{i\to\infty}x_{i+1}=\varphi\left(\lim_{i\to\infty}x_i\right),$$

and herefrom

$$\xi=\varphi(\xi).$$

Hence, $\xi$ is a root of Equation 6.13 and it can be calculated, in principle, to any accuracy by using the recurrence relation (6.14).