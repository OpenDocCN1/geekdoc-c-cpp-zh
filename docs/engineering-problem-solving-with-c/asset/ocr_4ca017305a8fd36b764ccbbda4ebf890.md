![](bbox=[0.25, 0.08, 0.9, 0.5])

# Figure 6.10 Cubic polynomials.

![](bbox=[0.22, 0.56, 0.65, 0.75])

# Figure 6.11 Incremental search.

is negative on one end and positive on the other. We are then assured that there is at least one root in this subinterval.

There are many variations of the incremental-search technique. The one that we discuss begins with the selection of a step size that is used to subdivide the original interval into a group of smaller subintervals, as shown in Figure 6.11. For each subinterval, we evaluate the function at both endpoints. If the product of the function values is negative, then there is a root in this subinterval. (A negative product implies that one function value is positive, whereas