# Chapter 5: Creating and Editing Primitive Objects

In the Parameters rollout are several Geodesic Base Type options, including Tetra, Octa, and Icosa. The Tetra type is based on a four-sided tetrahedron, the Octa type is based on an eight-sided Octahedron, and the Icosa type is based on the 20-sided Icosahedron. Setting the Segment value to 1 produces each of these Hedra shapes. Each type aligns the triangle faces differently.

GeoSpheres also have the same Smooth, Hemisphere, and Base to Pivot options as the Sphere primitive. Selecting the Hemisphere option changes the GeoSphere into a hemisphere, but you have no additional options like Chop and Squash. GeoSphere primitives do not include an option to be sliced.

# Tutorial: Comparing Spheres and GeoSpheres

To prove that GeoSpheres are more efficient than Sphere objects, follow these steps:

+   1. Create a normal Sphere, and set its Segment value to 4.
+   2. Next to the Sphere object, create a GeoSphere object with a Tetra Base Type and the number of Segments set to 4.
+   3. Create another GeoSphere object with the Octa Base Type and 4 Segments.
+   4. Finally, create a GeoSphere with the Icosa Base Type and 4 Segments.

Figure 5.14 shows these spheres as a comparison. The normal sphere, shown to the left, looks like a diamond, but the GeoSpheres still resemble spheres. Notice that the Icosa type GeoSphere, shown on the right, produces the smoothest sphere.

![](bbox=[0.005, 0.503, 0.557, 0.603])

Even with a similar number of segments, GeoSpheres are much more spherical.

# Tube

The Tube primitive is useful any time you need a pipe object. You can also use it to create ring-shaped objects that have rectangular cross sections. Creating a Tube object is very similar to the Cylinder and Cone objects. Tube parameters include two radii for the inner and outer tube walls. Tubes also have the Smooth and Slice options.

# Pyramid

Pyramid primitives are constructed with a rectangular base and triangles at each edge that rise to meet at the top, just like the ones in Egypt, only easier to build. Two different creation methods are used to create the base rectangle. With the Base/Apex method, you create the base by dragging corner to corner, and with the Center method, you drag from the base center to a corner.

The Width and Depth parameters define the base dimensions, and the Height value determines how tall the pyramid is. You can also specify the number of segments for each dimension.