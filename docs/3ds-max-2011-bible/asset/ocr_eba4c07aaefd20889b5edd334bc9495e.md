# Part VIII: Advanced Animation Techniques

# FIGURE 36.25

The hazard light flashing on

![](bbox=[0.07, 0.17, 0.82, 0.62])

# Tutorial: Animating a checkers move

As an example of working with function curves, you'll animate a checkers move in this tutorial. It is often easiest to block in the animation using keyframing and then to refine the animation in the Track View.

To animate a white checker making its moves, follow these steps:

+   1. Open the Checkers.max file from the Chap 36 directory on the DVD.
+   This file contains a simple checkerboard with one white piece and three red pieces.
+   The white checker is on the wrong-colored square to start, so first you move it into place and then to each successive position.

+   2. Turn on Auto Key. Move the time slider to frame 25, and move the white checker to the square with the "1" text object (visible in the Top viewport). Move the time slider to 50, and move the white piece to the "2" position. At frame 75, move it to the "3" position, and at 100, move it to the "4" position. Turn off Auto Key.

+   3. Right-click over the white piece, and choose Curve Editor to open the Track View-Curve Editor. The white piece's X, Y, and Z Position tracks should be highlighted, and you should be able to see the function curves in the graph editor. If not, find them by choosing Objects→ White Piece→ Transform→ Position→ X, Y and Z Position.
+   Keeping in mind that RGB (red, green, blue) = XYZ, you can see the white checker's movement across the board. From 0 to 25, it moves only in the X direction. From 25 to 100, it moves