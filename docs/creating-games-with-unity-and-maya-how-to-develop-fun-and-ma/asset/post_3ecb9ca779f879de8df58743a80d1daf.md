
## Plan of Attack

As implied in this chapter, the main focus will be on baking the lighting of the scene. This will actually take a few steps that build upon each other. First, before we start doing much lighting, we will look at some advanced shader construction—the use of Normal Maps, which will help to provide surfaces that appear bumpy (or not) and not just like flat objects with color on them. This advanced shader construction will come in handy as we look at Unity's lighting scheme and how to control Unity's lighting instruments.

Finally, once some real-time lighting has been established we will look at baking strategies and settings to get a nicely baked lightmap that will look good in the game. Along the way, we will light the scene for a couple of different scenarios—first for a bright sunny day (since it allows the effects of light maps to be seen most clearly), and then for the dark, damp, and dismal day that the game actually calls for.

### Tutorial 7.1: Normal Maps

**Normal maps** are maps that help create more tactile-looking surfaces. Normal maps don't actually change the polygons of a surface—they don't really change the object they are attached to, but they present the visible representation of a more complex form. The grandfather of normal maps was bump maps, but normal maps are more powerful in some important ways.

Bump maps were largely grayscale (or at least that was the only value that mattered to the 3D software rendering them). When the texture map that was used to define bump had pixels closer to white, they were rendered as raised and pixels close to black were rendered as receding. The power of this was that a surface looked as though it had all sorts of bumps and valleys when the geometry did not.

Normal maps take this to the next level in that they use a similar idea, but instead of simply rendering the surface as raised or lowered in one direction, they describe the x, y, and z coordinates of a normal vector. The science and math here is well beyond what is relevant, but the net results are low-poly forms that are able to visually indicate much higher forms. The textures react to change in light and behave in believable and predictable ways as a player moves around them. In 3D arenas where polycount is important (like games), normal maps are tremendously powerful.

Historically, there are three ways that normal maps are usually created. The first is to actually model a very high-poly version of a surface (including characters) and then generate a normal map from that high-poly mesh that will be applied to a much lower-rez version of the form. In many ways this is most accurate, and frankly often produces the best normal maps. However, this essentially means creating the form twice, which can take some serious time. Although for characters that will be seen throughout a game, this could well be a worthwhile technique.

The second method is to use some of the relatively new tools on the market (ZBrush or Mudbox) to paint normal maps. Essentially what these packages are doing is creating higher-resolution copies of a form that are sculpted (in some really fun ways) in these applications and then normal maps are generated and applied to their lower-resolution cousin. Especially for character work ZBrush and Mudbox are some really awesome tools. They have become ubiquitous in game character creation. If character design and creation are your thing, be sure to get your hands on one of these tools (I prefer Mudbox because it interfaces well into Maya, but there are fantastic results coming out of both packages).

The third method is the method we will be exploring—extracting a normal map from a color map. Up to this point we have been defining a surface by the color attributes alone. A rock wall is painted to look like a rock wall. However, this painted rock wall is flat without any of the real peaks and valleys that such a wall would have from one rock to the next. This means that the still image might work out, but as a player walks up to and past the wall, there is never any of the visual clues that there are actually rocks coming out of that mortar.

Because the color maps are complete, and because the raw versions of those color textures are carefully saved in the images folder of the Maya project file (Incursion–Maya), the core building blocks of this technique are at hand. A bit of time in Photoshop and a few additional tools will yield some reasonable normal maps.

The drawback to using Photoshop to develop normal maps is that the creation is a little more opaque. Figure 7.1 shows what a bump map would look like as opposed to a normal map.

![](img/0285f88bc840f313779e011725b623a5_170_0.png)

**FIGURE 7.1** Bump (top) vs. normal (bottom).

![](img/0285f88bc840f313779e011725b623a5_172_0.png)

FIGURE 7.2  Raw version of the inner walls texture. Notice the complex collection of layers that will pay off here.

### Tips and Tricks

Remember that in the texture creation chapter (Chapter 4), whenever we built a texture we kept a copy of the construction texture in the images folder and a flattened version in the sourceimages folder (both within the Maya project folder). Keeping that raw version pays dividends in situations like this. Because all the dirt and drips are on separate layers, those can just be hidden to reveal the base texture beneath.

If you are following exactly along with the tutorial and using the assets I use as provided on the web site (http://www.Creating3dGames.com), the file we are after, EntrywayWallsInnerUV, is in the images folder.

### Cleaning up the Raw Texture

**Step 3:** Hide all the grime, dirt, and drips layers. Do this in the Layers palette by just turning off the eye icon on the layers that are not wanted (Figure 7.3).

![](img/0285f88bc840f313779e011725b623a5_172_1.png)

FIGURE 7.3  Base texture without added dirt and grime

### Why?

The dirt and grime was very important for the effective color map. However, in the real world usually this dirt and grime is over the top of existing tactile attributes. This means, usually the grime is going over the peaks and settling into the valleys of a surface and not actually changing the rises and falls. Through this process we will be using the light and dark parts of the color texture to define (roughly) the high parts and low parts of the surface. If the drips (for instance) were left, the normal map would interpret them as actually recessed sections of the surface rather than grime atop a surface.

**Step 4:** Gray out areas without much bump (Figure 7.4). This can happen with an adjustment layer, or with a new layer with 50% gray filled or painted in over areas that are smooth.

![](img/0285f88bc840f313779e011725b623a5_173_0.png)

*FIGURE 7.4* Areas without bump grayed out.

### Why?

The two areas that are grayed out in Figure 7.4 are the cement floorboards and the cement wall under the roof. Since this is cement, it may have a bit of bump (which is why the gray isn't a solid gray), but not a whole lot. If this is not grayed out, then every dark splotch on the color part would register as a pockmark. Graying it out keeps the surface visually smooth.

**Step 5:** Flatten the layers. Layer>Flatten Image.

### Why?

Once we are down to the core color information, there is little need for all the other layers to be taking up all that memory space and slowing the work. Alternatively, the dirt layers could just be deleted instead.

### High Pass Filter

**Step 6:** Run a High Pass filter. Select Filter>Other>High Pass. Adjust the Radius to about 10 (although this is largely to taste; see Figure 7.5).

![](img/0285f88bc840f313779e011725b623a5_176_0.png)

**FIGURE 7.8** Sample of the newly created normal map.

![](img/0285f88bc840f313779e011725b623a5_176_1.png)

**FIGURE 7.9** Sample of first level of Gaussian blur.

### Why?

Even with our High Pass, there is still quite a bit of “noise” in that initial pass. Giving a little blur helps soften the noise and keeps the information where it should be. This shouldn’t be too high since too much of a blur will simply wipe out all the detail (including the desirable large detail).

### Tips and Tricks

How much to blur this first pass is tricky. Much of it is relative to the file being affected. A Radius of 1 might be just the trick for a 2048×2048 image, but way too much for a 512×512. Further, if the image is tileable and viewed much closer, it might need to be much higher (5 or more). So keep frequent saves to make sure you can go back to an earlier version if things aren’t going as planned.

### Layering to Increase Height

**Step 10:** Duplicate the Background layer. The quick keyboard shortcut for this is Ctrl-J (Command-J on a Mac). This will create a new layer (Layer 1) identical to the first that sits atop the original.

**Step 11:** Change the new Layer 1 Blending to Overlay. You can do this either within the Layers palette (immediately beneath the Layers tab) or by double-clicking the layer and in the Blending Options section of the Layer Style window changing the Blend Mode drop-down menu. The results can be seen in Figure 7.10.

![](img/0285f88bc840f313779e011725b623a5_176_2.png)

**FIGURE 7.10** Results of duplicate layer with an Overlay Blending Mode.

> **Warnings and Pitfalls**
>
> By using an additional layer and adding the value, this is no longer a valid normal map. Remember when we talked earlier about the normal vectors needing to equal exactly 1? Well, now they definitely do not, so be sure not to use the file in its current state or the results will be very unpredictable.

### Why?

Often the results of the NormalMapFilter are too muted. The amount the surface will be raised is just too low. By duplicating the information and adding the color information to the original via the Overlay Blending Mode, the height of the normal map will increase.

**Step 12:** Gaussian blur Layer 1 with a Radius of 2 (Figure 7.11).
