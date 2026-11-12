**Step 21:** Adjust the new polygons in 3D space. Change to vertex mode. In the side- and persp-view panels, select and move collections (often pairs) of vertices **only in Z** so that they move back to the appropriate place on the eyeball (Figure 8.9).

**FIGURE 8.9** Adjusting vertices around the eyeball.

![](bbox=[0.334, 0.161, 0.834, 0.386])

**Step 22:** Provide thickness to the eyelid. Once the general shape of the eye is complete, change to edge mode and double-click an edge of the inside of the ring of polygons (this will select the ring). Choose the Extrude tool (Polygons>Edit Mesh>Extrude), and then immediately swap to the Move tool. Move this newly extruded edge back into the eyeball along the Z-axis (Figure 8.10).

**FIGURE 8.10** Providing eyelid with thickness

![](bbox=[0.334, 0.476, 0.834, 0.709])

# **Why?**

Every time the Extrude tool is selected it extrudes a new collection of polygons. If the Extrude tool's manipulators are used, the new polygons are moved, scaled, or rotated along the polygons' normals. But swapping to the Move tool allows this new collection of polygons (or edges) to be manipulated *en masse* along a global direction (in this case Z).