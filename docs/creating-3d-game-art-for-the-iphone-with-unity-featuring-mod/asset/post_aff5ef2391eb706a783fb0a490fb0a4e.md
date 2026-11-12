
![](img/d3e3fa4010906e98ec76be003a6e31c2_105_0.png)

FIG 4.21 Here is the Trash Heap Model, Which Surrounds the Level.

## Texturing the Level

In this section, I want to talk about how the texture atlas for the level was created. We are going to look at how to measure the scene to determine texture size as well as creating UVs. I mentioned earlier that the entire level was created as one mesh item and then was later broken down and exported into separate objects. This made it much easier for me to create the UVs, and as I broke down the level into sections, the UV maps created were also copied. This meant that the coordinates would still line up correctly even though the sections were now saved into separate FBX files.

### Measuring the Scene

The first step is to measure the scene to determine the size. As mentioned earlier, I used the Dimensions tool, selected the polygons to get the measurement, and then multiplied this by my working texture size. Remember, my working texture size was 128 pixels so selecting a wall tile displayed a 4 x 4 size, which equals to 512 pixels (128 times 4) in the texture map. I then measured all of the items in the scene and kept note of the size they would need to relate to in the texture map.

### Creating the Textures

Before creating any UV coordinates, I created the texture atlas. This is a bit backwards from the way Tater and Thumper were created. As previously mentioned, I used CGTextures to download all of the texture reference I needed for the level and then used my measurement outline to build the texture atlas to the correct size specifications. The goal here is to use every pixel in the image and have each pixel mapped to an object. This stage is more difficult than the modeling since you have to logically work out a way for the textures to all fit in the map, yet retain the correct size. For instance, you can see in Fig. 4.22 that with my texture atlas, I've wasted some space when creating the textures for the barrel. This isn't going to ruin me, but it's not as optimized as it should be.

![](img/d3e3fa4010906e98ec76be003a6e31c2_106_0.png)

FIG 4.22 The Highlighted Areas Show Wasted Texture Space.

### Creating UVs

Once the texture map is complete, I then import this texture into modo and set the UV window to show the image. Now, while I create the UVs, I can use the image map as a guide to line up the coordinates to the image. Again, it's backwards to the way you'd usually work with UVs, but it also makes the UV layout process simple. In Fig. 4.23, you can see the UV map that was created and how it relates to the texture atlas.

![](img/d3e3fa4010906e98ec76be003a6e31c2_107_0.png)

### Lightmap UVs

For this level, I used lightmapping extensively, and I needed to be sure that I created a UV map that contained coordinates that didn't overlap. Nonoverlapping UVs is the key to creating a UV layout that is correct for lightmapping and that is to say that the current UV map won't do the trick. Not to worry, creating UVs for lightmapping is by far the easiest stage in the entire process. While still working under the single mesh for the entire level, I created a new UV map, which now leaves me with two UV maps for the mesh. The first UV map is for the texture and the second is for the lightmap. Now with the blank UV map selected, I used the UV projection tool, with the Projection mode set to Atlas and then just left-clicked in the UV editor window to create the projection. That's it. The Atlas projection unwrapped and arranged all of the coordinates in a manner that's perfect for creating a lightmap. In Fig. 4.24, you can see the UVs that were created for the purpose of creating a lightmap.

> **Generate Lightmap UVs in Unity iOS**
> 
> Unity iOS has a great new feature that allows you to generate UVs for lightmapping purposes in the Import Settings. We'll be taking a look at this option in Chapter 8.

![](img/d3e3fa4010906e98ec76be003a6e31c2_107_1.png)

## Summary

That brings us to the end of this chapter. We discussed several important topics such as building on the grid, breaking a level into sections, and setting a working texture size. As you can see, modeling a level isn’t overly complicated in terms of modeling technique. It most certainly can be more complicated than the level shown here, but the base concepts shown in this chapter will carry over into even the most complex level designs.

However, the techniques discussed in this chapter are not complete. In Chapter 8, we will revisit this level and further discuss lightmapping by detailing the process of using Beast in Unity iOS. We will also discuss how I was able to add dirt and grime to the lightmap in order to further provide some unique and random details to the level while minimizing the repeating nature of tiling textures.

![](img/d3e3fa4010906e98ec76be003a6e31c2_110_0.png)

## Animation Using Blender

### Rigging Tater

In this chapter, we are going to take a look at the process of rigging Tater for the purpose of creating several game animations such as running, walking, and shooting. This chapter will focus on using the open-source Blender application. Most 3D applications are very expensive, and Blender, being free, can be a great alternative for the independent game developer. Blender is available for all platforms, i.e., Windows, Mac OS, and Linux. Blender was chosen as the animation package for this book as it's a great companion to a modo pipeline. Although modo has some robust animation capabilities, it lacks a bone and skinning system, which is vital to creating skinned meshes for use in Unity iOS. Now, you could create a segmented character in modo that is animated using constraints and IK, but this type of character will not fit my project requirements.

As with all the content in this book, this chapter assumes that you have a working knowledge of the software, which in the case of the next three chapters is Blender. For the Blender sections of the book, I used the 2.53 Beta. You can download Blender 2.5 at http://www.blender.org.

### Tater's Weapon Load Out

Go to the resource site to view the video walkthrough for this chapter.

As we did with the previous chapters, we are going to take a look at the “why” before we get into the “how” by studying how bones and skinned meshes should be optimized for the iPhone and iPad hardware and how skinned meshes work in Unity iOS. By first understanding the why, we’ll then be able to correctly build a rigged character for use in a game targeted for the iPhone and iPad platforms. We’ll begin by taking a look at matching object sizes between modo, Blender, and Unity iOS.

One more thing worth mentioning is that even if you’re not a Blender user, this chapter will contain important information toward rigging and skinning a character for use in Unity iOS and the iPhone. The information in this chapter can easily be ported to other 3D applications such as Maya, 3DS Max, LightWave 3D, Softimage, or Cinema 4D. Be sure to check out the “My Dad Can Beat up Your Dad” sidebar.

### Matching Object Size

In order to properly get our models into Unity iOS, we need to first make sure that we have established a correct workflow for maintaining the correct object size as we move from modo to Blender into Unity iOS. In Chapter 2, we discussed the sizing differences between modo and Unity iOS, and we worked out a solution to compensating for the way in which the different programs internally handle object size in terms of units of measurement. Now, we are going to add another variable into the equation so to speak as we add Blender to the mix.

*The important thing to understand with a modo to Blender pipeline is that given the internal default units, a modo object will be half as small as a default Blender object when it's imported into Blender.*

My workflow is to create all objects using modo and use Blender for rigging, skinning, and animating skinned characters, as this currently isn't possible with modo. The important thing to understand with a modo to Blender pipeline is that given the internal default units, a modo object will be half as small as a default Blender object when it's imported into Blender. Remember from the previous chapters that in modo, we established the Default Unity iOS System to be in Game Units and that we would work with a setting of 1 meter per Game Unit. In Fig. 5.1, you can see that a default modo cube set to these specifications is exactly half the size of a default Blender cube.

It's important to understand this relationship, as Tater will be exported from Blender into Unity iOS, and I'll need to know how to correctly set the Scale Factor in the FBX Importer settings. Understanding the size ratio between modo and Blender objects will give me the vital information needed to enter the correct value. We know from Chapter 2 that when importing a default 1 meter per Game Unit object from modo to Unity iOS, we need to adjust the Scale Factor in the FBX Importer to 0.01. We also need to establish this same base setting for Blender objects imported into Unity iOS. In Fig. 5.2, you can

### My Dad Can Beat up Your Dad

Do a quick stop at almost any CG forum and you'll easily be able to find forum topics bantering back and forth about “my app X is better than your app Y.” It sometimes reminds me of the old philosophical debate that many of us discussed on the playground around the age of five: “Oh yeah, well my Dad can beat up your Dad.” Although healthy debate can often bring about new ideas, this particular debate about the best software is hardly ever constructive, nor is it easily settled.

It's best to realize that it's not about the software. It's about the artist's skill, technique, and creative problem solving to get a game completed that really matter. If you truly understand the principles of 3D, then it doesn't really matter which software you use, and it ultimately comes down to personal preference. For instance, I'm not an advanced Blender user. I think it's a great program and it makes a good solution for filling in modo's animation gaps, although at my day job, I use Maya for rigging and animation. However, by having a strong foundation in the process behind rigging
