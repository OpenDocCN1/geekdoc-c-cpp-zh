# Chapter 13: Modeling with Polygons and Patches

You can select multiple subobjects at the same time by dragging an outline over them. You can also select multiple subobjects by holding down the Ctrl key while clicking them. The Ctrl key can also deselect selected subobjects while maintaining the rest of the selection. Holding down the Alt key removes any selected vertices from the current selection set.

With one of the transform buttons selected, hold down the Shift key while clicking and dragging on a subobject to clone it. During cloning the Clone Part of Mesh dialog box appears, enabling you to Clone to Object or Clone to Element. Using the Clone to Object option makes the selection an entirely new object, and you are able to give the new object a name. If the Clone to Element option is selected, the clone remains part of the existing object but is a new element within that object.

If you hold down the Ctrl key while choosing a different subobject mode, the current selection is maintained for the new subobject type. For example, if you select all the polygons in the top half of a model using the Polygon subobject mode and click the Vertex subobject mode while holding down the Ctrl key, all vertices in the top half of the model are selected. This works only for the applicable subobjects. If the selection of polygons doesn’t have any borders, then holding down the Ctrl key while clicking the Border subobject mode selects nothing.

You also can hold down the Shift key to select only those subobjects that lie on the borders of the current selection. For example, selecting all the polygons on the top half of a model using the Polygon subobject mode and clicking the Vertex subobject mode with the Shift key held down selects only those vertices that surround the selection and not the interior vertices.

# Subobject selection

The Selection rollout, shown in Figure 13.2, includes options for selecting subobjects. The By Vertex option is available in all but the Vertex subobject mode. It requires that you click a vertex in order to select an edge, border, polygon, or element. It selects all edges and borders that are connected to a vertex when the vertex is selected. The Ignore Backfacing option selects only those subobjects with normals pointing toward the current viewport. For example, if you are trying to select some faces on a sphere, only the faces on the side closest to you are selected. If this option is off, then faces on both sides of the sphere are selected. This option is helpful if many subobjects are on top of one another in the viewport.

# Tip

**The select commands in the Edit menu also work with subobjects. For example, in Vertex subobject mode, you can select Edit > Select All (or press Ctrl+A) to select all vertices.**

The By Angle option selects adjacent polygons that are within the specified threshold. The threshold value is defined as the angle between the normals of adjacent polygons. For example, if you have a terrain mesh with a smooth, flat lake area in its middle, you can select the entire lake area if you set the Planar Threshold to 0 and click the lake.

The Selection rollout also includes four buttons. These buttons include Shrink, Grow, Ring, and Loop. Use the Grow button to increase the current selection around the perimeter of the current selection, as shown in Figure 13.3. Click the Shrink button to do the opposite.

The Ring and Loop buttons are available only in Edge and Border subobject modes. Use Ring and Loop to select all adjacent subobjects horizontally and vertically around the entire object. Ring selection looks for parallel edges, and Loop selection looks for all edges around an object that are aligned the same as the initial selection. For example, if you select a single edge of a sphere, the Ring button selects all edges going around the sphere and the Loop button selects all edges in a line from the top to the bottom of the sphere.