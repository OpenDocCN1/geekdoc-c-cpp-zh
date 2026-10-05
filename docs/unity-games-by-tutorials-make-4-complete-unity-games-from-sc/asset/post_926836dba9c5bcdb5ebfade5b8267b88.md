
## Animating the claw

Start by animating the IK Target for the left arm; Arm IK Target.L.

- Make sure you are still in Pose mode, and select that bone.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_487_0.png)

- Right-click on any of the axes in the Location section of the Properties shelf. This time, you'll create a keyframe for all three axes by selecting Insert Keyframes. All three fields turn yellow; your starting keyframes for this bone are now set.

| Transform | |
| :--- | :--- |
| X: | 0.00000 |
| Y: | 0.00000 |
| Z: | 0.00000 |

> Note: Only keyframe all axes if you know the object will be moving in all three directions. Creating keyframes only for the axes you are animating keeps your Dope Sheet nice and clean. This becomes more important as your animations get more complex.

- Continue creating the following keyframes for the Arm IK Target.L bone.

## Frame 20:

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_488_0.png)

## Frame 40:

## Frame 65:

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_488_1.png)

Now, you have the basic movement keyed for a claw attack. Press Alt-A to preview your animation. It's coming along, but it's definitely not quite right yet. This tweened animation is *too smooth*. Remember, adjusting the tweening times involves the *Graph editor*.

## Creating sharp, sudden movement with the Graph editor

Right now, the claw attack looks more like a friendly wave. You want the claw to quickly dart forward, hit whatever it's attacking and bounce off.

## Unity Games by Tutorials

## Chapter 17: Animating in Blender

At this point, the Graph editor should look like this:

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_489_0.png)

> Note: See the small dots at the ends of each scroll bar? Try dragging them to adjust the vertical or horizontal scale of the graph.

The tip of the attack animation is at frame 40. Making a sudden change in direction involves changing the curves at this frame to a sharp angle. However, simply dragging a handle doesn't create a sharp angle, it only adjusts the curve:

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_489_1.png)

To create a sharp angle, you need to change the Keyframe Handle Type. Select the keyframe itself — the dot in the middle, not one of the handles on either side — press V to open the Set Keyframe Handle Type menu, and select Vector.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_489_2.png)

raywenderlich.com

## Unity Games by Tutorials

Convert all three keyframes at frame 40 to Vector, and adjust their handles to look like this:

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_490_0.png)

Press Alt-A to preview your animation. Much better! The elbow draws back, has a short pause, then the springs shift forward. One thing that could use some adjustment is the animation after the strike. Right now, it doesn't look like it bounces off, or recoils, after hitting its target.

Move the playhead to frame 50 and set the following keyframe:

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_490_1.png)

Press Alt-A to preview. Now the animation feels much more natural.

> Note: This is a good method for creating an animation. Start by keying the basic outline of the animation first, then add keyframes where necessary, to add extra movement details.

## Adjusting the Pole Target to raise the elbow

The claw attack animation is almost complete. Using the Pole Target will allow you to raise the elbow, so that the arm comes up, and strikes from above. Select the Elbow.L pole bone.

- 1. Move the playhead to frame zero. The Pole Target will move up and down, so right-click the Location: Y field and select Insert Single Keyframe.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_491_0.png)

- 2. Move the playhead to frame 20. Change the Location: Y field to 1.5, right-click it, and select Insert Single Keyframe.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_491_1.png)

- 3. Move the playhead to frame 65 and create a keyframe setting the Y value back to zero.

Preview the animation and orbit around it while it's playing. Now the elbow comes up, as the arm is pulled back.

## Opening the claws using Forward Kinematics

For the claws, instead of moving the object they are aimed at, simply rotate them. This is called Forward Kinematics.

- Move the playhead to frame 0 then select the Thumb.L bone. Look in Properties shelf, ensure Rotation Mode is set to XYZ Euler, then right-click the Z value and create a single keyframe of 0.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_492_0.png)

- Move the playhead to frame 20 and change the Z Rotation to -50. Don't forget to right-click and select Single Keyframe.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_492_1.png)

- Move the playhead to frame 40 and set the Z Rotation back to 0 (remember to also duplicate the keyframe at frame zero and move it to frame 40).

Repeat this process for the Claw bone. At frame 20 for this bone, set the Z Rotation to 30:

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_493_0.png)

Preview your animation; the claw animation is nearly complete. The keyframes are all set; the only thing that could be better is the speed. The animation feels a bit slow.

## Scaling keyframes in the Dope Sheet

Selecting some keyframes and squashing or stretching them on the timeline is simple, using the Scale tool. One important to note is that the point in time it scales is from the playhead.

- Move your playhead to frame zero and press A to Select All. Press S to Scale:

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_493_1.png)

- Drag your cursor toward the playhead to compress the time for the selected keyframes. Scale it until the last keyframes are on frame 40, and left-click when you're finished.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_493_2.png)

This is a very easy way to speed up or slow down the timing of multiple keyframes. Just remember to move the playhead to the keyframe that should remain unchanged, before scaling.

## Copying the animation to the other arm

If you want your scorpion to be able to give the one-two-punch, the animation you just created needs to be copied to the right arm.

- 1. In the Dope Sheet, make sure the Claw Attack.L action is selected, and press the + (plus) button next to the action name to duplicate it. Rename the new one Claw Attack.R. Don't forget to click the F button.
- 2. In 3D View, select the Arm IK Target.L bone.
- 3. In the Graph editor, if your points aren't selected, press A to Select All.
- 4. With the cursor over the Graph editor, press Ctrl-C to copy the animation curves.
- 5. In the 3D View, select the Arm IK Target.R bone.
- 6. Make sure the playhead is at frame 0, then in the Properties panel, right-click one of the Location fields and Insert Keyframes. The X, Y and Z Location channels will appear in the Graph editor for the Arm IK Target.R object.
- 7. In the Graph Editor, press Ctrl-V to paste the animation data.

> Note: In my experience, the animation does not always look exactly mirrored, so you may need to play with the keyframes bit if you want them to be exactly the same. When animating a living creature, it's OK if each arm is not exactly the process will need to be repeated for each object. Take the channel(s) you are animating, and create an empty keyframe in that channel, so that you have somewhere to paste the animation.

Don't forget to double-check the XYZ Rotation Order pop-up when you rotate the thumb and claw bones – they need to be set to XYZ Euler. Once you paste the rotation values for the thumb, you'll see that it's rotating in the opposite direction to how it should be. To fix:

- 1. Move the playhead to the frame with the appropriate keyframe (if you scaled this animation the same as I did, it should be frame 12).
- 2. Select the Thumb.R bone in the 3D View. In the Properties panel, change the Z Rotation value from -50 to 50.
- 3. Right-click on the field and select Replace Single Keyframe.

> Note: Any time you change a keyed value, you need to use Replace Single Keyframe to update the keyframe itself. If you do not, your change will be removed as soon as you move the head.

Once you have the animation working for the right arm, be sure to use B to Select all the keyframes for the left arm, and press X followed by Delete Keyframes in the Dope Sheet to remove them from the Claw Attack. action.

> Note: If you'd like to see Blender file at this point, find 03-Scorpion-Animated.blend in the Resources folder.

## Where to go from here?

Congratulations! You've learned how to rig a character and create animations in Blender. I hope you had fun, and can see the potential for all kinds of character animations and object movement that can use in your games.

In this chapter, you've learned:

+- How to rig a model using bones.

- How to apply a mesh to rig so that it moves when the bones move.

- How to use Inverse Kinematics to make animations easier and more natural.

- How to use Pole Targets to aim a bone at specified object.

- How to animate an armature using keyframes and the Dope Sheet

- How to adjust animation tween to create smooth or sharp animations using the Graph editor.

- How to create multiple animations for a single armature using Actions, for use in Unity.

Try creating a separate Tail Smash Action, where the tail takes a swing and smashes to the ground — or a Victory Dance Action using the arms.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_495_0.png)
