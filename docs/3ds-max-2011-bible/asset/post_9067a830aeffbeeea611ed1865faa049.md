
## Chapter 27: Working with Compound Objects

### Filling object holes

If multiple holes exist between the objects, the Connect object attempts to patch them all. You can also use the button several times to connect a single object to multiple objects.

### Caution

**The Connect object doesn’t work well with NURBS (Non-Uniform Rational B-Splines) objects.**

The Parameters rollout includes a list of all the operands or objects involved in the connection. You can delete any of these with the Delete Operand button. The Extract Operand button lets you separate the Operand object from the Connect object.

In the Interpolation section, the Segments value is the number of segments used to create the bridge section, and the Tension value is the amount of curvature to use in an attempt to smooth the connected bridge.

The Bridge Smoothing option smoothes the faces of the bridge, and the Ends option smoothes where the bridge and the original objects connect.

### Tutorial: Creating a park bench

The Connect object is best used between two symmetrical copies of an object that need to be attached, as with a table or bridge. For this tutorial, you use the Connect object to create a park bench between two end pieces.

### Note

**Although the Connect compound object works fine, it requires that both holes have the same number of vertices. A more robust solution is the Editable Poly’s Bridge feature.**

- To connect two ends of a park bench, follow these steps:
- 
- 1. Open the Park bench.max file from the Chap 27 directory on the DVD.  
   This file includes symmetrical ends of the park bench. One end was created by extruding a spline shape and using the ShapeMerge tool to cut matching holes on the inner-facing surfaces. The Mirror tool was then used to create and rotate the symmetrical clone.
- 2. Select one end of the park bench, and select the Create → Compound → Connect menu command.
- 3. In the Pick Operand rollout, click the Pick Operand button, select the Move option, and click on the opposite side of the park bench.  
   The two end pieces connect.
- 4. In the Parameters rollout, select the Smoothing: Bridge option to smooth the seat of the bench.

Figure 27.15 shows the resulting park bench.

## Part VI: Advanced Modeling

### FIGURE 27.15

A Connect compound object can join two open holes in separate objects.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_777_0.png)

### Creating a Loft Object

Lofting is a term that comes from the shipbuilding industry. It describes a method for building ships that creates and positions the cross sections and then attaches a surface or skin along the length of the cross sections.

To create a Loft object, you need to have at least two spline shapes: one shape that defines the path of the Loft and another shape that defines its cross section. After the shapes are created, select the Create ◇ Compound menu command. A Loft button is enabled if two or more splines are present in the viewport.

### Tip

**Be aware of the orientation of the cross-section shape and the loft path before the loft is applied.** The cross section’s local Z-axis is always aligned with the path’s local Y-axis. By making the correct orientations before applying the loft, you can save some headache. If the orientations aren’t correct, you can edit the pivot on either object.

### Using the Get Shape and Get Path buttons

After you click the Loft button, the Creation Method rollout displays the Get Path and Get Shape buttons, which you use to specify which spline is the path and which spline is the cross section. Select a spline, and then click either the Get Path button or the Get Shape button. If you click the Get Shape button, the selected spline is the path, and the next spline shape you select is the cross section. If you click the Get Path button, the selected spline is the shape, and the next spline shape you select is the path.

### Note

After you click the Get Path or Get Shape button, although the cursor changes when you're over a valid spline, not all spline shapes can be used to create Loft objects. For example, you cannot use a spline created with the Donut button as a path.

When creating a Loft object with the Get Shape and Get Path buttons, you can specify either to Move the spline shape or to create a Copy or an Instance of it. The Move option replaces both splines with a Loft object. The Copy option leaves both splines in the viewport and creates a new Loft object. The Instance option maintains a link between the spline and the Loft object. This link enables you to modify the original spline. The Loft object is updated automatically.

The vertex order of the path spline is important. The Loft object is created starting at the vertex numbered 1.

### Note

You can tell which vertex is the first by enabling Vertex Numbering in the Selection rollout of an editable spline. The first vertex is also identified with a yellow box.

### Controlling surface parameters

All Loft objects include the Surface Parameters rollout. Using this rollout, you can set the smoothing of the Loft object with two different options: Smooth Length and Smooth Width. You can use the Mapping options to control the mapping of textures by setting values for the number of times the map repeats over the Length or Width of the Loft. The Normalize option applies the map to the surface evenly or proportionally according to the shape's vertex spacing. You can set the Loft object to automatically generate Material and Shape IDs, and you can specify the output of the Loft to be either a Patch or Mesh.

### Changing path parameters

The Path Parameters rollout, shown in Figure 27.16, lets you position several different cross-sectional shapes at different positions along the Loft path. The Path value indicates either the Distance or Percentage along the path where this new shape should be located. The Snap option, if turned on, enables you to snap to consistent distances along the path. The Path Steps option enables you to place new shapes at steps along the path where the vertices are located. Each path will have a different number of steps, depending on its complexity.

The viewport displays a small yellow X at the location where the new cross-sectional shape will be inserted. At the bottom of the rollout are three buttons, which are illustrated and described in Table 27.1.

## Part VI: Advanced Modeling

### FIGURE 27.16

The Loft compound object rollouts

![](img/ebbb4844f027f7d1c580e48108d2b6cb_779_0.png)

### TABLE 27.1

### Path Rollout Buttons

| Toolbar Button | Name | Description |
|---|---|---|
| Pick Shape | Selects a new cross-section spline to be inserted at the specified location |
| Previous Shape | Moves to the previous cross-section shape along the Loft path |
| Next Shape | Moves to the next cross-section shape along the Loft path |

### Setting skin parameters

The Skin Parameters rollout includes many options for determining the complexity of the Loft skin. You can specify whether to cap either end of the Loft using the Cap Start and/or Cap End options. The caps can be either Morph or Grid type.

This rollout also includes the following options for controlling the look of the skin:

- - Shape and Path Steps: Sets the number of segments that appear in each spline's cross-sectional shape and between each division along the path. The straight segments are ignored if the Optimize Path option is selected.
- - Optimize Shapes and Paths: Reduces the Loft's complexity by deleting any unneeded edges or vertices.
- - Adaptive Path Steps: Automatically determines the number of steps to use for the path in order to maintain a smooth curve.

## Chapter 27: Working with Compound Objects

- - **Contour:** Determines how the cross-sectional shapes line up with the path. If this option is enabled, the cross section is aligned to be perpendicular to the path at all times. If disabled, this option causes the cross-sectional shapes to maintain their orientation as the path is traversed.
- - **Banking:** Causes the cross-section shape to rotate as the path bends.
- - **Constant Cross-Section:** Scales the cross-sectional shapes in order to maintain a uniform width along the path. Turning off this option causes the cross sections to pinch at any sharp angles along the path.
- - **Linear Interpolation:** Causes straight linear edges to appear between different cross-sectional shapes. Turning off this option causes smooth curves to connect various shapes.
- - **Flip Normals:** Used to correct difficulties that would appear with the normals. Often the normals are flipped accidentally when the Loft is created.
- - **Quad Sides:** Creates four-sided polygons to connect to adjacent cross-section shapes with the same number of sides.
- - **Transform Degrade:** Makes the Loft skin disappear when subobjects are transformed. This feature can help you better visualize the cross-sectional area while it is being moved.

The Display options at the bottom of the Skin Parameters rollout give you the choice of displaying the skin in all viewports or displaying the Loft skin only in the viewports with shading turned on.

### Tutorial: Designing a slip-proof hanger

As an example of creating a Loft object with different cross-sectional shapes, you'll design a new hanger that includes some rough edges along its bottom section to keep slops from sliding off.

To design a hanger Loft object with different cross sections, follow these steps:

- 1. Open the Lofted slip-proof hanger.max file from the Chap 27 directory on the DVD. This file includes a spline outline of a hanger and two simple shapes.
- 2. Select the hanger spline, and choose the Create > Compound > Loft menu command.
- 3. In the Creation Method rollout, click the Get Shape button and then click the small circle shape (make sure that the Copy option is selected). This lofts the entire hanger with a circular cross section.
- 4. In the Path Parameters rollout, select the Path Steps option. A dialog box appears warning that this may change the relocate shapes. Click Yes to continue. Increment the Path value until the yellow X marker in the viewport is positioned at the beginning of the hanger’s bottom bar (at Step 53 for this tutorial). Click the Get Shape button again, and click the small circular shape again. This extends the circular cross section from the start at Step 0 to Step 53.
- 5. Increment the Path value by 1 to Step 54, click the Get Shape button, and select the star shape. This makes the remainder of the hanger use a star-shaped cross section. Increment the Path value again to the end of the hanger’s bottom bar (at Step 60), click the Get Shape button, and select the star shape again to end the star cross section.
- 6. In the Path Parameters rollout, increment the Path value a final time to Step 61, click the Get Shape button, and click the circular shape. Click the Pick Shape icon button at the bottom of the Path Parameters dialog box to change the cross section of the hanger to the end of the path. Right-click in the viewport to exit Get Shape mode.

> **Note**
> 
> If you forget to start and end a section with the same cross section, the loft blends between the two different cross sections.
