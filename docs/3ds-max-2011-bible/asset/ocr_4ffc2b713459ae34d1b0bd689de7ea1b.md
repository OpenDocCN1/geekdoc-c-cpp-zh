# Note

The name of this dialog box changes depending on the type of transformation taking place and the coordinate system. If the Select and Move button is selected along with the world coordinate system, the Transform Type-In dialog box is labeled Move Transform Type-In and the column titles indicate the coordinate system.

# Using the status bar Type-In fields

The status bar includes three fields labeled X, Y, and Z for displaying transformation coordinates. When you move, rotate, or scale an object, the X, Y, and Z offset values appear in these fields. The values depend on the type of transformation taking place. Translation shows the unit distances, rotation displays the angle in degrees, and scaling shows a percentage value of the original size.

When you click the Select Objects button, these fields show the absolute position of the cursor in world coordinates based on the active viewport.

You also can use these fields to enter values, as with the Transform Type-In dialog box. The type of transform depends on which transform button you select. The values that you enter can be either absolute coordinates or offset values, depending on the setting of the Transform Type-In toggle button that appears to the left of the transform fields. This toggle button lets you switch between Absolute and Offset modes, shown in Table 7.2.

# Tip

If you right-click any of these fields, a pop-up menu appears where you can cut, copy, or paste the current value.

# TABLE 7.2

# Absolute/Offset Buttons

| Button | Description |
| --- | --- |
|  | Absolute |
|  | Offset |

# Understanding the Transform Managers

To keep track of the position of every object in a scene, internally Max records the position of the object's vertices in reference to a Universal Coordinate System (UCS). This coordinate system defines vertex position using the X, Y, and Z coordinates from the scene's origin.

However, even though Max uses the UCS to internally keep track of all the points, this isn't always the easiest way to reference the position of an object. Imagine a train with several cars. For each individual train car, it is often easier to describe its position as an offset from the car in front of it.

The Transform Managers are three types of controls that help you define the system about which objects are transformed. These controls, found on the main toolbar and on the Axis Constraints toolbar, directly affect your transformations. They include the following: