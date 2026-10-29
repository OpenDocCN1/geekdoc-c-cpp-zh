# Chapter 26: Deforming Surfaces and Using the Mesh Modifiers

4. In the TurboSmooth rollout, set the Iterations value to 2.
Notice that the entire birdbath is smooth and the resolution is greatly increased, as shown in Figure 26.14.

# FIGURE 26.14

The TurboSmooth modifier can make a model flow better.

![](bbox=[0.02, 0.28, 0.95, 0.72])

# HSDS modifier

You use the HSDS (Hierarchical SubDivision Surfaces) modifier to increase the resolution and smoothing of a localized area. It works like the Tessellate modifier, except that it can work with small subobject sections instead of the entire object surface. The HSDS modifier lets you work with Vertex, Edge, Polygon, and Element subobjects. After a subobject area is selected, you can click the Subdivide button to subdivide the area. Each time you press the Subdivide button, the selected subobjects are subdivided again, and each subdivision level appears in the list above the Subdivide button.

Using the subdivision list, you can move back and forth between the various subdivision hierarchy levels. When edges are selected, you can specify a Crease value to maintain sharp edges. In the Advanced Options rollout, you can select to Smooth Result, Hide, or Delete Polygon. The Adaptive Subdivision button opens the Adaptive Subdivision dialog box, in which you can specify the detail parameters. This modifier also includes a Soft Selection rollout.