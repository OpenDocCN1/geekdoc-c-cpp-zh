# Chapter 7: Transforming Objects, Pivoting, Aligning, and Snapping

To use AutoGrid, click the AutoGrid option after selecting an object type to create. If no objects are in the scene, then the object is created as usual. If an object is in the scene, the cursor moves around on the surface of the object with its coordinate axes perpendicular to the surface that the cursor is over. Clicking and dragging creates the new object based on the precise location of the object under the mouse.

The AutoGrid option stays active for all new objects that you create until you turn it off by unchecking the box.

**Tip**
Holding down the Alt key before creating the object makes the new construction grid visible, disables the AutoGrid option, and causes all new objects to use the new active construction grid. You can disable this active construction grid by enabling the AutoGrid option again.

# Tutorial: Creating a spyglass

As you begin to build objects for an existing scene, you find that working away from the scene origin is much easier if you enable the AutoGrid feature for the new objects you create. This feature enables you to position the new objects on (or close to) the surfaces of the nearby objects. It works best with objects that have pivot points located at their edges, such as Box and Cylinder objects.

In this example, you quickly create a spyglass object using the AutoGrid without needing to perform additional moves.

To create a spyglass using the AutoGrid and Snap features, follow these steps:

+   1. Before starting, click the Left viewport and zoom way out so you can see the height of the spyglass pieces.
+   2. Select Create > Standard Primitives > Cylinder, and drag from the origin in the Top viewport to create a Cylinder object. Set the Radius value to 40 and the Height value to 200. Then enable the AutoGrid option in the Object Type rollout.
+   3. Drag from the origin again in the Top viewport to create another Cylinder object. Set its Radius to 35 and its Height to 200. Repeat this step three times, reducing the Radius by 5 each time.

Figure 7.17 shows the resulting spyglass object.

# Using Snap Options

Often, when an object is being transformed, you know exactly where you want to put it. The Snap feature can be the means whereby objects get to the precise place they should be. For example, if you are constructing a set of stairs from box primitives, you can enable the Edge Snap feature to make each adjacent step align precisely along the edge of the previous step. With the Snap feature enabled, an object automatically moves (or snaps) to the specified snap position when you place it close enough. If you enable the Snap features, they affect any transformations that you make in a scene.

Snap points are defined in the Grid and Snap Settings dialog box that you can open by choosing Tools > Grid and Snaps > Grid and Snap Settings or by right-clicking any of the first three Snap buttons on the main toolbar. (These Snap buttons have a small magnet icon in them.) Figure 7.18 shows the Snaps panel of the Grid and Snap Settings dialog box for Standard and NURBS objects. NURBS stands for Non-Uniform Rational B-Splines. They are a special type of object created from spline curves.

**Cross-Ref**
In addition to the snap points for standard objects, the Snaps panel also includes a list of snap points for NURBS objects. For more information on NURBS, see Bonus Chapter 3 on the DVD, “Working with NURBS.”