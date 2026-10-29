# Chapter 31: Painting in the Viewpoint Canvas and Rendering Surface Maps

Max can use the Render Surface Map feature to render several types of surface maps including:

+   - **Cavity map:** The Cavity map creates a grayscale map that highlights convex areas in white and concave areas in black. The Contrast value defines the difference between black and white values.
+   - **Density map:** The Density map option creates a map that shows the areas where the vertices are closest together as white and farther apart as black.
+   - **Dust map:** The Dust map option creates a grayscale map that identifies the areas that face upward as white and the underneath areas as black, as if the dust were to settle from above and land on all the white areas.
+   - **SubSurface map:** The SubSurface map is used to identify those areas of the mesh that are thickest as black and the thinnest areas of the mesh as white. This map type is used to show how likely light would pass through a given area. The Blur value is used to blur those areas between black and white.
+   - **Selection to Bitmap:** This map is used to identify a specific subobject selection. Each selected vertex is displayed as a white dot.
+   - **Texture Wrap:** The Texture Wrap feature lets you load in a texture that is wrapped about the object in a way to eliminate all seams. This texture could be a simple skin or hide texture. The Tile value is the number of times the texture is repeated end to end to cover the surface.
+   - **Bitmap Select:** This feature allows you to select specific subobject selections based on the color of the applied bitmap. For example, if you load a bitmap with white lines running through it, all polygon faces that touch those lines are selected.

To access the Render Surface Map panel, shown in Figure 31.14, select the Rendering→Render Surface Map. This feature works only on Editable Poly objects that have mapping coordinates. If any of these conditions are missing, a warning dialog box appears when you click one of the mapping buttons.

# FIGURE 31.14

The Render Surface Map panel can create several different types of maps.

![](bbox=[0.02, 0.83, 0.18, 0.96])