
You use the Smoothing Groups option to assign a subobject to a unique smoothing group. To do this, select a subobject and click a Smoothing Groups number. The Select By SG button, like the Select By ID button, opens a dialog box where you can enter a Smoothing Groups number, and all subobjects with that number are selected. The Clear All button clears all Smoothing Groups number assignments, and the Auto Smooth button automatically assigns Smoothing Groups numbers based on the angle between faces as set by the value to the right of the Auto Smooth button.

The Properties panel also includes options for setting vertex Color, Illumination, and Alpha values.

## Using the Freeform Tools

The middle tab in the Graphite Modeling tools includes an assortment of Freeform tools for sculpting and modeling surfaces as if working with clay. These tools are divided into two panels—PolyDraw and Paint Deform, as shown in Figure 14.20.

### FIGURE 14.20

The Freeform tools let you model by sculpting.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_467_0.png)

## Using the PolyDraw tools

The various PolyDraw tools let you create and extend the surface subobjects using tools that work like a common drawing program.

### Drag

The Drag tool lets you move selected subobjects around by simply dragging them with the mouse. Clicking a subobject automatically selects it and lets you drag it to a new position. Holding down the Shift key or the Ctrl key lets you drag edges or polygons regardless of the subobject mode that is selected. Pressing Shift+Ctrl keys together lets you drag entire edge loops, and the Alt key lets you move the subobject in a direction that is perpendicular to the view axis, which is great for dragging subobjects off to the side of an object.

### Step Build

The Step Build tool lets you click to place new vertices on the surface of the object. The location of these new vertices depends on the current Grid, on the current object's Surface or within the Selection using the On selections located to the right of the Step Build button. If you select the On: Surface option, then you can use the Pick button to select the object whose surface you want to create vertices on. After freestanding vertices are created, you can hold down the Shift key and drag over these new vertices to create a polygon. The Ctrl key lets you remove polygons, and the Alt key lets you remove vertices. With these controls, you can quickly remove and rebuild polygons to create new shapes.

### Extend

The Extend tool works on border subobjects and lets you add new polygons to fill the hole by dragging on the border vertices. If you press and hold the Shift key while dragging an edge, you can pull the edge away to create a new polygon. Dragging with the Shift+Ctrl keys lets you drag two adjacent edges out. The Ctrl key and a click deletes the polygon, and dragging with the Alt key held down moves the polygon perpendicular to the view axis.

### Optimize

The Optimize tool quickly collapses subobjects. Click an edge with this tool to remove it and to combine its two end points into one. The Shift key is used to target weld two vertices into a single one, and the Alt key removes vertices. The Shift+Ctrl key combo can remove an entire edge loop at once.

### Tutorial: Opening a diamond

Ever wonder what was inside a diamond? This example uses some of the PolyDraw tools to open up a diamond. Maybe there is treasure inside!

To edit a diamond-shaped object, follow these steps:

- 1. Select Create↳ Standard Primitives↳ Sphere, and drag in the Top viewport to create a Sphere object. Set its Segments value to 6. Then right-click, and select Convert To↳ Editable Poly from the pop-up quadmenu.
- 2. Open the Graphite Modeling tools, click the Freeform tab, select the Step Build tool, press and hold the Ctrl key, and click the center polygon to delete the polygon. Then click within the center polygon to create four vertices in the shape of a square. Then press and hold the Shift key, and drag near these vertices to create a polygon.
- 3. Select the Drag tool, and drag the new vertices until they are aligned with each other to form a square.
- 4. Select the Extend tool, and with the Shift key pressed, drag the edge on the left side of the open polygon toward the middle to create a new extended polygon. Then repeat for the left side.

Figure 14.21 shows the resulting diamond.

### Draw On and Pick

The Draw On drop-down list gives you three options for specifying the object that is drawn on: Grid, Surface, and Selection. If Surface is selected, you can use the Pick button to choose the surface object. You also can set an Offset, which is the distance above the surface on which the drawn objects appear.

### Tip

It is best to keep a non-zero offset value when drawing on the surface of an object, especially if the drawn object overlaps an edge. This keeps the surfaces from interpenetrating.

### Shapes and Solve Surface

The Shapes tool lets you draw polygonal shapes directly on the surface of an object. Figure 14.22 shows three polygons drawn on the surface of a torus. You also can delete drawn polygons with the Ctrl key. The completed polygons likely will have multiple vertices, but you can reduce the polygons to tris and quads using the Solve Surface button.

### FIGURE 14.21

The PolyDraw tools let you work quickly to add, remove, and rebuild polygons.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_469_0.png)

### FIGURE 14.22

Using the Shapes tool, you can draw polygons that conform to the surface of the underlying object.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_469_1.png)

## Chapter 14: Using the Graphite Modeling Tools and Painting with Objects

### Splines

The Splines tool lets you draw spline objects that follow the surface of the underlying object. The Ctrl key can be used to delete drawn splines.

### Surface, Topology, Strips, and Branches

The Surface tool covers the object with a mesh of quads by painting over the object. You can delete any polygon by clicking it with Ctrl key held down. The Topology tool lets you draw a series of parallel lines followed by a set of perpendicular lines to form quads. The Auto Weld option automatically welds vertices together to form a mesh. The Ctrl key extends a line from the nearest end point.

The Strips tool draws a consecutive row of quads that flow across the surface of the object. The Shift key extends the strip from the nearest edge. The Branches tool extends a tapered branch from a single polygon. For the branches, you can set a Taper amount; the Minimum Distance value sets the distance between the segments. This is useful for creating tentacles, as shown in Figure 14.23.

### FIGURE 14.23

Using the Branches tool, you can drag out extending arms from polygons.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_470_0.png)

## Using the Paint Deform tools

The Paint Deform tools let you sculpt the surface of an object by pushing, pulling, and modeling the object in organic ways like it was clay. Whenever any of the tools on the Paint Deform panel are selected, its settings for the brush’s Size and Strength (and sometimes Offset, depending on the tool) appear in the Paint Options panel to the side of the Paint Deform panel.

### Shift

The Shift tool lets you drag all subobjects within the brush radius, and all subobjects within the falloff radius are moved to a lesser extent. You can control the brush size and falloff in the Options panel, or you can press and hold the Ctrl key and drag to alter the brush’s radius. The Shift+drag changes the brush’s falloff indicated by the inner white circle.

## Part III: Modeling Basics

### Push/Pull

The Push/Pull tool also has Size and Strength values, but it is different in that the brush follows the surface of the object. Dragging over an area pulls the vertices within the brush’s radius outward, and holding down the Ctrl key pushes the vertices inward. The Shift key relaxes the area under the brush.

### Relax/Soften

The Relax/Soften brush removes any extreme changes in the surface such as hard edges of a cube. The Alt key lets you relax the surface without changing its volume, and the Ctrl key causes the surface to revert to its previous state.

### Flatten and Pinch/Spread

The Flatten brush pulls and bends out of the mesh causing the object to be working into a flat plane. The Ctrl key causes the object to revert to its previous state, and the Shift key accesses the Relax/Soften brush. The Pinch/Spread tool causes vertices to be pulled in closer to each other, and holding down the Alt key has the opposite effect and pushes them away.

### Smudge, Noise, and Exaggerate

The Smudge tool pushes the surrounding vertices away from the center of the brush. Dragging over the same vertices multiple times moves them each time. Holding down the Alt key causes the vertices to be moved only along the surface and not to be moved along the normal. The Noise tool randomly moves the vertices about to create a random noise pattern. The Exaggerate tool pushes vertices farther in the current direction to emphasize the details.

### Revert

At any point, you can use the Revert tool to gradually change the object back to its last saved point. You can set a save point by clicking the Commit button, which looks like a green check mark. The Cancel button (a red X) removes the recent changes from the object.

## Using the Selection Tools

The next tab offers several additional Selection tools. These tools make it possible to locate specific subobjects by looking for certain criteria such as concavity, normals, and symmetry. Figure 14.24 shows the panels for this tab.

### Selecting Tops, Open, and Non-Quads

The first three tools in the Selection tab are the Tops, Open, and Non-Quads tools. The Tops tool selects all vertices resulting from the extruded sections. This quickly lets you grab all extended sections and extend or reduce them as needed. The Open tool selects all open borders, and the Non-Quads tool finds all polygons that consist of trios or more than four corners. This is a valuable tool when working with edge loops.

### Copying and pasting selections

The Stored Selection panel lets you copy a selection of subobjects into two available stores. These copied selections can be restored at any time by clicking the Paste button. Additional buttons let you combine the two selection stores, subtracting one from another and getting only the intersecting selection between the two. The Clear button removes the selection from the store.
