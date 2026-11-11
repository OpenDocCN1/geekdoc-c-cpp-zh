ray (specified by a point and direction), we translate the point to the origin, rotate about the vector, and translate back. The projective PointToPoints method uses the same general approach that we used in two dimensions, replacing the solution of 2l simultaneous equations with a solution of four simultaneous equations and a $4 \times 4$ matrix inversion.

# ## 12.7 Associated Transformations

When we have an affine transformation $T$ on Euclidean space, we've said that we can transform either points or vectors, and we've incorporated this into our code. For an affine transformation, we've also seen how to transform covectors; in the code, we've defined a covector structure (which is very similar to the Vector structure in the sense of storing an array of doubles). And for affine transformations, there's an associated transformation, T.NormalMap, of covectors. We've bowed to convention here in calling this the "normal map" rather than the "covector map," since its use in graphics is almost entirely restricted to normal (co)vectors to triangles.

For a projective transformation, the associated map on vectors typically varies from point to point. In Figure 10.24, for instance, the top and bottom edges of the small square in the domain may be regarded as two identical vectors; after transformation, these vectors are no longer parallel. The associated map of vectors transformed them differently because they were based at different points. Thus, the associated vector transformation takes both a point and a vector as arguments. The details, and detailed rationale, are presented in a web addendum. The covector transform (for a projective transformation) similarly depends on the point of application.

One consequence of the point dependence for the vector and covector transformations of a projective transformation is that many operations—particularly those involving dot products of vectors, like computing how much light reflects from a surface—are best performed *before* the projective transformation near the end of the rendering pipeline.

# ## 12.8 Other Structures

Depending on how you plan to use the linear algebra library, it might make sense to create classes to represent other common geometric entities like rays, lines, planes in 3-space, ellipses, and ellipsoids (which are transformed to ellipses and ellipsoids, respectively, by nondegenerate linear and affine maps). A ray, for instance, might be represented by a Point and a direction Vector. It's then natural either to define

```
```c++
public static Ray operator*(AffineTransformation2 T, Ray r)
```
```

or to include in the AffineTransformation2 class a method like

```
```c++
public Ray RayTransform(Ray r)
```
```

A good implementation would transform the ray's Point by $T$, and would transform its direction Vector and normalize the result, because many computations on rays are easier when their directions are expressed as unit vectors.