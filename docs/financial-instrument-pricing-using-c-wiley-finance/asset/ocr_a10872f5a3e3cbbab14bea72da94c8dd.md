We conclude the discussion of the numerical approximation of the heat equation by comparing the run-time performance of the Crank–Nicolson (CN), Saul’yev ADE (ADEI) and Barakat and Clark ADE (ADEII) methods. In general, it is a trade-off between efficiency and the number of operations in order to achieve a given accuracy. We provide some basic conclusions:

+   - ADEI is fastest, then ADEII followed by CN (in general, ADEI is three times faster than CN, ADEII is [20, 50]% faster than CN depending on the size of the problem).
+   - CN and ADEII deliver more or less the same level of accuracy. ADEI is the least accurate of the three methods.
+   - For ADE in general, the rule of thumb for accurate results is NT ~ 5*NX.

We recommend that you perform your own experiments on the PDEs that are of interest to you.

# 13.5 CUBIC SPLINE INTERPOLATION

In this section we discuss a special kind of function called the cubic spline (Ahlberg, Nilson and Walsh, 1967). This is a function that is defined in an interval and whose values are equal to given values at prescribed mesh points in the interval. In each subinterval the spline is a third-order polynomial and both it and its first and second derivatives are continuous at the interior mesh points. We construct the cubic spline by solving a tridiagonal system of equations (that we already know how to solve and hence is a good way to test and debug our code). Our original aim in this chapter was primarily to test the accuracy of tridiagonal solvers but we then realised that it is useful in a wider context, for example:

+   - Interpolation of discrete data and producing a smooth function.
+   - Approximating continuous functions.
+   - Numerical integration (Stroud, 1974).
+   - Solving boundary value problems.

In interest rate applications cubic splines are used in the construction of yield curves and forward curves. In general, the x-axis corresponds to time while the y-axis can correspond to zero rates, forward rates, discount rates or some function of these rates (Duffy and Germani, 2013; Ron, 2000). More generally, cubic splines are used to interpolate between values that are known at discrete mesh points. We shall see examples in later chapters when we approximate the solution of the Black–Scholes PDE by the finite difference method. Having computed the option price at discrete points we can then interpolate these values to produce a value for any arbitrary value of the underlying variable.

We discuss two popular interpolation methods in this section. First, consider the pair of data values (x₀, y₀) and (x₁, y₁). We are interested in drawing a straight line between these points. Some algebra shows that the value y corresponding to a given value x is given by:

```
y = y₀ + (x - x₀) (y₁ - y₀)/(x₁ - x₀).  (13.32)
```