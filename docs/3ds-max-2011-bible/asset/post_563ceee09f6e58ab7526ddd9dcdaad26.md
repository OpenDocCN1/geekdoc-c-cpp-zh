
# Note

The name of this dialog box changes depending on the type of transformation taking place and the coordinate system. If the Select and Move button is selected along with the world coordinate system, the Transform Type-In dialog box is labeled Move Transform Type-In and the column titles indicate the coordinate system.

## Using the status bar Type-In fields

The status bar includes three fields labeled X, Y, and Z for displaying transformation coordinates. When you move, rotate, or scale an object, the X, Y, and Z offset values appear in these fields. The values depend on the type of transformation taking place. Translation shows the unit distances, rotation displays the angle in degrees, and scaling shows a percentage value of the original size.

When you click the Select Objects button, these fields show the absolute position of the cursor in world coordinates based on the active viewport.

You also can use these fields to enter values, as with the Transform Type-In dialog box. The type of transform depends on which transform button you select. The values that you enter can be either absolute coordinates or offset values, depending on the setting of the Transform Type-In toggle button that appears to the left of the transform fields. This toggle button lets you switch between Absolute and Offset modes, shown in Table 7.2.

### Tip

If you right-click any of these fields, a pop-up menu appears where you can cut, copy, or paste the current value.

## TABLE 7.2

### Absolute/Offset Buttons

| Button | Description |
| --- | --- |
|  | Absolute |
|  | Offset |

## Understanding the Transform Managers

To keep track of the position of every object in a scene, internally Max records the position of the object's vertices in reference to a Universal Coordinate System (UCS). This coordinate system defines vertex position using the X, Y, and Z coordinates from the scene's origin.

However, even though Max uses the UCS to internally keep track of all the points, this isn't always the easiest way to reference the position of an object. Imagine a train with several cars. For each individual train car, it is often easier to describe its position as an offset from the car in front of it.

The Transform Managers are three types of controls that help you define the system about which objects are transformed. These controls, found on the main toolbar and on the Axis Constraints toolbar, directly affect your transformations. They include the following:

- Reference Coordinate System: Defines the coordinate system about which the transformations take place.
- Transform Center settings: The Pivot Point Center, the Selection Center, and the Transform Coordinate Center. These settings specify the center about which the transformations take place.
- Axis Constraint settings: Allow the transformation to happen using only one axis or plane. These buttons are on the Axis Constraints toolbar.

## Chapter 7: Transforming Objects, Pivoting, Aligning, and Snapping

## Understanding reference coordinate systems

Max supports several reference coordinate systems based on the UCS, and knowing which reference coordinate system you are working with as you transform an object is important. Using the wrong reference coordinate system can produce unexpected transformations.

Within the viewports, the UCS coordinates are displayed as a set of coordinates in the lower-left corner of the viewport, and the transform gizmo is oriented with respect to the reference coordinate system.

To understand the concept of reference coordinate systems, imagine that you're visiting the Grand Canyon and are standing precariously on the edge of a lookout. To nervous onlookers calling the park rangers, the description of your position varies from viewpoint to viewpoint. A person standing by you would say you are next to him. A person on the other side of the canyon would say that you're across from her. A person at the floor of the canyon would say you're above him. And a person in an airplane would describe you as being on the east side of the canyon. Each person has a different viewpoint of you (the object), even though you have not moved.

Max recognizes the following reference coordinate systems:

- View Coordinate System: A reference coordinate system based on the viewports; X points right, Y points up, and Z points out of the screen (toward you). The views are fixed, making this perhaps the most intuitive coordinate system to work with.
- Screen Coordinate System: Identical to the View Coordinate System, except the active viewport determines the coordinate system axes, whereas the inactive viewports show the axes as defined by the active viewport.
- World Coordinate System: Specifies X pointing to the right, Z pointing up, and Y pointing into the screen (away from you). The coordinate axes remain fixed regardless of any transformations applied to an object. For Max, this system matches the UCS.
- Parent Coordinate System: Uses the reference coordinate system applied to a linked object's parent and maintains consistency between hierarchical transformations. If an object doesn't have a parent, then the world is its parent and the system works the same as the World Coordinate System.
- Local Coordinate System: Sets the coordinate system based on the selected object. The axes are located at the pivot point for the object. You can reorient and move the pivot point using the Pivot button in the Hierarchy panel.
- Gimbal Coordinate System: Provides interactive feedback for objects using the Euler XYZ controller. If the object doesn't use the Euler XYZ controller, then this coordinate system works just like the World Coordinate System.
- Grid Coordinate System: Uses the coordinate system for the active grid.
- Working Coordinate System: Lets you transform the selected object about the scene's Working Pivot as defined in the Hierarchy panel.
- Pick Coordinate System: Lets you select an object about which to transform. The Coordinate System list keeps the last four picked objects as coordinate system options.

All transforms occur relative to the current reference coordinate system as selected in the Referenced Coordinate System drop-down list found on the main toolbar.

## Part II: Working with Objects

Each of the three basic transforms can have a different coordinate system specified, or you can set it to change uniformly when a new coordinate system is selected. To do this, open the General panel in the Preference Settings dialog box and select the Constant option in the Reference Coordinate System section.

## Using a transform center

All transforms are done about a center point. When transforming an object, you must understand what the object's current center point is, as well as the coordinate system in which you're working.

The Transform Center flyout consists of three buttons: Use Pivot Point Center, Use Selection Center, and Use Transform Coordinate Center, which are shown in Table 7.3. Each of these buttons alters how the transformations are done. The origin of the Transform Gizmo is always positioned at the center point specified by these buttons.

| Button | Description |
|---|---|
| [图标] | Use Pivot Point Center |
| [图标] | Use Selection Center |
| [图标] | Use Transform Coordinate Center |

### Pivot Point Center

Pivot points are typically set to the center of an object when the object is first created, but they can be relocated anywhere within the scene including outside of the object. Relocating the pivot point allows you to change the point about which objects are rotated. For example, if you have a car model that you want to position along an incline, moving the pivot point to the bottom of one of the tires allows you to easily line up the car with the incline.

If you select the Use Pivot Point Center button, then the Select and Rotate tool rotates about the pivot point for the selected object, which can be located anywhere in the scene.

### Cross-Ref

> Pivot points are discussed in detail in the next section.

### Selection Center

The Use Selection Center button sets the transform center to the center of the selected object or objects regardless of the individual object's pivot point. If multiple objects are selected, then the center is computed to be in the middle of a bounding box that surrounds all the objects.
