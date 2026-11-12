# ## Fixing the Pelvis Bone for Hip Sway

In order to correctly setup the Pelvis so that the hips will swing correctly, I needed to add another bone. The reason being is that a bone's pivot will be located at the tail. However, I want to change the pivot of the Pelvis bone so that it will rotate more in the hip area of the model. First, I duplicated the Pelvis bone by pressing Shift + D. Next, I named this bone PelvisRotHelper and then selected the Pelvis bone and switched its direction by pressing Alt + F or by accessing the Switch Direction command in Edit Mode via the Specials menu, which can be activated by pressing the "W key" as shown in Fig. 5.30.

I then parented the PelvisRotHelper to the Pelvis with the Keep Offset option as shown in Fig. 5.31. Finally, the first Spine bone was parented to the PelvisRotHelper with the Connected option as shown in Fig. 5.32.

Finally, the leg bones (Thighs) are parented to the Pelvis bone. This setup creates a nice hip sway in that the Pelvis bone's rotation is located just below the first Spine bone and places the pivot of the rotation right in the hip area of the mesh as shown in Fig. 5.33.

# ## Disabling Inherit Rotation

The last step in building the rig is to disable the Inherit Rotation setting for the first Spine bone, the Chest and Shoulder bones. By telling these bones to not inherit the rotations from its parent, the bone will effectively stay

![](bbox=[0.34, 0.66, 0.94, 0.905])

FIG 5.30 The Pelvis Bone's Direction Was Flipped so Its Pivot Would Be in the Correct Place to Produce a Nice Hip Sway