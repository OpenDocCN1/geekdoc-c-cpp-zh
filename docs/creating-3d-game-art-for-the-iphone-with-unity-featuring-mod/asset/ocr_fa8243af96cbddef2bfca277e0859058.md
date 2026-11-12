available. Textures need to be filtered, and it's the job of the texture unit to apply operations to the pixels. For example, on iDevices that use OpenGL ES 1.1, you can use combiners in your Unity shaders, which determine how to combine the textures together, in order to combine two textures. It helps me to think of combiners like Photoshop blending modes, i.e., add and multiply. With the 3GS, iPhone 4 and iPad, you can combine up to eight textures since you have eight texture units available.

There are some performance gains to be made when only sampling one texture, as we'll discuss in the texturing chapters. For instance, instead of relying on a lightmap shader, which combines an RGB image with a lightmap via a multiply operation, you could just bake the lighting into the diffuse map and thus only need to apply one texture to your material as shown in Fig. 1.13.

![](bbox=[0.05, 0.37, 0.93, 0.56])

**Alpha Operations** There are two different ways to handle transparency in your textures, which are alpha blending and alpha testing. Alpha blending is the least expensive operation on the iPhone since with the TBD renderer, there isn't any additional memory bandwidth required to read color values from the frame buffer. With alpha testing, the alpha value is compared with a fixed value and is much more taxing on the system. In Fig. 1.14, you can see one of the iPhone shaders that ship with Unity iOS and that alpha testing has been disabled. Also, notice that the shader is set to use alpha blending instead.

Over the last several pages, we've been discussing the iPhone hardware and how it relates to Unity iOS. Now that we have an understanding of the hardware, we are at a position where we can realistically determine our game budget, as we'll discuss in the next section.

# Determining Your Game Budget

Before you can begin creating any game objects, you will need to create what I call the game budget. Your game budget outlines the standards that you will adhere to when creating content as well as coding your game. To begin, you'll