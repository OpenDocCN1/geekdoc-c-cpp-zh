# Part III: Modeling Basics

# Sweep modifier

The Sweep modifier works just like the loft compound object, letting you follow a spline path with a defined cross section, except that the Sweep modifier is a modifier, making it easier to apply and remove from splines and shapes. Another benefit of the Sweep modifier is that it has several Built-In Sections available that you can choose or you can pick your own. The built-in sections include many that are useful for architectural structures including Angle, Bar, Channel, Cylinder, Half Round, Pipe, Quarter Round, Tee, Tube, and Wide Flange.

Using the Merge From File button, you can choose a shape from another file. You can also set the number of interpolation steps. The Sweep Parameters rollout includes options for mirroring, offsetting, smoothing, aligning, and banking the generated sweep. The Union Intersection option causes self-intersecting portions of the path to be combined using a union Boolean command. You also can select to have mapping coordinates generated on the sweep object.

# Tutorial: Plumbing with pipes

If you want to create a shape that renders in the scene, you can use the Renderable Spline option or you can apply the Sweep modifier. In this example, you apply the Sweep modifier to a line that defines the path of a bathroom sink drain.

To create a pipe that follows a spline, follow these steps:

+   1. Open the Bathroom sink.max file from the Chap 12 directory on the DVD.
+   
+      This file includes a simple bathroom sink and a line that defines its drain path.
+   
+   2. With the spline selected, choose the Modifiers ▸ Patch/Spline Editing ▸ Sweep menu command to apply the Sweep modifier.
+   
+   3. In the Section Type rollout, choose the Cylinder option from the Built-In Section drop-down list. Then set the Radius value to 10.

Figure 12.36 shows the resulting sink complete with a drain created using a cylinder cross section.

# Trim/Extend modifier

The Trim/Extend modifier lets you trim the extending end of a spline or extend a spline until it meets another spline at a vertex. The Pick Locations button turns on Pick mode, where the cursor changes when it is over a valid point. Operations include Auto, Trim Only, and Extend Only with an option to compute Infinite Boundaries. You can also set the Intersection Projection to View, Construction Plane, or None.

# Using the Shape Check utility

The Shape Check utility is helpful in verifying that a shape doesn’t intersect itself. Shapes that have this problem cannot be extruded, lofted, or lathed without problems. To use this utility, open the Utilities panel (the icon for the Utilities panel looks like a hammer) and click the More button. Select Shape Check from the Utilities dialog box list, and click OK.

# Note

**The Shape Check utility is found in the Utilities panel and not in the Modifiers menu.**

The Shape Check rollout includes only two buttons: Pick Object and Close. Click the Pick Object button, and click the shape you want to check. Any intersection points are displayed as red squares, as shown in Figure 12.37, and the response field displays “Shape Self-Intersects.” If the shape doesn’t have any intersections, then the response field reports “Shape OK.”

# Note

**You can use the Shape Check utility on normal splines and on NURBS splines.**