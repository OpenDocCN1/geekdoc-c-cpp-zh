
## Unity's Animation System

### Tater's Weapon Load Out

Go to the resource site to view the video walk-through for this chapter.

Unity iOS has a very robust animation system. It allows you to blend, mix, and add animations, as well as syncing and controlling animation playback via time, speed, and blend weights.

> Unity iOS has a very robust animation system. It allows you to blend, mix, and add animations, as well as syncing and controlling animation playback via time, speed, and blend weights.

In Chapter 6, we discussed using the Blender's Action Editor to create separate animations that can be exported to multiple FBX files. Throughout your game, you will need to play these various animation clips during various states of the game play such as when a character is running, walking, or shooting. Now, it wouldn't look too nice if these animations were abruptly changing from one clip to the next. That is why Unity iOS supports animation blending.

In Unity iOS, you can have any number of animations playing on the character and all these animations will be blended together to produce the final animation. It's exactly the same concept as using Blender's NLA as shown in Fig. 7.1 to layer Actions together to produce a complex animation sequence.

![](img/d3e3fa4010906e98ec76be003a6e31c2_175_0.png)

FIG 7.1 Blender's NLA Editor Allows You to Create Transitions between Animations and Scale and Blend Clips.

With the Unity iOS Animation System, you can smoothly transition from one animation clip to another. It's important to understand these capabilities of the Animation System so that you can build your Actions in Blender accordingly. There are basically two routes you can use in animating your character.

### Route 1

Route 1 is to create each animation separately. For instance, let’s say your character will need to be able to perform a run, walk, and a shooting action. What I mean by creating each animation separately in this case is that you’ll not only need to create the run and walk actions but you also have to create a walk-shoot and run-shoot action. While you’re at it, you’ll also need an idle animation, which means you then have to create an idle-shoot animation as well. So, in order to adequately produce the three actions, that is, walk, run, and idle with a shooting action, you’ll also need to create another set of these animations containing the shooting action as well. This brings you to a total of six animations you’ll need to create for only three actions the character will be performing as shown in the diagram in Fig. 7.2.

![](img/d3e3fa4010906e98ec76be003a6e31c2_176_0.png)

FIG 7.2 This Image Shows How Three Actions Can Mean Creating Six Separate Animations.

As you can see, even with a simple character with three actions plus shooting, you are already doubling the amount of work in terms of animation. Animation is fun, but it’s not that fun. The solution to this issue can be found by heading down route two.

### Route 2

In this route, you will only need to create the three actions plus the shooting action that your character needs to perform. The reason being is that you can take the shoot animation and additively blend that action with another such as the run animation as shown in Fig. 7.3.

As stated earlier, the blending of animations can be done within Unity’s Animation System. You can set the blendMode using the AnimationState Interface. In Fig. 7.4, you can see the AnimationState has a variable for setting the blendMode. We will discuss this in depth in a moment. For now, just know that the blending will take place at run time.

**FIG 7.3** This Image Shows That by Using Blended Animations You’ll Only Need to Create Four Actions in Total.

![](img/d3e3fa4010906e98ec76be003a6e31c2_177_0.png)

![](img/d3e3fa4010906e98ec76be003a6e31c2_177_1.png)

**FIG 7.4** This Image Shows You a List of Properties for the AnimationState Class. Notice That the AnimationBlendMode Can Be Set to Additive.

In this chapter, we’re going to exclusively look at creating animations for the purpose of additively blending them in Unity iOS and we’ll start with Blender’s NLA Editor.

## Creating Animations Using Blender’s NLA Editor

In Chapter 6, we talked about using the Action Editor to create different animations and then exporting an Action for export to separate FBX files using the “model@action.fbx” notation. In this chapter, I’m going to introduce you to

![](img/d3e3fa4010906e98ec76be003a6e31c2_179_0.png)

In Unity iOS, all the bones are regarded as Transforms. This allows you to manipulate each bone just as you would any other object in Unity iOS.

In Blender, I'll still need the weapon attached to the character in order to animate the action correctly. What I did was to parent the weapon to Tater's IK_Hand.L Bone using a ChildOf constraint as shown in Fig. 7.6.

Notice that the constraint matches the location and rotation of the gun to the IK_Hand.L Bone. This is exactly what we'll be doing in Unity iOS. There are different ways to set this up in Unity iOS, but I just utilized Thumper's Pivot as it was originally set in modo to correctly attach Thumper to Tater's hand as shown in Fig. 7.7. In Fig. 7.8, you can see that you can work with pivots in Unity iOS by enabling Pivot mode in the Editor.

In Unity iOS, I attached a simple script to Thumper to parent it to the hand. The script takes a variable of type Transform, which represents the IK_Hand.L Bone in the mesh. In the script, the gun's Transform is then parented to the hand, and its local rotation is set to Quaternion.identity, which aligns it to the parent axes. The local position is set to zero via Vector3.zero. Finally, I offset the Euler angles by -80 on the Y-axis and -90 on the Z-axis in order to properly line up the gun to the hand bone like it was in Blender as shown in Fig. 7.9.

FIG 7.6 The Gun Was Parented to the IK_Hand.L Bone Using a ChildOf Constraint.

![](img/d3e3fa4010906e98ec76be003a6e31c2_179_1.png)

FIG 7.7 Here You Can See the Pivot Point That Was Seen in Modo.

![](img/d3e3fa4010906e98ec76be003a6e31c2_180_0.png)

FIG 7.8 The Poses Set on Your 3D Objects Are Available in Unity by Enabling Pivot Mode in the Editor.

![](img/d3e3fa4010906e98ec76be003a6e31c2_180_1.png)

FIG 7.9 Here You Can See a Script That Offsets the Rotation of the Weapon Using rotation.eulerAngles.

With this setup, you can replace the weapon when needed. As long as the pivots in different weapons match position and they’re relatively the same size in regards to how the character is going to hold the weapon, this workflow works well.

### Using the NLA Editor

Now that we've discussed how to handle weapons so to speak, we'll continue on with discussing the NLA Editor. The NLA Editor is used to mix and blend Actions to create complex animations. Let's look at an example of creating a shoot while running animation. In Figs. 7.10 and 7.11, you can see the run and shoot animations that were created for Tater.

It's hard to tell from the images, but the shoot animation has no keys set on the legs. By clicking the plus sign in the Action Editor, I created a new Action that starts with the bones in position from the previous Action's pose as shown in Fig. 7.12. However, the keyframes are removed in the new Action. I then keyframed a shooting animation and renamed this action to shoot.

Using the NLA Editor, you can then work with your animations as strips as they're called. It's much like using a video editor in that you can add strips or clips to a track and blend and transition between them. In our case, we just want to layer the shooting animation over the run, and this is done by placing the shoot track above the run and changing its blending mode to Add as shown in Fig. 7.13.

![](img/d3e3fa4010906e98ec76be003a6e31c2_181_0.png)

![](img/d3e3fa4010906e98ec76be003a6e31c2_182_0.png)

FIG 7.11 This Image Shows the Stride Action

![](img/d3e3fa4010906e98ec76be003a6e31c2_182_1.png)

FIG 7.12 The New Action Starts with the Bones in the Previous Action's Pose
