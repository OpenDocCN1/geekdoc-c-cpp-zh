# FIGURE 18.3

The Multi/Sub-Object material defines materials according to material IDs.

![](bbox=[0.03, 0.2, 0.65, 0.625])

# Cross-Ref

You can learn more about modeling with patches in Chapter 13, “Modeling with Polygons and Patches.”

To create a quilt using patches, follow these steps:

+   1. Open the Patch quilt.max file from the Chap 18 directory on the DVD.
+      This file contains a quilt made of patch objects that have been combined into one object.
+   2. Open the Material Editor by choosing Rendering→ Material Editor→ Slate Material Editor (or press M), and double-click on the Multi/Sub-Object material in the Material/Map Browser panel.
+      The Multi/Sub-Object material node loads into the Node View, and the Multi/Sub-Object Basic Parameters rollout displays in the Parameter Editor panel.
+   3. In the Multi/Sub-Object Basic Parameters rollout, click the color swatches to the right of the Material button to open the Color Selector. Select different colors for each of the first ten material ID slots.
+   4. Drag the Multi/Sub-Object material node’s output socket and drop it onto the patch object in the viewports. Close the Material Editor.
+   5. In the Modify panel, select the Patch subobject and scroll to the bottom of the Modify panel to the Surface Properties rollout.
+   6. Assign each patch a separate material ID by clicking a patch and changing the ID number in the rollout field.

Figure 18.4 shows the finished quilt. Because it’s a patch, you can drape it over objects easily.