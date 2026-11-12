![](bbox=[0.06, 0.12, 0.65, 0.43])

FIG 5.10 Here the Quality Was Set to 4 Bones and Skin Normals Is Activated

# ### Rigging Tater in Blender

This section will be devoted to creating a rig in Blender. Again, this is not going to be a step-by-step tutorial. There are entire books devoted to character rigging and animation, and it's a very deep topic. Instead, the focus of this section will be to provide you with the information that's specific to creating a rigged character for Unity iOS and a project targeted for the iDevices. Depending on your game, your rig or characters could be much different than mine, and it will be more helpful to detail the important aspects of rigging and how it relates to the iPhone and Unity iOS.

# ### iPhone and iPad Rigging Essentials

Just as with vertex count, with bones you need to subscribe to the concept of 'less is more.' You need to reduce the amount of bones used per character. For example, the Unity iOS manual suggests that you don't use more than 30 bones. For example, the skeleton that was built for Tater contains 21 bones as shown in Fig. 5.11.

The goal is to reduce the level of complexity of your rig, yet still be able to perform the animations determined for the character. For instance, Tater's hands were modeled into fists, and there's definitely no need to create bones for each individual finger. Notice in Fig. 5.12 that the hands consist of only one bone.