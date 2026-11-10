# 6.2 OPENGL INDEXING—BUILDING A TORUS

# 6.2.1 The Torus

Algorithms for producing a *torus* can be found on various websites. Paul Baker gives a step-by-step description for defining a circular slice, and then rotating the slice around a circle to form a donut, in his OpenGL bump mapping tutorial [PP07]. Figure 6.11 shows two views—from the side and from above.

![](bbox=[0.181, 0.294, 0.817, 0.469])

**Figure 6.11**
Building a torus.

The way that the torus vertex positions are generated is rather different from what was done to build the sphere. For the torus, the algorithm positions a vertex to the right of the origin, and then rotates that vertex in a circle on the XY plane using a rotation around the Z axis to form a “ring.” The ring is then moved outward by the “inner radius” distance. Texture coordinates and normal vectors are computed for each of these vertices as they are built. An additional vector tangent to the surface of the torus (called the *tangent vector*) is also generated for each vertex.

Vertices for additional torus rings are formed by rotating the original ring around the Y axis. Tangent and normal vectors for each resulting vertex are computed by also rotating the tangent and normal vectors of the original ring around the Y axis. After the vertices are created, they are traversed from ring to ring, and for each vertex two triangles are generated. The generation of six index table entries comprising the two triangles is done in a similar manner as we did for the sphere.

Our strategy for choosing texture coordinates for the remaining rings will be to arrange them so that the S axis of the texture image wraps halfway around the horizontal perimeter of the torus, and then repeats for the other half. As we rotate around the Y axis generating the rings, we specify a variable ring that starts