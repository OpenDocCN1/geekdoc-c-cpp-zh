# Why?

The dirt and grime was very important for the effective color map. However, in the real world usually this dirt and grime is over the top of existing tactile attributes. This means, usually the grime is going over the peaks and settling into the valleys of a surface and not actually changing the rises and falls. Through this process we will be using the light and dark parts of the color texture to define (roughly) the high parts and low parts of the surface. If the drips (for instance) were left, the normal map would interpret them as actually recessed sections of the surface rather than grime atop a surface.

**Step 4:** Gray out areas without much bump (Figure 7.4). This can happen with an adjustment layer, or with a new layer with 50% gray filled or painted in over areas that are smooth.

![](bbox=[0.496, 0.363, 0.795, 0.578])

*FIGURE 7.4* Areas without bump grayed out.

# Why?

The two areas that are grayed out in Figure 7.4 are the cement floorboards and the cement wall under the roof. Since this is cement, it may have a bit of bump (which is why the gray isn't a solid gray), but not a whole lot. If this is not grayed out, then every dark splotch on the color part would register at a pock mark. Graying it out keeps the surface visually smooth.

**Step 5:** Flatten the layers. Layer>Flatten Image.

# Why?

Once we are down to the core color information, there is little need for all the other layers to be taking up all that memory space and slowing the work. Alternately, the dirt layers could just be deleted instead.

# High Pass Filter

**Step 6:** Run a High Pass filter. Select Filter>Other>High Pass. Adjust the Radius to about 10 (although this is largely to taste (Figure 7.5).