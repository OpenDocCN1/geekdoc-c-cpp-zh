# Chapter 12: Drawing and Editing 2D Splines and Shapes

# FIGURE 12.36

The resulting drain pipe was created using the Sweep modifier.

![](bbox=[0.013, 0.154, 0.727, 0.557])

# Moving splines to 3D

Although splines can be rendered, the real benefit of splines in Max is to use them to create 3D objects and for animation paths. You can use splines in several ways as you model 3D objects, including Loft objects and modifiers. One way to use splines to make 3D objects is with modifiers.

# Note

As you build splines that will be used to create mesh objects, remember that the number of vertices in a spline determines the number of segments in the final mesh. For example, if you have a spline with 10 points that is extruded five times, then you'll end up with more than 50 polygons, but the same spline with 80 points would have more than 400 polygons.

# Cross-Ref

Using splines to create an animation path is covered in Chapter 21, “Understanding Animation and Keyframes,” and Loft objects are covered in Chapter 27, “Working with Compound Objects.” General information on working with modifiers is covered in Chapter 11, “Introducing Modifiers and Using the Modifier Stack.”

# Extruding splines

Because splines are drawn in a 2D plane, they already include two of the three dimensions. By adding a Height value to the shape, you can create a simple 3D object. The process of adding Height to a shape is called extruding.