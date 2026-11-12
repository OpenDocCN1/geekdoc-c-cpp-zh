
![](img/0285f88bc840f313779e011725b623a5_177_0.png)

*Figure 7.11* Blurring new layer.

### Why?

By making the next level up blurred a bit more, we are creating a stepped increase in the new height being created. Each successive copy will be blurred a bit more, thus increasing the height and spreading the up ramp out a bit.

- **Step 13:** Repeat the process of duplicating the level and then running a Gaussian Blur, but this time with a radius of 4.
- **Step 14:** Repeat the duplication and Gaussian blur process five more times, each time increasing the radius of the blur by 2 (Figure 7.12).

*Figure 7.12* Multiple layers of increasingly blurred normal maps.

![](img/0285f88bc840f313779e011725b623a5_177_1.png)

### Why?

Take a look at Figure 7.13, which shows the initial output by NormalMapFilter and compares it to the result of the multiple overlayed layers. Notice how much more information is there, and how much richer the normal map actually is.

![](img/0285f88bc840f313779e011725b623a5_178_0.png)

**FIGURE 7.13** Comparison between original output and layered approach.

### Housekeeping

- **Step 15:** Save again. Be sure you're saving as EntryWayWallsInnerNormalRaw.

### Why?

Since this strange bluish image makes it pretty tough to know what the result will look like, it will be important to have the raw version to come back to if the final result in Unity is not what was planned.

- **Step 16:** Flatten the image (Layer > Flatten Image).

### Why?

We will need to "normalize" the image to bring the normal vectors back into the needed value of 1, but this needs to be done to the total image and not just one layer.

- **Step 17:** Normalize the image. Choose Filter > NVidia Tools > NormalMapFilter. In the Alternate Conversion area check Normalize Only. Press OK.

### Why?

The other settings can all remain the same because none of them will be used. Normalize Only will ensure the red, green, and blue normal vectors are exactly 1 and thus ready to be a normal map.

- **Step 18:** Save the image for use in Unity. Save the file as EntryWay_WallsInner_Normal into the Incursion-Unity/Assets/EntryWay.fbm. The file format can be whatever you'd like (I saved it as a .psd).

### Why?

Due to our deft use of manual exporting, all the texture files related to the EntryWay are in this EntryWay.fbm folder that Unity created. Adding any new texture assets that are meant for EntryWay keeps the Project panel clean.

![](img/0285f88bc840f313779e011725b623a5_180_0.png)

Figure 7.14: Before (right) and after (left) using the normal map.

### Why?

Yes, it appears a bit hyper right now—it is too wet with too much specular. But because the scene has not been lit yet, we just need a glimpse of the visual effect of the process. Later it’ll be changed and made a bit dustier. Do note that normal maps show differently depending on the lighting that is illuminating it. Upon first applying the normal map, there may not be a huge difference in the appearance of the surface—this will come later when additional lights are placed in the scene. If you would like to experiment with some quick lighting (GameObject > Create Other > Point Light (or Spotlight or Directional Light)), you can get a quick feel for how lighting and shading are closely intertwined as the light is moved around. Don’t sweat the lighting too much at this point though. We will be working much more with lighting in steps to come.

- **Step 23:** Repeat this process for any surfaces that need a normal map. This could include the tiles and maybe even parts of the rusty beams. Don’t worry about areas that are mostly smooth (well-worn cement for example), but areas that should be bumpy need normal maps.

## Conclusion

Normal maps can add tremendous depth to a scene. If you are using a quick tool like CrazyBump, they won’t even take very long to implement. We could have made these while working in Maya, and indeed it would have made the model look better in Maya. However, because Unity interprets some things (especially normal maps) differently than Maya does, it is usually not worth getting too caught up making extensive materials in Maya. Do that assemblage in Unity.

## Tutorial 7.2: Lighting and Baking in Unity

Up to this point, the scene has made use of a very simple lighting scheme—it had none. OK, well, turning up the Ambient Light in the Render Settings could be considered a lighting scheme, but that’s stretching it. Ambient light in

any lights in the scene quite yet, just take a look at the following explanations to see what the lights do before placing any in the scene.

### Point Light

Think of point lights as a single light bulb suspended in space. Figure 7.15 shows a point light sitting in the scene (with ambient light turned off). There are really two types of handles that a selected point light presents in Unity 3. The first is the actual light source—the point from which the illumination emits. This light source can be moved, scaled, or rotated, although since the light is emanating from all sides, only moving it will yield any noticeable results. The second are the Range Handles. These handles are actually just the six little yellow dots at the intersection of the three yellow rings that surround the source. In any tool (move, rotate, or scale), selecting these handles will increase or decrease the falloff range of the light. The illumination from the point light will go no further than these handles.

![](img/0285f88bc840f313779e011725b623a5_182_0.png)

FIGURE 7.15 Point light and its relevant handles available in the Scene window.

### Tips and Tricks

These handles are really, really picky. The tip of the arrow of the cursor has to be exactly on that handle. Takes a little practice to grab those just right, but they are definitely more intuitive to use than the numerical range input field in the Inspector.

The Inspector shows the other options available for the point light. Because these are covered fairly well in the documentation, we will refrain from covering them all here except for a few tips.

**Intensity** and **range** have an interesting relationship. Intensity refers to the brightness of the illumination, but this illumination will still stay within the light's range.

**Cookies** are gobos from the theatre world. What they do is provide a textured light—a light with some shadow on it. Think of the shadow made as light streams through a tree without a dense canopy of leaves. Cookies can be handy to imply geometry that isn't there (think of plays that take place in a forest lit with a "cookie" so the audience can see the shadows of trees and leaves that are not actually present). For point lights, cookies must be Cube Maps with alpha channels.

**Shadows** are beautiful but expensive in terms of resources. It takes a good deal of horsepower to draw the shadows emitted by any light. Point lights are especially expensive because they are essentially six spotlights shooting out in each direction. This means drawing all these shadows and draw calls in realtime can very quickly drag your game to a crawl. Hard shadows are easier to draw than soft, but without some serious baking, multiple-point lights with shadows will kill a frame rate. Note that shadows drawn in realtime are available only with Unity Pro—although they will be present in baked scenes when using the free Unity.

**Halos** can be thought of as glows.

**Render mode** is used for determining how critical a light is when Unity is determining what to draw. For our level (and for most levels) Auto is a fine setting.

**Culling mask** determines what this light illuminates. By default it illuminates everything, but this can be restricted so a certain light only lights certain objects. This actually comes in handy more often than you'd think.

**Lightmapping** allows for the definition of whether this light is used in the lightmapping process or not. It can be used in both lightmapping and realtime of course, and in most situations a setting of Auto works fine.

### Spotlight

Illumination emanates from a single point from a spotlight but emits out in a cone shape just like a real spotlight. Figure 7.16 shows a spotlight and its relevant handles. It still has a Range handle, but only one, and it indicates the linear throw the light has. The new handles available here are the Spot Angle Handles, which allow for the angle of the spot.

The Move and Rotate tools are very important for this tool. Rotating to find the right spot to spotlight is the key to this tool.

Most of the notes for point lights apply to spotlights as well. A couple of notable exceptions are (1) for a spotlight, **cookies** can be a single image with an alpha channel, but it must have a black edge all the way around the image; and (2) upon import, the Texture Import settings must have Border Mipmaps activated, and the wrapping mode selected to Clamp.

### Directional Light

Directional lights can be a little goofy to understand. Figure 7.17 shows the scene with one directional light that is casting shadows. Remember that only Unity Pro will cast realtime shadows, but shadows help illustrate what this
