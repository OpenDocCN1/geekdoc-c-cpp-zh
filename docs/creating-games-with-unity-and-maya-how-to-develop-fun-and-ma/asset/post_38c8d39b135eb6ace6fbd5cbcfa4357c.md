
To optimize what we've created, we will be deleting edges that aren't needed and rearranging some of the edges that exist. Figure 2.15 shows one such edge that we should delete. Double-click the edge that will attempt to select an edge loop and then either press Delete on the keyboard (and then select and delete the vertices it leaves behind), or Ctrl-right-click and choose Edge Loop Utilities > To Edge Loop and Delete (which will automatically delete the left-behind points).

- **Step 15:** Adjust topology to ensure four-sided polygons. Look carefully at Figure 2.16. Note that this top polygon is actually a five-sided polygon. It's deceptive as sides 4 and 5 at first blush appear to be one edge, but there is a vertex in the middle where that other edge comes out. In a case like this, where all the polygons on the top of the deck are on the same plane, this five-sided poly would likely not cause any trouble; to be sure we will use another new tool, the **Split Polygon tool**.

  ![](img/0285f88bc840f313779e011725b623a5_44_0.png)

  **FIGURE 2.15** Edge that isn't needed and should be deleted. Make sure you delete the points it leaves behind.

  ![](img/0285f88bc840f313779e011725b623a5_44_1.png)

  **FIGURE 2.16** Deceptive five-sided polygon.

  In Object Mode, choose Polygons>Edit Mesh>Split Polygon Tool. This tool works by clicking and dragging on an edge to establish where to split the polygon. Usually click an edge and drag along the edge to a point (Figure 2.17). Click again on the opposite edge and drag to the point opposite the first. This will create two polygons (a four-sided one and a three-sided one) where there was once a five-sided polygon.

- **Step 16:** Clean corners. Now that we've used the Split Polygon tool, we can further optimize our polycount in places that make right-angle corners. Figure 2.18 shows the result of using the Split Polygon tool to make a new cut from corner to corner. After this diagonal cut is made, the two straight edges that used to make the corner can be deleted.

  ![](img/0285f88bc840f313779e011725b623a5_44_2.png)

  **FIGURE 2.17** Using the Split Polygon tool.

  ![](img/0285f88bc840f313779e011725b623a5_44_3.png)

  **FIGURE 2.18** Optimizing a corner. Split Polygon tool creates the diagonal which then makes two edges unneeded.

### Tips and Tricks

Be sure that when getting rid of the edges that are no longer needed that those edges as they continue down the side and bottom of the shape are deleted as well. Additionally, watch for left-over vertices that should be selected and deleted as well.

- **Step 17:** Repeat and optimize throughout right-angle corners (Figure 2.19).

  ![](img/0285f88bc840f313779e011725b623a5_45_0.png)

  **FIGURE 2.19** Optimized corners.

### Why?

Looking at Figure 2.19, you can count four four-sided polygons that were involved in the three right-angle turns the shape made. This makes for eight tris. Compare that with the seven four-sided polys that were there before (14 tris), and you can see how this sort of optimization can whittle down a polycount in a hurry. Ultimately there are some tradeoffs you have to make. It takes a bit of time to optimize, and if you're taking too much time out to optimize you're eating into your creation time. However, I find that if I do a bit of obvious optimizing as I go, it saves me from hours of painful optimization later.

- **Step 18:** Delete the polygons along the bottom. We don't see them, we don't need them, get rid of them.

  There is certainly some other optimization that can be done here, but we have looked at the basic techniques that are used to make a lean, mean mesh. Feel free to further optimize, but for now we'll move on.

- **Step 19:** Add the lip to the inside of the channel. Select the faces as shown in Figure 2.20 (the faces that are along the inside of the channel into the mountain), and use the Extrude tool to extrude them out just a small bit. This will create a new collection of faces along the dock top. Select these and extrude up to create the lip.

- **Step 20:** Duplicate and place the column roughly as shown in Figure 2.21. Yes, I realize it would be better to UV map the column first before duplicating it. And in fact, these columns we are placing now will undoubtedly be deleted and replaced by duplicates that are UV mapped. However, placing these here allows for some important placement of items in the upcoming steps.

in Unity. Or, create a plane for a wall that was completely invisible in Unity. Turning this on will give you a better idea of how things will appear in Unity.

## Roof Creation

- **Step 22:** Create a roof. Figure 2.22 shows a collection of cubes with one big plane across the top. The exact shape of this is unimportant, so don’t worry about that (although it’s safe to assume that the long vertical beams are paired 2×6s and the shorter horizontal ones are 2×4s). The importance of this is how we are going to optimize this form.

  ![](img/0285f88bc840f313779e011725b623a5_47_0.png)

  **FIGURE 2.22** *Untitled, document1.mb*

### Tips and Tricks

The roof shown in Figure 2.22 has a few additional extrusions (extruding edges instead of faces to get the outcropping bits), but to start with it was a single 1 Subdivision × 1 Subdivision plane. Working with planes (like the top of this roof unit) can be among the most efficient uses of polys available (a 1×1 subdivision plane is one—yes one—four-sided poly). However, remember that this one polygon has a front and a back. Since Backface Culling is turned on, quickly it will become apparent that the plane disappears if being viewed from the “wrong” side. Remember that we will be below this roof looking up, so make sure and either rotate the roof so its face is facing down, or use Polygons>Normals>Reverse to make sure the plane can be seen when the player is beneath it and looking up.

### Tips and Tricks

When working with something with regular repetitions like this roof has, use Maya’s Duplicate (Edit>Duplicate) and Duplicate With Transform (Edit>Duplicate With Transform). Create one cube. Ctrl-D will duplicate it, and if you move immediately in one move (with one click and drag) and press Shift-D, Maya will duplicate again, offsetting the new duplicate by the same amount as the last copy was moved. It’s a quick way to create lots of equally spaced copies.

## Handrails

- **Step 25:** Create handrails, optimize them into one mesh (Figure 2.23). Center the pivot, and name it `EntrywayHandrails`. Delete the history.

  ![](img/0285f88bc840f313779e011725b623a5_49_0.png)

  *FIGURE 2.23* Completed handrails.

### Tips and Tricks

If an element is optimized before duplicating (for instance deleting the top and bottom planes of the vertical posts of the handrails), it'll save the step later of selecting a big bunch of them later.

## Archway and Booleans

- **Step 26:** Create the start of the entry arch with a modified cube. Create a cube (Create>Polygons>Cube), then scale and position it similar to Figure 2.24. Select the top face, and using the Extrude tool, extrude and scale the top of the box (Figure 2.24).

  ![](img/0285f88bc840f313779e011725b623a5_49_1.png)

  *FIGURE 2.24* Beginning of entry arch.

### Why?

The idea for this next group of steps will be to use Maya's Boolean functions to create a form. Booleans work on the idea of subtracting (or adding or intersecting) two shapes. To make this work we have to have this block to subtract from. In the next step we will form the shape we wish to subtract from this block.

### Tips and Tricks

Notice that in Figure 2.24 the scaling that occurs after the plane is extruded only happens along the X axis. This makes sure that the front two polygons line up and make the Boolean to come a bit cleaner.

- **Step 27:** Create a cylinder with 60 (yes, 60) Axis Divisions. Do this one of two ways. Either create the cylinder (Create>Polygon Primitives>Cylinder), then in the Channel Box, select the polyCylinder node in the INPUTS section and change the Subdivision Axis entry there. Or, select Create>Polygon Primitives>Cylinder (Options) and in the Polygon Cylinder Options box, change the Axis Division entry to 60. Rotate and translate the cylinder to match Figure 2.25.

  ![](img/0285f88bc840f313779e011725b623a5_50_0.png)

  **FIGURE 2.25** Placed elements ready for Boolean function.

### Why?

“60 axis division?!” you cry incredulously, “all this talk of being efficient with our polycount and you make such a heavy primitive! What gives?” Yes, yes, 60 subdivisions is a lot, and it’s important to be very careful where to use such a heavy (high polycount) object. This is one of those places. The reason is that the curve across that archway is very large, and in fact at times in the game it may indeed cover the entire screen. When a curve spans such a large visual space, this is a good place to blow some of the polygon budget. When elements are small on screen—or never get much scrutiny in the course of game play—this is where to stay super stingy with polys. Note that although we started out with a 60-subdivision shape, we actually only used half of them, so there are only 30 subdivisions across the top of that arch.

### Warnings and Pitfalls

Although it is a bit difficult to see in the screenshot, that cylinder completely penetrates the altered cube and comes out the other side. For this Boolean function to work, the hole object (the cylinder) must be longer than the object it is being subtracted from.

- **Step 28:** Tweak the cylinder to make an arched entry (rather than a round tube). Press the space bar (to move into four-panel mode), then move the mouse over the Front View panel, and press the space bar again. This will make the Front View panel full screen. Switch to vertex mode (right-click the cylinder and select Vertex from the hotbox) and Marquee-select the vertices that make up the bottom half of the cylinder. Use the Translate tool to move them down below the bottom of the modified box (Figure 2.26).

- **Step 29:** Subtract the cylinder from the modified box. In Object Mode, select the box, then Shift-select the cylinder (the order of selection is important here). Choose Polygons>Mesh>Booleans>Difference. The result should be similar to Figure 2.27.
