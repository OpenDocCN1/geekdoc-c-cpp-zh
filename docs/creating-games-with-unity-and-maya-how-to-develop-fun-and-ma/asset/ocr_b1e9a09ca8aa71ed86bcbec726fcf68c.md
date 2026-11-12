![](bbox=[0.174, 0.107, 0.638, 0.412])

FIGURE 15.12 Placed AegisChung_Arms (child of Main Camera).

Step 5: Play the game. It's going to look weird (Figure 15.13).

![](bbox=[0.03, 0.461, 0.638, 0.711])

FIGURE 15.13 What the game looks like at this point—just wrong.

> > **Why?**
> >
> > The arms are too high, we can see through the inside of the arm, all the weapons are active and on top of each other, there's no way those weapons if fired would hit where the crosshairs are pointing. The list of things that are wrong go on and on. No worries though, we just need to get those arms adjusted.

Step 6: If the gun, knife, and flashlight are visible, deactivate them. If they are not visible, they have already been deactivated. These three meshes are children of the wrist so you have to dig way down. Be sure to work in the Hierarchy and expand the AegisChung_Arms GameObject and keep expanding down until AC_R_Wrist is expanded. Select AC_Knife and deactivate it in the Inspector panel. Do the same for AC_Rifle and AC_Flashlight.