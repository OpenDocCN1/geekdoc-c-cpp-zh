
**FIGURE 10.17** Testing the leg rig. Moving and rotating the modified circle allows the entire leg and foot to be modified.

![](img/0285f88bc840f313779e011725b623a5_311_0.png)

### Tips and Tricks

When working with this rig, further refinement can be done by moving the IK handles within the handle. For instance, moving the toe IK handles will raise the toe. Now, although this provides some quick-and-dirty access to foot movement, it is clumsy and crude. This version is saved in the files included on the web site (http://www.Creating3dGames.com) for this book as AegisChung-SingleMesh-SimpleFoot, but for an alternative foot rig (that's beyond the scope of this book), check out the AegisChung-SingleMesh also included in the sample files.

## Spine

The next chunk of joints will be up the spine, neck, and head. In reality, our spines are actually 24 articulating vertebrae (and another 9 fused vertebrae in the sacrum and coccyx). However, we won't be putting nearly that many joints in Aegis.

There are two reasons for this. First, controlling that many joints without a complex back rig is unwieldy and would make animation much too painful. But, in games, the most important reason is we are attempting to keep our data set manageable. A mesh that is being deformed by hundreds of joints will be a slow real-time calculation and thus slow the game down. Keeping the number of joints low keeps the mesh deformation calculations light and the game snappy. Picking the number of joints is another of the choices in that never-ending challenge of game design in which the designers and artists must find the balance between quality and performance.

- **Step 44:** Activate the Joint tool (Animation>Skeleton>Joint Tool) and in the side-view panel, create a string of six joints to match Figure 10.18. Name them as indicated in the screenshot.

![](img/0285f88bc840f313779e011725b623a5_313_0.png)

FIGURE 10.19 Creating the start of the arms.

![](img/0285f88bc840f313779e011725b623a5_313_1.png)

FIGURE 10.20 Adjusting the position of joints in the side view to more accurately match real anatomy.

- **Step 48:** Create and position a string of joints to control the middle, ring, and pinky fingers. Do this in either the front- or side-view panels with the Joint tool. Be sure to grow this new chain off of the extant AC_L_Wrist joint (with the Joint tool activated, first click the wrist joint (it will highlight green) and then start clicking to create new joints). The final results should look like Figure 10.21 (which is a perspective view for illustration purposes).

FIGURE 10.21 Newly created finger joints.

![](img/0285f88bc840f313779e011725b623a5_313_2.png)

### Tips and Tricks

> Figure 10.21 is the perspective view with a few options turned on. It uses Shading>Wireframe on Shaded and Shading>X-Ray Joints. This shows the wireframe of all the meshes, which can help indicate where the joints of the mesh actually are, and always draws the joints on top of everything else. Note that Figure 10.21 is in the persp view panel with X-Ray turned off.

### Why?

Fingers? Why fingers and not an individual finger? A lot of this depends on the needs of a game and a model. In our game the character will generally be holding a weapon or perhaps pressing a button. This means that the index finger and thumb would need to be separately articulated, but the middle, ring, and pinky fingers would not—they would generally function as a unit. This might be different for different games: the hand would be rigged in a different way if all the fingers needed to articulate separately. But to add joints to the ring and pinky fingers would be another eight joints (per hand), or 16 added joints for the model, considering that the entire rig now is 25 joints, rigging those extra fingers is a significant cost.

- **Step 49:** Create a string of joints for the pointer finger as shown in Figure 10.22. Build this chain off the wrist from either side- or front-view panels and remember to tweak their positions in front-, side-, and perspective-view panels to get their positioning right.

- **Step 50:** Create a string of joints for the thumb as shown in Figure 10.23. Again, build off the wrist in front- or side-view panels and go back and adjust later with just the Move tool.

![](img/0285f88bc840f313779e011725b623a5_314_0.png)

![](img/0285f88bc840f313779e011725b623a5_314_1.png)

### Tips and Tricks

OK, this is actually a disclaimer. There are a lot of joints in this hand that in non-game situations would definitely be needed. If you're screaming that there are no metacarpal joints, you're right. In most higher-res situations there are a vital part of hand rigging. To make matters worse, we are leaving out joints in the thumb that are critical for hand close-ups. But for game situations on hardware today we wish to strip down to the joints we need. Five years from now, even on mobile devices we might throw joints in with reckless abandon. Today though, the compromises are necessary.

- **Step 51:** Orient upper body joints. Select AC_Back_Base (probably easiest in the Outline), then choose Animation > Skeleton > Orient Joint. The results can sometimes be a little tough to see, but see the before and after shown in Figure 10.24.

![](img/0285f88bc840f313779e011725b623a5_315_0.png)

**FIGURE 10.24** Before and after orient joint image. Notice how the joints point toward the next joint, allowing the joints to be oriented correctly.

### Why?

When placing joints, it is pretty impossible (especially through the hand) to get them in just the right place without having to go back and move them. The problem is that the orientation of the parent joint (to wherever joint is created) is defined on the first click of placement. So when the joints are later moved into their correct locations, the parent joints no longer are pointing toward the next joint, which makes for awkward animation later. The Orient Joint command (which by default orients all the children of the selected joint) tells all the joints to take a look at the next joint in their chain and point to that chain (although this isn't perfect; see the following steps). Importantly, this only affects the joint's orientation, not its rotation (as can be seen in the Channels box). This means that later, zeroing out the rotation values of the joints will return them to their neutral pose.

- **Step 52:** Examine the newly oriented joints and manually adjust any that are needed. Swap to the Rotate tool and examine the joints in the upper body. Try rotating them and seeing if the axis of the rotation handle makes sense for that joint (be sure to undo the rotation each time). For instance, the elbow will really bend only in one direction. Does rotating that joint require rotation along only one axis? If not, it should be adjusted. Figure 10.26 shows the adjustment of my wrist joint (yours may or may not require such an adjustment). To adjust the orientation first we need to be selecting by component type and be able to select what Maya deems “miscellaneous components.” The easiest way to do this is in the top shelf (Figure 10.25—take careful note of the highlighted pressed buttons). Then when a joint is clicked it will show a few floating x, y, and z letters. Activate the Rotate tool and click any of these letters to get handles to adjust the orientation. Use the Rotate tool to rotate the orientation of the joint (Figure 10.26).

![](img/0285f88bc840f313779e011725b623a5_316_0.png)

**FIGURE 10.25** Saving, orienting joint correctly.

![](img/0285f88bc840f313779e011725b623a5_316_1.png)

**FIGURE 10.26** The process of adjusting joint orientation. First, click the x, y, or z, then use the Rotate tool to rotate the orientation to desired position.

### Why?

This can be a tedious process. Hopefully, the Orient Joint function lines things up pretty well for you and there is very little manual adjustment that needs to take place. Much of it depends on how carefully the joints are organized as they are placed, but if a series of joints are even just a little out of line, Maya will tend to twist joints to try and orient toward the next, thus they need to be readjusted manually.
