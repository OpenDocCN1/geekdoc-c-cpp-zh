# Chapter 12: Drawing and Editing 2D Splines and Shapes

To create a custom bookshelf using spline Boolean operations, follow these steps:

+   1. Open the Bookshelf.max file from the Chap 12 directory on the DVD. This file includes a triangle shape drawn with the Line primitive that is overlapped by three circles. All these shapes have been converted and combined into a single Editable Spline object.
+   
+   2. Select the shape, open the Modify panel, and select the Spline subobject mode (or press the 3 key) and select the triangle shape.
+   
+   3. Select the Subtraction Boolean operation (the middle icon) in the Geometry rollout, and click the Boolean button. Then select each of the circles and right-click to exit Boolean mode. Then click Spline in the Modifier Stack again to exit subobject mode.
+   
+   4. Back in the Modify panel, select the Extrude modifier from the Modifier drop-down list and enter an Amount of 1000. Select Zoom Extents All to resize your viewports, switch to the Perspective viewport, and view your bookshelf.

Figure 12.39 shows the finished bookshelf in the Perspective viewport ready to hang on the wall.

![](bbox=[0.018, 0.431, 0.735, 0.831])

# Lathing splines

Another useful modifier for 2D splines is the Lathe. This modifier rotates the spline about an axis to create an object with a circular cross section (such as a baseball bat). In the Parameters rollout, you can specify the Degrees to rotate (a value of 360 makes a full rotation) and Cappings, which add ends to the resulting mesh. Additional options include Weld Core, which causes all vertices at the center of the lathe to be welded together, and Flip Normals, which realigns all the normals.