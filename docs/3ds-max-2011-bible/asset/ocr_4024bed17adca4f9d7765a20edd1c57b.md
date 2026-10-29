# Chapter 13: Modeling with Polygons and Patches

+   5. For the base cross sections, right-click the ellipse shape and select **Convert to Editable Spline** from the pop-up quadmenu. Then enable Vertex subobject mode, click the Refine button in the Geometry rollout, and click the lower-left and lower-right corners of the ellipse to add two new vertices to the shape. Select and right-click these new vertices, and change their vertex type to Bézier Corner to make the bottom of their cross-section shapes flat.

+   6. Select the first cross-section shape at the swan’s nose, and convert it to an Editable Spline. Then click the Attach button, and select each cloned cross-section shape in order from the nose to the tail. This makes all the shapes part of the same Editable Spline object.

+   7. Choose **Modifiers > Patch/Spline Editing > CrossSection** to apply the CrossSection modifier to the Editable Spline object. Then choose **Modifiers > Patch/Spline Editing > Surface** to apply the Surface modifier. Next, you may need to enable the Flip Normals option to see the final swan model. This command creates a surface that covers the spline framework. The surface created is a patch object.

# Note

You may not need to enable the Flip Normals option depending on how you created your initial splines. ■

Figure 13.46 shows the completed swan model. Using the surface tools to create patch objects results in objects that are easy to modify. You can change any patch subobject by applying the Edit Patch modifier and using the rollouts in the Modify panel.

Another way to create this swan model is to use the CrossSection feature for the Editable Spline and then apply the Edit Patch modifier to create the finished surface. This method is cleaner and involves fewer modifiers.

# FIGURE 13.46

The brass swan was created using the CrossSection and Surface modifiers.

![](bbox=[0.011, 0.56, 0.731, 0.971])