# Handrails

**Step 25:** Create handrails, optimize them into one mesh (Figure 2.23).  
Center the pivot, and name it `EntrywayHandrails`. Delete the history.

![](bbox=[0.486, 0.18, 0.775, 0.287])

*FIGURE 2.23* Completed handrails.

# Tips and Tricks

If an element is optimized before duplicating (for instance deleting the top and bottom planes of the vertical posts of the handrails), it'll save the step later of selecting a big bunch of them later.

# Archway and Booleans

**Step 26:** Create the start of the entry arch with a modified cube. Create a cube (Create>Polygons>Cube), then scale and position it similar to Figure 2.24. Select the top face, and using the Extrude tool, extrude and scale the top of the box (Figure 2.24).

![](bbox=[0.412, 0.537, 0.854, 0.664])

*FIGURE 2.24* Beginning of entry arch.

# Why?

The idea for this next group of steps will be to use Maya's Boolean functions to create a form. Booleans work on the idea of subtracting (or adding or intersecting) two shapes. To make this work we have to have this block to subtract from. In the next step we will form the shape we wish to subtract from this block.

# Tips and Tricks

Notice that in Figure 2.24 the scaling that occurs after the plane is extruded only happens along the X axis. This makes sure that the front two polygons line up and make the Boolean to come a bit cleaner.