You can experiment with the code using various floating-point types and values for h. For example, we could keep decreasing h by a factor of 10 to determine when the divided differences start producing incorrect results for a given floating-point type. For example, in some cases the divided difference formula (22.9) can produce the value zero even though the exact second derivative is not zero! We discuss numerical differentiation with multiprecision data types in Appendix 1 to this book.

# 22.3.5 What is the Optimum Step Size?

What is the optimum value of h that minimises the sum of the magnitudes of the roundoff and discretisation errors (Conte and de Boor, 1981)? To answer this question in a concrete case, we take the example in Section 22.3.3 again. Let us assume that the error in computing e^x is ±1 × 10^-8. Then it can be shown that the roundoff when using formula (22.7) is:

R = ± (2 × 10^-8) / (2h).

The discretisation error can be computed approximately from equation (22.7):

T = -1/6 h^2 (f''' ~ 1).

The function to be minimised is thus:

g(h) = |R| + |T| = 10^-8 / h + 1/6 h^2.

The minimum value is the solution of g'(h) = 0 or h^3 = 3 × 10^-8. The optimum value is thus:

h = 10^-3 ∛30 ≈ 0.003.

You can experiment with various values to verify this result. See also Exercise 4.

# 22.4 NUMERICAL GREEKS

We now come to the topic of computing option sensitivities and how they are used to reduce risk. For more details, we refer to Haug (2007) and Hull (2006). Option sensitivity is the derivative of an option with respect to one or more parameters in the Black–Scholes equation. We focus on option delta, which is the derivative of the option value with respect to the underlying S while gamma is the derivative of delta with respect to S. In general, we wish to compute options accurately and efficiently. We list some choices:

+   - G1: Exact Greeks (Haug, 2007).
+   - G2: Numeric Greeks (Haug, 2007).
+   - G3: Using Monte Carlo and related simulation methods (Glasserman, 2004).
+   - G4: Using the binomial method.
+   - G5: Using the values from an FD option pricer (Duffy, 2004) and applying method G2.