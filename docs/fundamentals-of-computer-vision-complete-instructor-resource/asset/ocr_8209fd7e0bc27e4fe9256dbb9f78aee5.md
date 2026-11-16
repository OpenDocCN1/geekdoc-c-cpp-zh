1 1 1   2 2
1 1 1   2 2
1 1 1   2 2
1 1 1   2 2
1 1 1 1 1 ?

Figure 8.18 Ambiguity in label assignment.

+   2. If the two pixels have similar brightnesses, they will be considered “equivalent.” If the pixel above and the pixel to the left are already labeled, with identical labels, then label pixel i with that label also.

+   3. If both the pixel above and the pixel to the left are already labeled and the labels are different, it will be necessary to resolve this. Figure 8.18 demonstrates the situation that can arise as result of this comparison when the equivalence relation R(1, 2) is discovered at the pixel designated by the question mark.

Labeling conflicts are resolved in the following way. Suppose we discover that a new pixel, could be labeled either r or s. Without loss of generality, we assume r < s. Then for every element of M with label r, replace its label with s. In this way, the equivalence label for every equivalence will be the same, which really says that all the pixels labeled with r or s are in the same region.

This algorithm above is potentially very fast, since the relabeling in Step 3 can be accomplished in a single step, using a content-addressable memory [8.48].

# 8.4.3 An Example Application

Figure 8.19 illustrates a range image from the Microsoft Kinect® camera, demonstrating artifacts from the camera. These artifacts are small regions with brightness of zero. Running connected component labels on the image produces a label image in which each region

![](bbox=[0.09, 0.66, 0.88, 0.86])

Figure 8.19 LEFT: A range image with artifacts. Library name: d_box1.png. RIGHT: The label image after assigning a different label to each artifact and then assigning random pseudocolors to the labels.