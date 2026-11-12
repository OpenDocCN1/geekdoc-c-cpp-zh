
out the unit to pixel ratio so that you can be assured that your mapping and texture resolution is as efficient as possible.

Now, using Mip maps can help with texture memory as their purpose is to replace a texture with a lower resolution copy of the image the further the camera is away from that texture. However, you get the side effect of having blurry textures in your scene, which I really don't like. If you're working on the grid, you can manually create this effect by being sure that your meshes are using only a specific and proportional section of the texture atlas. Again, you're not wasting any resolution, and the texture coordinates map to the specific area of the atlas, which directly relates as a 1 to 1 relationship between the mesh size in units and the texture size in pixels.

Finally, the third reason is that objects can be tiled. You can make new and different configurations of objects via connecting the tiles, which results in objects being part of a reusable library of elements as was shown in Fig. 4.4.

## Does It Make Sense to Use the Grid?

When creating Tater and Thumper, we didn't use the grid. Not every object in your game makes sense to build on a grid. Organic type models don't work too well using the grid methodology. Again, we have to come back to every game being different and having its own set of requirements. It helps to know the different methodologies available so you can make the appropriate decisions for your own projects. The one thing that's common to all game projects is optimization. You need to always be thinking about the best ways to optimize your graphics, and building on the grid is just another way to help you accomplish this task.

## Determining Working Texture Size

So, we've talked about building on the grid, but we really haven't gotten into the particular process. To begin, we need to determine a working texture size that will be used in modo to establish our ratio between units in 3D space to pixels in our texture atlas. In Chapter 2, I mentioned that our Unit System in modo was set to Game Units and the Meters per Game Unit setting was set to 1.0. This means that we've determined that 1 square in modo's Grid and Workplane is equal to 1 unit. For building on the grid, we need to take this one step further and create another relationship between the grid and the Game Unit Setting in modo. We need to assign, in a theoretical sense, a texture resolution to a game unit. For example, I chose 128 pixels as my working texture size, which means I will now think of each game unit/meter in modo as representing 128 pixels. That is to say, in modo, I can reference my working texture size as 128 pixels per meter. Let's look at an example to illustrate this relationship. In Fig. 4.14, you can see that I have a single ground polygon selected, and with the Dimensions tool active, I can see this polygon is 4 × 4 game units or 4 × 4 m. If I take 128 times 4, I will get 512, which as you can also see in Fig. 4.14 is the exact size in pixels that the ground texture contains in the level texture atlas.

![](img/d3e3fa4010906e98ec76be003a6e31c2_99_0.png)

![](img/d3e3fa4010906e98ec76be003a6e31c2_99_1.png)

You can now see that the single ground polygon is created to match the texture resolution, and a 4 × 4 m polygon equals 512 pixels in my texture map. This relationship between units in modo to pixels in my texture exists simply because I set it up that way. There isn't a setting in modo to change other than being sure that I have set the Meters per Game Unit to 1.0. The relationship between the game units and pixels is arbitrary and something that I determined on my own, based off my own project requirements.

So how did I determine that 128 pixels is what I'd use for my working texture size? To answer this question, we need to look back to the hardware. On the iDevices, we can use up to a texture size in pixels of 2048 or 2 K. Now this is on the iPhone 3GS, iPod Touch third generation and up as it specifically relates to the support of OpenGL ES 2.0. I will typically use a maximum texture resolution of 1 K (1024 × 1024 pixels) as I've found it to be a good base resolution for the higher resolution iPhone 4 and iPad screens yet can easily be downsized for 3GS. So that leaves us with anywhere from around 64–1024 pixels that we can use as our working texture size. From there, I determined that 128 would be a good base number to start with. Again, there's not an exact formula, but something that you determine yourself. I could have easily used 256 and made each of my ground polygons 2 × 2 m, but when modeling, it was easier to use a 4 × 4 size.

## Creating the Ground

Now that I have a working texture size and have determined that each ground polygon will be exactly 4 × 4 m or game units in size, I can begin to layout the ground polygons. To start, the entire model is built into one mesh item.

![](img/d3e3fa4010906e98ec76be003a6e31c2_102_0.png)

FIG 4.17 The Gates Were Exported as a Separate Mesh.

![](img/d3e3fa4010906e98ec76be003a6e31c2_102_1.png)

FIG 4.18 The Props Will Be Randomly Distributed in the Level in Unity iOS.

300 vertices and shares the same material as the rest of the level. This allows me to place tons of these items randomly throughout the level without the cost of an additional draw call. These props are very easy to create. The barrel is a simple cylinder, and the boards are just boxes. The difficult aspect about creating a level like this isn't in the modeling stage, as the techniques used to model the assets are not advanced by any means.

## Creating a Skybox

A skybox is used to create an atmosphere for your level. A skybox is typically created using a box and uses a cubemap to apply a sky texture. This is a proven technique as it provides the least amount of distortion and wastes as little texture space as possible. I use CG Textures for downloading textures for my models and used the site for all the content created in this book. You can download textures for free up to 15 MB a day at http://www.cgtextures.com.

From CG Textures, you can download any sky texture in the cubemap format. The cubemap provided is in a strip format, so I use an excellent program called Pano2VR, for converting the file to a proper cubemap that would map perfectly with the automatically created UVs for a default box in modo. Pano2VR is available on both the Mac OS and PC and I use it often for creating environment maps. You can find more information about Pano2VR at http://gardenhomesoftware.com/pano2vr.php.

With that said, I found that I couldn't seem to get the quality in the sky that I wanted using a cubemap. With the cubemap, I was wasting a lot of empty space in the map, and the UVs for the box mesh wasn't utilizing the entire image map, which was causing a lot of pixelation. In Fig. 4.19, you can see the cubemap skybox and the wasted pixels.

FIG 4.19 The Wasted Pixels in the Cubemap Are Shaded Yellow

![](img/d3e3fa4010906e98ec76be003a6e31c2_103_0.png)

So, I decided to go with a six-sided cylinder in order to minimize the seams the actual box method was causing. With the cylinder, I was able to perform a simple cylindrical unwrap and then scale the UVs so that they covered the entire 0-1 space, which in turn would utilize all of the pixels in the map. The next step was to create a sky map that expanded to all sides of the image. I jumped back to Pano2VR and used the Transformation tools to export a Mirror Ball format. Lastly, I imported the file into Photoshop and used the Distort > Polar Coordinates filter set to Polar to Rectangular, which produces a specific unwrapping that would fit my texture map needs. In Fig. 4.20, you can see the final map that was created and cropped to 2048 × 2048 for use in Unity iOS.

![](img/d3e3fa4010906e98ec76be003a6e31c2_104_0.png)

FIG 4.20 This Is the Final Map I Created for the Sky, Which Doesn't Waste Any Texture Space.

## Creating the Trash Heap

Next, I'd like to talk about the heaps of trash surrounding the level. The trash heap is also very basic in terms of modeling. The process for creating the geometry was to simply create a mountain from as few polygons as possible. Again, I will use a max-smoothing angle to remove the facets in the polygons. This item will target a different texture atlas than the level. For this model, the UV layout was the key to creating a successful look. To create the UV map, I cut the UVs down into sections. I made sure that each section was proportional to each other so the texture would be a consistent size across the mesh. The UVs were overlapped and placed in the upper area of the 0-1 space. The bottom half is reserved for the target object that will be discussed in Chapter 7.

I used Luxology's ImageSynth 2.0 program to create all of the seamless textures for my maps. I went to CG Textures and downloaded several junk and trash yard photos, and using ImageSynth, I compiled a seamless texture that was used for mapping the geometry.

In Fig. 4.21, you can see the completed trash heap model. Notice that the trash heap texture uses a seamless texture in the top half of the texture atlas.
