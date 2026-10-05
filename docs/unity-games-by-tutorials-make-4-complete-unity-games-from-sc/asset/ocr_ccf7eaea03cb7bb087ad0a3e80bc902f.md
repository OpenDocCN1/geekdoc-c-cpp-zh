The Graph editor displays a motion graph for selected keyframes. This lets you fine-tune the speed of each tween, slowing or speeding up an animation on either side of a keyframe. This is called easing.

The Timeline shows a simplified overview of your entire timeline, with playback controls.

> Note: To move the playhead in any timeline view, Right-click and drag. Zoom and Pan controls are almost the same as in the 3D View: Scrollwheel to zoom, and Middle-click and drag to pan. Holding Shift to pan is not necessary in a 2D panel.

# Creating an Action for the tail animation

Blender allows you to create multiple animations for a single armature, which can be triggered independently in Unity. Each animation is called an Action. You'll use Actions to create a looping animation for a swaying tail and a separate, non-looping animation for a swaying claw.

> Note: For more information on how to trigger these animations in Unity, Chapter 5, "Animations."

+   1. At the bottom of the Dope Sheet panel, click the Dope Sheet pop-up and select Action Editor.

+   2. Click the New button to create a new Action.

![](bbox=[0.198, 0.633, 0.796, 0.676])

+   3. Click the Action name and change the name to Tail Sway.

+   4. **Important:** Click the F button next to the name. This gives the Action something called a Fake User, and forces Blender to save your action, even if it is unlinked. I won't go into detail on this, except to note that your Action may not be saved if you do not press this button!

![](bbox=[0.277, 0.82, 0.722, 0.866])