![](bbox=[0.056, 0.114, 0.866, 0.478])

**FIG 7.19** In This Image, You Can See That the Layered Animation in Blender Was Reproduced in Unity iOS Using an Animation Blending Just as Was Done in Blender in the NLA Editor.

# ## Using Dynamics in Blender to Animate Objects

In this section, we're going to take a look at the process of using the Bullet Physics Engine to create some procedural animation. In the book's demo app, you play as Tater running through his training facility shooting targets. The target, as shown in Fig. 7.20, is a simple wood board with a spray painted zombie face. Be sure to notice Tater's artistic talent with a spray can! The animation goal for this object is to explode into pieces when it's hit from a blast from Thumper as shown in Fig. 7.21.

Using physics can be great for this type of effect. The process covered in this chapter will "bake" the physics simulation from Blender into keyframes, which will then be played in Unity iOS from the FBX file. However, it's important to note that using this method can be heavier on GPU side. That's not necessarily a bad thing, as we've discussed throughout the book, you'll need to profile your game for potential bottlenecks. With newer hardware, the CPU on the iDevices are becoming more capable than the GPU, which means if your game is already heavy on rendering, this method might not be the best solution. To compliment this section, in Chapter 9, we'll discuss creating the same explosion effect in Unity iOS using a physics simulation,