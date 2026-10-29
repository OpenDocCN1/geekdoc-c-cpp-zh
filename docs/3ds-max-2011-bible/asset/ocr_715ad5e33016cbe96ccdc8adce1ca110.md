# FIGURE 7.8

The Locks rollout can prevent any transforms along an axis.

![](bbox=[0.019, 0.16, 0.202, 0.393])

# Tutorial: Landing a spaceship in port

Transformations are the most basic object manipulation that you will do and probably the most common. This tutorial includes a spaceship object and a spaceport. The goal is to position the spaceship on the landing pad of the spaceport, but it is too big and in the wrong spot. With a few clever transformations, you'll be set.

To transform a spaceship to land in a spaceport, follow these steps:

+   1. Open the Transforming spaceship.max file from the Chap 07 directory on the DVD.
+   2. To prevent any extraneous movements of the spaceport, select the spaceport by clicking it. Open the Hierarchy panel, and click the Link Info button. Then in the Locks rollout, select all nine boxes to restrict all transformations so that that spaceport won't be accidentally moved.
+   3. To position the spaceship over the landing platform, select the spaceship object and click the Select and Move button in the main toolbar (or press the W key). The Move Gizmo appears in the center of the spaceship object. If you don't see the Move Gizmo, press the X key. Make sure that the Reference Coordinate System is set to View and that the Use Selection Center option is enabled. Right-click the Left viewport to make it active, select the red X-axis line of the gizmo, and drag to the right until the center of the spaceship is over the landing pad.
+   4. Right-click the Front viewport, and drag the red X-axis gizmo line to the left to line up the spaceship with the center of the landing pad.
+   5. Click the Select and Uniform Scale button (or press the R key). Place the cursor over the center gizmo triangle, and drag downward until the spaceship fits within the landing pad.
+   6. Click the Select and Move button again (or press the W key), and drag the green Y-axis gizmo line downward in the Front viewport to move the spaceship toward the landing pad.
+   7. Click the Select and Rotate button (or press the E key). Right-click the Top viewport, and drag the blue Z-axis gizmo circle downward to rotate the spaceship clockwise so that its front end points away from the buildings.

Figure 7.9 shows the spaceship correctly positioned.