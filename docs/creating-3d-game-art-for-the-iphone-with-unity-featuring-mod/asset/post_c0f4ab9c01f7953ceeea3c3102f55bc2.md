
## Fixed-Function Pipeline

A FFP uses “fixed” or predefined functionality throughout the various stages of the pipeline, which include the command processing, 3D transformations, lighting calculations, rasterization, fog, and depth testing. You have the ability to enable or disable parts of the pipeline as well as configure various parameters, but the calculations or algorithms are predefined and cannot be changed.

## Fully Programmable Pipeline

A FPP replaces many of the “fixed” stages of the FFP with fully programmable stages. This allows you to write the code that will perform the calculations for each stage in the programmable pipeline. A FPP opens the door for enhanced shaders for your games as well as increased optimizations due to the fact that complex algorithms can be executed in a single pass on the shader and will definitely save on important CPU cycles. In Fig. 1.11, you can see a diagram of both pipelines.

![](img/d3e3fa4010906e98ec76be003a6e31c2_32_0.png)

**FIG 1.11** This Diagram Illustrates the Different Pipelines Available in OpenGL ES 1.1 and 2.0 Versions.

### Texturing

It’s very important to get your texture sizes down for the iPhone since the texture cache on board is small. The TBDR renderer is optimized to handle the texture cache efficiently, but you still must keep a close eye on your texture sizes and compress them to bring down the size. The iPhone uses a hardware compression scheme called PVRTC, which allows you to compress to 2 or 4 bits per pixel. This compression will help to reduce memory bandwidth. When you’re working out of your memory budget for textures, you’ll need to make some decisions on how to compress your textures. In Unity iOS, you can set the texture compression for your texture assets in the setting menu as shown in Fig. 1.12. However, in order for your textures to compress, they need to be in a power of 2, i.e., 1024 × 1024, 512 × 512, and so on.

Texture compression is also important since the memory on the iPhone is shared between the CPU and GPU as mentioned earlier. If your textures begin to take up most of the memory, you can quickly become in danger of your game crashing on the iPhone.

**Texture Units** With OpenGL ES 1.1, you only have two texture units (TUs) available, and with OpenGL ES 2.0, you can have up to eight texture units available. Textures need to be filtered, and it's the job of the texture unit to apply operations to the pixels. For example, on iDevices that use OpenGL ES 1.1, you can use combiners in your Unity shaders, which determine how to combine the textures together, in order to combine two textures. It helps me to think of combiners like Photoshop blending modes, i.e., add and multiply. With the 3GS, iPhone 4 and iPad, you can combine up to eight textures since you have eight texture units available.

![](img/d3e3fa4010906e98ec76be003a6e31c2_33_0.png)

**FIG 1.12** You Don’t Need to Compress Your Textures Outside of Unity iOS. Texture Compression Can Be Set per Texture in Unity iOS.

There are some performance gains to be made when only sampling one texture, as we'll discuss in the texturing chapters. For instance, instead of relying on a lightmap shader, which combines an RGB image with a lightmap via a multiply operation, you could just bake the lighting into the diffuse map and thus only need to apply one texture to your material as shown in Fig. 1.13.

![](img/d3e3fa4010906e98ec76be003a6e31c2_34_0.png)

**Alpha Operations** There are two different ways to handle transparency in your textures, which are alpha blending and alpha testing. Alpha blending is the least expensive operation on the iPhone since with the TBDR renderer, there isn't any additional memory bandwidth required to read color values from the frame buffer. With alpha testing, the alpha value is compared with a fixed value and is much more taxing on the system. In Fig. 1.14, you can see one of the iPhone shaders that ship with Unity iOS and that alpha testing has been disabled. Also, notice that the shader is set to use alpha blending instead.

**FIG 1.14** Here You Can See that the Shader Is Set to Use Alpha Blending Instead of Alpha Testing.

```shader
Shader "iPhone/Transparent/Vertex Color" {
    Properties {
        _Color ("Main Color", Color) = (1,1,1,1)
        _SpecColor ("Spec Color", Color) = (1,1,1,1)
        _Emission ("Emission", Color) = (0,0,0,0)
        _Shininess ("Shininess", Range (0.1, 1)) = 0.7
        _MainTex ("Base (RGB) Trans (A)", 2D) = "white" {}
    }
    Category {
        Tags {"Queue"="Transparent" "IgnoreProjector"="True" "RenderType"="Transparent"}
        Blend SrcAlpha OneMinusSrcAlpha
        AlphaTest Greater 0
        ZWrite Off
        SubShader {
            Material {
                Diffuse [_Color]
                Ambient [_Color]
                Shininess [_Shininess]
                Specular [_SpecColor]
                Emission [_Emission]
            }
            Pass {
                ColorMaterial AmbientAndDiffuse
                Lighting Off
                SeparateSpecular On
                SetTexture [_MainTex] {
                    Combine texture * primary, texture * primary
                }
                SetTexture [_MainTex] {
                    constantColor [_Color]
                    Combine previous * constant DOUBLE, previous * constant
                }
            }
        }
    }
}
```

Over the last several pages, we've been discussing the iPhone hardware and how it relates to Unity iOS. Now that we have an understanding of the hardware, we are at a position where we can realistically determine our game budget, as we'll discuss in the next section.

## Determining Your Game Budget

Before you can begin creating any game objects, you will need to create what I call the game budget. Your game budget outlines the standards that you will adhere to when creating content as well as coding your game. To begin, you'll need to decide what type of game you're going to create and what specific requirements this game will need. For instance, my game, Dead Bang, is a third-person shooter and is designed to be fast paced. What this means is that I need to design and optimize the game in order to maintain a frame rate of at least 30 fps, which would keep the game play running smoothly. Now that I know the frame rate I want to adhere to, I can set the frame budget, which is derived from the frame time and is the most important budget for your game. Almost all of the optimizations you do will be to adhere to your frame budget.

### Frame Rate Budget

Frame time is measured in milliseconds, so if I would like to target a frame rate of 30 fps, I would take 1000 divided by 30, which gives me a frame time of 33.3 milliseconds. What this means is that when profiling my game, I need to make sure that my frame time, which is the time it takes a frame to finish rendering is no longer than 33.3 milliseconds and thus my frame budget becomes 33.3 milliseconds. In order to determine if your game is meeting the required frame budget, you need to use the Internal Profiler. In Chapter 9, we will take a look at profiling a game in order to find areas that need to be optimized. For now, in Fig. 1.15, you can see the frametime variable in the Unity Internal Profiler within Xcode reflecting my required frame budget.

![](img/d3e3fa4010906e98ec76be003a6e31c2_36_0.png)

**FIG 1.15** You Can Use the Internal Profiler to Find Bottlenecks in Your Game.

### Rendering Budget

Next, I need to determine where I want to spend most of my time in terms of how long it takes for Unity iOS to process a frame or the frame time. For example, my game doesn't use much in the way of physics calculations, so I've determined that I can spend most of my frame time in rendering.

### Vertex Budget

In order to work out your vertex budget for individual game objects, you again need to think about the type of game you're creating. If you are creating a game that requires a lot of objects in the scene, then you'll need to reduce the vertex count per object. As I mentioned earlier, you'll want to take the base value of less than 10 K vertices per frame and distribute these vertices to what you consider to be the most important game objects. For example, you might want to give your hero character a bit more resolution in terms of vertex count while reducing the count for the enemies. This budget is subjective to your game requirements, but you can see that without understanding the constraints of the hardware, it would be impossible to create assets that run smoothly on the iPhone and iPad.

### Texture Budget

We've discussed that texture memory can take up a lot of the resources on the iPhone, and your texture budget will be the combined size of memory resources you're prepared to allocate textures in your game. You'll want to minimize how much memory your textures are eating up in your game, and there are several options for reducing the load such as using texture compression, shared materials, and texture atlases. Different devices are going to have different requirements as well. For instance, the iPad and iPhone 4 are going to need higher resolution textures since the screen size is larger, but you'll find that optimization becomes a little trickier since the iPad and iPhone are still only using the same PowerVR SGX535 GPU found in the 3GS despite having a larger screen as we discussed earlier.

### It All Sums Up

As we work through the chapters in this book, we'll take a more in-depth look at optimization at the various stages of modeling and texturing. However, the important thing to remember is that all of our budgets sum up to one factor, which is to meet the frame budget. The goal for any game in terms of
