Vector4f, respectively. In some cases (as we will see), JOML adds the fourth element (set to 1.0) to a Vector3f when needed to carry out a homogeneous operation.

# 3.3 MATRICES

A matrix is a rectangular array of values, and its elements are typically accessed by means of subscripts. The first subscript refers to the row number, and the second subscript refers to the column number, with the subscripts starting at 0. Most of the matrices that we will use for 3D graphics computations are of size 4x4, as shown in Figure 3.2.

![](bbox=[0.394, 0.357, 0.606, 0.471])

The GLSL language includes a data type called mat4 that can be used for storing 4x4 matrices. Similarly, JOML includes a class called Matrix4f for instantiating and storing 4x4 matrices.

The identity matrix contains all zeros, with ones along the diagonal:

![](bbox=[0.427, 0.611, 0.571, 0.693])

Any point or matrix multiplied by the identity matrix is unchanged. In JOML, the identity matrix is available through the function Matrix4f.identity().

The transpose of a matrix is computed by interchanging its rows and columns. For example:

![](bbox=[0.267, 0.827, 0.733, 0.919])