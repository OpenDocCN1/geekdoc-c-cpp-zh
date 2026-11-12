
- **Step 21:** Adjust the new polygons in 3D space. Change to vertex mode. In the side- and persp-view panels, select and move collections (often pairs) of vertices **only in Z** so that they move back to the appropriate place on the eyeball (Figure 8.9).

**FIGURE 8.9** Adjusting vertices around the eyeball.

![](img/0285f88bc840f313779e011725b623a5_209_0.png)

- **Step 22:** Provide thickness to the eyelid. Once the general shape of the eye is complete, change to edge mode and double-click an edge of the inside of the ring of polygons (this will select the ring). Choose the Extrude tool (Polygons>Edit Mesh>Extrude), and then immediately swap to the Move tool. Move this newly extruded edge back into the eyeball along the Z-axis (Figure 8.10).

**FIGURE 8.10** Providing eyelid with thickness

![](img/0285f88bc840f313779e011725b623a5_209_1.png)

### Why?

Every time the Extrude tool is selected it extrudes a new collection of polygons. If the Extrude tool's manipulators are used, the new polygons are moved, scaled, or rotated along the polygons' normals. But swapping to the Move tool allows this new collection of polygons (or edges) to be manipulated *en masse* along a global direction (in this case Z).

- **Step 23:** Mirror the mesh. Swap to object mode and select the face thus far. Select Edit>Duplicate Special (Options). In the Duplicate Special Options window choose Edit>Reset Settings. Change the Geometry Type to Instance. Change the Scale X input setting (the first column of Scale) to –1. Click the Duplicate Special button to finish the mirroring of the geometry (Figure 8.11).

![](img/0285f88bc840f313779e011725b623a5_210_0.png)

### Why?

Scaling an object –1 in any direction will create a mirror version of the object. By making sure this duplicate is an instance, we ensure that as one side of the face is built up, this duplicate will also update. Now this –1 scaled half of the character will not be the one imported into Unity (the normals are funky), but as a construction method, this works well to see the whole face rather than just one half at a time.

## Expanding Rings

- **Step 24:** Expand the rings. Change to edge mode and double-click one of the outer edges (this should select the outer ring of edges). Choose the Extrude tool and then immediately swap to the Scale tool and scale (by dragging on the middle cube manipulator handle) this new collection of edges out in every direction (Figure 8.12).

![](img/0285f88bc840f313779e011725b623a5_210_1.png)

### Why?

Keep extruding until there is a Phantom of the Opera-esque mask complete. Do not worry about the mass at the end of the nose.

## The Mouth

- **Step 28:** Repeat steps 15 to 27 to create the mouth. Again, the flow is to create a new polygon, then extrude the edges around. The biggest difference here is that instead of creating a complete ring, create a half ring (Figure 8.15).

FIGURE 8.15 First pass of the mouth

![](img/0285f88bc840f313779e011725b623a5_212_0.png)

- **Step 29:** Create an oral cavity. Do this by selecting the edges on the inside of the mouth and extruding back into the head. Finally take the very last collection of vertices and snap them to the center (hold X while using the Move tool). Marquee select these vertices and choose Polygons>Edit Mesh>Merge (Figure 8.16).

![](img/0285f88bc840f313779e011725b623a5_212_1.png)

FIGURE 8.16 Oral cavity creation.

### Why?

The oral cavity may not even be needed. If the game will never show the character with his mouth open then there is no need to blow this chunk of the poly budget here. However, since this is the main protagonist, including an oral cavity will allow for future possibilities. Still, it is the inside of the mouth, so no need to use any more polygons here than needed.

- **Step 30:** Add geometry as needed to finish lips. Figure 8.17 shows a new ring of edges created with the Insert Edge Loop Tool (Polygons>Edit Mesh>Insert Edge Loop Tool). Don't bury too many polygons here, but an extra ring can help with the lips volume.

![](img/0285f88bc840f313779e011725b623a5_213_0.png)

**FIGURE 8.17** Rounded lips via additional edge ring.

- **Step 31:** Extrude the outer ring to build up toward the upper face (Figure 8.18). Use the Extrude tool's move handles instead of the Scale tool. Since we are dealing with half the mouth, using the edge's normals gives a better result.

![](img/0285f88bc840f313779e011725b623a5_213_1.png)

**FIGURE 8.18** Extruding the outer ring to build geometry.

- **Step 32:** Periodically clean the mirror plane. Select the vertices that should be on the mirror plane and snap to the center (hold X down while moving in X). Figure 8.19 shows a quick cleanup of current progress.

- **Step 33:** Continue building out (and up) toward the mask.

![](img/0285f88bc840f313779e011725b623a5_214_0.png)

FIGURE 8.19 Cleaning up mirror plane.

- **Step 34:** As the two shapes get close to each other, snap vertices to match. While in vertex mode, holding down the V-key when moving a vertex will allow it to be snapped to another vertex (Figure 8.20).

FIGURE 8.20 Building toward the two meshes and snapping when close.

![](img/0285f88bc840f313779e011725b623a5_214_1.png)

## Mask and Mouth Together

- **Step 35:** Combine the mouth to the mask. In object mode select the mask and then Shift-select the mouth. Choose Polygons>Mesh>Combine.

### Why?

Ultimately, most of this character (except for the weapons) will be one single mesh. Although Maya and Unity will both support multiple meshes skinned to one joint structure, it is quicker computationally to have fewer meshes being deformed at one time. So for efficiency's sake, and because our faces are a single mesh, it will be important to have the mask and mouth be one mesh. Combine does this.

- **Step 36:** Merge appropriate vertices. Select the vertices that are at the seam where the two meshes combined. (Marquee select) and choose Polygons>Edit Mesh>Merge.

### Why?

Just because two meshes are combined so that it appears as though they are one mesh, that doesn't mean that the appropriate vertices are merged. And, in fact, if vertices are not manually merged, they remain separate after the Combine has happened. Manually merging makes sure that the seam is using shared vertices and not just lined-up ones.

- **Step 37:** Along the mouth, extrude out further rings to continue connecting to the lower edge of what was once the mask (Figure 8.21). Be sure to merge relevant vertices to connect new polys to one solid mesh.

- **Step 38:** Soften Normals. In object mode, select the mesh and choose Polygons>Normals>Soften Edge (Figure 8.22).

![](img/0285f88bc840f313779e011725b623a5_215_0.png)

![](img/0285f88bc840f313779e011725b623a5_215_1.png)

FIGURE 8.21 Extruding out to continue connecting the mouth to the bottom of what was the mask.

FIGURE 8.22 Results after softening normals.

### Why?

As new polygons are built, the normals of those edges and faces are still hard, which can give the mesh a very 1980s 3D look. By softening the edge, the low-poly version of the model can look surprisingly smooth and much more complex than the underlying polygons alone.

- **Step 39:** In object mode choose Edit>Duplicate Special (with X = –1). Make sure the center vertices are centered first.

### Why?

Along the process of combining, the old duplicate of the mask will have been lost. By mirroring again (via Duplicate Special), once again the shape of the face will be easier to see.

## Nose

- **Step 40:** Close the centermost gap with the Append to Polygon tool (Figure 8.23).

- **Step 41:** Create additional places to round the nose with additional polygons. Create these with the Insert Edge Loop tool (Figure 8.24).

![](img/0285f88bc840f313779e011725b623a5_216_0.png)

**FIGURE 8.23** Beginning to add mass to the nose. Start with creating a new poly with the Append to Polygon tool.

![](img/0285f88bc840f313779e011725b623a5_216_1.png)

**FIGURE 8.24** Adding geometry to the nose to allow for rounding of the form.

- **Step 42:** Bend the new vertices to find the form of the nose. Be sure to use all the view panels to find this form (Figure 8.25).

![](img/0285f88bc840f313779e011725b623a5_216_2.png)

**FIGURE 8.25** Roughing out the tip of the nose.

- **Step 43:** Create the upper edge of nostril. Select a pair of edges where the nostril would be and extrude them around to create the rough outline of the nostril (Figure 8.26).
