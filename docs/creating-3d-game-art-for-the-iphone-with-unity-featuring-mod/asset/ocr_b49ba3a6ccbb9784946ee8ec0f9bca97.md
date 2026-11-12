300 vertices and shares the same material as the rest of the level. This allows me to place tons of these items randomly throughout the level without the cost of an additional draw call. These props are very easy to create. The barrel is a simple cylinder, and the boards are just boxes. The difficult aspect about creating a level like this isn't in the modeling stage, as the techniques used to model the assets are not advanced by any means.

# ## Creating a Skybox

A skybox is used to create an atmosphere for your level. A skybox is typically created using a box and uses a cubemap to apply a sky texture. This is a proven technique as it provides the least amount of distortion and wastes as little texture space as possible. I use CG Textures for downloading textures for my models and used the site for all the content created in this book. You can download textures for free up to 15 MB a day at http://www.cgtextures.com.

From CG Textures, you can download any sky texture in the cubemap format. The cubemap provided is in a strip format, so I use an excellent program called Pano2VR, for converting the file to a proper cubemap that would map perfectly with the automatically created UVs for a default box in modo. Pano2VR is available on both the Mac OS and PC and I use it often for creating environment maps. You can find more information about Pano2VR at http://gardenhomesoftware.com/pano2vr.php.

With that said, I found that I couldn't seem to get the quality in the sky that I wanted using a cubemap. With the cubemap, I was wasting a lot of empty space in the map, and the UVs for the box mesh wasn't utilizing the entire image map, which was causing a lot of pixelation. In Fig. 4.19, you can see the cubemap skybox and the wasted pixels.

FIG 4.19 The Wasted Pixels in the Cubemap Are Shaded Yellow

![](bbox=[0.09, 0.6, 0.48, 0.92])

So, I decided to go with a six-sided cylinder in order to minimize the seams the actual box method was causing. With the cylinder, I was able to perform a simple cylindrical unwrap and then scale the UVs so that they covered the entire 0-1 space, which in turn would utilize all of the pixels in the map. The next step was to create a sky map that expanded to all sides of the image. I jumped back to Pano2VR and used the Transformation tools to export a Mirror Ball format. Lastly, I imported the file into Photoshop and used the Distort > Polar Coordinates filter set to Polar to Rectangular, which produces a specific unwrapping that would fit my texture map needs. In Fig. 4.20, you can see the final map that was created and cropped to 2048 x 2048 for use in Unity iOS.