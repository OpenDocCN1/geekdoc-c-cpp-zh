# Part VIII: Advanced Animation Techniques

# Tip

Holding down the Shift key while dragging a handle lets you drag the handle independently of the other handle.

# FIGURE 36.15

The Key dialog box lets you change the key’s Time, Value, or In and Out tangent curves.

![](bbox=[0.06, 0.35, 0.35, 0.52])

The Lock Tangents button lets you change the handles of several keys at the same time. If this button is disabled, adjusting a tangent handle affects only the key of that handle.

# Tutorial: Animating a flowing river

The default auto-tangent types create a function curve that has ease-in and ease-out built into the curve. This causes the animation to start slowly, speed up, and then slow to a stop. While this may be a good starting point for many animations, it won’t work for those that should have a constant speed. This example shows how to create a river with a material animated to a constant speed.

To create a flowing river, follow these steps:

+   1. Open the River.max file from the Chap 36 directory on the DVD.
+   This file contains a river surface made from a loft. The V Offset for the River Water material’s diffuse channel has been animated to simulate flowing water (yes, this river has a checkered past . . .).

+   2. Click the Play button.
+   The river flow starts out slow, speeds up, and then slows to a stop.

# Note

The river flows using a checker texture map. Make sure to select a viewport with textures enabled to see the flowing effect.

+   3. Open the Track View–Curve Editor, and locate and select the V Offset track for the river’s material. (You can find this track under the Scene Materials ⇨ River Water ⇨ Maps ⇨ Diffuse Color: Map #2 (Checker) ⇨ Coordinates ⇨ V Offset menu command.)

+   4. You have two easy options for creating an animation with a constant speed. The first changes the entire controller type; the second changes the individual key’s tangent types.
+   Option 1: Right-click over the V Offset track and choose Assign Controller or choose Assign from Controller on the menu bar to open the Assign Float Controller dialog box. Select Linear Float, and click OK.
+   or
+   Option 2: Select both keys by clicking one key, holding down the Ctrl button, and clicking the other, or by dragging an outline around both keys. Click the Set Tangents to Linear button.