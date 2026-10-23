A round-off error (rounding error) is the difference between the calculated approximation of a number and its exact mathematical value due to rounding. It is important to take this into consideration in numerical analysis and its applications where it is essential to estimate errors in calculations (including round-off errors) when using approximation equations and algorithms, especially when using finitely many digits to represent real numbers (which in theory have infinitely many digits). When a sequence of calculations subject to rounding error is made, errors may accumulate, sometimes dominating the calculation. In ill-conditioned problems, significant errors may accumulate.

We note that these definitions can be extended to cases in which the variables are vectors and matrices. In this case, the concept of the absolute value of a number is replaced by the concepts of vector norm and matrix norm, respectively. We discuss these concepts in more detail in later chapters when we need them in applying the finite difference method, for example.

# 8.4.1 Loss of Significance

This is an undesirable effect in calculations using finite-precision arithmetic. It occurs when an operation on two numbers increases relative error substantially more than it increases absolute error, for example in subtracting two nearly equal numbers (known as catastrophic cancellation). The effect is that the number of significant digits in the result is unacceptably reduced.

# 8.5 EXAMPLE: NUMERICAL QUADRATURE

We consider the common case of computing approximate values of one-dimensional integrals. In order to reduce the scope we focus on Gauss quadrature. This is a popular scheme in computational finance and it is a weighted sum of function values at specified points in the domain of integration. An n-point Gaussian quadrature rule yields a result that is exact for polynomials of degree 2n − 1 or less by a suitable choice of integration points and weights. In general, the domain of integration is [−1,1]:

∫₋₁¹ f(x)dx = Σⱼ=1ⁿ wⱼ f(xⱼ)

where:

wⱼ = weights, xⱼ = integration points j = 1, …, n.

This formula only produces good results if the function f(x) can be accurately approximated by a polynomial. For example, it is not suitable for functions with singularities. For a general interval (a, b) the Gauss integration rule becomes:

∫ₐᵇ f(x)dx ≈ (b − a)/2 Σⱼ=1ⁿ wⱼ f( (b − a)/2 xⱼ + (a + b)/2 ).

In this case the related polynomials are Legendre polynomials (Abramowitz and Stegun, 1965, formula 25.4.29).