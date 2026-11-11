# ## 7.9.2 Triangles in Space

The formulas given above—the parameterization of the triangle by a square, and the barycentric coordinates—don't depend on the dimension. They work just as well when the points A, B, and C are in 3-space as in the plane! There is one aspect of a triangle in 3-space that's different from the planar case: A triangle in 3-space is contained in a particular plane defined by an implicit equation of the form F(X) = (X − P) · n = 0. For P, we can use any of the three vertices of the triangle; for n, we can use the cross product

n = (B − A) × (C − B). (7.119)

If the angle at B is very near zero or π, this computation can be numerically unstable (see Section 7.10.4).

With this in mind, let's solve a frequently occurring problem: finding the intersection of a ray t ↦ P + td with a triangle ABC in 3-space. There are several cases. The intersection might occur where t < 0; the line containing the ray might not intersect the triangle at all; or the ray and the triangle might be in the same plane, and their intersection could be empty, a point, or a line segment. These last few cases have the property that a tiny numerical error—a slight change to one of the coordinates—can change the answer entirely. Such instabilities make the answers we compute almost useless. So, if the direction vector d is sufficiently close to perpendicular to the normal vector n, we'll return a result of “UNSTABLE” rather than computing an intersection. Our strategy is to first find the parameter t at which the ray intersects the plane of the triangle, then find Q = P + td, the intersection point in the plane, and finally find the barycentric coordinates of Q, which in turn tell us whether Q is inside the triangle.

For the most common situation—we'll make many ray-intersect-triangle computations for a single triangle—it's worth storing some additional data, per triangle, to speed the computation. We'll precompute the normal vector, n, and two vectors AB⊥ and AC⊥, in the plane of ABC with the property that (a) AB⊥ is perpendicular to AB, and (C − A) · AB⊥ = 1, and similarly for AC⊥. If X is the point X = αA + βB + γC in the plane of ABC, then we can compute γ easily as γ = AB⊥ · (X − C), and a similar computation gives us β. Finally, we find α = 1 − (β + γ).

With these ideas in mind, Listing 7.2 shows the actual structure.

If you consider any plane equation of the form f(X) = (X − A) · u = 0, then the value

f(P + td) = (P + td − A) · u (7.120)

is a linear function of t. For instance, if f is the equation of the plane of the triangle, we can solve for t to find the intersection of the ray with that plane. But suppose that f is the equation for the plane containing the edge AB and the normal vector n. Then f, when restricted to the triangle plane, is zero on the line AB, and nonzero on the point C (assuming the triangle is nondegenerate). That means that some multiple of f—namely X ↦ f(X)/f(C)—gives the barycentric coordinate at C. Now when we look at f(P + td), we can see how fast the C-coordinate of the projection of P + td into the triangle plane is changing. When we find the t-value at which the intersection occurs, we can therefore easily find the barycentric coordinate for the intersection point, as long as we know this plane equation.