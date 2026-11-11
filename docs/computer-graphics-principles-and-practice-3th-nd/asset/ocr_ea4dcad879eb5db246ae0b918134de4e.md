# 8.2.1  Boundaries

The **boundary** of a 1D mesh defined as a *formal sum* of the vertices of the mesh in which the coefficient of each vertex is determined as follows: Each edge from vertex *i* to vertex *j* adds +1 to the coefficient for *j*, and −1 to the coefficient for *i*; we sometimes write that the boundary of the edge *ij* is *j − i*. Applying this to the mesh above, we find that the boundary formal sum is (reading edge by edge, and writing *vᵢ* for the *i*th vertex)

$(v_2-v_1)+(v_3-v_2)+(v_4-v_3)+(v_1-v_4)+(v_6-v_5), \qquad (8.1)$

![](bbox=[0.71, 0.211, 0.93, 0.352])

Figure 8.4: A wagon-wheel-shaped mesh. An arrow from vertex *i* to vertex *j* indicates that (*i, j*) is an edge of the mesh, and not (*j, i*).

which simplifies to *v₆ − v₅*. Informally, we say that the boundary consists of vertices 5 and 6.

The reason for the formalism arises when we consider more interesting meshes, like the one shown in Figure 8.4. The boundary in this case consists of *v₁ + v₂ + v₃ + v₄ + v₅ − 5v₀*.

A 1D mesh whose boundary is zero (i.e., the formal sum in which all coefficients are zero) has the property that it’s easy to define “inside” and “outside” by a rule like the winding number rule for polygons in the plane. Such a mesh is called **closed**.

A 1D mesh where each vertex has degree 2 (i.e., where each vertex has an arriving edge and a leaving edge) is said to be a **manifold mesh**: In the abstract graph, every point has a neighborhood (a set of all points sufficiently near it) that resembles a small part of the real number line. A point in the interior of an edge, for example, has the edge interior as such a neighborhood. A vertex has the union of the interiors of the two adjacent edges, together with the vertex itself, as such a neighborhood.

We use the term “manifold mesh” to suggest that such meshes are like *manifolds*, which we will not formally define; there are many books that introduce the idea of manifolds with the appropriate supporting mathematics [dC76, GP10]. Informally, however, an *n*-dimensional manifold is an object *M* with the property that for any point *p* ∈ *M*, there’s a neighborhood of *p* (i.e., a set of all points in *M* close to *p*, defined appropriately) that looks like the set {**x** ∈ ℝⁿ : ||**x**|| < 1} (the “open ball”) in ℝⁿ. “Looks like” means that there’s a continuous map from the ball to the neighborhood and back. (These continuous maps are also required to be “consistent” with one another wherever their domains overlap; the precise details are beyond the scope of this book.) For example, the unit circle in the plane is a 1-manifold because one neighborhood of the point with angle coordinate θ consists of all points with coordinates θ − 0.1 to θ + 0.1; the correspondence to the unit ball in ℝ (i.e., the open interval −1 < x < 1) is u ↦ 10(u − θ). Similarly, familiar smooth surfaces in 3-space like the sphere, or the surface of a donut, are 2-manifolds. An atlas (i.e., a book showing maps of the whole world) is a kind of demonstration that the sphere is a manifold: Each page of the atlas gives a correspondence between some region of the globe (e.g., Western Europe) and a portion of the plane (i.e., the page of the atlas that shows Western Europe).

Shapes with corners (like a cube) can also be manifolds, but they are not *smooth* manifolds, which is what’s usually meant when the term is used informally—a continuous map that takes a small region around the corner of the cube and sends it to the plane ends up distorting things too much for all the required conditions for “smoothness” to hold.