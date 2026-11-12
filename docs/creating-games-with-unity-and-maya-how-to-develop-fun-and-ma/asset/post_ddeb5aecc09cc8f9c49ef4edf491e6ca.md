
Still, remember that the idea here is that this yields dividends by having joints that are oriented in ways that make the animation cleaner with fewer axes needing to be rotated for any movement. Further, this makes it so the joints can be returned to this neutral position by entering 0 in the Rotate X, Y, and Z input fields of the Channel Box.

- **Step 53:** Swap to Object Mode and mirror from the clavicle down. Select AC_L_Clavicle and choose Animation>Skeleton>Mirror Joint.

## Tips and Tricks

The settings from last time this was done should still be there (the mirror axis along YZ and the instructions to replace L_ with R_), although if the results are not as anticipated, undo and check the Mirror Joint options.

## Facial Rig

Unfortunately, out of the box, Unity does not support blendshapes (often the preferred method of rigging the face for animation). However, if you're familiar with Maya, you know that there are several camps when it comes to facial rigs; one fairly persuasive group argues that rigging the face with joints is a flexible and powerful solution.

In Unity, this is the only solution; however, an extensive facial rig can become both a performance and time killer. If you're playing a first-person shooter and are spending a lot of time examining facial expressions, there's something wrong with the game. If you're playing a third-person game, the majority of the time is spent looking at the character's back, so again, an extensive facial rig is not called for.

Of course, in cinematic cut scenes a good facial rig can really be valuable. And in fact, great strides are being made in facial animation in games as of late (take a look at the work coming out of Rockstar Games' L.A. Noire, for example). However, in this case, our budget doesn't allow for good voice talent (and animators and programmers hardly ever provide acceptable performances) so there is no need for a very complex facial rig.

However, a bit of facial movement, especially in the jaw and eyes can help a character have a bit of life so they don't feel quite so much like a walking mannequin. So in the coming steps we will create a very simple face rig that will provide some facial articulation but keep the joint count low.

- **Step 54:** Create a two-joint chain for the jaw. Do this from the side view and build the chain from the AC_Head_Base joint. Create the first joint just in front of the ear (the hinge of the mandible) and put the second down at the end of the chin (Figure 10.27). Be sure to press Enter after creating the joint at the chin to exit the tool.
- **Step 55:** Create an eye joint. Do not grow this joint out of any extant joints (we want it to be facing straight forward), but in the side-view panel activate the Joint tool again and create one joint (click and then press Enter) in the center of the eye. In the front-view panel, adjust its location to be in the center of the eye (Figure 10.28). Rename the joint AC_L_Eye.

![](img/0285f88bc840f313779e011725b623a5_318_0.png)

**FIGURE 10.27** Creating and naming the jaw joints.

![](img/0285f88bc840f313779e011725b623a5_318_1.png)

**FIGURE 10.28** Creating the eye joint.

- **Step 56:** Make AC_L_Eye a child of AC_Head_Base.
- **Step 57:** Mirror joint for AC_L_Eye.

## Preparing the Rig for Animation

Technically speaking, the rig could now be animated (although only the joints would move, not the character). For the legs, the animation would occur via the IK chain controlled with the handle we created. For the upper body, the joints would be selected and rotated. The problem is that most of these joints are inside the mesh, making them difficult to actually grab. Maya has developed some tools to help in this. Maya allows joints to be drawn in other ways than the default three intersecting circles.

In the following steps we will change the appearance of many of the joints to make them easier to see and access. This will make animating faster and more fun.

To further optimize the animation process we are going to restrict the kinds of attributes that can be animated. Animation on a computer is really the process of setting key poses at various times (called keyframes) that the computer interpolates between; in essence Maya or Unity figures out the frames between the poses the animator defines. Moving joints and then setting keyframes and then adjusting those keyframes is what animating is. Adjusting keyframes is a pretty critical part of the process and so having a small data set that is easier to manage becomes critical.

Right now, all the joints we have created can be moved, scaled, and rotated. In reality, in realistic animation like this game calls for, the joints should really only rotate. By telling joints that they translate and scale attributes are locked, we can avoid mistakes that would cause body parts to stretch unnaturally, and allow for keyframes to be set by simply pressing S on the keyboard (more on this later).

- **Step 58:** Change AC_Root to draw as a circle. To do this select AC_Root and open the Attribute Editor (Ctrl-A if it is not open). Look to the Joint section and expand it. Change the Draw Style from Bone to Circle.

### Why?

Move the mouse to the persp view panel and press 4 on the keyboard to go to Wireframe mode. The circle is probably too small. But we can change that.

- **Step 59:** Resize the circle representing the joint. Still with AC_Root selected and still in the Joint section of the Attribute Editor, change the Radius value to 1.3. Figure 10.29 shows what the wireframe should look like.

![](img/0285f88bc840f313779e011725b623a5_319_0.png)

**FIGURE 10.29** Resized Radius of a joint with a Circle draw style

### Why?

The absolute size of the radius is subjective. The goal is to make the circle a bit wider than the pouches on his belt so that it is easy to see and grab. However it shouldn't be so big that it's always in the way of the hands. This size can be tweaked to taste.

- **Step 60:** Change AC_Back_Base and AC_Back_Small to draw as CircleXY with a Radius of 0.75. Again, the process here is to select the joint, then in the Attribute Editor, in the Joint change the Draw Style from bone to (in this case) CircleXY. Then change the Radius setting immediately beneath it (Figure 10.30).

![](img/0285f88bc840f313779e011725b623a5_320_0.png)

### Why?

Visually, simply changing this forces the direction of the drawn circle. Although the circles could remain parallel to the ground, this sometimes makes the handle difficult to see. By rotating them up on their side, they are easy to see sticking out of Aegis's back and help define a little easier what the back rotation will usually be doing.

**FIGURE 10.30** AC_Back_Base and AC_Back_Small drawn as CircleXY with radius of 0.75.

- **Step 61:** Repeat this process for the rest of the joints in the upper body. For each joint, make a choice as to which Draw Style will provide the easiest access to the circle that is going to be drawn. Or, if you'd prefer, choose something besides a circle (Figure 10.31 shows my finished setup; I used Square for the eye joints).

![](img/0285f88bc840f313779e011725b623a5_320_1.png)

**FIGURE 10.31** Completed upper body adjustments to joint Draw Styles.

- **Step 62:** Change the color of the left-side joints to blue and the right side to red. To do this, select AC_L_Clavicle and then open the Attribute Editor. Look for the Display section and the Drawing Overrides section beneath that. Click the Enable Overrides checkbox and use the Color slider to pick a pretty blue. This will change all the joints all the way down the arm (although you won't be able to see the change until you click away from the joint). Repeat this for AC_R_Clavicle and choose a red color (Figure 10.32).

**FIGURE 10.32** Colored joints.

![](img/0285f88bc840f313779e011725b623a5_321_0.png)

### Why?

Once the animation process begins, there are going to be a lot of circles floating around. Sometimes, especially when animating from the side-view panel, it can become pretty difficult to see which side that circle represents. By color coding it becomes much easier to identify joints.

- **Step 63:** Color code other upper body joints as desired. You may wish to color code all the back joints one color and the head another, and so on.
- **Step 64:** Delete unnecessary joints. There are several joints that we placed that will actually not affect the polygons: the tips of all the fingers and thumbs (AC_L/R_FingersTip, AC_L/R_ThumbTip), the jaw tip (AC_Jaw_Tip), and the head tip (AC_Head_Tip). These joints were placed to give the joints that were their parents a location to point to, but they actually serve no purpose now. By deleting these joints (now that their parents are all oriented) we can further streamline the data set.
- **Step 65:** Lock and Hide unwanted transforms. Start with AC_L_Shoulder. Select this joint and activate the Channel Box. Select the words Translate X, Translate Y, and Translate Z (not the input fields). Right-click, hold and choose Lock and Hide Selected. Next, do the same for Scale X, Scale Y, and Scale Z and Visibility (Figure 10.33).
