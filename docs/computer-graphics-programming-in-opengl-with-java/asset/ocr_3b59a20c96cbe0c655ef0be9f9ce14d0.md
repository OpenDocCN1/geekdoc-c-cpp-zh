# # 6.1 PROCEDURAL MODELS—BUILDING A SPHERE

Some types of objects, such as spheres, cones, and so forth, have mathematical definitions that lend themselves to algorithmic generation. Consider for example a circle of radius R; coordinates of points around its perimeter are well-defined (Figure 6.1).

![](bbox=[0.369, 0.252, 0.617, 0.371])

**Figure 6.1**  
Points on a circle.

We can systematically use our knowledge of the geometry of a circle to algorithmically build a sphere model. Our strategy is as follows:

+   1. Select a *precision* representing a number of circular regions the sphere is divided into. In the left side Figure 6.2, the sphere is sliced into four regions.
+   2. Subdivide the circumference of each circular slice into some number of points. See the right side of Figure 6.2. More points and horizontal slices produces a more accurate and smoother model of the sphere. In our model, *each slice will have the same number of points, including at the very top and bottom (where those points are coincident).*

![](bbox=[0.24, 0.714, 0.746, 0.869])

**Figure 6.2**  
Building vertices for a sphere.