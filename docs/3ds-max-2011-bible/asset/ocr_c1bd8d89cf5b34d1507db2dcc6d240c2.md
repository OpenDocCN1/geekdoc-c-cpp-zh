# Parametric Deformer modifiers

Perhaps the most representative group of modifiers are the Parametric Deformers. These modifiers affect the geometry of objects by pulling, pushing, and stretching them. They all can be applied to any of the modeling types, including primitive objects.

# Note

In the upcoming examples, you might start to get sick of seeing the hammer model used over and over, but using the same model enables you to more easily compare the effects of the various modifiers, and it’s more interesting to look at than a simple box.

# Affect Region modifier

The Affect Region modifier can cause a local surface region to bubble up or be indented. Affect Region parameters include Falloff, Pinch, and Bubble values. The Falloff value sets the size of the affected area. The Pinch value makes the region tall and thin, and the Bubble value rounds the affected region. You also can select the Ignore Back Facing option. Figure 11.8 shows the Affect Region modifier applied to a Quad Patch with a Falloff value of 80 on the left and with a Bubble value of 1.0 on the right. The height and direction of the region are determined by the position of the modifier gizmo, which is a line connected by two points.

# Note

The Affect Region modifier accomplishes the same effect as the Soft Selection feature, but Affect Region applies the effect as a modifier, making it easier to discard.

![](bbox=[0.077, 0.565, 0.701, 0.731])

The Affect Region modifier can raise or lower the surface region of an object.

# Bend modifier

The Bend modifier can bend an object along any axis. Bend parameters include the Bend Angle and Direction, Bend Axis, and Limits. The Bend Angle defines the bend in the vertical direction, and the Direction value defines the bend in the horizontal direction.

Limit settings are the boundaries beyond which the modifier has no effect. You can set Upper and Lower Limits relative to the object’s center, which is placed at the object’s pivot point. Limits are useful if you want the modifier applied to only one half of the object. The Upper and Lower Limits are visible as a simple plane on the modifier gizmo. For example, if you want to bend a tall cylinder object and have the top half remain straight, you can simply set an Upper Limit for the cylinder at the location where you want it to stay linear.