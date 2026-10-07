# 216

# 7.6 The simplex algorithm

+   1. It includes the inequalities y ≥ 0, which are simply the transformed versions of the inequalities defining u.

+   2. u itself is the origin in y-space.

+   3. The cost function max c_u + cᵀy, where c_u is the value of the objective function at u and c is a transformed vector.

In short, we are back to the situation we know how handle! Figure 7.13 shows this algorithm in action, continuing with our earlier example.

The simplex algorithm is now fully defined. It moves from vertex to neighboring vertex, stopping when the objective is locally optimal, that is, when the coordinates of the local cost vector are all zero or negative. As we've seen, a vertex with this property must also be globally optimal. On the other hand, if the current vertex is not locally optimal, its local coordinate system includes some dimension along which the objective function can be improved, we move along this edge of the polyhedron—until we reach a neighboring vertex. By the nondegeneracy assumption (see footnote 3 in Section 7.6.1), this edge has nonzero length, and so strictly improve the objective value. The process must eventually halt.

# 7.6.3 Loose ends

There are important issues in the simplex algorithm that we haven't mentioned.

The starting vertex:

How do we find a vertex at start simplex? In our 2D and 3D examples we always started at the origin, which the linear programs happened to have inequalities with positive right-hand sides. In a general LP we won't always be fortunate. However turns out that finding a starting vertex can be reduced to an LP and solved by simplex!

To see this is done, with any linear program in standard form (recall Section 7.1.4), we know that LPs can always be rewritten this way.

```
min cᵀx such that Ax = b and x ≥ 0.
```

We first make that the right-hand sides of the equations are nonnegative: if b_i < 0, just multiply both sides of the ithth equation by -1.

Then we create a new LP as follows:

+   * Create new artificial variables z₁, ..., z_m ≥ 0, where m is the number of equations.
* Add zᵢ to the left-hand side of the ith equation.
* Let the objective, to be minimized, be z₁ + z₂ + ... + zₘ.

For this new LP, it's easy to come up with a starting vertex, namely, the one with z_i = b_i for all i and all other variables. Therefore we can solve it by simplex, to obtain the optimum solution.