# Part III: Modeling Basics

# FIGURE 13.45

The CrossSection modifier joins several cross-section splines into a network of splines ready for a surface.

![](bbox=[0.07, 0.22, 0.82, 0.6])

The object to the right in Figure 13.46 shows the spline structure with the Surface modifier applied.

# Tutorial: Modeling a brass swan

In Chapter 2 you added a background image of a brass swan to the viewports. In this tutorial, you use the CrossSection and Surface modifiers to create a swan based on these background images.

To create a brass swan, follow these steps:

+   1. Open the Brass swan.max file from the Chap 13 directory on the DVD.
+      This file includes the background images needed to create the swan model.

+   2. Select Create > Shapes > Ellipse, and drag in the Top viewport to create a simple ellipse that is roughly the shape of the swan's nose. Use the transform tools to move, rotate, and scale the ellipse to match the cross section of the background image.

+   3. Hold down the Shift key, and drag the ellipse shape to the base of the swan's nose to create a clone. Use the transform tools to align this clone to the background image in the Front and Left viewports.

# Note

Although background images have been loaded for the Top, Front, and Left viewports, you need only two viewports to align all the cross sections. In this example, the Top viewport is misaligned with the other two viewports.

+   4. Continue to create cloned copies of the ellipse shape, and match them to each changing cross section in the background images.