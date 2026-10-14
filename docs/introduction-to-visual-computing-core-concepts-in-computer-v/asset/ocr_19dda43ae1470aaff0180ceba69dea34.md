![](bbox=[0.18, 0.15, 0.82, 0.33])

Figure 14.11. This figure shows a complex shape being texture mapped using a spherical (top) and an orthogonal (bottom) mapping. The spherical mapping uses the normals (left) or rays going out from the center of the object to pick the texture coordinates.

![](bbox=[0.18, 0.44, 0.82, 0.6])

Figure 14.12. This figure shows orthogonal (left) and cylindrical (right) mapping on a vase and a cylindrical mapping (top) and a spherical mapping (bottom) on a teapot.

simpler shape that can be easily parametrized and for which texture coordinates can be assigned using the above method. Then we find a way to map vertices of the complex shape to the vertices of the simple shape and assign the texture coordinates to the corresponding vertex in the complex shape. Many methods can be designed to achieve this mapping from the complex to the simpler shape and we consider a few examples here.

The object can be enclosed in a simple geometry like a sphere (Figure 14.11). At any vertex of the complex shape, the normal can be extended and the texture coordinates at the point where this extended normal meets the enclosing simpler geometry can be used as the texture coordinates at the vertex. Or, a ray can be