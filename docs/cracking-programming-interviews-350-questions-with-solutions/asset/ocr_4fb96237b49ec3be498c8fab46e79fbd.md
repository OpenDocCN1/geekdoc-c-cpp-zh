p.(line from y to z) ≥ 0

By symmetry, we take for granted that

p.(line from z to y) ≥ 0

Next we give the triangle analysis. With the linear algorithm we compute in.V, on.V, and out.V for the triangle V. If out.V holds, then, on account of P₁, also out.V holds. If in.V holds, then, on account of P₀ and u's convexity, also in.u holds. If on.V holds (i.e. each edge of the triangle has a p-value ≥ 0, and one or two p-values (= 0) we distinguish two cases:

+   1. Two edges have a p-value = 0; and they coincide with the vertex joining these two edges, etc coincides with a vertex of u, hence on.u holds.
+   
+   2. One edge has a p-value = 0; x then is in the interior of that edge. If that edge is an edge of u, on.u holds. If that edge is not an edge of u, it is an edge between two nonadjacent vertices of u, so that (u is convex) in.u holds.

# Remarks

First we observe that the line from y to z is a clockwise boundary line of V₀, the line from z to y is a clockwise boundary line of V₁, and p.(line from y to z) = −p.(line from z to y).

Secondly we consider two cases for p.(line from y to z) ≥ 0:

+   1. p.(line from y to z) = 1, hence p.(line from z to y) = −1, hence (because line from z to y is a clockwise boundary line of V₁) out.V₁, hence out.V₀ ⇒ out.V₁.
+   
+   2. p.(line from y to z) = 0. Again we distinguish two cases:
+      a) x on the line segment yz (bounds included), hence on.V₀ and on.V₁, hence ¬out.V₀ and ¬out.V₁, hence out.V₀ ⇒ out.V₁.
+      b) x not on the line segment yz, hence because line between y and z is a boundary line of V₁, out.V₁, hence out.V₀ ⇒ out.V₁.

# 1.23  The problem of the balanced segments

# Problem Description

For a sequence X (i: 0 ≤ i < N), N ≥ 0, of 0's and 1's, a balanced segment X(i : p ≤ i ≤ q) of length q − p is defined as a segment such