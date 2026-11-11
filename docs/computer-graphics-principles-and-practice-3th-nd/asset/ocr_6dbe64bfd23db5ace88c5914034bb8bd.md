+   - 8.3.1 Manifold Meshes .............................................................. 193
+   - 8.3.2 Nonmanifold Meshes ........................................................... 195
+   - 8.3.3 Memory Requirements for Mesh Structures .............................. 196
+   - 8.3.4 A Few Mesh Operations ........................................................ 197
+   - 8.3.5 Edge Collapse .................................................................... 197
+   - 8.3.6 Edge Swap ......................................................................... 197
+   - 8.4 Discussion and Further Reading ............................................... 198
+   - 8.5 Exercises ................................................................................. 198

# 9 Functions on Meshes ................................................................. 201

A real-valued function defined at the vertices of a mesh can be extended linearly across each face by barycentric interpolation to define a function on the entire mesh. Such extensions are used in texture mapping, for instance. By considering what happens when a single vertex value is 1, and all others are 0, we see that all our piecewise-linear extensions are combinations of certain basic piecewise-linear mesh functions; replacing these basis functions with other, smoother functions can lead to smoother interpolation of values.

+   - 9.1 Introduction ........................................................................... 201
+   - 9.2 Code for Barycentric Interpolation ............................................. 203
+     - 9.2.1 A Different View of Linear Interpolation ............................... 207
+     - 9.2.2 Scanline Interpolation .......................................................... 208
+   - 9.3 Limitations of Piecewise Linear Extension .................................. 210
+     - 9.3.1 Dependence on Mesh Structure ........................................... 211
+   - 9.4 Smoother Extensions ................................................................. 211
+     - 9.4.1 Nonconvex Spaces ................................................................. 211
+     - 9.4.2 Which Interpolation Method Should I Really Use? .................. 213
+   - 9.5 Functions Multiply Defined at Vertices ....................................... 213
+   - 9.6 Application: Texture Mapping .................................................... 214
+     - 9.6.1 Assignment of Texture Coordinates ....................................... 215
+     - 9.6.2 Details of Texture Mapping .................................................. 216
+     - 9.6.3 Texture-Mapping Problems ................................................... 216
+   - 9.7 Discussion ................................................................................ 217
+   - 9.8 Exercises ................................................................................. 217

# 10 Transformations in Two Dimensions ........................................... 221

Linear and affine transformations are the building blocks of graphics. They occur in modeling, in rendering, in animation, and in just about every other context imaginable. They are the natural tools for transforming objects represented as meshes, because they preserve the mesh structure perfectly. We introduce linear and affine transformations in the plane, because most of the interesting phenomena are present there, the exception being the behavior of rotations in three dimensions, which we discuss in Chapter 11. We also discuss the relationship of transformations to matrices, the use of homogeneous coordinates, the uses of hierarchies of transformations in modeling, and the idea of coordinate “frames.”

+   - 10.1 Introduction ......................................................................... 221
+   - 10.2 Five Examples ........................................................................ 222