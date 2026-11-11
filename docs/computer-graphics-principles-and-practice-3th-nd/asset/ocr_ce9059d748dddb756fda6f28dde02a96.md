◇ (b) Now use this to explain why every 3 × 3 skew-symmetric matrix has 0 as an eigenvalue, hence det S = 0.

**Exercise 11.10:** In the description of the virtual-sphere controller, we used the angle θ = cos⁻¹(P · Q), which involves a dot product of points rather than vectors. This worked only because we assumed that the center of our virtual sphere was the origin.

+   - (a) Suppose the center was some other point B; how would we have computed θ?

+   - (b) Now suppose that the virtual sphere was no longer assumed to be a unit sphere. How would we compute θ?

**Exercise 11.11:** Use the 3D test bed to implement virtual-sphere control for viewing.

**Exercise 11.12:** Given a point P and a direction v, describe how to build a transformation on R³ that rotates by θ about the line determined by P and v so that the plane through P, orthogonal to v, rotates counterclockwise by θ when viewed from the point P + v.

**Exercise 11.13:** We saw in Chapter 7 that if f is the test function for the plane containing the point Q and with normal n, that is, f(P) = (P − Q) · n, then we could compute the intersection of the ray t → A + tv with this plane by writing g(t) = A + tv and solving f(g(t)) = 0. Suppose that T is a linear transformation with 4 × 4 matrix M—perhaps translation by some amount, or a rotation about the y-axis by 30°. We can imagine applying T to every point of the plane defined by f to get a new plane, and then finding the intersection of our ray with the new plane.

+   - (a) George proposes that a test function f̃ for the new plane can be defined by f̃(P) = f(T(P)). Is he correct? If not, adjust his claim to a correct one.

+   - (b) Show that f(g(t)) = 0 if and only if f̃(g(t)) = 0, where g(t) = M⁻¹A + tM⁻¹w.

+   - (c) Describe how you can use the idea of part (b) to compute a ray-object intersection between a ray and an object that has been transformed by some affine transformation, assuming you know how to do ray-object intersection for some standard form of the object. This allows you, for instance, to ray-trace a stretched, rotated unit sphere (i.e., an ellipsoid) if you only know how to ray-trace the standard unit sphere.

+   - ◇ (d) Often in ray tracing it’s necessary to determine not only the intersection point, but also the normal vector at the intersection point. Suppose that instead of intersecting a ray R with a transformed sphere, you intersect an inverse-transformed version of R with the unit sphere at the origin, and find the intersection at a point P = (x,y,z) with normal vector n = [x y z]ᵀ. How can you find the normal vector to the transformed sphere? Note: This approach to ray tracing is somewhat out of favor for complex scenes, as traversing the modeling hierarchy for every ray is a big cost. Instead, flattening the hierarchy by converting everything to triangles and using a spatial data structure to accelerate intersection testing turns out to be faster in general, but not always: In a forest of 1 million identical trees, each a copy of a single million-triangle tree, the spatial data structure approach fails. Instead, we make a spatial data structure whose leaves are bounding boxes for the individual trees, use the transforming-rays trick of this exercise, and proceed to trace each ray in the archetype tree’s modeling space, possibly using a spatial data structure there to accelerate the computation. This is another application of the Coordinate-System/Basis principle.