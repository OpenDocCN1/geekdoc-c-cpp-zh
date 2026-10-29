# Chapter 31: Painting in the Viewpoint Canvas and Rendering Surface Maps

# FIGURE 31.12

The Color Palette can display colors as a list or as swatches.

Copy

Delete Paste

New Color Picker

![](bbox=[0.02, 0.35, 0.22, 0.61])

The Paintbox also includes three subobject selection icons. These icons can be used to select certain Vertices, Faces, or Elements to be painted. This limits the painting to the selected subobjects only. You also can select to Ignore Backfacing and use Soft Selection.

The Blur brush button lets you blur colors across polygons using a brush that works just like the Paint and Erase brushes.

The Adjust Color dialog box lets you change all the painted colors applied to an object using HSV or RGB color sliders. The Preview option makes the color adjustment visible in the viewports if selected. Below the Adjust Color icon is the Blur Selected icon that blurs together all the vertex colors based on the designated Amount value.

Colors can be mixed between layers using the various blending modes. Clicking the New Layer button adds a new instance of the Vertex Paint modifier to the Modifier Stack; the Delete Layer button does the opposite. Click the Condense to a Single Layer button to merge all the consecutive Vertex Paint modifiers to a single instance using the selected blending mode.

# Tutorial: Marking heart tension

As an example of using the Vertex Paint modifier, imagine a doctor who has a 3D model of the human heart. While discussing the results of the latest test with a patient, the doctor can color parts of the heart model to illustrate the various points.

To color on a human heart using the Vertex Paint modifier, follow these steps:

+   1. Open the Vertex paint on the heart.max file from the Chap 31 directory on the DVD. This file includes a heart mesh created by Viewpoint Datalabs.

+   2. Select a portion of the heart model, and choose Modifiers→Mesh Editing→Vertex Paint to apply the Vertex Paint modifier.