# FIGURE 22.1

The Attachment constraint sticks one object to the surface of another.

![](bbox=[0.072, 0.165, 0.784, 0.561])

# Tutorial: Rolling a tire down a hill with the Surface constraint

Moving a vehicle across a landscape can be a difficult procedure if you need to place every rotation and position key, but with the Surface constraint, it becomes easy. In this tutorial, you use the Surface constraint to roll a tire down a hill.

To roll a tire down a hill with the Surface constraint, follow these steps:

+   1. Open the Tire rolling on a hill.max file from the Chap 22 directory on the DVD. This file includes a patch grid hill and a wheel object made from primitives.
+   2. Create a dummy object from the Helpers category, and link the tire object to it as a child. This causes the tire to move along with the dummy object. Position the dummy object's pivot point at the bottom of the tire and the top of the hill. The pivot point can be moved using the Affect Pivot Only button in the Hierarchy panel.
+   3. Select the dummy object, choose Animation ⇨ Constraints ⇨ Surface Constraint, and select the hill object.
+   4. In the Surface Controller Parameters rollout, select the Align to V and Flip options to position the dummy and tire objects at the top of the hill. Set the V Position value to 50 to move the tire down the hill.
+   5. Click the Auto Key button (or press the N key), drag the Time Slider to frame 100, and change the U Position to 100. Click the Animate button again to deactivate it, and click the Play Animation button to see the tire move down the hill.