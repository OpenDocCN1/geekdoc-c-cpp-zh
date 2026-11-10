point in space, where the vector is the distance and direction from the origin to that point. In Figure 3.6, vector V (shown in red) can be specified either as the difference between points P1 and P2 or as an equivalent distance from the origin to P3. In all of our applications, we specify V as simply (x,y,z), the same notation used to specify the point P3.

![](bbox=[0.309, 0.257, 0.691, 0.476])

It is convenient to represent a vector the same way as a point, because we can use our matrix transforms on points or vectors interchangeably. However, it also can be confusing. For this reason we sometimes will notate a vector with a small arrow above it (such as V⃗). Many graphics systems do not distinguish between a point and a vector at all, such as in GLSL and JOML, which provide data types vec3/vec4 and classes Vector3f/Vector4f (respectively) that can hold either points or vectors. Some systems (such as the graphicslib3D library used in a previous edition of this book) have separate point and vector classes, and enforce appropriate use of one or the other depending on the operation being done. It is an open debate as to whether it is clearer to use one data type for both or separate data types.

There are several vector operations that are used frequently in 3D graphics, for which there are functions available in JOML and GLSL. For example, assuming vectors A(u,v,w) and B(x,y,z):

# Addition and Subtraction:

+   A ± B = (u ± x, v ± y, w ± z)  
+   JOML: Vector3f.add(Vector3f) and Vector3f.sub(Vector3f)  
+   GLSL: vec3 ± vec3