detail in nearby objects. However, the further the patches are from the camera, the less likely there will even be enough pixels in the rasterization to warrant the number of vertices we are generating!

Changing the number of vertices in a patch based on the distance from the camera is a technique called *level of detail*, or *LOD*. Sellers et al. describe a way of controlling LOD in instanced tessellation [SW15], by modifying the control shader. Program 12.5 shows a simplified version of the approach by Sellers et al. The strategy is to use the patch's perceived size to determine the values of its tessellation levels. Since the tessellated grid for a patch will eventually be placed within the square defined by the four control points entering the control shader, we can use the locations of the control points relative to the camera to determine how many vertices should be generated for the patch. The steps are as follows:

+   1. Calculate the screen locations of the four control points by applying the MVP matrix to them.
+   2. Calculate the lengths of the sides of the square (i.e., the width and height) defined by the control points (in screen space). Note that even though the four control points form a square, these side lengths can differ because the perspective matrix has been applied.
+   3. Scale the lengths' values by a tunable constant, depending on the precision needed for the tessellation levels (based on the amount of detail in the height map).
+   4. Add 1 to the scaled length values, to avoid the possibility of specifying a tessellation level of 0 (which would result in no vertices being generated).
+   5. Set the tessellation levels to the corresponding calculated width and height values.

Recall that in our instanced example we are not creating just one grid, but 64×64 of them. So the five steps in the previous list are performed for each patch. Thus, the level of detail varies from patch to patch.

All of the changes are in the control shader and are shown in Program 12.5, with the generated output following in Figure 12.10. Note that the variable gl_InvocationID refers to which vertex in the patch is being processed (not which patch is being processed). Therefore, the LOD computation which tells the tessellator how many vertices to generate occurs during the processing of the 0th vertex in each patch.