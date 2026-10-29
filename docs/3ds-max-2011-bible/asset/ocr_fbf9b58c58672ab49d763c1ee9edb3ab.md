# Part III: Modeling Basics

# Cross-Ref

Each of the Selection modifiers is covered for the various modeling types in its respective chapter. For example, to learn about the Patch Select modifier, see Bonus Chapter 3 on the DVD, “Working with NURBS.”

When a Selection modifier is applied to an object, the transform buttons on the main toolbar become inactive. If you want to transform the subobject selection, you can do so with the XForm modifier.

# Volume Select modifier

Among the Selection modifiers, the Volume Select modifier is unique. It selects subobjects based on the area defined by the modifier’s gizmo. The Volume Select modifier selects all subobjects within the volume from a single object or from multiple objects. One of the benefits of using this modifier is that the subobjects within the volume can change as the object is moved during an animation sequence. It also can work with several objects at once.

In the Parameters rollout for the Volume Select modifier, you can specify whether subobjects selected within a given volume should be Object, Vertex, or Face subobjects. Any new selection can Replace, be Added to, or be Subtracted from the current selection. You can use the Invert option to select the subobjects outside of the current volume. You can also choose either a Window or Crossing Selection Type.

The actual shape of the gizmo can be a Box, Sphere, Cylinder, or Mesh Object. To use a Mesh Object, click the button beneath the Mesh Object option and then click the object to use in a viewport. In addition to selecting by a gizmo-defined volume, you can also select subobjects based on certain surface characteristics, such as Material IDs, Smoothing Groups, or a Texture Map including Mapping Channel or Vertex Color. This makes it possible to quickly select all vertices that have a Vertex Color assigned to them.

The Alignment options can Fit or Center the gizmo on the current subobject selection. The Reset button moves the gizmo to its original position and orientation, which typically is the bounding box of the object. The Auto Fit option automatically changes the size and orientation of the gizmo as the object it encompasses changes.

# Note

The Volume Select modifier also includes a Soft Selection rollout. Soft Selection lets you select adjacent subobjects to a lesser extent. The result is a smoother selection over a broader surface area. The Soft Selection options are explained in Chapter 10, “Accessing Subobjects and Using Modeling Helpers.”

# Tutorial: Applying damage to a car

In this tutorial, you use the Volume Select modifier to select the front corner of a car and then apply Noise and XForm modifiers to make the corner look like it’s been damaged in a collision.

To use modifiers to make a section of a car appear damaged, follow these steps:

+   1. Open the Damaged car.max file from the Chap 11 directory on the DVD.
+      This file includes a car model created by Viewpoint Databanks.
+   
+   2. With the front end of the car selected, choose the Modifiers → Selection Modifiers → Volume Select menu command.
+      This command applies the Volume Select modifier to the group.