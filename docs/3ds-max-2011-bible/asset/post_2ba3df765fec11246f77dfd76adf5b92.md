
## FIGURE 13.35

The Selection rollout includes icon buttons for selecting the various subobject modes.

Edge subobject mode

Handle subobject mode

Patch subobject mode

Vertex subobject mode

Element subobject mode

![](img/ebbb4844f027f7d1c580e48108d2b6cb_430_0.png)

The By Vertex option is available in all but the Vertex subobject mode. It requires that you click a vertex in order to select an Edge, Face, Polygon, or Element. It selects all edges and faces that are connected to a vertex when the vertex is selected. This is handy because selecting a vertex is often easier than selecting numerous faces or edges.

The Ignore Backfacing option selects only those subobjects with normals pointing toward the current viewport. This option is helpful if many subobjects are on top of one another in the viewport. For example, if a sphere object were converted into an Editable Patch, you could enable the Ignore Backfacing option, and then selecting subobjects on the front of the sphere would not select the subobjects on the back of the sphere at the same time.

The Shrink and Grow buttons decrease or increase the selected subobjects by adding or deleting all adjacent subobjects to the current selection. The Ring and Loop buttons are available only in Edge subobject mode. Ring selects all edges that are parallel to the current edge, and Loop selects all other edges that have the same alignment as the current edge.

The Select Open Edges option is active only in Edge subobject mode. This button lets you select all the edges in the patch that are connected only to one face. This provides an easy way to quickly locate all the holes in your current model.

At the bottom of the Selection rollout is some information on the current selection. This lists the current subobject type and number selected.

## Part III: Modeling Basics

## Cross-Ref

The Soft Selection rollout allows you to alter (to a lesser extent) adjacent nonselected subobjects when selected subobjects are moved, creating a smooth transition. Check out the details of this rollout in Chapter 10, “Accessing Subobjects and Using Modeling Helpers.”

## Working with patch Geometry

Much of the power of editing patches is contained within the Geometry rollout, shown in Figure 13.36. You can use this rollout to attach new patches, weld and delete vertices, and bind and hide elements. Some Geometry rollout buttons may be disabled in the various subobject modes but are enabled in one of the other subobject editing modes.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_431_0.png)

The Geometry rollout (shown in two parts) includes controls for editing patches.

## Attach

The Attach button is available in all subobject modes, even when you’re not in subobject mode. You use it to add objects to the current Editable Patch object, such as primitives, mesh objects, and other patch objects. Be aware that you cannot attach a spline. Objects that are attached to an Editable Patch also become Editable Patches. Most Editable Patch features work only if all the involved patch pieces are attached as part of the same patch object.

To use this feature, select an object, click the Attach button, and move the mouse over the object to attach. The cursor changes over acceptable objects. Click the object to be attached. Click the Attach button again or right-click in the viewport to exit Attach mode. The Reorient option aligns the attached object’s Local Coordinate System with the Local Coordinate System of the patch to which it is being attached.

## Caution

Converting mesh objects to patch objects results in objects with many vertices.

## FIGURE 13.38

Moving the Vertex handles alters the adjacent faces.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_433_0.png)

You can switch between these two vertex types by right-clicking a vertex while in vertex subobject mode and selecting the desired type from the pop-up quadmenu.

## Note

Holding down the Shift key while clicking and dragging on a handle unlocks the handles and automatically changes the vertex type to Corner.

## Bind and Unbind

You can use the Bind button to connect edge vertices of one patch to an edge of another patch, which is useful for connecting edges with a different number of vertices. Be aware that the two patches must be part of the same object (you can make them part of the same object using the Attach button) and that the corner vertices must be welded together first. If you try to bind a vertex before welding the corner vertices, the Bind action won’t work. To use the Bind feature, click the Bind button and then drag a line from a vertex to the edge where it should join.

The Bind button attaches vertices to edges; to attach vertices to vertices, use one of the Weld buttons. When you bind vertices, the point of contact between the two patches is seamless and the vertex becomes part of the interior. To exit Bind mode, click the Bind button again or right-click in a viewport.

You use the Unbind button to detach vertices that have been connected using the Bind button.

## Create

You can use the Create button in the Vertex subobject mode to create patch vertices by clicking in the viewport. Use the Create button in Patch or Element subobject mode to connect the created vertices into three-sided or four-sided patches. Right-click in the viewport or click again on the Create button to exit Create mode.

The order in which you click the vertices determines the direction of the normal vector, which determines the visibility of the patch in the viewports (unless the Force 2-Sided display option is enabled). If you click the vertices in a clockwise direction, then the normal vector points away from the current viewport. The counterclockwise order points the normal vector out toward the user (which makes it visible).

## Tip

An easy way to determine the direction of the normal vector is to curl the fingers on your right hand in the direction that the vertices were clicked. Your thumb points toward the direction of the normal vector. This is called the right-hand rule.

## Chapter 13: Modeling with Polygons and Patches

## Delete

The Delete button (or pressing the Delete key) deletes the selected vertices. This button works for all the subobject types.

## Note

Deleting a vertex also deletes all faces and edges connected to that vertex. For example, deleting a single (top) vertex from a sphere that has been converted to an Editable Patch object leaves only a hemisphere.

## Break

Click the Break button to create a separate vertex for adjoining faces that are connected by a single vertex.

Patches are all connected by vertices: Moving one vertex changes the position of all adjoining patches. The Break button enables you to move the vertex associated with each patch independent of the others. The button is available only in Vertex subobject mode.

## Hide and Unhide All

The Hide and Unhide All buttons hide and unhide selected vertices. They can be used in any subobject mode. To hide a subobject, select the subobject and click the Hide button. To unhide the hidden subobjects, click the Unhide All button. Clicking the Unhide All button makes all subobjects, regardless of type, visible.

## Weld Selected and Weld Target

The Weld button enables you to weld two or more vertices into one vertex. To use this feature, move the vertices close to one another, drag an outline over them to select them, and then click the Weld button. You can tell whether the weld was successful by looking at the number of vertices selected at the bottom of the Selection rollout. If the weld was unsuccessful, increase the Weld threshold specified by the spinner and try again.

The Weld Target button lets you select a vertex and drag and drop it on top of another vertex. If the target vertex is within the number of pixels specified by the spinner, the vertices are welded into one vertex. To exit Weld Target mode, click the Target button again or right-click in the viewport.

Figure 13.39 shows two inverted sloping patches that have been combined. The resolution of the patch on the right is twice that of the patch on the left. The Bind button was used to attach the center vertex to the edge of the other patch. Notice that the seam between the two patches is smooth.

## Copy and Paste Tangents

Getting the handle positions between vertices just right can be tricky, but after you get it right, the Copy and Paste buttons in the Tangent section let you copy the handle orientation between vertices. The Paste Length option enables you to paste the length of the handle as well.

## Vertex surface properties

In Vertex subobject mode, the Surface Properties rollout that appears lets you color the object by assigning colors to its vertices. For each vertex, you also can specify an Illumination color and an Alpha value, which sets the transparency. You also can specify vertex colors in Patch and Element subobject modes.

## Cross-Ref

You can find more information on vertex colors in Chapter 33, “Creating Baked Textures and Normal Maps.”
