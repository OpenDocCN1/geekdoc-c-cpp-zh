# Part IX: Working with Characters

# FIGURE 39.8

The moose’s skin has been rigged using the CAT tools.

![](bbox=[0.07, 0.22, 0.78, 0.65])

# Animating a CAT Rig

The best rig in the world doesn’t do you much good if you can’t animate it well. Luckily, CAT’s animation tools are excellent, just like its rigging tools. CAT uses the concept of animation layers to hold its animation keys. This allows you to blend between different motions.

# Cross-Ref

Animation layers are also discussed in Chapter 34, “Using Animation Layers, Modifiers, and Complex Controllers.” ■

All the animation controls for CAT rigs are found in the Motion panel whenever any of the rig’s bones are selected. Within the Layer Manager rollout, shown in Figure 39.9, is a list of the available animation layers. To create a new animation layer, select from four different types, using the Add Layer drop-down list at the bottom right of the list. The four animation layer types include the following:

+   - Absolute Layer: Holds animation key data that defines full motions
+   - Local Adjustment Layer: Holds relative key data relative to the local coordinate system of the above layer
+   - World Adjustment Layer: Applies relative motion in world space that is independent of the previous layers
+   - CAT Motion Layer: Is used to create procedural-based looping motion such as walk cycles