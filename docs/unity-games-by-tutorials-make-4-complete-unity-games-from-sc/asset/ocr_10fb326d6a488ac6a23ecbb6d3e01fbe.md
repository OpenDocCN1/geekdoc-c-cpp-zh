![](bbox=[0.158, 0.087, 0.831, 0.269])

+   Don't forget to go to Properties > Bone to name the bone Elbow.L, and deselect the Deform checkbox.

+   Switch to Pose Mode and select the forearm bone. Go to Properties > Constraints, click the Pole Target field, and select Armature. select the Elbow.L bone.

+   Orbit around your model to ensure the elbow is pointed at the Pole Target. If it's not, adjust the Pole Angle until it looks right. -90 worked for me.

![](bbox=[0.218, 0.467, 0.781, 0.597])

> Note: In Blender, input fields that have arrows on the left and right side can be adjusted by clicking on them and dragging left and right.

# Flipping the arm bones for the other arm

+   Remember when you flipped the arm geometry in the modeling chapter? Flipping the bones is the same: First, make sure you're in Edit mode, then press Shift-S to snap the 3D Cursor to the center. (period) to Transform around the cursor. Select all the arm bones, including the IK and Pole Targets, and press Shift-D then Enter to duplicate. Ctrl-M X then Enter to mirror over the X-axis.