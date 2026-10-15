![](bbox=[0.09, 0.12, 0.94, 0.27])

# FIGURE 2.18

(a) The identification of edges e and e′ involve the creation of a new boundary, which is a loop.

(b) Removing a "loop boundary" by adding a face.

of these two edges remove the boundary. Note that the edges can be identified in two ways: a sphere can be created, but also a projective plane, according to the way the edges are identified. In the case of the projective plane, a new twist is added.

# Connectivity

Until now, all considered surfaces are connected, i.e. informally, made of one piece: intuitively, you can walk on the surface between any two of its points. More formally, a path between two points x and y in X ⊂ ℝⁿ, where x, y ∈ X, means a continuous map γ : [0,1] → X, such that γ(0) = x and γ(1) = y. x and y are said connected by the path γ. The path is closed when γ(0) = γ(1).

Let X ⊂ ℝⁿ, and let R be the relation defined on points of X, such that xRy if and only if x and y are connected by a path in X. R is an equivalence relation, and its equivalence classes are the connected components of X: in other words, a path in X exists between any two points of a connected component, and no path exists in X between two points of two distinct connected components.

We can generalize our presentation of surfaces in order to take into account nonconnected surfaces, i.e. surfaces made of several connected components; the definition of the characteristic numbers (number of boundaries, orientability factor, genus) could be adapted, but it is more interesting (since more precise) to look at the characteristics of each connected component.

# 2.4 Manifolds, Quasi-manifolds, Pseudo-manifolds, Complexes

2-dimensional manifolds

Let us define a polygon of degree k as a closed disc (i.e. a 2-dimensional