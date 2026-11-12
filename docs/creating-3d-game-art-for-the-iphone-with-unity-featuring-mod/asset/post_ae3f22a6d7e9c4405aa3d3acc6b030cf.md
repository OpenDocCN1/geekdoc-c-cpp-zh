
of color values. A value of 0 will produce a linear interpolation while 1 will produce a gradient-based interpolation, which can produce artifacts at the cost of detail.

Ambient Occlusion is also an important setting as it can produce subtle occlusion shading in your scene. The Max Distance controls how far a ray can travel before it's considered to be not occluded. A value of 0 means that the ray is infinitely long. Contrast controls the transition between occluded and not occluded rays. Ambient Occlusion can provide a nice subtle shading effect to your scene. In Fig. 8.22, you can see the difference between a scene with Ambient Occlusion and without Ambient Occlusion. The difference is subtle. Ambient Occlusion tends to help anchor the object in the scene with increased shading in the corner areas where light has difficulty reaching.

![](img/d3e3fa4010906e98ec76be003a6e31c2_220_0.png)

> **FIG 8.22** Here You Can See the Difference between Occlusion On and Off. Notice That the Lightmap with Ambient Occlusion Seems to Anchor the Objects, Especially in Shadow Areas.

Something else to consider is that you can compress the lightmaps via the Compression toggle on the Maps tab of the Lightmapping Editor. Compression can cause artifacts to appear in your maps, as the compression setting toggles PVRTC 4 and RGB16 compression on your maps. However, by not compressing the files, you risk eating up texture memory. Again, you'll need to test and profile your game to see which is the best route to take in terms of compression.

## Beast Custom Settings

At some point, you might find yourself needing to make some custom adjustment to the Beast settings. Beast reads baked settings from an XML file, which can be edited. From the Lightmap Editor, you can choose to generate a custom Beast file as shown in Fig. 8.23. This will add an XML file, which holds all of the Beast's render settings into your lightmaps folder. This XML file allows you to make custom adjustments such as Anti-Aliasing Settings and choose a different environment type as shown in Fig. 8.24.

![](img/d3e3fa4010906e98ec76be003a6e31c2_222_0.png)

> **FIG 8.24** The Custom Beast File Is in the XML Format and Can Be Used to Edit or Change Settings Not Available in the Lightmap Editor.

You can see an example from the Beast API manual that shows how the XML file can be changed to use IBL. The Beast API manual can be found on the Illuminate Labs Web site. However, during the writing of this book, Illuminate Labs was purchased by Autodesk, which means this information will be shifted toward the Autodesk site at some point.

```xml
<EnvironmentSettings>
    <!--The type of Environment. None, SkyLight (constant color) or IBL (image based)-->
    <gEnvironment>SkyHDR</gEnvironment>
    <!--Environment SkyLight color. Only used for the Unity3D used for avoiding gamma correction errors and to remap HDR textures to something that fits your needs -->
    <gIntensity>1.0</gIntensity>
    <rIntensity>1.0</rIntensity>
    <!--This is the environment color. Used if type in SkyLight-->
    <SkyLightColor>
        <r>0.7</r>
        <g>0.7</g>
        <b>0.7</b>
        <a>1.0</a>
    </SkyLightColor>
    <!--The image file to be used in HDR or OpenEXR format. The file should be long lat. Used if type is IBL-->
    <IBLImageFile>filename.exr</IBLImageFile>
</EnvironmentSettings>
```

Change to IBL

> **FIG 8.25** Here You Can See That You Can Replace "SkyLight" to "IBL" in the gEnvironment Key Within the Custom Beast XML File.

## Adjusting Lightmaps

Once the bake is completed, you can then further edit the maps in an image editor such as Photoshop to adjust exposure and color, as well as paint grime, to break up any repeating patterns in the level.

It's important to note that in the following sections, we'll be changing the lightmaps used in Unity iOS by Beast, which are found in the directory of the scene in a folder named the same as the scene. If you decide to bake the scene again, you will lose your edits, as Beast will overwrite the files. A good workflow is to place the grime or dirt on a separate layer in Photoshop so that if you do need to re-bake the scene, you can easily re-apply your dirt layer. The same goes for any color correction. It's a good idea to use Adjustment Layers in Photoshop with Levels or Exposure changes so that you can easily re-apply these effects again.

## Color Grading Maps

The lightmaps created are in the EXR format, which is an HDR format. This is great because, since these files contain HDR floating point values, you can take these files into Photoshop and interactively adjust the lighting and color values to create different looks without re-baking the scene. This works because Beast bakes the lighting within a full 32-bit floating-point HDR pipeline as mentioned earlier in the chapter. With Beast, you can push lighting values above white, i.e., a value of 1.0, which is referred to as "super-white." This means that when editing the file in a program that supports HDR, you can have access to all this lighting information when adjusting exposure and color. For example, to have access to super-white values in Photoshop, I cranked the intensity of the Directional Light to 2.0. This resulted in my scene being blown out as shown in Fig. 8.26.

![](img/d3e3fa4010906e98ec76be003a6e31c2_223_0.png)

> **FIG 8.26** The Lightmap Scene Is Very Blown Out Due to Having a High Light Intensity.

Next, I opened the Far lightmap into Photoshop by simply double-clicking the file since I have the Image Application set to Photoshop in the Unity iOS preferences and tweaked the exposure, as well as increased the blue tone in the shadow areas.

In order to properly gauge your color grading, you'll need to adjust the Proof Setup in Photoshop. I mentioned earlier that Beast renders in floating-point linear space, which means the files are at a gamma of 1.0. Files stored in linear space will look dark on your monitor, but in this case, we actually want to view the file in its default linear gamma of 1.0 in order to accurately set the exposure. To do this in Photoshop, go to View and make sure that Proof Colors is enabled. Then, go to View > Proof Setup and choose Monitor RGB as shown in Fig. 8.27. This will set the display to view the image in its default gamma, which will make any color correction or exposure changes done in Photoshop match how they'll look in Unity iOS.

### Photoshop and 32-Bit HDR

Photoshop can work with 32-bit HDR files, but most of the tools are not available in this mode. Some good tools to use in this mode are Levels, Exposure, and HDR Toning found under the Image > Adjustments menu.

![](img/d3e3fa4010906e98ec76be003a6e31c2_224_0.png)

> **FIG 8.27** We Need to Change the Proof Setup to Monitor RGB in Order to View the Image at Its Default Linear Gamma.

Since the EXR file contains HDR values, I have access to the entire lighting range and can lower the blown out areas of the map. This gives me a lot of flexibility when editing the lightmap since I'm not locked to a limited range in lighting values as is found with typical 8-bit or low-dynamic range images. In Fig. 8.28, you can see that I used the HDR Toning tools to affect the overall look of the lightmap, which produces a more pleasing style to the game. Again, having the HDR values in the map allows me to make exposure changes in post instead of having to re-bake the lightmap repeatedly, as well as allows me to push and pull the lighting to create various looks. For instance, looking back at Fig. 8.28, you can see that I was able to introduce a little bit of a blooming effect by adjusting the lightmap.

Saving the EXR in Photoshop results in the file automatically being updated in Unity iOS. This is a great workflow for experimenting with different looks for the scene and in the visual effects world is referred to as color grading. In Fig. 8.29, you can see that by adjusting the exposure and color values,
