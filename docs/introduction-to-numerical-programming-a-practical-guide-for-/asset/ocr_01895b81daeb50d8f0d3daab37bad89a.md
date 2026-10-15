# 10.9 Midpoint Rule

In an attempt to consistently construct an open-type formula not employing explicitly the end points of the integration interval, one can start by approximating the integral of f(x) on [a, b] by the trapezoidal rule, respectively for the integration spacings h and h/2:

∫ₐᵇ f(x)dx ≈ h [ f₁/2 + f₂ + f₃ + ⋯ + fₙ/2 ],  (10.54)

∫ₐᵇ f(x)dx ≈ h/2 [ f₁/2 + f₃/₂ + f₂ + f₅/₂ + f₃ + ⋯ + fₙ/2 ].  (10.55)

The integrand values for semiinteger indexes correspond to the midpoints of the (n − 1) integration subintervals of length h:

fᵢ₊₁/₂ ≡ f(a + (i − 1/2)h).

Subtracting twice Equation 10.55 from 10.54, the integer-index values (including those for the domain boundaries) cancel out and one obtains the so-called midpoint rule:

∫ₐᵇ f(x)dx ≈ h ∑ᵢ₌₁ⁿ⁻¹ fᵢ₊₁/₂.  (10.56)

Not using information from the integration limits, this is indeed an open formula. The remainder of the midpoint rule results from the remainders of the trapezoidal formulas 10.54 and 10.55, and it turns out to maintain the same order with respect to h:

R = (b − a)h² / 24 f''(ξ),   ξ ∈ [a, b].  (10.57)

The straightforward implementation of the midpoint rule (10.56) is of limited practical interest. On the contrary, an adaptive algorithm with automatic integration step control, similar to the one implemented in function qTrapzCtrl, is most useful for practical evaluations of improper integrals of the second kind.

The particular arrangement of the integration abscissas in the midpoint rule does not enable, however, a recurrence relation between approximations resulted by doubling the number of subintervals. Such an approach is possible instead by tripling the number of subintervals and involves only integrand values in the new mesh points, by implicitly reusing the information from previously used nodes, as can be seen

![](bbox=[0.25, 0.78, 0.75, 0.88])

FIGURE 10.5 Algorithmic reduction of integration subintervals in the adaptive midpoint rule. Empty circles indicate new values that have to be calculated, while filled circles indicate values already calculated at the previous steps.