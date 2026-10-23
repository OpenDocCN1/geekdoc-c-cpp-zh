```
double SphereGlobalFunction(double x)
{
    return x*x;
}
```

The output is:

```
Function Ackley, x and y values: -30, -8048.57
Function Rastrigin, x and y values: 2.87297e-08, 1.40831e-10
Function Sphere, x and y values: 2.84217e-14, 8.07794e-28
Function Test, x and y values: 8.09975e-21, 6.5606e-41
```

In general, many benchmark multivariate optimisation examples in the literature have been designed to produce the easily checked results:

```
f(x*) = 0,  where x* = (x*_0, ..., x*_{n-1}),    x*_j = 0,    j = 0, ..., n - 1.      (A2.13)
```

# A2.6 MULTIVARIATE OPTIMISATION

We conclude this appendix with a short overview of multivariate optimisation, which is a generalisation of the one-dimensional methods to n independent variables. We focus on the steepest ascent (descent) method, set up a basic software framework and give some examples for two-factor problems.

# A2.7 NONLINEAR PROGRAMMING AND MULTIVARIABLE OPTIMISATION

In this section we introduce the mathematical formulation of unconstrained multivariable optimisation problems (minimise or maximise a given objective function).

Consider the scalar function F : ℝⁿ → ℝ¹, n ≥ 1 that maps n-dimensional Euclidean space into the real line. In general, we wish to find a point x in Euclidean space that minimises or maximises this function. The general optimisation problem is to find a real number z such that:

```
optimise  z = F(x),    x = (x₁, ..., xₙ)ᵀ.      (A2.14)
```

Here F is called the objective function and the problem is unconstrained because there are no restrictions placed on x. We note that maximisation of F(x) is the same as the minimisation of its additive inverse − F(x). In the main, we are usually interested in minimisation problems.

We now introduce some terms. The gradient function ∇F associated with F = F(x₁, ..., xₙ) is a vector defined by:

```
∇F = ( ∂F/∂x₁, ..., ∂F/∂xₙ )ᵀ.      (A2.15)
```