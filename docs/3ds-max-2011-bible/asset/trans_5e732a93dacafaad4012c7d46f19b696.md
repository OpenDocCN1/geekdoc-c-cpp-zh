

## Part III: Modeling Basics

### FIGURE 13.5

A clown head created from an editable poly by selecting and moving vertices

![](img/ebbb4844f027f7d1c580e48108d2b6cb_403_0.png)

### FIGURE 13.6

The Edit Geometry rollout includes many general-purpose editing features.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_403_1.png)

Many of the buttons for the Editable Poly include a small icon to the right of the button that opens a settings caddy. These caddy interfaces appear around the selected subobject and allow you to change the settings and immediately see the results in the viewports. The OK button (a check mark icon) applies the settings and closes the dialog box, and the Apply button (a plus sign icon) applies the settings and leaves the dialog box open. These caddy interfaces are included next to the buttons such as Extrude, Bevel, Outline, and Inset.

Editable Poly objects include all their common buttons in the Edit Geometry rollout and all subobject-specific buttons is a separate rollout named after the subobject mode, such as Edit Vertices or Edit Edges.

### Repeat Last

The first button in the Edit Geometry rollout is the Repeat Last button. This button repeats the last subobject command. This button does not work on all features, but it’s very convenient for certain actions.

### Tip

The tooltip for this button displays the last repeatable command.

### Enabling constraints

The Constraints options limit the movement of subobjects to a specified subobject. The available constraints are None, Edge, Face, and Normal. For example, if you select and move a vertex with the Edge constraint enabled, then the movement is constrained to the adjacent edges.

### Tutorial: Creating a roof truss

When creating houses, modeling the roof can be tricky, but using an edge constraint makes it much easier.

To create a triangular roof truss, follow these steps:

- 1. Select Create Standard Primitives Box, and drag in the Top viewport to create a Box object centered over the Y-axis.
- 2. Right-click the box object and select Convert To Editable Poly in the pop-up quadmenu.
- 3. Open the Modify panel, and choose the Vertex subobject mode. In the Constraints drop-down list of the Edit Geometry panel, select the Edge option.
- 4. With the Select and Move tool, drag over the top-left corners and drag them to the Y-axis, then repeat for the top-right corners.

Notice that the points are constrained to the top edge as they are dragged. Moving both sets of points results in a simple perfect triangle.

### Tip

An even easier way to create such a triangle would be to use the Gengon primitive found among the Extended Primitives.

### Preserve UVs

UV coordinates define how a texture map is applied to an object’s surface. These UV coordinates are tied closely to the surface subobject positions, so moving a subobject after a texture is applied moves the texture also. This could cause discontinuities to the texture map. The Preserve UVs option lets you make subobject changes without altering the UV coordinates for an existing texture.

## Chapter 13: Modeling with Polygons and Patches

### Collapse

The Collapse button is used to collapse all the selected subobjects to a single subobject located at the averaged center of the selection. This button is similar to the Weld button, except that the selected vertices don’t need to be within a Threshold value to be combined. This button works in all subobject modes.

### Attach and Detach

The Attach button is available with all subobject modes, even when you are not in subobject mode. Use the Attach button to add objects to the current Editable Poly object. You can add primitives, splines, patch objects, and other mesh objects. Any object attached to a mesh object is automatically converted into an editable poly and inherits the object color of the object to which it is attached. Any objects added to a poly object can be selected individually using the Element subobject mode.

### Caution

**If you attach an object that is smoothed using NURMS, the NURMS are lost when the object is attached.**

To use this feature, select the main object and click the Attach button. Move the mouse over the object to be attached; the cursor changes over acceptable objects. Click the object to select it. Click the Attach button again or right-click in the viewport to exit Attach mode.

### Note

**If the object that you click to attach already has a material applied that is different from the current Editable Poly object, then a dialog box appears giving you options to Match Material IDs to Material, Match Material to Material IDs, or Do not Modify Material IDs or Material. Materials and Material IDs are discussed in more detail in Chapter 15, “Using the Slate Material Editor.”**

Clicking the Attach List button opens the Attach List dialog box (which looks just like the Select Objects (H) dialog box) where you can select from a list of all the objects to attach. The list contains only objects that you can attach.

### Note

**When you enter a subobject mode, the Attach List button changes to a Detach button for poly objects.**

Attaching objects is different from grouping objects because all attached objects act as a single object with the same object color, name, and transforms. You can access individual attached objects using the Element subobject mode.

Use the Detach button to separate the selected subobjects from the rest of the object. To use this button, select the subobject and click the Detach button. The Detach dialog box opens, enabling you to name the new detached subobject. You also have the options to Detach to Element or to Detach as Clone. All subobject modes except Edge have a Detach option. This button appears in place of the Attach List button in all subobject modes.

### Slicing and cutting options

The Slice Plane button lets you split the poly object along a plane. When you click the Slice Plane button, a yellow slice plane gizmo appears on the selected object. You can move, rotate, and scale this gizmo using the transform buttons. After you properly position the plane and set all options, click the Slice button to finish slicing the mesh. All intersected faces split in two, and new vertices and edges are added to the mesh where the Slice Plane intersects the original mesh.

## Part III: Modeling Basics

The Slice Plane mode stays active until you deselect the Slice Plane button or until you right-click in the viewport; this feature enables you to make several slices in one session. The Slice Plane button is enabled for all subobject modes. For the Editable Poly object, a Reset Plane button is located next to the Slice Plane button. Use this button to reset the slice plane to its original location. You use the Split option to double the number of vertices and edges along the Slice Plane, so each side can be separated from the other. When used in Element mode, the Split option breaks the sliced object into two separate elements.

The QuickSlice button lets you click anywhere on an Editable Poly object where you want a slicing line to be located. You can then move the mouse, and the QuickSlice line rotates about the point you clicked on. When you click the mouse again, a new vertex is added at every place where the QuickSlice line intersects an object edge. This is a very convenient tool for slicing objects because the slice line follows the surface of the object, so you can see exactly where the slice will take place.

For the QuickSlice and Cut tools, you can enable the Full Interactivity option (located near the bottom of the Edit Geometry rollout). With this option enabled, the slice lines are shown as you move the mouse about the surface. With Full Interactivity disabled, the resulting lines are shown only when the mouse is clicked.

For Editable Poly objects, the Cut button is interactive. If you click a polygon corner, the cut edge snaps to the corner, and a new edge extends from the corner to a nearby corner. As you move the mouse around, the edge moves until you click where the edge should end. If you click in the middle of an edge or face, then new edges appear to the nearest corner.

### Tutorial: Combining, cutting, and separating a car model

When dealing with a model that includes interior parts, you may want to slice the object and separate a portion to reveal the interior. Although this can be accomplished using a camera clipping plane, which is explained in Chapter 19, “Configuring and Aiming Cameras,” a more permanent solution uses the QuickSlice and Detach operations.

To combine, slice, and detach a car model, follow these steps:

- 1. Open the Sliced car.max file from the Chap 13 directory on the DVD.
- 2. Before you can slice the car, you'll need to combine the entire car into a single Editable Poly object. Select one of the body parts, right-click on it, and select the Convert To▸Editable Poly in the pop-up quadmenu.
- 3. Open the Modify panel, and click on the dialog box icon next to the Attach button in the Edit Geometry rollout.
- 4. In the Attach List dialog box that opens, click the Select All button (or use the Ctrl+A shortcut) and select the Attach button. In the Attach Options dialog box that appears, select the Match Material IDs to Material option, you can leave the Condense Materials and IDs option checked, and then click OK. All objects are now combined into a single Editable Poly object.
- 5. Click the QuickSlice button, which is also in the Edit Geometry rollout, and click in the Top viewport at the point where you want to slice the car. Then drag to align the slicing plane, and click again to make the slice. Click on the QuickSlice button again to exit QuickSlice mode.
- 6. Select the Polygon subobject mode, and drag over all the polygons below the slice line in the Top viewport. Then click the Detach button in the Edit Geometry rollout. In the Detach dialog box, enter the name Car Front and click OK.
- 7. Disable Polygon subobject mode, and use the Select and Move tool to separate the car front from the rest of the car.

Figure 13.8 shows the separated car front.

