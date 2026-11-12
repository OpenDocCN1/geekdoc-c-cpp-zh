
## Tips and Tricks

These manipulator handles are important since they will allow us to refine the projection to closely match the shape of the polygons being mapped. Sometimes though, if a click goes awry, the handles can disappear. If this happens and they disappear, do the following. First, change to object mode and select the mesh. Next, open the Channel Box and look for a node (in the INPUTS section) called polyCylProj1 (or some other number). Select this node, and then choose the Show Manipulator tool (the ninth tool down in the toolbox, just beneath the Soft Selection tool).

- **Step 12:** Expand the projection so it completely surrounds the arm. Do this by dragging the red rectangles that are at either end of the line that is at the cylinder’s equator (Figure 9.8). Make sure they touch.

![](img/0285f88bc840f313779e011725b623a5_262_0.png)

**FIGURE 9.8** Expanding the coverage of the cylindrical projection.

### Why?

This is an important step because it makes it so the texture does not repeat (it was using the texture once for the front of the arm and once for the back, which meant two seams). Now, the texture will wrap completely around the arm with no repeating, and leave us with one seam (currently across the back of the arm).

- **Step 13:** Rotate the seam to the inside of the arm. The center circle of the projection manipulator is a handle itself. Click-drag this handle to rotate the seam (where the two red rectangle handles meet) to the inside of the arm (Figure 9.9).

**FIGURE 9.9** Rotating the seam to the inside of the arm.

![](img/0285f88bc840f313779e011725b623a5_263_0.png)

### Why?

Of constant concern to the artist tasked with UV mapping should be where to hide the seams. Hiding the seam across the back of a character might seem like a good idea at first until the game becomes third person and suddenly all we see is the back of the character. A much smarter place to hide seams for things like legs and arms are where the seam is tucked between two surfaces. It turns out that the inside of the arm and leg also have natural seams since that's where the fabric of shirts and pants are often sewn together.

- **Step 14:** Rotate the projection to match the rotation of the arm. At the bottom edge of the projection cylinder is a little red T (Figure 9.10, left). Clicking this T will reveal a new set of manipulation handles (Figure 9.10, right) that allows the projection to be moved, scaled, or rotated. Use the rotation handles to rotate the projection to more closely match the angle of the collection of polygons being mapped.

### Tips and Tricks

Getting back to the first set of manipulation handles can be done by clicking the little red T again.

![](img/0285f88bc840f313779e011725b623a5_264_0.png)

**FIGURE 9.10** Rotating cylindrical projection to match rotation of the arm.

- **Step 15:** Press 6 on the keyboard to see how the checkers are falling into place (Figure 9.11).

![](img/0285f88bc840f313779e011725b623a5_264_1.png)

**FIGURE 9.11** Checkers showing well-distributed texture.

- **Step 16:** Adjust the scale if needed to eliminate most distortions in the checkers.

- **Step 17:** Move this new shell to the side in the UV Texture Editor. Open the UV Texture Editor and this projection should still have its handles visible there. Grab the manipulator handles by either the yellow circle in the middle or the red triangle handle and move this projection (and its shell) away from the mass of other UVs (Figure 9.12).

### Why?

Yes, this shell is much too big—it's taking up the size that the entire form will eventually take up. That's OK. Right now the shells should be big enough to easily illustrate the size of the checkerboard pattern so we can see relative sizes. Later the shells will be scaled and arranged.

**FIGURE 9.12** Sequestering the newly created shell.

![](img/0285f88bc840f313779e011725b623a5_265_0.png)

- **Step 18:** Use the Smooth UV tool to unfold the new shell. In the UV Texture Editor right-click-hold and select UV from the hotbox (to tell Maya you want to deal with UVs now). Marquee select this new shell. Activate the Smooth UV tool in the top-left corner of the UV Texture Editor (Figure 9.13). This will show two little buttons at the bottom left corner of the shell called Unfold and Relax. Drag the Unfold button left and right to see the shell relax. Be sure to watch the view panel as well to see the checker pattern relax into better proportions.

**FIGURE 9.13** Using the UV Smooth tool to relax a shell.

![](img/0285f88bc840f313779e011725b623a5_265_1.png)

- **Step 19:** Repeat process for the other arm.

- **Step 20:** Repeat this technique for each of the legs (Figure 9.14). Project one leg at a time and come all the way up to the bottom of the belt pouches. Note that there will be several shells created through this process. Be sure to use the UV Smooth tool to unfold each individually.

![](img/0285f88bc840f313779e011725b623a5_266_0.png)

**FIGURE 9.14** Cylindrical mapping the legs.

### Tips and Tricks

Inevitably after making a projection you will discover that the projection didn't cover enough polygons or you ended up grabbing polys you didn't need. No worries. If a polygon is missing, just make the selection again and create another mapping. If you grabbed too many, just move the extras aside and pick them up in further mapping functions.

## Sewing Up Certain Seams

Among the shells are two separate shells for the fly (crotch) area. While there usually is a seam that runs along the side of the zipper and then down through the middle of the crotch, getting the zipper flap to look right when the two shells are separate as they are can be quite difficult.

This can be an issue for the butt area and various other places as UV mapping occurs. The fly area just provides a quick and easy example of how projected shells can (and should) be combined to assist in later texture painting.

- **Step 21:** Find the edges where the fly is split. In the persp view panel, select a few of the edges along the seam. Take a look in the UV Texture Editor to find out what these edges are (Figure 9.15).

**FIGURE 9.15** Tracking down which edges in 3D are represented in the UV Texture Editor.

![](img/0285f88bc840f313779e011725b623a5_267_0.png)

- **Step 22:** Find matching-sized shells and remove faces that offset the balance of the new combined crotch. The steps ahead work easiest if there are no flaps of polygons hanging off of a shell (your particular UV layout may be different). In the UV Texture Editor, begin selecting down the fly on either shell until the end is reached of the smaller of the two shells. Select the edges along the end of that desired shell (where it connects to the unwanted flap) and choose Polygons>Cut UV Edges. Then, select a UV on the chunk of the shell to remove. Ctrl-right-click-hold and select To Shell, and then use the Move tool to move this new shell away (Figure 9.16).

**FIGURE 9.16** Finding and creating two shells that will share a common edge without additional flaps.

![](img/0285f88bc840f313779e011725b623a5_267_1.png)

### Why?

Remember that the idea here is that mapping the crotch will be much easier if things like the fly area are one shell. Your particular situation may vary, but in step 22, we're looking at getting rid of flaps of stuff that will make combining the crotch and then preparing the shells combine to finish the crotch.

**FIGURE 9.19** Pouch to map.

![](img/0285f88bc840f313779e011725b623a5_269_0.png)

- **Step 27:** Map the pouch. Choose Create UVs>Automatic Mapping (Options). Make sure the Planes setting is set to 6. Press Project. In the UV Texture Editor the faces that have just been mapped will be highlighted in salmon. Before selecting anything else, in the UV Texture Editor right-click-hold and choose UV. Immediately Marquee select all the faces that are in that top-right quadrant. At this point, all the other faces will show up in that space, but if the Move tool is immediately used, the UVs for the pouch can be moved off to the side (Figure 9.20).

**FIGURE 9.20** Initial projection on the pouch.

![](img/0285f88bc840f313779e011725b623a5_269_1.png)

- **Step 28:** Sew it up. Figure 9.21 shows the pouch sewn up. The process was the same as sewing up the pillow back in the set design: select an edge on the outside of a shell (which will select an edge elsewhere on another shell), check in the 3D view if these edges should be sewn together, then use Polygons>Move and Sew UVs. Repeat until the pouch is assembled.

### Why?

Note that there are two shells here—one is the pouch and the second is the clasp. Since the clasp is another type of material, it's an easy place to leave a seam. If this shell were to be sewn onto the larger shell, the results would be a very distorted shell.
