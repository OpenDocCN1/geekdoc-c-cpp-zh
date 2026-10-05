
# Unity Games by Tutorials

## Chapter 17: Animating in Blender

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_472_0.png)

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_472_1.png)

- 4. Switch back to Pose mode and select the yellow bone at the end of the tail. In the Properties panel, click the Bone Constraints tab, click the Pole Target field, and select the Armature. Another field appears below lets you choose the specific bone. Select the Tail Pole bone.

- 5. Press 1 to switch to Front view. It doesn't look quite right... the tail is pointed to the side, instead of the Pole Target!

- 6. Back in the Bone Constraints tab, find the Pole Angle field. Click and drag side-to-side to adjust this number and see how the changes affect your model in real time. In this case, a value of -90 degrees works perfectly.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_472_2.png)

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_472_3.png)

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_472_4.png)

- Press 3 to go back to Side view, then select the Tail Target bone and press 1 again to switch back to Front View. Move the bone left and right (G to grab) to see how it affects the tail.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_472_5.png)

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_472_6.png)

Fantastic! The rig for the tail is now complete.

## Adding the arm bones

Select the existing armature and enter Edit mode. You'll use the same armature for the arm bones.

- 1. Start in Top view, set your 3D Cursor to the spot where the left arm meets the body. Press Shift-A to create the first bone.

- 2. Press P to switch to front view, as your first bone is created in an upright position. Click the middle portion of the bone to select the whole bone. Drag the blue arrow up until its base is inline with the center of the arm.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_473_0.png)

- 3. Press A to deselect, then select the end of the bone, and press G to grab it and move it approximately to the elbow.

- 4. Press 7 to switch to Top view. Drag the green arrow to move the end of the bone forward to align it in this view, too.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_473_1.png)

- 5. Stay in Top view and press E to extrude a new bone to the midpoint of where the “thumb” meets the “hand,” shown here.

- 6. Press E again to extrude a “thumb” bone.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_474_0.png)

- 7. Click the end of bone 2 and press E to extrude a bone to the midpoint of where the large claw meets the “hand.”

- 8. Press E to extrude the bone for large claw.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_474_1.png)

> **Note:** Name each bone, and be sure to use “L” at the end of each name. In the Properties > Armature tab, select the Names checkbox to see bone names in 3D View.

## Adding the arm IK

Another way to create an IK Target is to extrude it from the joint you want to point at. You want the “hand” to point at the IK Target, but not the claws, which will move separately.

- 1. Select the sphere at the intersection of the arm and “thumb” bones.

- 2. Press E and extrude a bone out the left.

- 4. In the Properties panel, under the Bone tab, rename the bone IK Target.L. Don't forget to scroll down and deselect the Deform checkbox.

- 5. Switch to Pose mode, select the IK Target.L bone first, then Shift-select the “forearm” bone. Press Ctrl+C and select Inverse Kinematics. The forearm turns yellow.

- 6. Select the forearm. For the purposes of IK, this has two bones. In the Bone Constraints tab, set the Chain Length to 2.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_475_1.png)

## Adding the Pole Target for the elbow

- 1. Switch to Edit mode. Select the sphere at the “elbow” of the arm.

- 2. Press 1 to switch to Front view, and press E to extrude the arm upward.

- 3. Press A to Select None, then select the bone, press Alt-P and select Clear Parent. Press 7 to switch to Top view, press G and drag the bone away from the arm a bit.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_476_0.png)

- Don't forget to go to Properties > Bone to name the bone Elbow.L, and deselect the Deform checkbox.

- Switch to Pose Mode and select the forearm bone. Go to Properties > Constraints, click the Pole Target field, and select Armature select Elbow.L bone.

- Orbit around your model to ensure the elbow is pointed at the Pole Target. If it's not, adjust the Pole Angle until it looks right. -90 worked for me.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_476_1.png)

> **Note:** In Blender, input fields that have arrows on the left and right side can be adjusted by clicking on them and dragging left and right.

## Flipping the arm bones for the other arm

- Remember when you flipped the arm geometry in the modeling chapter? Flipping the bones is the same: First, make sure you're in Edit mode, then press Shift-S to snap the 3D Cursor to the center. Transform around the cursor. Select all the arm bones, including the IK and Pole Targets, and press Shift-D then Enter to duplicate. Ctrl-M X then Enter to mirror over the X-axis.

- 2. In the menu at the bottom of the 3D View, select Armature ▸ Flip Names to automatically rename bones with L to .R, for the right arm.

- 3. Switch to **Object Mode**. You've created new bones, but they have not had their Automatic Weights set up for the mesh. Select the mesh, then **Shift-click** the armature. Press **Ctrl-P** and select **Set Parent To Armature Deform ▸ With Automatic Weights**. The mesh is already parented to the armature, so now it just recalculates the automatic weights; this time for all the new bones.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_477_0.png)

- 4. What happened to the right arm? When the bones got flipped, the **Pole Angle** for the elbow stayed the same. Switch to **Pose mode** and select the yellow-highlighted bone in the right arm. In the **Properties** panel, click the **Bone Constraints** tab, and change the **Pole Angle** to **90.**

Your rig is now complete! Time for some movement...

> **Note:** Don't forget to save. If you want to look at the rig I made, open **02-Scorpion-Rigged.blend** in the Resources folder.

## Animation

Creating animation in Blender is similar to other apps; it uses **keyframes** and **tweening**.

A keyframe is a point in time where you specified the position, for example. Then you set another keyframe at a different time. When you play the animation, the object will move smoothly from the position set by the first keyframe, to the position set by the second keyframe. This automatically generated motion is called tweening.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_478_0.png)

At the top of the screen, switch to the Animation workspace. There are some new panels:

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_478_1.png)

- The Dope Sheet shows you an overview of everything that is animated, in your scene. Every property you animate will show up as a channel in the left column, with its keyframes displayed in the timeline column.

The Graph editor displays a motion graph for selected keyframes. This lets you fine-tune the speed of each tween, slowing or speeding up animation on either side of a keyframe. This is called easing.

The Timeline shows a simplified overview of your entire timeline, with playback controls.

> **Note:** To move the playhead in any timeline view, Right-click and drag. Zoom and Pan controls are almost the same as in the 3D View: Scrollwheel to zoom, and Middle-click and drag to pan. Holding Shift to pan is not necessary in a 2D panel.

## Creating an Action for the tail animation

Blender allows you to create multiple animations for a single armature, which can be triggered independently in Unity. Each animation is called an Action. You'll use Actions to create a looping animation for a swaying tail and a separate, non-looping animation for a swaying claw.

> **Note:** For more information on how to trigger these animations in Unity, Chapter 5, "Animations."

- 1. At the bottom of the Dope Sheet panel, click the Dope Sheet pop-up and select Action Editor.

- 2. Click the New button to create a new Action.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_479_0.png)

- 3. Click the Action name and change the name to Tail Sway.

- 4. **Important:** Click the F button next to the name. This gives the Action something called a Fake User, and forces Blender to save your action, even if it is unlinked. I won't go into detail on this, except to note that your Action may not be saved if you do not press this button!

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_479_1.png)
