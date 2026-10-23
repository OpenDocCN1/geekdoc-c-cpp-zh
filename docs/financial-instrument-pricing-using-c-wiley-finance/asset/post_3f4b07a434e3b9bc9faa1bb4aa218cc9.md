
More detailed and technical information can be found in Appendix 2. This chapter concentrates on the mathematics and software design issues.

## 19.2 MATHEMATICAL AND NUMERICAL BACKGROUND

Consider the scalar function f: R^n → R^1, n ≥ 1 that maps n-dimensional Euclidean space to the real line. In general, we wish to find a point x in n-dimensional Euclidean space that minimises or maximises this function. The general optimisation problem is:

optimise z = f(x),    x = (x₁, ..., xₙ)ᵀ.    (19.1)

Here, f is called the objective function and xᵀ is the transpose of the vector x. The problem is unconstrained because there are no restrictions placed on the whereabouts of the solution x. We note that maximisation of f(x) is the same as the minimisation of its additive inverse −f(x). In the main, we are usually interested in minimisation problems.

In general, there are no constraints on the point x that solves the optimisation problem (19.1). The objective function has a local (or relative) minimum at x₀ if there exists an interval (or more generally, a neighbourhood) around x₀ such that f(x) ≥ f(x₀) for all x for which the function is defined. If f(x) ≥ f(x₀) for all x for which the function is defined then x₀ is called a global (absolute) minimum. In general, the optimisation problem (19.1) may have zero, one or many solutions.

We can extend problem (19.1) by discussing multivariable optimisation problems with constraints. There are many kinds of constraints, for example:

- Equality constraints:

  g(x) = 0.    (19.2)

- Inequality constraints:

  g(x) ≥ 0.    (19.3)

- Linear constraints:

  g(x) = A xᵀ − b (g(x) = (g₁(x), ..., gₘ(x))ᵀ)    (19.4)

  where A is a constant n × m matrix, b is an m-dimensional vector, x is an n-dimensional vector, g is a given function of its arguments and the symbol T denotes the transpose of a vector or of a matrix.

A special case is a quadratic program in which each constraint is linear and the objective function has the form:

f(x₁, ..., xₙ) = Σᵢ=1ⁿ Σⱼ=1ⁿ cᵢⱼ xᵢ xⱼ + Σⱼ=1ⁿ dⱼ xⱼ    (19.5)

where cᵢⱼ and dⱼ are known constants, 1 ≤ i, j ≤ n.

We now reduce the scope of the problem in this chapter to univariate unconstrained nonlinear problems of the form:

optimise z = f(x), x ∈ (−∞, ∞). (19.6)

In some cases we may be interested in finding a local or global minimum in an interval, thus leading to a one-variable constrained problem:

optimise z = f(x) subject to a ≤ x ≤ b. (19.7)

Closely related to optimisation is the problem of finding the zeros (or roots) of a nonlinear function:

f(x) = 0, x ∈ (−∞, ∞). (19.8)

In general, it is not possible to find an analytical solution to this problem and we must employ numerical methods, for example the bisection or Newton–Raphson method.

It is possible to find the solution of a system of n nonlinear equations:

f(x) = 0, x = (x₁, …, xₙ)ᵀ ∈ ℝⁿ (19.9)

where:

f(x) = (f₁(x), …, fₙ(x))ᵀ, f : ℝⁿ → ℝⁿ

F(x) = Σⱼ=1ⁿ fⱼ²(x) = f(x)ᵀ f(x)

by defining the following objective function:

f(x*) = 0 ⇔ x* is a minimum of F(x). (19.10)

The desired solution is F(x*) = 0 and this is true only when x* satisfies (19.9). The function F(x) may have any number of local minima with F(x*) > 0 which have no relevance to the current problem except as nuisances. Hence if there is any solution at all it is the global minimum that we require. This is advantageous in the one-dimensional case for unimodal functions. A unimodal function f(x) defined in an interval is one that has one and only one point at which f(x) has a local minimum or local maximum.

## 19.3 SEQUENTIAL SEARCH METHODS

In some cases it may be possible to find a function minimum by using school calculus, but in general we need to employ numerical methods. In this section we discuss two methods for unimodal functions in an interval:

- The three-point interval search.
- Golden-mean search.

These methods can be seen as divide-and-conquer methods because we bracket the interval into subintervals and we discard those subintervals in which we know that the minimum value does not lie. The three-point interval search method divides the interval into quarters and the objective function is evaluated at the three equally spaced interior points. The interior point yielding the best value of the objective function is determined. The new subinterval is now centred at this point and made up of two-quarters of the current interval. The golden-mean search method is applicable to a strictly unimodal function by successively narrowing the range of values inside which the extremum is known to exist. In this case the algorithm maintains the function values for triples of points whose distances form a golden ratio. A readable discussion of these methods can be found in Bronson and Naadimuthu (1997).

## 19.4 SOLUTIONS OF NONLINEAR EQUATIONS

The theory of nonlinear equations is well established. In this section we discuss the problem of finding real values x that satisfy the equation:

f(x) = 0

where f is a real-valued function. The methods to be discussed are:

- Bisection method.
- Newton’s method.
- Secant method.
- Steffensen iteration.

The bisection method assumes that the function f(x) has a zero in the interval (a, b) and we assume that the signs are opposite at the end points, that is f(a)f(b) < 0. For convenience, let us assume that f(a) < 0. The method divides the interval into equal parts until we arrive at an interval that is so small that it contains the zero of the function and is small enough to satisfy the given tolerance. The basic algorithm is defined using a sequence of intervals of ever-diminishing size:

(a, b) ⊃ (a₁, b₁) ⊃ (a₂, b₂) ⊃ (a₃, b₃) ⊃ ...

where:

(aₖ, bₖ) = { (mₖ, bₖ₋₁) if f(mₖ) < 0
(aₖ₋₁, mₖ) if f(mₖ) > 0 } (19.11)

and

mₖ = ½(aₖ₋₁ + bₖ₋₁).

After n steps the root is in an interval having a length given by:

bₙ − aₙ = 2⁻¹(bₙ₋₁ − aₙ₋₁) = 2⁻ⁿ(b − a) (19.12)

mₙ₊₁ (is the root). (19.13)

Thus, the deviation from the exact root α is given by:

α = m_{n+1} ± d_n, d_n = 2^{-n-1}(b − a). (19.14)

In general, we are interested in locating the zero of the function to within a given tolerance TOL. This means that we calculate the number of subdivisions of the original interval (a, b). To this end, some arithmetic based on equation (19.14) gives us the following estimate:

n > [log((b−a)/TOL)] / log 2 − 1. (19.15)

The advantage of the bisection method is that we can always define an interval of arbitrary size in which the zero is located. The disadvantage is that convergence is slow. In fact, at each step we gain one binary digit in accuracy. We note also that the rate of convergence is independent of the given function f(x). The method may be used to give us good initial approximations to second-order nonlinear solvers.

Newton–Raphson is probably one of the most famous iterative schemes in numerical analysis. The main advantage of the Newton–Raphson method is that it converges quickly. We say that its order of convergence is two, by which we mean that the error at each iteration decreases quadratically:

x_{n+1} = x_n + h_n, h_n = − f(x_n)/f'(x_n), n = 0, 1, 2, … (19.16)

The disadvantage is that the choice of the initial approximation is vitally important. If it is not chosen carefully the method may not converge at all or it may even converge to the wrong solution. A possible solution is to first use the bisection method to bracket the solution to a given accuracy (for example, 10^{−1}) and then apply the Newton–Raphson method. Furthermore, we must have an analytical expression for the derivative of f and this may not always be available.

The secant method can be derived from the Newton–Raphson method by approximating the derivative by divided differences. The resulting iterative scheme now becomes:

x_{n+1} = x_n + h_n, h_n = −f_n (x_n − x_{n−1})/(f_n − f_{n−1}), f_n ≠ f_{n−1} where f_n = f(x_n). (19.17)

We note that the secant method needs two initial approximations in contrast to Newton–Raphson which only needs one initial approximation. In general, we must be careful when programming the secant method when the function values are close to each other or when the solutions at levels n and n + 1 are close to each other; in such cases we calculate terms that are effectively 0/0!

A disadvantage of the secant method is that it is only first-order accurate. In order to achieve second-order accuracy without having to evaluate derivatives we propose Steffensen's method, given by the scheme:

x_{n+1} = x_n − f(x_n)/g(x_n)
