# Part IX: Working with Characters

text field directly under the bones list lets you locate specific bones in the list by typing the name. Only one bone at a time may be selected from the list. The Remove button removes the selected bone from the bone list.

# Tutorial: Attaching skin to a CAT rig

For human figures, using a biped skeleton saves lots of time. For this example, because he's human in form, you'll bind a biped skeleton to the Future man model.

To bind the skin of a model to a biped skeleton, follow these steps:

+   1. Open the Marvin Moose CAT rig - final.max file from the Chap 40 directory on the DVD. This file includes the CAT rig built in Chapter 39 for the Marvin Moose character.
+   2. With the CAT rig aligned to the skin mesh, select Unfreeze All from the right-click quadmenu and disable the See-Through option in the Object Properties dialog box. Select the moose model, and choose Modifiers > Animation Modifiers > Skin to apply the Skin modifier.
+   3. In the Parameters rollout, click the Add button. The Select Bones dialog box opens. Click the All button to select all the bones, and click Select. Don't include the Footsteps, Character001, or the Leg Platform objects.
+   4. In the Parameters rollout, select each of the bones in the list and click the Edit Envelopes button. Zoom in on the highlighted bone (which is the left shin bone), select the cross-section handles for this bone, and set the Radius values to 0.15 near the body and 0.1 for the other end. Figure 40.2 shows the moose skin with all the CAT rig bones added.

# FIGURE 40.2

Bone references are added to the skin modifier.

![](bbox=[0.07, 0.64, 0.92, 0.92])