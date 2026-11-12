
## Summary

In this chapter, we discussed several key aspects for creating bones and painting weights as they pertain to the iPhone and Unity iOS. This chapter discussed the usage of Blender in a modo to Blender pipeline; however, the techniques and principles discussed in this chapter can be utilized in any 3D package. We discussed the importance of the iDevice hardware and how Unity utilizes VFP-optimized skinning paths and what you need to do to make sure you take advantage of these optimizations. We also discussed the importance of bone count and making sure you utilize a maximum influence of no more than 4 bones per vertex. Finally, we took a look at Tater's skeleton as it was created in Blender and some useful weight tools such as Clean Weights and X Mirror.

In Chapter 6, we'll focus on creating additional animation controller bones and IK target bones. We'll also discuss how FBX animation is imported by Unity.

![](img/d3e3fa4010906e98ec76be003a6e31c2_138_0.png)

## Animation Using Blender

### IK and Basic Animation

In Chapter 5, we took an in-depth look at creating bones using Blender as they pertain to animating a character game asset for your Unity iOS or iPad game. In this chapter, we are going to continue where we left off with Tater and finish up his rig. We are going to look at adding constraints and IK to the Armature, and we'll also do some additional organization to the rig to make things easier when animating.

Once the rig is completed, we'll talk about creating animations for our character in Blender and exporting the animations to an FBX file for use in Unity iOS. Let's get started by completing Tater's rig by adding IK constraints.

### Tater’s Weapon Load Out

Go to the resource site to view the video walkthrough for this chapter.

## Completing the Rig: Adding IK

Usually, in larger studios, a Technical Director, or more specifically titled as a Character TD, handles rigging. It’s true, rigging a character can be a pretty difficult and technical process. However, I found that rigging is much like scripting in that at first, most, including myself, are wary of it until you actually get in there and see that while it is a technical process it has varying degrees of difficulty with some stages being much easier than others. Let's look at it this way, there's a big difference between programming an entire OS versus writing a script to rotate an object in your Unity iOS game. By that same token, there's a big difference in having to create a character rig for a feature film versus a rig that allows you to create simple run, jump, and shoot animations for your game. Yes, you want your game animations to look great and set your work apart, but you're also working with a limited number of bones and your focus is on keeping the overall broad feel of the motion versus capturing every single minute detail. The point is, your game rig, especially in regards to the iPhone and iPad, doesn't need to have hundreds of overly complex and sophisticated controls. In fact, the simpler your rig is the better. In Fig. 6.1, you can see the completed rig for Tater. In Tater's rig, there are four IK targets and four pole targets used to rotate the knees and elbows. As you can see in Fig. 6.1, there aren't many controls used to animate Tater.

![](img/d3e3fa4010906e98ec76be003a6e31c2_139_0.png)

**FIG. 6.1** In This Image, You Can See the Controls Used to Animate Tater. Notice that There Aren't Many Controls to Deal With.

Let's examine the controls for the rig. First, we'll start with the feet and legs, which have a total of five controls as shown in Fig. 6.2.

In the feet, I have the IK target for the legs. The Foot Controller allows me to pick up Tater's foot and rotate it at the ankle as shown in Fig. 6.3. The Foot Bone is set up to allow Tater to raise his heel as shown in Fig. 6.4. The Toe Bone is used to articulate the toes as shown in Fig. 6.5.

Finally, I have the knee controls, which allow me to point the knees as shown in Fig. 6.6. These controls are Pole Vectors set on the IK Constraint.

![](img/d3e3fa4010906e98ec76be003a6e31c2_140_0.png)

**FIG. 6.2** Here You Can See the Controls for the Feet.

![](img/d3e3fa4010906e98ec76be003a6e31c2_140_1.png)

**FIG. 6.3** The Foot Controller Bone Is the Main Control for the Foot.

![](img/d3e3fa4010906e98ec76be003a6e31c2_141_0.png)

**FIG. 6.4** The Foot Bone is Used to Raise the Heel. Notice that its Direction Has Been Flipped.

![](img/d3e3fa4010906e98ec76be003a6e31c2_141_1.png)

**FIG. 6.5** The Toe Bone Allows You to Articulate the Tip of the Boot.

As you will see in the next section, setting up these controls for the feet and legs was actually a simple task, yet I'm getting a lot of articulation. These controls allow me to move the leg, animate toe taps, stomp the heel, and position the knees as well as when used together to help create a good articulation in run and walk cycles.

Next, let's take a look at the arms. The arms have an IK target as well. The Hand Bone is constrained to the IK target so that it drives the translation and rotation of the hand, and I can hide the actual Hand Bone. Basically, by removing the Hand Bone as a control, I have one less control to worry about and a cleaner rig. I then have an elbow control, which is also a Pole Vector on the arm's IK Constraint just as with the legs. This allows me to position the elbow as shown in Fig. 6.7.

![](img/d3e3fa4010906e98ec76be003a6e31c2_142_0.png)

**FIG. 6.6** The Knee Bone Is Set as the Pole Target in the IK Constraint for the Leg. It Allows Me to Point the Knee.

![](img/d3e3fa4010906e98ec76be003a6e31c2_142_1.png)

**FIG. 6.7** The Elbow Bone Is Set as the Pole Target in the IK Constraint for the Arm. It Allows Me to Position the Elbow.

Finally, I have a Shoulder Bone, which allows me to move the shoulders to help in animation involving the arms as well as performing tasks such as shoulder shrugging as shown in Fig. 6.8.

![](img/d3e3fa4010906e98ec76be003a6e31c2_143_0.png)

**FIG. 6.8** In This Image, the Clavicle Bones Were Rotated to Produce a Shoulder Shrug.

The final controls on the rig are covering the centerline of Tater’s body. There is a Pelvis Bone for controlling the hips as shown in Fig. 6.9. There are two Spine Bones and a Head Bone for articulating the upper body such as twisting as shown in Fig. 6.10.

![](img/d3e3fa4010906e98ec76be003a6e31c2_144_0.png)

**FIG. 6.9** The Pelvis Bone Is Used to Control the Hips.

![](img/d3e3fa4010906e98ec76be003a6e31c2_144_1.png)

**FIG. 6.10** The Bones Located at Tater's Centerline Are Used for Twisting the Body.

Now that we’ve discussed an overview of the rig, let’s now take a look at how these controls were created. We’ll start with the legs.

## Setting Up IK for Legs

The first thing I needed to do was to add another bone to the foot area that would act as the main controller for the leg and foot. I selected the tail of the Foot Bone and aligned the 3D Cursor to the tail by using Shift + S and choosing Cursor to Selected. I then added a new bone called CTRL_Foot.L from this position as shown in Fig. 6.11.

Next, I needed to create a bone called IK_Foot.L that will be used as the IK target when using the IK Constraint. This bone is created from the ankle as well. In Fig. 6.12, you can see the correct position for IK_Foot.L.

**FIG. 6.11** Here You Can See the Bone that Controls the Foot’s Location and Rotation.

![](img/d3e3fa4010906e98ec76be003a6e31c2_145_0.png)

**FIG. 6.12** Here You Can See the Correct Position for the IK Target Bone for the Foot.

![](img/d3e3fa4010906e98ec76be003a6e31c2_145_1.png)

> *When creating bones in Blender, it's important to adopt the .L and .R naming convention so that you can use the Copy Pose and Paste Pose functions.*

Once these controller bones were in place, I could then start setting up the relationships. I needed to switch the direction of the Foot Bone heel by
