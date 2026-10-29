
## Chapter 11: Introducing Modifiers and Using the Modifier Stack

+   3. In the Modifier Stack, click the plus icon to the left of the modifier name and select the Gizmo subobject. Move the gizmo in the Top viewport so only the front corner of the car is selected. In the Parameters rollout, select the Vertex option.

+   4. Choose the Modifiers ⇨ Parametric Deformers ⇨ Noise menu command to apply the Noise modifier to the selected volume. In the Parameters rollout, enable the Fractal option and set the X, Y, and Z Strength values to 30.

+   5. Choose Modifiers ⇨ Parametric Deformers ⇨ XForm to apply the XForm modifier, and use its gizmo to push the selected area up and to the left in the Top viewport. This step makes the section look dented.

Figure 11.7 shows the resulting damaged car. Notice that the rest of the object is fine and only the selected volume area is damaged.

# FIGURE 11.7

The Noise and XForm modifiers are applied to just the subobject selection.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_334_0.png)

# Cross-Ref

You can see another example of how a Selection modifier can be used to select and apply a modifier to a subobject selection in Chapter 10, “Accessing Subobjects and Using Modeling Helpers.”

## Parametric Deformer modifiers

Perhaps the most representative group of modifiers are the Parametric Deformers. These modifiers affect the geometry of objects by pulling, pushing, and stretching them. They all can be applied to any of the modeling types, including primitive objects.

### Note

In the upcoming examples, you might start to get sick of seeing the hammer model used over and over, but using the same model enables you to more easily compare the effects of the various modifiers, and it’s more interesting to look at than a simple box.

### Affect Region modifier

The Affect Region modifier can cause a local surface region to bubble up or be indented. Affect Region parameters include Falloff, Pinch, and Bubble values. The Falloff value sets the size of the affected area. The Pinch value makes the region tall and thin, and the Bubble value rounds the affected region. You also can select the Ignore Back Facing option. Figure 11.8 shows the Affect Region modifier applied to a Quad Patch with a Falloff value of 80 on the left and with a Bubble value of 1.0 on the right. The height and direction of the region are determined by the position of the modifier gizmo, which is a line connected by two points.

### Note

The Affect Region modifier accomplishes the same effect as the Soft Selection feature, but Affect Region applies the effect as a modifier, making it easier to discard.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_335_0.png)

The Affect Region modifier can raise or lower the surface region of an object.

### Bend modifier

The Bend modifier can bend an object along any axis. Bend parameters include the Bend Angle and Direction, Bend Axis, and Limits. The Bend Angle defines the bend in the vertical direction, and the Direction value defines the bend in the horizontal direction.

Limit settings are the boundaries beyond which the modifier has no effect. You can set Upper and Lower Limits relative to the object’s center, which is placed at the object’s pivot point. Limits are useful if you want the modifier applied to only one half of the object. The Upper and Lower Limits are visible as a simple plane on the modifier gizmo. For example, if you want to bend a tall cylinder object and have the top half remain straight, you can simply set an Upper Limit for the cylinder at the location where you want it to stay linear.

### Note

Several modifiers have the option to impose limits on the modifier, including Upper and Lower Limit values.

The hammer in Figure 11.9 shows several bending options. The left hammer shows a Bend value of 75 degrees around the Z-axis, the middle hammer also has a Direction value of 60, and the right hammer has an Upper Limit of 8.

# FIGURE 11.9

The Bend modifier can bend objects about any axis.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_336_0.png)

### Tutorial: Bending a tree

If you have a tree model that you want to bend as if the wind were blowing, you can apply the Bend modifier. The tree then bends about its Pivot Point. Luckily, all the trees and plants found in the AEC Objects category have their Pivot Points set about their base, so bending a tree is really easy.

To bend a tree using the Bend modifier, follow these steps:

+   1. Select the Create > AEC Objects > Foliage menu command to access the available trees. Select a long, thin tree like the Yucca, and click in the Top viewport to add it to the scene.
+   2. With the tree selected, select the Modifiers > Parametric Deformers > Bend menu command to apply the Bend modifier to the tree.
+   3. In the Parameters rollout found in the Modify panel, set the Bend Axis to Z and the Bend Angle to 60.
      The tree bends as desired.

Figure 11.10 shows the bending Yucca plant. To animate this tree bending back and forth, just set keys for the Angle parameter.

### Displace modifier

The Displace modifier offers two unique sets of features. It can alter an object's geometry by displacing elements using a gizmo, or it can change the object's surface using a grayscale bitmap image. The Displace gizmo can have one of four different shapes: Planar, Cylindrical, Spherical, or Shrink Wrap. This gizmo can be placed exterior to an object or inside an object to push it from the inside.

## Part III: Modeling Basics

# FIGURE 11.10

The Bend modifier can be used to bend trees.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_337_0.png)

### Caution

In order for the Displace modifier to work, the surface requires a dense mesh, which can lead to very high polygon counts. ■

The Displace modifier parameters include Strength and Decay values. You can also specify the dimensions of the gizmo. A cylindrical-shaped gizmo can be capped or uncapped. The alignment parameters let you align the gizmo to the X-axis, Y-axis, or Z-axis, or you can align it to the current view. The rest of the parameters deal with displacing the surface using a bitmap image. Figure 11.11 shows a Quad Patch with the Plane-shaped gizmo applied with a Strength value of 25. To the right is a Quad Patch with the Sphere-shaped gizmo.

# Cross-Ref

The Displace modifier can also alter an object’s geometry using a grayscale bitmap image. This is similar to a Displacement map, which is covered in Chapter 17, “Adding Material Details with Maps.” In many ways, the Displace gizmo works like the Conform compound object. You can learn about the Conform compound object in Chapter 27, “Working with Compound Objects.”

## Chapter 11: Introducing Modifiers and Using the Modifier Stack

# FIGURE 11.11

You can use the Displace modifier’s gizmo as a modeling tool to change the surface of an object.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_338_0.png)

### Lattice modifier

The Lattice modifier changes an object into a lattice by creating struts where all the edges are located or by replacing each joint with an object. The Lattice modifier considers all edges as struts and all vertices as joints.

The parameters for this modifier include several options to determine how to apply the effect. These options include Apply to Entire Object, to Joints Only, to Struts Only, or Both (Struts and Joints). If the Apply to Entire Object option isn’t selected, then the modifier is applied to the current subobject.

For struts, you can specify Radius, Segments, Sides, and Material ID values. You can also specify to Ignore Hidden Edges, to create End Caps, and to Smooth the Struts.

For joints, you can select Tetra, Octa, or Icosa types with Radius, Segments, and Material ID values. There are also controls for Mapping Coordinates.

### Note

Although the joints settings enable you to select only one of three different types, you can use the Scatter compound object to place any type of object instead of the three defaults. To do this, apply the Lattice modifier and then select the Distribute Using All Vertices option in the Scatter Objects rollout.

Figure 11.12 shows the effect of the Lattice modifier. The left hammer has only joints applied, the middle hammer has only struts applied, and the right hammer has both applied.

### Mirror modifier

You can use the Mirror modifier to create a mirrored copy of an object or subobject. The Parameters rollout lets you pick a mirror axis or plane and an Offset value. The Copy option creates a copy of the mirrored object and retains the original selection.

### Note

The Mirror modifier works the same as the Mirror command found in the Tools menu, but the modifier is handy if you want to be able to quickly discard the mirroring changes.
