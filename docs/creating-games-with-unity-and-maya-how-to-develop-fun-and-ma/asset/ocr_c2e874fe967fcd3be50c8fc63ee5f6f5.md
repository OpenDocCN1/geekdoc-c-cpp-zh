![](bbox=[0.19, 0.11, 0.66, 0.34])

FIGURE 8.19 Cleaning up mirror plane.

**Step 34:** As the two shapes get close to each other, snap vertices to match. While in vertex mode, holding down the V-key when moving a vertex will allow it to be snapped to another vertex (Figure 8.20).

FIGURE 8.20 Building toward the two meshes and snapping when close.

![](bbox=[0.05, 0.46, 0.92, 0.66])

# Mask and Mouth Together

**Step 35:** Combine the mouth to the mask. In object mode select the mask and then Shift-select the mouth. Choose Polygons>Mesh>Combine.

# Why?

Ultimately, most of this character (except for the weapons) will be one single mesh. Although Maya and Unity will both support multiple meshes skinned to one joint structure, it is quicker computationally to have fewer meshes being deformed at one time. So for efficiency's sake, and because our faces are a single mesh, it will be important to have the mask and mouth be one mesh. Combine does this.

**Step 36:** Merge appropriate vertices. Select the vertices that are at the seam where the two meshes combined. (Marquee select) and choose Polygons>Edit Mesh>Merge.