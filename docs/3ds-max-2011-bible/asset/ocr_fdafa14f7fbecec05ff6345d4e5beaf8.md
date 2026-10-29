# Part IX: Working with Characters

character appear blue, and all the matching vertices appear green. All vertices that cannot be matched appear red.

If you drag over bones or vertices in the viewports, you can select them. Clicking the Mirror Paste button pastes the envelopes and vertex weights of the selected vertices to their matches. Or you can select the Paste Green to Blue Bones button or one of its neighbors to copy all the green bones or vertices to their matches, or vice versa.

The Display Projection drop-down list projects the position of the selected vertices onto the Mirror Plane so you can compare their locations relative to each other. With lots of vertices in your skin, you want to enable the Manual Update, or the viewport refreshes become slow.

# Tutorial: Mirroring skin weights

Now that you have spent the time correcting the skin weights for the left boot, you use the Mirror Weights feature to apply the same weights to the opposite foot.

To apply the skin weights to a character, follow these steps:

+   1. Open the Future man with corrected weights - final.max file from the Chap 40 directory on the DVD.
+   2. With envelope mode turned on, click the Mirror Mode button in the Mirror Parameters rollout. An orange gizmo is added to the viewport that divides the model, as shown in Figure 40.8.
+   3. Drag over all the vertices that make up the left boot, and then click the Paste Blue to Green Verts button. All the vertex weights on the left side of the model are copied to the right side. The pasted vertices turn yellow once pasted.

# FIGURE 40.8

In Mirror mode, matched bones and vertices appear green and blue.

![](bbox=[0.2, 0.86, 0.92, 0.98])