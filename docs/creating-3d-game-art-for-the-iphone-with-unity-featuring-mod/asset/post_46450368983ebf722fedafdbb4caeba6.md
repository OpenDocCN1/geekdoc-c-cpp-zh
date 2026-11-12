
![](img/d3e3fa4010906e98ec76be003a6e31c2_93_0.png)

**FIG 4.8** This image shows what areas are visible to the player.

## Creating the Level

In these last sections, we've covered the importance and reasoning behind breaking our level down into sections. You can now see how this type of level design can have a dramatic impact on the scene's performance. Now, we'll move on to looking at some practical examples as I illustrate the process in creating Tater's Training Yard.

### Determining the Vertex Count

Determining a proper vertex count is always an important step in the design process of your level. This budget should always be worked out before any modeling is started. In Chapter 2, we discussed creating a performance test scene using the Penelope tutorial elements provided by Unity Technologies. We don't need to cover this again, but I just wanted to reiterate the importance of testing performance and determining budgets before any actual modeling is done. It can be very detrimental to your project to realize late in the game that your models have been created with too much resolution. When this happens, you're forced to make several difficult decisions as to what other aspects of your game will need to be sacrificed to compensate.

> *It can be very detrimental to your project to realize late in the game that your models have been created with too much resolution. When this happens, you're forced to make several difficult decisions as to what other aspects of your game will need to be sacrificed to compensate.*

As you will recall from Chapter 2, using the test performance scene, we were able to gauge a working vertex count. We will use this vertex count as a base to follow. Again, it's not the ultimate answer that we stick to no matter what happens in our game as many factors come into play, which affect our frame rate such as script performance, texture memory, and physics calculations. However, it's very helpful to have a base number to work toward when creating models. Without this base, we'd essentially be modeling in the dark so to speak.

### Further Testing

I mentioned earlier in the "What Can Reasonably Be Accomplished" section that I performed some testing with transparency before committing to a solution in the model. Again, I definitely want to reiterate that it's always easier to realize device limitations and that a particular idea won't work in the design phase rather than the finished model phase.

> *It's always easier to realize device limitations and that a particular idea won't work in the design phase rather than the finished model phase.*

As previously mentioned, the iPad and iPhone 4 can suffer from fill-rate issues. As discussed in detail in Chapter 1, this is largely due to the fact that it's using the same 256 MB RAM and SGX 535 GPU as the iPhone 3GS to render to displays that are higher resolution. Knowing this up-front, which is another reason it pays to have a thorough understanding of the different iDevice hardware, urged me to test the transparency capabilities on the iPad and iPhone 4 before I committed to creating the chain-link fences using an alpha shader.

In Fig. 4.9, you can see the simple test scene I used to test the transparency shader and fill rate on the iPad and iPhone 4.

The scene has several of the chain-link fence polygons with a shader using alpha testing. Now, I'll also mention that using a shader that performs alpha testing can be quite expensive on the iDevices, so again, this is a good opportunity to test it up-front. The test is simple: install the scene on the iPad and iPhone while using the Internal Profiler to monitor the frame rate as I fill the entire screen with the transparent polygon. I also used the controls to quickly move in and out and around the transparent polygons as the screen goes from being filled to semi-filled with the transparent polygons. I did this to try and "stress" the iPad and iPhone 4 as the GPU is being tasked with drawing the polygons. Checking the Internal Profiler's output over a period of time didn't indicate any major issues. Once the entire level was complete with all of the textures and geometry in place, I still found that the alpha test shader was still performing well with only a 1 or 2 millisecond drop.

**FIG 4.9** This Scene Was Used to Test Fill-Rate Issues on the iPhone 4 and iPad.

![](img/d3e3fa4010906e98ec76be003a6e31c2_95_0.png)

![](img/d3e3fa4010906e98ec76be003a6e31c2_95_1.png)

**FIG 4.10** An Example of a Texture Atlas.

## Using Texture Atlas

Using texture atlases in your projects are a great way to increase texture optimizations and keep artwork consistent across multiple objects. In Fig. 4.10, you can see the texture atlas that was built for Tater's Training Yard level.

Texture memory is vital on the iPad and iPhone 3GS and can often be the main culprit behind low performance and crashes. With the iPhone 4, you have double the amount of memory at 512 MB, but you still need to keep your texture usage as optimized and efficient as possible. This is where the usage of a texture atlas comes into play. A texture atlas is a single image that acts as a container, which houses the coordinates for several smaller image sections through which multiple objects can target.

The result is that several objects can use the same texture and thus minimize the number of textures that need to be loaded in your scene. By using a texture atlas, you fit the textures for the entire level into one image map. This can dramatically increase the performance of your game by using less memory for textures. In Fig. 4.11, you can see how the objects in my level target the different areas on the texture atlas.

![](img/d3e3fa4010906e98ec76be003a6e31c2_96_0.png)

Any empty space in your texture atlas is a missed opportunity for adding detail in your game.

**FIG 4.11** This Image Shows the Relation Between the Level Texture Atlas and the Actual Models.

Using a texture atlas is best utilized when "Building on the Grid," as we'll discuss in the next section. Building your textures on a grid allows you to optimize the atlas so that it's as efficient as possible, utilizing every single pixel in the image. The main thing to remember with texture atlases is that any empty space in your atlas is a missed opportunity for adding detail in your game. The image is going to be loaded in your game so you might as well make sure that every pixel counts.

## Building on the Grid

Building on the grid is a technique common to level creation in games. It's the process of building your objects into tiles or puzzle-like pieces so that they can be snapped together in a seamless fashion to build a level. The grid comes into play as the tiles are built on a grid-based or predetermined sizes such as 256 × 256 or 512 × 512 as shown in Fig. 4.12.

Building on the grid is very efficient for building levels. Let's take a look at three important reasons. First, you get a consistent texel density as the mesh size in 3D space matches the texture on the grid in pixels. For instance, in my level, you can see that the ground mesh is created from tiles that are 512 × 512 units, and these mesh tiles directly relate to a portion of the texture atlas that is also 512 × 512 in pixels as shown in Fig. 4.13. I'll also note that this portion of the texture atlas that represents the ground occupies 512 × 512 pixels of the 1024 × 1024 pixel image. The ground portion is seamless on all sides so that it can easily be tiled. Also note that the ground texture is in a power of two format as well as the level texture atlas. However, I can create texture areas in the texture atlas that are not a power of two, but because they are contained within the power of 2 texture atlas, they can still be compressed using PVRTC compression. If you look back to Fig. 4.12, you can see that the board textures are not in a power of 2.

![](img/d3e3fa4010906e98ec76be003a6e31c2_97_0.png)

**FIG 4.12** This Image Shows the Texture Atlas Divided into Tiles and the Resolutions the Tiles Relate To.

The second reason is that there's no wasting of resolution in the game as building on the grid helps you to place texture resolution appropriately. For instance, let's say you have a doorway mesh that's only 128 × 256 units in size in 3D space. It would be a huge waste to map a 1024 × 1024 pixel image to this mesh. Building on the grid helps you to work

![](img/d3e3fa4010906e98ec76be003a6e31c2_97_1.png)

**FIG 4.13** The Ground Is Made into a Tile of 512 × 512 and Is Mapped to a Texture Tile of 512 × 512 in the Texture Atlas.
