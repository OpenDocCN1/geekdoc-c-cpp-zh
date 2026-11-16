![](bbox=[0.16, 0.11, 0.83, 0.3])

Figure 4.13 Composite barycentric map for different types of barycentric coordinates for 100 uniform steps.

# 4.5 PRACTICAL CONSIDERATIONS

Composite barycentric mappings depend on two main choices: the underlying barycentric coordinates \(\phi\) and the vertex paths \(\psi\). In this section we illustrate the influence of these choices on the composite mapping.

# 4.5.1 Choosing the coordinates

In general, the vertex paths \(\psi_i\) produce an arbitrary intermediate shape, which may be concave or weakly convex. For this reason we need barycentric coordinates that are well-defined for arbitrary simple polygons. We suggest using mean value (see Section 1.2.3), harmonic (see Section 1.2.8), or maximum entropy coordinates (see Section 2.2.9). Figure 4.13 shows an example of a composite barycentric mapping for these three different coordinates.

# 4.5.2 Choosing the vertex paths

To create intermediate shapes, the natural vertex path that works in any dimension and for any shape is to linearly interpolate the shapes from source to target. However, this interpolation is not invariant with respect to similarity transformations, while the mapping is. Moreover, linear interpolation of the vertices is more likely to produce self-intersecting polygons in the case of rotations, which invalidates the mapping, since barycentric coordinates are well-defined only for non-self-intersecting polygons. For these reasons, linear interpolation is not well-suited for creating the intermediate shapes for the composite barycentric mappings.

Instead, the intermediate polygons can be computed by linearly interpolating the turning angle and the edge lengths [352], which generates more natural results than linearly interpolating the vertices, because edges and angles are invariant with respect to similarity transformations. Figure 4.14 shows how the composite barycentric mapping changes when this method is used instead of linearly interpolating the