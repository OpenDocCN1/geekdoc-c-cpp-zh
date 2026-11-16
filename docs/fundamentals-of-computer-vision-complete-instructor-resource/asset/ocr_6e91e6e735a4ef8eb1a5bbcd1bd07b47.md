![](bbox=[0.09, 0.12, 0.86, 0.34])

Figure 8.9 LEFT: The village of Appledore, North Devon, UK. The authors are grateful to Matthew Rowe, Irene Rowe, and David Rowe for this picture. Library Name: ColoredHouses-sm.jpg RIGHT: The three-dimensional RGB color space for the image on the left. Each point in the color space corresponds to a pixel in the image and is shown at coordinates, < r, g, b > with color < r, g, b >.

The student is advised (again) to take a course in pattern recognition to gain an understanding of this concept in more depth.

The k-means algorithm is presented in Figure 8.10:

Performance of color clustering has been compared to the problem Michelangelo would have had if he had been required to color the Sistine chapel with crayons. Figure 8.11 illustrates the results of using a small box of 10 crayons, a medium box of 24 crayons, and

+   1. In the 3D color space < r, g, b >, choose a set of k initial cluster centers. How you pick the initial cluster centers is problem-dependent. For example, if you are clustering points in a color space, where the dimensions are red, green, and blue, you might scatter all your cluster centers uniformly over this 3-space, or you might put all of them along the line from <0,0,0> to <maxred, maxgreen, maxblue>.
+   2. Assign each pixel in the image as belonging to the closest cluster center. That is, for the pixel at < x, y >, whose color is < r, g, b >, compute the distance to cluster mean i whose color is ri gi bi, using
+      d_i,x,y = sqrt((r - ri)^2 + (g - gi)^2 + (b - bi)^2). (8.18)
+      The pixel at < x, y > is said to "belong" to cluster i if d_i,x,y < d_j,x,y for any cluster j, j != i.
+   3. Compute the mean of each cluster, that is, the color that is the average of all the colors in that cluster. This becomes the new center of that cluster.
+   4. Reassign each pixel to the cluster with the nearest mean.
+   5. If nothing has changed in this iteration, exit; otherwise go back to step 2.

Figure 8.10 K-means clustering of colors.