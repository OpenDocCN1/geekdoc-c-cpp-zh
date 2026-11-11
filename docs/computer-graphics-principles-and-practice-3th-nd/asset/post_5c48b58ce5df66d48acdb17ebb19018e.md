
- (c) Show that the formula is correct by arguing that area is a continuous function of coordinates, and that there is, at most, one extension of a continuous function on $X$ to a continuous function on $X\cup\operatorname{boundary}(X)$ when $X$ is a subset of $\mathbb{R}^n$.

**Exercise 7.15:** Another approach to generalizing the area formula from the “one vertex at the origin” case to the general case is this: Compute the signed area of the triangle $P_0P_1P_2$ by computing the signed areas of $OP_0P_1$, $OP_1P_2$, and $OP_2P_0$ and then adding or subtracting appropriately. Draw a picture to figure out what the relationship among the four signed areas should be, and use it to derive the general formula for the signed area of $P_0P_1P_2$.

**Exercise 7.16:** Numerical considerations: In the formula for the area of a polygon, suppose that we are using finite precision arithmetic and we add $L$, where $L$ is a very large number, to the $x$-coordinates of all the polygon’s vertices. What happens to the computation? What if we instead perform the computation by writing the coordinates of the vertices in a coordinate system based at the “center” of the polygon—the average of all the vertices?

**Exercise 7.17:** Consider a ray that starts at $P=(-3,-3)$ and has direction $\mathbf{d}=\begin{bmatrix}1\\2\end{bmatrix}$. It intersects the ellipse defined by $(x/3)^2+y^2=1$ at two points. To find these points, we can write

$$R(t)=P+t\mathbf{d}\tag{7.142}$$

$$R(t)^{\mathsf{T}}\begin{bmatrix}1/9 & 0\\0 & 1\end{bmatrix}R(t)=1\tag{7.143}$$

where the $^{\mathsf{T}}$ indicates transpose. If we solve the second equation for $t$, we will have found the parameters $t_1$ and $t_2$ of the intersection points, from which we can compute the points.

- (a) Draw a picture representing this situation.
- (b) Confirm that the equations above really do determine the points of intersection by writing out the product explicitly.
- (c) Now consider the intersection of the ray defined by the point $Q=(-1,-3)$ and the direction $\mathbf{e}=\begin{bmatrix}1/3\\2\end{bmatrix}$, with the unit circle. Once again, draw a picture and express this problem as a similar pair of equations; the matrix in this case will be the identity matrix.
- (d) Expand these later equations; compare them to the ones you arrived at in part (b).
- (e) Explain the similarity: How are $\mathbf{d}$ and $\mathbf{e}$ related? How are the ellipse and the unit circle related? We’ll return to this kind of transformation from a general problem (compute an intersection with an ellipse) to an equivalent standard problem (compute an intersection of a different ray with the unit circle) when we study ray tracing.

**Exercise 7.18:** The function $\gamma:\mathbb{R}\to\mathbb{R}^2:t\mapsto(3+2t,4-3t)$ describes a line in parametric form.

- (a) Find two distinct points $P$ and $Q$ on the line. (There are an infinite number of correct answers to this part.)
- (b) Use these two to find an implicit form for the line; convert via algebra to the form $Ax+By+C=0$.

**Exercise 7.19:** You're given two nondegenerate line segments in the plane, the first with endpoints *A* and *B* and the second with endpoints *C* and *D*, and all coordinates are integers. Your job is to determine whether the segments intersect, and the intersection point, if any.

- (a) Write a short program to do this. If the segments are parallel, there are three cases: They're disjoint (return *false*), they share an endpoint (return *false*), or they overlap in an interval (return *true*, but don't return an intersection point, since it's not unique). If the segments are nonparallel and intersect, they may share an endpoint (return *false*), the endpoint of one may be interior to the other (return *true*, and the endpoint), or the interiors of the segments may intersect at some point (*x*, *y*) whose coordinates may not be integers, but will be rational numbers. In this case, you should return an *integer triple* (*x*, *y*, *w*), where the intersection is at (*x*/*w*, *y*/*w*).
- (b) Explain why returning an integer triple is more useful than returning a floating-point representation of the rational coordinates.
- (c) Suppose you have two integer triples of the form above, (*x*₁, *y*₁, *w*₁) and (*x*₂, *y*₂, *w*₂). How would you test them for “equality,” that is, how would you test whether they represent the same rational point in the plane?
- (d) For an extra challenge, try to write all your code in part (a) so that there are no divisions, and the code is as clean as possible. The sort of multiple-case mess that's implicit in programs like this arises from the multiple possible ways that segments can intersect; you can't really make the code *too clean*.

## Chapter 8: A Simple Way to Describe Shape in 2D and 3D

### 8.1 Introduction

We now turn to a discussion of the **triangle mesh**, the most widely used representation of shape in graphics. Triangle meshes consist of many triangles joined along their edges to form a surface (see Figure 8.1). Other meshes, in which the basic elements are quads (quadrilaterals), or other polygons are sometimes used, but there can be problems associated with them. For instance, it’s easy to create a quadrilateral whose four vertices do not all lie in a plane; how should the interior be filled in? For triangles, this is not a problem: There’s always a plane containing any three vertices. Because triangle meshes are so widespread, we concentrate on them in this chapter.

It’s easy to see how to create certain shapes with triangle meshes. Starting with any polyhedron, for instance, we can subdivide the faces into triangles. Figure 8.2 shows this for the cube. For more complex shapes, it’s possible to approximate the shape with a mesh. One way to do this is to find the locations of many points on the shape, and then connect adjacent locations with a mesh structure. Such an approximation, if the points are close enough to one another, can look very much like a smooth surface. Consider the case of the icosahedron, which looks a lot like a sphere: Each point of the icosahedral mesh is very close to a point of the sphere, and vice versa. Similarly, each normal vector to a triangle mesh is very close to a vector normal to the sphere at a corresponding point, and vice versa. There is a distinction, however: The function that assigns normal vectors to points of the sphere is continuous, while for the icosahedron, it’s **piecewise constant** (the normal vector doesn’t change as you move about on a triangular facet). This distinction can be important when we try to consider the reflection of light from surfaces described with planar facets.

![](img/f464cd0043eb5336aa0543fe20a0561b_237_0.png)

*Figure 8.1: A triangle mesh, consisting of vertices, edges, and triangular faces.*

### 8.2.1 Boundaries

The **boundary** of a 1D mesh is defined as a *formal sum* of the vertices of the mesh in which the coefficient of each vertex is determined as follows: Each edge from vertex *i* to vertex *j* adds +1 to the coefficient for *j*, and −1 to the coefficient for *i*; we sometimes write that the boundary of the edge *ij* is *j − i*. Applying this to the mesh above, we find that the boundary formal sum is (reading edge by edge, and writing *vᵢ* for the *i*th vertex)

$$
(v_2-v_1)+(v_3-v_2)+(v_4-v_3)+(v_1-v_4)+(v_6-v_5), \qquad \tag{8.1}
$$

![](img/f464cd0043eb5336aa0543fe20a0561b_240_0.png)

Figure 8.4: A wagon-wheel-shaped mesh. An arrow from vertex *i* to vertex *j* indicates that (*i, j*) is an edge of the mesh, and not (*j, i*).

which simplifies to *v₆ − v₅*. Informally, we say that the boundary consists of vertices 5 and 6.

The reason for the formalism arises when we consider more interesting meshes, like the one shown in Figure 8.4. The boundary in this case consists of *v₁ + v₂ + v₃ + v₄ + v₅ − 5v₀*.

A 1D mesh whose boundary is zero (i.e., the formal sum in which all coefficients are zero) has the property that it’s easy to define “inside” and “outside” by a rule like the winding number rule for polygons in the plane. Such a mesh is called **closed**.

A 1D mesh where each vertex has degree 2 (i.e., where each vertex has an arriving edge and a leaving edge) is said to be a **manifold mesh**: In the abstract graph, every point has a neighborhood (a set of all points sufficiently near it) that resembles a small part of the real number line. A point in the interior of an edge, for example, has the edge interior as such a neighborhood. A vertex has the union of the interiors of the two adjacent edges, together with the vertex itself, as such a neighborhood.

We use the term “manifold mesh” to suggest that such meshes are like *manifolds*, which we will not formally define; there are many books that introduce the idea of manifolds with the appropriate supporting mathematics [dC76, GP10]. Informally, however, an *n*-dimensional manifold is an object *M* with the property that for any point *p* ∈ *M*, there’s a neighborhood of *p* (i.e., a set of all points in *M* close to *p*, defined appropriately) that looks like the set {**x** ∈ ℝⁿ : ||**x**|| < 1} (the “open ball”) in ℝⁿ. “Looks like” means that there’s a continuous map from the ball to the neighborhood and back. (These continuous maps are also required to be “consistent” with one another wherever their domains overlap; the precise details are beyond the scope of this book.) For example, the unit circle in the plane is a 1-manifold because one neighborhood of the point with angle coordinate θ consists of all points with coordinates θ − 0.1 to θ + 0.1; the correspondence to the unit ball in ℝ (i.e., the open interval −1 < x < 1) is u ↦ 10(u − θ). Similarly, familiar smooth surfaces in 3-space like the sphere, or the surface of a donut, are 2-manifolds. An atlas (i.e., a book showing maps of the whole world) is a kind of demonstration that the sphere is a manifold: Each page of the atlas gives a correspondence between some region of the globe (e.g., Western Europe) and a portion of the plane (i.e., the page of the atlas that shows Western Europe).

Shapes with corners (like a cube) can also be manifolds, but they are not *smooth* manifolds, which is what’s usually meant when the term is used informally—a continuous map that takes a small region around the corner of the cube and sends it to the plane ends up distorting things too much for all the required conditions for “smoothness” to hold.
