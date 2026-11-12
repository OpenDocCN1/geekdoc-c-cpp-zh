
![](img/d3e3fa4010906e98ec76be003a6e31c2_118_0.png)

FIG 5.10 Here the Quality Was Set to 4 Bones and Skin Normals Is Activated

## Rigging Tater in Blender

This section will be devoted to creating a rig in Blender. Again, this is not going to be a step-by-step tutorial. There are entire books devoted to character rigging and animation, and it's a very deep topic. Instead, the focus of this section will be to provide you with the information that's specific to creating a rigged character for Unity iOS and a project targeted for the iDevices. Depending on your game, your rig or characters could be much different than mine, and it will be more helpful to detail the important aspects of rigging and how it relates to the iPhone and Unity iOS.

### iPhone and iPad Rigging Essentials

Just as with vertex count, with bones you need to subscribe to the concept of 'less is more.' You need to reduce the amount of bones used per character. For example, the Unity iOS manual suggests that you don't use more than 30 bones. For example, the skeleton that was built for Tater contains 21 bones as shown in Fig. 5.11.

The goal is to reduce the level of complexity of your rig, yet still be able to perform the animations determined for the character. For instance, Tater's hands were modeled into fists, and there's definitely no need to create bones for each individual finger. Notice in Fig. 5.12 that the hands consist of only one bone.

FIG 5.11 The Image Shows the Basic Skeleton for Tater.

![](img/d3e3fa4010906e98ec76be003a6e31c2_119_0.png)

Adding bones to the Blender Armature that you’re not using to deform the mesh results in a pointless performance hit. You don’t want to include these bones in the Vertex Groups so you can simply tell them to not deform the mesh by disabling the Deform option in the Bones Properties as shown in Fig. 5.13. This essentially removes any influence for the bone. As you will see in Chapter 6, we will tell any controller bones used for IK and constraints to not influence the mesh by disabling the Deform option for these bones. When I first started using Blender, I was thrown off by the fact that bones are not considered objects themselves. They are in fact components of the Armature object and all rigging should be done with bones and constraints contained within one Armature. With Maya or 3ds Max, you can constrain or parent bones to Curves or other objects; however, with Blender, this can cause dependency issues. Instead, any control objects for IK or constraints are done with bones in the Armature object. Because of this, you need to make sure that the controller bones you create are just used for constraints and IK. You need to make sure that these bones are not influencing the vertices of the mesh. Again, the easiest method is to just tell the controller bone to not influence the Vertex Group or weighting by disabling its Deform option.

![](img/d3e3fa4010906e98ec76be003a6e31c2_120_0.png)

However, another good option for controlling bone influence on a vertex is by using the Clean Weight tool, which can be found on the Tool Shelf (T-key) while in Weight Paint mode as shown in Fig. 5.14.

The Clean Weight tool will remove vertices with low weights from the current group and will essentially remove the bone from influencing the mesh. This tool is helpful for controlling how many bones are influencing a particular vertex. Remember, in Unity iOS and most game engines for that matter, we can't have a bone influence of more than 4 bones per vertex. This tool can help pick up any stray bones that are affecting a particular vertex with only a small weight value, which may make it hard to detect while painting weights.

Now that we've discussed the essential principles for creating bones, we'll now look at creating some bones for Tater as well as painting weights. Remember, there are some key points to consider when building your rig. Be sure to reduce the amount of bones. Only use what is absolutely necessary, and don't exceed more than 30 total bones. Also, be sure to reduce the maximum influence of bones to no more than 4 per vertex.

![](img/d3e3fa4010906e98ec76be003a6e31c2_120_1.png)

Finally, be sure to disable bones that are used for IK and constraints, as you don’t want these bones to influence the mesh. In Fig. 5.15, you can see a chart that shows these key points.

### Creating the Basic Skeleton

During the modeling phase of Tater, he was built in the classic “T-Pose” for the purpose of rigging the character as shown in Fig. 5.16.

It’s important to point out that the arms and legs were pre-bent for the purpose of applying IK to the bones that make up the arm and leg chains as shown in Fig. 5.17.

The reason being is that this pre-bend in the joint areas gives the IK Solver a preferred angle to work with when calculating the bone rotations.

There are many different ways to go about creating a skeleton for a character. In this section, we’re going to discuss building the basic skeleton and then applying skin weights to that skeleton. In Chapter 6, we’ll discuss adding extra bones, which will serve as animation controls and IK targets. The manner in which you create a skeleton for your character is completely up to your project requirements and the level of animation needed for your character. For the book’s demo app, Tater will need to have basic animation cycles such as run, walk, and shoot. It’s important to state that a lot can be achieved through a simple skeleton layout. As with all aspects of game development, it comes down to a delicate balance

![](img/d3e3fa4010906e98ec76be003a6e31c2_121_0.png)

FIG 5.14 The Clean Weight Tool Can Be Found in the Tool Shelf in Weight Paint Mode.

![](img/d3e3fa4010906e98ec76be003a6e31c2_121_1.png)

FIG 5.15 Here You Can See a Chart Showing the Key Points for Using Bones in Your Characters.

**FIG 5.17** Here You Can See that the Arms Have Been Modeled with a "Pre-bend" at the Elbows so that the Arm Bone Chains Can Be Created with This Bend.

![](img/d3e3fa4010906e98ec76be003a6e31c2_123_0.png)

From a side view, I then adjust each bone so that the tips are located on edge loops and that the bones are located near the back and curved like an actual spine to help create cleaner deformations during animation as shown in Fig. 5.21.

Next, I need to create the arm and leg bones. Now, you can create one side of the leg and arm bones and then mirror those over; however, I chose to use the Armature's X-Axis Mirror function to automatically create the bones on both sides as I work. In Fig. 5.22, you can see that with the chest bone selected and X-Axis Mirror enabled on the Armature options, I pressed Shift + E to mirror extrude the bones out for the shoulder, bicep, forearm, and hand.

Now, the shoulder bones are connected to the chest bone, which isn't what I want. In order to separate the shoulder bones, I pressed Alt + P and chose Disconnect Bone from the menu and then separated the bones as shown in Fig. 5.23.

I would like to bring attention to the placement of the arm bones as shown in Fig. 5.24. Notice that I placed the tips of the bones in the edge loops of the arms. Also notice that there is a nice "pre-bend" between the bicep and forearm to help with IK and that the tip of the bicep bone is placed near the actual elbow of the mesh to help with deformations.

![](img/d3e3fa4010906e98ec76be003a6e31c2_124_0.png)

**FIG 5.18** The 3D Cursor Is Placed in the Pelvis Region to Set the Point Where the Armature Will Be Created. Snapping the Cursor to the Grid Ensures that It Is Aligned to the Center of the Grid.

Next, I moved onto the legs. In order to use the X-Axis Mirror function of the Armature, I first extruded the first leg bone, the thigh, from the Pelvis bone and separated it using Alt + P, just as I did with the shoulder and arm bones. I then positioned the thigh in the leg and continued to mirror extrude the calf, foot, and toe using Shift + E. In Fig. 5.25, you can see the completed legs.

At this point, I needed to rename all of the bones. I used the typical naming convention of appending “.L” or “.R” to the bone name depending on the side the bone was located. This is important for painting mirrored weights and using the Copy Pose functions. I also created three Bone Groups so that I could color code the bones to indicate its orientation, i.e., bones on the left are blue, bones on the right are red, and the center are green. To create a Bone Group, select the bones in Pose Mode and click the
