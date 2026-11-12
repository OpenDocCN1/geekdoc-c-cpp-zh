
**FIGURE 4.9** Scaled UVs to allow multiple repeating texture.

![](img/0285f88bc840f313779e011725b623a5_95_0.png)

## Conclusion

And there you have it. This same technique will work for most any texture that needs to be tiled. Admittedly, it can get trickier for surfaces like (ironically) tile, where getting the ends to line up can take some deft handling. But, the work will pay off. As large surfaces become visible, the effective texture will pay visual dividends down the road.

Notice that there are some good things happening here. Zoom down and place the camera about where a player would be in the game; the texture should hold up pretty well. However, when the camera is way up (as in Figure 4.9), the repeating pattern will be pretty clear. Some of this will become a nonissue once the scene is baked, and since we are never very high in relation to this dock, it's unlikely we'll notice the repeating pattern. If, in the game, we do have a distracting repeating pattern, we can go back and scale the texture a bit, or work with a larger sampling of texture, or both.

## Tutorial 4.2. Nontiled Textures and Their Dirt

One of the biggest errors of young 3D students is that they are too clean. Yes, I agree it's hard to believe that 18- and 19-year-olds can ever be accused of that, but in 3D this is almost always the case.

This is what happens: The student goes out and does some good research, tracks down some great resource textures, creates the appropriate paintings of the surface from copying and pasting the necessary textures together, and then slaps that onto the surface. The problem emerges once everything is put together. In reality, the region where two surfaces meet is a really interesting area. It collects all sorts of dirt, grime, and visually interesting things if it's an inside corner (think of where the floor meets the wall), and collects all sorts of drips on outside corners. When the texture artist fails to take this into account, the scene loses much of the visual information that clues the eye in on these all-important corners.

For the first part of this tutorial, we will look at how to put together a texture-for-texture space without overlapping UVs. For the second part, we will take this texture and dirty it down.

- **Step 1:** Select an object with nonoverlapping UVs and open the UV Texture Editor (Figure 4.10). For this tutorial, I will be texturing the small portico (downloadable at www.Creating3dGames.com) of the main door that lets Aegis Chung into the facility.

> **Warnings and Pitfalls**
>
> Make sure that the object is selected in Object Mode; if in any component mode, the next step won't work. Outputting a UV Snapshot only works when the whole object is selected, not just its parts.

![](img/0285f88bc840f313779e011725b623a5_96_0.png)

### UV Snapshots

- **Step 2:** Output a UV Snapshot. When the UV Map is displayed in the UV Texture Editor, choose Polygons->UV Snapshot (all within the UV Texture Editor). Within the UV Snapshot window, make sure Size X and Size Y both read 2048 and that the image format is set to TIFF. Change the name to EntryWay_PorticoUV.

> **Tips and Tricks**
>
> Notice that the File Name input field includes a path. Notice that this path is (or should be) the project file and the images folder within the project file. The images folder is one of the default output locations for Maya. Once again, having the project set correctly raises its head.

### Why?

Why 2048x2048? First it's a power-of-two value texture. But why not 1024x1024 or even 4096x4096 or even 512x512? This is a good question; what size to make a texture is dictated largely by experience and the situation. In this case, we will be spending some time within this portico, and so we want to have a reasonable resolution so that the walls that surround the player hold up to visual scrutiny. Now, we may discover that we don't need 2048×2048 (that is in fact a big texture). I suspect a 1024×1024 might do the job just fine. But because Unity allows for some really easy adjustments in the size that it imports files to, there is little penalty from creating the texture a little larger for now, and then optimizing if need be or the situation allows. It's better to have the resolution and not need it than the other way around.

- **Step 3:** Open the UV map in Photoshop (Figure 4.11).

**FIGURE 4.11** UV Snapshot.

![](img/0285f88bc840f313779e011725b623a5_97_0.png)

### Preparing the UV Snapshot for Painting in Photoshop

- **Step 4:** Copy the UV guidelines to another layer. The easiest way to do this is to open the Channels palette (Window > Channels). Ctrl-click the Alpha 1 channel (this will select the white lines), choose Edit > Copy, and then Edit > Paste. Open the Layers palette and rename this new layer UV Guidelines.

### Why?

The UV Snapshot in Photoshop is the image that will serve as the guide to know what texture is being applied where. If a red line is painted through the middle of a wall on this map, bring this map into the color channel of the material, and the red line will appear in the scene (on the wall). This is tremendously powerful since texture is placed right where it should be on the mesh.

However, painting on top of the default image is a problem because it covers up the guides that help to know where on the surface is being manipulated. By duplicating the UV lines onto another layer, new layers can be created between this new UV Guidelines layer and the Background layer. So as the texture map is created it remains clear where on the object you are applying texture.

> **Tips and Tricks**
>
> Depending on the texture being built, this new UV Guidelines may be more effective with black lines. Remember a layer can have a stroke applied (Edit > Stroke) or invert the white lines to black (Image > Adjustments > Invert).

### Painting the Texture

- **Step 5:** Lay down an initial color pass using photo reference. Figure 4.12 shows the results of my first pass. It is made with many copies of BunkerPainted0010 (http://cgtextures.com/texview.php?id=47345) for the white painted parts, and ConcreteBare0314 (http://cgtextures.com/texview.php?id=44689) for the cement floorboards. If you'd like to use these same textures the links are on the supporting web site (http://www.Creating3dGames.com), although feel free to use whatever you feel is most effective here.

![](img/0285f88bc840f313779e011725b623a5_98_0.png)

> **Tips and Tricks**
>
> As much as possible, try and use nondestructive methods to cobble together swatches of texture. My favorite way to do this is by applying layer masks to each layer, and then paint out sections by painting black on the mask. Then if I need some of that texture back later, I can just paint it back in with white on the layer mask.

- **Step 6:** Find and download an image that provides some good grime for corners. Figure 4.13 shows ConcreteDirty0271 from CGTextures (http://cgtextures.com/texview.php?id=51950). We're looking for a straight edge (at the bottom of the image) and then an organic color shape next to that. Don't worry about the stuff at the top of the image (we'll mask it out).

- **Step 7:** Import or cut and paste the image into the UV Snapshot. Scale it and rotate it so the "grime" sits at the base of the wall (Figure 4.14).

![](img/0285f88bc840f313779e011725b623a5_99_0.png)

![](img/0285f88bc840f313779e011725b623a5_99_1.png)

> **Tips and Tricks**
>
> Be sure that as these new layers are created or copy and pasted that they are named. As discussed earlier, naming is important both for the efficacy of the artist creating the asset, and for the artists who inherit assets later.

### Layer Mixing

- **Step 8:** In the Layers palette (and on this newly created grime layer), change the Layer Mixing setting from Normal to Multiply (Figure 4.15).

### Why?

The Layer Mix option of the Layers palette is incredibly powerful. It allows the layers to interact in important ways beyond just "put this layer atop the one beneath it." Multiply is one of my favorites because its
