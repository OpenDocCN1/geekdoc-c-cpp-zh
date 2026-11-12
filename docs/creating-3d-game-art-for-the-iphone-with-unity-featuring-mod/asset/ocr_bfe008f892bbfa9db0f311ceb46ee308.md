the Inherit Rotation setting in the Bone Properties. However, after messing with the completed rig, I decided that it would be best if the Clavicle Bones did inherit the rotations for the Chest Bone. I also decided that the Head and Spine Bones should also inherit rotations. That's just a part of rigging, and it's important to thoroughly test your rig because once you start putting it through the paces, you inevitably find areas where you'll need to make changes.

# Creating a Master Control

Again, once the final rig was completed, I created one last bone that would be used as a root in which all of the bones and controls would fall under. The purpose of this bone is that it allows me to move or rotate the character as a whole. In Fig. 6.26, you can see the Master control. The Pelvis, CNTRL_Foot.L, and CNTRL_Foot.R Bones are parented to the Master control.

![](bbox=[0.336, 0.435, 0.946, 0.89])

FIG 6.26 The Master Control Is the Root of the Entire Rig and Can Be Used to Move Tarek as a Whole.