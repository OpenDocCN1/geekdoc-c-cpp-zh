These methods can be seen as divide-and-conquer methods because we bracket the interval into subintervals and we discard those subintervals in which we know that the minimum value does not lie. The three-point interval search method divides the interval into quarters and the objective function is evaluated at the three equally spaced interior points. The interior point yielding the best value of the objective function is determined. The new subinterval is now centred at this point and made up of two-quarters of the current interval. The golden-mean search method is applicable to a strictly unimodal function by successively narrowing the range of values inside which the extremum is known to exist. In this case the algorithm maintains the function values for triples of points whose distances form a golden ratio. A readable discussion of these methods can be found in Bronson and Naadimuthu (1997).

# 19.4 SOLUTIONS OF NONLINEAR EQUATIONS

The theory of nonlinear equations is well established. In this section we discuss the problem of finding real values x that satisfy the equation:

f(x) = 0

where f is a real-valued function. The methods to be discussed are:

+   - Bisection method.
+   - Newton’s method.
+   - Secant method.
+   - Steffensen iteration.

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